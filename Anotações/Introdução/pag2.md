# Instalando o Symfony no Linux

Esta seção da documentação orienta sobre como instalar o Symfony 6 ou superior em um sistema Linux, incluindo a configuração de ferramentas necessárias e a criação de um projeto de teste.

## 1. Pré-requisitos

Antes de instalar o Symfony, certifique-se de que as seguintes ferramentas estão instaladas em sua máquina:

- **Git**: Sistema de controle de versão.
- **PHP**: Linguagem de programação necessária para executar o Symfony.
- **Composer**: Gerenciador de dependências para PHP.

### 1.1. Instalando o Git

Certifique-se de que o Git está instalado:

```bash
sudo apt install git
```

### 1.2. Instalando o PHP

Instale o PHP usando o seguinte comando:

```bash
sudo apt install php
```

### 1.3. Instalando o Composer

1. Acesse o link oficial do Composer e siga as instruções de instalação: [Instalação do Composer](https://getcomposer.org/download/).
2. Após baixar o Composer, mova o arquivo para uma área acessível em todo o sistema:

```bash
sudo mv composer.phar /usr/local/bin/composer
```

## 2. Instalando o Symfony

### 2.1. Acesse o Link de Download

Para baixar o Symfony, acesse o seguinte link: [Download Symfony](https://symfony.com/download).

### 2.2. Instalando o Symfony CLI

Execute o seguinte comando para instalar o Symfony CLI:

```bash
wget https://get.symfony.com/cli/installer -O - | bash
```

### 2.3. Criando o Projeto

Crie um novo projeto Symfony especificando a versão 6 ou superior:

```bash
symfony new new_project --version=6.*
```

## 3. Rodando o Projeto

Após a criação do projeto, navegue até o diretório do projeto e inicie o servidor embutido do Symfony:

```bash
cd new_project
symfony serve
```

Ao executar o comando acima, o Symfony gerará um link. Você pode acessá-lo em seu navegador para visualizar a página inicial padrão que vem com o pacote de instalação.

## 4. Correção de Possíveis Erros

### 4.1. Erro de "Page not found"

Se você visualizar a mensagem **# Page not found**, pode ser devido à falta do certificado de autenticação. Para corrigir esse problema, execute o seguinte comando:

```bash
symfony server:ca:install
```

Isso instalará o certificado necessário para que o Symfony funcione corretamente.

## Conclusão

Com os passos acima, você deverá ter o Symfony 6 ou superior instalado e funcionando em seu sistema Linux. Com isso, você está pronto para começar a desenvolver aplicações web usando este poderoso framework.
