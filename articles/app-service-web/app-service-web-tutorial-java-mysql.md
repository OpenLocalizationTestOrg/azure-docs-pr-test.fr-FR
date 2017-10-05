---
title: "Créer une application web Java et MySQL dans Azure"
description: "Découvrez comment obtenir une application Java qui se connecte au service de base de données Azure MySQL dans Azure App Service."
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
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="f861a-103">Créer une application web Java et MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="f861a-104">Ce didacticiel vous montre comment créer une application web Java dans Azure et comment la connecter à une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="f861a-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="f861a-105">Lorsque vous avez terminé, une application [Spring Boot](https://projects.spring.io/spring-boot/) stockera des données dans [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) s’exécutant sous [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="f861a-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Application Java s’exécutant dans Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="f861a-107">Ce tutoriel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f861a-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f861a-108">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="f861a-109">Connecter une application exemple à la base de données</span><span class="sxs-lookup"><span data-stu-id="f861a-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="f861a-110">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f861a-111">Mise à jour et redéploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="f861a-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="f861a-112">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f861a-113">Surveiller l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f861a-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f861a-114">Prerequisites</span></span>

1. [<span data-ttu-id="f861a-115">Téléchargement et installation de Git</span><span class="sxs-lookup"><span data-stu-id="f861a-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="f861a-116">Téléchargement et installation du JDK Java 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="f861a-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="f861a-117">Téléchargement, installation et démarrage de MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f861a-118">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f861a-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f861a-119">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="f861a-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="f861a-120">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f861a-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="f861a-121">Préparation du MySQL local</span><span class="sxs-lookup"><span data-stu-id="f861a-121">Prepare local MySQL</span></span> 

<span data-ttu-id="f861a-122">Dans cette étape, vous allez créer une base de données dans un serveur MySQL local pour tester l’application en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f861a-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="f861a-123">Connexion au serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-123">Connect to MySQL server</span></span>

<span data-ttu-id="f861a-124">Dans une fenêtre de terminal, connectez-vous à votre serveur MySQL local.</span><span class="sxs-lookup"><span data-stu-id="f861a-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="f861a-125">Vous pouvez utiliser cette fenêtre de terminal pour exécuter toutes les commandes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f861a-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="f861a-126">Si vous êtes invité à entrer un mot de passe, tapez le mot de passe du compte `root`.</span><span class="sxs-lookup"><span data-stu-id="f861a-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="f861a-127">Si vous avez oublié votre mot de passe de compte racine, consultez [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html) (MySQL : réinitialisation du mot de passe racine).</span><span class="sxs-lookup"><span data-stu-id="f861a-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="f861a-128">Si la commande est exécutée correctement, votre serveur MySQL est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f861a-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="f861a-129">Dans le cas contraire, assurez-vous que votre serveur MySQL local est démarré en suivant ces [étapes consécutives à l’installation de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="f861a-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="f861a-130">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="f861a-130">Create a database</span></span> 

<span data-ttu-id="f861a-131">Dans l’invite `mysql`, créez une base de données et une table pour les éléments d’action.</span><span class="sxs-lookup"><span data-stu-id="f861a-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="f861a-132">Quittez votre connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="f861a-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="f861a-133">Création et exécution de l’application exemple</span><span class="sxs-lookup"><span data-stu-id="f861a-133">Create and run the sample app</span></span> 

<span data-ttu-id="f861a-134">Dans cette étape, vous allez cloner l’application Spring Boot, la configurer pour utiliser la base de données locale MySQL et l’exécuter sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f861a-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="f861a-135">Clonage de l’exemple</span><span class="sxs-lookup"><span data-stu-id="f861a-135">Clone the sample</span></span>

<span data-ttu-id="f861a-136">Dans la fenêtre de terminal, accédez à un répertoire de travail et clonez l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="f861a-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="f861a-137">Configuration de l’application pour utiliser la base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="f861a-138">Mettez à jour `spring.datasource.password` et la valeur dans *spring-boot-mysql-todo/src/main/resources/application.properties* avec le mot de passe racine utilisé pour ouvrir l’invite MySQL :</span><span class="sxs-lookup"><span data-stu-id="f861a-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="f861a-139">Créer et exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="f861a-139">Build and run the sample</span></span>

<span data-ttu-id="f861a-140">Générez et exécutez l’exemple à l’aide du wrapper Maven inclus dans le référentiel :</span><span class="sxs-lookup"><span data-stu-id="f861a-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="f861a-141">Ouvrez votre navigateur sur http://localhost: 8080 pour voir l’exemple en action.</span><span class="sxs-lookup"><span data-stu-id="f861a-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="f861a-142">Lorsque vous ajoutez des tâches à la liste, utilisez les commandes SQL suivantes dans l’invite MySQL pour afficher les données stockées dans MySQL.</span><span class="sxs-lookup"><span data-stu-id="f861a-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="f861a-143">Arrêtez l’application en appuyant sur `Ctrl`+`C` dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="f861a-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="f861a-144">Création d’une base de données Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="f861a-145">À cette étape, vous allez créer une instance [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) à l’aide de [l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f861a-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="f861a-146">Vous configurez l’exemple d’application pour utiliser cette base de données par la suite dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f861a-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="f861a-147">Utilisez l’interface Azure CLI 2.0 dans une fenêtre de terminal pour créer les ressources nécessaires pour héberger votre application Java dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f861a-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="f861a-148">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="f861a-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="f861a-149">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f861a-149">Create a resource group</span></span>

<span data-ttu-id="f861a-150">Créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f861a-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f861a-151">Un groupe de ressources Azure est un conteneur logique où les ressources associées comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="f861a-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="f861a-152">L’exemple suivant crée un groupe de ressources nommé dans la région Europe du Nord :</span><span class="sxs-lookup"><span data-stu-id="f861a-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="f861a-153">Pour connaître les valeurs que vous pouvez utiliser pour `--location`, utilisez la commande [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="f861a-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="f861a-154">Création d’un serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-154">Create a MySQL server</span></span>

<span data-ttu-id="f861a-155">Créez un serveur Azure Database pour MySQL (préversion) avec la commande [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="f861a-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="f861a-156">Indiquez le nom unique de votre propre serveur MySQL là où se trouve l’espace réservé `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="f861a-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="f861a-157">Ce nom fait partie du nom d’hôte de votre serveur MySQL, `<mysql_server_name>.mysql.database.azure.com`, et doit donc être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="f861a-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="f861a-158">Remplacez également `<admin_user>` et `<admin_password>` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f861a-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="f861a-159">Lorsque le serveur MySQL est créé, l’interface Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f861a-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="f861a-160">Configuration d’un pare-feu de serveur</span><span class="sxs-lookup"><span data-stu-id="f861a-160">Configure server firewall</span></span>

<span data-ttu-id="f861a-161">Créez une règle de pare-feu pour votre serveur MySQL afin d’autoriser les connexions client à l’aide de la commande [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="f861a-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="f861a-162">Azure Database pour MySQL (version préliminaire) ne permet pas encore les connexions automatiques à partir des services Azure.</span><span class="sxs-lookup"><span data-stu-id="f861a-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="f861a-163">Étant donné que les adresses IP sont affectées dynamiquement dans Azure, il est préférable d’activer toutes les adresses IP pour le moment.</span><span class="sxs-lookup"><span data-stu-id="f861a-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="f861a-164">Le service est pour le moment disponible en version préliminaire, mais de meilleures méthodes de sécurisation de votre base de données seront activées.</span><span class="sxs-lookup"><span data-stu-id="f861a-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="f861a-165">Configurer la base de données Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="f861a-166">Dans la fenêtre de terminal sur votre ordinateur, connectez-vous au serveur MySQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f861a-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="f861a-167">Utilisez la valeur que vous avez spécifiée précédemment pour `<admin_user>` et `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="f861a-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="f861a-168">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="f861a-168">Create a database</span></span> 

<span data-ttu-id="f861a-169">Dans l’invite `mysql`, créez une base de données et une table pour les éléments d’action.</span><span class="sxs-lookup"><span data-stu-id="f861a-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="f861a-170">Création d’un utilisateur avec des autorisations</span><span class="sxs-lookup"><span data-stu-id="f861a-170">Create a user with permissions</span></span>

<span data-ttu-id="f861a-171">Créez un utilisateur de base de données et accordez-lui tous les privilèges dans la base de données `tododb`.</span><span class="sxs-lookup"><span data-stu-id="f861a-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="f861a-172">Remplacez les espaces réservés `<Javaapp_user>` et `<Javaapp_password>` avec le nom de votre propre application unique.</span><span class="sxs-lookup"><span data-stu-id="f861a-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="f861a-173">Quittez votre connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="f861a-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="f861a-174">Déployer l’exemple dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f861a-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="f861a-175">Créez un plan Azure App Service avec le niveau tarifaire **Gratuit** à l’aide de la commande d’interface de ligne de commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="f861a-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="f861a-176">Le plan App Service définit les ressources physiques utilisées pour héberger vos applications.</span><span class="sxs-lookup"><span data-stu-id="f861a-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="f861a-177">Toutes les applications affectées à un plan App Service partagent ces ressources, ce qui vous permet de réduire les coûts lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="f861a-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="f861a-178">Lorsque le plan est prêt, l’interface de ligne de commande Azure affiche une sortie similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f861a-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="f861a-179">Création d’une application web Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-179">Create an Azure Web app</span></span>

 <span data-ttu-id="f861a-180">Utilisez la commande d’interface de ligne de commande [az webapp create](/cli/azure/appservice/web#create) pour créer une définition d’application web dans le plan App Service `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="f861a-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="f861a-181">La définition d’application web fournit une URL pour accéder à votre application et permet de configurer plusieurs options pour déployer votre code dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f861a-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="f861a-182">Remplacez l’espace réservé `<app_name>` avec votre propre nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="f861a-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="f861a-183">Ce nom unique est utilisé dans le nom de domaine par défaut de l’application web. Pour cette raison, ce nom doit être unique sur l’ensemble des applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f861a-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="f861a-184">Vous pouvez mapper une entrée de nom de domaine personnalisée vers l’application web avant de l’exposer à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f861a-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="f861a-185">Une fois que la définition de l’application web est prête, l’interface de ligne de commande Azure affiche des informations similaires à celles de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f861a-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="f861a-186">Configurer Java</span><span class="sxs-lookup"><span data-stu-id="f861a-186">Configure Java</span></span> 

<span data-ttu-id="f861a-187">Définissez la configuration d’exécution Java dont votre application a besoin avec la commande [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="f861a-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="f861a-188">La commande suivante configure l’application web de manière à ce qu’elle s’exécute sur un JDK Java 8 récent et sur [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="f861a-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="f861a-189">Configuration de l’application pour utiliser Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f861a-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="f861a-190">Avant d’exécuter l’exemple d’application, définissez les paramètres de l’application sur l’application web pour utiliser la base de données Azure MySQL que vous avez créée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f861a-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="f861a-191">Ces propriétés sont exposées à l’application web en tant que variables d’environnement et remplacent les valeurs définies dans les propriétés d’application dans l’application web empaquetée.</span><span class="sxs-lookup"><span data-stu-id="f861a-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="f861a-192">Définissez les paramètres d’application à l’aide de [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) dans l’interface de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="f861a-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="f861a-193">Obtention des informations d’identification de déploiement FTP</span><span class="sxs-lookup"><span data-stu-id="f861a-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="f861a-194">Vous pouvez déployer votre application dans Azure App Service de plusieurs façons, notamment FTP, Git local ainsi que GitHub, Visual Studio Team Services et BitBucket.</span><span class="sxs-lookup"><span data-stu-id="f861a-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="f861a-195">Pour cet exemple, FTP pour déployer le fichier .WAR basé précédemment sur votre ordinateur local dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f861a-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="f861a-196">Pour déterminer les informations d’identification à transmettre dans une commande FTP à l’application web, utilisez la commande [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) :</span><span class="sxs-lookup"><span data-stu-id="f861a-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="f861a-197">Télécharger l’application via FTP</span><span class="sxs-lookup"><span data-stu-id="f861a-197">Upload the app using FTP</span></span>

<span data-ttu-id="f861a-198">Utilisez votre outil FTP préféré pour déployer le fichier .WAR dans le dossier */site/wwwroot/webapps* sur l’adresse du serveur extraite du champ `URL` de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="f861a-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="f861a-199">Supprimez le répertoire existant de l’application (racine) par défaut et remplacez le ROOT.war existant avec le fichier .WAR créé plus haut dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f861a-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="f861a-200">Tester l’application web</span><span class="sxs-lookup"><span data-stu-id="f861a-200">Test the web app</span></span>

<span data-ttu-id="f861a-201">Accédez à `http://<app_name>.azurewebsites.net/` et ajoutez quelques tâches à la liste.</span><span class="sxs-lookup"><span data-stu-id="f861a-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Application Java s’exécutant dans Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="f861a-203">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="f861a-203">**Congratulations!**</span></span> <span data-ttu-id="f861a-204">Vous exécutez une application Java pilotée par les données dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f861a-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="f861a-205">Mise à jour de l’application et redéploiement</span><span class="sxs-lookup"><span data-stu-id="f861a-205">Update the app and redeploy</span></span>

<span data-ttu-id="f861a-206">Mettez à jour l’application pour inclure une colonne supplémentaire dans la liste des tâches pour le jour où l’élément a été créé.</span><span class="sxs-lookup"><span data-stu-id="f861a-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="f861a-207">Spring Boot gère la mise à jour du schéma de base de données pour vous, pendant que le modèle de données change sans modifier vos enregistrements de base de données existants.</span><span class="sxs-lookup"><span data-stu-id="f861a-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="f861a-208">Sur votre système local, ouvrez *src/main/java/com/example/fabrikam/TodoItem.java* et ajoutez les importations suivantes à la classe :</span><span class="sxs-lookup"><span data-stu-id="f861a-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="f861a-209">Ajouter une `String` propriété `timeCreated` à *src/main/java/com/example/fabrikam/TodoItem.java*, en l’initialisant avec un horodatage lors de la création de l’objet.</span><span class="sxs-lookup"><span data-stu-id="f861a-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="f861a-210">Ajoutez des méthodes getter et setter pour la nouvelle propriété `timeCreated` lorsque vous modifiez ce fichier.</span><span class="sxs-lookup"><span data-stu-id="f861a-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="f861a-211">Mettez à jour *src/main/java/com/example/fabrikam/TodoDemoController.java* avec une ligne dans la méthode `updateTodo` pour définir l’horodatage :</span><span class="sxs-lookup"><span data-stu-id="f861a-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="f861a-212">Ajoutez la prise en charge pour le nouveau champ dans le modèle Thymeleaf.</span><span class="sxs-lookup"><span data-stu-id="f861a-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="f861a-213">Mettez à jour *src/main/resources/templates/index.html* avec un nouvel en-tête de table pour l’horodatage et un nouveau champ pour afficher la valeur de l’horodatage dans chaque ligne de données de table.</span><span class="sxs-lookup"><span data-stu-id="f861a-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="f861a-214">Régénérez l’application :</span><span class="sxs-lookup"><span data-stu-id="f861a-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="f861a-215">Téléchargez en FTP le fichier .WAR mis à jour comme auparavant, en supprimant le répertoire existant *site/wwwroot/webapps/ROOT* et *ROOT.war*, puis en téléchargeant le fichier .WAR mis à jour en tant que ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="f861a-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="f861a-216">Lorsque vous actualisez l’application, une colonne **Heure de création** est maintenant visible.</span><span class="sxs-lookup"><span data-stu-id="f861a-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="f861a-217">Lorsque vous ajoutez une nouvelle tâche, l’application remplit automatiquement l’horodatage.</span><span class="sxs-lookup"><span data-stu-id="f861a-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="f861a-218">Vos tâches existantes restent inchangées et fonctionnent avec l’application même si le modèle de données sous-jacent a changé.</span><span class="sxs-lookup"><span data-stu-id="f861a-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![Mise à jour d’application Java avec une nouvelle colonne](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="f861a-220">Diffuser les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="f861a-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="f861a-221">Pendant l’exécution de votre application Java dans Azure App Service, vous pouvez acheminer les journaux de la console directement vers votre terminal.</span><span class="sxs-lookup"><span data-stu-id="f861a-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="f861a-222">De cette façon, vous pouvez obtenir les mêmes messages de diagnostic pour vous aider à déboguer les erreurs d’application.</span><span class="sxs-lookup"><span data-stu-id="f861a-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="f861a-223">Pour démarrer la diffusion de journaux, utilisez la commande [az webapp log tail](/cli/azure/appservice/web/log#tail).</span><span class="sxs-lookup"><span data-stu-id="f861a-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="f861a-224">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-224">Manage your Azure web app</span></span>

<span data-ttu-id="f861a-225">Accédez au portail Azure pour voir l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="f861a-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="f861a-226">Pour ce faire, connectez-vous au portail : [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f861a-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="f861a-227">Dans le menu de gauche, cliquez sur **App Service**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="f861a-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="f861a-229">Par défaut, le panneau de votre application web affiche la page **Présentation**.</span><span class="sxs-lookup"><span data-stu-id="f861a-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="f861a-230">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="f861a-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="f861a-231">Ici, vous pouvez également effectuer des tâches de gestion (arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="f861a-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="f861a-232">Les onglets figurant sur le côté gauche du panneau affichent les différentes pages de configuration que vous pouvez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="f861a-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Panneau App Service sur le portail Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="f861a-234">Ces onglets affichent les nombreuses fonctionnalités exceptionnelles que vous pouvez ajouter à votre application web.</span><span class="sxs-lookup"><span data-stu-id="f861a-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="f861a-235">La liste suivante fournit quelques exemples des possibilités :</span><span class="sxs-lookup"><span data-stu-id="f861a-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="f861a-236">Mapper un nom DNS personnalisé</span><span class="sxs-lookup"><span data-stu-id="f861a-236">Map a custom DNS name</span></span>
* <span data-ttu-id="f861a-237">Lier un certificat SSL personnalisé</span><span class="sxs-lookup"><span data-stu-id="f861a-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="f861a-238">Configurer le déploiement continu</span><span class="sxs-lookup"><span data-stu-id="f861a-238">Configure continuous deployment</span></span>
* <span data-ttu-id="f861a-239">Montée en puissance et augmentation de la taille des instances</span><span class="sxs-lookup"><span data-stu-id="f861a-239">Scale up and out</span></span>
* <span data-ttu-id="f861a-240">Ajouter une authentification utilisateur</span><span class="sxs-lookup"><span data-stu-id="f861a-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f861a-241">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="f861a-241">Clean up resources</span></span>

<span data-ttu-id="f861a-242">Si vous n’avez pas besoin de ces ressources pour un autre didacticiel (voir [Étapes suivantes](#next)), vous pouvez les supprimer en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f861a-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="f861a-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f861a-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f861a-244">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="f861a-245">Connecter un exemple d’application Java à MySQL</span><span class="sxs-lookup"><span data-stu-id="f861a-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="f861a-246">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f861a-247">Mise à jour et redéploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="f861a-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="f861a-248">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f861a-249">Gérer l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="f861a-250">Passez au didacticiel suivant pour découvrir comment mapper un nom DNS personnalisé à l’application.</span><span class="sxs-lookup"><span data-stu-id="f861a-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="f861a-251">Mapper un nom DNS personnalisé existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="f861a-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)