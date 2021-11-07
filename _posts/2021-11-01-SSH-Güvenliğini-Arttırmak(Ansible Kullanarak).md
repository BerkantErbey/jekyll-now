---
published: true
---




## Giriş
  * Bu yazımda **ssh-audit** aracıyla hedef makinedeki ssh bağlantı güvenliği açıklarını bulup, açıkları kapamak için gereken değişiklikleri **Ansible** ile yapacağız.

## .sshd_config ve ssh_config Arasındaki Fark?
  * sshd nin açılımı ssh daemondur. SSH Portuna gelen bağlantıları dinler. sshd_config bulunduğumuz makineye gelen bağlantıları karşılamada kullanılan ayarlardır.
  * ssh_config de ise ssh istemcisi için yapılan ayarlar bulunur. Yani ssh_config başka makinelere bağlanırken kullanılan ayarlar içindir.

## ssh-audit ile Açıkları Bulmak

  * ssh-audit kurulur.
{% gist f831cf512355fd37bcc2b1c3f54f518c %}

  * sshd_config ayarları yapılarak güvenliği arttırılacak makine taratılır. İster uzak bir makineden ister kendisinden taratabiliriz.

    >ssh-audit localhost

![alt text](https://berkanterbey.github.io/images/002.png "ssh-audit komutunun çıktısı")

![alt text](https://berkanterbey.github.io/images/003.png "ssh-audit komutunun çıktısı")

  * Çıkan sonuca göre anahtar değişim algoritmalarında (KexAlgorithms), HostKeyAlgoritms de, kullanılan şifreleme algoritmalarında (ciphers) ve mesaj kimlik doğrulama kodlarında yeşille belirtilen algoritmalar güvenli olduğundan kalacak, sarı ve kırmızı olanlar sshd_config den çıkartılacak.

  * Birden fazla sunucunun olduğu bir ortamda, teker teker bu ayarları dağıtmak çok fazla zaman alacağından **Ansible** ile dağıtacağız.

  * Ansible ile dağıtırken her işletim sistemi sürümüne göre desteklenen algoritmalarda değişiklikler olabilir. Bundan dolayı playbook umuza sunucuların işletim sistemini bakıp, sadece Ubuntu 20.04 (focal) için çalışacak şekilde ayarlanacak. Dilerseniz farklı işletim sistemlerinide benzer yöntemle ekleyebilirsiniz.

  * Yapacağımız işlemi kısaca özetlersek
    * sshd_config hedef makineye kopyalamak (var olan izin ve sahiplikleri koruyarak)
    * sshd_config de belirtilen hostkeyleri **yoksa oluşturmak**
    * ssh servisini yeniden başlatmak (**değişiklik olmuşsa**)



  
* Ubuntu 20.04 Focal için örnek sshd_config dosyamız.

{% gist 385c8c1ef4c298e69d764f1456895dd1 %}


## .deb Paketi Nasıl Oluşturulur?

  * Öncelikle çalıştırılabilir bir dosyaya ihtiyacımız var. C dilinde ufak bir program yazıp onu derleyeceğim.

{% gist b9fb9c07d373289ad40fc671c30ced24 %}

  * Yazdığımız kodu derleyip çalıştırılabilir dosya haline getiriyoruz. 

```shell
# Derleme
gcc random.c -o random
# Oluşan dosyanın tipi
file random
>random: ELF 64-bit LSB pie executable,...
```


  * Yükleme dizinini oluşturup ilgili düzenlemeleri yapıyoruz. (/usr/local/bin olarak seçiyorum)

![alt text](https://berkanterbey.github.io/images/003.png "ssh-audit komutunun çıktısı")



```shell
# DEBIAN dizini ve yükleme dizini oluşturulur.
mkdir -p random_1.21-3.amd64/DEBIAN
mkdir -p random_1.21-3.amd64/usr/local/bin

cp control random_1.21-3.amd64/DEBIAN/
cp random random_1.21-3.amd64/usr/local/bin/
# Alttaki komut çalıştıktan sonra random_1.21-3.amd64.deb isimli paket oluşur.
dpkg-deb --build --root-owner-group random_1.21-3.amd64
```


## .deb Paketinin Kurulumu

  * Oluşturduğumuz .deb uzantılı paketi kuralım.

```shell
# dpkg ile .deb uzantılı paketi yüklüyoruz sistemimize.
sudo dpkg -i random_1.21-3.amd64

# Programının yüklenip yüklenmediğini anlamak için
which random
>/usr/bin/random
random
>Random number is 93
```

Bir sonraki yazımızda görüşmek üzere ;)
