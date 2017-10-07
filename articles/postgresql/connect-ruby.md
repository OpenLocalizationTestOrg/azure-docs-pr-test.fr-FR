---
title: "aaaConnect tooAzure base de données PostgreSQL à l’aide de Ruby | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code Ruby, vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour PostgreSQL."
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
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="14b96-103">Base de données Azure pour PostgreSQL : utilisez Ruby tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="14b96-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="14b96-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données PostgreSQL utilisant un [Ruby](https://www.ruby-lang.org) application.</span><span class="sxs-lookup"><span data-stu-id="14b96-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="14b96-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="14b96-106">Cet article suppose que vous êtes familiarisé avec le développement à l’aide de Ruby, mais que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14b96-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="14b96-107">Prerequisites</span></span>
<span data-ttu-id="14b96-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="14b96-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="14b96-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="14b96-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="14b96-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="14b96-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="14b96-111">Installer Ruby</span><span class="sxs-lookup"><span data-stu-id="14b96-111">Install Ruby</span></span>
<span data-ttu-id="14b96-112">Installez Ruby sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="14b96-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="14b96-113">Windows</span><span class="sxs-lookup"><span data-stu-id="14b96-113">Windows</span></span>
- <span data-ttu-id="14b96-114">Télécharger et installer la version plus récente hello de [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="14b96-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="14b96-115">Sur hello terminer d’écran du programme d’installation MSI hello, hello case indiquant que « exécuter 'installer ridk' tooinstall MSYS2 et chaîne d’outils de développement ».</span><span class="sxs-lookup"><span data-stu-id="14b96-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="14b96-116">Puis cliquez sur **Terminer** programme d’installation de toolaunch hello suivant.</span><span class="sxs-lookup"><span data-stu-id="14b96-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="14b96-117">permet de lancer le programme d’installation de Hello RubyInstaller2 pour Windows.</span><span class="sxs-lookup"><span data-stu-id="14b96-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="14b96-118">Type de mise à jour du référentiel de hello MSYS2 tooinstall 2.</span><span class="sxs-lookup"><span data-stu-id="14b96-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="14b96-119">Après que qu’il se termine et retourne l’invite d’installation toohello, fermez la fenêtre de commande hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="14b96-120">Lancez une nouvelle invite de commandes (cmd) à partir du menu Démarrer de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="14b96-121">Hello de test installation Ruby `ruby -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="14b96-122">Tester l’installation de marque hello `gem -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="14b96-123">Générer le module de PostgreSQL hello pour Ruby à l’aide de la marque en exécutant la commande hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="14b96-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="14b96-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="14b96-124">MacOS</span></span>
- <span data-ttu-id="14b96-125">Installer Ruby à l’aide de Homebrew en exécutant la commande hello `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="14b96-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="14b96-126">Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="14b96-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="14b96-127">Hello de test installation Ruby `ruby -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="14b96-128">Tester l’installation de marque hello `gem -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="14b96-129">Générer le module de PostgreSQL hello pour Ruby à l’aide de la marque en exécutant la commande hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="14b96-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="14b96-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="14b96-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="14b96-131">Installer Ruby en exécutant la commande hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="14b96-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="14b96-132">Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="14b96-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="14b96-133">Hello de test installation Ruby `ruby -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="14b96-134">Installer les dernières mises à jour de hello pour la marque en exécutant la commande hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="14b96-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="14b96-135">Tester l’installation de marque hello `gem -v` toosee version installée de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="14b96-136">Installer hello gcc, la marque et autres outils de génération, en exécutant la commande hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="14b96-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="14b96-137">Installer les bibliothèques de PostgreSQL hello en exécutant la commande hello `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="14b96-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="14b96-138">Générer le module de pg Ruby hello à l’aide de la marque en exécutant la commande hello `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="14b96-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="14b96-139">Exécuter le code Ruby</span><span class="sxs-lookup"><span data-stu-id="14b96-139">Run Ruby code</span></span> 
- <span data-ttu-id="14b96-140">Enregistrer le code de hello dans un fichier texte et enregistrez-le hello dans un dossier du projet avec .rb d’extension de fichier, tel que `C:\rubypostgres\read.rb` ou`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="14b96-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="14b96-141">le code hello toorun, lancez l’invite de commandes hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="14b96-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="14b96-142">Accédez au répertoire dans votre dossier de projet `cd rubypostgres`, puis tapez la commande hello `ruby read.rb` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="14b96-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="14b96-143">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="14b96-143">Get connection information</span></span>
<span data-ttu-id="14b96-144">Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="14b96-145">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="14b96-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="14b96-146">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="14b96-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="14b96-147">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="14b96-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="14b96-148">Cliquez sur le nom du serveur hello **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="14b96-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="14b96-149">Serveur hello sélectionnez **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="14b96-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="14b96-150">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="14b96-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="14b96-151">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="14b96-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="14b96-152">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** nom d’utilisateur admin page tooview hello Server.</span><span class="sxs-lookup"><span data-stu-id="14b96-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="14b96-153">Si nécessaire, le mot de passe réinitialisé hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="14b96-154">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="14b96-154">Connect and create a table</span></span>
<span data-ttu-id="14b96-155">Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="14b96-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="14b96-156">code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="14b96-157">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) les commandes toorun hello DROP, CREATE TABLE et INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="14b96-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="14b96-158">Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="14b96-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="14b96-159">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="14b96-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="14b96-160">Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="14b96-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection toodatabase'

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

## <a name="read-data"></a><span data-ttu-id="14b96-161">Lire les données</span><span class="sxs-lookup"><span data-stu-id="14b96-161">Read data</span></span>
<span data-ttu-id="14b96-162">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="14b96-163">code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="14b96-164">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) commande SELECT toorun hello, en conservant les résultats hello dans un jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="14b96-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="14b96-165">Hello collection de jeu de résultats est itérée au sein hello `resultSet.each do` boucle, en conservant les valeurs de ligne actuelles hello Bonjour `row` variable.</span><span class="sxs-lookup"><span data-stu-id="14b96-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="14b96-166">Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="14b96-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="14b96-167">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="14b96-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="14b96-168">Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="14b96-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="update-data"></a><span data-ttu-id="14b96-169">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="14b96-169">Update data</span></span>
<span data-ttu-id="14b96-170">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="14b96-171">code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="14b96-172">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello commande de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="14b96-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="14b96-173">Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="14b96-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="14b96-174">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="14b96-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="14b96-175">Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="14b96-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="14b96-176">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="14b96-176">Delete data</span></span>
<span data-ttu-id="14b96-177">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="14b96-178">code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="14b96-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="14b96-179">Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello commande de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="14b96-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="14b96-180">Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="14b96-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="14b96-181">Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.</span><span class="sxs-lookup"><span data-stu-id="14b96-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="14b96-182">Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="14b96-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="14b96-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14b96-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="14b96-184">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="14b96-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
