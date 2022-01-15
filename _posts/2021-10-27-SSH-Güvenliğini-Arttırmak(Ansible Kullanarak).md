---
published: true
---




## Giriş
  * Merhaba, Bu yazımda **ssh-audit** aracıyla hedef makinedeki ssh bağlantı güvenliği açıklarını bulup, açıkları kapamak için gereken değişiklikleri **Ansible** ile yapacağız.

## .sshd_config ve ssh_config Arasındaki Fark?
  * sshd nin açılımı ssh daemondur. SSH Portuna gelen bağlantıları dinler. sshd_config bulunduğumuz makineye gelen bağlantıları karşılamada kullanılan ayarlardır.
  * ssh_config de ise ssh istemcisi için yapılan ayarlar bulunur. Yani ssh_config başka makinelere bağlanırken kullanılan ayarlar içindir.

## ssh-audit ile Açıkları Bulmak

  * ssh-audit kurulur.
{% gist f831cf512355fd37bcc2b1c3f54f518c %}

  * sshd_config ayarları yapılarak güvenliği arttırılacak makine taratılır. İster uzak bir makineden ister kendisinden taratabiliriz.

    >ssh-audit localhost
  
* Çıkan sonuca göre anahtar değişim algoritmalarında (KexAlgorithms), HostKeyAlgoritms de, kullanılan şifreleme algoritmalarında (ciphers) ve mesaj kimlik doğrulama kodlarında yeşille belirtilen algoritmalar güvenli olduğundan kalacak, sarı ve kırmızı olanlar sshd_config den çıkartılacak.

  * Ubuntu 20.04 Focal için örnek sshd_config dosyamız.

{% gist 9668e9b36b7ca93c1fb399369f41ae60 %}

## Ansible ile Otomasyon

  * Birden fazla sunucunun olduğu bir ortamda, teker teker bu ayarları dağıtmak çok fazla zaman alacağından **Ansible** ile dağıtacağız.

  * Ansible ile dağıtırken her işletim sistemi sürümüne göre desteklenen algoritmalarda değişiklikler olabilir. Bundan dolayı playbook umuza sunucuların işletim sistemini bakıp, sadece Ubuntu 20.04 (focal) için çalışacak şekilde ayarlanacak. Dilerseniz farklı işletim sistemlerinide benzer yöntemle ekleyebilirsiniz.

  * Aşağıdaki ekran görüntüsünde host02.txt dosyasında belirtilen makinelerde işletim sistemi kod adı bilgisine ulaşıyoruz.

{% gist 713f9e1675998fea47d7a05bdb636e2f %}

  * Yapacağımız işlemi kısaca özetlersek
    * sshd_config hedef makineye kopyalamak (var olan izin ve sahiplikleri koruyarak)
    * sshd_config de belirtilen hostkeyleri **yoksa oluşturmak**
    * ssh servisini yeniden başlatmak (**değişiklik olmuşsa**)


{% gist b9fb9c07d373289ad40fc671c30ced24 %}

  * Yazdığımız kodu derleyip çalıştırılabilir dosya haline getiriyoruz. 



Bir sonraki yazımızda görüşmek üzere ;)
