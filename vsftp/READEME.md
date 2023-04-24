# vsftpd Porject

Step1:Download the project

git clone https://github.com/lgb861213/vsftpd.git

Step2: And then directly execute the docker build command to build the docker image


cd vsftpd

docker build --no-cache -t docker_image_name .

Step3: use the builded docker image create a new container

docker run -d --name container_name -p 21:21 docker_image_name


