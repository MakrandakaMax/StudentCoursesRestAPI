# StudentCoursesRestAPI
This Project consists of flask example with mysql connectivity

This project will be used to demonstrate APIs and Docker connectivity in the subsequent versions

## Architecture of the Application
![Preview](./images/StudentFlaskAppArchitecture.png)

## Steps
git clone https://github.com/MakrandakaMax/StudentCoursesRestAPI.git

cd StudentCoursesRestAPI

Dockerfile already included in StudentCoursesRestAPI folder:
FROM python:3.7-alpine
LABEL author=Max
ARG HOME_DIR='/studentcourses'
ADD . $HOME_DIR
ENV MYSQL_USERNAME='makrand'
ENV MYSQL_PASSWORD='password'
ENV MYSQL_SERVER='localhost'
ENV MYSQL_SERVER_PORT='3306'
ENV MYSQL_DATABASE='test'
EXPOSE 8080
WORKDIR $HOME_DIR
RUN pip install -r requirements.txt
ENTRYPOINT ["python", "app.py"] 

docker image build -t student:1.0 .

docker container run -d --name mysql -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=test -e MYSQL_USER=makrand -e MYSQL_PASSWORD=password mysql:5.6

docker inspect mysql | grep IPAddress

docker container run -d --name pythonapp -e MYSQL_SERVER=172.17.0.2 -p 8080:8080 student:1.0
