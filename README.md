# StudentCoursesRestAPI
This Project consists of flask example with mysql connectivity

This project will be used to demonstrate APIs and Docker connectivity in the subsequent versions

## Architecture of the Application
![Preview](./images/StudentFlaskAppArchitecture.png)

## Steps
git clone https://github.com/MakrandakaMax/StudentCoursesRestAPI.git

cd StudentCoursesRestAPI

docker image build -t student:1.0 .

docker container run -d --name mysql -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=test -e MYSQL_USER=makrand -e MYSQL_PASSWORD=password mysql:5.6

docker inspect mysql | grep IPAddress # to check the mysql ipaddress which most likely be 172.17.0.2

docker container run -d --name pythonapp -e MYSQL_SERVER=172.17.0.2 -p 8080:8080 student:1.0
