---
title: "Se connecter tooAzure de base de données de MySQL à l’aide de Go | Documents Microsoft"
description: "Ce démarrage rapide fournit plusieurs exemples de code Go vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
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
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="4025a-103">Base de données Azure pour MySQL : utilisent la commande Go langage tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="4025a-103">Azure Database for MySQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="4025a-104">Ce démarrage rapide montre comment tooconnect tooan base de données Azure pour MySQL à l’aide de code hello écrite dans [accédez](https://golang.org/) langage à partir des plates-formes Windows, Ubuntu Linux et Apple macOS.</span><span class="sxs-lookup"><span data-stu-id="4025a-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using code written in hello [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="4025a-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="4025a-106">Cet article suppose que vous êtes familiarisé avec le développement à l’aide de Go, mais que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="4025a-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4025a-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4025a-107">Prerequisites</span></span>
<span data-ttu-id="4025a-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="4025a-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4025a-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4025a-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4025a-110">Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="4025a-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="4025a-111">Installer le connecteur pour Go et MySQL</span><span class="sxs-lookup"><span data-stu-id="4025a-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="4025a-112">Installer [accédez](https://golang.org/doc/install) et hello [go-sql-pilote pour MySQL](https://github.com/go-sql-driver/mysql#installation) sur votre propre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4025a-112">Install [Go](https://golang.org/doc/install) and hello [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="4025a-113">Selon votre plateforme, suivez les étapes de hello :</span><span class="sxs-lookup"><span data-stu-id="4025a-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="4025a-114">Windows</span><span class="sxs-lookup"><span data-stu-id="4025a-114">Windows</span></span>
1. <span data-ttu-id="4025a-115">[Télécharger](https://golang.org/dl/) et installer Go pour Microsoft Windows, en fonction de toohello [des instructions d’installation](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="4025a-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="4025a-116">Lancez l’invite de commandes hello à partir du menu Démarrer de hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="4025a-117">Créez un dossier pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="4025a-117">Make a folder for your project such.</span></span> <span data-ttu-id="4025a-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="4025a-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="4025a-119">Placez-vous dans le dossier du projet hello, tel que `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="4025a-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="4025a-120">Définissez la variable d’environnement hello pour le répertoire de code source GOPATH toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="4025a-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="4025a-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="4025a-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="4025a-122">Installer hello [go-sql-pilote pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant hello `go get github.com/go-sql-driver/mysql` commande.</span><span class="sxs-lookup"><span data-stu-id="4025a-122">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="4025a-123">En résumé, installez Go, puis exécuter ces commandes dans une invite de commandes hello :</span><span class="sxs-lookup"><span data-stu-id="4025a-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="4025a-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4025a-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="4025a-125">Lancez l’interpréteur de commandes Bash hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="4025a-126">Installez Go en exécutant la commande `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="4025a-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="4025a-127">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="4025a-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="4025a-128">Placez-vous dans le dossier de hello, tel que `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="4025a-128">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="4025a-129">Ensemble hello GOPATH environnement variable toopoint tooa source valide répertoire, tel que votre accueil actuel du répertoire atteindre le dossier.</span><span class="sxs-lookup"><span data-stu-id="4025a-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="4025a-130">À l’interpréteur de commandes bash hello, exécutez `export GOPATH=~/go` tooadd hello accédez répertoire comme hello GOPATH pour la session d’interpréteur de commandes en cours hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="4025a-131">Installer hello [go-sql-pilote pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant hello `go get github.com/go-sql-driver/mysql` commande.</span><span class="sxs-lookup"><span data-stu-id="4025a-131">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="4025a-132">Pour résumer, exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="4025a-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="4025a-133">Système d’exploitation mac d’Apple</span><span class="sxs-lookup"><span data-stu-id="4025a-133">Apple macOS</span></span>
1. <span data-ttu-id="4025a-134">Téléchargez et installez accèdent selon toohello [des instructions d’installation](https://golang.org/doc/install) correspondant à votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="4025a-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="4025a-135">Lancez l’interpréteur de commandes Bash hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="4025a-136">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="4025a-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="4025a-137">Placez-vous dans le dossier de hello, tel que `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="4025a-137">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="4025a-138">Ensemble hello GOPATH environnement variable toopoint tooa source valide répertoire, tel que votre accueil actuel du répertoire atteindre le dossier.</span><span class="sxs-lookup"><span data-stu-id="4025a-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="4025a-139">À l’interpréteur de commandes bash hello, exécutez `export GOPATH=~/go` tooadd hello accédez répertoire comme hello GOPATH pour la session d’interpréteur de commandes en cours hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="4025a-140">Installer hello [go-sql-pilote pour mysql](https://github.com/go-sql-driver/mysql#installation) en exécutant hello `go get github.com/go-sql-driver/mysql` commande.</span><span class="sxs-lookup"><span data-stu-id="4025a-140">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="4025a-141">Pour résumer, installez Go, puis exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="4025a-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="4025a-142">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="4025a-142">Get connection information</span></span>
<span data-ttu-id="4025a-143">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="4025a-143">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="4025a-144">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="4025a-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4025a-145">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4025a-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4025a-146">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez accroissant, tel que **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="4025a-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="4025a-147">Cliquez sur le nom du serveur hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="4025a-147">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="4025a-148">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="4025a-148">Select hello server's **Properties** page.</span></span> <span data-ttu-id="4025a-149">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="4025a-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4025a-150">![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4025a-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4025a-151">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-151">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="4025a-152">Générer et exécuter du code Go</span><span class="sxs-lookup"><span data-stu-id="4025a-152">Build and run Go code</span></span> 
1. <span data-ttu-id="4025a-153">toowrite Golang code, vous pouvez utiliser un simple éditeur de texte, tel que le bloc-notes dans Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) dans Ubuntu ou TextEdit dans macOS.</span><span class="sxs-lookup"><span data-stu-id="4025a-153">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="4025a-154">Si vous préférez un environnement de développement interactif (EDI) plus complet, essayez [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft, ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="4025a-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="4025a-155">Collez hello code Go à partir des sections hello ci-dessous dans des fichiers texte et enregistrer dans votre dossier de projet avec l’extension de fichier \*.consultez la rubrique, telles que le chemin d’accès au Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` ou chemin d’accès de Linux `~/go/src/mysqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="4025a-155">Paste hello Go code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="4025a-156">Recherchez hello `HOST`, `DATABASE`, `USER`, et `PASSWORD` constantes dans le code hello et valeurs de l’exemple hello remplacer par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4025a-156">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span> 
4. <span data-ttu-id="4025a-157">Lancez l’invite de commandes hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="4025a-157">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="4025a-158">Basculez dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="4025a-158">Change directory into your project folder.</span></span> <span data-ttu-id="4025a-159">Par exemple, sur Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="4025a-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="4025a-160">Sur Linux `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="4025a-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="4025a-161">Certains éditeurs d’IDE hello mentionnés offrent des fonctions de débogage et d’exécution sans nécessiter de commandes d’environnement.</span><span class="sxs-lookup"><span data-stu-id="4025a-161">Some of hello IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="4025a-162">Exécuter le code de hello en tapant la commande hello `go run createtable.go` toocompile hello application et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="4025a-162">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="4025a-163">Vous pouvez également les code hello toobuild dans une application native, `go build createtable.go`, puis lancez `createtable.exe` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="4025a-163">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="4025a-164">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="4025a-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="4025a-165">Utilisez hello suivantes tooconnect toohello server de code, créer une table et chargez à l’aide de données hello un **insérer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="4025a-165">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="4025a-166">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [pilote sql accédez pour mysql](https://github.com/go-sql-driver/mysql#installation) comme un toocommunicate pilote avec Bonjour Azure de base de données de MySQL et hello [fmt package](https://golang.org/pkg/fmt/)imprimée d’entrée et en sortie sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-166">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="4025a-167">Hello code appelle la méthode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de données MySQL et la connexion de hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="4025a-167">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="4025a-168">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="4025a-169">appels de code Bonjour Bonjour [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) méthode plusieurs fois toorun plusieurs commandes DDL.</span><span class="sxs-lookup"><span data-stu-id="4025a-169">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several DDL commands.</span></span> <span data-ttu-id="4025a-170">code de Hello utilise également hello [Prepare()](http://go-database-sql.org/prepared.html) et Exec() toorun préparées avec des paramètres différents tooinsert trois lignes.</span><span class="sxs-lookup"><span data-stu-id="4025a-170">hello code also uses hello [Prepare()](http://go-database-sql.org/prepared.html) and Exec() toorun prepared statements with different parameters tooinsert three rows.</span></span> <span data-ttu-id="4025a-171">Chaque fois qu’une méthode checkError() personnalisée est toocheck utilisé si une erreur s’est produite et un dysfonctionnement tooexit.</span><span class="sxs-lookup"><span data-stu-id="4025a-171">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="4025a-172">Remplacez hello `host`, `database`, `user`, et `password` constantes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4025a-172">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase.")

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

## <a name="read-data"></a><span data-ttu-id="4025a-173">Lire les données</span><span class="sxs-lookup"><span data-stu-id="4025a-173">Read data</span></span>
<span data-ttu-id="4025a-174">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="4025a-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="4025a-175">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [pilote sql accédez pour mysql](https://github.com/go-sql-driver/mysql#installation) comme un toocommunicate pilote avec Bonjour Azure de base de données de MySQL et hello [fmt package](https://golang.org/pkg/fmt/)imprimée d’entrée et en sortie sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="4025a-176">Hello code appelle la méthode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de données MySQL et la connexion de hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="4025a-176">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="4025a-177">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="4025a-178">appels de code Bonjour Bonjour [Query()](https://golang.org/pkg/database/sql/#DB.Query) commande select de la méthode toorun hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-178">hello code calls hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) method toorun hello select command.</span></span> <span data-ttu-id="4025a-179">Ensuite il exécute [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate dans le jeu de résultats hello et [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) les valeurs de colonne de tooparse hello, l’enregistrement de la valeur de hello dans des variables.</span><span class="sxs-lookup"><span data-stu-id="4025a-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate through hello result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello column values, saving hello value into variables.</span></span> <span data-ttu-id="4025a-180">Chaque fois qu’une méthode checkError() personnalisée est toocheck utilisé si une erreur s’est produite et un dysfonctionnement tooexit.</span><span class="sxs-lookup"><span data-stu-id="4025a-180">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="4025a-181">Remplacez hello `host`, `database`, `user`, et `password` constantes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4025a-181">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
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

## <a name="update-data"></a><span data-ttu-id="4025a-182">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="4025a-182">Update data</span></span>
<span data-ttu-id="4025a-183">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="4025a-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="4025a-184">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [pilote sql accédez pour mysql](https://github.com/go-sql-driver/mysql#installation) comme un toocommunicate pilote avec Bonjour Azure de base de données de MySQL et hello [fmt package](https://golang.org/pkg/fmt/)imprimée d’entrée et en sortie sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="4025a-185">Hello code appelle la méthode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de données MySQL et la connexion de hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="4025a-185">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="4025a-186">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="4025a-187">appels de code Bonjour Bonjour [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) commande de mise à jour de la méthode toorun hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello update command.</span></span> <span data-ttu-id="4025a-188">Chaque fois qu’une méthode checkError() personnalisée est toocheck utilisé si une erreur s’est produite et un dysfonctionnement tooexit.</span><span class="sxs-lookup"><span data-stu-id="4025a-188">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="4025a-189">Remplacez hello `host`, `database`, `user`, et `password` constantes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4025a-189">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="4025a-190">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="4025a-190">Delete data</span></span>
<span data-ttu-id="4025a-191">Suivant de hello utilisation tooconnect de code et supprimer des données à l’aide un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="4025a-191">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4025a-192">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [pilote sql accédez pour mysql](https://github.com/go-sql-driver/mysql#installation) comme un toocommunicate pilote avec Bonjour Azure de base de données de MySQL et hello [fmt package](https://golang.org/pkg/fmt/)imprimée d’entrée et en sortie sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="4025a-193">Hello code appelle la méthode [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure base de données MySQL et la connexion de hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="4025a-193">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="4025a-194">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4025a-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="4025a-195">appels de code Bonjour Bonjour [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun de méthode de commande delete.</span><span class="sxs-lookup"><span data-stu-id="4025a-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello delete command.</span></span> <span data-ttu-id="4025a-196">Chaque fois qu’une méthode checkError() personnalisée est toocheck utilisé si une erreur s’est produite et un dysfonctionnement tooexit.</span><span class="sxs-lookup"><span data-stu-id="4025a-196">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="4025a-197">Remplacez hello `host`, `database`, `user`, et `password` constantes avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4025a-197">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="4025a-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4025a-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4025a-199">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="4025a-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
