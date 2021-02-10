# angular-10-basic-authentication-example

Angular 10 - Basic HTTP Authentication Example

To see a demo and further details go to https://jasonwatmore.com/post/2020/10/17/angular-10-basic-http-authentication-tutorial-example


# Nginx config

server {

        listen 9002;
        server_name localhost;
        root /Users/gali/projects/angular-jwt-auth/dist/angular-jwt-auth;

        location / {
                try_files $uri $uri/ index.html;
        }

        location /api {
            proxy_set_header Host $host:$server_port;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Host $http_protocol$http_host;
            keepalive_timeout  600;
            proxy_connect_timeout       300;
            proxy_send_timeout          300;
            proxy_read_timeout          300;
            send_timeout                300;
            proxy_pass http://127.0.0.1:9001;
        }

}