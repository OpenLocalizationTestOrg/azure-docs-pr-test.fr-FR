---
title: "Créer une application web Docker Python et PostgreSQL dans Azure | Microsoft Docs"
description: "Découvrez comment faire fonctionner une application Docker Python dans Azure en établissant une connexion à une base de données PostgreSQL."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="196ee-103">Créer une application web Docker Python et PostgreSQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="196ee-104">Azure Web Apps offre un service d’hébergement web hautement évolutif et appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="196ee-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="196ee-105">Ce didacticiel vous montre comment créer une application web Docker Python de base dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ee-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="196ee-106">Vous allez connecter cette application à une base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="196ee-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="196ee-107">Ceci fait, vous disposerez d’une application Python Flask s’exécutant dans un conteneur Docker sur [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="196ee-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Application Docker Python Flask dans Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="196ee-109">Vous pouvez suivre la procédure ci-dessous sur macOS.</span><span class="sxs-lookup"><span data-stu-id="196ee-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="196ee-110">Les instructions pour Linux et Windows sont identiques dans la plupart des cas, mais les différences ne sont pas détaillées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="196ee-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="196ee-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="196ee-111">Prerequisites</span></span>

<span data-ttu-id="196ee-112">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="196ee-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="196ee-113">Installez Git</span><span class="sxs-lookup"><span data-stu-id="196ee-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="196ee-114">Installez Python</span><span class="sxs-lookup"><span data-stu-id="196ee-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="196ee-115">Téléchargez et exécutez PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="196ee-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="196ee-116">Installez Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="196ee-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="196ee-117">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="196ee-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="196ee-118">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="196ee-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="196ee-119">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="196ee-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="196ee-120">Test de l’installation PostgreSQL locale et création d’une base de données</span><span class="sxs-lookup"><span data-stu-id="196ee-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="196ee-121">Ouvrez la fenêtre de terminal et exécutez `psql postgres` pour vous connecter à votre serveur PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="196ee-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="196ee-122">Si la connexion est établie, cela signifie que votre base de données PostgreSQL est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="196ee-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="196ee-123">Dans le cas contraire, assurez-vous que votre base de données PostgresQL est démarrée en suivant les étapes décrites dans la page [Downloads - PostgreSQL Core Distribution (Téléchargements - Distribution principale de PostgreSQL)](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="196ee-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="196ee-124">Créez une base de données appelée *eventregistration* et configurez un utilisateur de base de données nommé *manager* avec le mot de passe *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="196ee-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="196ee-125">Entrez *\q* pour quitter le client PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="196ee-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="196ee-126">Création d’une application Python Flask locale</span><span class="sxs-lookup"><span data-stu-id="196ee-126">Create local Python Flask application</span></span>

<span data-ttu-id="196ee-127">Cette étape consiste à configurer le projet Python Flask local.</span><span class="sxs-lookup"><span data-stu-id="196ee-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="196ee-128">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="196ee-128">Clone the sample application</span></span>

<span data-ttu-id="196ee-129">Ouvrez la fenêtre de terminal et entrez `CD` pour accéder à un répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="196ee-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="196ee-130">Exécutez les commandes suivantes pour cloner l’exemple de référentiel, puis accédez à la version *0.1-initialapp*.</span><span class="sxs-lookup"><span data-stu-id="196ee-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="196ee-131">Cet exemple de référentiel contient une application [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="196ee-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="196ee-132">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="196ee-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="196ee-133">Plus tard, vous simplifierez ce processus en créant un conteneur Docker à utiliser avec la base de données de production.</span><span class="sxs-lookup"><span data-stu-id="196ee-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="196ee-134">Installez les packages requis et démarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="196ee-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="196ee-135">Lorsque l’application est entièrement chargée, vous obtenez un message similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="196ee-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="196ee-136">Naviguez jusqu’à http://127.0.0.1:5000 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="196ee-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="196ee-137">Cliquez sur **S’inscrire**</span><span class="sxs-lookup"><span data-stu-id="196ee-137">Click **Register!**</span></span> <span data-ttu-id="196ee-138">et créez un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="196ee-138">and create a test user.</span></span>

![Application Python Flask s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="196ee-140">L’exemple d’application Flask stocke les données utilisateur dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="196ee-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="196ee-141">Si vous parvenez à inscrire un utilisateur, votre application écrit les données dans la base de données PostgreSQL locale.</span><span class="sxs-lookup"><span data-stu-id="196ee-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="196ee-142">À tout moment, pour arrêter le serveur Flask, tapez Ctrl+C dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="196ee-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="196ee-143">Création d’une base de données de production PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="196ee-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="196ee-144">Dans cette étape, vous allez créer une base de données PostgreSQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ee-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="196ee-145">Lorsque votre application est déployée sur Azure, elle utilise cette base de données cloud.</span><span class="sxs-lookup"><span data-stu-id="196ee-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="196ee-146">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-146">Log in to Azure</span></span>

<span data-ttu-id="196ee-147">Vous allez maintenant utiliser Azure CLI 2.0 pour créer les ressources nécessaires à l’hébergement de votre application Python dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="196ee-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="196ee-148">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="196ee-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="196ee-149">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="196ee-149">Create a resource group</span></span>

<span data-ttu-id="196ee-150">Créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="196ee-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="196ee-151">L’exemple suivant crée un groupe de ressources nommé dans la région États-Unis de l’Ouest :</span><span class="sxs-lookup"><span data-stu-id="196ee-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="196ee-152">Utilisez la commande [az appservice list-locations](/cli/azure/appservice#list-locations) dans Azure CLI pour afficher la liste des emplacements disponibles.</span><span class="sxs-lookup"><span data-stu-id="196ee-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="196ee-153">Créer un serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="196ee-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="196ee-154">Créez un serveur PostgreSQL avec la commande [az postgres server create](/cli/azure/documentdb#create).</span><span class="sxs-lookup"><span data-stu-id="196ee-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="196ee-155">Dans la commande suivante, remplacez un nom de serveur unique par l’espace réservé *\<postgresql_name>* et un nom d’utilisateur par l’espace réservé *\<admin_username>*.</span><span class="sxs-lookup"><span data-stu-id="196ee-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="196ee-156">Le nom de serveur est utilisé dans votre point de terminaison PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`). C’est pourquoi, il doit être unique parmi l’ensemble des serveurs dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ee-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="196ee-157">Le nom d’utilisateur correspond au compte d’utilisateur administrateur de la base de données initiale.</span><span class="sxs-lookup"><span data-stu-id="196ee-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="196ee-158">Vous êtes invité à choisir un mot de passe pour cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="196ee-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="196ee-159">Lorsque le serveur de base de données Azure pour PostgreSQL est créé, l’interface Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="196ee-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="196ee-160">Création d’une règle de pare-feu pour le serveur de base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="196ee-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="196ee-161">Exécutez la commande Azure CLI suivante pour autoriser l’accès à la base de données à partir de toutes les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="196ee-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="196ee-162">L’interface Azure CLI confirme la création de la règle de pare-feu avec une sortie similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="196ee-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="196ee-163">Connexion de votre application Python Flask à la base de données</span><span class="sxs-lookup"><span data-stu-id="196ee-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="196ee-164">Dans cette étape, vous connectez votre exemple d’application Python Flask au serveur de base de données Azure pour PostgreSQL que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="196ee-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="196ee-165">Création d’une base de données vide et configuration d’un nouvel utilisateur de l’application de base de données</span><span class="sxs-lookup"><span data-stu-id="196ee-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="196ee-166">Créez un utilisateur de base de données avec accès à une seule base de données.</span><span class="sxs-lookup"><span data-stu-id="196ee-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="196ee-167">Vous allez utiliser ces informations d’identification pour éviter que l’application ait un accès complet au serveur.</span><span class="sxs-lookup"><span data-stu-id="196ee-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="196ee-168">Connectez-vous à la base de données (vous êtes invité à entrer votre mot de passe d’administrateur).</span><span class="sxs-lookup"><span data-stu-id="196ee-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="196ee-169">Créez la base de données et l’utilisateur à partir de l’interface de ligne de commande de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="196ee-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="196ee-170">Entrez *\q* pour quitter le client PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="196ee-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="196ee-171">Test de l’application en local sur la base de données Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="196ee-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="196ee-172">Revenons maintenant au dossier *app* du référentiel Github cloné. Vous pouvez exécuter l’application Python Flask en mettant à jour les variables d’environnement de la base de données.</span><span class="sxs-lookup"><span data-stu-id="196ee-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="196ee-173">Lorsque l’application est entièrement chargée, vous obtenez un message similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="196ee-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="196ee-174">Naviguez jusqu’à http://127.0.0.1:5000 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="196ee-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="196ee-175">Cliquez sur **S’inscrire**</span><span class="sxs-lookup"><span data-stu-id="196ee-175">Click **Register!**</span></span> <span data-ttu-id="196ee-176">et créez une inscription de test.</span><span class="sxs-lookup"><span data-stu-id="196ee-176">and create a test registration.</span></span> <span data-ttu-id="196ee-177">Vous écrivez maintenant des données dans la base de données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ee-177">You are now writing data to the database in Azure.</span></span>

![Application Python Flask s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="196ee-179">Exécution de l’application à partir d’un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="196ee-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="196ee-180">Créez l’image conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="196ee-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="196ee-181">Docker affiche une confirmation de création du conteneur.</span><span class="sxs-lookup"><span data-stu-id="196ee-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="196ee-182">Ajoutez les variables d’environnement de base de données dans le fichier de variables d’environnement *db.env*.</span><span class="sxs-lookup"><span data-stu-id="196ee-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="196ee-183">L’application va se connecter à la base de données de production PostgreSQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ee-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="196ee-184">Exécutez l’application à partir du conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="196ee-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="196ee-185">La commande suivante spécifie le fichier de variables d’environnement et mappe le port Flask par défaut 5000 au port local 5000.</span><span class="sxs-lookup"><span data-stu-id="196ee-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="196ee-186">La sortie est similaire à ce que vous avez vu plus haut.</span><span class="sxs-lookup"><span data-stu-id="196ee-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="196ee-187">Toutefois, la migration de la base de données initiale n’a plus besoin d’être effectuée et elle est donc ignorée.</span><span class="sxs-lookup"><span data-stu-id="196ee-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="196ee-188">La base de données contient déjà l’inscription que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="196ee-188">The database already contains the registration you created previously.</span></span>

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="196ee-190">Charger le conteneur Docker vers un registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="196ee-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="196ee-191">Dans cette étape, vous chargez le conteneur Docker dans un registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="196ee-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="196ee-192">Vous allez utiliser Azure Container Registry, mais vous pourriez aussi d’autres registres très répandus, comme Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="196ee-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="196ee-193">Création d’un Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="196ee-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="196ee-194">Dans la commande suivante, pour créer un registre de conteneurs, remplacez *\<registry_name>* par un nom unique de registre de conteneurs Azure de votre choix.</span><span class="sxs-lookup"><span data-stu-id="196ee-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="196ee-195">Sortie</span><span class="sxs-lookup"><span data-stu-id="196ee-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="196ee-196">Récupération des informations d’identification du Registre pour l’extraction et la transmission d’images Docker</span><span class="sxs-lookup"><span data-stu-id="196ee-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="196ee-197">Pour afficher les informations d’identification du registre, activez d’abord le mode administration.</span><span class="sxs-lookup"><span data-stu-id="196ee-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="196ee-198">Vous voyez deux mots de passe.</span><span class="sxs-lookup"><span data-stu-id="196ee-198">You see two passwords.</span></span> <span data-ttu-id="196ee-199">Notez le nom d’utilisateur et le premier mot de passe.</span><span class="sxs-lookup"><span data-stu-id="196ee-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="196ee-200">Chargement de votre conteneur Docker vers Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="196ee-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="196ee-201">Déploiement de l’application Docker Python Flask sur Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="196ee-202">Dans cette étape, vous déployez votre application Python Flask basée sur le conteneur Docker dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="196ee-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="196ee-203">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="196ee-203">Create an App Service plan</span></span>

<span data-ttu-id="196ee-204">Créez un plan App Service avec la commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="196ee-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="196ee-205">L’exemple suivant crée un plan App Service Linux nommé *myAppServicePlan* avec le niveau tarifaire S1 :</span><span class="sxs-lookup"><span data-stu-id="196ee-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="196ee-206">Lorsque le plan App Service est créé, l’interface Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="196ee-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="196ee-207">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="196ee-207">Create a web app</span></span>

<span data-ttu-id="196ee-208">Créez une application web dans le plan App Service *myAppServicePlan* avec la commande [az webapp create](/cli/azure/webapp#create).</span><span class="sxs-lookup"><span data-stu-id="196ee-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="196ee-209">L’application web vous offre un espace d’hébergement pour déployer votre code, et fournit une URL pour vous permettre d’afficher l’application déployée.</span><span class="sxs-lookup"><span data-stu-id="196ee-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="196ee-210">Utilisez  pour créer l’application web.</span><span class="sxs-lookup"><span data-stu-id="196ee-210">Use  to create the web app.</span></span> 

<span data-ttu-id="196ee-211">Dans la commande suivante, remplacez l’espace réservé *\<app_name>* par un nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="196ee-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="196ee-212">Ce nom est utilisé dans l’URL par défaut de l’application web. C’est pourquoi il doit être unique parmi l’ensemble des applications dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="196ee-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="196ee-213">Une fois l’application web créée, Azure CLI affiche des informations similaires à celles de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="196ee-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="196ee-214">Configuration des variables d’environnement de base de données</span><span class="sxs-lookup"><span data-stu-id="196ee-214">Configure the database environment variables</span></span>

<span data-ttu-id="196ee-215">Plus haut dans ce didacticiel, vous avez défini des variables d’environnement pour vous connecter à votre base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="196ee-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="196ee-216">Dans App Service, vous définissez les variables d’environnement comme des _paramètres d’application_ à l’aide de la commande [az webapp config appsettings set](/cli/azure/webapp/config#set).</span><span class="sxs-lookup"><span data-stu-id="196ee-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="196ee-217">L’exemple suivant spécifie les informations de connexion à la base de données comme des paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="196ee-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="196ee-218">Il utilise également la variable *PORT* qui mappe le PORT 5000 de votre conteneur Docker pour qu’il reçoive le trafic HTTP sur le PORT 80.</span><span class="sxs-lookup"><span data-stu-id="196ee-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="196ee-219">Configuation du déploiement du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="196ee-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="196ee-220">AppService peut automatiquement télécharger et exécuter un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="196ee-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="196ee-221">Chaque fois que vous mettez à jour le conteneur Docker ou modifiez les paramètres, redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="196ee-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="196ee-222">Le redémarrage garantit que tous les paramètres sont appliqués et que le dernier conteneur est extrait du registre.</span><span class="sxs-lookup"><span data-stu-id="196ee-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="196ee-223">Rechercher l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="196ee-224">Accédez à l’application web déployée à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="196ee-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="196ee-225">L’application web prend plus de temps à se charger, car le conteneur doit être téléchargé et démarré lorsque sa configuration est modifiée.</span><span class="sxs-lookup"><span data-stu-id="196ee-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="196ee-226">Vous verrez des invités déjà inscrits, qui ont été enregistrés dans la base de données de production Azure à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="196ee-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="196ee-228">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="196ee-228">**Congratulations!**</span></span> <span data-ttu-id="196ee-229">Vous exécutez une application Python Flask basée sur un conteneur Docker dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="196ee-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="196ee-230">Mettre à jour le modèle de données et redéployer</span><span class="sxs-lookup"><span data-stu-id="196ee-230">Update data model and redeploy</span></span>

<span data-ttu-id="196ee-231">Dans cette étape, vous ajoutez le nombre de participants à chaque inscription d’événement en mettant à jour le modèle Invité.</span><span class="sxs-lookup"><span data-stu-id="196ee-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="196ee-232">Vérifiez la version *0.2-migration* avec la commande git suivante :</span><span class="sxs-lookup"><span data-stu-id="196ee-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="196ee-233">Cette version a déjà apporté les modifications nécessaires aux vues, aux contrôleurs et au modèle.</span><span class="sxs-lookup"><span data-stu-id="196ee-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="196ee-234">Elle inclut également une migration de base de données générée via *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="196ee-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="196ee-235">Vous pouvez voir toutes les modifications apportées, via la commande git suivante :</span><span class="sxs-lookup"><span data-stu-id="196ee-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="196ee-236">Tester vos modifications en local</span><span class="sxs-lookup"><span data-stu-id="196ee-236">Test your changes locally</span></span>

<span data-ttu-id="196ee-237">Exécutez les commandes suivantes pour tester vos modifications en local en exécutant le serveur Flask.</span><span class="sxs-lookup"><span data-stu-id="196ee-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="196ee-238">Mac / Linux :</span><span class="sxs-lookup"><span data-stu-id="196ee-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="196ee-239">Accédez à http://127.0.0.1:5000 dans votre navigateur pour afficher les modifications.</span><span class="sxs-lookup"><span data-stu-id="196ee-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="196ee-240">Créez une inscription de test.</span><span class="sxs-lookup"><span data-stu-id="196ee-240">Create a test registration.</span></span>

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="196ee-242">Publier les modifications dans Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-242">Publish changes to Azure</span></span>

<span data-ttu-id="196ee-243">Générez la nouvelle image Docker, placez-la dans le registre de conteneurs et redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="196ee-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="196ee-244">Accédez à votre application web Azure et essayez de nouveau la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="196ee-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="196ee-245">Créez un autre enregistrement d’événements.</span><span class="sxs-lookup"><span data-stu-id="196ee-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Application Docker Python Flask dans Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="196ee-247">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-247">Manage your Azure web app</span></span>

<span data-ttu-id="196ee-248">Accédez au [portail Azure](https://portal.azure.com) pour voir l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="196ee-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="196ee-249">Dans le menu de gauche, cliquez sur **App Services**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="196ee-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="196ee-251">Par défaut, le portail affiche la page **Vue d’ensemble** de votre application web.</span><span class="sxs-lookup"><span data-stu-id="196ee-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="196ee-252">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="196ee-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="196ee-253">Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="196ee-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="196ee-254">Les onglets sur le côté gauche de la page affichent les différentes pages de configuration que vous pouvez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="196ee-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Page App Service du Portail Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="196ee-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="196ee-256">Next steps</span></span>

<span data-ttu-id="196ee-257">Passez au didacticiel suivant pour découvrir comment mapper un nom DNS personnalisé à votre application web.</span><span class="sxs-lookup"><span data-stu-id="196ee-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="196ee-258">Mapper un nom DNS personnalisé existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="196ee-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
