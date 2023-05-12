Запустить контейнер с ubuntu, используя механизм LXC

```
root@WIN-ITTRKFDRUUI:~# lxc-create -n test-container -t ubuntu

root@WIN-ITTRKFDRUUI:~# lxc-ls -f
NAME           STATE   AUTOSTART GROUPS IPV4      IPV6 UNPRIVILEGED      
test-container STOPPED 0         -      -         -    false    
```

Ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает
```
root@WIN-ITTRKFDRUUI:~# vi /var/lib/lxc/test-container/config

lxc.cgroup2.memory.max = 256M
```
Добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно

```
NAME           STATE   AUTOSTART GROUPS IPV4      IPV6 UNPRIVILEGED
test-container STOPPED 0         -      -         -    false

root@WIN-ITTRKFDRUUI:~# vi /var/lib/lxc/test-container/config
lxc.start.auto  =  1

NAME           STATE   AUTOSTART GROUPS IPV4      IPV6 UNPRIVILEGED
test-container STOPPED 1         -      -         -    false
```

Опробовать ограничить количество ядер CPU

cpuset.cpus — какие ядра может использовать контейнер, номера начиная с нуля, например 0,1 или 0-3
```
root@WIN-ITTRKFDRUUI:~# vi /var/lib/lxc/test-container/config

lxc.cgroup.cpuset.cpus = 0-2
```