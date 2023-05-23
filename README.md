# 10.1-HW
### Домашнее задание к занятию 10.1 - "Keepalived/vrrp" - Семкин Вячеслав
***
### Задание 1
Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived. 

*В качестве решения предоставьте:*   
*- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;*   
*- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.*   

**Ответ:**

Первая нода

```
vrrp_instance failover_test {
state MASTER
interface enp0s3
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.88.191
}
virtual_ipaddress {
192.168.88.240 dev enp0s8 label enp0s3:vip
}
}
```

![1-1](https://github.com/SemkinVA/10.1-HW/blob/main/1-1.png)

Вторая нода

```
vrrp_instance failover_test {
state BACKUP
interface enp0s3
virtual_router_id 10
priority 100
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.88.190
}
virtual_ipaddress {
192.168.88.240 dev enp0s8 label enp0s3:vip
}
}
```

![1-2](https://github.com/SemkinVA/10.1-HW/blob/main/1-2.png)
