---
title: "Se connecter à la base de données Azure pour PostgreSQL à l’aide du langage Go | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit un exemple de langage de programmation Go, que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="3f5ca-103">Base de données Azure pour PostgreSQL : Utilisation du langage Go pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="3f5ca-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="3f5ca-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour PostgreSQL en utilisant du code écrit dans le langage [Go](https://golang.org/) (golang).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="3f5ca-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="3f5ca-106">Cet article suppose que vous connaissez les bases du développement à l’aide de Go, mais que vous ne connaissez pas la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f5ca-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3f5ca-107">Prerequisites</span></span>
<span data-ttu-id="3f5ca-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="3f5ca-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3f5ca-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="3f5ca-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="3f5ca-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3f5ca-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="3f5ca-111">Installer le connecteur pour Go et pq</span><span class="sxs-lookup"><span data-stu-id="3f5ca-111">Install Go and pq connector</span></span>
<span data-ttu-id="3f5ca-112">Installez [Go](https://golang.org/doc/install) et le [pilote Pure Go Postgres (pq)](https://github.com/lib/pq) sur votre propre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="3f5ca-113">Suivez les étapes correspondant à votre plateforme :</span><span class="sxs-lookup"><span data-stu-id="3f5ca-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="3f5ca-114">Windows</span><span class="sxs-lookup"><span data-stu-id="3f5ca-114">Windows</span></span>
1. <span data-ttu-id="3f5ca-115">[Téléchargez](https://golang.org/doc/install) et installez Go pour Microsoft Windows en fonction des [instructions d’installation](https://golang.org/dl/).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="3f5ca-116">Lancez l’invite de commandes à partir du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="3f5ca-117">Créez un dossier pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-117">Make a folder for your project such.</span></span> <span data-ttu-id="3f5ca-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="3f5ca-119">Basculez dans le dossier de projet, par exemple `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="3f5ca-120">Définissez la variable d’environnement afin que GOPATH indique le répertoire du code source.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="3f5ca-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="3f5ca-122">Installez le [pilote Pure Go Postgres (pq)](https://github.com/lib/pq) en exécutant la commande `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="3f5ca-123">Pour résumer, installez Go, puis exécutez ces commandes dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="3f5ca-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="3f5ca-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="3f5ca-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="3f5ca-125">Lancez l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="3f5ca-126">Installez Go en exécutant la commande `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="3f5ca-127">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="3f5ca-128">Basculez dans le dossier de projet, par exemple `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="3f5ca-129">Définir la variable d’environnement GOPATH pour indiquer un répertoire source valide, par exemple le dossier de votre répertoire de base Go.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="3f5ca-130">Sur l’interpréteur de commandes Bash, exécutez `export GOPATH=~/go` pour ajouter le répertoire Go en tant que GOPATH pour la session d’interpréteur de commandes en cours.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="3f5ca-131">Installez le [pilote Pure Go Postgres (pq)](https://github.com/lib/pq) en exécutant la commande `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="3f5ca-132">Pour résumer, exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="3f5ca-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="3f5ca-133">Système d’exploitation mac d’Apple</span><span class="sxs-lookup"><span data-stu-id="3f5ca-133">Apple macOS</span></span>
1. <span data-ttu-id="3f5ca-134">Téléchargez et installez Go en fonction des [instructions d’installation](https://golang.org/doc/install) correspondant à votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="3f5ca-135">Lancez l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="3f5ca-136">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="3f5ca-137">Basculez dans le dossier de projet, par exemple `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="3f5ca-138">Définir la variable d’environnement GOPATH pour indiquer un répertoire source valide, par exemple le dossier de votre répertoire de base Go.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="3f5ca-139">Sur l’interpréteur de commandes Bash, exécutez `export GOPATH=~/go` pour ajouter le répertoire Go en tant que GOPATH pour la session d’interpréteur de commandes en cours.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="3f5ca-140">Installez le [pilote Pure Go Postgres (pq)](https://github.com/lib/pq) en exécutant la commande `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="3f5ca-141">Pour résumer, installez Go, puis exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="3f5ca-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="3f5ca-142">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="3f5ca-142">Get connection information</span></span>
<span data-ttu-id="3f5ca-143">Obtenez les informations de connexion requises pour vous connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="3f5ca-144">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3f5ca-145">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3f5ca-146">Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="3f5ca-147">Cliquez sur le nom du serveur **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="3f5ca-148">Sélectionnez la page **Présentation** du serveur.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="3f5ca-149">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3f5ca-150">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="3f5ca-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="3f5ca-151">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** et affichez le nom de connexion de l’administrateur du serveur.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="3f5ca-152">Si nécessaire, réinitialisez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="3f5ca-153">Générer et exécuter du code Go</span><span class="sxs-lookup"><span data-stu-id="3f5ca-153">Build and run Go code</span></span> 
1. <span data-ttu-id="3f5ca-154">Pour écrire du code Golang, vous pouvez utiliser un éditeur de texte de base, tel que NotePad sous Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) sous Ubuntu, et TextEdit sous mac.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="3f5ca-155">Si vous préférez un environnement de développement interactif (EDI) plus complet, essayez [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft, ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="3f5ca-156">Collez le code Golang des sections ci-dessous dans les fichiers textes et enregistrez les fichiers dans un dossier de projet avec l’extension de fichier \*.go, par exemple le chemin d’accès Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` ou le chemin d’accès Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="3f5ca-157">Recherchez les constantes `HOST`, `DATABASE`, `USER`, et `PASSWORD` dans le code et remplacez les valeurs test par les valeurs que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="3f5ca-158">Lancez l’invite de commandes ou l’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="3f5ca-159">Basculez dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-159">Change directory into your project folder.</span></span> <span data-ttu-id="3f5ca-160">Par exemple, sur Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="3f5ca-161">Sur Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="3f5ca-162">Certains environnements EDI mentionnés offrent des fonctionnalités de débogage et de prise en charge du CLR sans nécessiter l’utilisation de l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="3f5ca-163">Exécutez le code en tapant la commande `go run createtable.go` afin de compiler l’application et de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="3f5ca-164">Vous pouvez également générer le code dans une application native, `go build createtable.go`, puis lancer `createtable.exe` afin d’exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="3f5ca-165">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="3f5ca-165">Connect and create a table</span></span>
<span data-ttu-id="3f5ca-166">Utilisez le code suivant pour vous connecter et créer une table à l’aide de l’instruction **CREATE TABLE**, suivie des instructions SQL **INSERT INTO** pour ajouter des lignes à la table.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="3f5ca-167">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [package pq](http://godoc.org/github.com/lib/pq) qui sert de pilote pour communiquer avec le serveur Postgres, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="3f5ca-168">Le code appelle la méthode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) afin de se connecter à la base de données Azure pour PostgreSQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="3f5ca-169">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="3f5ca-170">Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) plusieurs fois pour exécuter plusieurs commandes SQL.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="3f5ca-171">À chaque fois, utilisez une méthode checkError() personnalisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="3f5ca-172">Remplacez les paramètres `HOST`, `DATABASE`, `USER` et `PASSWORD` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a><span data-ttu-id="3f5ca-173">Lire les données</span><span class="sxs-lookup"><span data-stu-id="3f5ca-173">Read data</span></span>
<span data-ttu-id="3f5ca-174">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="3f5ca-175">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [package pq](http://godoc.org/github.com/lib/pq) qui sert de pilote pour communiquer avec le serveur Postgres, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="3f5ca-176">Le code appelle la méthode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) afin de se connecter à la base de données Azure pour PostgreSQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="3f5ca-177">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="3f5ca-178">La requête Select est exécutée par le biais d’un appel à la méthode [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), et les lignes obtenues sont conservées dans une variable de type [lignes](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="3f5ca-179">Le code lit les valeurs de données de la colonne dans la ligne actuelle à l’aide de la méthode [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) et effectue une boucle sur les lignes à l’aide de l’itérateur [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) jusqu’à la suppression de toutes les lignes.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="3f5ca-180">Les valeurs de colonne de chaque ligne sont imprimées en sortie sur la console. À chaque fois, utilisez une méthode checkError() personnalisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="3f5ca-181">Remplacez les paramètres `HOST`, `DATABASE`, `USER` et `PASSWORD` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="3f5ca-182">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="3f5ca-182">Update data</span></span>
<span data-ttu-id="3f5ca-183">Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="3f5ca-184">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [package pq](http://godoc.org/github.com/lib/pq) qui sert de pilote pour communiquer avec le serveur Postgres, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="3f5ca-185">Le code appelle la méthode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) afin de se connecter à la base de données Azure pour PostgreSQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="3f5ca-186">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="3f5ca-187">Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) pour exécuter l’instruction SQL qui met à jour la table.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="3f5ca-188">Utilisez une méthode checkError() personnalisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="3f5ca-189">Remplacez les paramètres `HOST`, `DATABASE`, `USER` et `PASSWORD` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="3f5ca-190">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="3f5ca-190">Delete data</span></span>
<span data-ttu-id="3f5ca-191">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="3f5ca-192">Le code importe trois packages : le [package sql](https://golang.org/pkg/database/sql/), le [package pq](http://godoc.org/github.com/lib/pq) qui sert de pilote pour communiquer avec le serveur Postgres, et le [package fmt](https://golang.org/pkg/fmt/) pour les entrées et sorties imprimées sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="3f5ca-193">Le code appelle la méthode [sql.Open()](http://godoc.org/github.com/lib/pq#Open) afin de se connecter à la base de données Azure pour PostgreSQL et vérifie la connexion à l’aide de la méthode [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="3f5ca-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="3f5ca-194">Un [descripteur de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout : il contient le pool de connexions pour le serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="3f5ca-195">Le code appelle la méthode [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) pour exécuter l’instruction SQL qui met à jour la table.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="3f5ca-196">Utilisez une méthode checkError() personnalisée pour vérifier si une erreur s’est produite. Si tel est le cas, dépêchez-vous de quitter l’application.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="3f5ca-197">Remplacez les paramètres `HOST`, `DATABASE`, `USER` et `PASSWORD` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3f5ca-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="3f5ca-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f5ca-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3f5ca-199">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="3f5ca-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
