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
found nothing interesting to me so i went to the smb 445 and used enum4linux to get info on the service.

![Screenshot_2022-11-10_13_01_03](https://user-images.githubusercontent.com/99975622/201925976-689e032b-5561-4640-b0a3-2e9a888bdb1d.png)
 adn we found a pics share which we might be able to access and view its contents usign smbclient.
 ![Screenshot_2022-11-10_13_01_06](https://user-images.githubusercontent.com/99975622/201926190-658ba806-4a8b-4047-9f4f-7950b479bf50.png)

Well, we find some of pics. Lets get them and see if we can find anything interesting.
![Screenshot_2022-11-10_13_05_36](https://user-images.githubusercontent.com/99975622/201926335-b8c1682a-71b9-4b96-9e46-f80b7e318009.png)
Screenshot_2022-11-10_12_53_51.png
