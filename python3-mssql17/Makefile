PYTHON_IMAGE_NAME=centos8-mssql

DOCKER_NETWORK=test-mssql

MSSQL_CONTAINER_NAME=mssql
MSSQL_PASSWORD=Test123!!!

PYTHON_CONTAINER_NAME=python-pyodbc-mssql17

all: mssql-run mssql-exec build run connect exec

mssql-run:
	docker run --name ${MSSQL_CONTAINER_NAME} -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=${MSSQL_PASSWORD}" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest
	echo Started MSSQL Server

mssql-exec:
	echo Run the following to create a database MYDB
	echo >1 CREATE DATABASE MYDB
	echo >2 GO
	echo >1
	docker exec -it ${MSSQL_CONTAINER_NAME} /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P ${MSSQL_PASSWORD}

build:
	docker build -t ${PYTHON_IMAGE_NAME} .
	echo Built ${PYTHON_IMAGE_NAME}

run:
	docker run -v ${PWD}/src:/app -d --rm --name ${PYTHON_CONTAINER_NAME} ${PYTHON_IMAGE_NAME} tail -f /dev/null

connect:
	docker network create ${DOCKER_NETWORK}
	docker network connect ${DOCKER_NETWORK} ${MSSQL_CONTAINER_NAME}
	docker network connect ${DOCKER_NETWORK} ${PYTHON_CONTAINER_NAME}

exec:
	docker exec -it ${PYTHON_CONTAINER_NAME} /bin/bash

clean:
	docker rm -f ${MSSQL_CONTAINER_NAME} ${PYTHON_CONTAINER_NAME}
	docker network rm ${DOCKER_NETWORK}
