---
title: "Se connecter tooAzure de base de données de MySQL à partir de Python | Documents Microsoft"
description: "Ce démarrage rapide fournit que du code Python plusieurs exemples que vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Base de données Azure pour MySQL : utilisation de Python tooconnect et interroger des données
Ce démarrage rapide montre comment toouse [Python](https://python.org) tooconnect tooan base de données Azure pour MySQL. Il utilise tooquery d’instructions SQL, insertion, mise à jour et supprimer des données de base de données hello de plateformes Windows, Mac OS et Ubuntu Linux. Hello dans cet article suppose que vous êtes familiarisé avec le développement à l’aide de Python et tooworking nouvelle base de données Azure pour MySQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>Installer Python et hello connecteur MySQL
Installer [Python](https://www.python.org/downloads/) et hello [connecteur MySQL pour Python](https://dev.mysql.com/downloads/connector/python/) sur votre propre ordinateur. Selon votre plateforme, suivez les étapes de hello :

### <a name="windows"></a>Windows
1. Téléchargez et installez Python 2.7 sur [python.org](https://www.python.org/downloads/windows/). 
2. Vérifiez l’installation de Python hello en lançant l’invite de commandes hello. Exécutez la commande hello `C:\python27\python.exe -V` à l’aide du numéro de version de hello majuscules V commutateur toosee hello.
3. Installer le connecteur de Python hello pour MySQL à partir de [mysql.com](https://dev.mysql.com/downloads/connector/python/) tooyour correspond à la version de Python.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Sous Linux (Ubuntu), Python est généralement installé dans le cadre de l’installation par défaut de hello.
2. Vérifiez l’installation de Python hello en lançant l’interpréteur de commandes bash hello. Exécutez la commande hello `python -V` à l’aide du numéro de version de hello majuscules V commutateur toosee hello.
3. Vérification de l’installation de PIP hello en exécutant hello `pip show pip -V` commande numéro de version toosee hello. 
4. PIP peut être inclus dans certaines versions de Python. Si l’adresse PIP n’est pas installé, vous pouvez installer hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, en exécutant la commande `sudo apt-get install python-pip`.
5. Mise à jour PIP toohello version la plus récente, en exécutant hello `pip install -U pip` commande.
6. Installer le connecteur de MySQL de hello pour Python et ses dépendances à l’aide des commandes PIP hello :

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. Sous Mac OS, Python est généralement installé dans le cadre de l’installation de système d’exploitation par défaut hello.
2. Vérifiez l’installation de Python hello en lançant l’interpréteur de commandes bash hello. Exécutez la commande hello `python -V` à l’aide du numéro de version de hello majuscules V commutateur toosee hello.
3. Vérification de l’installation de PIP hello en exécutant hello `pip show pip -V` commande numéro de version toosee hello.
4. PIP peut être inclus dans certaines versions de Python. Si l’adresse PIP n’est pas installé, vous pouvez installer hello [PIP](https://pip.pypa.io/en/stable/installing/) package.
5. Mise à jour PIP toohello version la plus récente, en exécutant hello `pip install -U pip` commande.
6. Installer le connecteur de MySQL de hello pour Python et ses dépendances à l’aide des commandes PIP hello :

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez accroissant, tel que **myserver4demo**.
3. Cliquez sur le nom du serveur hello **myserver4demo**.
4. Serveur hello sélectionnez **propriétés** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-python/1_server-properties-name-login.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.
   

## <a name="run-python-code"></a>Exécuter du code Python
- Collez hello de code dans un fichier texte, enregistrez le fichier de hello dans un dossier du projet avec .py d’extension de fichier, tel que C:\pythonmysql\createtable.py ou /home/username/pythonmysql/createtable.py
- le code hello toorun, lancez l’invite de commandes hello ou bash shell. Basculez dans votre dossier de projet : `cd pythonmysql`. Puis tapez la commande de python hello suivi par nom de fichier hello `python createtable.py` application hello de toorun. Sur hello du système d’exploitation Windows, si python.exe est introuvable, vous pouvez fournir hello toohello de chemin complet de l’exécutable, ou ajouter le chemin d’accès de hello Python dans la variable d’environnement path hello. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Se connecter, créer des tables et insérer des données
Utilisez hello suivantes tooconnect toohello server de code, créer une table et chargez à l’aide de données hello un **insérer** instruction SQL. 

Dans le code hello, bibliothèque de mysql.connector hello est importé. Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello. code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute la requête SQL hello par rapport à la base de données MySQL. 

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. 

Dans le code hello, bibliothèque de mysql.connector hello est importé. Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello. code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute l’instruction SQL de hello par rapport à la base de données MySQL. les lignes de données de Hello sont lues à l’aide de hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) (méthode). jeu de résultats Hello est conservé dans une ligne de la collection et d’un itérateur est tooloop utilisé sur les lignes hello.

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a>Mettre à jour des données
Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL. 

Dans le code hello, bibliothèque de mysql.connector hello est importé.  Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello. code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute l’instruction SQL de hello par rapport à la base de données MySQL. 

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a>Suppression de données
Suivant de hello utilisation tooconnect de code et supprimer des données à l’aide un **supprimer** instruction SQL. 

Dans le code hello, bibliothèque de mysql.connector hello est importé.  Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello. code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute la requête SQL hello par rapport à la base de données MySQL. 

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./concepts-migrate-import-export.md)
