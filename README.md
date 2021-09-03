# jmeter_docker_loadtest


docker pull vinsdocker/jmmaster
docker pull vinsdocker/jmserver


docker run -dit --name slave01 vinsdocker/jmserver /bin/bash
docker run -dit --name slave02 vinsdocker/jmserver /bin/bash
docker run -dit --name slave03 vinsdocker/jmserver /bin/bash
docker run -dit --name slave04 vinsdocker/jmserver /bin/bash
docker run -dit --name slave05 vinsdocker/jmserver /bin/bash
docker run -dit --name slave06 vinsdocker/jmserver /bin/bash

mkdir -p /app/loadtest/tests

docker run -it -v $PWD/tests:/jmeter/apache-jmeter-5.4/bin/tests vinsdocker/jmmaster /bin/bash


To see the IP:

docker inspect --format '{{ .Name }} => {{ .NetworkSettings.IPAddress }}' $(sudo docker ps -a -q)


Commands to be executed in the master container's jmeter/jmeter5.4.1/bin

jmeter -Jserver.rmi.ssl.disable=true -n -t tests/getOtp.jmx -l ./tests/csv_$(date +"%Y%m%d%H%M").csv -e -o ./tests/reports_$(date +"%Y%m%d%H%M") -R172.17.0.2,172.17.0.3,172.17.0.4

jmeter -Jserver.rmi.ssl.disable=true -n -t tests/Plan_purchase_API.jmx -l ./tests/csv_$(date +"%Y%m%d%H%M").csv -e -o ./tests/reports_$(date +"%Y%m%d%H%M") -R172.17.0.2,172.17.0.3,172.17.0.4





jmeter -Jserver.rmi.ssl.disable=true -n -t tests/getPlanList.jmx -l ./tests/get_planlist_csv_$(date +"%Y%m%d%H%M").csv -e -o ./tests/get_planlist_reports_$(date +"%Y%m%d%H%M") -R172.17.0.2,172.17.0.3,172.17.0.4





