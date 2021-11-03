
#creating docker container

docker run -d --name infra infracloudio/csvserver:latest

docker logs container_id

#i found thise error while reading the file "/csvserver/inputdata": open /csvserver/inputdata: no such file 

#i created gensv.sh 

./gensv.sh > inputFIle

chmod 555 inputFile (read,execute)

docker run -d -v /opt/inputFile:/csvserver/inputdata/ --name infra infracloudio/csvserver

docker ps

docker -d -v /opt/inputFile:/csvserver/inputdata -p 9393:9300 --name infra infracloudio/csvserver

#successfully runing

docker -d -v /opt/inputFile:/csvserver/inputdata -p 9393:9300 -e CSVSERVER_BORDER=orange --name infra infracloudio/csvserver

#http://52.66.149.223:9393/
#i can see 10 csv s on browser
#wget -O ./part-1-output http://localhost:9393/raw
#docker logs [container_id] >& part-1-logs



#part -2



docker rm $(docker ps -aq)

#one service that is csvserver

vi docker-compse.yml 

docker-compose up -d

# http://52.66.149.223:9393 

#part -3

docker rm $(docker ps -aq)

#i add promotheus service to docker-compose-part3

# i configure promotheus.yml located /etc/promotheus/promotheus.yml
# under static-configs  -targets[ 52.66.149.223:9393/metrics]

# 52.66.149.223:9090

#i pass querry csvserver_records 

# it shows ===> csvserver_records{csv_identifier="Y3N2c2VydmVyIGdlbmVyYXRlZCBhdDogMTYzNTkzNzQ4Nw==", instance="52.66.149.223:9393", job="csvserver-monitor"}
#10 













