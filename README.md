# solr_task_csvdata_to_solr

->created new container in docker name- Apache jupyter,Done the neccessary installation and updates 

apt-get upgrade <br>
apt-get update <br>
apt install python3 <br>
apt install python3-pip <br>
pip3 install jupyter <br>
jupyter notebook --ip=0.0.0.0 -port=8888 --allow -root <br>

->installing solr on docker container 

wget https://www.apache.org/dyn/closer.lua/lucene/solr/8.11.2/solr-8.11.2.tgz?action=download <br>
mv solr-8.11.2.tgz\?action\=download solr-8.11.2.tgz <br>
tar zxf solr-8.11.2.tgz <br>
cd solr-8.11.2 <br>
apt-get install openjdk-8-jre <br>
cd bin <br>
./solr start –force <br>
./solr create -c test1 -force <br>

->using jupyter notebook sending csv data to solr server(python) <br>

pip install requests <br>
import requests <br>


solr_url = "http://localhost:8983/solr/test1/update/csv?separator=%3B&commit=true" <br>

headers = { <br>
    "Content-type": "text/csv" <br>
} <br>

data = open("Tests.csv",mode='rb') <br>

response = requests.post(solr_url, headers=headers, data=data) <br>

if response.status_code != 200: <br>
    print("Error sending data to Solr") <br>
else: <br>
    print("Data sent to Solr successfully") <br>
