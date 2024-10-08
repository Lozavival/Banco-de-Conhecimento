# Ambientes Virtuais em Python

**Palavras-chave:** #python #bibliotecas #framework  
**Última modificação:** <%+ tp.file.last_modified_date('DD/MM/YYYY HH:mm') %>  
**Notas de estudo relacionadas:**  
\-----

Um ambiente virtual empacota todas as dependências de um projeto e as armazena em um diretório, fazendo com que nenhum pacote seja instalado diretamente no sistema operacional. Sendo assim, cada projeto pode possuir seu próprio ambiente e, consequentemente, suas bibliotecas ou até mesmo o Python em versões específicas.

Isso possibilita que possamos, por exemplo:

1. Usar ferramentas que funcionam apenas com versões específicas do Python (ou projetos que só funcionem com uma versão específica de uma biblioteca ou framework).
2. Isolar de todo o resto apenas aquilo que é estritamente necessário para aquele programa rodar (pacotes, bibliotecas, frameworks etc.).

---

## Tabela de Conteúdos

- [venv](#venv)
    - [Criação do Ambiente Virtual (venv)](#cria%C3%A7%C3%A3o-do-ambiente-virtual-venv)
    - [Ativação e Desativação do Ambiente Virtual (venv)](#ativa%C3%A7%C3%A3o-e-desativa%C3%A7%C3%A3o-do-ambiente-virtual-venv)
    - [Replicando Ambientes Virtuais (venv)](#replicando-ambientes-virtuais-venv)
    - [Configuração de Variáveis de Ambiente (venv)](#configura%C3%A7%C3%A3o-de-vari%C3%A1veis-de-ambiente-venv)
- [Conda](#conda)
    - [Criação do Ambiente Virtual (Conda)](#cria%C3%A7%C3%A3o-do-ambiente-virtual-conda)
        - [Especificando a Localização do Ambiente (Conda)](#especificando-a-localiza%C3%A7%C3%A3o-do-ambiente-conda)
    - [Ativação e Desativação do Ambiente Virtual (Conda)](#ativa%C3%A7%C3%A3o-e-desativa%C3%A7%C3%A3o-do-ambiente-virtual-conda)
    - [Replicando Ambientes Virtuais (Conda)](#replicando-ambientes-virtuais-conda)
    - [Configuração de Variáveis de Ambiente (Conda)](#configura%C3%A7%C3%A3o-de-vari%C3%A1veis-de-ambiente-conda)
- [Referências](#refer%C3%AAncias)

---

## venv

`venv` é um módulo nativo do Python com suporte para criação de ambientes virtuais leves.

### Criação do Ambiente Virtual (venv)

Para criar ambientes virtuais utilizando o módulo `venv`, utilizamos o seguinte comando:

```bash
python3 -m venv /path/to/new/virtual/environment
```

É comum criarmos o ambiente virtual em uma pasta `venv` localizada na raiz do projeto. Para isso, navegue até o diretório do projeto e execute o comando `python3 -m venv venv/`.

Isso criará o diretório especificado, caso ele não exista, ou o reutilizará, caso já exista.

### Ativação e Desativação do Ambiente Virtual (venv)

Um ambiente virtual pode ser "ativado" por meio de um script presente no seu diretório de binários (`bin` em sistemas POSIX, `Scripts` no Windows). A invocação do script de ativação é específico da plataforma; os comandos de ativação dos shells mais comuns de ambas plataforma estão listados abaixo.

|   Shell    | Comando de ativação               |
|:----------:|:--------------------------------- |
|  bash/zsh  | `source <venv>/bin/activate`      |
|    fish    | `source <venv>/bin/activate.fish` |
|  csh/tcsh  | `source <venv>/bin/activate.csh`  |
|    cmd     | `<venv>\Scripts\activate.bat`     |
| PowerShell | `<venv>\Scripts\Activate.ps1`     |

Nos comandos acima, `<venv>` deve ser substituído pelo caminho para o diretório que contém o ambiente virtual.

A desativação de um ambiente virtual é feita com o comando:

```bash
deactivate
```

### Replicando Ambientes Virtuais (venv)

Após ativar o ambiente virtual, é possível começar a instalar pacotes nele com o comando `pip install`. Porém, ao invés de instalar cada pacote individualmente, o pip permite que todas as dependências de um projeto sejam declaradas em um arquivo `requirements.txt`. Isso é útil para que possamos replicar nossos ambientes virtuais.

É possível exportar a lista de todos os pacotes instalados e suas versões por meio do comando `pip freeze`. Podemos, então, salvar esta lista no arquivo `requirements.txt` por meio do seguinte comando:

```bash
pip freeze > requirements.txt
```

Para instalar todos os pacotes listados neste arquivo, utilizamos a flag `-r`:

```bash
pip install -r requirements.txt
```

### Configuração de Variáveis de Ambiente (venv)

Para configurar variáveis de ambientes dentro de um ambiente virtual do Python, basta adicioná-las a seu arquivo de ativação. Nesse caso, as variáveis serão criadas toda vez que o venv for ativado.

- Se você estiver rodando um terminal PowerShell, deve editar o arquivo `Scripts/Activate.ps1`:

    ```ps1
    $env:VAR_NAME = value
    ```

- Se estiver rodando no cmd, edite o `Scripts/activate.bat`:

    ```bat
    set VAR_NAME = value
    ```

- Se estiver usando o bash, edite o arquivo `bin/activate`:

    ```bash
    export VAR_NAME=value
    ```

Outra opção é criar, na raiz do diretório do projeto, um arquivo `.env` e nele inserir as credenciais desejadas:

```bash
VAR_NAME=value
```

Nos exemplos acima, substitua `VAR_NAME` e `value` pelo nome e valor da sua nova variável de ambiente, respectivamente.

**Nota:** em muitos casos, usamos variáveis de ambiente para armazenar informações sensíveis, como chaves de API e senhas. Sendo assim, a prática mais comum é adicionar uma exceção para arquivos `.env`, para que eles não sejam enviados por commit para o controle do código-fonte, e, em seu lugar, adicionamos um arquivo `.env.example`, contendo a lista de todas as variáveis que o projeto requer, mas sem incluir seus valores. Dessa forma, fornecemos um guia ao usuários do projeto acerca de quais variáveis devem ser configuradas sem expor nossos dados sensíveis.

## Conda

Conda é um sistema de gerenciamento de pacotes e ambientes de código aberto, e pode ser utilizado como uma alternativa ao módulo `venv`.

### Criação do Ambiente Virtual (Conda)

Para criar ambientes virtuais utilizando o conda, utilizamos o seguinte comando:

```bash
conda create -n <nome-do-ambiente>
```

É possível especificar, no comando acima, a versão do Python e os pacotes (com ou sem versão) desejados. Por exemplo:

```bash
conda create -n <nome-do-ambiente> python=3.9 scipy=0.17.3 astroid babel
```

Também é possível criar um ambiente virtual a partir de um arquivo `environment.yml`. Isso é feito com o seguinte comando:

```bash
conda env create -f environment.yml
```

Para remover um ambiente, execute:

```bash
conda remove -n <nome-do-ambiente> --all
```

ou

```bash
conda env remove --name <nome-do-ambiente>
```

#### Especificando a Localização do Ambiente (Conda)

Por padrão, novos ambientes virtuais são instalados na pasta `envs` de seu diretório conda. Porém, é possível alterar esse local ao informar um diretório alvo ao criar o ambiente.

```bash
conda create --prefix ./venv
```

No exemplo acima, o ambiente virtual será criado no subdiretório `venv` do diretório do projeto. Os benefícios desse procedimento, em detrimento do anterior, são os seguintes:

- É fácil identificar que aquele projeto usa um ambiente virtual;
- O projeto é auto-contido, pois tudo é armazenado em uma única pasta;
- Não é necessário criar um nome diferente para cada ambiente virtual (de cada projeto) criado.

### Ativação e Desativação do Ambiente Virtual (Conda)

Para ativar um ambiente virtual criado na pasta padrão `envs`, utilizamos o seguinte comando:

```bash
conda activate <nome-do-ambiente>
```

Caso o ambiente tenha sido criado dentro do diretório do projeto (por exemplo, em um subdiretório `venv`), sua ativação é feita pelo comando:

```bash
conda activate ./venv
```

É possível que você receba o seguinte aviso se não tiver ativado seu ambiente:

```txt
Warning:
This Python interpreter is in a conda environment, but the environment has
not been activated. Libraries may fail to load. To activate this environment
please see https://conda.io/activation.
```

Nesse caso, caso você utilize Windows, execute o seguinte comando no Anaconda Prompt:

```bash
c:\Anaconda3\Scripts\activate base
```

Para desativar um ambiente, digite:

```bash
conda deactivate
```

### Replicando Ambientes Virtuais (Conda)

Para criar uma cópia exata de um ambiente na mesma máquina, podemos **cloná-lo**:

```bash
conda create --name <nome-do-novo-ambiente> --clone <nome-do-novo-ambiente>
```

Outra opção é usar arquivos de especificação explícitos para criar **ambientes conda idênticos**, na mesma máquina ou não. **Atenção:** esse processo normalmente não é multiplataforma.

Primeiro, criamos uma lista de especificações com o comando:

```bash
conda list --explicit > spec-file.txt
```

Para criar um ambiente idêntico ao anterior:

```bash
conda create --name <nome-do-ambiente> --file spec-file.txt
```

Para utilizar o arquivo de specs para instalar todos os pacotes listados:

```bash
conda install --name <nome-do-ambiente> --file spec-file.txt
```

Por fim, podemos também **compartilhar** nosso ambiente (por exemplo, para que ele possa ser recriado). Esse processo permite que o ambiente seja rapidamente reproduzido, com todos os seus pacotes, versões e variáveis de ambiente.

Primeiramente, é necessário que o ambiente a ser exportado esteja ativo. Em seguida, executamos o comando:

```bash
conda env export > environment.yml
```

Agora, basta compartilhar uma cópia de seu arquivo `environment.yml` para que outra pessoa possa recriar seu ambiente.

### Configuração de Variáveis de Ambiente (Conda)

Primeiramente, é necessário que um ambiente esteja ativo.

Para listar todas as variáveis de ambiente, rode:

```bash
conda env config vars list
```

Para adicionar novas variáveis de ambiente, rode:

```bash
conda env config vars set var_name=value
```

Para remover uma variável de ambiente, rode:

```bash
conda env config vars unset var_name
```

Nos comandos acima, substitua `var_name` e `value` pelo nome e valor da nova variável, respectivamente.

Assim que você tenha configurado uma variável de ambiente, é necessário reativar seu ambiente.

---

## Referências

Aulas e [materiais](../6%20-%20Anexos/28.%20Ambientes%20Virtuais.ipynb) disponibilizados no curso [Python Impressionador](https://www.hashtagtreinamentos.com/curso-python)

["Criando ambientes virtuais para projetos Python com o Virtualenv" - TreinaWeb](https://www.treinaweb.com.br/blog/criando-ambientes-virtuais-para-projetos-python-com-o-virtualenv)

["venv - Creation of virtual environments" - Documentação do Python](https://docs.python.org/3/library/venv.html)

["Installing packages using pip and virtual environments" - Documentação do Python](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment)

["Ambientes virtuais em Python" - Alura](https://www.alura.com.br/artigos/ambientes-virtuais-em-python)

["Working with Environment Variables in Python" - Twilio](https://www.twilio.com/blog/environment-variables-python)

["Managing environments" - Documentação do Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
