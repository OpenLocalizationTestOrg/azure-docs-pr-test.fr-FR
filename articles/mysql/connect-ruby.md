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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Base de données Azure pour MySQL : utilisez Ruby tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide un [Ruby](https://www.ruby-lang.org) application et hello [mysql2](https://rubygems.org/gems/mysql2) marque de plateformes Windows, Ubuntu Linux et Mac. Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Cet article suppose que vous êtes familiarisé avec le développement à l’aide de Ruby, mais que vous êtes tooworking nouvelle base de données Azure pour MySQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a>Installer Ruby
Installez Ruby, de marque et de bibliothèque de MySQL2 hello sur votre propre ordinateur. 

### <a name="windows"></a>Windows
1. Téléchargez et installez la version de hello 2.3 [Ruby](http://rubyinstaller.org/downloads/).
2. Lancez une nouvelle invite de commandes (cmd) à partir du menu Démarrer de hello.
3. Accédez au répertoire dans hello Ruby active pour la version 2.3. `cd c:\Ruby23-x64\bin`
4. Hello de test Ruby installation en exécutant la commande hello `ruby -v` toosee version installée de hello.
5. Tester l’installation de marque hello en exécutant la commande hello `gem -v` toosee version installée de hello.
6. Générer le module de hello Mysql2 pour Ruby à l’aide de la marque en exécutant la commande hello `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Installer Ruby à l’aide de Homebrew en exécutant la commande hello `brew install ruby`. Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Hello de test Ruby installation en exécutant la commande hello `ruby -v` toosee version installée de hello.
3. Tester l’installation de marque hello en exécutant la commande hello `gem -v` toosee version installée de hello.
4. Générer le module de hello Mysql2 pour Ruby à l’aide de la marque en exécutant la commande hello `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Installer Ruby en exécutant la commande hello `sudo apt-get install ruby-full`. Pour plus d’options d’installation, consultez hello Ruby [la documentation d’installation](https://www.ruby-lang.org/en/documentation/installation/).
2. Hello de test Ruby installation en exécutant la commande hello `ruby -v` toosee version installée de hello.
3. Installer les dernières mises à jour de hello pour la marque en exécutant la commande hello `sudo gem update --system`.
4. Tester l’installation de marque hello en exécutant la commande hello `gem -v` toosee version installée de hello.
5. Installer hello gcc, la marque et autres outils de génération, en exécutant la commande hello `sudo apt-get install build-essential`.
6. Installer les bibliothèques de développement hello MySQL client en exécutant la commande hello `sudo apt-get install libmysqlclient-dev`.
7. Générer le module de mysql2 hello pour Ruby à l’aide de la marque en exécutant la commande hello `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez accroissant, tel que **myserver4demo**.
3. Cliquez sur le nom du serveur hello **myserver4demo**.
4. Serveur hello sélectionnez **propriétés** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-ruby/1_server-properties-name-login.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="run-ruby-code"></a>Exécuter le code Ruby 
1. Collez hello Ruby code à partir des sections hello ci-dessous dans des fichiers texte et enregistrer des fichiers de hello dans un dossier de projet avec .rb d’extension de fichier, tel que `C:\rubymysql\createtable.rb` ou `/home/username/rubymysql/createtable.rb`.
2. le code hello toorun, lancez l’invite de commandes hello ou bash shell. Basculez dans votre dossier de projet `cd rubymysql`.
3. Puis tapez la commande hello ruby suivi par nom de fichier hello, tel que `ruby createtable.rb` application hello de toorun.
4. Sur hello du système d’exploitation Windows, si l’application hello ruby n’est pas dans votre variable d’environnement path, vous devrez peut-être toouse hello chemin d’accès complet toolaunch hello nœud application tel que`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Se connecter et créer une table
Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.

code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL. Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) plusieurs fois toorun hello DROP, CREATE TABLE, commandes et de INSERT INTO. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs. 
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

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. 

code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL. Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) commandes SELECT de toorun hello. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs. 

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

## <a name="update-data"></a>Mettre à jour des données
Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.

code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL. Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) commandes de mise à jour toorun hello. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs. 

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


## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. 

code de Hello utilise un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() méthode tooconnect tooAzure base de données MySQL. Ensuite, il appelle la méthode [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) commandes DELETE de hello toorun. Ensuite, il appelle la méthode [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connexion de hello tooclose avant la fin.

Remplacez hello `host`, `database`, `username`, et `password` de chaînes avec vos propres valeurs. 

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

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./concepts-migrate-import-export.md)
