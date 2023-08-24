# 2048_game
  
                                               Hosting a web game on ngninx 

Pre-requisites : 
* Visual studio or any terminal ( I would prefer visual studio for clear and easy view )
* Docker
* Source code url : https://github.com/gabrielecirulli/2048

-------------------------------------------------------------------------------------------------------------------------------------

1. Create a New folder named as 2048 and create a new Dockerfile in it.

2. Run these commands in the Dockerfile.
   
    ![Screenshot from 2023-08-24 14-12-42](https://github.com/RajasekharVadapalli/2048_game/assets/142224224/776ce4d5-4a5d-40d3-9d37-f14cffb31f27)

   FROM - It is used to pull your required image from DockerHub
   
   RUN apt-get update - This command is used to update the package index files on the system, which contain information about available packages and their versions
   
   RUN apt-get install  -y nginx zip curl - To install nginx, zip, curl on docker container
   
   RUN echo "daemon off;" >>/etc/nginx/nginx.conf - To add into the configuration file																															
   
   RUN curl -o /var/www/html/master.zip -L https://github.com/gabrielecirulli/2048/archive/refs/heads/master.zip - Used to download the contents from git repo to local zip folder
   
   RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip - Here it's basically unzipping into master.zip folder and move all conents to /var/www/html/
   ( master.zip is the default zip file from source git repo )
   
   EXPOSE 80 - It is exposing on port 80 but itself in the container ( we need to port forward it to 80:80 )

   CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"] - It is to run the config file from its location /usr/sbin/nginx

4. Build a Docker image and name it as 2048-game
   
    ![Screenshot from 2023-08-24 14-41-29](https://github.com/RajasekharVadapalli/2048_game/assets/142224224/89e0f3cf-bf30-4a10-a522-26a9f598b85b)
       ( I have already built the image so showing as cached, nothing to worry. It should work if not raise issue on this repo )

5. You can check your docker images by using docker images. Run docker image by using this command ( docker run -d -p 80:80 54dc5883a5e8 )
    ![Screenshot from 2023-08-24 14-52-09](https://github.com/RajasekharVadapalli/2048_game/assets/142224224/7d26a817-2988-4d34-925f-4b96beb78f21)
         ( here -p is used to port forward inside container to outside by 80:80 as mentioned above and 54dc5883a5e8 is my image id ( you can use tag instead of image id as well ) )

6. Hurrah..... ! That's it. ( you can check by going on your browser http://localhost:80 )
   ![Screenshot 2023-08-24 at 14-58-33 2048](https://github.com/RajasekharVadapalli/2048_game/assets/142224224/e7f2840b-89e4-437e-908b-eb4ef9f05344)



   





   
   
   
