

<img src="https://www.vulnhub.com/media/img/entry/watermarked/d1844af893edd2b0716dafa35a8172dc143c3911.png">

Ctf Download;
https://www.vulnhub.com/entry/sickos-12,144/

First of all, we find out which ip the machine has.


![1](https://user-images.githubusercontent.com/32979760/124518976-a7151b80-ddf0-11eb-8d20-2ed7fedd68b6.PNG)

In the screenshot below, we see the ip address of the machine.

![2](https://user-images.githubusercontent.com/32979760/124519211-4c2ff400-ddf1-11eb-9403-b1acd11c975e.PNG)

Then we run the following command using nmap.

![3](https://user-images.githubusercontent.com/32979760/124519278-7f728300-ddf1-11eb-89b6-275961b6f749.PNG)

Below we see the results.

![4](https://user-images.githubusercontent.com/32979760/124519353-b6489900-ddf1-11eb-870d-4a2f4650b41f.PNG)![12](https://user-images.githubusercontent.com/32979760/124520366-f1000080-ddf4-11eb-90e9-4d7841ac2982.PNG)


When we look at the screenshot above, http server is running on port 80. What are we waiting for? Let's go.

![5](https://user-images.githubusercontent.com/32979760/124519411-e7c16480-ddf1-11eb-84a6-aae415a054e8.PNG)

Keanu Reeves welcomes us. he's a john wick. he is a neo. he is a 47 ronin.Anyway, this has nothing to do with our topic, let's continue :D

![6](https://user-images.githubusercontent.com/32979760/124519563-5999ae00-ddf2-11eb-87f8-f75a34f25d5b.PNG)

We'll save the image and examine it.

![7](https://user-images.githubusercontent.com/32979760/124519757-e2b0e500-ddf2-11eb-8895-074086c6922d.PNG)

When we examine the image, we see that we cannot obtain any data.

now it's time to do directory exploration

![8](https://user-images.githubusercontent.com/32979760/124519815-2b689e00-ddf3-11eb-8885-02a3fe571f66.PNG)

We start searching directories with dirb.

![9](https://user-images.githubusercontent.com/32979760/124519884-610d8700-ddf3-11eb-84e3-4586340c1812.PNG)

As we saw above, we found 2 results. We will check with Nikto for vulnerability scanning.

![10](https://user-images.githubusercontent.com/32979760/124519973-adf15d80-ddf3-11eb-8770-6bce78fa6fee.PNG)

![11](https://user-images.githubusercontent.com/32979760/124520129-2f48f000-ddf4-11eb-821b-55842215803a.PNG)

Looking at the screenshot above, we couldn't find anything for the home directory. now we will scan the test directory.

![12](https://user-images.githubusercontent.com/32979760/124520391-0a08b180-ddf5-11eb-8bff-5ad0afed99dd.PNG)

Looking at the screenshot, the put method is allowed in the test directory. so it is possible to upload files here. We will try to upload a reverse shell.

i will use this.

https://github.com/pentestmonkey/php-reverse-shell

![13](https://user-images.githubusercontent.com/32979760/124520626-a763e580-ddf5-11eb-891f-9d108f90c887.PNG)

After downloading it, we have to enter our own ip address there.
You can change the port as you want.

![14](https://user-images.githubusercontent.com/32979760/124520849-5dc7ca80-ddf6-11eb-8d8b-20407d27b77a.PNG)

We upload the shell with curl.

![15](https://user-images.githubusercontent.com/32979760/124520940-9bc4ee80-ddf6-11eb-8dfb-ec6ee65e2405.PNG)

we have successfully uploaded the shell, let's open a shell connection immediately.

![16](https://user-images.githubusercontent.com/32979760/124521009-d038aa80-ddf6-11eb-917c-be579ec30a25.PNG)

Since I entered 4444 in the port variable in the shell, I have to open the connection with 4444.

![17](https://user-images.githubusercontent.com/32979760/124521300-af248980-ddf7-11eb-9b73-d98731ba620f.PNG)

When I visited http://192.168.56.102/test/reverse.php from the address bar, the shell connection was opened.

![18](https://user-images.githubusercontent.com/32979760/124521440-26f2b400-ddf8-11eb-866c-17242ba35626.PNG)

We need to be root.We detect kernel version and operating system version.

We find the appropriate exploit.
https://www.exploit-db.com/exploits/37292

![19](https://user-images.githubusercontent.com/32979760/124521646-fbbc9480-ddf8-11eb-8436-4badb48e1562.PNG)

we upload the exploit.

![20](https://user-images.githubusercontent.com/32979760/124522029-5d313300-ddfa-11eb-9c2e-e0a6bf0d54a7.PNG)

we see the exploit failed

We review the crondaily.

![21](https://user-images.githubusercontent.com/32979760/124522114-b8632580-ddfa-11eb-9289-82cf385ffd4d.PNG)

When we look here, we see that lighthttpd and chkrootkit services are running on a scheduled basis.
We're looking at the chkrootkit version.

![22](https://user-images.githubusercontent.com/32979760/124522212-1f80da00-ddfb-11eb-9aa5-bc4c565ba9c6.PNG)

We see that the version is 0.49

![23](https://user-images.githubusercontent.com/32979760/124522276-5bb43a80-ddfb-11eb-86f1-bcff8d03cd94.PNG)

We found the appropriate exploit.

Finally, after running the code below, we become root.

<code>echo 'chmod 777 /etc/sudoers && echo "www-data ALL=NOPASSWD: ALL"  /etc/sudoers && chmod 440 /etc/sudoers'  /tmp/update</code>


![16](https://user-images.githubusercontent.com/32979760/124590915-5939fb00-de64-11eb-92ae-919ab8252f7f.png)
