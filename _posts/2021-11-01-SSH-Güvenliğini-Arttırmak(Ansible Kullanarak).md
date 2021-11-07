---
published: false
---

## Giriş
  * Bu yazımda ssh-audit aracıyla hedef makinedeki ssh bağlantı güvenliği açıklarını bulup, açıkları kapamak için gereken değişiklikleri Ansible ile yapacağız.

## .sshd_config ve ssh_config Arasındaki Fark?
  * sshd nin açılımı ssh daemondur. SSH Portuna gelen bağlantıları dinler. sshd_config bulunduğumuz makineye gelen bağlantıları karşılamada kullanılan ayarlardır.
  ssh_config de ise ssh istemcisi için yapılan ayarlar bulunur. Yani ssh_config başka makinelere bağlanırken kullanılan ayarlar içindir.

## .deb Paketleri Hakkında Genel Bilgi

  * .deb paketleri control(paket hakkında temel bilgiler) dosyası ve yükleme öncesi ve sonrası betikler(postrm,postinst,prerm,preinst) ve yükleme dizininden oluşur. Yükleme dizini linux dosya sistemindeki gibi olmalıdır. Yani /usr/bin /usr/sbin /usr/local/bin /opt gibi.

  * control dosyasının içeriği

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
