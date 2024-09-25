Para criar URLs amigáveis em um site desenvolvido em PHP, Bootstrap e JavaScript, você pode seguir estes passos:

## 1. Ativar o módulo de reescrita no Apache (mod_rewrite)

Se você estiver usando o servidor Apache, é necessário ativar o módulo mod_rewrite. Em um ambiente Linux, você pode fazer isso com o seguinte comando:

```bash

  sudo a2enmod rewrite

```

## 2. Configurar o arquivo `.htaccess`

Crie ou edite um arquivo `.htaccess` na raiz do seu site e adicione as seguintes regras para reescrever as URLs:

  ```htacces
  RewriteEngine On

  # Remove o arquivo index.php das URLs
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule ^(.*)$ index.php?url=$1 [L,QSA]

  ```
Essas regras fazem o Apache reescrever a URL para ser processada pelo arquivo `index.php`, passando o caminho amigável como um parâmetro `url`.

## 3. Tratar a URL no PHP

No arquivo `index.php`, você pode capturar o valor da URL amigável e tratá-la para carregar as páginas corretas. Por exemplo:

  ```PHP
  
  <?php
    // Captura a URL amigável
    $url = isset($_GET['url']) ? $_GET['url'] : 'inicio'; // Se não houver URL, carrega 'inicio'
    $url = rtrim($url, '/'); // Remove a barra no final da URL, se houver
    $url = filter_var($url, FILTER_SANITIZE_URL); // Sanitiza a URL

    // Divide a URL em partes
    $urlParts = explode('/', $url);

    // Carrega a página baseada no primeiro segmento da URL
    $page = $urlParts[0];

    switch ($page) {
        case 'inicio':
            include 'paginas/inicio.php';
            break;
        case 'sobre':
            include 'paginas/sobre.php';
            break;
        case 'contato':
            include 'paginas/contato.php';
            break;
        default:
            include 'paginas/404.php'; // Página de erro 404
            break;
    }
  ?>

  ```
##  4. Estrutura de Pastas

Organize suas páginas em uma pasta `pages` para facilitar o gerenciamento. Por exemplo:

  ```bash
  
  /paginas
  /inicio.php
  /sobre.php
  /contato.php
  /404.php

  ```
##  5. Usando URLs amigáveis no Bootstrap e JavaScript

Em seus links, em vez de usar URLs como `index.php?page=about`, use o formato amigável:

  ```html

  <a href="/sobre">Sobre</a>
  <a href="/contato">Contato</a>

  ```
## 6. Validação e Segurança

- `Sanitização:` Sempre sanitize os valores recebidos da URL para evitar vulnerabilidades, como injeção de código.

- `Validação:` Verifique se as páginas realmente existem antes de tentar incluí-las, para evitar que usuários maliciosos manipulem URLs.

Com esses passos, você conseguirá criar URLs amigáveis em seu site em PHP, utilizando Bootstrap e JavaScript.

#### Doni7Brandão
