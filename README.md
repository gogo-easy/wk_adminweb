## NgRouter 网关管理系统

### 启动

#### ngr admin web 
1. cd  ./
2. npm install 
3. npm start 或者 pm2 start ecosystem.json --only ngrAdminWeb_local

### ngr admin web static resource
#### 方法1
1. cd web/Public/static 目录
2. npm install
3. npm start &

#### 方法2
1. cd /web/Public/static 目录
2. npm run build
3. 将web/Public/static下build目录放置到nginx（如下例子放到/opt/ngrAdminWebResource/），采用nginx运行,nginx server配置如下：

````
    server {
            listen  8080;
            #server_name   localhost;
            access_log  /var/log/ngrAdminWebResource/access.log main;
            error_log  /var/log/ngrAdminWebResource/error.log;
            root   /opt/ngrAdminWebResource/;
            index  index.html index.htm;
            location / {
                    if (!-e \$request_filename) {
                            rewrite ^(.*)$ /index.index.html?s=\$1 last;
                            break;
                    }
            }

            location ~* ^.+\.(gif|jpg|jpeg|png|bmp|swf)$
            {
                    access_log  off;
                    expires     1d;
            }

            location ~* ^.+\.(js|css)?$
            {
                    access_log  off;
                    expires     1h;
            }
    }


````
  
