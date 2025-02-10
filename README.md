This project originates from and thanks to the original author:  
https://github.com/Vovanys/zabbix_nginx_vts

# zabbix_nginx_vts  
Zabbix monitoring scripts for `nginx-module-vts`  

**Requirements**  

- [nginx](https://nginx.org/en/) and the installed module [nginx-module-vts](https://github.com/vozlt/nginx-module-vts)  

The scripts are modified from the NGINX PLUS monitoring scripts [nginx-plus-zabbix](https://github.com/strannick-ru/nginx-plus-zabbix). Some features were added, and some were broken :) since PLUS is more advanced and provides more data.  
Server discovery and their statistics were added because the original script only searched for upstreams.  

### **Installation**  

1. Add the following to `/etc/zabbix/zabbix_agentd.d/userparameter_nginx_vts.conf`:  

```text
UserParameter=nginx.stat.[*],/etc/zabbix/scripts/nginx-stats.py $1 $2 $3 $4 $5 $6 $7
UserParameter=nginx.discovery[*],/etc/zabbix/scripts/nginx-discovery.py $1
```

2. Restart the Zabbix agent  
3. Import the Zabbix template  
4. Add a macro to the host specifying the path to the status URL in JSON format (!!!)  
   Example: `{$URL_VTS_STATUS}`, e.g., `https://site.com/status/format/json`  

   ![macros](https://github.com/johe123qwe/zabbix_nginx_vts/blob/master/img/macros.jpg?raw=true)  

5. Attach the Nginx VTS template to the network node  
6. Check for fresh data  

   ![lastdata](https://github.com/johe123qwe/zabbix_nginx_vts/blob/master/img/lastdata.jpg?raw=true)  

   ![discovery](https://github.com/johe123qwe/zabbix_nginx_vts/blob/master/img/discovery.jpg?raw=true)