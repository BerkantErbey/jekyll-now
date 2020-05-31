---
published: true
---



## Terminalde Alarm Kurmak


Bu yazıda Terminalde alarm kurmak isteseydik bunu nasıl yapardık sorularının cevabını vereceğim bu yazıda.

Kimi zaman süre tutmaya ihtiyacımız olur bilgisayar kullanırken. Bu gibi durumlarda telefondan ya da websitesi ya da bir uygulamadan alarm kurmak yerine terminali kullanabiliriz.

Temel olarak mantığımız belirli bir süre bekleyip ses çalmak olacak. Bunun için terminaldeki “**sleep**” komutunu kullanacağız. Ses çalmak içinde terminalden çalışabilen herhangi bir medya oynatıcıyı kullanacağız.

	sleep 5s
    
Sleep komutundan sonra yazdığımız parametre bekleyeceğimiz süreyi belirtiyor.

s->saniye , m->dakika h->saat

Terminalde iki komutu birlikte çalıştırabilmek için “**&&**” kullanacağız

	command1 && command2
    
Medya oynatıcı olarak “**mpv**” yi kullanacağım. Öncelikle “mpv” yi yükleyelim.
“mpv” nin bulunduğu paketin adresini kendi güncelleme listelerimize eklemeliyiz.
	
    sudo add-apt-repository ppa:mc3man/mpv-tests
	sudo apt update && sudo apt install mpv
    
“mpv” yi yükledik. “mpv” nin çalışma şekli
	
    mpv filename
    
Şimdi iki komutumuzu beraber çalıştıralım

	sleep 25m && mpv alarm.ogg
    
25 dakika sonra çalmasını istediğimiz ses dosyası çalacak. Terminalde alarm kurmak bu kadar basit.
