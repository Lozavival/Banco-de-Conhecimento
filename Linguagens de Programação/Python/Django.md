# Criação de Sites com Django

**Palavras-chave:** #python, #python-impressionador, #framework, #web

Segundo a própria documentação, "Django é um framework web de Python de alto nível que permite o rápido desenvolvimento de sites seguros e de fácil manutenção".

---

## Pré-requisitos

1. [Classes e Orientação a Objetos](Orientação%20a%20Objetos.md)
2. [Ambientes Virtuais](Ambientes%20Virtuais.md)

## Planejamento do Site

É muito importante, antes de tudo, idealizar e definir a estrutura do site, para orientar e servir de guia durante sua criação. Caso, ao longo do desenvolvimento, sejam necessárias alterações no planejamento, podemos alterá-lo, mas esse passo inicial reduz essa possibilidade, pois já sabemos de antemão o que queremos fazer.

Nesse momento, podemos nos utilizar, por exemplo, de esboços/rascunhos para as nossas páginas e estruturas de tópicos para os nossos modelos, bem como listar (com o maior detalhamento possível) as funcionalidades que desejamos, para termos uma referência do que devemos construir.

É importante dar especial atenção aos modelos, para evitar que, futuramente, sejam necessárias mudanças significativas no banco de dados (para se adicionar ou remover atributos, por exemplo), visto que as páginas podem ser alteradas com maior impunidade ao andamento do projeto como um todo. Especialmente, dê atenção ao modelo dos usuários, pois qualquer alteração futura (ao longo do desenvolvimento) requer exclusão e recriação do banco de dados.

## Estrutura Inicial do Django

Aqui estão listados os comandos básicos e passos iniciais para se criar um projeto no Django. Para saber todos os comandos existentes com `django-admin` e `manage.py`, acesse a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/django-admin/).

### Instalação do Django

Após criar e ativar um ambiente virtual, é preciso instalar o django utilizando o pip:

```bash
pip install django
```

### Criação do Projeto

O primeiro passo para a criação de todo site é iniciar o projeto do django:

```bash
django-admin startproject [nome-do-projeto] [caminho-para-o-projeto]
```

Quando criamos um projeto, é automaticamente criado também um banco de dados sqlite.

### Criação de um Aplicativo

Aplicativos são utilizados para separar funcionalidades totalmente diferentes de um mesmo projeto. As páginas e os modelos serão definidos no aplicativo, e cada aplicativo é vinculado ao projeto.

Para criar um aplicativo, devemos rodar o seguinte comando:

```bash
django-admin startapp [nome-do-app] [caminho-para-o-app]
```

### Migrações

Ao iniciar um novo projeto e sempre que fizermos qualquer alteração na estrutura do banco de dados (ou seja, alterarmos algum modelo), é necessário fazer uma migração para atualizá-lo.

```bash
python manage.py makemigrations
python manage.py migrate
```

Para que a migração tenha efeito, é importante que o servidor esteja pausado ao aplicá-la.

### Criação do SuperUsuário

Para que tenhamos acesso às funções administrativas do site, é necessário criar um superusuário. Esse processo só precisa ser feito uma vez, no início do projeto.

```bash
python manage.py createsuperuser
```

Em seguida, será necessário inserir no terminal as seguintes informações: nome de usuário, email, senha e confirmação de senha. Encerrado esse processo, o superusuário será criado.

### Conexão de um App ao Projeto

Após criar um novo aplicativo, devemos conectá-lo ao nosso projeto. Para isso, devemos executar os seguintes passos:

1. No arquivo `[nome-do-projeto]/settings.py`, acrescentar o aplicativo à lista de `INSTALLED_APPS`, como no exemplo abaixo.

    ```python
    INSTALLED_APPS = [
        ...,    # outros aplicativos
        'nome-do-novo-aplicativo'
    ]
    ```

