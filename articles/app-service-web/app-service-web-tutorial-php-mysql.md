---
title: "Créer une application web PHP et MySQL dans Azure | Microsoft Docs"
description: "Découvrez comment faire fonctionner une application PHP dans Azure en établissant une connexion à une base de données MySQL dans Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e8d8962180f7534b0b9074f03ecc8ea431ae1a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="6ba99-103">Créer une application web PHP et MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="6ba99-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="6ba99-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6ba99-105">Ce didacticiel vous montre comment créer une application web PHP dans Azure et comment la connecter à une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="6ba99-105">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="6ba99-106">Une fois terminé, vous disposerez d’une application [Laravel](https://laravel.com/) s’exécutant dans Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="6ba99-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Application PHP exécutée dans Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="6ba99-108">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ba99-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6ba99-109">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6ba99-110">Connexion d’une application PHP à MySQL</span><span class="sxs-lookup"><span data-stu-id="6ba99-110">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="6ba99-111">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="6ba99-112">Mise à jour du modèle de données et redéploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="6ba99-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="6ba99-113">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6ba99-114">Gestion de l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ba99-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6ba99-115">Prerequisites</span></span>

<span data-ttu-id="6ba99-116">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="6ba99-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="6ba99-117">Installez Git</span><span class="sxs-lookup"><span data-stu-id="6ba99-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="6ba99-118">Installez PHP 5.6.4 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="6ba99-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="6ba99-119">Installez Composer</span><span class="sxs-lookup"><span data-stu-id="6ba99-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="6ba99-120">Activation des extensions PHP suivantes requises par Laravel : OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="6ba99-120">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="6ba99-121">Installez et démarrez MySQL</span><span class="sxs-lookup"><span data-stu-id="6ba99-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="6ba99-122">Préparation du MySQL local</span><span class="sxs-lookup"><span data-stu-id="6ba99-122">Prepare local MySQL</span></span>

<span data-ttu-id="6ba99-123">Dans cette étape, vous allez créer une base de données dans votre serveur MySQL local qui vous sera utile dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6ba99-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="6ba99-124">Se connecter au serveur MySQL local</span><span class="sxs-lookup"><span data-stu-id="6ba99-124">Connect to local MySQL server</span></span>

<span data-ttu-id="6ba99-125">Dans une fenêtre de terminal, connectez-vous à votre serveur MySQL local.</span><span class="sxs-lookup"><span data-stu-id="6ba99-125">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="6ba99-126">Vous pouvez utiliser cette fenêtre de terminal pour exécuter toutes les commandes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6ba99-126">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="6ba99-127">Si vous êtes invité à entrer un mot de passe, tapez le mot de passe du compte `root`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-127">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="6ba99-128">Si vous avez oublié votre mot de passe de compte racine, consultez [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html) (MySQL : réinitialisation du mot de passe racine).</span><span class="sxs-lookup"><span data-stu-id="6ba99-128">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="6ba99-129">Si la commande est exécutée correctement, votre serveur MySQL est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6ba99-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="6ba99-130">Dans le cas contraire, assurez-vous que votre serveur MySQL local est démarré en suivant ces [étapes consécutives à l’installation de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="6ba99-130">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="6ba99-131">Créer une base de données locale</span><span class="sxs-lookup"><span data-stu-id="6ba99-131">Create a database locally</span></span>

<span data-ttu-id="6ba99-132">À l’invite `mysql`, créez une base de données.</span><span class="sxs-lookup"><span data-stu-id="6ba99-132">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="6ba99-133">Quittez votre connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="6ba99-134">Créer une application PHP locale</span><span class="sxs-lookup"><span data-stu-id="6ba99-134">Create a PHP app locally</span></span>
<span data-ttu-id="6ba99-135">Dans cette étape, vous allez créer un exemple d’application Laravel, configurer sa connexion à la base de données et l’exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="6ba99-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="6ba99-136">Clonage de l’exemple</span><span class="sxs-lookup"><span data-stu-id="6ba99-136">Clone the sample</span></span>

<span data-ttu-id="6ba99-137">Dans la fenêtre de terminal, `cd` vers un répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="6ba99-137">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="6ba99-138">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="6ba99-138">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="6ba99-139">`cd` vers votre répertoire cloné.</span><span class="sxs-lookup"><span data-stu-id="6ba99-139">`cd` to your cloned directory.</span></span>
<span data-ttu-id="6ba99-140">Installez les packages requis.</span><span class="sxs-lookup"><span data-stu-id="6ba99-140">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="6ba99-141">Configuration de la connexion MySQL</span><span class="sxs-lookup"><span data-stu-id="6ba99-141">Configure MySQL connection</span></span>

<span data-ttu-id="6ba99-142">À la racine du référentiel, créez un fichier nommé *.env*.</span><span class="sxs-lookup"><span data-stu-id="6ba99-142">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="6ba99-143">Copiez les variables suivantes dans le fichier *.env*.</span><span class="sxs-lookup"><span data-stu-id="6ba99-143">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="6ba99-144">Remplacez l’espace réservé _&lt;root_password>_ par le mot de passe de l’utilisateur racine de MySQL.</span><span class="sxs-lookup"><span data-stu-id="6ba99-144">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="6ba99-145">Pour en savoir plus sur la manière dont Laravel utilise ce fichier _.env_, consultez [Configuration de l’environnement Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="6ba99-145">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="6ba99-146">Télécharger l’exemple localement</span><span class="sxs-lookup"><span data-stu-id="6ba99-146">Run the sample locally</span></span>

<span data-ttu-id="6ba99-147">Exécutez les [migrations de base de données Laravel](https://laravel.com/docs/5.4/migrations) pour créer les tables requises par l’application.</span><span class="sxs-lookup"><span data-stu-id="6ba99-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="6ba99-148">Pour voir quelles tables sont créées dans les migrations, consultez le répertoire _database/migrations_ dans le référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="6ba99-148">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6ba99-149">Générez une nouvelle clé d’application Laravel.</span><span class="sxs-lookup"><span data-stu-id="6ba99-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="6ba99-150">Exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="6ba99-150">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6ba99-151">Dans un navigateur, accédez à `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-151">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="6ba99-152">Ajoutez quelques tâches dans la page.</span><span class="sxs-lookup"><span data-stu-id="6ba99-152">Add a few tasks in the page.</span></span>

![PHP se connecte correctement à MySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="6ba99-154">Pour arrêter PHP, tapez `Ctrl + C` dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="6ba99-154">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="6ba99-155">Création de MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-155">Create MySQL in Azure</span></span>

<span data-ttu-id="6ba99-156">Dans cette étape, vous allez créer une base de données MySQL dans [Azure Database pour MySQL (Version préliminaire)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="6ba99-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="6ba99-157">Ensuite, vous configurerez l’application PHP pour la connexion à cette base de données.</span><span class="sxs-lookup"><span data-stu-id="6ba99-157">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6ba99-158">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6ba99-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="6ba99-159">Création d’un serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="6ba99-159">Create a MySQL server</span></span>

<span data-ttu-id="6ba99-160">Créez un serveur Azure Database pour MySQL (préversion) avec la commande [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="6ba99-160">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="6ba99-161">Dans la commande suivante, indiquez le nom unique de votre propre serveur MySQL là où se trouve l’espace réservé _&lt;mysql_server_name>_ (les caractères valides sont `a-z`, `0-9` et `-`).</span><span class="sxs-lookup"><span data-stu-id="6ba99-161">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="6ba99-162">Ce nom fait partie du nom d’hôte du serveur MySQL (`<mysql_server_name>.database.windows.net`) et doit donc être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="6ba99-162">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="6ba99-163">Lorsque le serveur MySQL est créé, l’interface Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6ba99-163">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="6ba99-164">Configuration d’un pare-feu de serveur</span><span class="sxs-lookup"><span data-stu-id="6ba99-164">Configure server firewall</span></span>

<span data-ttu-id="6ba99-165">Créez une règle de pare-feu pour votre serveur MySQL afin d’autoriser les connexions client à l’aide de la commande [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="6ba99-165">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="6ba99-166">Pour le moment, Azure Database pour MySQL (version préliminaire) ne limite pas les connexions aux services Azure seulement.</span><span class="sxs-lookup"><span data-stu-id="6ba99-166">Azure Database for MySQL (Preview) doesn't currently limit connections only to Azure services.</span></span> <span data-ttu-id="6ba99-167">Étant donné que les adresses IP sont affectées dynamiquement dans Azure, il est préférable d’activer toutes les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="6ba99-167">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses.</span></span> <span data-ttu-id="6ba99-168">Le service est en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="6ba99-168">The service is in preview.</span></span> <span data-ttu-id="6ba99-169">Les meilleures méthodes de sécurisation de votre base de données sont planifiées.</span><span class="sxs-lookup"><span data-stu-id="6ba99-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="6ba99-170">Se connecter au serveur de production MySQL localement</span><span class="sxs-lookup"><span data-stu-id="6ba99-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="6ba99-171">Dans la fenêtre de terminal, connectez-vous au serveur MySQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="6ba99-172">Utilisez la valeur spécifiée précédemment pour _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="6ba99-173">Lorsqu’une invite de mot de passe apparaît, utilisez _$tr0ngPa$w0rd!_, que vous avez spécifié lors de la création de la base de données.</span><span class="sxs-lookup"><span data-stu-id="6ba99-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="6ba99-174">Création d’une base de données de production</span><span class="sxs-lookup"><span data-stu-id="6ba99-174">Create a production database</span></span>

<span data-ttu-id="6ba99-175">À l’invite `mysql`, créez une base de données.</span><span class="sxs-lookup"><span data-stu-id="6ba99-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="6ba99-176">Création d’un utilisateur avec des autorisations</span><span class="sxs-lookup"><span data-stu-id="6ba99-176">Create a user with permissions</span></span>

<span data-ttu-id="6ba99-177">Créez un utilisateur de base de données nommé _phpappuser_ et accordez-lui tous les privilèges dans la base de données `sampledb`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="6ba99-178">Quittez la connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="6ba99-179">Connexion de l’application à Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="6ba99-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="6ba99-180">Dans cette étape, vous allez connecter l’application PHP à la base de données MySQL que vous avez créée dans Azure Database pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6ba99-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="6ba99-181">Configurer la connexion à la base de données</span><span class="sxs-lookup"><span data-stu-id="6ba99-181">Configure the database connection</span></span>

<span data-ttu-id="6ba99-182">À la racine du référentiel, créez un fichier _.env.production_ et copiez-y les variables suivantes.</span><span class="sxs-lookup"><span data-stu-id="6ba99-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="6ba99-183">Remplacez l’espace réservé _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="6ba99-184">Enregistrez les modifications.</span><span class="sxs-lookup"><span data-stu-id="6ba99-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="6ba99-185">Pour sécuriser vos informations de connexion MySQL, ce fichier est déjà exclu du référentiel Git (consultez _.gitignore_ dans la racine du référentiel).</span><span class="sxs-lookup"><span data-stu-id="6ba99-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="6ba99-186">Vous apprendrez ultérieurement à configurer les variables d’environnement dans App Service pour vous connecter à votre base de données dans Azure Database pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6ba99-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="6ba99-187">Avec les variables d’environnement, vous n’avez pas besoin du fichier *.env* dans App Service.</span><span class="sxs-lookup"><span data-stu-id="6ba99-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="6ba99-188">Configuration du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="6ba99-188">Configure SSL certificate</span></span>

<span data-ttu-id="6ba99-189">Par défaut, la base de données Azure pour MySQL applique les connexions SSL à partir des clients.</span><span class="sxs-lookup"><span data-stu-id="6ba99-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="6ba99-190">Pour vous connecter à votre base de données MySQL dans Azure, vous devez utiliser un certificat SSL _.pem_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-190">To connect to your MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="6ba99-191">Ouvrez _config/database.php_ et ajoutez les paramètres _sslmode_ et _options_ à `connections.mysql`, comme illustré dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6ba99-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="6ba99-192">Pour savoir comment générer ce fichier _certificate.pem_, consultez l’article [Configuration de la connectivité SSL dans votre application pour se connecter en toute sécurité à la base de données Azure pour MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="6ba99-192">To learn how to generate this _certificate.pem_, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="6ba99-193">Le chemin d’accès _/ssl/certificate.pem_ pointe vers un fichier _certificate.pem_ existant dans le référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="6ba99-193">The path _/ssl/certificate.pem_ points to an existing _certificate.pem_ file in the Git repository.</span></span> <span data-ttu-id="6ba99-194">Dans ce didacticiel, ce fichier est fourni pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="6ba99-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="6ba99-195">Il est préférable de ne pas valider vos certificats _.pem_ dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="6ba99-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-the-application-locally"></a><span data-ttu-id="6ba99-196">Tester localement l’application</span><span class="sxs-lookup"><span data-stu-id="6ba99-196">Test the application locally</span></span>

<span data-ttu-id="6ba99-197">Exécutez les migrations de base de données Laravel avec _.env.production_ comme fichier d’environnement pour créer les tables dans votre base de données MySQL dans Azure Database pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6ba99-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="6ba99-198">N’oubliez pas que _. env.production_ contient les informations de connexion à votre base de données MySQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6ba99-199">_.env.production_ n’a pas encore de clé d’application valide.</span><span class="sxs-lookup"><span data-stu-id="6ba99-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="6ba99-200">Générez-en une pour lui dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="6ba99-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="6ba99-201">Exécutez l’exemple d’application avec _.env.production_ comme fichier d’environnement.</span><span class="sxs-lookup"><span data-stu-id="6ba99-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="6ba99-202">Accédez à `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="6ba99-203">Si la page se charge sans erreur, l’application PHP se connecte à la base de données MySQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="6ba99-204">Ajoutez quelques tâches dans la page.</span><span class="sxs-lookup"><span data-stu-id="6ba99-204">Add a few tasks in the page.</span></span>

![PHP se connecte correctement à Azure Database pour MySQL (version préliminaire)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="6ba99-206">Pour arrêter PHP, tapez `Ctrl + C` dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="6ba99-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="6ba99-207">Validation de vos modifications</span><span class="sxs-lookup"><span data-stu-id="6ba99-207">Commit your changes</span></span>

<span data-ttu-id="6ba99-208">Exécutez les commandes Git suivantes pour valider vos modifications :</span><span class="sxs-lookup"><span data-stu-id="6ba99-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="6ba99-209">Votre application est prête à être déployée.</span><span class="sxs-lookup"><span data-stu-id="6ba99-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="6ba99-210">Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-210">Deploy to Azure</span></span>

<span data-ttu-id="6ba99-211">Dans cette étape, vous allez déployer l’application PHP connectée à MySQL dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6ba99-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6ba99-212">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="6ba99-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="6ba99-213">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="6ba99-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-the-php-version"></a><span data-ttu-id="6ba99-214">Définition de la version PHP</span><span class="sxs-lookup"><span data-stu-id="6ba99-214">Set the PHP version</span></span>

<span data-ttu-id="6ba99-215">Définissez la version PHP requise par l’application en utilisant la commande [az webapp config set](/cli/azure/webapp/config#set).</span><span class="sxs-lookup"><span data-stu-id="6ba99-215">Set the PHP version that the application requires by using the [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="6ba99-216">La commande suivante définit la version PHP sur _7.0_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-216">The following command sets the PHP version to _7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="6ba99-217">Configuration des paramètres de la base de données</span><span class="sxs-lookup"><span data-stu-id="6ba99-217">Configure database settings</span></span>

<span data-ttu-id="6ba99-218">Comme indiqué précédemment, vous pouvez vous connecter à votre base de données Azure MySQL en utilisant des variables d’environnement dans App Service.</span><span class="sxs-lookup"><span data-stu-id="6ba99-218">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="6ba99-219">Dans App Service, vous définissez les variables d’environnement en tant que _paramètres d’application_ à l’aide de la commande [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="6ba99-219">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="6ba99-220">La commande suivante configure les paramètres d’application `DB_HOST`, `DB_DATABASE`, `DB_USERNAME` et `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="6ba99-221">Remplacez les espaces réservés _&lt;appname>_ et _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="6ba99-222">Vous pouvez utiliser la méthode PHP [getenv](http://www.php.net/manual/function.getenv.php) pour accéder aux paramètres.</span><span class="sxs-lookup"><span data-stu-id="6ba99-222">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="6ba99-223">Votre code Laravel utilise un wrapper [env](https://laravel.com/docs/5.4/helpers#method-env) sur le PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="6ba99-224">Par exemple, la configuration MySQL dans _config/database.php_ ressemble au code suivant :</span><span class="sxs-lookup"><span data-stu-id="6ba99-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="6ba99-225">Configuration des variables d’environnement Laravel</span><span class="sxs-lookup"><span data-stu-id="6ba99-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="6ba99-226">Laravel a besoin d’une clé d’application dans App Service.</span><span class="sxs-lookup"><span data-stu-id="6ba99-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="6ba99-227">Vous pouvez la configurer avec les paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="6ba99-227">You can configure it with app settings.</span></span>

<span data-ttu-id="6ba99-228">Utilisez `php artisan` pour générer une nouvelle clé d’application sans l’enregistrer dans _.env_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="6ba99-229">Définissez la clé d’application dans l’application web App Service en utilisant la commande [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="6ba99-229">Set the application key in the App Service web app by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="6ba99-230">Remplacez les espaces réservés _&lt;appname>_ et _&lt;outputofphpartisankey:generate>_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="6ba99-231">`APP_DEBUG="true"` indique à Laravel de renvoyer les informations de débogage lorsque l’application web déployée rencontre des erreurs.</span><span class="sxs-lookup"><span data-stu-id="6ba99-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="6ba99-232">Lorsque vous exécutez une application de production, affectez-lui la valeur `false`, qui est plus sécurisée.</span><span class="sxs-lookup"><span data-stu-id="6ba99-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="6ba99-233">Définition du chemin d’accès de l’application virtuelle</span><span class="sxs-lookup"><span data-stu-id="6ba99-233">Set the virtual application path</span></span>

<span data-ttu-id="6ba99-234">Définissez le chemin d’accès de l’application virtuelle pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="6ba99-234">Set the virtual application path for the web app.</span></span> <span data-ttu-id="6ba99-235">Cette étape est requise car le [cycle de vie de l’application Laravel](https://laravel.com/docs/5.4/lifecycle) commence dans le répertoire _public_ et non pas dans le répertoire racine de votre application.</span><span class="sxs-lookup"><span data-stu-id="6ba99-235">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="6ba99-236">Les autres infrastructures PHP dont le cycle de vie démarre dans le répertoire racine peuvent fonctionner sans configuration manuelle du chemin d’accès à l’application virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6ba99-236">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="6ba99-237">Définissez le chemin d’accès à l’application virtuelle en utilisant la commande [az resource update](/cli/azure/resource#update).</span><span class="sxs-lookup"><span data-stu-id="6ba99-237">Set the virtual application path by using the [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="6ba99-238">Remplacez l’espace réservé _&lt;appname>_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-238">Replace the _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="6ba99-239">Par défaut, Azure App Service pointe le chemin d’accès à l’application virtuelle (_/_) vers le répertoire racine des fichiers d’application déployés (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="6ba99-239">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="6ba99-240">Configuration d’un utilisateur de déploiement</span><span class="sxs-lookup"><span data-stu-id="6ba99-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="6ba99-241">Configurer le déploiement Git local</span><span class="sxs-lookup"><span data-stu-id="6ba99-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-to-azure-from-git"></a><span data-ttu-id="6ba99-242">Effectuer une transmission de type push vers Azure à partir de Git</span><span class="sxs-lookup"><span data-stu-id="6ba99-242">Push to Azure from Git</span></span>

<span data-ttu-id="6ba99-243">Ajoutez un référentiel distant Azure dans votre référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="6ba99-243">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="6ba99-244">Effectuez une transmission de type push vers le référentiel distant Azure pour déployer l’application PHP.</span><span class="sxs-lookup"><span data-stu-id="6ba99-244">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="6ba99-245">Le mot de passe que vous avez fourni précédemment dans le cadre de la création de l’utilisateur du déploiement vous est demandé.</span><span class="sxs-lookup"><span data-stu-id="6ba99-245">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="6ba99-246">Au cours du déploiement, Azure App Service communique sa progression avec Git.</span><span class="sxs-lookup"><span data-stu-id="6ba99-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="6ba99-247">Vous remarquerez peut-être que le processus de déploiement installe les packages [Composer](https://getcomposer.org/) à la fin.</span><span class="sxs-lookup"><span data-stu-id="6ba99-247">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="6ba99-248">App Service n’exécute pas ces automatisations pendant le déploiement par défaut. Cet exemple de référentiel possède donc trois fichiers supplémentaires dans son répertoire racine pour l’activer :</span><span class="sxs-lookup"><span data-stu-id="6ba99-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="6ba99-249">`.deployment` : ce fichier indique à App Service d’exécuter `bash deploy.sh` en tant que script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="6ba99-249">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="6ba99-250">`deploy.sh` : le script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="6ba99-250">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="6ba99-251">Si vous examinez le fichier, vous verrez qu’il exécute `php composer.phar install` après `npm install`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-251">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="6ba99-252">`composer.phar` - Le Gestionnaire de package Composer.</span><span class="sxs-lookup"><span data-stu-id="6ba99-252">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="6ba99-253">Vous pouvez utiliser cette approche pour ajouter une étape à votre déploiement Git sur App Service.</span><span class="sxs-lookup"><span data-stu-id="6ba99-253">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="6ba99-254">Pour plus d'informations, consultez le [script de déploiement personnalisé](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="6ba99-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="6ba99-255">Rechercher l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-255">Browse to the Azure web app</span></span>

<span data-ttu-id="6ba99-256">Accédez à `http://<app_name>.azurewebsites.net` et ajoutez quelques tâches à la liste.</span><span class="sxs-lookup"><span data-stu-id="6ba99-256">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![Application PHP exécutée dans Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="6ba99-258">Félicitations, vous exécutez une application PHP orientée données dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6ba99-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="6ba99-259">Mettre à jour et redéployer un modèle localement</span><span class="sxs-lookup"><span data-stu-id="6ba99-259">Update model locally and redeploy</span></span>

<span data-ttu-id="6ba99-260">Dans cette étape, vous allez apporter une modification simple au modèle de données `task` et à l’application web, puis publier la mise à jour sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-260">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="6ba99-261">Pour le scénario des tâches, vous modifiez l’application afin de pouvoir marquer une tâche comme terminée.</span><span class="sxs-lookup"><span data-stu-id="6ba99-261">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="6ba99-262">Ajout d’une colonne</span><span class="sxs-lookup"><span data-stu-id="6ba99-262">Add a column</span></span>

<span data-ttu-id="6ba99-263">Dans le terminal, accédez à la racine du référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="6ba99-263">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="6ba99-264">Générez une nouvelle migration de base de données pour la table `tasks` :</span><span class="sxs-lookup"><span data-stu-id="6ba99-264">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="6ba99-265">Cette commande affiche le nom du fichier de migration qui est généré.</span><span class="sxs-lookup"><span data-stu-id="6ba99-265">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="6ba99-266">Recherchez ce fichier dans _database/migrations_ et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="6ba99-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="6ba99-267">Remplacez la méthode `up` par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="6ba99-267">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="6ba99-268">Le code ci-dessus ajoute une colonne booléenne dans la table `tasks` nommée `complete`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-268">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="6ba99-269">Remplacez la méthode `down` par le code suivant pour l’action de restauration :</span><span class="sxs-lookup"><span data-stu-id="6ba99-269">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="6ba99-270">Dans le terminal, exécutez les migrations de base de données Laravel pour apporter la modification dans la base de données locale.</span><span class="sxs-lookup"><span data-stu-id="6ba99-270">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6ba99-271">Selon la [convention d’affectation de noms Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), le modèle `Task` (voir _app/Task.php_) est mappé à la table `tasks` par défaut.</span><span class="sxs-lookup"><span data-stu-id="6ba99-271">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="6ba99-272">Mise à jour de la logique d’application</span><span class="sxs-lookup"><span data-stu-id="6ba99-272">Update application logic</span></span>

<span data-ttu-id="6ba99-273">Ouvrez le fichier *routes/web.php*.</span><span class="sxs-lookup"><span data-stu-id="6ba99-273">Open the *routes/web.php* file.</span></span> <span data-ttu-id="6ba99-274">L’application définit ici ses itinéraires et sa logique métier.</span><span class="sxs-lookup"><span data-stu-id="6ba99-274">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="6ba99-275">À la fin du fichier, ajoutez un itinéraire avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="6ba99-275">At the end of the file, add a route with the following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="6ba99-276">Le code ci-dessus effectue une simple mise à jour du modèle de données en basculant la valeur de `complete`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-276">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="6ba99-277">Mise à jour de la vue</span><span class="sxs-lookup"><span data-stu-id="6ba99-277">Update the view</span></span>

<span data-ttu-id="6ba99-278">Ouvrez le fichier *resources/views/tasks.blade.php*.</span><span class="sxs-lookup"><span data-stu-id="6ba99-278">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="6ba99-279">Recherchez la balise d’ouverture `<tr>` et remplacez-la par :</span><span class="sxs-lookup"><span data-stu-id="6ba99-279">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="6ba99-280">Le code ci-dessus modifie la couleur de la ligne selon que la tâche est terminée ou non.</span><span class="sxs-lookup"><span data-stu-id="6ba99-280">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="6ba99-281">La ligne suivante contient le code suivant :</span><span class="sxs-lookup"><span data-stu-id="6ba99-281">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="6ba99-282">Remplacez la ligne entière par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="6ba99-282">Replace the entire line with the following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="6ba99-283">Le code ci-dessus ajoute le bouton Envoyer qui fait référence à l’itinéraire défini précédemment.</span><span class="sxs-lookup"><span data-stu-id="6ba99-283">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="6ba99-284">Test des modifications en local</span><span class="sxs-lookup"><span data-stu-id="6ba99-284">Test the changes locally</span></span>

<span data-ttu-id="6ba99-285">À partir du répertoire racine du référentiel Git, exécutez le serveur de développement.</span><span class="sxs-lookup"><span data-stu-id="6ba99-285">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6ba99-286">Pour voir l’évolution de l’état de la tâche, accédez à `http://localhost:8000` et activez la case à cocher.</span><span class="sxs-lookup"><span data-stu-id="6ba99-286">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![Case à cocher ajoutée à la tâche](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="6ba99-288">Pour arrêter PHP, tapez `Ctrl + C` dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="6ba99-288">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="6ba99-289">Publier les modifications dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-289">Publish changes to Azure</span></span>

<span data-ttu-id="6ba99-290">Dans le terminal, exécutez les migrations de base de données Laravel avec la chaîne de connexion de production pour apporter la modification dans la base de données Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-290">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6ba99-291">Validez toutes les modifications dans Git, puis envoyez les modifications de code à Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-291">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="6ba99-292">Une fois le `git push` terminé, accédez à l’application web Azure et essayez la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6ba99-292">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Modifications du modèle et de la base de données publiées dans Azure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="6ba99-294">Si vous avez ajouté des tâches, celles-ci sont conservées dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="6ba99-294">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="6ba99-295">Les mises à jour appliquées au schéma de données n’affectent pas les données existantes.</span><span class="sxs-lookup"><span data-stu-id="6ba99-295">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="6ba99-296">Diffuser les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="6ba99-296">Stream diagnostic logs</span></span>

<span data-ttu-id="6ba99-297">Pendant l’exécution de l’application PHP dans Azure App Service, vous pouvez acheminer les journaux de la console vers votre terminal.</span><span class="sxs-lookup"><span data-stu-id="6ba99-297">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="6ba99-298">De cette façon, vous pouvez obtenir les mêmes messages de diagnostic pour vous aider à déboguer les erreurs d’application.</span><span class="sxs-lookup"><span data-stu-id="6ba99-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="6ba99-299">Pour démarrer la diffusion de journaux, utilisez la commande [az webapp log tail](/cli/azure/webapp/log#tail).</span><span class="sxs-lookup"><span data-stu-id="6ba99-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="6ba99-300">Une fois que la diffusion a démarré, actualisez l’application web Azure dans le navigateur pour générer un trafic web.</span><span class="sxs-lookup"><span data-stu-id="6ba99-300">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="6ba99-301">Vous pouvez maintenant voir les journaux de la console acheminés vers le terminal.</span><span class="sxs-lookup"><span data-stu-id="6ba99-301">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="6ba99-302">Si vous ne voyez pas les journaux de la console, attendez 30 secondes et vérifiez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="6ba99-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="6ba99-303">Pour arrêter la diffusion de journaux à tout moment, tapez `Ctrl`+`C`.</span><span class="sxs-lookup"><span data-stu-id="6ba99-303">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="6ba99-304">Une application PHP peut utiliser la commande [error_log()](http://php.net/manual/function.error-log.php) pour envoyer le résultat vers la console.</span><span class="sxs-lookup"><span data-stu-id="6ba99-304">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="6ba99-305">L’exemple d’application utilise cette approche dans _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="6ba99-305">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="6ba99-306">[Laravel utilise Monolog](https://laravel.com/docs/5.4/errors) comme fournisseur de journalisation, de la même manière qu’une infrastructure web.</span><span class="sxs-lookup"><span data-stu-id="6ba99-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="6ba99-307">Pour savoir comment faire en sorte que Monolog envoie les messages vers la console, consultez [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out) (PHP : utilisation de Monolog pour envoyer le journal vers la console (php://out)).</span><span class="sxs-lookup"><span data-stu-id="6ba99-307">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="6ba99-308">Gérer l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-308">Manage the Azure web app</span></span>

<span data-ttu-id="6ba99-309">Accédez au [Portail Azure](https://portal.azure.com) pour gérer l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="6ba99-309">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="6ba99-310">Dans le menu de gauche, cliquez sur **App Services**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba99-310">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="6ba99-312">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="6ba99-312">You see your web app's Overview page.</span></span> <span data-ttu-id="6ba99-313">Ici, vous pouvez effectuer des tâches de gestion de base (arrêter, démarrer, redémarrer, parcourir et supprimer).</span><span class="sxs-lookup"><span data-stu-id="6ba99-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="6ba99-314">Le menu de gauche fournit des pages vous permettant de configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="6ba99-314">The left menu provides pages for configuring your app.</span></span>

![Page App Service du Portail Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6ba99-316">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ba99-316">Next steps</span></span>

<span data-ttu-id="6ba99-317">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="6ba99-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6ba99-318">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6ba99-319">Connexion d’une application PHP à MySQL</span><span class="sxs-lookup"><span data-stu-id="6ba99-319">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="6ba99-320">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-320">Deploy the app to Azure</span></span>
> * <span data-ttu-id="6ba99-321">Mise à jour du modèle de données et redéploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="6ba99-321">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="6ba99-322">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6ba99-323">Gérer l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-323">Manage the app in the Azure portal</span></span>

<span data-ttu-id="6ba99-324">Passez au didacticiel suivant pour découvrir comment mapper un nom DNS personnalisé à une application web.</span><span class="sxs-lookup"><span data-stu-id="6ba99-324">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ba99-325">Mapper un nom DNS personnalisé existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="6ba99-325">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
