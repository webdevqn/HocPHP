1. Go to www folder by cd command line
2. git clone git@github.com:webdevqn/HocPHP.git
3. We will get folder HocPHP after downloading
4. cd to folder HocPHP to start to code
5. sudo nano /etc/nginx/sites-available/HocPHP.conf
6. We get the command screen, copy all content into, change the folder as your computer and save:

server {
    listen 80;

    root /home/webdevqn/www/HocPHP;
    index index.php index.html index.htm;

    server_name hocphp.vu;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        try_files $uri /index.php =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}


7. Create a link from available to enabled: sudo ln -s /etc/nginx/sites-available/HocPHP.conf /etc/nginx/sites-enabled
8. Restart service: sudo service nginx restart
9. Open file host to create a new virtual host: sudo nano /etc/hosts
10. Insert a new line to create a new virtual host with any names you like: 127.0.0.1   hocphp.vu
11. Finish, go out at the browser, we can type: hocphp.vu to get the site.
