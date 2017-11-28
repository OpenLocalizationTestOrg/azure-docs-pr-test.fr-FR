---
title: "aaaConnect tooAzure base de données PostgreSQL à l’aide du langage Go | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple langage programmation Go vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour PostgreSQL."
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
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="cd7f8-103">Base de données Azure pour PostgreSQL : utilisent la commande Go langage tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="cd7f8-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="cd7f8-104">Ce démarrage rapide montre comment tooconnect tooan base de données Azure pour PostgreSQL à l’aide de code hello écrite dans [accédez](https://golang.org/) language (golang).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="cd7f8-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="cd7f8-106">Cet article suppose que vous êtes familiarisé avec le développement à l’aide de Go, mais que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd7f8-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cd7f8-107">Prerequisites</span></span>
<span data-ttu-id="cd7f8-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="cd7f8-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="cd7f8-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="cd7f8-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="cd7f8-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cd7f8-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="cd7f8-111">Installer le connecteur pour Go et pq</span><span class="sxs-lookup"><span data-stu-id="cd7f8-111">Install Go and pq connector</span></span>
<span data-ttu-id="cd7f8-112">Installer [accédez](https://golang.org/doc/install) et hello [Pure Postgres accédez pilote (LQ)](https://github.com/lib/pq) sur votre propre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="cd7f8-113">Selon votre plateforme, suivez les étapes de hello :</span><span class="sxs-lookup"><span data-stu-id="cd7f8-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="cd7f8-114">Windows</span><span class="sxs-lookup"><span data-stu-id="cd7f8-114">Windows</span></span>
1. <span data-ttu-id="cd7f8-115">[Télécharger](https://golang.org/dl/) et installer Go pour Microsoft Windows, en fonction de toohello [des instructions d’installation](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="cd7f8-116">Lancez l’invite de commandes hello à partir du menu Démarrer de hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="cd7f8-117">Créez un dossier pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-117">Make a folder for your project such.</span></span> <span data-ttu-id="cd7f8-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="cd7f8-119">Placez-vous dans le dossier du projet hello, tel que `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="cd7f8-120">Définissez la variable d’environnement hello pour le répertoire de code source GOPATH toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="cd7f8-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="cd7f8-122">Installer hello [Pure Postgres accédez pilote (LQ)](https://github.com/lib/pq) en exécutant hello `go get github.com/lib/pq` commande.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="cd7f8-123">En résumé, installez Go, puis exécuter ces commandes dans une invite de commandes hello :</span><span class="sxs-lookup"><span data-stu-id="cd7f8-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="cd7f8-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="cd7f8-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="cd7f8-125">Lancez l’interpréteur de commandes Bash hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="cd7f8-126">Installez Go en exécutant la commande `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="cd7f8-127">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="cd7f8-128">Placez-vous dans le dossier de hello, tel que `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="cd7f8-129">Ensemble hello GOPATH environnement variable toopoint tooa source valide répertoire, tel que votre accueil actuel du répertoire atteindre le dossier.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="cd7f8-130">À l’interpréteur de commandes bash hello, exécutez `export GOPATH=~/go` tooadd hello accédez répertoire comme hello GOPATH pour la session d’interpréteur de commandes en cours hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="cd7f8-131">Installer hello [Pure Postgres accédez pilote (LQ)](https://github.com/lib/pq) en exécutant hello `go get github.com/lib/pq` commande.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="cd7f8-132">Pour résumer, exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="cd7f8-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="cd7f8-133">Système d’exploitation mac d’Apple</span><span class="sxs-lookup"><span data-stu-id="cd7f8-133">Apple macOS</span></span>
1. <span data-ttu-id="cd7f8-134">Téléchargez et installez accèdent selon toohello [des instructions d’installation](https://golang.org/doc/install) correspondant à votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="cd7f8-135">Lancez l’interpréteur de commandes Bash hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="cd7f8-136">Créez un dossier pour votre projet dans votre répertoire de base, par exemple `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="cd7f8-137">Placez-vous dans le dossier de hello, tel que `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="cd7f8-138">Ensemble hello GOPATH environnement variable toopoint tooa source valide répertoire, tel que votre accueil actuel du répertoire atteindre le dossier.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="cd7f8-139">À l’interpréteur de commandes bash hello, exécutez `export GOPATH=~/go` tooadd hello accédez répertoire comme hello GOPATH pour la session d’interpréteur de commandes en cours hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="cd7f8-140">Installer hello [Pure Postgres accédez pilote (LQ)](https://github.com/lib/pq) en exécutant hello `go get github.com/lib/pq` commande.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="cd7f8-141">Pour résumer, installez Go, puis exécutez ces commandes Bash :</span><span class="sxs-lookup"><span data-stu-id="cd7f8-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="cd7f8-142">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="cd7f8-142">Get connection information</span></span>
<span data-ttu-id="cd7f8-143">Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="cd7f8-144">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cd7f8-145">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cd7f8-146">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="cd7f8-147">Cliquez sur le nom du serveur hello **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="cd7f8-148">Serveur hello sélectionnez **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="cd7f8-149">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cd7f8-150">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="cd7f8-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="cd7f8-151">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page et le nom de connexion d’administrateur du serveur hello de vue.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="cd7f8-152">Si nécessaire, le mot de passe réinitialisé hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="cd7f8-153">Générer et exécuter du code Go</span><span class="sxs-lookup"><span data-stu-id="cd7f8-153">Build and run Go code</span></span> 
1. <span data-ttu-id="cd7f8-154">toowrite Golang code, vous pouvez utiliser un simple éditeur de texte, tel que le bloc-notes dans Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) ou [Nano](https://www.nano-editor.org/) dans Ubuntu ou TextEdit dans macOS.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="cd7f8-155">Si vous préférez un environnement de développement interactif (EDI) plus complet, essayez [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft, ou [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="cd7f8-156">Collez le code de Golang de hello à partir des sections hello ci-dessous dans des fichiers texte et enregistrer dans votre dossier de projet avec l’extension de fichier \*.consultez la rubrique, telles que le chemin d’accès au Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` ou chemin d’accès de Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="cd7f8-157">Recherchez hello `HOST`, `DATABASE`, `USER`, et `PASSWORD` constantes dans le code hello et valeurs de l’exemple hello remplacer par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="cd7f8-158">Lancez l’invite de commandes hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="cd7f8-159">Basculez dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-159">Change directory into your project folder.</span></span> <span data-ttu-id="cd7f8-160">Par exemple, sur Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="cd7f8-161">Sur Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="cd7f8-162">Certains des environnements IDE de hello mentionnés offrent des fonctions de débogage et d’exécution sans nécessiter de commandes d’environnement.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="cd7f8-163">Exécuter le code de hello en tapant la commande hello `go run createtable.go` toocompile hello application et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="cd7f8-164">Vous pouvez également les code hello toobuild dans une application native, `go build createtable.go`, puis lancez `createtable.exe` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="cd7f8-165">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="cd7f8-165">Connect and create a table</span></span>
<span data-ttu-id="cd7f8-166">Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="cd7f8-167">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [package de pq](http://godoc.org/github.com/lib/pq) comme un toocommunicate pilote avec hello Postgres server et hello [fmt package](https://golang.org/pkg/fmt/) pour impression entrée et sortie de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="cd7f8-168">Hello code appelle la méthode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de données PostgreSQL et connexion hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cd7f8-169">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="cd7f8-170">appels de code Bonjour Bonjour [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) méthode plusieurs fois toorun plusieurs commandes SQL.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="cd7f8-171">Chaque fois un toocheck de méthode checkError() personnalisé que si une erreur s’est produite, paniquer tooexit si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="cd7f8-172">Remplacez hello `HOST`, `DATABASE`, `USER`, et `PASSWORD` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase")

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

## <a name="read-data"></a><span data-ttu-id="cd7f8-173">Lire les données</span><span class="sxs-lookup"><span data-stu-id="cd7f8-173">Read data</span></span>
<span data-ttu-id="cd7f8-174">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="cd7f8-175">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [package de pq](http://godoc.org/github.com/lib/pq) comme un toocommunicate pilote avec hello Postgres server et hello [fmt package](https://golang.org/pkg/fmt/) pour impression entrée et sortie de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="cd7f8-176">Hello code appelle la méthode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de données PostgreSQL et connexion hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cd7f8-177">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="cd7f8-178">requête select de Hello est exécutée en appelant la méthode [db. Query()](https://golang.org/pkg/database/sql/#DB.Query), et les lignes résultant hello est conservée dans une variable de type [lignes](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="cd7f8-179">code de Hello lit des valeurs de données de colonne hello hello ligne en cours à l’aide de la méthode [lignes. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) et effectue une boucle sur les lignes de hello à l’aide d’itérateur de hello [lignes. Next()](https://golang.org/pkg/database/sql/#Rows.Next) jusqu'à ce que plus aucune ligne n’existe.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="cd7f8-180">Les valeurs de colonne de chaque ligne sont console toohello imprimée out. Chaque fois un toocheck de méthode checkError() personnalisé que si une erreur s’est produite, paniquer tooexit si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="cd7f8-181">Remplacez hello `HOST`, `DATABASE`, `USER`, et `PASSWORD` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase")

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

## <a name="update-data"></a><span data-ttu-id="cd7f8-182">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="cd7f8-182">Update data</span></span>
<span data-ttu-id="cd7f8-183">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="cd7f8-184">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [package de pq](http://godoc.org/github.com/lib/pq) comme un toocommunicate pilote avec hello Postgres server et hello [fmt package](https://golang.org/pkg/fmt/) pour impression entrée et sortie de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="cd7f8-185">Hello code appelle la méthode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de données PostgreSQL et connexion hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cd7f8-186">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="cd7f8-187">appels de code Bonjour Bonjour [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun de méthode instruction SQL qui met à jour la table de hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="cd7f8-188">Un toocheck de méthode checkError() personnalisée si une erreur s’est produite et un dysfonctionnement tooexit si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="cd7f8-189">Remplacez hello `HOST`, `DATABASE`, `USER`, et `PASSWORD` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="cd7f8-190">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="cd7f8-190">Delete data</span></span>
<span data-ttu-id="cd7f8-191">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="cd7f8-192">code de Hello importe trois packages : hello [package sql](https://golang.org/pkg/database/sql/), hello [package de pq](http://godoc.org/github.com/lib/pq) comme un toocommunicate pilote avec hello Postgres server et hello [fmt package](https://golang.org/pkg/fmt/) pour impression entrée et sortie de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="cd7f8-193">Hello code appelle la méthode [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure base de données PostgreSQL et connexion hello de vérifications à l’aide de la méthode [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="cd7f8-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cd7f8-194">A [handle de la base de données](https://golang.org/pkg/database/sql/#DB) est utilisé partout, contenant le pool de connexions hello pour le serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="cd7f8-195">appels de code Bonjour Bonjour [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun de méthode instruction SQL qui met à jour la table de hello.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="cd7f8-196">Un toocheck de méthode checkError() personnalisée si une erreur s’est produite et un dysfonctionnement tooexit si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="cd7f8-197">Remplacez hello `HOST`, `DATABASE`, `USER`, et `PASSWORD` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="cd7f8-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="cd7f8-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd7f8-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cd7f8-199">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="cd7f8-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
