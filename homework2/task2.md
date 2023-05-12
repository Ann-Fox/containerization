
### Задание 2*: настроить автоматическую маршрутизацию между контейнерами. Адреса можно взять: 10.0.12.0/24 и 10.0.13.0/24.

Задание со звездочкой - повышенной сложности, это нужно учесть при выполнении (но сделать его необходимо).
```
lxc-create -n container1 -t ubuntu
Добаялем стат IP

vi /var/lib/lxc/container1/config
lxc.net.0.ipv4.address = 10.0.0.11/24

root@WIN-ITTRKFDRUUI:~# lxc-ls -f
NAME           STATE   AUTOSTART GROUPS IPV4      IPV6 UNPRIVILEGED
container1     RUNNING 1         -      10.0.0.11 -    false
```

Создаем 2 контейнер и добавим стат ip

```
lxc-create -n test123 -t ubuntu

vi /var/lib/lxc/test123/config
lxc.net.0.ipv4.address = 10.0.0.10/24

root@WIN-ITTRKFDRUUI:~# lxc-ls -f
NAME           STATE   AUTOSTART GROUPS IPV4      IPV6 UNPRIVILEGED
container1     RUNNING 1         -      10.0.0.11 -    false
test123        RUNNING 1         -      10.0.0.10 -    false

root@WIN-ITTRKFDRUUI:~# lxc-attach -n container1

root@WIN-ITTRKFDRUUI:~# ping 10.0.0.10
PING 10.0.0.10 (10.0.0.10) 56(84) bytes of data.
64 bytes from 10.0.0.10: icmp_seq=1 ttl=64 time=8.36 ms
64 bytes from 10.0.0.10: icmp_seq=2 ttl=64 time=0.189 ms
64 bytes from 10.0.0.10: icmp_seq=3 ttl=64 time=0.037 ms
64 bytes from 10.0.0.10: icmp_seq=4 ttl=64 time=0.037 ms
root@WIN-ITTRKFDRUUI:~# exit

root@WIN-ITTRKFDRUUI:~# lxc-attach -n test123
root@WIN-ITTRKFDRUUI:~# ping 10.0.0.11
PING 10.0.0.11 (10.0.0.11) 56(84) bytes of data.
64 bytes from 10.0.0.11: icmp_seq=1 ttl=64 time=0.279 ms
64 bytes from 10.0.0.11: icmp_seq=2 ttl=64 time=0.034 ms
64 bytes from 10.0.0.11: icmp_seq=3 ttl=64 time=0.047 ms
64 bytes from 10.0.0.11: icmp_seq=4 ttl=64 time=0.039 ms
64 bytes from 10.0.0.11: icmp_seq=5 ttl=64 time=0.037 ms
```
