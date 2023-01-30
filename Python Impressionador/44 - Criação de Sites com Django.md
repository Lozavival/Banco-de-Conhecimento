---
tags: python, python-impressionador, framework, web
---

# Criação de Sites com Django

Descrição

---

## Pré-requisitos

1. [Classes e Orientação a Objetos](35%20-%20Orientação%20a%20Objetos%20-%20Classes%20e%20Métodos)
2. [Ambientes Virtuais](28%20-%20Ambientes%20Virtuais)

## Planejamento do Site

É muito importante, antes de tudo, idealizar e definir a estrutura do site, para orientar e servir de guia durante sua criação. Caso, ao longo do desenvolvimento, sejam necessárias alterações no planejamento, podemos alterá-lo, mas esse passo inicial reduz essa possibilidade, pois já sabemos de antemão o que queremos fazer.

Nesse momento, podemos nos utilizar, por exemplo, de esboços/rascunhos para as nossas views e estruturas de tópicos para os nossos modles, bem como listar (com o maior detalhamento possível) as funcionalidades que desejamos, para termos uma referência do que devemos construir.

É importante dar especial atenção aos models, para evitar que, futuramente, sejam necessárias mudanças significativas no banco de dados (para se adicionar ou remover atributos, por exemplo), visto que as views podem ser alteradas com maior impunidade ao andamento do projeto como um todo. Especialmente, dê atenção ao modelo dos susuários, pois qualquer alteração futura (ao longo do desenvolvimento) requer exclusão e recriação do banco de dados para ser aplicada.

## Estrutura Inicial do Django

### Instalação

Após criar e ativar um ambiente virtual, é preciso instalar o django utilizando o pip:

```bash
pip install django
```

### Criação do Projeto

O primeiro passo para a criação de todo site é iniciar o projeto do django:

```bash
django-admin startproject [nome-do-projeto] [caminho-para-o-projeto]
```

Quando criamos um projeto, é automaticamente criado também um banco de dados.

### Criação de um Aplicativo

Aplicativos são utilizados para separar funcionalidades totalmente diferentes de um mesmo projeto (por exemplo, exibição de vídeos e escrita de blogs). As views e os modelos serão definidos no aplicativo, e cada aplicativo é vinculado ao projeto.

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

Em seguida, será necessário inserir no terminal as seguintes informações: nome de usuário, email e senha (duas vezes para segurança). Encerrado esse processo, o superusuário será criado.

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

Imagens estáticas são imagens criadas pelo construtor do site (logos, imagens de fundo etc.), enquanto imagens de mídia são imagens enviadas pelos usuários (por exemplo, fotos postadas no Instagram). Para que esses aruivos possam ser armazenados, é necessário criar duas pastas: "static" e "media".

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

A criação de modelos, ou seja, a adição de tabelas ao banco de dados é feita no arquivo `models.py` do respectivo aplicativo. Não esqueça que, após uma alteração nos models, é necessário fazer uma [migração](#Migrações) do banco de dados.

Cada tabela do banco de dados, ou seja, cada objeto, será uma classe do Python que herda a classe `models.Model` do módulo `django.db`. Dentro dessa classe, devemos apenas criar os campos (atributos) que queremos para determinado objeto, definindo o tipo de dado que cada campo armazenará.

Para ver os tipos de campos disponíveis e sua descrição, bem como seus parâmetros obrigatórios, consulte a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/models/fields/#field-types).<br> Para ver os argumentos opcionais disponíveis para todos os tipos de campos, consulte a [documentação](https://docs.djangoproject.com/pt-br/4.1/ref/models/fields/#field-options).<br>**Importante:** para utilizar o campo `ImageField`, é necessário instalar a biblioteca Pillow (basta executar o comando `pip install pillow`).

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

- Recomenda-se sempre criar o nome de um modelo no singular, pois o django automaticamente adiciona um "s" ao final na visualizaçao de administrador.

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

#### Configurações adicionais

Para configurar como cada entrada será representada na lista de objetos da tela de administrador, devemos definir a função `__str__` da classe. 

Por exemplo, caso desejássemos que fosse exibido o título de cada filme, poderíamos, no exemplo anterior, definir a classe da seguinte forma:

```python
class Filme(models.Model):
	...    # definição dos campos

	def __str__(self):
		return self.titulo
```

Como isso não altera a estrutura do banco de dados, não é necessário efetuar uma migração.

### Páginas

Para criar uma página do site, é necessário configurar três coisas: o *URL* (link onde a página aparecerá), a *view* (o que acontece quando acessar a página) e o *template* (parte visual que será exibida, ou seja, os arquivos HTML).

#### Configuração das URLs

A configuração das URLs do aplicativo ocorre de forma muito similar à do projeto como um todo. No arquivo `urls.py` presente na pasta do aplicativo, vamos criar uma variável `urlpatterns` e nela configurar os links do site:

```python
from django.urls import path

urlpatterns = [
	path('link-da-página/', view-da-página)
]
```

#### Views

#### Template

## Referências

[Django Documentation - django-admin and manage.py](https://docs.djangoproject.com/pt-br/4.1/ref/django-admin/)

[Documentação do Django](https://docs.djangoproject.com/pt-br/4.1/)
