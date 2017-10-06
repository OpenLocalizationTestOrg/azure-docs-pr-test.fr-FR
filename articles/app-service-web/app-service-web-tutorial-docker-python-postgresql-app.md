---
title: aaaBuild une application web Python de Docker et PostgreSQL dans Azure | Documents Microsoft
description: "Découvrez comment tooget une application Python de Docker fonctionne dans Azure, avec une connexion tooa PostgreSQL de base de données."
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="179bf-103">Créer une application web Docker Python et PostgreSQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="179bf-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="179bf-104">Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement.</span><span class="sxs-lookup"><span data-stu-id="179bf-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="179bf-105">Ce didacticiel montre comment une base Python de Docker de toocreate web application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="179bf-106">Vous vous connecterez à cette base de données PostgreSQL tooa application.</span><span class="sxs-lookup"><span data-stu-id="179bf-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="179bf-107">Ceci fait, vous disposerez d’une application Python Flask s’exécutant dans un conteneur Docker sur [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="179bf-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Application Docker Python Flask dans Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="179bf-109">Vous pouvez suivre les étapes de hello ci-dessous sur macOS.</span><span class="sxs-lookup"><span data-stu-id="179bf-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="179bf-110">Les instructions de Linux et Windows sont même hello dans la plupart des cas, mais les différences hello ne sont pas détaillés dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="179bf-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="179bf-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="179bf-111">Prerequisites</span></span>

<span data-ttu-id="179bf-112">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="179bf-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="179bf-113">Installez Git</span><span class="sxs-lookup"><span data-stu-id="179bf-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="179bf-114">Installez Python</span><span class="sxs-lookup"><span data-stu-id="179bf-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="179bf-115">Téléchargez et exécutez PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="179bf-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="179bf-116">Installez Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="179bf-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="179bf-117">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="179bf-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="179bf-118">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="179bf-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="179bf-119">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="179bf-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="179bf-120">Test de l’installation PostgreSQL locale et création d’une base de données</span><span class="sxs-lookup"><span data-stu-id="179bf-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="179bf-121">Ouvrez la fenêtre de terminal hello et exécutez `psql postgres` tooconnect tooyour local PostgreSQL serveur.</span><span class="sxs-lookup"><span data-stu-id="179bf-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="179bf-122">Si la connexion est établie, cela signifie que votre base de données PostgreSQL est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="179bf-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="179bf-123">Dans le cas contraire, assurez-vous que votre base de données PostgresQL locale est démarré en suivant les étapes de hello à [téléchargements - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="179bf-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="179bf-124">Créez une base de données appelée *eventregistration* et configurez un utilisateur de base de données nommé *manager* avec le mot de passe *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="179bf-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="179bf-125">Type *\q* client de PostgreSQL tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="179bf-126">Création d’une application Python Flask locale</span><span class="sxs-lookup"><span data-stu-id="179bf-126">Create local Python Flask application</span></span>

<span data-ttu-id="179bf-127">Dans cette étape, vous définir un projet local Python ballon hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="179bf-128">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="179bf-128">Clone hello sample application</span></span>

