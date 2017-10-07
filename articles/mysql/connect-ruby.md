---
title: "Se connecter tooAzure de base de données de MySQL à l’aide de Ruby | Documents Microsoft"
description: "Ce démarrage rapide fournit plusieurs exemples de code Ruby vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="2f643-103">Base de données Azure pour MySQL : utilisez Ruby tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="2f643-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="2f643-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide un [Ruby](https://www.ruby-lang.org) application et hello [mysql2](https://rubygems.org/gems/mysql2) marque de plateformes Windows, Ubuntu Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="2f643-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="2f643-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="2f643-106">Cet article suppose que vous êtes familiarisé avec le développement à l’aide de Ruby, mais que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f643-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2f643-107">Prerequisites</span></span>
<span data-ttu-id="2f643-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="2f643-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2f643-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="2f643-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="2f643-110">Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2f643-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="2f643-111">Installer Ruby</span><span class="sxs-lookup"><span data-stu-id="2f643-111">Install Ruby</span></span>
<span data-ttu-id="2f643-112">Installez Ruby, de marque et de bibliothèque de MySQL2 hello sur votre propre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2f643-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="2f643-113">Windows</span><span class="sxs-lookup"><span data-stu-id="2f643-113">Windows</span></span>
1. <span data-ttu-id="2f643-114">Téléchargez et installez la version de hello 2.3 [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2f643-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="2f643-115">Lancez une nouvelle invite de commandes (cmd) à partir du menu Démarrer de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="2f643-116">Accédez au répertoire dans hello Ruby active pour la version 2.3.</span><span class="sxs-lookup"><span data-stu-id="2f643-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="2f643-117">Hello de test Ruby installation en exécutant la commande hello `ruby -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="2f643-118">Tester l’installation de marque hello en exécutant la commande hello `gem -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="2f643-119">Générer le module de hello Mysql2 pour Ruby à l’aide de la marque en exécutant la commande hello `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="2f643-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="2f643-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="2f643-120">MacOS</span></span>
1. <span data-ttu-id="2f643-121">Installer Ruby à l’aide de Homebrew en exécutant la commande hello `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="2f643-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="2f643-122">Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="2f643-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="2f643-123">Hello de test Ruby installation en exécutant la commande hello `ruby -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="2f643-124">Tester l’installation de marque hello en exécutant la commande hello `gem -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="2f643-125">Générer le module de hello Mysql2 pour Ruby à l’aide de la marque en exécutant la commande hello `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="2f643-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="2f643-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2f643-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="2f643-127">Installer Ruby en exécutant la commande hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="2f643-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="2f643-128">Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="2f643-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="2f643-129">Hello de test Ruby installation en exécutant la commande hello `ruby -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="2f643-130">Installer les dernières mises à jour de hello pour la marque en exécutant la commande hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="2f643-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="2f643-131">Tester l’installation de marque hello en exécutant la commande hello `gem -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="2f643-132">Installer hello gcc, la marque et autres outils de génération, en exécutant la commande hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="2f643-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="2f643-133">Installer les bibliothèques de développement hello MySQL client en exécutant la commande hello `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="2f643-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="2f643-134">Générer le module de mysql2 hello pour Ruby à l’aide de la marque en exécutant la commande hello `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="2f643-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="2f643-135">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="2f643-135">Get connection information</span></span>
<span data-ttu-id="2f643-136">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="2f643-137">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="2f643-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2f643-138">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2f643-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2f643-139">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez accroissant, tel que **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="2f643-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="2f643-140">Cliquez sur le nom du serveur hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="2f643-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="2f643-141">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="2f643-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="2f643-142">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="2f643-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2f643-143">![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="2f643-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="2f643-144">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="2f643-145">Exécuter le code Ruby</span><span class="sxs-lookup"><span data-stu-id="2f643-145">Run Ruby code</span></span> 
1. <span data-ttu-id="2f643-146">Collez hello Ruby code à partir des sections hello ci-dessous dans des fichiers texte et enregistrer des fichiers de hello dans un dossier de projet avec .rb d’extension de fichier, tel que `C:\rubymysql\createtable.rb` ou `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="2f643-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="2f643-147">le code hello toorun, lancez l’invite de commandes hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="2f643-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="2f643-148">Basculez dans votre dossier de projet `cd rubymysql`.</span><span class="sxs-lookup"><span data-stu-id="2f643-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="2f643-149">Puis tapez la commande hello ruby suivi par nom de fichier hello, tel que `ruby createtable.rb` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="2f643-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="2f643-150">Sur hello du système d’exploitation Windows, si l’application hello ruby n’est pas dans votre variable d’environnement path, vous devrez peut-être toouse hello chemin d’accès complet toolaunch hello nœud application tel que`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="2f643-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="2f643-151">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="2f643-151">Connect and create a table</span></span>
<span data-ttu-id="2f643-152">Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="2f643-153">code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="2f643-154">Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) plusieurs fois toorun hello DROP, CREATE TABLE, commandes et de INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="2f643-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="2f643-155">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="2f643-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f643-156">Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2f643-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a><span data-ttu-id="2f643-157">Lire les données</span><span class="sxs-lookup"><span data-stu-id="2f643-157">Read data</span></span>
<span data-ttu-id="2f643-158">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2f643-159">code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="2f643-160">Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) commandes SELECT de toorun hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="2f643-161">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="2f643-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f643-162">Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2f643-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a><span data-ttu-id="2f643-163">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="2f643-163">Update data</span></span>
<span data-ttu-id="2f643-164">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="2f643-165">code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="2f643-166">Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) commandes de mise à jour toorun hello.</span><span class="sxs-lookup"><span data-stu-id="2f643-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="2f643-167">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="2f643-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f643-168">Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2f643-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a><span data-ttu-id="2f643-169">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="2f643-169">Delete data</span></span>
<span data-ttu-id="2f643-170">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2f643-171">code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="2f643-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="2f643-172">Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) commandes DELETE de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="2f643-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="2f643-173">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="2f643-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f643-174">Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2f643-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a><span data-ttu-id="2f643-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f643-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2f643-176">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="2f643-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
