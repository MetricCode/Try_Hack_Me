# @author : M3tr1c_r00t
This is a medium ranked room which deals with smd which helps us in getting the login creds and finally gain root priviledges.
![Screenshot_2022-11-10_13_25_43](https://user-images.githubusercontent.com/99975622/201920574-c01f1e89-64d2-4e16-9cac-ff994c81039d.png)

so were gonna start by **Enumaration** as always :)  .....
**NB** I split the scripts to show the output of the scan 
![Screenshot_2022-11-10_12_47_07](https://user-images.githubusercontent.com/99975622/201922194-87e52b35-ece0-4284-8303-18847c003357.png)

Well, there were a couple of ports open so and some which caught my eye are ftp and 445 smb
And we can see that on ftp anonymous login is allowed.
So we can use the username ftp/ anonmyous and any password it doesnt matter and we'll be logged in right through.

![Screenshot_2022-11-10_12_53_51](https://user-images.githubusercontent.com/99975622/201924904-ef984079-55ee-4dea-be3a-f6dca97b6a3d.png)
I downloaded all the files in the script folder and go through them.

![Screenshot_2022-11-10_12_55_09](https://user-images.githubusercontent.com/99975622/201925728-3e0c6d56-3067-4bbd-bf61-d056f9cbf31d.png)
We're gonna use ftp to get out reverse shell and gain priviledges but i wanna go through smb and basically how we can use it as a possible vulnerability.So we're gonna use enum4linux to get info on the service.

![Screenshot_2022-11-10_13_01_03](https://user-images.githubusercontent.com/99975622/201925976-689e032b-5561-4640-b0a3-2e9a888bdb1d.png)
 adn we find a pics share which we might be able to access and view its contents using smbclient.
 ![Screenshot_2022-11-10_13_01_06](https://user-images.githubusercontent.com/99975622/201926190-658ba806-4a8b-4047-9f4f-7950b479bf50.png)

Well, we find some of pics. Lets get them and see if we can find anything interesting.
![Screenshot_2022-11-10_13_05_36](https://user-images.githubusercontent.com/99975622/201926335-b8c1682a-71b9-4b96-9e46-f80b7e318009.png)
You can analyse files that you get here and find something that can help you.

Lets go back to getting a reverse shell.
According to the clean.sh file, i can guess that its being executed by a cronjob to be regularly checking for files in the /tmp/ directory and delete it.
\n
So i renamed the clean.sh file to clean1.sh and created a new clean.sh file, put a reverse shell one -liner script in it, made it executable and uploaded it to the ftp server using put command.

![Screenshot_2022-11-10_13_13_53](https://user-images.githubusercontent.com/99975622/201929836-fe302824-9d2c-46f6-8448-726f10ebbe69.png)
next up...
![Screenshot_2022-11-10_13_14_46](https://user-images.githubusercontent.com/99975622/201930079-74fccd4c-34e8-4c9f-9d49-c4f462097cd2.png)
 Next, open up a netcat listener on the port you assigned and then wait for a few seconds and you get a reverse shell!
 ![Screenshot_2022-11-10_13_15_14](https://user-images.githubusercontent.com/99975622/201930411-efd21e3d-6a0c-4b35-8f6b-888778f83aec.png)
 And we get a reverse shell.
 I tried to check the crontab and sudo -l priviledges but no luck.
 And we go and get linpeas....
 Connected to linpeas using a python http.server and curl command.
 
![Screenshot_2022-11-10_13_17_55](https://user-images.githubusercontent.com/99975622/201930883-9e6e20da-beb3-435c-b643-58b5fdf11cc8.png)

And i get the CVE-2021-4034 which is an exploit for pwnkit.
I used a python script to gain access after uploading it to the remote machine using python http server, executed it and i became root.
![Screenshot_2022-11-10_13_18_25](https://user-images.githubusercontent.com/99975622/201932268-042b7bde-7d21-483a-bd46-da9b6455c1de.png)

You can get the python script on github tho i cant remember the repo. Just google "pwnkit python script github" and youll find it .
![Screenshot_2022-11-10_13_20_01](https://user-images.githubusercontent.com/99975622/201932322-8b08f385-085f-43f6-8317-8122ebcec55b.png)


and here's root!
![Screenshot_2022-11-10_13_22_36](https://user-images.githubusercontent.com/99975622/201932633-5f2e85bd-cdeb-4fe9-a371-374410f4a2e6.png)

