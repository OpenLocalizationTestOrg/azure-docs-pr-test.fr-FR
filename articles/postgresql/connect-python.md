---
title: "Se connecter tooAzure de base de données pour PostgreSQL à partir de Python | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code Python que vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour PostgreSQL."
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
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="ec45d-103">Base de données Azure pour PostgreSQL : utilisation de Python tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="ec45d-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="ec45d-104">Ce démarrage rapide montre comment toouse [Python](https://python.org) tooconnect tooan base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="ec45d-105">Il montre également comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer les données dans la base de données hello macOS, Ubuntu Linux et les plateformes Windows.</span><span class="sxs-lookup"><span data-stu-id="ec45d-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="ec45d-106">Hello dans cet article suppose que vous êtes familiarisé avec le développement à l’aide de Python et tooworking nouvelle base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec45d-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ec45d-107">Prerequisites</span></span>
<span data-ttu-id="ec45d-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="ec45d-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="ec45d-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="ec45d-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="ec45d-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="ec45d-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="ec45d-111">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ec45d-111">You also need:</span></span>
- <span data-ttu-id="ec45d-112">Installation de [python](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ec45d-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="ec45d-113">Installation du package [pip](https://pip.pypa.io/en/stable/installing/) (déjà installé si vous utilisez des binaires Python 2 >=2.7.9 ou Python 3 >=3.4 téléchargés depuis [python.org](https://python.org)).</span><span class="sxs-lookup"><span data-stu-id="ec45d-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="ec45d-114">Installer les bibliothèques de connexions de Python hello pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ec45d-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="ec45d-115">Installer hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, ce qui vous permet de tooconnect et requête de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="ec45d-116">psycopg2 est [disponible sur PyPI](https://pypi.python.org/pypi/psycopg2/) sous forme de hello de [roue](http://pythonwheels.com/) packages pour les plateformes de hello courants (Linux, OS x, Windows).</span><span class="sxs-lookup"><span data-stu-id="ec45d-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="ec45d-117">Utilisez pip installez tooget hello version binaire module hello, y compris toutes les dépendances de hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="ec45d-118">Sur votre ordinateur, lancez une interface de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="ec45d-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="ec45d-119">Sur Linux, lancez l’interpréteur de commandes Bash hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="ec45d-120">Sur Mac OS, lancez hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="ec45d-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="ec45d-121">Sur Windows, lancez hello invite de commandes à partir du Menu Démarrer de hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="ec45d-122">Assurez-vous que vous utilisez une version plus récente hello pip en exécutant une commande comme :</span><span class="sxs-lookup"><span data-stu-id="ec45d-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="ec45d-123">Exécutez hello suivant package psycopg2 de commande tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="ec45d-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="ec45d-124">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="ec45d-124">Get connection information</span></span>
<span data-ttu-id="ec45d-125">Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="ec45d-126">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="ec45d-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ec45d-127">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ec45d-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ec45d-128">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez **mypgserver-20170401** (serveur vous venez de créer pour hello).</span><span class="sxs-lookup"><span data-stu-id="ec45d-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="ec45d-129">Cliquez sur le nom du serveur hello **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="ec45d-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="ec45d-130">Serveur hello sélectionnez **vue d’ensemble** page et notez hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="ec45d-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="ec45d-131">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="ec45d-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="ec45d-132">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="ec45d-133">Comment toorun code Python</span><span class="sxs-lookup"><span data-stu-id="ec45d-133">How toorun Python code</span></span>
<span data-ttu-id="ec45d-134">Cette rubrique contient un total de quatre exemples de code, qui effectuent chacun une fonction spécifique.</span><span class="sxs-lookup"><span data-stu-id="ec45d-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="ec45d-135">Hello instructions suivantes indiquent comment toocreate un fichier texte, insérer un bloc de code, puis enregistrez le fichier de hello afin que vous pouvez l’exécuter ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ec45d-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="ec45d-136">Être vraiment toocreate quatre fichiers distincts, un pour chaque bloc de code.</span><span class="sxs-lookup"><span data-stu-id="ec45d-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="ec45d-137">Dans l’éditeur de texte que vous préférez, créez un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="ec45d-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="ec45d-138">Copiez et collez un des exemples de code hello dans les sections suivantes dans le fichier de texte hello de hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="ec45d-139">Remplacez hello **hôte**, **dbname**, **utilisateur**, et **mot de passe** paramètres avec des valeurs hello que vous avez spécifié lors de la création de hello serveur et base de données.</span><span class="sxs-lookup"><span data-stu-id="ec45d-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="ec45d-140">Enregistrez-le hello avec l’extension de .py hello (par exemple postgres.py) dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="ec45d-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="ec45d-141">Si vous exécutez hello du système d’exploitation Windows, être vraiment tooselect codage UTF-8 lors de l’enregistrement du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ec45d-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="ec45d-142">Lancer l’environnement d’invite de commandes ou un interpréteur de commandes hello et modifiez hello tooyour projet répertoire, par exemple `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="ec45d-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="ec45d-143">le code hello toorun, hello de type commande Python suivi par nom de fichier hello, par exemple `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="ec45d-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="ec45d-144">À partir de Python version 3, vous pouvez voir l’erreur de hello `SyntaxError: Missing parentheses in call too'print'` hello suivant des blocs de code lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="ec45d-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="ec45d-145">Si cela se produit, remplacez chaque commande de toohello appel `print "string"` avec un appel de fonction à l’aide de parenthèses, tel que `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="ec45d-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="ec45d-146">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="ec45d-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="ec45d-147">Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) fonctionne avec **insérer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="ec45d-148">Hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="ec45d-149">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ec45d-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

<span data-ttu-id="ec45d-150">Une fois que le code de hello s’exécute avec succès, hello sortie apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec45d-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Sortie de ligne de commande](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="ec45d-152">Lire les données</span><span class="sxs-lookup"><span data-stu-id="ec45d-152">Read data</span></span>
<span data-ttu-id="ec45d-153">Les données de salutation tooread insérées à l’aide de code de suivant de hello utilisation [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) fonctionne avec **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="ec45d-154">Cette fonction accepte une requête et retourne un ensemble de résultats pouvant être itéré sur avec utilisation hello de [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="ec45d-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="ec45d-155">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ec45d-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

## <a name="update-data"></a><span data-ttu-id="ec45d-156">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="ec45d-156">Update data</span></span>
<span data-ttu-id="ec45d-157">Ligne de l’inventaire de hello tooupdate que vous avez inséré précédemment à l’aide de code de suivant de hello utilisation [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) fonctionne avec **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="ec45d-158">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ec45d-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="ec45d-159">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="ec45d-159">Delete data</span></span>
<span data-ttu-id="ec45d-160">Toodelete un élément d’inventaire que vous avez inséré précédemment à l’aide de code suivant de hello utilisation [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) fonctionne avec **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="ec45d-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="ec45d-161">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ec45d-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

## <a name="next-steps"></a><span data-ttu-id="ec45d-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec45d-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ec45d-163">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="ec45d-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
