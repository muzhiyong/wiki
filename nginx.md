```
yum install pcre-devel  lua-devel

./configure --user=www --group=www --add-module=/opt/soft/module/ngx_module_redis --add-module=/opt/soft/module/ngx_module_lua --add-module=/opt/soft/module/ngx_cache_purge --add-module=/opt/soft/module/ngx_module_upstream_check --add-module=/opt/soft/module/ngx_module_upstream_hash --add-module=/opt/soft/module/ngx_module_memc --add-module=/opt/soft/module/ngx_module_srcache --add-module=/opt/soft/module/ngx_module_echo --add-module=/opt/soft/module/ngx_devel_kit --add-module=/opt/soft/module/ngx_module_set_misc --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module

```




