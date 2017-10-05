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
# <a name="azure-database-for-mysql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="5588d-103">Base de données Azure pour MySQL : Utilisation du langage Go pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="5588d-103">Azure Database for MySQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="5588d-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour MySQL à l’aide d’un code écrit dans le langage [Go](https://golang.org/) à partir de plateformes Windows, Ubuntu Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="5588d-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using code written in the [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="5588d-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="5588d-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="5588d-106">Cet article suppose que vous connaissez les bases du développement à l’aide de Go, mais que vous ne connaissez pas la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="5588d-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5588d-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5588d-107">Prerequisites</span></span>
<span data-ttu-id="5588d-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="5588d-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5588d-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="5588d-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="5588d-110">Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="5588d-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="5588d-111">Installer le connecteur pour Go et MySQL</span><span class="sxs-lookup"><span data-stu-id="5588d-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="5588d-112">Installez [Go](https://golang.org/doc/install) et le [pilote-go-sql pour MySQL](https://github.com/go-sql-driver/mysql#installation) sur votre propre machine.</span><span class="sxs-lookup"><span data-stu-id="5588d-112">Install [Go](https://golang.org/doc/install) and the [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="5588d-113">Suivez les étapes correspondant à votre plateforme :</span><span class="sxs-lookup"><span data-stu-id="5588d-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="5588d-114">Windows</span><span class="sxs-lookup"><span data-stu-id="5588d-114">Windows</span></span>
1. <span data-ttu-id="5588d-115">[Téléchargez](https://golang.org/doc/install) et installez Go pour Microsoft Windows en fonction des [instructions d’installation](https://golang.org/dl/).</span><span class="sxs-lookup"><span data-stu-id="5588d-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="5588d-116">Lancez l’invite de commandes à partir du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="5588d-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="5588d-117">Créez un dossier pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="5588d-117">Make a folder for your project such.</span></span> <span data-ttu-id="5588d-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="5588d-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="5588d-119">Basculez dans le dossier de projet, par exemple `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="5588d-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="5588d-120">Définissez la variable d’environnement afin que GOPATH indique le répertoire du code source.</span><span class="sxs-lookup"><span data-stu-id="5588d-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="5588d-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="5588d-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="5588d-122">Installez le [pilote-go-sql pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant la commande `go get github.com/go-sql-driver/mysql`.</span><span class="sxs-lookup"><span data-stu-id="5588d-122">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="5588d-123">Pour résumer, installez Go, puis exécutez ces commandes dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="5588d-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="5588d-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5588d-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="5588d-125">Lancez l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="5588d-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="5588d-126">Installez Go en exécutant la commande `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="5588d-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="5588d-127">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="5588d-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="5588d-128">Basculez dans le dossier de projet, par exemple `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="5588d-128">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="5588d-129">Définir la variable d’environnement GOPATH pour indiquer un répertoire source valide, par exemple le dossier de votre répertoire de base Go.</span><span class="sxs-lookup"><span data-stu-id="5588d-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="5588d-130">Sur l’interpréteur de commandes Bash, exécutez `export GOPATH=~/go` pour ajouter le répertoire Go en tant que GOPATH pour la session d’interpréteur de commandes en cours.</span><span class="sxs-lookup"><span data-stu-id="5588d-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="5588d-131">Installez le [pilote-go-sql pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant la commande `go get github.com/go-sql-driver/mysql`.</span><span class="sxs-lookup"><span data-stu-id="5588d-131">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="5588d-132">Pour résumer, exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="5588d-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="5588d-133">Système d’exploitation mac d’Apple</span><span class="sxs-lookup"><span data-stu-id="5588d-133">Apple macOS</span></span>
1. <span data-ttu-id="5588d-134">Téléchargez et installez Go en fonction des [instructions d’installation](https://golang.org/doc/install) correspondant à votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="5588d-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="5588d-135">Lancez l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="5588d-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="5588d-136">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="5588d-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="5588d-137">Basculez dans le dossier de projet, par exemple `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="5588d-137">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="5588d-138">Définir la variable d’environnement GOPATH pour indiquer un répertoire source valide, par exemple le dossier de votre répertoire de base Go.</span><span class="sxs-lookup"><span data-stu-id="5588d-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="5588d-139">Sur l’interpréteur de commandes Bash, exécutez `export GOPATH=~/go` pour ajouter le répertoire Go en tant que GOPATH pour la session d’interpréteur de commandes en cours.</span><span class="sxs-lookup"><span data-stu-id="5588d-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="5588d-140">Installez le [pilote-go-sql pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant la commande `go get github.com/go-sql-driver/mysql`.</span><span class="sxs-lookup"><span data-stu-id="5588d-140">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="5588d-141">Pour résumer, installez Go, puis exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="5588d-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="5588d-142">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="5588d-142">Get connection information</span></span>
<span data-ttu-id="5588d-143">Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="5588d-143">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="5588d-144">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5588d-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5588d-145">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5588d-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5588d-146">Dans le menu de gauche du Portail Azure, cliquez sur **Toutes les ressources** et recherchez le serveur que vous venez de créer, par exemple **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="5588d-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="5588d-147">Cliquez sur le nom du serveur, **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="5588d-147">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="5588d-148">Sélectionnez la page **Propriétés** du serveur.</span><span class="sxs-lookup"><span data-stu-id="5588d-148">Select the server's **Properties** page.</span></span> <span data-ttu-id="5588d-149">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="5588d-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5588d-150">![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5588d-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5588d-151">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5588d-151">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="5588d-152">Générer et exécuter du code Go</span><span class="sxs-lookup"><span data-stu-id="5588d-152">Build and run Go code</span></span> 
1. <span data-ttu-id="5588d-153">Pour écrire du code Golang, vous pouvez utiliser un éditeur de texte de base, tel que NotePad sous Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) sous Ubuntu, et TextEdit sous mac.</span><span class="sxs-lookup"><span data-stu-id="5588d-153">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="5588d-154">Si vous préférez un environnement de développement interactif (EDI) plus complet, essayez [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft, ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="5588d-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="5588d-155">Collez le code Go des sections ci-dessous dans les fichiers textes et enregistrez les fichiers dans un dossier de projet avec l’extension de fichier \*.go, par exemple le chemin d’accès Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` ou le chemin d’accès Linux `~/go/src/mysqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="5588d-155">Paste the Go code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="5588d-156">Recherchez les constantes `HOST`, `DATABASE`, `USER`, et `PASSWORD` dans le code et remplacez les valeurs test par les valeurs que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5588d-156">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span> 
4. <span data-ttu-id="5588d-157">Lancez l’invite de commandes ou l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="5588d-157">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="5588d-158">Basculez dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="5588d-158">Change directory into your project folder.</span></span> <span data-ttu-id="5588d-159">Par exemple, sur Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="5588d-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="5588d-160">Sur Linux `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="5588d-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="5588d-161">Certains éditeurs EDI mentionnés offrent des fonctionnalités de débogage et de prise en charge du CLR sans nécessiter l’utilisation de l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="5588d-161">Some of the IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="5588d-162">Exécutez le code en tapant la commande `go run createtable.go` afin de compiler l’application et de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="5588d-162">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="5588d-163">Vous pouvez également générer le code dans une application native, `go build createtable.go`, puis lancer `createtable.exe` afin d’exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="5588d-163">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5588d-164">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="5588d-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="5588d-165">Utilisez le code suivant pour vous connecter au serveur, créer une table et charger les données à l’aide d’une instruction SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="5588d-165">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="5588d-166">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5588d-166">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="5588d-167">Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="5588d-167">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="5588d-168">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="5588d-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="5588d-169">Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) plusieurs fois pour exécuter plusieurs commandes DDL.</span><span class="sxs-lookup"><span data-stu-id="5588d-169">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several DDL commands.</span></span> <span data-ttu-id="5588d-170">Le code utilise également les méthodes [Prepare()](http://go-database-sql.org/prepared.html) et Exec() pour exécuter des instructions préparées avec des paramètres différents pour insérer trois lignes.</span><span class="sxs-lookup"><span data-stu-id="5588d-170">The code also uses the [Prepare()](http://go-database-sql.org/prepared.html) and Exec() to run prepared statements with different parameters to insert three rows.</span></span> <span data-ttu-id="5588d-171">À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="5588d-171">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="5588d-172">Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5588d-172">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="5588d-173">Lire les données</span><span class="sxs-lookup"><span data-stu-id="5588d-173">Read data</span></span>
<span data-ttu-id="5588d-174">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="5588d-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="5588d-175">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5588d-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="5588d-176">Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="5588d-176">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="5588d-177">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="5588d-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="5588d-178">Le code appelle la méthode [Query()](https://golang.org/pkg/database/sql/#DB.Query) pour exécuter la commande de sélection.</span><span class="sxs-lookup"><span data-stu-id="5588d-178">The code calls the [Query()](https://golang.org/pkg/database/sql/#DB.Query) method to run the select command.</span></span> <span data-ttu-id="5588d-179">Ensuite il exécute [Next()](https://golang.org/pkg/database/sql/#Rows.Next) pour itérer au sein du jeu de résultats et [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) pour analyser les valeurs de colonne, pour ensuite les enregistrer sous la forme de variables.</span><span class="sxs-lookup"><span data-stu-id="5588d-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) to iterate through the result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) to parse the column values, saving the value into variables.</span></span> <span data-ttu-id="5588d-180">À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="5588d-180">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="5588d-181">Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5588d-181">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="5588d-182">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="5588d-182">Update data</span></span>
<span data-ttu-id="5588d-183">Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="5588d-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="5588d-184">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5588d-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="5588d-185">Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="5588d-185">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="5588d-186">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="5588d-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="5588d-187">Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) pour exécuter la commande de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="5588d-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the update command.</span></span> <span data-ttu-id="5588d-188">À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="5588d-188">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="5588d-189">Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5588d-189">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="5588d-190">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="5588d-190">Delete data</span></span>
<span data-ttu-id="5588d-191">Utilisez le code suivant pour vous connecter et supprimer des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="5588d-191">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="5588d-192">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [pilote go sql](https://github.com/go-sql-driver/mysql#installation) qui sert de pilote pour communiquer avec la base de données Azure, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5588d-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="5588d-193">Le code appelle la méthode [sql.Open()](http://go-database-sql.org/accessing.html) afin de se connecter à la base de données Azure pour MySQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="5588d-193">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="5588d-194">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="5588d-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="5588d-195">Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) pour exécuter la commande de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="5588d-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the delete command.</span></span> <span data-ttu-id="5588d-196">À chaque fois, une méthode checkError() personnalisée est utilisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="5588d-196">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="5588d-197">Remplacez les constantes `host`, `database`, `user` et `password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5588d-197">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="5588d-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5588d-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5588d-199">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="5588d-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
