# solr_task_csvdata_to_solr

#->created new container in docker name- Apache jupyter,Done the neccessary installation and updates 

# apt-get upgrade
# apt-get update
apt install python3
apt install python3-pip
pip3 install jupyter
jupyter notebook --ip=0.0.0.0 -port=8888 --allow -root

->installing solr on docker container 

wget https://www.apache.org/dyn/closer.lua/lucene/solr/8.11.2/solr-8.11.2.tgz?action=download
mv solr-8.11.2.tgz\?action\=download solr-8.11.2.tgz
tar zxf solr-8.11.2.tgz
cd solr-8.11.2
apt-get install openjdk-8-jre
cd bin
./solr start –force
./solr create -c test1 -force

->using jupyter notebook sending csv data to solr server(python)

pip install requests
import requests


solr_url = "http://localhost:8983/solr/test1/update/csv?separator=%3B&commit=true"

headers = {
    "Content-type": "text/csv"
}

data = open("Tests.csv",mode='rb')

response = requests.post(solr_url, headers=headers, data=data)

if response.status_code != 200:
    print("Error sending data to Solr")
else:
    print("Data sent to Solr successfully")
