# TrixEx

[Unit]
Description=Gunicorn instance
After=network.target
[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/TrixEx
Environment="PATH=/home/ubuntu/TrixEx/venv/bin"
ExecStart=/home/ubuntu/TrixEx/venv/bin/gunicorn --workers 3 --bind unix:TrixEx.sock -m 007 wsgi:application
[Install]
WantedBy=multi-user.target

server {
    listen 80;
    server_name 3.138.135.8;
    location / {
        include proxy_params;
        proxy_pass http://unix:/home/ubuntu/TrixEx/TrixEx.sock;
    }
}

http://3.128.182.106/index