---
title: "Se connecter à Azure Database pour MySQL avec Python | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit plusieurs exemples de code Python, que vous pouvez utiliser pour vous connecter et interroger des données d’Azure Database pour MySQL."
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
ms.openlocfilehash: 4c3a2e65b83fab6fe5b8b7778782a747bb5e9cf9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-python-to-connect-and-query-data"></a><span data-ttu-id="5f16a-103">Azure Database pour MySQL : Utiliser Python pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="5f16a-103">Azure Database for MySQL: Use Python to connect and query data</span></span>
<span data-ttu-id="5f16a-104">Ce guide de démarrage rapide vous explique comment utiliser [Python](https://python.org) pour se connecter à une base de données Azure Database pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for MySQL.</span></span> <span data-ttu-id="5f16a-105">Il utilise des instructions SQL pour interroger, insérer, mettre à jour et supprimer des données de la base de données sur des plateformes Mac OS et Ubuntu Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="5f16a-105">It uses SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="5f16a-106">Cet article suppose que vous connaissez les bases du développement Python et que vous ne savez pas utiliser Azure Database pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f16a-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5f16a-107">Prerequisites</span></span>
<span data-ttu-id="5f16a-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="5f16a-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5f16a-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="5f16a-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="5f16a-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5f16a-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-the-mysql-connector"></a><span data-ttu-id="5f16a-111">Installer Python et le connecteur MySQL</span><span class="sxs-lookup"><span data-stu-id="5f16a-111">Install Python and the MySQL connector</span></span>
<span data-ttu-id="5f16a-112">Installez [Python](https://www.python.org/downloads/) et le [connecteur MySQL pour Python](https://dev.mysql.com/downloads/connector/python/) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5f16a-112">Install [Python](https://www.python.org/downloads/) and the [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="5f16a-113">Suivez les étapes correspondant à votre plateforme :</span><span class="sxs-lookup"><span data-stu-id="5f16a-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="5f16a-114">Windows</span><span class="sxs-lookup"><span data-stu-id="5f16a-114">Windows</span></span>
1. <span data-ttu-id="5f16a-115">Téléchargez et installez Python 2.7 sur [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="5f16a-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="5f16a-116">Vérifiez l’installation de Python en lançant l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="5f16a-116">Check the Python installation by launching the command prompt.</span></span> <span data-ttu-id="5f16a-117">Exécutez la commande `C:\python27\python.exe -V` à l’aide du commutateur V majuscule pour voir le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="5f16a-117">Run the command `C:\python27\python.exe -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="5f16a-118">Installez le connecteur Python pour MySQL correspondant à votre version de Python sur [mysql.com](https://dev.mysql.com/downloads/connector/python/).</span><span class="sxs-lookup"><span data-stu-id="5f16a-118">Install the Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding to your version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5f16a-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5f16a-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="5f16a-120">Sous Linux (Ubuntu), Python est généralement installé dans le cadre de l’installation par défaut.</span><span class="sxs-lookup"><span data-stu-id="5f16a-120">In Linux (Ubuntu), Python is typically installed as part of the default installation.</span></span>
2. <span data-ttu-id="5f16a-121">Vérifiez l’installation de Python en lançant l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="5f16a-121">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="5f16a-122">Exécutez la commande `python -V` à l’aide du commutateur V majuscule pour voir le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="5f16a-122">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="5f16a-123">Vérifier l’installation de PIP en exécutant la commande `pip show pip -V` pour voir le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="5f16a-123">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span> 
4. <span data-ttu-id="5f16a-124">PIP peut être inclus dans certaines versions de Python.</span><span class="sxs-lookup"><span data-stu-id="5f16a-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="5f16a-125">Si PIP n’est pas installé, vous pouvez installer le package [PIP] (https://pip.pypa.io/en/stable/installing/) en exécutant la commande `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="5f16a-125">If PIP is not installed, you may install the [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="5f16a-126">Passez à la dernière version de PIP en exécutant la commande `pip install -U pip`.</span><span class="sxs-lookup"><span data-stu-id="5f16a-126">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="5f16a-127">Installez le connecteur MySQL pour Python et ses dépendances à l’aide de la commande PIP :</span><span class="sxs-lookup"><span data-stu-id="5f16a-127">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="5f16a-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="5f16a-128">MacOS</span></span>
1. <span data-ttu-id="5f16a-129">Sous Mac OS, Python est généralement installé dans le cadre de l’installation par défaut du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="5f16a-129">In Mac OS, Python is typically installed as part of the default OS installation.</span></span>
2. <span data-ttu-id="5f16a-130">Vérifiez l’installation de Python en lançant l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="5f16a-130">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="5f16a-131">Exécutez la commande `python -V` à l’aide du commutateur V majuscule pour voir le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="5f16a-131">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="5f16a-132">Vérifier l’installation de PIP en exécutant la commande `pip show pip -V` pour voir le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="5f16a-132">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span>
4. <span data-ttu-id="5f16a-133">PIP peut être inclus dans certaines versions de Python.</span><span class="sxs-lookup"><span data-stu-id="5f16a-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="5f16a-134">Si PIP n’est pas installé, vous pouvez installer le package [PIP](https://pip.pypa.io/en/stable/installing/).</span><span class="sxs-lookup"><span data-stu-id="5f16a-134">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="5f16a-135">Passez à la dernière version de PIP en exécutant la commande `pip install -U pip`.</span><span class="sxs-lookup"><span data-stu-id="5f16a-135">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="5f16a-136">Installez le connecteur MySQL pour Python et ses dépendances à l’aide de la commande PIP :</span><span class="sxs-lookup"><span data-stu-id="5f16a-136">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="5f16a-137">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="5f16a-137">Get connection information</span></span>
<span data-ttu-id="5f16a-138">Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-138">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="5f16a-139">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5f16a-139">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5f16a-140">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5f16a-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5f16a-141">Dans le menu de gauche du Portail Azure, cliquez sur **Toutes les ressources** et recherchez le serveur que vous venez de créer, par exemple **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-141">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="5f16a-142">Cliquez sur le nom du serveur, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-142">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="5f16a-143">Sélectionnez la page **Propriétés** du serveur.</span><span class="sxs-lookup"><span data-stu-id="5f16a-143">Select the server's **Properties** page.</span></span> <span data-ttu-id="5f16a-144">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-144">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5f16a-145">![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5f16a-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5f16a-146">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5f16a-146">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="5f16a-147">Exécuter du code Python</span><span class="sxs-lookup"><span data-stu-id="5f16a-147">Run Python Code</span></span>
- <span data-ttu-id="5f16a-148">Collez le code dans un fichier texte et enregistrez le fichier dans un dossier de projet avec l’extension de fichier .py, par exemple C:\pythonmysql\createtable.py ou /home/username/pythonmysql/createtable.py.</span><span class="sxs-lookup"><span data-stu-id="5f16a-148">Paste the code into a text file, and save the file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="5f16a-149">Pour exécuter le code, lancez l’invite de commandes ou l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="5f16a-149">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="5f16a-150">Basculez dans votre dossier de projet : `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="5f16a-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="5f16a-151">Ensuite, tapez la commande Python suivie du nom de fichier pour exécuter l’application :`python createtable.py`.</span><span class="sxs-lookup"><span data-stu-id="5f16a-151">Then type the python command followed by the file name `python createtable.py` to run the application.</span></span> <span data-ttu-id="5f16a-152">Sur le système d’exploitation Windows, si python.exe est introuvable, vous pouvez fournir le chemin d’accès complet de l’exécutable ou ajouter le chemin d’accès de Python dans la variable d’environnement du chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="5f16a-152">On the Windows OS, if python.exe is not found, you may provide the full path to the executable, or add the Python path into the path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5f16a-153">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="5f16a-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="5f16a-154">Utilisez le code suivant pour vous connecter au serveur, créer une table et charger les données à l’aide d’une instruction SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-154">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="5f16a-155">Dans le code, la bibliothèque mysql.connector est importée.</span><span class="sxs-lookup"><span data-stu-id="5f16a-155">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="5f16a-156">La fonction [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) est utilisée pour se connecter à Azure Database pour MySQL à l’aide des [arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations.</span><span class="sxs-lookup"><span data-stu-id="5f16a-156">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5f16a-157">Le code utilise un curseur sur la connexion, et la méthode [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) exécute la requête SQL sur la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-157">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5f16a-158">Remplacez les paramètres `host`, `user`, `password` et `database` par les valeurs que vous avez spécifiées lorsque vous avez créé le serveur et la base de données.</span><span class="sxs-lookup"><span data-stu-id="5f16a-158">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
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

## <a name="read-data"></a><span data-ttu-id="5f16a-159">Lire les données</span><span class="sxs-lookup"><span data-stu-id="5f16a-159">Read data</span></span>
<span data-ttu-id="5f16a-160">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-160">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="5f16a-161">Dans le code, la bibliothèque mysql.connector est importée.</span><span class="sxs-lookup"><span data-stu-id="5f16a-161">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="5f16a-162">La fonction [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) est utilisée pour se connecter à Azure Database pour MySQL à l’aide des [arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations.</span><span class="sxs-lookup"><span data-stu-id="5f16a-162">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5f16a-163">Le code utilise un curseur sur la connexion, et la méthode [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) exécute l’instruction SQL sur la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-163">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> <span data-ttu-id="5f16a-164">Les lignes de données sont lues suivant la méthode [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html).</span><span class="sxs-lookup"><span data-stu-id="5f16a-164">The data rows are read using the [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="5f16a-165">Le jeu de résultats est conservé dans une ligne de la collection et un itérateur for est utilisé pour exécuter les lignes en boucle.</span><span class="sxs-lookup"><span data-stu-id="5f16a-165">The result set is kept in a collection row and a for iterator is used to loop over the rows.</span></span>

<span data-ttu-id="5f16a-166">Remplacez les paramètres `host`, `user`, `password` et `database` par les valeurs que vous avez spécifiées lorsque vous avez créé le serveur et la base de données.</span><span class="sxs-lookup"><span data-stu-id="5f16a-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
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

## <a name="update-data"></a><span data-ttu-id="5f16a-167">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="5f16a-167">Update data</span></span>
<span data-ttu-id="5f16a-168">Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-168">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="5f16a-169">Dans le code, la bibliothèque mysql.connector est importée.</span><span class="sxs-lookup"><span data-stu-id="5f16a-169">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="5f16a-170">La fonction [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) est utilisée pour se connecter à Azure Database pour MySQL à l’aide des [arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations.</span><span class="sxs-lookup"><span data-stu-id="5f16a-170">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5f16a-171">Le code utilise un curseur sur la connexion, et la méthode [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) exécute l’instruction SQL sur la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-171">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> 

<span data-ttu-id="5f16a-172">Remplacez les paramètres `host`, `user`, `password` et `database` par les valeurs que vous avez spécifiées lorsque vous avez créé le serveur et la base de données.</span><span class="sxs-lookup"><span data-stu-id="5f16a-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in the table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="5f16a-173">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="5f16a-173">Delete data</span></span>
<span data-ttu-id="5f16a-174">Utilisez le code suivant pour vous connecter et supprimer des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="5f16a-174">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="5f16a-175">Dans le code, la bibliothèque mysql.connector est importée.</span><span class="sxs-lookup"><span data-stu-id="5f16a-175">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="5f16a-176">La fonction [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) est utilisée pour se connecter à Azure Database pour MySQL à l’aide des [arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations.</span><span class="sxs-lookup"><span data-stu-id="5f16a-176">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5f16a-177">Le code utilise un curseur sur la connexion, et la méthode [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) exécute la requête SQL sur la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="5f16a-177">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5f16a-178">Remplacez les paramètres `host`, `user`, `password` et `database` par les valeurs que vous avez spécifiées lorsque vous avez créé le serveur et la base de données.</span><span class="sxs-lookup"><span data-stu-id="5f16a-178">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
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
    print("Something is wrong with the user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in the table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="5f16a-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f16a-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5f16a-180">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="5f16a-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
