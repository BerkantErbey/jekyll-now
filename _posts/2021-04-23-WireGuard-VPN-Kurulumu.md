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

* Wireguard paketi kurulur.

```apt update && apt install wireguard```

* Sunucuda açık ve kapalı anahtarları üretiriz.

```shell
# Wireguard ile alakalı ayarlamaların olduğu dizin
cd /etc/wireguard
# Dizin izinlerini ayarlama (root kullanıcısıyla giriş yaptığınızdan emin olun)
umask 077
# Açık ve kapalı anahtarları üretme
wg genkey | tee privatekey | wg pubkey > publickey
```
* Sunucuda IP paketlerini yönlendirme özelliğini açıyoruz.

`/etc/sysctl.conf` içerisinde `net.ipv4.ip_forward=1` satırını yorumdan çıkarmamız yeterli oluyor. Değiştirdiğimiz ayarın aktif olması için `sudo sysctl -p` komutunu çalıştırıyoruz.

* Güvenlik duvarı ayarlamalarını yapmaya başlıyoruz. Sunucu olarak Ubuntu kullandığımdan ufw yi kullanacağım.

SSH protokolünün portuna ve VPN protokolü için kullanacağım udp portuna(kendi isteğinize göre bir port numarası seçebilirsiniz) izin verip güvenlik duvarını aktifleştiriyorum.

```shell
sudo ufw allow ssh
sudo ufw allow VPNPortu/udp
sudo ufw enable
```

* Sunucuda gerçekleştireceğimiz son adım wireguard protokolünün kullanacağı bacağın ayarlamalarını yapmak ve bu ayarlamaları `sudo wg-quick up wg0` komutuyla aktifleştiriyoruz.

{% gist 94aad68564c44161354db4f45192c042 %}

### İstemcide yapılacak ayarlamalar

* Sunucu adımlarında olduğu gibi wireguard paketi kuruyoruz ve açık,kapalı anahtarlarımızı üretiyoruz.

* İstemcide wg bacağının ayarlamaları aşağıda bulunmaktadır. Sunucu tarafında olduğu gibi aktifleştiriyoruz.

{% gist 23afb965e4cddbe3eef788b7892179b6 %}
