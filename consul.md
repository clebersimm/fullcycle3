# Curso fullcycle 3.0 comunicação de sistemas - Consul   

### Levantar o servidor   
```
docker-compose up -d   
docker exec -it consul01 sh   
```

### Dentro do container   
Modo desenvolvedor   
```
consul agent -dev   
consul members   
curl localhost:8500/v1/catalog/nodes   
apk -U add bind-tools   
dig @localhost -p 8600 consul01.node.consul   
```

### Cluster - servers   
```
docker exec -it consulserver01 sh   
consul agent -server -bootstrap-expect=3 -node=consulserver01 -bind=<ipcontainer> -data-dir=/var/lib/consul -config-dir=/etc/consul.d    
mkdir /var/lib/consul   
mkdir /etc/consul.d   
docker exec -it consulserver02 sh   
consul agent -server -bootstrap-expect=3 -node=consulserver02 -bind=172.21.0.4 -data-dir=/var/lib/consul -config-dir=/etc/consul.d   
docker exec -it consulserver03 sh   
consul agent -server -bootstrap-expect=3 -node=consulserver03 -bind=172.21.0.2 -data-dir=/var/lib/consul -config-dir=/etc/consul.d    
consul join 172.21.0.3    
```

### Agents (client)   

```
consul agent -bind=<ipcontainer> -data-dir=/var/lib/consul -config-dir=/etc/consul.d     
consul agent -bind=<ipcontainer> -data-dir=/var/lib/consul -config-dir=/etc/consul.d -retry-join=<ipserverconsul>     
apk add nginx   
```
