#par-1
#creating docker container

docker run -d --name infra infracloudio/csvserver:latest

docker logs container_id

#i found thise error while reading the file "/csvserver/inputdata": open /csvserver/inputdata: no such file 

#i created gensv.sh 

./gensv.sh > inputFIle

chmod 555 inputFile (read,execute)

docker run -d -v /opt/inputFile:/csvserver/inputdata/ --name infra infracloudio/csvserver

docker ps
docker stop infra
docker rm infra

docker -d -v /opt/inputFile:/csvserver/inputdata -p 9393:9300 --name infra infracloudio/csvserver

#successfully runing

docker -d -v /opt/inputFile:/csvserver/inputdata -p 9393:9300 -e CSVSERVER_BORDER=orange --name infra infracloudio/csvserver

http://52.66.149.223:9393/

#i can see 10 csv s on browser

wget -O ./part-1-output http://localhost:9393/raw
docker logs [container_id] >& part-1-logs
