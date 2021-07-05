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

![4](https://user-images.githubusercontent.com/32979760/124519353-b6489900-ddf1-11eb-870d-4a2f4650b41f.PNG)

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

