---
title: "Se connecter à la base de données Azure pour MySQL à l’aide de Go | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit plusieurs exemples de code Go que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: 42a6b1c37de08971674c8b38f1e13bfd657f8b03
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-go-language-to-connect-and-query-data"></a>Base de données Azure pour MySQL : Utilisation du langage Go pour se connecter et interroger des données
Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour MySQL à l’aide d’un code écrit dans le langage [Go](https://golang.org/) à partir de plateformes Windows, Ubuntu Linux et Mac. Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer. Cet article suppose que vous connaissez les bases du développement à l’aide de Go, mais que vous ne connaissez pas la base de données Azure pour MySQL.

## <a name="prerequisites"></a>Composants requis
Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a>Installer le connecteur pour Go et MySQL
Installez [Go](https://golang.org/doc/install) et le [pilote-go-sql pour MySQL](https://github.com/go-sql-driver/mysql#installation) sur votre propre machine. Suivez les étapes correspondant à votre plateforme :

### <a name="windows"></a>Windows
1. [Téléchargez](https://golang.org/doc/install) et installez Go pour Microsoft Windows en fonction des [instructions d’installation](https://golang.org/dl/).
2. Lancez l’invite de commandes à partir du menu Démarrer.
3. Créez un dossier pour votre projet. `mkdir  %USERPROFILE%\go\src\mysqlgo`.
4. Basculez dans le dossier de projet, par exemple `cd %USERPROFILE%\go\src\mysqlgo`.
5. Définissez la variable d’environnement afin que GOPATH indique le répertoire du code source. `set GOPATH=%USERPROFILE%\go`.
6. Installez le [pilote-go-sql pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant la commande `go get github.com/go-sql-driver/mysql`.

   Pour résumer, installez Go, puis exécutez ces commandes dans l’invite de commandes :
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Lancez l’interpréteur de commandes Bash. 
2. Installez Go en exécutant la commande `sudo apt-get install golang-go`.
3. Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/mysqlgo/`.
4. Basculez dans le dossier de projet, par exemple `cd ~/go/src/mysqlgo/`.
5. Définir la variable d’environnement GOPATH pour indiquer un répertoire source valide, par exemple le dossier de votre répertoire de base Go. Sur l’interpréteur de commandes Bash, exécutez `export GOPATH=~/go` pour ajouter le répertoire Go en tant que GOPATH pour la session d’interpréteur de commandes en cours.
6. Installez le [pilote-go-sql pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant la commande `go get github.com/go-sql-driver/mysql`.

   Pour résumer, exécutez ces commandes Bash :
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a>Système d’exploitation mac d’Apple
1. Téléchargez et installez Go en fonction des [instructions d’installation](https://golang.org/doc/install) correspondant à votre plateforme. 
2. Lancez l’interpréteur de commandes Bash. 
3. Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/mysqlgo/`.
4. Basculez dans le dossier de projet, par exemple `cd ~/go/src/mysqlgo/`.
5. Définir la variable d’environnement GOPATH pour indiquer un répertoire source valide, par exemple le dossier de votre répertoire de base Go. Sur l’interpréteur de commandes Bash, exécutez `export GOPATH=~/go` pour ajouter le répertoire Go en tant que GOPATH pour la session d’interpréteur de commandes en cours.
6. Installez le [pilote-go-sql pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant la commande `go get github.com/go-sql-driver/mysql`.

   Pour résumer, installez Go, puis exécutez ces commandes Bash :
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL. Vous devez disposer du nom de serveur complet et des informations d’identification.

1. Connectez-vous au [portail Azure](https://portal.azure.com/).
2. Dans le menu de gauche du Portail Azure, cliquez sur **Toutes les ressources** et recherchez le serveur que vous venez de créer, par exemple **myserver4demo**.
3. Cliquez sur le nom du serveur, **myserver4demo**.
4. Sélectionnez la page **Propriétés** du serveur. Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.
 ![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-go/1_server-properties-name-login.png)
5. Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.
   

## <a name="build-and-run-go-code"></a>Générer et exécuter du code Go 
1. Pour écrire du code Golang, vous pouvez utiliser un éditeur de texte de base, tel que NotePad sous Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) sous Ubuntu, et TextEdit sous mac. Si vous préférez un environnement de développement interactif (EDI) plus complet, essayez [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft, ou [Atom](https://atom.io/).
2. Collez le code Go des sections ci-dessous dans les fichiers textes et enregistrez les fichiers dans un dossier de projet avec l’extension de fichier \*.go, par exemple le chemin d’accès Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` ou le chemin d’accès Linux `~/go/src/mysqlgo/createtable.go`.
3. Recherchez les constantes `HOST`, `DATABASE`, `USER`, et `PASSWORD` dans le code et remplacez les valeurs test par les valeurs que vous souhaitez. 
4. Lancez l’invite de commandes ou l’interpréteur de commandes Bash. Basculez dans votre dossier de projet. Par exemple, sur Windows `cd %USERPROFILE%\go\src\mysqlgo\`. Sur Linux `cd ~/go/src/mysqlgo/`.  Certains éditeurs EDI mentionnés offrent des fonctionnalités de débogage et de prise en charge du CLR sans nécessiter l’utilisation de l’interpréteur de commandes.
5. Exécutez le code en tapant la commande `go run createtable.go` afin de compiler l’application et de l’exécuter. 
6. Vous pouvez également générer le code dans une application native, `go build createtable.go`, puis lancer `createtable.exe` afin d’exécuter l’application.

## <a name="connect-create-table-and-insert-data"></a>Se connecter, créer des tables et insérer des données
Utilisez le code suivant pour vous connecter au serveur, créer une table et charger les données à l’aide d’une instruction SQL **INSERT**. 

Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.

Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données. Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) plusieurs fois pour exécuter plusieurs commandes DDL. Le code utilise également les méthodes [Prepare()](http://go-database-sql.org/prepared.html) et Exec() pour exécuter des instructions préparées avec des paramètres différents pour insérer trois lignes. À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.

Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a>Lire les données
Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**. 

Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.

Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données. Le code appelle la méthode [Query()](https://golang.org/pkg/database/sql/#DB.Query) pour exécuter la commande de sélection. Ensuite il exécute [Next()](https://golang.org/pkg/database/sql/#Rows.Next) pour itérer au sein du jeu de résultats et [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) pour analyser les valeurs de colonne, pour ensuite les enregistrer sous la forme de variables. À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.

Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from the table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a>Mettre à jour des données
Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**. 

Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.

Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données. Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) pour exécuter la commande de mise à jour. À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.

Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a>Suppression de données
Utilisez le code suivant pour vous connecter et supprimer des données à l’aide d’une instruction SQL **DELETE**. 

Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.

Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données. Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) pour exécuter la commande de mise à jour. À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.

Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs. 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./concepts-migrate-import-export.md)
