

İndirme Linki; https://www.vulnhub.com/entry/lord-of-the-root-101%2C129/

Lab kurulumunu tamamladıktan sonra sanal makinenin ip adresini bulmak için

<code>netdiscover -i eth1 -r 192.168.56/24 </code>  komutunu çalıştırıyoruz.
![1](https://user-images.githubusercontent.com/32979760/115157062-e6548b80-a08f-11eb-845a-7d17f1ce0738.PNG)

![2](https://user-images.githubusercontent.com/32979760/115157080-f66c6b00-a08f-11eb-9f61-bde36fe19ada.PNG)

Yukarıda çıktıya baktığımızda sanal makinenin ip adresini bulmuş olduk.Şimdi gelecek adımda nmap taraması yapacağız.

<code>nmap -T5 -A -n 192.168.56.104 </code> 

komutunu çalıştırıyoruz

![3](https://user-images.githubusercontent.com/32979760/115157157-5cf18900-a090-11eb-900d-553683414dcc.PNG)

Çıktıdan anlaşılacağı üzere ssh servisinin açık olduğunu görüyoruz ve ssh bağlantısı kurmaya çalışıyoruz.
<code>ssh root@192.168.56.104</code>
komutunu çalıştırıyorum.

![4](https://user-images.githubusercontent.com/32979760/115157220-b8bc1200-a090-11eb-83e9-e240c7105d88.PNG)

Çıktıya baktığımızda port knocking işlemi yapmamız gerektiği mesajı verilmiştir.

Buradaki python toolu indirilmiştir; https://github.com/grongor/knock

<code>./knock.py 192.168.56.104 1 2 3 </code>

komutunu çalıştırıyoruz ve portları knockluyoruz.

![5](https://user-images.githubusercontent.com/32979760/115157381-9a0a4b00-a091-11eb-89eb-efa0e17613c0.PNG)

Ve tekrar nmap ile tarama yapıyoruz.

<code>nmap -T5 -sS -A -n 192.168.56.104 --top-ports 1000 </code>

komutunu çalıştırıyoruz.

![6](https://user-images.githubusercontent.com/32979760/115157471-10a74880-a092-11eb-8c46-fcd3378537c4.PNG)

Çıktıda görüleceği üzere 1337. portun açık olduğu görülmüştür ve web sitesi ziyaret edilmiştir.

![7](https://user-images.githubusercontent.com/32979760/115157551-99be7f80-a092-11eb-86cd-4f44efa4fbd6.PNG)

Web sitesini ziyaret ettiğimizde bir fotoğraf ve üzerinde yüzüğü mordora götüreceğim diye bir yazı yazmaktadır.
Sitenin kaynak koduna bakıldığında sadece fotoğrafın tek satırlık img srcsi görülmüştür bu sayfadan bir şey elde edemeyeceğimiz anlaşılmıştır ve dizin keşfine geçilmiştir.




