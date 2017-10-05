---
title: "Se connecter à la base de données Azure pour PostgreSQL à l’aide de Ruby | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit un exemple de code Ruby, que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 9153a5a843dd5c18f27a3af232fea3b152240fe1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="05daa-103">Base de données Azure pour PostgreSQL : Utilisation de Ruby pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="05daa-103">Azure Database for PostgreSQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="05daa-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour PostgreSQL en utilisant une application [Ruby](https://www.ruby-lang.org).</span><span class="sxs-lookup"><span data-stu-id="05daa-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="05daa-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="05daa-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="05daa-106">Cet article suppose que vous connaissez les bases du développement à l’aide de Ruby, mais que vous ne connaissez pas la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="05daa-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05daa-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="05daa-107">Prerequisites</span></span>
<span data-ttu-id="05daa-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="05daa-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="05daa-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="05daa-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="05daa-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="05daa-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="05daa-111">Installer Ruby</span><span class="sxs-lookup"><span data-stu-id="05daa-111">Install Ruby</span></span>
<span data-ttu-id="05daa-112">Installez Ruby sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="05daa-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="05daa-113">Windows</span><span class="sxs-lookup"><span data-stu-id="05daa-113">Windows</span></span>
- <span data-ttu-id="05daa-114">Téléchargez et installez la dernière version de [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="05daa-114">Download and Install the latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="05daa-115">Sur l’écran de fin du programme d’installation MSI, cochez la case relative à l’exécution de la commande « ridk install » pour installer MSYS2 et la chaîne d’outils de développement.</span><span class="sxs-lookup"><span data-stu-id="05daa-115">On the finish screen of the MSI installer, check the box that says "Run 'ridk install' to install MSYS2 and development toolchain."</span></span> <span data-ttu-id="05daa-116">Ensuite, cliquez sur **Terminer** pour lancer le programme d’installation suivant.</span><span class="sxs-lookup"><span data-stu-id="05daa-116">Then click **Finish** to launch the next installer.</span></span>
- <span data-ttu-id="05daa-117">Le programme d’installation RubyInstaller2 pour Windows se lance.</span><span class="sxs-lookup"><span data-stu-id="05daa-117">The RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="05daa-118">Saisissez « 2 » pour installer la mise à jour de la base de données de référentiel MSYS2.</span><span class="sxs-lookup"><span data-stu-id="05daa-118">Type 2 to install the MSYS2 repository update.</span></span> <span data-ttu-id="05daa-119">Une fois l’opération terminée, lorsque l’invite d’installation s’affiche à nouveau, fermez la fenêtre de commande.</span><span class="sxs-lookup"><span data-stu-id="05daa-119">After it finishes and returns to the installation prompt, close the command window.</span></span>
- <span data-ttu-id="05daa-120">Démarrez une nouvelle invite de commandes (cmd) à partir du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="05daa-120">Launch a new command prompt (cmd) from the Start menu.</span></span>
- <span data-ttu-id="05daa-121">Testez l’installation de Ruby (`ruby -v`) pour afficher la version installée.</span><span class="sxs-lookup"><span data-stu-id="05daa-121">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="05daa-122">Testez l’installation de Gem (`gem -v`) pour afficher la version installée.</span><span class="sxs-lookup"><span data-stu-id="05daa-122">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="05daa-123">Compilez le module PostgreSQL pour Ruby à l’aide de Gem, en exécutant la commande `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="05daa-123">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="05daa-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="05daa-124">MacOS</span></span>
- <span data-ttu-id="05daa-125">Installez Ruby à l’aide de Homebrew, en exécutant la commande `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="05daa-125">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="05daa-126">Pour accéder à d’autres options d’installation, consultez la [documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/#homebrew) de Ruby.</span><span class="sxs-lookup"><span data-stu-id="05daa-126">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="05daa-127">Testez l’installation de Ruby (`ruby -v`) pour afficher la version installée.</span><span class="sxs-lookup"><span data-stu-id="05daa-127">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="05daa-128">Testez l’installation de Gem (`gem -v`) pour afficher la version installée.</span><span class="sxs-lookup"><span data-stu-id="05daa-128">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="05daa-129">Compilez le module PostgreSQL pour Ruby à l’aide de Gem, en exécutant la commande `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="05daa-129">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="05daa-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="05daa-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="05daa-131">Installez Ruby en exécutant la commande `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="05daa-131">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="05daa-132">Pour accéder à d’autres options d’installation, consultez la [documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/) de Ruby.</span><span class="sxs-lookup"><span data-stu-id="05daa-132">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="05daa-133">Testez l’installation de Ruby (`ruby -v`) pour afficher la version installée.</span><span class="sxs-lookup"><span data-stu-id="05daa-133">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="05daa-134">Installez les dernières mises à jour de Gem en exécutant la commande `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="05daa-134">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
- <span data-ttu-id="05daa-135">Testez l’installation de Gem (`gem -v`) pour afficher la version installée.</span><span class="sxs-lookup"><span data-stu-id="05daa-135">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="05daa-136">Installez les outils de compilation gcc, make, etc. en exécutant la commande `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="05daa-136">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="05daa-137">Installer les bibliothèques PostgreSQL en exécutant la commande `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="05daa-137">Install the PostgreSQL libraries by running the command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="05daa-138">Générez le module pg Ruby à l’aide de Gem en exécutant la commande `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="05daa-138">Build the Ruby pg module using Gem by running the command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="05daa-139">Exécuter le code Ruby</span><span class="sxs-lookup"><span data-stu-id="05daa-139">Run Ruby code</span></span> 
- <span data-ttu-id="05daa-140">Enregistrez le code dans un fichier texte, puis enregistrez ce fichier dans un dossier du projet avec l’extension .rb. Exemples : `C:\rubypostgres\read.rb` ou `/home/username/rubypostgres/read.rb`.</span><span class="sxs-lookup"><span data-stu-id="05daa-140">Save the code into a text file, and save the file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="05daa-141">Pour exécuter le code, lancez l’invite de commandes ou l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="05daa-141">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="05daa-142">Remplacez le répertoire dans votre dossier de projet `cd rubypostgres`, puis saisissez la commande `ruby read.rb` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="05daa-142">Change directory into your project folder `cd rubypostgres`, then type the command `ruby read.rb` to run the application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="05daa-143">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="05daa-143">Get connection information</span></span>
<span data-ttu-id="05daa-144">Obtenez les informations de connexion requises pour vous connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="05daa-144">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="05daa-145">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="05daa-145">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="05daa-146">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="05daa-146">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="05daa-147">Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="05daa-147">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="05daa-148">Cliquez sur le nom du serveur **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="05daa-148">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="05daa-149">Sélectionnez la page **Présentation** du serveur.</span><span class="sxs-lookup"><span data-stu-id="05daa-149">Select the server's **Overview** page.</span></span> <span data-ttu-id="05daa-150">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="05daa-150">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="05daa-151">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="05daa-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="05daa-152">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur.</span><span class="sxs-lookup"><span data-stu-id="05daa-152">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name.</span></span> <span data-ttu-id="05daa-153">Si nécessaire, réinitialisez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="05daa-153">If necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="05daa-154">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="05daa-154">Connect and create a table</span></span>
<span data-ttu-id="05daa-155">Utilisez le code suivant pour vous connecter et créer une table à l’aide de l’instruction **CREATE TABLE**, suivie des instructions SQL **INSERT INTO** pour ajouter des lignes à la table.</span><span class="sxs-lookup"><span data-stu-id="05daa-155">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="05daa-156">Le code utilise un objet [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec le constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="05daa-156">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="05daa-157">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) pour exécuter les commandes DROP, CREATE TABLE et INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="05daa-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="05daa-158">Le code vérifie les erreurs à l’aide de la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="05daa-158">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="05daa-159">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) pour fermer la connexion, avant de s’arrêter.</span><span class="sxs-lookup"><span data-stu-id="05daa-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="05daa-160">Remplacez les chaînes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="05daa-160">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="05daa-161">Lire les données</span><span class="sxs-lookup"><span data-stu-id="05daa-161">Read data</span></span>
<span data-ttu-id="05daa-162">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="05daa-162">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="05daa-163">Le code utilise un objet [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec le constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="05daa-163">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="05daa-164">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) pour exécuter la commande SELECT, en conservant les résultats dans un jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="05daa-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the SELECT command, keeping the results in a result set.</span></span> <span data-ttu-id="05daa-165">La collection de jeu de résultats est itérée au sein de la boucle `resultSet.each do`, les valeurs de ligne actuelles étant conservées dans la variable `row`.</span><span class="sxs-lookup"><span data-stu-id="05daa-165">The result set collection is iterated over using the `resultSet.each do` loop, keeping the current row values in the `row` variable.</span></span> <span data-ttu-id="05daa-166">Le code vérifie les erreurs à l’aide de la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="05daa-166">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="05daa-167">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) pour fermer la connexion, avant de s’arrêter.</span><span class="sxs-lookup"><span data-stu-id="05daa-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="05daa-168">Remplacez les chaînes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="05daa-168">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="05daa-169">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="05daa-169">Update data</span></span>
<span data-ttu-id="05daa-170">Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="05daa-170">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="05daa-171">Le code utilise un objet [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec le constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="05daa-171">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="05daa-172">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) pour exécuter la commande UPDATE.</span><span class="sxs-lookup"><span data-stu-id="05daa-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="05daa-173">Le code vérifie les erreurs à l’aide de la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="05daa-173">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="05daa-174">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) pour fermer la connexion, avant de s’arrêter.</span><span class="sxs-lookup"><span data-stu-id="05daa-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="05daa-175">Remplacez les chaînes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="05daa-175">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="05daa-176">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="05daa-176">Delete data</span></span>
<span data-ttu-id="05daa-177">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="05daa-177">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="05daa-178">Le code utilise un objet [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec le constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="05daa-178">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="05daa-179">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) pour exécuter la commande UPDATE.</span><span class="sxs-lookup"><span data-stu-id="05daa-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="05daa-180">Le code vérifie les erreurs à l’aide de la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="05daa-180">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="05daa-181">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) pour fermer la connexion, avant de s’arrêter.</span><span class="sxs-lookup"><span data-stu-id="05daa-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="05daa-182">Remplacez les chaînes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="05daa-182">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="05daa-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05daa-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="05daa-184">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="05daa-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
