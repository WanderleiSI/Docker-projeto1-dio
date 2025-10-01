# Docker-projeto1-dio
Exemplo de como servir uma página HTML usando Docker Compose e o servidor Apache (httpd). Desafio DIO.

# 🚀 Desafio DIO: Aplicação HTML em Contêiner Apache com Docker Compose

Este repositório contém o código e a configuração para o desafio prático da formação **Docker Fundamentals** da **Digital Innovation One (DIO)**. O objetivo é subir uma aplicação web simples (HTML) utilizando o **Docker Compose** e o servidor web **Apache HTTPD** dentro de um contêiner.

---

## 💻 Tecnologias Utilizadas

* **Docker:** Para a conteinerização da aplicação.
* **Docker Compose:** Para orquestrar e definir o serviço Apache.
* **Apache HTTPD:** Servidor web oficial (`httpd:latest`) que serve a página HTML.
* **HTML/CSS:** Aplicação web simples ("Hello World" estilizado).

---

## 📂 Estrutura de Pastas

A estrutura do projeto simula o ambiente onde os arquivos foram criados, conforme o desafio:

.
├── compose/
│   └── docker-projeto1-dio/
│       └── compose.yml      # Definição do serviço Apache com Docker Compose
└── data/
└── docker-projeto1-dio/
└── index.html       # Arquivo HTML da aplicação

---

## 🛠️ Como Executar o Projeto

Siga os passos abaixo para construir e subir a aplicação em contêineres:

### 1. Criar a Estrutura de Pastas e Arquivos

Você precisa garantir que as pastas e os arquivos estejam configurados exatamente como definidos no `docker-compose.yml`.

1.  **Crie os diretórios:**
    ```bash
    mkdir -p /compose/docker-projeto1-dio
    mkdir -p /data/docker-projeto1-dio
    ```

2.  **Crie o arquivo `compose.yml`:**
    * Caminho: `/compose/docker-projeto1-dio/compose.yml`
    * Conteúdo:
    ```yaml
    services:
      apache:
        image: httpd:latest
        container_name: my-apache-app
        ports:
          - "80:80"
        volumes:
          # Mapeia a pasta da aplicação para o diretório de documentos do Apache
          - /data/docker-projeto1-dio:/usr/local/apache2/htdocs
    ```

3.  **Crie o arquivo `index.html`:**
    * Caminho: `/data/docker-projeto1-dio/index.html`
    * Conteúdo (A página simples de "Olá, Mundo!"):
    ```html
    <!DOCTYPE html>
    <html lang="pt-BR">
    </html>
    ```

### 2. Subir o Contêiner

Acesse o diretório que contém o arquivo `compose.yml` e execute o comando do Docker Compose:

```bash
# Mude para a pasta do docker-compose
cd /compose/docker-projeto1-dio

# Suba o serviço em modo detached (-d)
docker compose up -d
```

### 3. Verificar o Resultado

Acesse a aplicação no seu navegador:
```bash
http://localhost:80
```

Se estiver executando o Docker em uma máquina virtual ou servidor, use o IP da máquina.

### 4. Parar e Remover

Para derrubar o serviço e remover o contêiner e a rede, execute:

```bash
docker compose down
```

### Detalhes da Configuração

O arquivo compose.yml realiza o seguinte:

* image: httpd:latest: Define que será utilizada a imagem oficial mais recente do servidor Apache.

* ports: - "80:80": Mapeia a porta 80 da máquina host (sua máquina) para a porta 80 do contêiner (porta padrão do Apache).

* volumes:: Cria um bind mount (montagem de volume):

    * O conteúdo do diretório /data/docker-projeto1-dio na máquina host é sincronizado com o diretório de documentos do Apache (/usr/local/apache2/htdocs) dentro do contêiner. Isso garante que o Apache sirva o seu index.html.