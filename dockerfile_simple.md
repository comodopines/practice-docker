/
|---->/apps
|.     |---->main.py
|.     |---->Dockerfile

#Dockerfile structure
1) FROM
2) ADD
   COPY
3) RUN
4) CMD

#Create docker Image
docker build -t <myImage> .

#Run the docker image
docker run <myImage>

#If you have interactive image
docker run -it <myImage>

What ahppens underneath
1) FROM commands pulls the packages from docker.io/library/python:3.8@sha
2) ADD commands adds files to working directory in container - copy a file
3) RUN command runs commands on the fly - like pip install
X) Image builds
|.     |---->main.py Image gets exported where
|.     |---->each of the above layer gets exported and written to image
|.     |---->image gets named to docker.io/library/<myImage>

4) CMD is used when we run - dockere run <myImage>

####Sample Dockerfile
FROM python:3.8
ADD main.py .
RUN pip install requests, beautifulsoup4
CMD [ "python", "./main.py" ]

