# Guia Detalhado de Instalação e Configuração do Docker para Projetos Symfony

## 1. Verificando a Instalação do Docker

Antes de configurar o Docker, é essencial garantir que ele esteja instalado e funcionando corretamente no seu sistema. Para verificar o status do Docker, execute:

```bash
sudo systemctl status docker
```

### Explicação:
- **`sudo systemctl`**: Este comando gerencia serviços no Linux. Ele exige privilégios de administrador (por isso usamos `sudo`).
- **`status docker`**: Verifica o status do serviço Docker. Se o Docker estiver rodando, o resultado incluirá uma linha indicando que o status do serviço é "active (running)".

Se o Docker não estiver instalado ou não estiver rodando, você precisará instalar ou iniciar o serviço:

- Para instalar, siga as instruções da [documentação oficial do Docker](https://docs.docker.com/engine/install/).
- Para iniciar o serviço, use:
  ```bash
  sudo systemctl start docker
  ```

## 2. Configurando o Docker no Projeto Symfony

### 2.1. Copiando os Arquivos de Configuração

Para configurar o Docker em um projeto Symfony, você precisará de arquivos de configuração como o `docker-compose.yml`. Estes arquivos descrevem como os contêineres devem ser configurados (por exemplo, servidor web, PHP, banco de dados). 

**Passos:**
1. Copie o arquivo `docker-compose.yml` (e outros necessários) da pasta `pacote-criacao-docker-projetos-symfony` para o diretório raiz do seu projeto Symfony.
2. Certifique-se de que as configurações (como versões de PHP, MySQL e portas) estejam adequadas às necessidades do seu projeto.

### 2.2. Subindo os Contêineres Docker

Com os arquivos de configuração no lugar, você pode criar e iniciar os contêineres usando:

```bash
docker-compose up -d --build
```

### Explicação:
- **`docker-compose`**: Ferramenta que permite definir e gerenciar múltiplos contêineres Docker com base em um único arquivo de configuração (`docker-compose.yml`).
- **`up`**: Este comando cria e inicia os contêineres definidos no arquivo `docker-compose.yml`. Se os contêineres já existirem, ele apenas os inicia.
- **`-d`**: "Detached mode". Isso executa os contêineres em segundo plano, permitindo que você continue usando o terminal.
- **`--build`**: Força a reconstrução das imagens dos contêineres antes de iniciá-los. Isso é útil se você alterou o `Dockerfile` ou alguma dependência do projeto.

Ao final, o Docker criará e executará os serviços descritos no arquivo `docker-compose.yml` (como PHP, MySQL, Nginx, etc.) no modo background.

### 2.3. Verificando as Imagens Criadas

Após subir os contêineres, você pode verificar as imagens Docker criadas com:

```bash
docker images
```

### Explicação:
- **`docker images`**: Lista todas as imagens Docker que estão presentes no sistema. Imagens são basicamente os "blueprints" dos contêineres, contendo tudo o que o contêiner precisa para rodar, como o sistema operacional, bibliotecas e a aplicação.
  
A saída incluirá os seguintes campos:
- **REPOSITORY**: Nome do repositório ou imagem (ex: `mysql`, `php`, `nginx`).
- **TAG**: Versão da imagem (ex: `latest`, `8.0` para PHP 8).
- **IMAGE ID**: Um identificador único da imagem.
- **CREATED**: A data e hora em que a imagem foi criada.
- **SIZE**: O tamanho total da imagem.

### 2.4. Verificando os Contêineres em Execução

Para ver quais contêineres estão em execução no momento, use:

```bash
docker ps
```

### Explicação:
- **`docker ps`**: Mostra uma lista de todos os contêineres em execução no momento. Para listar todos os contêineres (incluindo os que não estão em execução), você pode usar `docker ps -a`.

A saída do comando incluirá os seguintes campos:
- **CONTAINER ID**: Um identificador único para o contêiner.
- **IMAGE**: A imagem Docker usada para criar o contêiner (ex: `php`, `mysql`).
- **COMMAND**: O comando que está sendo executado no contêiner.
- **CREATED**: O tempo desde que o contêiner foi criado.
- **STATUS**: O status atual do contêiner (por exemplo, `Up` significa que está rodando).
- **PORTS**: As portas que estão sendo usadas e mapeadas (ex: `0.0.0.0:8080->80/tcp` significa que o contêiner está expondo a porta 80 para o host na porta 8080).
- **NAMES**: Nome dado ao contêiner, o que facilita a referência em vez de usar o CONTAINER ID.

## 3. Acessando o Bash do Contêiner

Quando precisar interagir diretamente com o contêiner (por exemplo, rodar comandos Symfony ou PHP), você pode acessar o terminal do contêiner com o seguinte comando:

```bash
docker-compose exec php /bin/bash
```

### Explicação:
- **`docker-compose exec`**: Permite executar comandos em um contêiner específico. Ao contrário do `docker exec`, este comando faz referência ao serviço definido no `docker-compose.yml`.
- **`php`**: O nome do serviço ou contêiner (definido no `docker-compose.yml`), onde o PHP está rodando.
- **`/bin/bash`**: Inicia um terminal bash dentro do contêiner.

Após a execução desse comando, você estará no terminal do contêiner. Aqui, você poderá rodar comandos diretamente no ambiente configurado pelo Docker, como:

```bash
symfony serve
```

Este comando iniciará o servidor Symfony dentro do contêiner.

### Dica:
Lembre-se de que qualquer comando que você executa dentro do contêiner estará limitado ao ambiente Docker e não afetará diretamente o sistema host. Isso permite que você mantenha um ambiente de desenvolvimento isolado.

---

## Conclusão

Seguindo este guia detalhado, você será capaz de configurar e gerenciar o Docker para seu projeto Symfony. O Docker facilita o processo de desenvolvimento ao criar ambientes de desenvolvimento consistentes, ajudando a eliminar problemas relacionados a diferenças entre ambientes locais e de produção. Além disso, ele oferece controle total sobre a configuração dos serviços e simplifica a interação com ferramentas e tecnologias como PHP, MySQL e servidores web.
