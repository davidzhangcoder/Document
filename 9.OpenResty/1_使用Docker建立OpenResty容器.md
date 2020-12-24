1.使用Docker建立OpenResty容器  
20201109

复制配置文件到本地  
docker cp openresty:/usr/local/openresty/nginx/conf/nginx.conf /Users/davidzhang/Documents/dockerworkspace/openresty/conf/

用复制下来的配置文件建立容器  
docker run -itd --name openresty -p 80:80 -v /Users/davidzhang/Documents/dockerworkspace/openresty/conf/nginx.conf:/usr/local/openresty/nginx/conf/nginx.conf -v /Users/davidzhang/Documents/dockerworkspace/openresty/lua:/data openresty/openresty