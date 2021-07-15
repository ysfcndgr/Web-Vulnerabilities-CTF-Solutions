<img src="https://www.vulnhub.com/media/img/entry/watermarked/c6edb628ba708851fef8a8e99a862164393d7829.png">

Download; https://www.vulnhub.com/entry/sectalks-bne0x03-simple,141/

![1](https://user-images.githubusercontent.com/32979760/125840714-b93dfa98-e837-4e4b-badc-a1ab7138b08f.PNG)

We scan the machine with nmap.
When we look at the results, the http service is running on port 80. let's request then.

![2](https://user-images.githubusercontent.com/32979760/125840880-20a6b6ae-56f6-40ac-bb4e-94f080866025.PNG)

We use nikto.When we look at the results, we see the docs directory and license.txt.
We will use dirb for directory discovery

![3](https://user-images.githubusercontent.com/32979760/125841318-20c95fb0-5070-40dc-9d7b-ff7718c18173.PNG)

![4](https://user-images.githubusercontent.com/32979760/125841454-5f07b47d-08d9-4ebb-a7d3-aa1ef72370d5.PNG)

We look at the license.txt file and see that cutePhP is used there and see if there is an exploit associated with it.

![5](https://user-images.githubusercontent.com/32979760/125841494-2e8cff7c-c37c-4ce3-8730-5e00d5188334.PNG)

We found the exploit, now we are doing the necessary steps.

![6](https://user-images.githubusercontent.com/32979760/125841594-bdd82bf3-2dee-489e-9335-18963adea1f1.PNG)

We register

![7](https://user-images.githubusercontent.com/32979760/125841648-7b3730a7-04bb-44a1-bb0a-00176924da45.PNG)

We see the file upload page above.Now. We save the php reverse shell file as rev.jpeg and open burpsuite while doing this.

![8](https://user-images.githubusercontent.com/32979760/125841892-75989766-7d87-4763-8666-01a3217827dc.PNG)

We are making the necessary adjustments for the reverse shell.

![9](https://user-images.githubusercontent.com/32979760/125842119-f3c3b0f4-53b6-4afe-be95-4f4cae73f3b9.PNG)

We change the rev.jpeg file to rev.php.
We go to the uploads directory.

![9](https://user-images.githubusercontent.com/32979760/125841956-1937dd5c-6b29-409a-965f-0459018a07b8.PNG)

We can see that we have uploaded.



![10](https://user-images.githubusercontent.com/32979760/125842223-f73785c3-7ce5-49c8-92aa-c221c6587b64.PNG)

We open a reverse connection with nc.



![12](https://user-images.githubusercontent.com/32979760/125842349-66c5ab17-e562-4d5d-a2ae-f0f1f420707f.PNG)

When we click on the file we uploaded to the uploads directory, we get a connection.

![11](https://user-images.githubusercontent.com/32979760/125842683-1d36ea61-f30a-4de1-b9e1-de4e6ec1b6e1.PNG)

I use the exploit in the screenshot above to become root.

![13](https://user-images.githubusercontent.com/32979760/125842923-f832051c-2ed6-4055-981f-885dbc7d3c74.PNG)

I see that I am root.

![14](https://user-images.githubusercontent.com/32979760/125842992-ca71c0ca-09b9-4989-87bc-6e123d6ccea1.PNG)

I read the flag.txt in the root directory and the ctf ends there.


