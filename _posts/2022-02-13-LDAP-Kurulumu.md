---
published: true
---


## Giriş
  * Merhaba, Bu yazımda **LDAP** hakkında konuşacağız. LDAP nedir , ne için kullanılır , nasıl kurulur gibi sorulara cevap arayacağız. Ek bilgiler ve öğrendiklerimizi uygulama

## LDAP Nedir??
  * Türkçesi Basit Dizin Erişim Protokolüdür. 
  * Aşama gözetilerek yapılan sınıflama(hiyerarşik) yapısına sahiptir.
  * Dizin servislerindeki amaç aranılan nesnenin/bilginin ağda nerede bulunduğudur. Dallanan bu yapıda her bir dal için **dn** adı verilen ayırt edici isim (distinguished name) bulunur.
  * LDAP TCP/IP protokolünü temel alır genellikle 389(tcp) portunu kullanır.
  * LDAP sunucusunu dizin servisini ve protokolü tanımlamış özel bir **NoSQL** veritabanı diyebiliriz.

## LDAP Kullanım Alanları

  * Kimlik Doğrulama & Yetkilendirme
    * Linux tabanlı bir çok uygulamada (Jenkins, Gitlab,  Eposta Sunucuları ...)
      * Bu gibi uygulamalarda kullandığımız ldap yapısına ait, bind user(dizinde arama/sorgu yapabilen sadece okuma yetkisi olan kullanıcı), kullanıcıların ve grupların dizinde nerede bulunduğunu girerek ldaptaki kullanıcı veya grupları kimlik doğrulama amacı ile kullanabiliriz.
        -- LDAP AYAR RESMİ --

  * Dizinde Çeşitli Objelerin Tutulması
    * DNS Kayıtları
    * Bilgisayarlar 

    >ssh-audit localhost



{% gist 9668e9b36b7ca93c1fb399369f41ae60 %}

## LDAP Kurulumu

  * Kurulum için Debian 11 (bullseye) bir sunucu seçtim. 
  * Aşağıdaki komutla ilgili paketleri yüklüyoruz.

    >sudo apt update && sudo apt install slapd ldap-utils -y

  ![alt text](https://berkanterbey.github.io/images/020.png "slapd parola")

  * Paket kurulurken kendiliğinden search base i oluşturuyor /etc/resolv.conf daki bilgilere göre.

    > sudo slapcat
  * Komutun çıktısı sizin durumunuza uymuyorsa aşağıdaki komutla değiştirebilirsiniz (Örn: **cloudsio.com**) 

    > sudo dpkg-reconfigure slapd

  ![alt text](https://berkanterbey.github.io/images/21-26.gif "dpkg-reconfigure slapd adımları")
  
    > sudo slapcat

  ![alt text](https://berkanterbey.github.io/images/027.png "slapcat komut çıktısı")

Bir sonraki yazımızda görüşmek üzere ;)
