# Infracloudio
## Part1

Run the docker container with below command and you will get error as below
```sh
docker run infracloudio/csvserver
# error while reading the file "/csvserver/inputdata": open/csvserver/inputdata: no such file or directory
```

For resolve this error we need to create inputFile in csvserver/solution/ with the help of gencsv.sh so lets create.
First we need Clone code infracloudio/csvserver/
```sh
git clone https://github.com/infracloudio/csvserver.git 
```

Go to csvserver/solution dir and create gencsv.sh file 
```sh
cd  /root/assignment/csvserver/solution/ 
```

Create gencsv.sh as below 
```sh
     vim gencsv.sh
     #!/bin/bash
     for i in {1..10}
     do
       A=$i
       B=$RANDOM
       C="$A,$B"
       echo $C >> inputFile
     done

```

Run the gencsv.sh script which will genrate inputFile
```sh
./gencsv.sh
```

InputFile is created now run docker container to resolved issue
```sh
docker run -v /root/assignment/csvserver/solution/inputFile:/csvserver/inputdata -d --name part1 infracloudio/csvserver:latest
```

Now the container is up and running so we can check Port inside the contaiener or port column in docker ps command output as below
```sh 
docker ps 
  #output >>78e83b008a8   infracloudio/csvserver:latest   "/csvserver/csvserver"   3 seconds ago   Up 2 seconds   9300/tcp   part1
```
Now we need to port map here to 9300 and also set environment variable CSVSERVER-BORDER to have value Orange 

```sh
docker run -p 9393:9300 -e CSVSERVER_BORDER=Orange -v /root/assignment/csvserver/solution/inputFile:/csvserver/inputdata -d --name part1 infracloudio/csvserver:latest
 ```
Now we can verify it 
```sh 
curl localhost:9393
```
your server address in your browser.
```sh
localhost:9393
```
