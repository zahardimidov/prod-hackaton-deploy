# Instruction


### Setup environment
python3.10 -m venv venv
source venv/bin/activate
pip install -r requirements.txt


### Setup VS code
CMP + SHIFT + P
Python: Select Interpreter
Введите путь к интерпретатору
./venv/bin/python3.10# fastapi_auth


### Setup server

git clone <URL>

docker build -t fastapi_auth:latest .
docker run -p 127.0.0.1:4500:4500 fastapi_auth:latest# prod-hackaton-backend



### Setup docker on your server

https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository


### Setup nginx on your server
https://medium.com/@deltarfd/how-to-set-up-nginx-on-ubuntu-server-fc392c88fb59


<code>
nano /etc/nginx/sites-available/

server {
    listen 80;
    server_name myvehicles.ru;

    location / {
        proxy_pass http://0.0.0.0:3000/;
    }
    location /api/ {
        proxy_pass http://0.0.0.0:4545/;
    }
    location /webhook {
        proxy_pass http://0.0.0.0:4545/webhook;
    }
}
</code>

### Setup ssl sertificate on your server
https://timeweb.cloud/docs/unix-guides/ustanovka-ssl-na-nginx


### Setup startup service

sudo nano /etc/systemd/system/vehiclebot.service
   
[Unit]
Description=Docker Compose Application
Requires=docker.service
After=docker.service

[Service]
Restart=always
WorkingDirectory=/path/to/your/docker-compose/directory
ExecStart=/usr/local/bin/docker-compose up
ExecStop=/usr/local/bin/docker-compose down

[Install]
WantedBy=multi-user.target


sudo systemctl daemon-reload

sudo systemctl start vehiclebot.service

sudo systemctl status vehiclebot.service# prod-hackaton-deploy
