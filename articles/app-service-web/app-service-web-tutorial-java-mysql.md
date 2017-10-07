---
title: aaaBuild une application web Java et MySQL dans Azure
description: "Découvrez comment tooget une application Java qui connecte service de base de données MySQL de Azure toohello dans Azure app service."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="1f949-103">Créer une application web Java et MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="1f949-104">Ce didacticiel vous montre comment toocreate Java web application dans Azure et le connecter tooa base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="1f949-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="1f949-105">Lorsque vous avez terminé, une application [Spring Boot](https://projects.spring.io/spring-boot/) stockera des données dans [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) s’exécutant sous [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="1f949-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Application Java s’exécutant dans Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="1f949-107">Ce tutoriel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f949-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f949-108">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="1f949-109">Se connecter à une base de données exemple application toohello</span><span class="sxs-lookup"><span data-stu-id="1f949-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="1f949-110">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="1f949-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="1f949-111">Mettre à jour et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="1f949-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="1f949-112">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="1f949-113">Analyser l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1f949-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f949-114">Prerequisites</span></span>

1. [<span data-ttu-id="1f949-115">Téléchargement et installation de Git</span><span class="sxs-lookup"><span data-stu-id="1f949-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="1f949-116">Téléchargez et installez hello Java JDK de 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="1f949-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="1f949-117">Téléchargement, installation et démarrage de MySQL</span><span class="sxs-lookup"><span data-stu-id="1f949-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1f949-118">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1f949-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1f949-119">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1f949-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1f949-120">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1f949-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="1f949-121">Préparation du MySQL local</span><span class="sxs-lookup"><span data-stu-id="1f949-121">Prepare local MySQL</span></span> 

<span data-ttu-id="1f949-122">Dans cette étape, vous créez une base de données dans un serveur MySQL local à utiliser dans le test application hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1f949-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="1f949-123">Se connecter tooMySQL server</span><span class="sxs-lookup"><span data-stu-id="1f949-123">Connect tooMySQL server</span></span>

<span data-ttu-id="1f949-124">Dans une fenêtre de terminal, connectez-vous tooyour local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="1f949-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="1f949-125">Vous pouvez utiliser cette fenêtre de terminal de toorun toutes les commandes hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1f949-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="1f949-126">Si vous êtes invité à entrer un mot de passe, entrez le mot de passe hello pour hello `root` compte.</span><span class="sxs-lookup"><span data-stu-id="1f949-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="1f949-127">Si vous avez oublié votre mot de passe du compte racine, consultez [MySQL : comment tooReset hello mot de passe racine](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="1f949-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="1f949-128">Si la commande est exécutée correctement, votre serveur MySQL est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1f949-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="1f949-129">Dans le cas contraire, assurez-vous que votre serveur MySQL local est démarrée par hello suivant [les étapes de post-installation MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="1f949-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="1f949-130">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="1f949-130">Create a database</span></span> 

<span data-ttu-id="1f949-131">Bonjour `mysql` invite, créer une base de données et une table pour hello choses.</span><span class="sxs-lookup"><span data-stu-id="1f949-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="1f949-132">Quittez votre connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="1f949-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="1f949-133">Créer et exécuter l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="1f949-133">Create and run hello sample app</span></span> 

<span data-ttu-id="1f949-134">Dans cette étape, vous clonez l’exemple d’application de démarrage du ressort, configurez la base de données MySQL locale toouse hello et exécutez sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1f949-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="1f949-135">Exemple hello de clone</span><span class="sxs-lookup"><span data-stu-id="1f949-135">Clone hello sample</span></span>

<span data-ttu-id="1f949-136">Dans la fenêtre de terminal hello, accédez à tooa utilisation dépôt d’exemples hello active et clone.</span><span class="sxs-lookup"><span data-stu-id="1f949-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="1f949-137">Configurer la base de données de MySQL hello application toouse hello</span><span class="sxs-lookup"><span data-stu-id="1f949-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="1f949-138">Hello de mise à jour `spring.datasource.password` et la valeur de *spring-boot-mysql-todo/src/main/resources/application.properties* avec hello même mot de passe racine utilisé invite de MySQL tooopen hello :</span><span class="sxs-lookup"><span data-stu-id="1f949-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="1f949-139">Générer et exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="1f949-139">Build and run hello sample</span></span>

<span data-ttu-id="1f949-140">Générer et exécuter l’exemple hello à l’aide du wrapper de Maven hello inclus dans le référentiel de hello :</span><span class="sxs-lookup"><span data-stu-id="1f949-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="1f949-141">Dans l’exemple hello en action, ouvrez votre toosee toohttp://localhost:8080 de navigateur.</span><span class="sxs-lookup"><span data-stu-id="1f949-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="1f949-142">Lorsque vous ajoutez la liste des tâches de toohello, utilisez hello SQL suivant des commandes hello MySQL tooview invite hello présentes dans MySQL.</span><span class="sxs-lookup"><span data-stu-id="1f949-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="1f949-143">Arrêter l’application hello en appuyant sur `Ctrl` + `C` Bonjour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="1f949-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="1f949-144">Création d’une base de données Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="1f949-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="1f949-145">Dans cette étape, vous allez créer un [base de données Azure pour MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1f949-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="1f949-146">Vous configurez toouse d’application exemple hello cette base de données ultérieurement dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="1f949-147">Hello utilisation Azure CLI 2.0 dans un fenêtre de terminal toocreate hello des ressources nécessaires toohost votre application Java dans Azure app service.</span><span class="sxs-lookup"><span data-stu-id="1f949-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="1f949-148">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="1f949-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="1f949-149">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1f949-149">Create a resource group</span></span>

<span data-ttu-id="1f949-150">Créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="1f949-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1f949-151">Un groupe de ressources Azure est un conteneur logique où les ressources associées comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="1f949-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="1f949-152">Hello exemple suivant crée un groupe de ressources dans la région Europe du Nord hello :</span><span class="sxs-lookup"><span data-stu-id="1f949-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="1f949-153">Vous pouvez utiliser pour les valeurs possibles hello toosee `--location`, utilisez hello [Liste emplacements az app service](/cli/azure/appservice#list-locations) commande.</span><span class="sxs-lookup"><span data-stu-id="1f949-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="1f949-154">Création d’un serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="1f949-154">Create a MySQL server</span></span>

<span data-ttu-id="1f949-155">Créer un serveur de base de données Azure pour MySQL (version préliminaire) avec hello [az mysql server créer](/cli/azure/mysql/server#create) commande.</span><span class="sxs-lookup"><span data-stu-id="1f949-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="1f949-156">Remplacez par votre propre nom de serveur MySQL unique dans lequel vous consultez hello `<mysql_server_name>` espace réservé.</span><span class="sxs-lookup"><span data-stu-id="1f949-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="1f949-157">Ce nom fait partie du nom d’hôte de votre serveur MySQL `<mysql_server_name>.mysql.database.azure.com`, par conséquent, il doit toobe global unique.</span><span class="sxs-lookup"><span data-stu-id="1f949-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="1f949-158">Remplacez également `<admin_user>` et `<admin_password>` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="1f949-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="1f949-159">Lorsque le serveur MySQL de hello est créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1f949-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="1f949-160">Configuration d’un pare-feu de serveur</span><span class="sxs-lookup"><span data-stu-id="1f949-160">Configure server firewall</span></span>

<span data-ttu-id="1f949-161">Créer une règle de pare-feu pour votre client de tooallow MySQL server connexions à l’aide de hello [az mysql server-règle de pare-feu créer](/cli/azure/mysql/server/firewall-rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="1f949-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="1f949-162">Azure Database pour MySQL (version préliminaire) ne permet pas encore les connexions automatiques à partir des services Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="1f949-163">Comme les adresses IP dans Azure sont attribuées dynamiquement, il est mieux tooenable toutes les adresses IP pour maintenant.</span><span class="sxs-lookup"><span data-stu-id="1f949-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="1f949-164">Service de hello continue son aperçu, meilleures méthodes pour la sécurisation de votre base de données seront activés.</span><span class="sxs-lookup"><span data-stu-id="1f949-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="1f949-165">Configurer la base de données MySQL de Azure hello</span><span class="sxs-lookup"><span data-stu-id="1f949-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="1f949-166">Dans la fenêtre de terminal hello sur votre ordinateur, connectez-vous toohello MySQL server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="1f949-167">Utilisez la valeur hello spécifiée précédemment pour `<admin_user>` et `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="1f949-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="1f949-168">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="1f949-168">Create a database</span></span> 

<span data-ttu-id="1f949-169">Bonjour `mysql` invite, créer une base de données et une table pour hello choses.</span><span class="sxs-lookup"><span data-stu-id="1f949-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="1f949-170">Création d’un utilisateur avec des autorisations</span><span class="sxs-lookup"><span data-stu-id="1f949-170">Create a user with permissions</span></span>

<span data-ttu-id="1f949-171">Créer un utilisateur de base de données et de lui donner tous les privilèges Bonjour `tododb` base de données.</span><span class="sxs-lookup"><span data-stu-id="1f949-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="1f949-172">Remplacez les espaces réservés de hello `<Javaapp_user>` et `<Javaapp_password>` avec votre propre nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="1f949-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="1f949-173">Quittez votre connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="1f949-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="1f949-174">Déployer hello exemple tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="1f949-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="1f949-175">Créer un plan de Service d’application Azure avec hello **libre** tarification à l’aide de hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande CLI.</span><span class="sxs-lookup"><span data-stu-id="1f949-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="1f949-176">un plan de Hello définit hello ressources physiques utilisées toohost vos applications.</span><span class="sxs-lookup"><span data-stu-id="1f949-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="1f949-177">Toutes les applications affectées tooan un plan de partagent ces ressources, ce qui vous toosave coût lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="1f949-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="1f949-178">Lorsque le plan de hello est prêt, hello Qu'azure CLI montre similaire de sortie toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1f949-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="1f949-179">Création d’une application web Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-179">Create an Azure Web app</span></span>

 <span data-ttu-id="1f949-180">Hello d’utilisation [az webapp créer](/cli/azure/appservice/web#create) toocreate de commande CLI une définition d’application web Bonjour `myAppServicePlan` plan App Service.</span><span class="sxs-lookup"><span data-stu-id="1f949-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="1f949-181">définition d’application web Hello fournit à votre application un tooaccess URL et configure plusieurs options toodeploy tooAzure de votre code.</span><span class="sxs-lookup"><span data-stu-id="1f949-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="1f949-182">Hello de substitution `<app_name>` espace réservé avec votre propre nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="1f949-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="1f949-183">Ce nom unique fait partie du nom de domaine par défaut hello pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="1f949-184">Vous pouvez mapper une application web de domaine personnalisé nom entrée toohello avant de vous exposez tooyour utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1f949-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="1f949-185">Lors de la définition d’application web hello est prête, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1f949-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="1f949-186">Configurer Java</span><span class="sxs-lookup"><span data-stu-id="1f949-186">Configure Java</span></span> 

<span data-ttu-id="1f949-187">Configuration de hello Java runtime dont votre application a besoin par hello [mise à jour du fichier config web app service az](/cli/azure/appservice/web/config#update) commande.</span><span class="sxs-lookup"><span data-stu-id="1f949-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="1f949-188">Hello commande suivante configure hello web application toorun sur une récente Java JDK de 8 et [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="1f949-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="1f949-189">Configurer la base de données de SQL Azure hello application toouse hello</span><span class="sxs-lookup"><span data-stu-id="1f949-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="1f949-190">Avant d’exécuter l’exemple d’application hello, définir les paramètres de l’application sur hello web application toouse hello Azure base de données MySQL que vous avez créé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="1f949-191">Ces propriétés sont toohello exposé à l’application web en tant que variables d’environnement et remplacent les valeurs de hello définies dans application.properties hello à l’intérieur de hello empaquetée web app.</span><span class="sxs-lookup"><span data-stu-id="1f949-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="1f949-192">Définir les paramètres de l’application à l’aide de [az webapp configuration appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) Bonjour CLI :</span><span class="sxs-lookup"><span data-stu-id="1f949-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="1f949-193">Obtention des informations d’identification de déploiement FTP</span><span class="sxs-lookup"><span data-stu-id="1f949-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="1f949-194">Vous pouvez déployer votre application tooAzure service d’applications de différentes manières, notamment FTP, local Git, GitHub, Visual Studio Team Services et BitBucket.</span><span class="sxs-lookup"><span data-stu-id="1f949-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="1f949-195">Pour cet exemple, FTP toodeploy hello. Fichier WAR créé précédemment sur votre ordinateur local de tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="1f949-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="1f949-196">toodetermine les informations d’identification les toopass le long dans un toohello commande ftp application Web, utilisez [az app service web de déploiement liste-publication-profils](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) commande :</span><span class="sxs-lookup"><span data-stu-id="1f949-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="1f949-197">Télécharger l’application hello à l’aide de FTP</span><span class="sxs-lookup"><span data-stu-id="1f949-197">Upload hello app using FTP</span></span>

<span data-ttu-id="1f949-198">Utilisez votre hello de toodeploy outil FTP favori. Toohello de fichier WAR */site/wwwroot/webapps* dossier sur l’adresse du serveur hello provenant de hello `URL` champ dans la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="1f949-199">Supprimer le répertoire de l’application hello existant par défaut (racine) et remplacez hello existants dans ROOT.war hello. Fichier WAR intégré hello plus haut dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="1f949-200">Application de test hello web</span><span class="sxs-lookup"><span data-stu-id="1f949-200">Test hello web app</span></span>

<span data-ttu-id="1f949-201">Parcourir trop`http://<app_name>.azurewebsites.net/` et ajouter quelques tâches toohello.</span><span class="sxs-lookup"><span data-stu-id="1f949-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Application Java s’exécutant dans Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="1f949-203">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="1f949-203">**Congratulations!**</span></span> <span data-ttu-id="1f949-204">Vous exécutez une application Java pilotée par les données dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1f949-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="1f949-205">Redéploiement et application hello de mise à jour</span><span class="sxs-lookup"><span data-stu-id="1f949-205">Update hello app and redeploy</span></span>

<span data-ttu-id="1f949-206">Mettre à jour hello application tooinclude une colonne supplémentaire dans la liste de tâches hello pour quel élément de hello jour a été créée.</span><span class="sxs-lookup"><span data-stu-id="1f949-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="1f949-207">Démarrage du ressort gère sans modifier vos enregistrements de base de données existante en tant que les modifications du modèle de données hello schéma de base de données mise à jour hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="1f949-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="1f949-208">Sur votre système local, ouvrez *src/main/java/com/example/fabrikam/TodoItem.java* et ajoutez suivant de hello importe toohello classe :</span><span class="sxs-lookup"><span data-stu-id="1f949-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="1f949-209">Ajouter un `String` propriété `timeCreated` trop*src/main/java/com/example/fabrikam/TodoItem.java*, l’initialiser avec un horodateur de création de l’objet.</span><span class="sxs-lookup"><span data-stu-id="1f949-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="1f949-210">Ajouter des accesseurs Get/Set pour hello nouvelle `timeCreated` propriété lorsque vous modifiez ce fichier.</span><span class="sxs-lookup"><span data-stu-id="1f949-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="1f949-211">Mise à jour *src/main/java/com/example/fabrikam/TodoDemoController.java* avec une ligne Bonjour `updateTodo` méthode tooset hello horodateur :</span><span class="sxs-lookup"><span data-stu-id="1f949-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="1f949-212">Ajouter la prise en charge pour le nouveau champ de hello dans le modèle de Thymeleaf hello.</span><span class="sxs-lookup"><span data-stu-id="1f949-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="1f949-213">Mise à jour *src/main/resources/templates/index.html* avec un nouvel en-tête de table pour hello timestamp et une nouvelle valeur hello toodisplay champ timestamp hello dans chaque ligne de données de table.</span><span class="sxs-lookup"><span data-stu-id="1f949-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="1f949-214">Régénérer l’application hello :</span><span class="sxs-lookup"><span data-stu-id="1f949-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="1f949-215">FTP hello mis à jour. WAR comme précédemment, supprimer des domaines existants de hello *site/wwwroot/WebApp/ROOT* active et *ROOT.war*, puis télécharger hello mis à jour. Fichier WAR comme ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="1f949-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="1f949-216">Lorsque vous actualisez l’application hello, un **créé** colonne est maintenant visible.</span><span class="sxs-lookup"><span data-stu-id="1f949-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="1f949-217">Lorsque vous ajoutez une nouvelle tâche, application hello remplir automatiquement hello timestamp.</span><span class="sxs-lookup"><span data-stu-id="1f949-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="1f949-218">Vos tâches existantes restent inchangées et de travailler avec l’application hello même si hello sous-jacente du modèle de données a changé.</span><span class="sxs-lookup"><span data-stu-id="1f949-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Mise à jour d’application Java avec une nouvelle colonne](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="1f949-220">Diffuser les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="1f949-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="1f949-221">Pendant que votre application Java s’exécute dans Azure App Service, vous pouvez obtenir les console hello journaux transmis directement tooyour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="1f949-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="1f949-222">De cette façon, vous pouvez obtenir hello des messages de diagnostic mêmes toohelp vous déboguez des erreurs d’application.</span><span class="sxs-lookup"><span data-stu-id="1f949-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="1f949-223">journal toostart de diffusion en continu, utilisez hello [la fin du journal de az webapp](/cli/azure/appservice/web/log#tail) commande.</span><span class="sxs-lookup"><span data-stu-id="1f949-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="1f949-224">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-224">Manage your Azure web app</span></span>

<span data-ttu-id="1f949-225">Accédez à toohello toosee portail Azure hello web app, que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1f949-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="1f949-226">toodo, connectez-vous trop[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f949-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="1f949-227">Dans le menu de gauche hello, cliquez sur **du Service d’applications**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="1f949-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="1f949-229">Par défaut, les lames de votre application web montre hello **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="1f949-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="1f949-230">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="1f949-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="1f949-231">Ici, vous pouvez également effectuer des tâches de gestion (arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="1f949-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="1f949-232">onglets Hello sur le côté gauche de hello du Panneau de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="1f949-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Panneau App Service sur le portail Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="1f949-234">Ces onglets dans le panneau de hello affichent hello de nombreuses fonctionnalités, vous pouvez ajouter l’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="1f949-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="1f949-235">Hello suivant liste vous donne quelques possibilités de hello :</span><span class="sxs-lookup"><span data-stu-id="1f949-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="1f949-236">Mapper un nom DNS personnalisé</span><span class="sxs-lookup"><span data-stu-id="1f949-236">Map a custom DNS name</span></span>
* <span data-ttu-id="1f949-237">Lier un certificat SSL personnalisé</span><span class="sxs-lookup"><span data-stu-id="1f949-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="1f949-238">Configurer le déploiement continu</span><span class="sxs-lookup"><span data-stu-id="1f949-238">Configure continuous deployment</span></span>
* <span data-ttu-id="1f949-239">Montée en puissance et augmentation de la taille des instances</span><span class="sxs-lookup"><span data-stu-id="1f949-239">Scale up and out</span></span>
* <span data-ttu-id="1f949-240">Ajouter une authentification utilisateur</span><span class="sxs-lookup"><span data-stu-id="1f949-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="1f949-241">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="1f949-241">Clean up resources</span></span>

<span data-ttu-id="1f949-242">Si vous ne devez pas ces ressources pour un autre didacticiel (consultez [étapes](#next)), vous pouvez les supprimer en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1f949-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="1f949-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f949-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f949-244">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="1f949-245">Se connecter à un toohello d’application exemple Java MySQL</span><span class="sxs-lookup"><span data-stu-id="1f949-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="1f949-246">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="1f949-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="1f949-247">Mettre à jour et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="1f949-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="1f949-248">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="1f949-249">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f949-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="1f949-250">Avancer toolearn de didacticiel suivant toohello toohello application de noms toomap DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="1f949-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="1f949-251">Mapper une tooAzure de nom DNS personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="1f949-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
