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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Base de données Azure pour PostgreSQL : utilisez Ruby tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données PostgreSQL utilisant un [Ruby](https://www.ruby-lang.org) application. Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Cet article suppose que vous êtes familiarisé avec le développement à l’aide de Ruby, mais que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Créer une base de données - Portail](quickstart-create-server-database-portal.md)
- [Créer une base de données - Interface de ligne de commande Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Installer Ruby
Installez Ruby sur votre ordinateur. 

### <a name="windows"></a>Windows
- Télécharger et installer la version plus récente hello de [Ruby](http://rubyinstaller.org/downloads/).
- Sur hello terminer d’écran du programme d’installation MSI hello, hello case indiquant que « exécuter 'installer ridk' tooinstall MSYS2 et chaîne d’outils de développement ». Puis cliquez sur **Terminer** programme d’installation de toolaunch hello suivant.
- permet de lancer le programme d’installation de Hello RubyInstaller2 pour Windows. Type de mise à jour du référentiel de hello MSYS2 tooinstall 2. Après que qu’il se termine et retourne l’invite d’installation toohello, fermez la fenêtre de commande hello.
- Lancez une nouvelle invite de commandes (cmd) à partir du menu Démarrer de hello.
- Hello de test installation Ruby `ruby -v` toosee version installée de hello.
- Tester l’installation de marque hello `gem -v` toosee version installée de hello.
- Générer le module de PostgreSQL hello pour Ruby à l’aide de la marque en exécutant la commande hello `gem install pg`.

### <a name="macos"></a>MacOS
- Installer Ruby à l’aide de Homebrew en exécutant la commande hello `brew install ruby`. Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Hello de test installation Ruby `ruby -v` toosee version installée de hello.
- Tester l’installation de marque hello `gem -v` toosee version installée de hello.
- Générer le module de PostgreSQL hello pour Ruby à l’aide de la marque en exécutant la commande hello `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Installer Ruby en exécutant la commande hello `sudo apt-get install ruby-full`. Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/).
- Hello de test installation Ruby `ruby -v` toosee version installée de hello.
- Installer les dernières mises à jour de hello pour la marque en exécutant la commande hello `sudo gem update --system`.
- Tester l’installation de marque hello `gem -v` toosee version installée de hello.
- Installer hello gcc, la marque et autres outils de génération, en exécutant la commande hello `sudo apt-get install build-essential`.
- Installer les bibliothèques de PostgreSQL hello en exécutant la commande hello `sudo apt-get install libpq-dev`.
- Générer le module de pg Ruby hello à l’aide de la marque en exécutant la commande hello `sudo gem install pg`.

## <a name="run-ruby-code"></a>Exécuter le code Ruby 
- Enregistrer le code de hello dans un fichier texte et enregistrez-le hello dans un dossier du projet avec .rb d’extension de fichier, tel que `C:\rubypostgres\read.rb` ou`/home/username/rubypostgres/read.rb`
- le code hello toorun, lancez l’invite de commandes hello ou bash shell. Accédez au répertoire dans votre dossier de projet `cd rubypostgres`, puis tapez la commande hello `ruby read.rb` application hello de toorun.

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **mypgserver-20170401**.
3. Cliquez sur le nom du serveur hello **mypgserver-20170401**.
4. Serveur hello sélectionnez **vue d’ensemble** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-ruby/1-connection-string.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** nom d’utilisateur admin page tooview hello Server. Si nécessaire, le mot de passe réinitialisé hello.

## <a name="connect-and-create-a-table"></a>Se connecter et créer une table
Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.

code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) les commandes toorun hello DROP, CREATE TABLE et INSERT INTO. Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs. 
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

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. 

code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) commande SELECT toorun hello, en conservant les résultats hello dans un jeu de résultats. Hello collection de jeu de résultats est itérée au sein hello `resultSet.each do` boucle, en conservant les valeurs de ligne actuelles hello Bonjour `row` variable. Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs. 

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

## <a name="update-data"></a>Mettre à jour des données
Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.

code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello commande de mise à jour. Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs. 

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


## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. 

code de Hello utilise un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) objet avec constructeur [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello commande de mise à jour. Hello code vérifie les erreurs à l’aide de hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `user`, et `password` de chaînes avec vos propres valeurs. 

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

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./howto-migrate-using-export-and-import.md)
