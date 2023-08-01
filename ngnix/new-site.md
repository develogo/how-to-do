# Configuração de um Site Nginx

Este guia o levará através da configuração de um site Nginx chamado `test.develogo.dev`, desde a criação das pastas e arquivos até a criação do certificado SSL com Certbot.

## Pré-requisitos

* Servidor Ubuntu com Nginx instalado
* Domínio apontado para o IP do seu servidor
* Certbot instalado

## Passos

### 1. Criação de pastas e arquivos

Primeiro, crie um diretório para o seu site:

```bash
sudo mkdir -p /var/www/test.develogo.dev/html
```

### 2. Propriedade dos arquivos

Em seguida, altere a propriedade desses arquivos para o usuário do servidor web:

```bash
sudo chown -R www-data:www-data /var/www/test.develogo.dev
```

### 3. Crie uma página de teste

Crie uma simples página HTML de teste:

```bash
echo "<h1>Bem-vindo ao test.develogo.dev!</h1>" | sudo tee /var/www/test.develogo.dev/html/index.html
```

### 4. Configure o Nginx

Crie um novo arquivo de configuração para o seu site:

```bash
sudo nano /etc/nginx/sites-available/test.develogo.dev
```

Adicione a seguinte configuração ao arquivo:

```bash
server {
    listen 80;
    listen [::]:80;

    server_name test.develogo.dev www.test.develogo.dev;

    location / {
        root /var/www/test.develogo.dev/html;
        index index.html;
    }
}
```

### 5. Ativar o site

Ative o site criando um link simbólico do arquivo de configuração para a pasta `sites-enabled`:

```bash
sudo ln -s /etc/nginx/sites-available/test.develogo.dev /etc/nginx/sites-enabled/
```

### 6. Verifique a configuração do Nginx

Verifique se a configuração do Nginx está correta:

```bash
sudo nginx -t
```

### 7. Recarregue o Nginx

Recarregue o Nginx para aplicar as novas configurações:

```bash
sudo systemctl reload nginx
```

### 8. Obtenha um certificado SSL com Certbot

Use o Certbot para obter um certificado SSL para o seu site:

```bash
sudo certbot --nginx -d test.develogo.dev -d www.test.develogo.dev
```

Siga as instruções na tela para concluir a configuração.

Agora, você deve ser capaz de acessar seu site em http://test.develogo.dev e https://test.develogo.dev.

```javascript
Certifique-se de substituir `test.develogo.dev` pelo nome do seu domínio em todas as etapas.
```


