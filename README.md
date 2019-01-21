# pyodbc_databricks
Informações de erro: SQLSTATE: 01000 Código: 0 Mensagem: [unixODBC] [Gerenciador de driver] Não é possível abrir lib 'ODBC Driver 17 para SQL Server': arquivo não encontrado
</br>
#instale o pip3 </br>
%sh</br>
sudo apt-get -y install python3-pip</br>
sudo pip install --upgrade pip</br>
sudo apt-get update</br>

#instalei via codigo o pyodb
%sh    
apt-get -y install unixodbc-dev
/databricks/python/bin/pip install pyodbc

# update do pyodbc
%sh 
sudo apt-get install python3-pip -y
pip3 install --upgrade pyodbc

#ver a versão do linus instalado
%sh
cat /etc/*-release


# copie o curl da sua versão no link https://docs.microsoft.com/en-us/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-2017

#instale
%sh

curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
  

sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev

#valida seu drive
%sh

odbcinst -j
odbcinst -q -d -n "ODBC Driver 17 for SQL Server"

#string de conexão
from sqlalchemy import create_engine
import pyodbc

params = urllib.parse.quote_plus("DRIVER={ODBC Driver 17 for SQL Server};SERVER=server;DATABASE=database;UID=user;PWD=password")
engine = create_engine("mssql+pyodbc:///?odbc_connect=%s" % params)

#insere os dados do seu pandas as ps dataframe para o SQL
df.to_sql('tabela', engine, if_exists='append')

print("Insert Concluido")

