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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="e47b2-103">Base de données Azure pour MySQL : utilisation de Python tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="e47b2-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="e47b2-104">Ce démarrage rapide montre comment toouse [Python](https://python.org) tooconnect tooan base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="e47b2-105">Il utilise tooquery d’instructions SQL, insertion, mise à jour et supprimer des données de base de données hello de plateformes Windows, Mac OS et Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="e47b2-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="e47b2-106">Hello dans cet article suppose que vous êtes familiarisé avec le développement à l’aide de Python et tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e47b2-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e47b2-107">Prerequisites</span></span>
<span data-ttu-id="e47b2-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="e47b2-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e47b2-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="e47b2-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="e47b2-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e47b2-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="e47b2-111">Installer Python et hello connecteur MySQL</span><span class="sxs-lookup"><span data-stu-id="e47b2-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="e47b2-112">Installer [Python](https://www.python.org/downloads/) et hello [connecteur MySQL pour Python](https://dev.mysql.com/downloads/connector/python/) sur votre propre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e47b2-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="e47b2-113">Selon votre plateforme, suivez les étapes de hello :</span><span class="sxs-lookup"><span data-stu-id="e47b2-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="e47b2-114">Windows</span><span class="sxs-lookup"><span data-stu-id="e47b2-114">Windows</span></span>
1. <span data-ttu-id="e47b2-115">Téléchargez et installez Python 2.7 sur [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="e47b2-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="e47b2-116">Vérifiez l’installation de Python hello en lançant l’invite de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="e47b2-117">Exécutez la commande hello `C:\python27\python.exe -V` à l’aide du numéro de version de hello majuscules V commutateur toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="e47b2-118">Installer le connecteur de Python hello pour MySQL à partir de [mysql.com](https://dev.mysql.com/downloads/connector/python/) tooyour correspond à la version de Python.</span><span class="sxs-lookup"><span data-stu-id="e47b2-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e47b2-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e47b2-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="e47b2-120">Sous Linux (Ubuntu), Python est généralement installé dans le cadre de l’installation par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="e47b2-121">Vérifiez l’installation de Python hello en lançant l’interpréteur de commandes bash hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="e47b2-122">Exécutez la commande hello `python -V` à l’aide du numéro de version de hello majuscules V commutateur toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="e47b2-123">Vérification de l’installation de PIP hello en exécutant hello `pip show pip -V` commande numéro de version toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="e47b2-124">PIP peut être inclus dans certaines versions de Python.</span><span class="sxs-lookup"><span data-stu-id="e47b2-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="e47b2-125">Si l’adresse PIP n’est pas installé, vous pouvez installer hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, en exécutant la commande `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="e47b2-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="e47b2-126">Mise à jour PIP toohello version la plus récente, en exécutant hello `pip install -U pip` commande.</span><span class="sxs-lookup"><span data-stu-id="e47b2-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="e47b2-127">Installer le connecteur de MySQL de hello pour Python et ses dépendances à l’aide des commandes PIP hello :</span><span class="sxs-lookup"><span data-stu-id="e47b2-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="e47b2-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="e47b2-128">MacOS</span></span>
1. <span data-ttu-id="e47b2-129">Sous Mac OS, Python est généralement installé dans le cadre de l’installation de système d’exploitation par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="e47b2-130">Vérifiez l’installation de Python hello en lançant l’interpréteur de commandes bash hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="e47b2-131">Exécutez la commande hello `python -V` à l’aide du numéro de version de hello majuscules V commutateur toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="e47b2-132">Vérification de l’installation de PIP hello en exécutant hello `pip show pip -V` commande numéro de version toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="e47b2-133">PIP peut être inclus dans certaines versions de Python.</span><span class="sxs-lookup"><span data-stu-id="e47b2-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="e47b2-134">Si l’adresse PIP n’est pas installé, vous pouvez installer hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span><span class="sxs-lookup"><span data-stu-id="e47b2-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="e47b2-135">Mise à jour PIP toohello version la plus récente, en exécutant hello `pip install -U pip` commande.</span><span class="sxs-lookup"><span data-stu-id="e47b2-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="e47b2-136">Installer le connecteur de MySQL de hello pour Python et ses dépendances à l’aide des commandes PIP hello :</span><span class="sxs-lookup"><span data-stu-id="e47b2-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="e47b2-137">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="e47b2-137">Get connection information</span></span>
<span data-ttu-id="e47b2-138">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="e47b2-139">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="e47b2-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e47b2-140">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e47b2-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e47b2-141">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez accroissant, tel que **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e47b2-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="e47b2-142">Cliquez sur le nom du serveur hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="e47b2-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="e47b2-143">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="e47b2-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="e47b2-144">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="e47b2-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e47b2-145">![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="e47b2-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="e47b2-146">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="e47b2-147">Exécuter du code Python</span><span class="sxs-lookup"><span data-stu-id="e47b2-147">Run Python Code</span></span>
- <span data-ttu-id="e47b2-148">Collez hello de code dans un fichier texte, enregistrez le fichier de hello dans un dossier du projet avec .py d’extension de fichier, tel que C:\pythonmysql\createtable.py ou /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="e47b2-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="e47b2-149">le code hello toorun, lancez l’invite de commandes hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="e47b2-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="e47b2-150">Basculez dans votre dossier de projet : `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="e47b2-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="e47b2-151">Puis tapez la commande de python hello suivi par nom de fichier hello `python createtable.py` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="e47b2-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="e47b2-152">Sur hello du système d’exploitation Windows, si python.exe est introuvable, vous pouvez fournir hello toohello de chemin complet de l’exécutable, ou ajouter le chemin d’accès de hello Python dans la variable d’environnement path hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="e47b2-153">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="e47b2-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="e47b2-154">Utilisez hello suivantes tooconnect toohello server de code, créer une table et chargez à l’aide de données hello un **insérer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="e47b2-155">Dans le code hello, bibliothèque de mysql.connector hello est importé.</span><span class="sxs-lookup"><span data-stu-id="e47b2-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="e47b2-156">Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e47b2-157">code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute la requête SQL hello par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="e47b2-158">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="e47b2-159">Lire les données</span><span class="sxs-lookup"><span data-stu-id="e47b2-159">Read data</span></span>
<span data-ttu-id="e47b2-160">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="e47b2-161">Dans le code hello, bibliothèque de mysql.connector hello est importé.</span><span class="sxs-lookup"><span data-stu-id="e47b2-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="e47b2-162">Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e47b2-163">code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute l’instruction SQL de hello par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="e47b2-164">les lignes de données de Hello sont lues à l’aide de hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) (méthode).</span><span class="sxs-lookup"><span data-stu-id="e47b2-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="e47b2-165">jeu de résultats Hello est conservé dans une ligne de la collection et d’un itérateur est tooloop utilisé sur les lignes hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="e47b2-166">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="update-data"></a><span data-ttu-id="e47b2-167">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="e47b2-167">Update data</span></span>
<span data-ttu-id="e47b2-168">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="e47b2-169">Dans le code hello, bibliothèque de mysql.connector hello est importé.</span><span class="sxs-lookup"><span data-stu-id="e47b2-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="e47b2-170">Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e47b2-171">code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute l’instruction SQL de hello par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="e47b2-172">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="delete-data"></a><span data-ttu-id="e47b2-173">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="e47b2-173">Delete data</span></span>
<span data-ttu-id="e47b2-174">Suivant de hello utilisation tooconnect de code et supprimer des données à l’aide un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e47b2-175">Dans le code hello, bibliothèque de mysql.connector hello est importé.</span><span class="sxs-lookup"><span data-stu-id="e47b2-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="e47b2-176">Hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) fonction est utilisée tooconnect tooAzure base de données MySQL à l’aide de hello [les arguments de connexion](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) dans la collection de configurations hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="e47b2-177">code de Hello utilise un curseur sur la connexion de hello, et [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) méthode s’exécute la requête SQL hello par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="e47b2-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="e47b2-178">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e47b2-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e47b2-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e47b2-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e47b2-180">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="e47b2-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
