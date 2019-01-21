# pyodbc_databricks
Informações de erro: SQLSTATE: 01000 Código: 0 Mensagem: [unixODBC] [Gerenciador de driver] Não é possível abrir lib 'ODBC Driver 17 para SQL Server': arquivo não encontrado
</br></br>
# instale o pip3 </br></br>
%sh</br>
sudo apt-get -y install python3-pip</br>
sudo pip install --upgrade pip</br>
sudo apt-get update</br></br>

# instalei via codigo o pyodb</br></br>
%sh    </br>
apt-get -y install unixodbc-dev</br>
/databricks/python/bin/pip install pyodbc</br></br>

# update do pyodbc</br></br>
%sh </br>
sudo apt-get install python3-pip -y</br>
pip3 install --upgrade pyodbc</br></br>

# ver a versão do linus instalado</br></br>
%sh</br>
cat /etc/*-release</br></br>


# copie o curl da sua versão no link https://docs.microsoft.com/en-us/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-2017</br></br></br></br></br>

# instale o drive do sql</br></br>
%sh</br>

curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -</br>
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list</br></br>
  

sudo apt-get update</br>
sudo ACCEPT_EULA=Y apt-get install msodbcsql17</br>
</br></br>
sudo ACCEPT_EULA=Y apt-get install mssql-tools</br>
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile</br>
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc</br>
source ~/.bashrc</br></br>
sudo apt-get install unixodbc-dev</br></br></br>

# valida seu drive</br></br>
%sh</br>

odbcinst -j</br>
odbcinst -q -d -n "ODBC Driver 17 for SQL Server"</br></br>

# string de conexão</br></br>
from sqlalchemy import create_engine</br>
import pyodbc</br></br>

params = urllib.parse.quote_plus("DRIVER={ODBC Driver 17 for SQL Server};SERVER=server;DATABASE=database;UID=user;PWD=password")</br>
engine = create_engine("mssql+pyodbc:///?odbc_connect=%s" % params)</br></br>

# insere os dados do seu pandas as ps dataframe para o SQL</br>
df.to_sql('tabela', engine, if_exists='append')</br></br>

print("Insert Concluido")</br></br>

