---
published: true
---
cloudsio

## Giriş
  * Merhaba, Bu yazımda **LDAP** hakkında konuşacağız. LDAP nedir , ne için kullanılır , nasıl kurulur gibi sorulara cevap arayacağız.

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

![alt text](https://berkanterbey.github.io/images/002.png "ssh-audit komutunun çıktısı")

![alt text](https://berkanterbey.github.io/images/003.png "ssh-audit komutunun çıktısı")


{% gist 9668e9b36b7ca93c1fb399369f41ae60 %}

## LDAP Kurulumu

  * Kurulum için Debian 11 (bullseye) bir sunucu seçtim. 
  * Aşağıdaki komutla ilgili paketleri yüklüyoruz.

    >sudo apt update && sudo apt install slapd ldap-utils -y

  ![alt text](https://berkanterbey.github.io/images/020.png "slapd parola")

  * Ansible ile dağıtırken her işletim sistemi sürümüne göre desteklenen algoritmalarda değişiklikler olabilir. Bundan dolayı playbook umuza sunucuların işletim sistemini bakıp, sadece Ubuntu 20.04 (focal) için çalışacak şekilde ayarlanacak. Dilerseniz farklı işletim sistemlerinide benzer yöntemle ekleyebilirsiniz.

  * Aşağıdaki ekran görüntüsünde host02.txt dosyasında belirtilen makinelerde işletim sistemi kod adı bilgisine ulaşıyoruz.

![alt text](https://berkanterbey.github.io/images/004.png "Ansible İşletim Sistemi tanıma")


{% gist 713f9e1675998fea47d7a05bdb636e2f %}


  * Yapacağımız işlemi kısaca özetlersek
    * sshd_config hedef makineye kopyalamak (var olan izin ve sahiplikleri koruyarak)
    * sshd_config de belirtilen hostkeyleri **yoksa oluşturmak**
    * ssh servisini yeniden başlatmak (**değişiklik olmuşsa**)

{% gist 3189b4eff66986f91bdf1c5e478cb421 %}  


Bir sonraki yazımızda görüşmek üzere ;)
