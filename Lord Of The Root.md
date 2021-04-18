

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

<code>dirb http://192.168.56.104/1337 </code>

komutu çalıştırılmıştır.

![8](https://user-images.githubusercontent.com/32979760/115157993-ad6ae580-a094-11eb-9b54-0d622a0bab96.PNG)

ve çıktıdan görebileceğimiz gibi images klasörü bulunmuştur, images klasöründeki dosyalar indirilmiş fotoğrafların kontrast ayarlarıyla oynanmış exiftool ve binwalk ile incelenmiştir.Bu araştırmalardan herhangi bir sonuç elde edilememiştir.Her CTF'de kontrol edilmesi gereken sayfalardan birisi olan robots.txt'ye bakılmıştır.

![9](https://user-images.githubusercontent.com/32979760/115158146-7c3ee500-a095-11eb-9b45-17909bbb7b61.PNG)

Yukarıdaki çıktıda gördüğümüz gibi bizi yine bir fotoğraf karşılamaktadır ve sayfanın kaynak koduna bakılmıştır.

![10](https://user-images.githubusercontent.com/32979760/115158221-c7f18e80-a095-11eb-9922-1bc2baa26ef7.PNG)

ve çıktıda göreceğimiz üzere bir şeyler bulduk. 2 defa encode edilmiş base64 formatında görüyoruz bunları decode ediyoruz.

![11](https://user-images.githubusercontent.com/32979760/115158353-6978e000-a096-11eb-8116-c0e53f3953b3.PNG)

çıktıda bulduğumuz dizine gidiyoruz.

![12](https://user-images.githubusercontent.com/32979760/115158402-a04ef600-a096-11eb-9bcc-63fa18bd0910.PNG)

ve bizi mordorun kapıları karşılıyor :) .
Bu giriş sayfasında sql injection açığı olduğu düşünülmüştür ve gerekli testlere devam edilmiştir
Burpu çalıştırıyoruz intercepti aktif edip post isteği atıyoruz ve buradaki isteği kaydediyoruz.

![14](https://user-images.githubusercontent.com/32979760/115158581-882ba680-a097-11eb-8cf1-bb82d49f2071.PNG)

buradaki isteği kaydettikten sonra text editör ile açıyoruz

![15](https://user-images.githubusercontent.com/32979760/115158650-dc368b00-a097-11eb-8b65-d93c208f224c.PNG)

gördüğünüz gibi usertest yazısının sonuna * karakteri eklenmiştir.Bu burp için post isteğinin, payloadların nereye gönderileceği belirtilmiştir.Dosyayı kaydedip kapatıyoruz.

<code>sqlmap -r burpresult.txt(dosya adımız) --technique T --dbms mysql --dbs </code>

komutunu çalıştırıyoruz ve açığın var olduğunu görüp veritabanı isimlerini çekmeyi başlıyoruz.

![16](https://user-images.githubusercontent.com/32979760/115159382-8bc12c80-a09b-11eb-8a64-90496a8f0fc8.PNG)

Veritabanı isimlerine bakıldığında Webapp adlı veritabanının bilgileri çekileceği aşikardır.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T --tables -D Webapp </code>

![17](https://user-images.githubusercontent.com/32979760/115159498-12760980-a09c-11eb-9987-4817fbe2b799.PNG)
![18](https://user-images.githubusercontent.com/32979760/115159528-376a7c80-a09c-11eb-87ed-046d6005935c.PNG)

Tek tablo olan Users tablosunun içerisindeki kolonları çekmeye başlayalım ama önce kolon içerisindeki verileri çekmek için kolon isimlerini öğrenelim.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T -D Webapp -T Users --columns</code>
![19](https://user-images.githubusercontent.com/32979760/115159674-ffb00480-a09c-11eb-9055-972398caaeff.PNG)

burada bize lazım olan username ve password kolonları olduğu için oradaki verileri çekmeye başlıyoruz.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T -D Webapp -T Users -C username --dump </code>
  
![20](https://user-images.githubusercontent.com/32979760/115159839-c75cf600-a09d-11eb-9e06-8a69ee243808.PNG)

username bilgilerini çektik şimdi password bilgilerini çekelim.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T -D Webapp -T Users -C password --dump </code>


