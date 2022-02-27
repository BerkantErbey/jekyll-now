---
published: true
---


## Giriş
  * Merhaba, Bu yazımda **LDAP** hakkında konuşacağız. LDAP nedir , ne için kullanılır , nasıl kurulur gibi sorulara cevap arayacağız.

## LDAP Nedir??
  * Türkçesi Basit Dizin Erişim Protokolüdür. 
  * Aşama gözetilerek yapılan sınıflama(hiyerarşik) yapısına sahiptir.
  * Dizin servislerindeki amaç aranılan nesnenin/bilginin ağda nerede bulunduğudur. Dallanan bu yapıda her bir dal için **dn** adı verilen ayırt edici isim (distinguished name) bulunur.
  * LDAP TCP/IP protokolünü temel alır genellikle 389(tcp) portunu kullanır.

## LDAP Kullanım Alanları

  * Kimlik Doğrulama
    * Linux tabanlı bir çok uygulamada (Jenkins, Gitlab,  Eposta Sunucuları ...)
{% gist f831cf512355fd37bcc2b1c3f54f518c %}
      * Bu gibi uygulamalarda kullandığımız ldap yapısına ait, bind user(dizinde arama/sorgu yapabilen sadece okuma yetkisi olan kullanıcı), kullanıcıların dizinde nerede bulunduğu, grupların dizinde nerede bulunduğunu girerek ldaptaki kullanıcı veya grupları kimlik doğrulama amacı ile kullanabiliriz.
      

  * sshd_config ayarları yapılarak güvenliği arttırılacak makine taratılır. İster uzak bir makineden ister kendisinden taratabiliriz.

    >ssh-audit localhost

![alt text](https://berkanterbey.github.io/images/002.png "ssh-audit komutunun çıktısı")

![alt text](https://berkanterbey.github.io/images/003.png "ssh-audit komutunun çıktısı")

  * Çıkan sonuca göre anahtar değişim algoritmalarında (KexAlgorithms), HostKeyAlgoritms de, kullanılan şifreleme algoritmalarında (ciphers) ve mesaj kimlik doğrulama kodlarında yeşille belirtilen algoritmalar güvenli olduğundan kalacak, sarı ve kırmızı olanlar sshd_config den çıkartılacak.

  * Ubuntu 20.04 Focal için örnek sshd_config dosyamız.

{% gist 9668e9b36b7ca93c1fb399369f41ae60 %}

## Ansible ile Otomasyon

  * Birden fazla sunucunun olduğu bir ortamda, teker teker bu ayarları dağıtmak çok fazla zaman alacağından **Ansible** ile dağıtacağız.

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