2. Em seguida, devemos definir, na variável `urlpatterns` do arquivo `[nome-do-projeto]/urls.py`, o link no qual será exibido o novo aplicativo. Para isso, podemos adicionar todos os links do projeto a essa lista ou criar um arquivo `urls.py` dentro de cada aplicativo e apenas referenciar os arquivos de cada app no arquivo do projeto. Será adotada a segunda abordagem.
    1. Em primeiro lugar, devemos criar, dentro da pasta do novo aplicativo, um arquivo chamado `urls.py`.
    2. No arquivo `[nome-do-projeto]/urls.py`, importar a função `include()` e adicionar os URLs a `urlpatterns`, seguindo o exemplo:

        ```python
        from django.urls import include, path

        urlpatterns = [
            ...,    # outros URLs
            path('link-desejado/', include('[nome-do-aplicativo].urls'))
        ]
        ```

    3. Por fim, devemos configurar os links no arquivo `urls.py` do novo aplicativo, conforme descrito em [[#Configuração dos links]].

### Execução do site

Para rodar o site, devemos executar o seguinte comando:

```bash
python manage.py runserver
```

Isso criará, no terminal, um URL (via endereço de IP) que pode ser acessado no navegador para visualização do site.

### Pastas Static e Media

Imagens estáticas são imagens criadas pelo construtor do site (logos, imagens de fundo etc.), enquanto imagens de mídia são imagens enviadas pelos usuários (por exemplo, fotos postadas no Instagram). Para que esses arquivos possam ser armazenados, é necessário criar duas pastas: "static" e "media".

A pasta "static" é utilizada para armazenar os arquivos estático (edições visuais das páginas do site, podendo ser arquivos CSS, JavaScript ou imagens). No arquivo `[nome-do-projeto]/settings.py` é necessário que as seguintes variáveis estejam definidas:

```python
STATIC_URL = 'static/'

STATICFILES_DIRS = [
    BASE_DIR / "static"
]
```

Não é necessário que a pasta "static" esteja localizada na raiz do projeto. Nesse caso, basta adicionar o caminho relativo nas variáveis acima.

Feito isso, é necessário ainda adicionar um link para as imagens no arquivo `[nome-do-projeto]/urls.py`. Para isso, precisamos importar as variáveis utilizadas e incluí-las na lista de `urlpatterns`, como mostrado abaixo:

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

O processo de criação e configuração da pasta "media" é análogo ao da pasta "static". Após criar a pasta na raiz do projeto (ou em alguma outra pasta de escolha), devemos definir as seguintes variáveis no arquivo `[nome-do-projeto]/settings.py`:

```python
MEDIA_URL = 'media/'

MEDIA_ROOT = BASE_DIR / "media"
```

Por fim, devemos novamente adicionar um link para as imagens no arquivo `[nome-do-projeto]/urls.py`, como mostrado abaixo:

```python
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

Concluído esse procedimento, o site já é capaz de armazenar arquivos estáticos e mídias enviadas pelo usuário.

## Configuração de um Aplicativo

### Modelos

#### Criação do Modelo

A criação de modelos, ou seja, a adição de tabelas ao banco de dados é feita no arquivo `models.py` do respectivo aplicativo. Não esqueça que, após uma alteração nos models, é necessário fazer uma [migração](#migrações) do banco de dados.

Cada tabela do banco de dados, ou seja, cada objeto, será uma classe do Python que herda a classe `models.Model` do módulo `django.db`. Dentro dessa classe, devemos apenas criar os campos (atributos) que queremos para determinado objeto, definindo o tipo de dado que cada campo armazenará.

Para ver os tipos de campos disponíveis e sua descrição, bem como seus parâmetros obrigatórios, consulte a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/models/fields/#field-types).  
Para ver os argumentos opcionais disponíveis para todos os tipos de campos, consulte a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/models/fields/#field-options).  
**Importante:** para utilizar o campo `ImageField`, é necessário instalar a biblioteca Pillow (basta executar o comando `pip install pillow`).

Confira abaixo o exemplo da criação de um modelo de filmes:

```python
from django.db import models
from django.utils import timezone

LISTA_CATEGORIAS = (
    ("DRAMA", "Drama"),
    ("COMEDIA", "Comédia"),
    ("ACAO", "Ação"),
    ("TERROR", "Terror")
)

class Filme(models.Model):
    titulo = models.CharField(max_length=100)
    descricao = models.TextField(max_length=1000)
    thumb = models.ImageField(upload_to='thumb_filmes')  # upload_to = nome da pasta em que a imagem será armazenada
    categoria = models.CharField(max_length=15, choices=LISTA_CATEGORIAS)
    visualizacoes = models.IntegerField(default=0)
    data_estreia = models.DateField()
    data_adicao = models.DateTimeField(default=timezone.now)
```

- Recomenda-se sempre criar o nome de um modelo no singular, pois o django automaticamente adiciona um "s" ao final na visualização de administrador.

#### Registro do Modelo

Após a criação do novo modelo no arquivo `models.py`, é necessário ainda registrá-lo no arquivo `admin.py` para que ele seja acessível pelo código (até o momento, apenas criamos a tabela no banco de dados). Para isso, devemos importar a classe e registrá-la no administrador do site.

Note que, como nesse passo não é realizada nenhuma mudança no banco de dados, não é necessário fazer uma migração.

Seguindo o exemplo de um modelo de filme, devemos registrá-lo no arquivo `admin.py` da seguinte forma:

```python
from django.contrib import admin
from .models import Filme

admin.site.register(Filme)
```

A partir desse ponto, já é possível adicionar novos objetos daquela classe, ou seja, novas entradas no banco de dados.

#### \_\_str\_\_

Para configurar como cada entrada será representada na lista de objetos da tela de administrador, devemos definir a função `__str__` da classe.

Por exemplo, caso desejássemos que fosse exibido o título de cada filme, poderíamos, no exemplo anterior, definir a classe da seguinte forma:

```python
class Filme(models.Model):
    ...    # definição dos campos

    def __str__(self):
        return self.titulo
```

Como isso não altera a estrutura do banco de dados, não é necessário efetuar uma migração.

#### Chave Estrangeira

Uma chave estrangeira é uma relação do tipo muitos-para-um, ou seja, é um campo utilizado para relacionar dois modelos. Para mais informações, acesse a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/models/fields/#foreignkey).

Recomenda-se que a chave estrangeira seja o primeiro campo a ser criado quando se define um novo modelo, para evitar modificações futuras (a nova tabela já é conectada à outra desde sua criação).

Para criar um campo do tipo Chave Estrangeira, precisamos passar três parâmetros>

- o modelo com o qual será feita a relação, que deve receber uma string contendo o nome da classe que representa tal modelo;
- `related_name`: campo a ser "criado" no modelo "original" para que possamos acessar (no [contexto](#contextos)) todos os objetos do novo modelo relacionados a ele;
- `on_delete`: qual comportamento de uma constraint SQL deve ser emulado quando o objeto referenciado na Chave Estrangeira é deletado.

Por exemplo, caso desejemos criar um aplicativo de séries, precisaremos criar os modelos de série e episódio, e é trivial perceber que cada episódio só pode estar relacionado a uma única série, porém cada série pode possuir vários episódios. Assim, utilizamos uma Chave Estrangeira para representar tal relação:

```python
class Serie(models.Model):
    ...

class Episodio(models.Model):
    serie = models.ForeignKey("Serie", related_name='episodios', on_delete=models.CASCADE)
```

No exemplo acima, podemos acessar todos os episódios de uma série em um arquivo HTML pela tag `{{ serie.episodios.all }}`, por exemplo, e, se a série for deletada, todos os episódios também serão excluídos do banco de dados.

### Páginas

Para criar uma página do site, é necessário configurar três coisas: o *URL* (link onde a página aparecerá), a *view* (o que acontece quando acessar a página) e o *template* (parte visual que será exibida, ou seja, os arquivos HTML).

#### Configuração das URLs

A configuração das URLs do aplicativo ocorre de forma muito similar à do projeto como um todo. No arquivo `urls.py` presente na pasta do aplicativo, vamos criar uma variável `urlpatterns` e nela configurar os links do site:

```python
from django.urls import path
from .views import view, MyView

urlpatterns = [
    path('padrão-da-url/', view),  # FBV
    path('padrão-da-url/', MyView.as_view())  # CBV
]
```

#### Views

As views podem ser definidas de duas formas: Function Based Views (FBV), na qual criamos uma função para representar a view, e Class Based Views (CBV), na qual a view é representada por uma classe.

Uma das vantagens da FBV é sua facilidade de implementação, principalmente para projetos menores ou páginas com funcionalidades reduzidas (por exemplo, caso desejemos uma página estática que apenas exibe informações pré-determinadas na tela, a implementação de FBV é muito mais direta). Por outro lado, como a CBV funciona baseada na herança de classes já implementada pelo framework, muitas funcionalidades já vêm prontas para uso, o que é uma vantagem da CBV em comparação com a FBV, na qual devemos implementar manualmente na função tudo o que desejamos.

##### Function Based Views

Por padrão, toda função de view recebe um parâmetro *request* (que indica se é uma requisição do tipo GET, POST etc.) e deve retornar a chamada da função *render*, que recebe como parâmetros o request e o nome do template a ser utilizado.

A estrutura básica que deve estar presente no arquivo `views.py` é a seguinte:

```python
from django.shortcuts import render

def view(request):
    return render(request, "template.html")
```

##### Class Based Views

Para construir uma classe que representa uma view, devemos obrigatoriamente herdar alguma classe padrão do Django. A lista de todas as classes disponíveis pode ser lida na [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/class-based-views/).

```python
from .models import MyModel
from django.views.generic import TemplateView, ListView

class MyView(TempleteView):
    template_name = template1.html

class MyObjects(ListView):
    template_name = template2.html
    model = MyModel
    # nesse caso, a variável passada no context é sempre chamada de "object_lust"
```

##### Passagem de Parâmetros para as Views

O DetailView, por exemplo, cria uma página diferente para cada objeto. Sendo assim, é necessário fazer alterações à configuração do URL:

```python
from django.urls import path
from .views import MyDetailView

urlpatterns = [
    path('padrão-da-url/<int:pk>', MyDetailView.as_view() )
]
```

Os sinais `<>` indicam a presença de uma variável dentro do URL. Dentro deles, é preciso passar a informação a ser exibida no seguinte formato: `<tipo-da-variável:variável>`. No exemplo acima, "pk" significa "primary key", ou seja, o id do item no banco de dados.

#### Templates

No arquivo `settings.py` (presente no diretório do projeto), dentro da variável `TEMPLATES`, podemos configurar duas opções para armazenar os [arquivos HTML](#configuração-das-páginas-html), contendo os templates a serem usados no site:

- Se a opção `APP_DIRS` estiver com o valor `True`, podemos armazenar os arquivos em uma parta chamada `templates`, que deve ser criada dentro do diretório do aplicativo.
    - Recomenda-se utilizar essa alternativa para criar páginas específicas para cada view daquele aplicativo.
- Dentro da opção `DIRS`, podemos adicionar uma (ou mais) pastas, e armazenar os templates nas pastas configuradas.
    - Recomenda-se criar essa pasta na raiz do projeto e utilizá-la para armazenar configurações que afetem/estejam presentes em todas as páginas do site (fonte, barra de navegação, rodapé etc.).

## Configuração das Páginas HTML

***Nota:*** ao longo desta seção, a palavra "template" será utilizada com seu significado cotidiano (ou seja, "padrão", "base"), e não como referência ao elemento *template* do django.

### Blocos Dinâmicas

O Django permite a inclusão de blocos dinâmicas nos arquivos em HTML, isto é, tags cujo valor pode ser alterado nas páginas sem ser necessário alterar o arquivo original em si. Isso permite a criação de templates para as páginas, pois podemos mesclar trechos estáticos e dinâmicos, evitando a necessidade de repetição de código nos diferentes arquivos HTML utilizados no site.

Para isso, devemos adicionar a estrutura de bloco no arquivo contendo o template, dentro da tag que desejamos alterar dinamicamente:

```html
<tag>
    {% block nome-do-bloco %}
    {% endblock %}
</tag>
```

e, no arquivo que utilizará o template, informamos que a página **estenderá** o template e passamos dentro do bloco o valor que queremos que ele assuma:

```html
{% extends 'arquivo-do-template.html' %}

{% block nome-do-bloco %}
Conteúdo que desejamos inserir.
{% endblock %}
```

Por exemplo, se quisermos alterar o título e o conteúdo de cada página dinamicamente, criamos o nosso arquivo do template, digamos, `base.html`:

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>
        {% block titulo %}
        {% endblock %}
    </title>
    {% block head %}
    {% endblock %}
</head>
<body>
    {% block content %}
    {% endblock %}
    <p>
        Este parágrafo estará presente em todas as páginas que utilizarem esse template, logo abaixo do conteúdo que adicionarmos dinamicamente dentro do bloco "content".
    </p>
</body>
</html>
```

e no nosso arquivo que utilizará esse template, digamos, `homepage.html`, estendemos a base e informamos o valor que desejamos que cada bloco assuma:

```html
{% extends 'base.html' %}

{% block titulo %}
HomePage
{% endblock %}

{% block content %}
<h2>Essa é a homepage do nosso site</h2>
{% endblock %}
```

### Trechos de Código

Uma outra forma de utilizar templates para as páginas HTML é construir determinada seção do conteúdo (por exemplo, o rodapé) em um arquivo próprio e **incluir** tal seção na página.

O processo para **incluir** um trecho da página é similar ao processo de extender um template, porém nesse caso devemos utilizar a tag `include` e inserí-la no local em que desejamos aquela seção.

Seguindo com o exemplo anterior, podemos criar uma barra de navegação em um arquivo separado, digamos, `navbar.html`:

```html
<nav>
    <!-- conteúdo da barra de navegação -->
</nav>
```

e incluí-la logo no início do nosso bloco "content":

```html
{% extends 'base.html' %}

{% block titulo %}
HomePage
{% endblock %}

{% block content %}
{% include 'navbar.html' %}
<h2>Essa é a homepage do nosso site</h2>
{% endblock %}
```

Caso desejemos incluir determinado trecho de código em todas as páginas, também é possível adicionar a tag `include` em templates que posteriormente serão estendidos.

### Incluindo Imagens Estáticas

Caso desejemos incluir uma imagem do nosso site, após feita a configuração descrita na seção [[#Pastas Static e Media]], devemos simplesmente adicionar a seguinte estrutura no nosso código:

```html
{% load static %}

<!-- Código HTML -->

<img src="{% static 'caminho-para-a-imagem/nome-do-arquivo.extensão' %}">

<!-- Código HTML -->
```

### Links Dinâmicos

É possível passar como parâmetro do `href` (de uma tag `<a>`, por exemplo) o URL de uma view específica do site.

Para isso, devemos novamente configurar ambos arquivos `urls.py`:

- No arquivo referente ao aplicativo, devemos 1) adicionar o parâmetro `name` na chamada da função `path` e 2) definir a variável `app_name` (recomenda-se utilizar o nome do aplicativo para facilitar o entendimento).

    ```python
    from django.urls import path
    from .views import MyView

    app_name = 'app'
    
    urlpatterns = [
        path('padrão-da-url/', MyView.as_view(), name='página')
    ]
    ```

- No arquivo referente ao projeto como um todo, devemos adicionar à chamada da função **`include`** o parâmetro `namespace` com o mesmo valor definido no passo anterior na variável `app_name`.

    ```python
    from django.urls import include, path
    ...  # outros imports

    urlpatterns = [
        ...,    # outros URLs
        path('link-desejado/', include('[nome-do-aplicativo].urls', namespace='app'))
    ]
    ```

Feitas essas configurações, é agora possível acessar esses links dentro dos arquivos HTML. Para isso, adicionamos ao `href` a tag `url` do Django e passamos como parâmetro a URL de redirecionamento, no formato `namespace:name` da página desejada:

```html
<!-- resto da página -->

<a href="{% url 'app:página' %}">Link Dinâmico</a>

<!-- resto da página -->
```

Caso a URL receba um parâmetro, como mostrado [aqui](#passagem-de-parâmetros-para-as-views), devemos ainda passar dado parâmetro à tag `url`:

```html
<!-- resto da página -->

<a href="{% url 'app:página' object.attribute %}">Link Dinâmico</a>

<!-- resto da página -->
```

## Contextos

<https://docs.djangoproject.com/pt-br/4.1/topics/templates/#the-django-template-language>

Ao configurarmos as nossas views, podemos passar variáveis para as páginas HTML, por meio de um *context*.

Em FBV, esse *context* é passado como um terceiro argumento para a função `render`, como no exemplo abaixo:

```python
from django.shortcuts import render
from .models import MyModel

def view(request):
    context = {}
    lista_models = MyModel.objects.all()   # lista todos os objetos do model no bando de dados
    context["lista_models"] = lista_models
    return render(request, "template.html", context)
```

A chave do dicionário representa o nome da variável que estará disponível no arquivo HTML da view.

A lista e descrição de todos os métodos de query do banco de dados pode ser encontrada na [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/models/querysets/#queryset-api).

Feito isso, poderemos agora acessar a variável `lista_models` no nosso arquivo `template.html` e fazer operações com ela. Por exemplo, para exibir na página todos os objetos, utilizamos a seguinte tag:

```html
{{ lista_models }}
```

Em CBV, o contexto já é passado automaticamente e depende de qual classe padrão está sendo herdada. O conteúdo do contexto e a variável de acesso (nos arquivos HTML) de cada classe estão descritos na [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/class-based-views/).

### Estrutura Forloop

Também é possível utilizar uma estrutura de `for` no arquivo HTML:

```html
{% for object in object_list %}
<hr>
<p>{{ object.attribute1 }}</p>
<p>{{ object.attribute2 }}</p>
<img src="{{ object.image.url }}">
{% endfor %}
```

Como é muito comum querermos acessar também o índice do objeto, existe uma estrutura chamada `forloop.counter`. Por exemplo, caso queiramos listar todos os episódios de uma série com seu respectivo número, podemos utilizar o seguinte código:

 ```python
 <h1>Episódios</h1>
 {% for episodio in object.episodios.all %}
 <p>Episódio {{ forloop.counter }}: {{ episodio.titulo }}</p>
 {% endfor %}
```

### Adicionando Variáveis ao Contexto de uma Classe

Caso desejemos passar outras variáveis no contexto, além da variável padrão da classe que está sendo herdada, precisamos apenas sobrescrever sua função `get_context_data`:

```python
class MyView(View):
    template_name = "template.html"
    model = MyModel
    
    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context['nova-variável'] = novo_valor
        return context
```

### Gerenciadores de Contexto

No tópico anterior, aprendemos a passar novas variáveis para uma view específica. Com **gerenciadores de contexto**, podemos passar uma variável para todas as views do nosso site.

Para configurar um gerenciador de contexto, é necessário criar, dentro da pasta do aplicativo, um novo arquivo Python (comumente chamado `context.py`). Nesse arquivo, cada variável personalizada será representada por uma função, que recebe como parâmetro o `request` e retorna um `context`.

Por exemplo, caso queiramos listar todos os filmes de uma plataforma em ordem decrescente de data de criação (ou seja, do mais novo para o mais antigo), podemos criar a seguinte função:

```python
from .models import Filme

def lista_filmes_recentes(request):
    lista_filmes = Filme.objects.all().order_by("-data_criacao")  # o sinal negativo indica ordem decrescente
    return {"lista_filmes_recentes": lista_filmes}
```

Em seguida, para que as variáveis sejam acessíveis nas páginas HTML, é necessário alterar o arquivo `settings.py`, adicionando o novo context à lista de `context_processors` presente no parâmetro `OPTIONS` da variável `TEMPLATES`, seguindo o seguinte padrão: `nome-do-app.nome-do-arquivo.nome-da-função-do-context`.

```python
TEMPLATES = [
    {
        ...
        'OPTIONS': {
            'context_processors': [
                ...
                'filme.context.lista_filmes_recentes'
            ]
        }
    }
]
```

A partir deste ponto, os novos contextos definidos serão acessíveis a partir de todos os arquivos HTML do projeto.

### Filtros

É possível adicionar filtros às variáveis e argumentos das tags.

Por exemplo, caso queiramos exibir apenas os 50 primeiros caracteres da descrição de um objeto do modelo, podemos utiliza o seguinte código em nosso arquivo HTML:

```html
<p>
    {{ object.descricao|slice:":50" }}
</p>
```

## Alterando o modelo a partir da view

Por vezes, desejamos atualizar algum atributo de um objeto do modelo ao se acessar uma página do nosso site (por exemplo, contabilizar uma visualização de um filme). Isso é feito ao se alterar o comportamento da view quando ela recebe um requisição do tipo GET.

Views baseadas em classes (CBV) têm um método padrão que processa tais requisições. Assim, para alterarmos o modelo ao acessarmos a página, devemos sobrescrever o método, aplicando as alterações desejadas e retornando a chamada no método da classe pai.

Para aplicar as alterações desejadas, precisamos primeiro recuperar o objeto (cuja view foi requisitada) com o método `self.get_objects()`, fazer as modificações necessárias e, por fim, salvar as alterações feitas com o método `self.save()`.

Seguindo o exemplo da visualização do filme, podemos utilizar o seguinte código:

```python
def get(self, request, *args, **kwargs):
    filme = self.get_object()  # descobre qual filme foi acessado
    filme.visualizacoes += 1   # contabiliza a visualização
    filme.save()               # salva a alteração
    return super().get(request, *args, **kwargs)  # redireciona o usuário para a URL final
```

## Formulários

### Barra de Pesquisa

Ao criar formulários no HTML com a tag `form`, devemos sempre passar o atributo `method`, indicando se desejamos fazer um `GET` ou `POST`, e o atributo `action`, que indica qual ação será realizada (no caso de um GET, para qual URL o usuário será direcionado). Além disso, devemos sempre configurar, na tag `input`, o atributo `name`, que será usado ao sobrescrevermos a função `get_queryset` da nossa view.

Por exemplo, para criar uma barra de busca de filmes pelo título, podemos criar o seguinte formulário:

```html
[pesquisa.html]
<form action="{{% url 'filme:pesquisafilme' %}}" method="get">
    <input type="text" name="query" placeholder="Pesquisar...">
    <input type="submit" value="">
</form>
```

```python
[views.py]
class PesquisaFilme(ListView):
    template_name = pesquisa.html
    model = Filme

    def get_queryset(self):  # edita o *object_list* retornado no context da página
        termo_pesquisa = self.request.GET.get('query')  # recupera o valor do parâmetro "query" da requisição
        if termo_pesquisa:
            object_list = self.model.object.filter(titulo__icontains=termo_pesquisa)
            return object_list
        else:
            return None
```

```python
[urls.py - nenhuma alteração específica é necessária]
from .models import PesquisaFilme

urlpatterns = [
    path('pesquisa/', PesquisaFilme.as_view(), name="pesquisafilme")
]
```

## Usuário

### Criando um Usuário Personalizado

O Django, por padrão, já cria um modelo de usuário ao criarmos um projeto, porém muitas vezes desejamos incluir novos campos de dados a esse modelo. **Cuidado:** ao alterarmos o modelo do usuário no meio do desenvolvimento do projeto, será necessário excluir o banco de dados atual e as todas as migrações realizadas e criar um novo banco de dados (incluindo superusuário), portanto é importantíssimo planejar e estruturar esse modelo para evitar futuras complicações.

Para modificar o usuário padrão do Django, devemos importar e herdar a classe `AbstractUser` e, na nova classe, criar os novos campos personalizados que desejamos.

```python
from django.contrib.auth.models import AbstractUser

class Usuario(AbstractUser):
    novo_campo = models.Field()
```

Ao registrarmos o novo modelo do arquivo `admin.py`, devemos passar um segundo argumento para a função `register`:

```python
from django.contrib import admin
from .models import Usuario
from django.contrib.auth.admin import UserAdmin

# configura a exibição do novo campo do admin do site
campos = list(UserAdmin.fieldsets)
campos.append(
    ("Histórico", {'fields': ("filmes_vistos")})
)
UserAdmin.fieldsets = tuple(campos)

admin.site.register(Usuario, UserAdmin)
```

Isso inclui automaticamente ao nosso modelo funcionalidades de gerenciamento de usuário (login e logout, sessão do usuário, permanecer logado ao fechar navegador etc.).

Por fim, no arquivo `settings.py`, devemos criar a variável `AUTH_USER_MODEL` para indicar a nova tabela do banco de dados a ser usada para autenticação:

```python
# Password validator
AUTH_USER_MODEL = "app.Usuario"
AUTH_PASSWORD_VALIDATORS = [
    ...
```

### Exibindo Atributos do Usuário

Por padrão, as CBV passam, no contexto, qual usuário está logado e acessando aquela view. Sendo assim, para exibir informações do usuário em uma página, podemos acessar seus atributos pela variável `{{ request.user }}`.

Por exemplo, caso queiramos exibir na tela todos os filmes que um usuário já assistiu na plataforma, podemos utilizar o seguinte código:

```html
<section>
    <h2>Assistir Novamente</h2>
    {% for filme in request.user.filmes_vistos.all %}
    <p>{{ filme.titulo }}</p>
    {% endfor %}
</section>
```

### Bloqueio de Páginas

Muitas vezes, desejamos bloquear certas páginas do site para que sejam acessadas apenas por usuários com login realizado.

Isso é feito ao tornarmos a classe que gerencia tal view uma subclasse da classe padrão `LoginRequiredMixin`.  
**Importante:** a classe `LoginRequiredMixin` deve sempre ser a primeira classe a ser herdada pela view a ser bloqueada.

```python
from django.contrib.auth.mixins import LoginRequiredMixin

class MyPage1(LoginRequiredMixin, View):  # funciona
    ...

class MyPage2(View, LoginRequiredMixin):  # não funciona
    ...
```

Além disso, no nosso arquivo `settings.py` devemos configurar o endereço para o qual o usuário que não estiver logado será redirecionado ao tentar acessar uma página bloqueada. Para isso, devemos criar duas variáveis:

```python
# link para o qual o usuário será redirecionado ao fazer login
LOGIN_REDIRECT_URL = 'app:página'

# página de login
LOGIN_URL = 'app:página'
```

Para informações mais detalhadas acerca de como (?) os links, consulte a seção [Links Dinâmicos](#links-dinâmicos).

### Login e Logout

Como os formulários de login e logout são muito comuns em quase todos os sites, o django já fornece views prontas dentro do módulo `django.contrib.auth.views`. Com isso, precisamos apenas criar o template e definir o URL.

```python
[urls.py]
from django.contrib.auth import views as auth_view
...

urlpatterns = [
    ...
    path('login/', auth_view.LoginView.as_view(template_name="login.html"), name="login"),
    path('logout/', auth_view.LogoutView.as_view(template_name="logout.html"), name="logout"),
]
```

```html
```

### Personalizando a Página de acordo com Login

Muitas vezes, queremos alterar determinado trecho da página de acordo com a realização ou não de login por parte do usuário.

Para isso, é necessário editarmos o arquivo HTML do template, e basta verificarmos a condição `{{ user.is_authenticated }}` ao criarmos determinada seção da página.

Por exemplo, caso queiramos alterar um botão de "Login" para "Sair" (ou seja, alterar o texto a ser exibido e o link de redirecionamento), podemos utilizar o seguinte código:

```html
<div>
    {% if user.is_authenticated %}
    <a href="{% url 'app:logout' %}">
        <button>Sair</button>
    </a>
    {% else %}
    <a href="{% url 'app:login' %}">
        <button>Login</button>
    </a>
    {% endif %}
</div>
```

### Redirecionando Usuários

Para redirecionar o usuário para outra página do site, utilizamos a função `redirect`, que recebe como parâmetro a página para a qual o usuário deve ser redirecionado, no formato `app_name:name`.

```python
from django.shortcuts import redirect

class HomePage(TemplateView):
    template_name = "homepage.html"
    
    def get(self, request, *args, **kwargs):
        if request.user.is_authenticated:
            return redirect("app:homefilme")
        else:
            return super().get(request, *args, **kwargs)

class HomeFilmes(LoginRequiredMixin, ListView):
    ...
```

### Editar Informações do Usuário

É necessário saber qual usuário será alterado.

```python
[urls.py]

urlpatterns = [
    ...,
    path('editarperfil/<int:pk>', EditarPerfil.as_view(), name='editarperfil')
]
```

```python
[views.py]

from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import UpdateView
from .models import Usuario

class EditarPerfil(LoginRequiredMixin, UpdateView):
    template_name = "editarperfil.html"
    model = Usuario
    fields = ['first_name', 'last_name', 'email']

    def get_success_url(self):
        return reverse('app:página')
```

Automaticamente, o `UpdateView` cria um formulário com os campos passados em `fields` e, ao submetermos e validarmos o formulário, o banco de dados será atualizado.

#### Alteração de Senha

Da mesma forma que o formulário de login, o Django também fornece uma view pronta para para alteração de senha.

```python
[urls.py]

from django.contrib.auth import views as auth_view
from django.urls import path, reverse_lazy

urlpatterns = [
    ...,
    path('mudarsenha/', auth_view.PasswordChangeView.as_view(template_name='mudarsenha.html', success_url=reverse_lazy('app:home')), name='mudarsenha')
]
```

## Criação de Formulários

### Formulário Padrão

A classe padrão `LoginView`, por exemplo, automaticamente passa, no contexto, a variável `form`, responsável por gerenciar o formulário de login. Para adicionar o formulário à página, basta adicionarmos ao template a tag `{{ form }}`, como no exemplo abaixo. Recomenda-se utilizar essa tag dentro de um `fieldset`.

```html
<form method="post">
    <fieldset>
        <legend>Faça login para continuar</legend>
        {{ form }}
    </fieldset>
    <button type="submit">Fazer login</button>
</form>
```

### Crispy-forms

O `crispy-forms` é uma ferramenta que permite a renderização rápida de formulários do Django por meio do Bootstrap. Para mais informações, acesse <https://github.com/django-crispy-forms/crispy-bootstrap5>.

```bash
pip install django-crispy-forms
pip install crispy-bootstrap5
```

Após instalação, devemos incluir o `crispy-forms` no arquivo `settings.py` como se fosse um aplicativo do nosso projeto e configurar seu uso:

```python
INSTALLED_APPS = [
    ...,
    'crispy_forms',
    'crispy-bootstrap5'
]

...

CRISPY_ALLOWED_TEMPLATE_PACKS = 'bootstrap5'

CRISPY_TEMPLATE_PACK = 'bootstrap5'
```

Além disso, é necessário também incluir o Bootstrap no seu arquivo HTML. Para isso, basta adicionar, dentro da seção `head`, a tag `<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">`, conforme descrito na [documentação](https://getbootstrap.com/docs/5.3/getting-started/introduction/).

Com isso, já é possível utilizar o `crispy-forms` para tornar nosso formulário bonito:

```html
{% load crispy_forms_tags %}

<form method="post">
    <fieldset>
        <legend>Faça login para continuar</legend>
        {{ form|crispy }}
    </fieldset>
    <button type="submit">Fazer login</button>
</form>
```

### CSRF Token

Toda vez que criarmos um formulário do tipo POST no Django, devemos obrigatoriamente incluir um `csrf token`, ou seja, um token de verificação para aumentar a segurança da comunicação entre a página e o backend do site.

Para ativar esse token, basta adicionarmos a tag `{% csrf_token %}` no início do formulário:

```html
{% load crispy_forms_tags %}

<form method="post">
    {% csrf_token %}
    <fieldset>
        <legend>Faça login para continuar</legend>
        {{ form|crispy }}
    </fieldset>
    <button type="submit">Fazer login</button>
</form>
```

### Formulários Personalizados

Além das estruturas prontas fornecidas por algumas CBV padrões do Django, podemos criar formulário personalizados nas views do nosso projeto. É uma boa prática criar esses formulários em um novo arquivo chamado `forms.py` dentro da pasta do aplicativo.

<https://docs.djangoproject.com/pt-br/4.1/ref/forms/>

Para saber todos os tipos de campos de formulário disponíveis, bem como os parâmetros que eles aceitam, consulte a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/forms/fields/). Por exemplo, para desabilitar a legenda de um campo (ou seja, exibir apenas o input), podemos utilizar o parâmetro `label=False`.

No exemplo abaixo, construímos um exemplo de formulário de criação de conta para um modelo de usuário personalizado.

```python
from django import forms
from django.contrib.auth.forms import UserCreationForm
from .models import Usuario

class CriarContaForm(UserCreationForm):
    email = forms.EmailField()

    class Meta:
        model = Usuario
        fields = ('username', 'email', 'password1', 'password2')
```

Em seguida, precisamos importar o novo formulário no arquivo `views.py` e criar a view correspondente:

```python
from django.views.generic import FormView
from .forms import CriarContaForm

class CriarConta(FormView):
    template_name = "criarconta.html"
    form_class = CriarContaForm
```

**Atenção:** ao contrário dos formulários padrões do Django, não há validação automática de formulários personalizadas. Assim, ao criarmos subclasses de `FormView`, devemos editar também dois métodos:

```python
from django.shortcuts import reverse
from django.views.generic import FormView
from .forms import CriarContaForm

class CriarConta(FormView):
    template_name = "criarconta.html"
    form_class = CriarContaForm

    def form_valid(self, form):
        form.save()  # como criamos um novo objeto no banco de dados, precisamos salvá-lo
        return super().form_valid(form)

    def get_success_url(self):
        # "O que acontecerá quando o formulário for bem-sucedido?"
        # Deve sempre retornar um link para o qual o usuário será redirecionado, por meio da função reverse()
        return reverse("app:login")
```

A criação do formulário no template HTML não sofre alteração em relação aos formulários padrões do Django.

## Redirecionamento Dinâmico de Usuários

```html
<form method="post">
    {% csrf_token %}
    <div>
        {{ form }}
    </div>
    <button type="submit">
        Acessar
    </button>
</form>
```

```python
[forms.py]

from django import Forms

class FormHomepage(forms.Form)
    email = forms.EmailField(label=False)
```

```python
[views.py]

from django.shortcuts import redirect, reverse
from django.views.generic import FormView
from .forms import FormHomepage
from .models import Usuario

class HomePage(FormView):
    template_name = "homepage.html"
    form_class = FormHomepage

    def get(self, request, *args, **kwargs):
        if request.user.is_authenticated:
            return redirect('filme:homefilme')
        else:
            return super().get(request, *args, **kwargs)

    def get_success_url(self):
        email = self.request.POST.get("email")
        usuario = Usuario.object.filter(email=email)
        if usuario:
            return reverse('filme:login')
        else:
            return reverse('filme:criarconta')
```

## Adaptando o Projeto para Produção

Para publicarmos o site (produção), é necessário fazer algumas alterações ao arquivo `settings.py` do projeto:

- Primeiro, precisamos setar a variável `DEBUG` para `False` (isso impede que os usuários executem códigos dentro do nosso site);
- Em seguida, precisamos adicionar à lista de `ALLOWED_HOSTS` o link que utilizaremos na produção;
- Por fim, precisamos configurar a variável `STATIC_ROOT` (similar à `MEDIA_ROOT`).

Além disso, é necessário configurar o [Whitenoise](https://whitenoise.evans.io/en/latest/) para que possamos utilizar os arquivos estáticos no site. Para isso, precisamos primeiro instalá-lo com o comando `pip install whitenoise`, em seguida adicioná-lo à lista de middlewares (em geral, isso é feito logo abaixo do middleware de segurança).

Ao final do processo, as alterações a serem realizadas no arquivo `settings.py` são as seguintes:

```python
...

DEBUG = False

ALLOWED_HOSTS = [
    "127.0.0.1",  # localhost
    "link-da-produção"
]

...

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',
    ...
]

...

STATIC_ROOT = BASE_DIR / "staticfiles"

...
```

### Banco de Dados Online

Para auxiliar o gerenciamento e comunicação com o banco de dados, utilizaremos a biblioteca [dj-database-url](https://github.com/jazzband/dj-database-url).

Primeiro, devemos instalar essa biblioteca e sua dependência:

```bash
pip install dj-database-url
pip install psycopg2
```

Em seguida, é necessário fazer as seguintes alterações ao arquivo `settings.py`:

```python
import dj_database_url

...

DATABASES['default'] = dj_database_url.config(
    conn_max_age=600,
    conn_health_checks=True,
)
```

Por fim, é necessário executar uma [migração](#migrações) para que sejam criadas todas as tabelas necessárias. Como estamos utilizando um novo banco de dados, é necessário também criar um novo [superusuário](#criação-do-superusuário), bem como adicionar novamente todos os objetos anteriores.

**Importante:** caso apenas o comando `python manage.py migrate` seja executado, não terá efeito nenhum sobre o banco de dados online; é necessário rodar o comando no serviço de hospedagem utilizado (por exemplo, `heroku run python manage.py migrate`).

### Arquivos de Mídia em Produção (com Cloudinary)

Para gerenciarmos nossos arquivos de mídia em produção com o Cloudinary, vamos utilizar a biblioteca [Django Cloudinary Storage](https://pypi.org/project/dj3-cloudinary-storage/).

```bash
pip install cloudinary dj3-cloudinary-storage
```

Após instalação, é necessário alterar o arquivo `settings.py`, adicionando o cloudinary à lista de aplicativos instalados (abaixo de `django.contrib.staticfiles`) e configurando duas novas variáveis:

```python
INSTALLED_APPS = [
    # ...
    'django.contrib.staticfiles',
    'cloudinary_storage',
    'cloudinary',
    # ...
]

CLOUDINARY_STORAGE = {
    'CLOUD_NAME': 'your_cloud_name',
    'API_KEY': 'your_api_key',
    'API_SECRET': 'your_api_secret'
}

DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

## Referências

Aulas e [materiais](https://drive.google.com/drive/folders/1zEFcbpo1tQtQw-a1vfblxZzXKWbTccdf) disponibilizados no curso [Python Impressionador](https://www.hashtagtreinamentos.com/curso-python)

[Documentação do Django](https://docs.djangoproject.com/pt-br/4.1/)
