# Infraestrutura por Código - Aplicação em Python para gerenciar infraestrutura construída com Terraform

- **Aluno:** Francisco Pinheiro Janela
- **Curso:** Engenharia da Computação
- **Semestre:** 6
- **Contato:** franciscopj@al.insper.edu.br
- **Ano:** 2022


# Como Operar com o meu programa:

## Pré-requisitos

Para começar a operar com o meu programa, sigam o passo a passo indicado no readme do [meu repositório](https://github.com/fran-janela/projeto-comp-nuvem) no github.

## Como usar

Ao iniciar o programa pela primeira vez, o usuário se depara com a escolha entre a configuração das regiões, podendo, nesse caminho, gerenciar instâncias, gerenciar security groups e levantar aplicações em **HA** (High Availability), e a configuração do ambiente do IAM, onde o usuário pode gerenciar usuários e políticas(restrições).

Para facilitar, a árvore de navegação abaixo, pode trazer mais facilidade para o usuário se encontrar pelo programa:

```
├── Configuração de Regiões
│   ├── Criar, deletar ou escolher uma região
│   ├── Gerenciar Instâncias
│   │   ├── Listar Instâncias
│   │   ├── Criar Instância
│   │   ├── Deletar Instância
│   │   ├── Atualizar Configuração de uma Instância
│   │   └── Voltar
│   ├── Gerenciar Security Groups
│   │   ├── Listar Security Groups
│   │   ├── Criar Security Group
│   │   ├── Deletar Security Group
│   │   ├── Adicionar Regras a um Security Group
│   │   ├── Deletar Regras de um Security Group
│   │   └── Voltar
│   └── Levantar Aplicações em HA
├── Configuração do IAM
│   ├── Limpar ou Restaurar a Infraestrutura do IAM
│   ├── Gerenciar Usuários
│   │   ├── Listar Usuários
│   │   ├── Criar Usuário
│   │   ├── Deletar Usuário
│   │   ├── Adicionar Políticas a um Usuário
│   │   ├── Deletar Políticas de um Usuário
│   │   └── Voltar
│   └── Gerenciar Políticas
│       ├── Listar Políticas
│       ├── Importar Política
│       └── Voltar
└── Sair
```

Em sua maioria, as instruções de uso de cada uma das funcionalidades está autocontida no próprio programa, mas existem algumas considerações que podem ser feitas:

### Configuração de Regiões

#### Criar, deletar ou escolher uma região

Ao escolher a opção de deletar uma região, não existe confirmação necessária, e se o comando for executado, a região será deletada, ou seja, irá perder todos os recursos criados naquela região de uma vez. Portanto, é importante que o usuário tenha certeza de que deseja deletar a região.

#### Gerenciar Instâncias

- Ao Listar as Instâncias, o usuário deve escolher pelo número mostrado na tela aquela que quer visualizar mais informações.

- Ao Criar uma Instância, o usuário deve escolher o tipo de instância que deseja criar, e o nome da instância que deseja criar. O nome da instância deve ser único, ou seja, não pode haver duas instâncias com o mesmo nome na mesma região. Além disso, o número de instâncias olocado é a quantidade de réplicas aquelas configurações que irão ser criadas. Por fim, o Sistema Operacional pré definido é o `Ubuntu Server 18.04 LTS`.

- Ao atualizar a configuração de uma instância estará mudando todas as réplicas criadas. Quando for feita a mudança de número de instâncias, será sempre a com índice maior que será deletada. Ao mudar os *ids* dos security groups, deverá passar novamente todos aqueles que desejar aplicar à instância, configurações antigas serão perdidas.

#### Gerenciar Security Groups

- Ao Listar os Security Groups, o usuário deve escolher pelo número mostrado na tela aquele que quer visualizar mais informações.

- Ao Criar um Security Group, o usuário deve escolher o nome do Security Group que deseja criar. O nome do Security Group deve ser único, ou seja, não pode haver dois Security Groups com o mesmo nome na mesma região. Além disso, poderá ser criado quantas regras de Ingress e Egress que o usuário desejar, se atentando somente à liberação de todas as portas para não correr riscos de segurança.

- Só será possível deletar um Security Group se ele não estiver sendo usado, ou seja, se quiser deletá-lo, deve remover todas as dependências dele nas instâncias da região.

### Configuração do IAM

#### Limpar ou Restaurar a Infraestrutura do IAM

- Limpar a infraestrutura do IAM significa apagar todas as configurações pré criadas para usuários, mas todos as políticas importadas continuarão sendo criadas quando for restaurada a infraestrutura.

- A Infraestrutura vem configurada com 4 políticas de teste: *AdministratorAccess*, *AdminNorthVirginia*, *AdminOregon* e *AdminOhio*. Essas políticas são criadas automaticamente quando a infraestrutura é restaurada, e não podem ser deletadas.

#### Gerenciar Usuários

- Ao Listar os Usuários, desta vez o usuário não precisa escolher pelo número mostrado na tela, pois o programa já irá mostrar as informações de todos os usuários e todas as políticas atreladas a eles.

- Ao Criar um Usuário, o usuário deve escolher o nome do Usuário que deseja criar. O nome do Usuário deve ser único, ou seja, não pode haver dois Usuários com o mesmo nome na mesma região. Além disso, a senha aparecerá somente na criação deste, então guarde-a em um local seguro antes de continuar. Atrelar uma política (restrição) ao usuário, deve ser feita posteriormente com a função de adicionar políticas.

- Ao deletar um Usuário, o usuário não poderá ser recuperado, e todas as configurações de políticas atreladas também serão descartadas, mas as políticas em si ainda continuarão existindo.

#### Gerenciar Políticas

- Ao Listar as Políticas, o usuário deve escolher pelo número mostrado na tela aquela que quer visualizar mais informações.

- Para importar uma política, o usuário deve passar o *path* completo do arquivo `.json`. Caso seja um arquivo válido, a regra será criada e permanentemente adicionada ao seu repositório de políticas. Para deletá-la, deve apagar o arquivo .json criado em `iam/policies/`. O nome da política será o nome do arquivo, sem a extensão.

- Para facilitar a criação, construa a política pela dashboard da AWS e copie o conteúdo do arquivo `.json` gerado.

## Começando

Para seguir esse tutorial é necessário:

- **Tecnologias:** Terraform, Python
- **Documentos:** [Terraform AWS Docs](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

## O que é Terraform?


## Motivação

Minha motivação para a criação desta aplicação e, consequentemente, este tutorial veio da crescente vontade de apresnder sobre infraestrutura e Computação Nuvem, o que me fez produzir algo robusto e confiável, que pudesse ser utilizado por pessoas com pouco conhecimento em infraestrutura, mas com a vontade de aprender.