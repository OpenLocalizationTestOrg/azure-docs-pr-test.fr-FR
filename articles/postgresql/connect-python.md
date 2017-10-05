---
title: "Se connecter à la base de données Azure pour PostgreSQL à partir de Python | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit un exemple de code Python que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: d682d94143fb9fd5e2c2a578c3cb0dcfa101462c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-python-to-connect-and-query-data"></a><span data-ttu-id="e662f-103">Base de données Azure pour PostgreSQL : Utilisation de Python pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="e662f-103">Azure Database for PostgreSQL: Use Python to connect and query data</span></span>
<span data-ttu-id="e662f-104">Ce guide de démarrage rapide vous explique comment utiliser [Python](https://python.org) pour se connecter à une base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e662f-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e662f-105">Il explique aussi comment utiliser des instructions SQL pour interroger, insérer, mettre à jour et supprimer des données de la base de données sur des plateformes Mac OS, Ubuntu Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="e662f-105">It also demonstrates how to use SQL statements to query, insert, update, and delete data in the database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="e662f-106">Cet article suppose que vous connaissez les bases du développement via Python, et que vous ne savez pas utiliser la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e662f-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e662f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e662f-107">Prerequisites</span></span>
<span data-ttu-id="e662f-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="e662f-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e662f-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="e662f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="e662f-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="e662f-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="e662f-111">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e662f-111">You also need:</span></span>
- <span data-ttu-id="e662f-112">Installation de [python](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e662f-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="e662f-113">Installation du package [pip](https://pip.pypa.io/en/stable/installing/) (déjà installé si vous utilisez des binaires Python 2 >=2.7.9 ou Python 3 >=3.4 téléchargés depuis [python.org](https://python.org)).</span><span class="sxs-lookup"><span data-stu-id="e662f-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-the-python-connection-libraries-for-postgresql"></a><span data-ttu-id="e662f-114">Installer des bibliothèques de connexions Python pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e662f-114">Install the Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="e662f-115">Installez le package [psycopg2](http://initd.org/psycopg/docs/install.html), qui vous permet de vous connecter et d’interroger la base de données.</span><span class="sxs-lookup"><span data-stu-id="e662f-115">Install the [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you to connect and query the database.</span></span> <span data-ttu-id="e662f-116">Il est [disponible sur PyPI](https://pypi.python.org/pypi/psycopg2/) sous la forme de package en [roue](http://pythonwheels.com/) et pour les plateformes courantes (Linux, OSX, Windows).</span><span class="sxs-lookup"><span data-stu-id="e662f-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in the form of [wheel](http://pythonwheels.com/) packages for the most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="e662f-117">Utilisez l’installation de pip pour obtenir la version binaire du module qui inclut toutes les dépendances.</span><span class="sxs-lookup"><span data-stu-id="e662f-117">Use pip install to get the binary version of the module including all the dependencies.</span></span>

1. <span data-ttu-id="e662f-118">Sur votre ordinateur, lancez une interface de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="e662f-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="e662f-119">Sur Linux, lancez l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="e662f-119">On Linux, launch the Bash shell.</span></span>
    - <span data-ttu-id="e662f-120">Sur macOS, lancez le Terminal.</span><span class="sxs-lookup"><span data-stu-id="e662f-120">On macOS, launch the Terminal.</span></span>
    - <span data-ttu-id="e662f-121">Sur Windows, lancez l’invite de commandes à partir du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="e662f-121">On Windows, launch the Command Prompt from the Start Menu.</span></span>
2. <span data-ttu-id="e662f-122">Veillez à utiliser la version la plus récente de pip en exécutant cette commande, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e662f-122">Ensure that you are using the most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="e662f-123">Exécutez la commande suivante pour installer le package psycopg2 :</span><span class="sxs-lookup"><span data-stu-id="e662f-123">Run the following command to install the psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="e662f-124">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="e662f-124">Get connection information</span></span>
<span data-ttu-id="e662f-125">Obtenez les informations de connexion requises pour vous connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e662f-125">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e662f-126">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e662f-126">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e662f-127">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e662f-127">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e662f-128">Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez **mypgserver-20170401** (le serveur que vous venez de créer).</span><span class="sxs-lookup"><span data-stu-id="e662f-128">From the left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (the server you just created).</span></span>
3. <span data-ttu-id="e662f-129">Cliquez sur le nom du serveur **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="e662f-129">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="e662f-130">Sélectionnez la page **Vue d’ensemble** du serveur, puis notez le **nom du serveur** et le **nom de connexion de l’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="e662f-130">Select the server's **Overview** page, and then make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e662f-131">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="e662f-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="e662f-132">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e662f-132">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="how-to-run-python-code"></a><span data-ttu-id="e662f-133">Comment exécuter du code Python</span><span class="sxs-lookup"><span data-stu-id="e662f-133">How to run Python code</span></span>
<span data-ttu-id="e662f-134">Cette rubrique contient un total de quatre exemples de code, qui effectuent chacun une fonction spécifique.</span><span class="sxs-lookup"><span data-stu-id="e662f-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="e662f-135">Les instructions suivantes expliquent comment créer un fichier texte, insérer un bloc de code, et enregistrer ce fichier pour pouvoir l’exécuter ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e662f-135">The following instructions indicate how to create a text file, insert a code block, and then save the file so that you can run it later.</span></span> <span data-ttu-id="e662f-136">Veillez à créer quatre fichiers différents, un pour chaque bloc de code.</span><span class="sxs-lookup"><span data-stu-id="e662f-136">Be sure to create four separate files, one for each code block.</span></span>

- <span data-ttu-id="e662f-137">Dans l’éditeur de texte que vous préférez, créez un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="e662f-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="e662f-138">Dans le fichier texte, copiez et collez un des exemples de code présents dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="e662f-138">Copy and paste one of the code samples in the following sections into the text file.</span></span> <span data-ttu-id="e662f-139">Remplacez les paramètres **host**, **dbname**, **user** et **password** par les valeurs spécifiées lors de la création du serveur et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e662f-139">Replace the **host**, **dbname**, **user**, and **password** parameters with the values that you specified when you created the server and database.</span></span>
- <span data-ttu-id="e662f-140">Enregistrez le fichier avec l’extension .py (par exemple postgres.py) dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="e662f-140">Save the file with the .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="e662f-141">Si vous êtes sous un système d’exploitation Windows, veillez à sélectionner l’encodage UTF-8 lors de l’enregistrement du fichier.</span><span class="sxs-lookup"><span data-stu-id="e662f-141">If you are running the Windows OS, be sure to select UTF-8 encoding when saving the file.</span></span> 
- <span data-ttu-id="e662f-142">Lancer l’invite de commande ou l’interpréteur de commandes Bash, puis modifiez le répertoire de votre dossier de projet, par exemple `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="e662f-142">Launch the Command Prompt or Bash shell and then change the directory to your project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="e662f-143">Pour exécuter le code, tapez la commande Python suivie du nom de fichier, par exemple `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="e662f-143">To run the code, type the Python command followed by the file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="e662f-144">À partir de Python version 3, il est possible que vous rencontriez l’erreur `SyntaxError: Missing parentheses in call to 'print'` lors de l’exécution des blocs de code suivants.</span><span class="sxs-lookup"><span data-stu-id="e662f-144">Starting in Python version 3, you may see the error `SyntaxError: Missing parentheses in call to 'print'` when running the following code blocks.</span></span> <span data-ttu-id="e662f-145">Dans ce cas, remplacez chaque appel à la commande `print "string"` par un appel de fonction avec parenthèses, par exemple `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="e662f-145">If that happens, replace each call to the command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="e662f-146">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="e662f-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="e662f-147">Utilisez le code suivant pour vous connecter et charger les données à l’aide de la fonction [psycopg2.connect](http://initd.org/psycopg/docs/connection.html), avec l’instruction SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="e662f-147">Use the following code to connect and load the data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="e662f-148">La fonction [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) est utilisée pour exécuter la requête SQL sur la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e662f-148">The [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used to execute the SQL query against PostgreSQL database.</span></span> <span data-ttu-id="e662f-149">Remplacez les paramètres host, dbname, user et password par les valeurs spécifiées lors de la création du serveur et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e662f-149">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="e662f-150">Une fois que le code s’exécute avec succès, la sortie s’affiche comme suit :</span><span class="sxs-lookup"><span data-stu-id="e662f-150">After the code runs successfully, the output appears as follows:</span></span>

![Sortie de ligne de commande](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="e662f-152">Lire les données</span><span class="sxs-lookup"><span data-stu-id="e662f-152">Read data</span></span>
<span data-ttu-id="e662f-153">Utilisez le code suivant pour lire les données insérées à l’aide de la fonction [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute), avec l’instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="e662f-153">Use the following code to read the data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="e662f-154">Cette fonction accepte une requête et renvoie un jeu de résultats qui peut être itéré à l’aide de [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="e662f-154">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="e662f-155">Remplacez les paramètres host, dbname, user et password par les valeurs spécifiées lors de la création du serveur et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e662f-155">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="e662f-156">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="e662f-156">Update data</span></span>
<span data-ttu-id="e662f-157">Utilisez le code suivant pour mettre à jour la ligne d’inventaire que vous avez insérée précédemment à l’aide de la fonction [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) et de l’instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="e662f-157">Use the following code to update the inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="e662f-158">Remplacez les paramètres host, dbname, user et password par les valeurs spécifiées lors de la création du serveur et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e662f-158">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in the table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="e662f-159">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="e662f-159">Delete data</span></span>
<span data-ttu-id="e662f-160">Utilisez le code suivant pour supprimer une ligne d’inventaire que vous avez insérée précédemment à l’aide de la fonction [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) et de l’instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="e662f-160">Use the following code to delete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="e662f-161">Remplacez les paramètres host, dbname, user et password par les valeurs spécifiées lors de la création du serveur et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e662f-161">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="e662f-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e662f-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e662f-163">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="e662f-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
