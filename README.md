# Get access to unlimited MySQL Servers with ONE phpMyAdmin (PMA) instance
<p align="center">
  <img width="586" alt="Capture d’écran 2022-07-08 à 23 37 26" src="https://user-images.githubusercontent.com/55393279/178075007-ac16ced8-73be-499b-8ec3-8079cc3d3f9e.png">
</p>


## Config I use

MacBook Pro M1 2020 <br>
Docker version 20.10.17, build 100c701 <br>
docker-compose version 1.29.2, build 5becea4c <br>
docker-compose file version 3.9 <br>

## Run it
* Copy .env.example file to .env
* Type the command ```docker-compose up -d```. It will automatically download images, create containers, volumes and network. If you have this error : ```ERROR: no matching manifest for linux/arm64/v8 in the manifest list entries```, you probably need to uncomment ```platform: linux/x86_64```.

## Explanation
By specifying ```PMA_HOSTS``` && ```PMA_PORTS``` environment variables to PMA, it will understand that we have more than one server.<br>
<a href="https://github.com/phpmyadmin/docker/blob/master/apache/config.inc.php#L59">Here</a> is how it work
![pma_conf](https://user-images.githubusercontent.com/55393279/178077464-356a6b30-bbb0-4fc3-8659-0c348b7bb2eb.png)
then it will automatically combine the MySQL host and the MySQL port.
![pma_conf2](https://user-images.githubusercontent.com/55393279/178078198-49560824-56bd-4f48-b221-48431032061a.png) <br>

For user authentication, if you don't specify ```PMA_USER``` && ```PMA_PASSWORD```, the user and the password will be ```MYSQL_USER``` && ```MYSQL_PASSWORD``` environment variables defined in each MySQL services in docker compose. <br>
<img width="586" alt="Capture d’écran 2022-07-08 à 23 37 43" src="https://user-images.githubusercontent.com/55393279/178079030-0cc83ffd-5e0c-4b5c-9590-25611e4de2b7.png">

We are here on the same docker compose, but il can also easily work if not. You just need to defined (like I did) the same network on each docker-compose (or pass the --network argument in a docker run command).
