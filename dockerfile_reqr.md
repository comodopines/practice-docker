/
|---->myFolder/
|.     |---->app/
|.     |.     |----> main.py
|.     |
|.     |---->venv/
|.     |.     |----> main.py
|.     |
|.     |---->Dockerfile
|.     |---->requirements.txt

#Sample DockerFile
FROM python:3.8

#Create directory and move to it
WORKDIR /apps/myFolder

#Copy requriements.txt from the cur dir to WORKDIR
COPY requirements.txt .

#RUN copied requirements.txt with pip install
RUN pip install -r requirements.txt

#COPY the pwd./app to WORKDIR/app
COPY ./app ./app

CMD ["python", "./app/main.py"]

#####################
#BUILD the image
docker build -t <myImage> .

#Docker container image is created, run it
docker run <myImage>

#Docker container image is created, run it by port mapping. This port 8454 should be in your falsk app in app, port=8545, host="0.0.0.0"
docker run -p 5484:8454 <myImage>
 
 
 
