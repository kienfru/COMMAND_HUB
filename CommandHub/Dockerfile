
#sudo vim dockerfile


FROM jenkins/jenkins:lts

USER root

RUN apt-get update && \
    apt-get install -y wget unzip && \
    wget https://releases.hashicorp.com/terraform/1.5.2/terraform_1.5.2_linux_amd64.zip && \
    unzip terraform_1.5.2_linux_amd64.zip && \
    mv terraform /usr/local/bin/ && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm terraform_1.5.2_linux_amd64.zip


USER jenkins


EXPOSE 8080


ENTRYPOINT ["/usr/local/bin/jenkins.sh"]






######################################################################################

 # to build an image from the file
docker build -t terrajens .  

#run a container from the image
docker run -d -p 8080:8080 --name myjenkins terrajens 

#once inside a jenkins container, you need to switch to rootuser to bypass privilage 
#so that you can run commands
docker exec -it -u root myjenkins bash

# to tag an image before pushing it to dockerhub
docker tag terrajens:latest kienche/terrajens:latest

docker push kienche/terrajens:latest
