<h2 align="center">前端部署说明</h2> 

   
### 介绍
该微服务前端部分使用Vue.js框架。目前采用nginx代理的方式部署到服务器上。所涉及的内容为：Vue打包、nginx的配置等

### 打包
- 打开终端，定位到前端项目目录
- 输入npm run build
- 完成后可在项目目录中找到dist文件夹，产生了打包文件（static、index.html）

### 配置
- 将打包文件（static、index.html）,放到服务器上，本例放到了服务器桌面，新建文件夹（web）目录下 C:\Users\Administrator\Desktop\web
- 打开nginx目录下的nginx.conf文件，修改里面的配置：
    ① 在server中配置nginx端口号listen
    ② 在server中配置打包文件定位目录location，例：
        location / {
            root   C:\Users\Administrator\Desktop\web;
            index  index.html;
        }
    ③ 在server中配置访问后端的接口地址location，添加下图代码。图中的172.20.41.8:3099改为后端的地址，其他不变
        location ^~/admin/{
            proxy_pass http://172.20.41.8:3099/admin/;
            include proxy_setting.conf;
        }
        
        location ^~/auth/{
            proxy_pass http://172.20.41.8:3099/auth/;
            include proxy_setting.conf;
        }
- 保存配置，启动nginx



### 查看效果
    打开浏览器，输入网址172.20.41.9:9011/#/login （172.20.41.9为服务器ip，9011为nginx的端口号）