<span data-ttu-id="179bf-129">Fenêtre de terminal ouverte hello et `CD` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="179bf-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="179bf-130">Suivante d’exécution hello commandes tooclone hello exemple référentiel et passer toohello *initialapp de 0,1* release.</span><span class="sxs-lookup"><span data-stu-id="179bf-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="179bf-131">Cet exemple de référentiel contient une application [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="179bf-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="179bf-132">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="179bf-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="179bf-133">Dans une étape ultérieure vous simplifiez ce processus en générant un toouse de conteneur Docker avec la base de données de production hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="179bf-134">Installer des packages hello requis et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="179bf-135">Lors de l’application hello est entièrement chargée, vous voyez quelque chose de similaire toohello message suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="179bf-136">Accédez toohttp://127.0.0.1:5000 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="179bf-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="179bf-137">Cliquez sur **S’inscrire**</span><span class="sxs-lookup"><span data-stu-id="179bf-137">Click **Register!**</span></span> <span data-ttu-id="179bf-138">et créez un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="179bf-138">and create a test user.</span></span>

![Application Python Flask s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="179bf-140">Hello, exemple d’application ballon stocke les données utilisateur dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="179bf-141">Si vous parvenez à l’inscription d’un utilisateur, votre application écrit les données toohello PostgreSQL base de données locale.</span><span class="sxs-lookup"><span data-stu-id="179bf-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="179bf-142">serveur de ballon hello toostop à tout moment, tapez Ctrl + C dans hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="179bf-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="179bf-143">Création d’une base de données de production PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="179bf-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="179bf-144">Dans cette étape, vous allez créer une base de données PostgreSQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="179bf-145">Lorsque votre application est déployée tooAzure, il utilisera cette base de données du cloud.</span><span class="sxs-lookup"><span data-stu-id="179bf-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="179bf-146">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="179bf-146">Log in tooAzure</span></span>

<span data-ttu-id="179bf-147">Vous êtes en train de ressources de cours toouse hello Azure CLI 2.0 toocreate hello nécessaire toohost votre application Python dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="179bf-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="179bf-148">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="179bf-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="179bf-149">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="179bf-149">Create a resource group</span></span>

<span data-ttu-id="179bf-150">Créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec hello [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="179bf-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="179bf-151">Hello exemple suivant crée un groupe de ressources dans la région ouest des États-Unis hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="179bf-152">Hello d’utilisation [Liste emplacements az appservice](/cli/azure/appservice#list-locations) les emplacements disponibles toolist de commande CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="179bf-153">Créer un serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="179bf-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="179bf-154">Créer un serveur de PostgreSQL avec hello [az postgres serveur créer](/cli/azure/documentdb#create) commande.</span><span class="sxs-lookup"><span data-stu-id="179bf-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="179bf-155">Bonjour suivant de commande, remplacez par un nom unique pour hello  *\<postgresql_name >* espace réservé et un nom d’utilisateur pour hello  *\<admin_username >* espace réservé .</span><span class="sxs-lookup"><span data-stu-id="179bf-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="179bf-156">nom du serveur Hello est utilisé dans le cadre de votre point de terminaison PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), de sorte que le nom hello doit toobe unique sur tous les serveurs dans Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="179bf-157">nom d’utilisateur Hello est pour le compte d’utilisateur admin hello initiale de la base de données.</span><span class="sxs-lookup"><span data-stu-id="179bf-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="179bf-158">Vous êtes invité à toopick un mot de passe pour cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="179bf-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="179bf-159">Lorsque hello Azure de base de données PostgreSQL serveur est créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="179bf-160">Créer une règle de pare-feu pour hello Azure de base de données PostgreSQL serveur</span><span class="sxs-lookup"><span data-stu-id="179bf-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="179bf-161">Exécutez hello suivant de base de données access toohello CLI d’Azure commande tooallow à partir de toutes les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="179bf-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="179bf-162">Hello CLI d’Azure confirme la création de règles de pare-feu hello avec toohello similaire de sortie l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="179bf-163">Se connecter à votre base de données Python ballon application toohello</span><span class="sxs-lookup"><span data-stu-id="179bf-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="179bf-164">Dans cette étape, vous vous connectez votre application toohello base de données Azure de Python ballon exemple pour serveur PostgreSQL que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="179bf-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="179bf-165">Création d’une base de données vide et configuration d’un nouvel utilisateur de l’application de base de données</span><span class="sxs-lookup"><span data-stu-id="179bf-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="179bf-166">Créer un utilisateur de base de données access tooa seule base de données uniquement.</span><span class="sxs-lookup"><span data-stu-id="179bf-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="179bf-167">Vous utiliserez ces tooavoid des informations d’identification donnant hello application complète toohello serveur d’accès.</span><span class="sxs-lookup"><span data-stu-id="179bf-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="179bf-168">Se connecter toohello de base de données (vous êtes invité à entrer votre mot de passe d’administrateur).</span><span class="sxs-lookup"><span data-stu-id="179bf-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="179bf-169">Créer des base de données hello et l’utilisateur à partir de hello PostgreSQL CLI.</span><span class="sxs-lookup"><span data-stu-id="179bf-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="179bf-170">Type *\q* client de PostgreSQL tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="179bf-171">Tester l’application hello localement par rapport à la base de données Azure PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="179bf-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="179bf-172">Si vous revenez en maintenant toohello *application* dossier Hello cloner le référentiel Github, vous pouvez exécuter des applications de Python ballon hello en mettant à jour les variables d’environnement hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="179bf-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="179bf-173">Lors de l’application hello est entièrement chargée, vous voyez quelque chose de similaire toohello message suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="179bf-174">Accédez toohttp://127.0.0.1:5000 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="179bf-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="179bf-175">Cliquez sur **S’inscrire**</span><span class="sxs-lookup"><span data-stu-id="179bf-175">Click **Register!**</span></span> <span data-ttu-id="179bf-176">et créez une inscription de test.</span><span class="sxs-lookup"><span data-stu-id="179bf-176">and create a test registration.</span></span> <span data-ttu-id="179bf-177">Maintenant, vous écrivez toohello de données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-177">You are now writing data toohello database in Azure.</span></span>

![Application Python Flask s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="179bf-179">Exécution de l’application hello à partir d’un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="179bf-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="179bf-180">Création d’image de conteneur Docker hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="179bf-181">Docker affiche une confirmation que le conteneur de hello informatique créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="179bf-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="179bf-182">Ajouter la base de données environnement variables tooan variable fichier d’environnement *db.env*.</span><span class="sxs-lookup"><span data-stu-id="179bf-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="179bf-183">application Hello se connecte à base de données PostgreSQL toohello de production dans Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="179bf-184">Exécuter l’application hello de conteneur Docker de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="179bf-185">Bonjour commande suivante spécifie le fichier de variable d’environnement hello et mappe hello par défaut ballon port 5000 toolocal port 5000.</span><span class="sxs-lookup"><span data-stu-id="179bf-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="179bf-186">sortie de Hello est toowhat similaires, vous avez vu plus haut.</span><span class="sxs-lookup"><span data-stu-id="179bf-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="179bf-187">Toutefois, la migration de base de données initiale hello n’a plus besoin toobe effectuée et qu’elle est donc ignorée.</span><span class="sxs-lookup"><span data-stu-id="179bf-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="179bf-188">base de données Hello contient déjà un enregistrement hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="179bf-188">hello database already contains hello registration you created previously.</span></span>

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="179bf-190">Télécharger le Registre de conteneur hello Docker conteneur tooa</span><span class="sxs-lookup"><span data-stu-id="179bf-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="179bf-191">Dans cette étape, vous téléchargez Registre de conteneur tooa hello Docker conteneur.</span><span class="sxs-lookup"><span data-stu-id="179bf-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="179bf-192">Vous allez utiliser Azure Container Registry, mais vous pourriez aussi d’autres registres très répandus, comme Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="179bf-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="179bf-193">Création d’un Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="179bf-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="179bf-194">Bonjour suivant commande toocreate un Registre de conteneur remplacer  *\<registry_name >* avec un nom de Registre de conteneur Azure unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="179bf-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="179bf-195">Sortie</span><span class="sxs-lookup"><span data-stu-id="179bf-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="179bf-196">Récupérer les informations d’identification du Registre hello pour les poussées et les images Docker</span><span class="sxs-lookup"><span data-stu-id="179bf-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="179bf-197">informations d’identification du Registre tooshow, activer le mode d’administration tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="179bf-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="179bf-198">Vous voyez deux mots de passe.</span><span class="sxs-lookup"><span data-stu-id="179bf-198">You see two passwords.</span></span> <span data-ttu-id="179bf-199">Notez hello nom d’utilisateur et mot de passe premier hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="179bf-200">Télécharger votre tooAzure de conteneur Docker Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="179bf-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="179bf-201">Déployer hello Docker Python ballon application tooAzure</span><span class="sxs-lookup"><span data-stu-id="179bf-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="179bf-202">Dans cette étape, vous déployez votre tooAzure d’application de la Python ballon lors du conteneur Docker du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="179bf-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="179bf-203">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="179bf-203">Create an App Service plan</span></span>

<span data-ttu-id="179bf-204">Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande.</span><span class="sxs-lookup"><span data-stu-id="179bf-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="179bf-205">Hello exemple suivant crée un plan de Service d’applications basés sur Linux nommé *myAppServicePlan* à l’aide de hello S1, niveau de tarification :</span><span class="sxs-lookup"><span data-stu-id="179bf-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="179bf-206">Lorsque hello plan App Service est créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="179bf-207">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="179bf-207">Create a web app</span></span>

<span data-ttu-id="179bf-208">Créer une application web Bonjour *myAppServicePlan* plan App Service avec hello [az webapp créer](/cli/azure/webapp#create) commande.</span><span class="sxs-lookup"><span data-stu-id="179bf-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="179bf-209">fournit les application Hello web vous un hébergement toodeploy votre code et de l’espace fournit une URL pour vous tooview hello déployé l’application.</span><span class="sxs-lookup"><span data-stu-id="179bf-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="179bf-210">Utilisez l’application web toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="179bf-211">Bonjour suivant de commande, remplacez hello  *\<nom_application >* espace réservé avec un nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="179bf-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="179bf-212">Ce nom fait partie de l’URL par défaut de hello pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="179bf-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="179bf-213">Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="179bf-214">Configurer les variables d’environnement hello de base de données</span><span class="sxs-lookup"><span data-stu-id="179bf-214">Configure hello database environment variables</span></span>

<span data-ttu-id="179bf-215">Plus haut dans le didacticiel de hello, vous avez défini de données PostgreSQL tooyour environnement variables tooconnect.</span><span class="sxs-lookup"><span data-stu-id="179bf-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="179bf-216">Dans le Service d’application, vous définissez les variables d’environnement _paramètres de l’application_ à l’aide de hello [az webapp configuration appsettings défini](/cli/azure/webapp/config#set) commande.</span><span class="sxs-lookup"><span data-stu-id="179bf-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="179bf-217">Hello exemple suivant spécifie détails de connexion de base de données hello en tant que paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="179bf-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="179bf-218">Il utilise également hello *PORT* variable toomap PORT 5000 à partir de votre conteneur Docker tooreceive HTTP le trafic sur le PORT 80.</span><span class="sxs-lookup"><span data-stu-id="179bf-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="179bf-219">Configuation du déploiement du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="179bf-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="179bf-220">AppService peut automatiquement télécharger et exécuter un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="179bf-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="179bf-221">Chaque fois que vous mettez à jour le conteneur Docker de hello ou modifiez les paramètres de hello, redémarrez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="179bf-222">Le redémarrage permet de s’assurer que tous les paramètres sont appliqués et conteneur de dernière hello est extraite à partir du Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="179bf-223">Parcourir toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="179bf-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="179bf-224">Parcourir l’application web toohello déployé à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="179bf-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="179bf-225">Hello web application prend plus de temps tooload parce que le conteneur de hello a toobe téléchargé et démarré après la modification de configuration du conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="179bf-226">Vous voyez des invités précédemment enregistrées qui ont été enregistrées de base de données de production Azure toohello à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="179bf-228">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="179bf-228">**Congratulations!**</span></span> <span data-ttu-id="179bf-229">Vous exécutez une application Python Flask basée sur un conteneur Docker dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="179bf-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="179bf-230">Mettre à jour le modèle de données et redéployer</span><span class="sxs-lookup"><span data-stu-id="179bf-230">Update data model and redeploy</span></span>

<span data-ttu-id="179bf-231">Dans cette étape, vous ajoutez nombre hello d’inscription d’événement de participants tooeach en mettant à jour le modèle d’invité hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="179bf-232">Extraire hello *0,2-migration* mise en production avec hello git commande suivante :</span><span class="sxs-lookup"><span data-stu-id="179bf-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="179bf-233">Cette version a déjà été hello du modèle, les contrôleurs et les modifications nécessaires tooviews.</span><span class="sxs-lookup"><span data-stu-id="179bf-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="179bf-234">Elle inclut également une migration de base de données générée via *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="179bf-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="179bf-235">Vous pouvez voir toutes les modifications apportées via hello git commande suivante :</span><span class="sxs-lookup"><span data-stu-id="179bf-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="179bf-236">Tester vos modifications en local</span><span class="sxs-lookup"><span data-stu-id="179bf-236">Test your changes locally</span></span>

<span data-ttu-id="179bf-237">Exécutez hello suivant de commandes tootest vos modifications localement par serveur de ballon hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="179bf-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="179bf-238">Mac / Linux :</span><span class="sxs-lookup"><span data-stu-id="179bf-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="179bf-239">Accédez à toohttp://127.0.0.1:5000 vos modifications de hello tooview navigateur.</span><span class="sxs-lookup"><span data-stu-id="179bf-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="179bf-240">Créez une inscription de test.</span><span class="sxs-lookup"><span data-stu-id="179bf-240">Create a test registration.</span></span>

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="179bf-242">Publier les modifications tooAzure</span><span class="sxs-lookup"><span data-stu-id="179bf-242">Publish changes tooAzure</span></span>

<span data-ttu-id="179bf-243">Générer la nouvelle image de docker hello, poussez-le Registre de conteneur toohello et redémarrez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="179bf-244">Accédez tooyour Azure web app et essayer à nouveau de nouvelles fonctionnalités de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="179bf-245">Créez un autre enregistrement d’événements.</span><span class="sxs-lookup"><span data-stu-id="179bf-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Application Docker Python Flask dans Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="179bf-247">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="179bf-247">Manage your Azure web app</span></span>

<span data-ttu-id="179bf-248">Accédez toohello [portail Azure](https://portal.azure.com) toosee vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="179bf-249">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="179bf-251">Par défaut, le portail de hello affiche de votre application web **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="179bf-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="179bf-252">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="179bf-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="179bf-253">Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="179bf-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="179bf-254">onglets Hello sur le côté gauche de hello de page de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="179bf-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Page App Service du Portail Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="179bf-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="179bf-256">Next steps</span></span>

<span data-ttu-id="179bf-257">Avancer toolearn de didacticiel suivant toohello tooyour l’application web de noms toomap DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="179bf-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="179bf-258">Mapper une tooAzure de nom DNS personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="179bf-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
