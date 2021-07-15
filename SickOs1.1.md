<img src="https://www.vulnhub.com/media/img/entry/watermarked/cbd2ae104def568317fa3350532afcf70add7f41.png">

Download Ctf Box = https://www.vulnhub.com/entry/sickos-11,132/

We scanning the machine with nmap

![1](https://user-images.githubusercontent.com/32979760/124984005-6102c680-e041-11eb-84bc-ca799a9c9106.PNG)

![2](https://user-images.githubusercontent.com/32979760/124984233-9f988100-e041-11eb-84f1-19e449e2cb28.PNG)

We look at the scan results.We see that port 3128 is open.

![3](https://user-images.githubusercontent.com/32979760/125792930-58c38a0e-fa8b-463a-8a1f-6d0a9319e096.PNG)

we're scanning this place with nikto

![4](https://user-images.githubusercontent.com/32979760/125793099-1910a96b-102a-4cf6-9a13-165de21b4352.PNG)

We get the page with curl.

![5](https://user-images.githubusercontent.com/32979760/125793280-f6bada55-e091-40a5-ac20-959e8239d78c.PNG)

We use the above payload to exploit shellshock.

![6](https://user-images.githubusercontent.com/32979760/125793419-1d6d26dc-8d55-460a-9ffe-fd54292d6174.PNG)

then we can inspect the crontab and become root.
