---
published: true
---

![alt text](https://www.wireguard.com/img/wireguard.svg "WireGuard Logo")




Bu blogdaki ilk Türkçe yazım...

## WireGuard VPN Nedir?
  * WireGuard ücretsiz ve açık kaynaklı bir VPN protokolüdür. Bu VPN protokolü UDP paketlerini kullanır. Diğer VPN protokollerinden farkı ise küçük kod tabanı sayesinde daha az saldırı yüzeyi sunması, daha fazla bantgenişliğini daha düşük gecikmeyle destekleyebilmesidir. Daha küçük kod tabanına sahip olması büyük takımlar yerine bireysel kullanıcıların da kodu rahatlıkla inceleyebilmesi anlamına geliyor.

## WireGuard Nasıl Çalışır?

  * WireGuard SSH protokolüyle temelde aynı şekilde çalışır. Sunucu ve istemci kendi aralarında açık anahtarlarını paylaşırlar. Diğer VPN protokollerinde olduğu gibi bağlantıları yönetmeye, aradaki bağlantının durumu hakkında endişelenmeye, arka plan servislerini yönetmeye ihtiyaç yoktur.

## Kurulum

Temelde elimizde bir sunucu ve en az bir tane istemci olmalı. Sunucu için herhangi bir bulut sağlayıcıdan sanal makine kiralayabilirsiniz.


### Sunucuda yapılacak ayarlamalar

Wireguard paketi kurulur.

```apt update && apt install wireguard```

Sunucuda açık ve kapalı anahtarları üretiriz.

```shell
# Wireguard ile alakalı ayarlamaların olduğu dizin
cd /etc/wireguard
# Dizin izinlerini ayarlama (root kullanıcısıyla giriş yaptığınızdan emin olun)
umask 077
# Açık ve kapalı anahtarları üretme
wg genkey | tee privatekey | wg pubkey > publickey
```


## Simple use-case demo (Installing a software)

Sometimes we need to install package/software to many servers. In such cases, we can use the automation tool like Ansible.
Thanks to Ansible, we can perform parallel and multiple tasks

At first , we create project folder

```mkdir -pv testLab && cd testLab```

We write the machines in the inventory file to determine which machines the commands will run on.
  ```
  # hosts.txt (Inventory file)
  [test]
  192.168.1.143
  ```

I solved the authentication problem on the host machine by adding the main machine's public key under the authorized_keys file (/root/.ssh/authorized_keys)

We can list tasks in myPlaybook.yml with this command  

  ```ansible-playbook --list-tasks myPlayBook.yml```

This playbook contains 3 tasks.

1.Remove tixati program on host

{% gist c1f14b461868fc75bc8c22f3568cfa4f %}

2.Add qbittorrent's repo to host

{% gist b735ef3ce1546ec66bd1151650458f37 %}

3.Install qbittorrent to host

{% gist 18496abe2110db95f55c17aee3e97004 %}

You can access the full playbook here

  {% gist 87c1ab6de1f3fd40728db58e2d7e4097 %}

We run our commands on desired machines with the following command

```ansible-playbook -i hosts.txt myPlayBook.yml```
