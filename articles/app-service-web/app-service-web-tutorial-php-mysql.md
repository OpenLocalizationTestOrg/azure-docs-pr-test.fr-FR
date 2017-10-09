---
title: aaaBuild une application web PHP et MySQL dans Azure | Documents Microsoft
description: "Découvrez comment tooget une application PHP dans Azure, avec tooa de connexion MySQL de base de données dans Azure."
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
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="6d1f4-103">Créer une application web PHP et MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="6d1f4-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6d1f4-105">Ce didacticiel montre comment toocreate PHP application dans Azure web et le connecter tooa base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="6d1f4-106">Une fois terminé, vous disposerez d’une application [Laravel](https://laravel.com/) s’exécutant dans Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Application PHP exécutée dans Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="6d1f4-108">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d1f4-109">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6d1f4-110">Se connecter à un tooMySQL d’application PHP</span><span class="sxs-lookup"><span data-stu-id="6d1f4-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="6d1f4-111">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="6d1f4-112">Mettre à jour le modèle de données hello et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="6d1f4-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="6d1f4-113">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6d1f4-114">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d1f4-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6d1f4-115">Prerequisites</span></span>

<span data-ttu-id="6d1f4-116">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="6d1f4-117">Installez Git</span><span class="sxs-lookup"><span data-stu-id="6d1f4-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="6d1f4-118">Installez PHP 5.6.4 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="6d1f4-119">Installez Composer</span><span class="sxs-lookup"><span data-stu-id="6d1f4-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="6d1f4-120">Activer hello suivant les besoins de Laravel les extensions PHP : OpenSSL, PDO-MySQL, Mbstring, Générateur de jetons, XML</span><span class="sxs-lookup"><span data-stu-id="6d1f4-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="6d1f4-121">Installez et démarrez MySQL</span><span class="sxs-lookup"><span data-stu-id="6d1f4-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="6d1f4-122">Préparation du MySQL local</span><span class="sxs-lookup"><span data-stu-id="6d1f4-122">Prepare local MySQL</span></span>

<span data-ttu-id="6d1f4-123">Dans cette étape, vous allez créer une base de données dans votre serveur MySQL local qui vous sera utile dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="6d1f4-124">Se connecter toolocal MySQL server</span><span class="sxs-lookup"><span data-stu-id="6d1f4-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="6d1f4-125">Dans une fenêtre de terminal, connectez-vous tooyour local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="6d1f4-126">Vous pouvez utiliser cette fenêtre de terminal de toorun toutes les commandes hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="6d1f4-127">Si vous êtes invité à entrer un mot de passe, entrez le mot de passe hello pour hello `root` compte.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="6d1f4-128">Si vous avez oublié votre mot de passe du compte racine, consultez [MySQL : comment tooReset hello mot de passe racine](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="6d1f4-129">Si la commande est exécutée correctement, votre serveur MySQL est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="6d1f4-130">Dans le cas contraire, assurez-vous que votre serveur MySQL local est démarrée par hello suivant [les étapes de post-installation MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="6d1f4-131">Créer une base de données locale</span><span class="sxs-lookup"><span data-stu-id="6d1f4-131">Create a database locally</span></span>

<span data-ttu-id="6d1f4-132">À hello `mysql` invite, créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="6d1f4-133">Quittez votre connexion au serveur en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="6d1f4-134">Créer une application PHP locale</span><span class="sxs-lookup"><span data-stu-id="6d1f4-134">Create a PHP app locally</span></span>
<span data-ttu-id="6d1f4-135">Dans cette étape, vous allez créer un exemple d’application Laravel, configurer sa connexion à la base de données et l’exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="6d1f4-136">Exemple hello de clone</span><span class="sxs-lookup"><span data-stu-id="6d1f4-136">Clone hello sample</span></span>

<span data-ttu-id="6d1f4-137">Dans la fenêtre de terminal hello, `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="6d1f4-138">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="6d1f4-139">`cd`répertoire de tooyour cloné.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="6d1f4-140">Installer les packages hello requis.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="6d1f4-141">Configuration de la connexion MySQL</span><span class="sxs-lookup"><span data-stu-id="6d1f4-141">Configure MySQL connection</span></span>

<span data-ttu-id="6d1f4-142">Dans la racine du référentiel hello, créez un fichier nommé *.env*.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="6d1f4-143">Hello copie suivant des variables dans hello *.env* fichier.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="6d1f4-144">Remplacez hello  _&lt;root_password >_ espace réservé avec mot de passe de l’utilisateur racine hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

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

<span data-ttu-id="6d1f4-145">Pour plus d’informations sur la façon dont Laravel utilise hello _.env_ de fichiers, consultez [Configuration de l’environnement Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="6d1f4-146">Exécuter les exemples hello localement</span><span class="sxs-lookup"><span data-stu-id="6d1f4-146">Run hello sample locally</span></span>

<span data-ttu-id="6d1f4-147">Exécutez [migrations de base de données Laravel](https://laravel.com/docs/5.4/migrations) toocreate hello tables des besoins de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="6d1f4-148">toosee les tables sont créées dans les migrations hello, recherchez Bonjour _base de données/migrations_ répertoire dans le référentiel Git de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6d1f4-149">Générez une nouvelle clé d’application Laravel.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="6d1f4-150">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6d1f4-151">Accédez trop`http://localhost:8000` dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="6d1f4-152">Ajouter quelques tâches dans la page de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-152">Add a few tasks in hello page.</span></span>

![PHP connecte correctement tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="6d1f4-154">toostop PHP, tapez `Ctrl + C` Bonjour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="6d1f4-155">Création de MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-155">Create MySQL in Azure</span></span>

<span data-ttu-id="6d1f4-156">Dans cette étape, vous allez créer une base de données MySQL dans [Azure Database pour MySQL (Version préliminaire)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="6d1f4-157">Ensuite, vous configurez hello PHP tooconnect toothis base de données.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6d1f4-158">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6d1f4-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="6d1f4-159">Création d’un serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="6d1f4-159">Create a MySQL server</span></span>

<span data-ttu-id="6d1f4-160">Créer un serveur de base de données Azure pour MySQL (version préliminaire) avec hello [az mysql server créer](/cli/azure/mysql/server#create) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="6d1f4-161">Bonjour suivant de commande, remplacez le nom de votre serveur MySQL dans lequel vous consultez hello  _&lt;mysql_server_name >_ espace réservé (les caractères valides sont `a-z`, `0-9`, et `-`).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="6d1f4-162">Ce nom fait partie du nom d’hôte du serveur hello MySQL (`<mysql_server_name>.database.windows.net`), il doit toobe global unique.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="6d1f4-163">Lorsque le serveur MySQL de hello est créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="6d1f4-164">Configuration d’un pare-feu de serveur</span><span class="sxs-lookup"><span data-stu-id="6d1f4-164">Configure server firewall</span></span>

<span data-ttu-id="6d1f4-165">Créer une règle de pare-feu pour votre client de tooallow MySQL server connexions à l’aide de hello [az mysql server-règle de pare-feu créer](/cli/azure/mysql/server/firewall-rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="6d1f4-166">Services de tooAzure uniquement les connexions actuellement ne limite pas la base de données Azure pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="6d1f4-167">Comme les adresses IP dans Azure sont attribuées dynamiquement, il s’agit d’une meilleure tooenable toutes les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="6d1f4-168">service de Hello est en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-168">hello service is in preview.</span></span> <span data-ttu-id="6d1f4-169">Les meilleures méthodes de sécurisation de votre base de données sont planifiées.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="6d1f4-170">Se connecter localement tooproduction MySQL server</span><span class="sxs-lookup"><span data-stu-id="6d1f4-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="6d1f4-171">Dans la fenêtre de terminal hello, connectez-vous toohello MySQL server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="6d1f4-172">Utilisez la valeur hello spécifiée précédemment pour  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="6d1f4-173">Lors de l’invité à entrer un mot de passe, utilisez _tr0ngPa $$ w0rd !_, que vous avez spécifiés lors de la création de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="6d1f4-174">Création d’une base de données de production</span><span class="sxs-lookup"><span data-stu-id="6d1f4-174">Create a production database</span></span>

<span data-ttu-id="6d1f4-175">À hello `mysql` invite, créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="6d1f4-176">Création d’un utilisateur avec des autorisations</span><span class="sxs-lookup"><span data-stu-id="6d1f4-176">Create a user with permissions</span></span>

<span data-ttu-id="6d1f4-177">Créez un utilisateur de base de données appelé _phpappuser_ et lui donner tous les privilèges Bonjour `sampledb` base de données.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="6d1f4-178">Quitter la connexion au serveur hello en tapant `quit`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="6d1f4-179">Connecter l’application tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="6d1f4-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="6d1f4-180">Dans cette étape, vous vous connectez hello PHP application toohello base de données MySQL que vous avez créé dans la base de données Azure pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="6d1f4-181">Configurer la connexion de base de données hello</span><span class="sxs-lookup"><span data-stu-id="6d1f4-181">Configure hello database connection</span></span>

<span data-ttu-id="6d1f4-182">Dans la racine du référentiel hello, créez un _. env.production_ fichier et copiez hello suivant des variables dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="6d1f4-183">Remplacez l’espace réservé de hello  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="6d1f4-184">Enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="6d1f4-185">toosecure vos informations de connexion MySQL, ce fichier sont déjà exclues de référentiel Git de hello (consultez _.gitignore_ dans la racine du référentiel hello).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="6d1f4-186">Une version ultérieure, vous découvrez comment les variables d’environnement tooconfigure dans tooyour tooconnect de Service d’applications de base de données dans la base de données Azure pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="6d1f4-187">Avec les variables d’environnement, vous n’avez pas besoin hello *.env* fichier dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="6d1f4-188">Configuration du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="6d1f4-188">Configure SSL certificate</span></span>

<span data-ttu-id="6d1f4-189">Par défaut, la base de données Azure pour MySQL applique les connexions SSL à partir des clients.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="6d1f4-190">tooconnect tooyour base de données MySQL dans Azure, vous devez utiliser un _.pem_ certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="6d1f4-191">Ouvrez _config/database.php_ et ajoutez hello _sslmode_ et _options_ paramètres trop`connections.mysql`, comme indiqué dans hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="6d1f4-192">toolearn comment toogenerate cela _certificate.pem_, consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="6d1f4-193">chemin d’accès Hello _/ssl/certificate.pem_ pointe tooan existant _certificate.pem_ fichier dans le référentiel Git de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="6d1f4-194">Dans ce didacticiel, ce fichier est fourni pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="6d1f4-195">Il est préférable de ne pas valider vos certificats _.pem_ dans le contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="6d1f4-196">Tester l’application hello localement</span><span class="sxs-lookup"><span data-stu-id="6d1f4-196">Test hello application locally</span></span>

<span data-ttu-id="6d1f4-197">Exécuter les migrations de base de données Laravel avec _. env.production_ comme hello tables environnement fichier toocreate hello votre base de données MySQL dans la base de données Azure pour MySQL (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="6d1f4-198">N’oubliez pas que _. env.production_ a base de données de MySQL hello connexion informations tooyour dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6d1f4-199">_.env.production_ n’a pas encore de clé d’application valide.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="6d1f4-200">Générer un nouveau pour elle dans hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="6d1f4-201">Exécutez l’exemple d’application hello avec _. env.production_ en tant que fichier d’environnement hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="6d1f4-202">Accédez trop`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="6d1f4-203">Si le chargement de la page hello sans erreurs hello application PHP se connecte toohello de la base de données MySQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="6d1f4-204">Ajouter quelques tâches dans la page de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-204">Add a few tasks in hello page.</span></span>

![PHP connecte correctement tooAzure de base de données de MySQL (version préliminaire)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="6d1f4-206">toostop PHP, tapez `Ctrl + C` Bonjour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="6d1f4-207">Validation de vos modifications</span><span class="sxs-lookup"><span data-stu-id="6d1f4-207">Commit your changes</span></span>

<span data-ttu-id="6d1f4-208">Exécutez hello suivant toocommit de commandes Git vos modifications :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="6d1f4-209">Votre application est toobe prêt déployée.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="6d1f4-210">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-210">Deploy tooAzure</span></span>

<span data-ttu-id="6d1f4-211">Dans cette étape, vous déployez hello PHP de connexion MySQL application tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6d1f4-212">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="6d1f4-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="6d1f4-213">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="6d1f4-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="6d1f4-214">Définir la version PHP hello</span><span class="sxs-lookup"><span data-stu-id="6d1f4-214">Set hello PHP version</span></span>

<span data-ttu-id="6d1f4-215">Version PHP hello Set qui hello application requiert à l’aide de hello [az webapp configuration défini](/cli/azure/webapp/config#set) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="6d1f4-216">Hello commande suivante définit hello PHP version too_7.0_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="6d1f4-217">Configuration des paramètres de la base de données</span><span class="sxs-lookup"><span data-stu-id="6d1f4-217">Configure database settings</span></span>

<span data-ttu-id="6d1f4-218">Comme indiqué précédemment, vous pouvez vous connecter à Azure MySQL tooyour de base de données à l’aide de variables d’environnement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="6d1f4-219">Dans le Service d’application, vous définissez les variables d’environnement _paramètres de l’application_ à l’aide de hello [az webapp configuration appsettings défini](/cli/azure/webapp/config/appsettings#set) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="6d1f4-220">Hello commande suivante configure les paramètres de l’application hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, et `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="6d1f4-221">Remplacez les espaces réservés de hello  _&lt;appname >_ et  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="6d1f4-222">Vous pouvez utiliser hello PHP [getenv](http://www.php.net/manual/function.getenv.php) méthode tooaccess hello paramètres.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="6d1f4-223">Hello Laravel code utilise un [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper sur hello PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="6d1f4-224">Par exemple, les configuration MySQL hello dans _config/database.php_ ressemble à hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="6d1f4-225">Configuration des variables d’environnement Laravel</span><span class="sxs-lookup"><span data-stu-id="6d1f4-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="6d1f4-226">Laravel a besoin d’une clé d’application dans App Service.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="6d1f4-227">Vous pouvez la configurer avec les paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-227">You can configure it with app settings.</span></span>

<span data-ttu-id="6d1f4-228">Utilisez `php artisan` toogenerate une nouvelle clé d’application sans l’enregistrer too_.env_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="6d1f4-229">Définir une clé de l’application hello Bonjour du Service d’applications, application web à l’aide de hello [az webapp configuration appsettings défini](/cli/azure/webapp/config/appsettings#set) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="6d1f4-230">Remplacez les espaces réservés de hello  _&lt;appname >_ et  _&lt;outputofphpartisankey : générer >_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="6d1f4-231">`APP_DEBUG="true"`Indique les informations débogage Laravel tooreturn hello déployé l’application web rencontre des erreurs.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="6d1f4-232">Lorsque vous exécutez une application de production, définissez-le trop`false`, qui est plus sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="6d1f4-233">Le chemin d’accès de jeu hello application virtuelle</span><span class="sxs-lookup"><span data-stu-id="6d1f4-233">Set hello virtual application path</span></span>

<span data-ttu-id="6d1f4-234">Définissez hello chemin d’accès virtuel pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="6d1f4-235">Cette étape est requise car hello [cycle de vie des applications Laravel](https://laravel.com/docs/5.4/lifecycle) commence dans hello _public_ répertoire au lieu du répertoire racine de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="6d1f4-236">Autres infrastructures PHP dont du cycle de vie Démarrer dans le répertoire racine de hello peuvent fonctionner sans configuration manuelle de hello chemin d’accès virtuel.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="6d1f4-237">Ensemble hello chemin d’accès virtuel à l’aide de hello [mise à jour de la ressource az](/cli/azure/resource#update) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="6d1f4-238">Remplacez hello  _&lt;appname >_ espace réservé.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-238">Replace hello _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="6d1f4-239">Par défaut, les points de Service d’applications Azure hello racine chemin d’accès virtuel (_/_) répertoire toohello Hello déployé les fichiers d’application (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="6d1f4-240">Configuration d’un utilisateur de déploiement</span><span class="sxs-lookup"><span data-stu-id="6d1f4-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="6d1f4-241">Configurer le déploiement Git local</span><span class="sxs-lookup"><span data-stu-id="6d1f4-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="6d1f4-242">TooAzure par émission de données à partir de Git</span><span class="sxs-lookup"><span data-stu-id="6d1f4-242">Push tooAzure from Git</span></span>

<span data-ttu-id="6d1f4-243">Ajouter un référentiel Git Azure tooyour à distance.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="6d1f4-244">Push application PHP de toohello toodeploy distant Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="6d1f4-245">Vous êtes invité au mot de passe hello fourni précédemment dans le cadre de la création de l’utilisateur du déploiement hello hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="6d1f4-246">Au cours du déploiement, Azure App Service communique sa progression avec Git.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
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
> <span data-ttu-id="6d1f4-247">Vous pouvez remarquer que le processus de déploiement hello installe [Composer](https://getcomposer.org/) packages à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="6d1f4-248">Service de l’application ne s’exécute pas ces automatisations durant le déploiement de la valeur par défaut, donc ce dépôt d’exemples possède trois autres fichiers dans son tooenable du répertoire racine qu’il :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="6d1f4-249">`.deployment`-Ce fichier indique du Service d’applications toorun `bash deploy.sh` en tant que script de déploiement personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="6d1f4-250">`deploy.sh`-hello du script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="6d1f4-251">Si vous passez en revue le fichier de hello, vous verrez qu’il s’exécute `php composer.phar install` après `npm install`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="6d1f4-252">`composer.phar`-Gestionnaire de package de Composer hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="6d1f4-253">Vous pouvez utiliser cette approche tooadd n’importe quel ordinateur étape tooyour déploiement Git tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="6d1f4-254">Pour plus d'informations, consultez le [script de déploiement personnalisé](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="6d1f4-255">Parcourir toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="6d1f4-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="6d1f4-256">Parcourir trop`http://<app_name>.azurewebsites.net` et ajouter quelques tâches toohello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Application PHP exécutée dans Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="6d1f4-258">Félicitations, vous exécutez une application PHP orientée données dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="6d1f4-259">Mettre à jour et redéployer un modèle localement</span><span class="sxs-lookup"><span data-stu-id="6d1f4-259">Update model locally and redeploy</span></span>

<span data-ttu-id="6d1f4-260">Dans cette étape, vous apportez une modification simple de toohello `task` données de modèle, hello webapp et puis publiez tooAzure de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="6d1f4-261">Pour le scénario de tâches hello, vous modifiez application hello afin que vous pouvez marquer une tâche comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="6d1f4-262">Ajout d’une colonne</span><span class="sxs-lookup"><span data-stu-id="6d1f4-262">Add a column</span></span>

<span data-ttu-id="6d1f4-263">Bonjour terminal, accédez à racine toohello du référentiel Git de hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="6d1f4-264">Générer une nouvelle migration de base de données pour hello `tasks` table :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="6d1f4-265">Cette commande indique hello de nom du fichier de migration hello qui est généré.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="6d1f4-266">Recherchez ce fichier dans _database/migrations_ et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="6d1f4-267">Remplacez hello `up` méthode avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="6d1f4-268">Hello code précédent ajoute une colonne booléenne Bonjour `tasks` table appelée `complete`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="6d1f4-269">Remplacez hello `down` méthode avec hello suivant le code d’action de restauration hello :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="6d1f4-270">Bonjour Terminal Server, exécutez les Laravel de base de données migrations toomake hello modifications dans la base de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6d1f4-271">En fonction de hello [convention d’affectation de noms de Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modèle de hello `Task` (consultez _app/Task.php_) mappe toohello `tasks` table par défaut.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="6d1f4-272">Mise à jour de la logique d’application</span><span class="sxs-lookup"><span data-stu-id="6d1f4-272">Update application logic</span></span>

<span data-ttu-id="6d1f4-273">Ouvrez hello *routes/web.php* fichier.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="6d1f4-274">application Hello définit ses itinéraires et la logique d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="6d1f4-275">En bas de hello du fichier de hello, ajoutez un itinéraire avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-275">At hello end of hello file, add a route with hello following code:</span></span>

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

<span data-ttu-id="6d1f4-276">Hello code précédent crée un modèle de données de mise à jour simple toohello en basculant la valeur hello `complete`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="6d1f4-277">Vue hello de mise à jour</span><span class="sxs-lookup"><span data-stu-id="6d1f4-277">Update hello view</span></span>

<span data-ttu-id="6d1f4-278">Ouvrez hello *resources/views/tasks.blade.php* fichier.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="6d1f4-279">Recherche hello `<tr>` balise d’ouverture et remplacez-la par :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="6d1f4-280">Hello précédant le code change de couleur ligne hello selon que la tâche hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="6d1f4-281">Dans la ligne suivante de hello, vous avez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="6d1f4-282">Remplacez toute ligne de hello hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-282">Replace hello entire line with hello following code:</span></span>

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

<span data-ttu-id="6d1f4-283">Hello code précédent ajoute bouton Envoyer hello qui fait référence à itinéraire hello que vous avez défini précédemment.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="6d1f4-284">Tester des modifications hello localement</span><span class="sxs-lookup"><span data-stu-id="6d1f4-284">Test hello changes locally</span></span>

<span data-ttu-id="6d1f4-285">À partir du répertoire racine de hello du référentiel Git de hello, exécutez le serveur de développement hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6d1f4-286">toosee hello changement d’état de la tâche, accédez trop`http://localhost:8000` puis hello select case.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Case à cocher ajouté tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="6d1f4-288">toostop PHP, tapez `Ctrl + C` Bonjour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="6d1f4-289">Publier les modifications tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-289">Publish changes tooAzure</span></span>

<span data-ttu-id="6d1f4-290">Bonjour Terminal Server, exécuter les migrations de base de données Laravel avec hello production chaîne connexion toomake hello modification Bonjour Azure de base de données.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6d1f4-291">Valider toutes les modifications de hello dans Git et puis envoyez tooAzure de modifications de code hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="6d1f4-292">Une fois hello `git push` terminée, accédez toohello Azure web app et test hello nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![Les modifications de modèle et de la base de données publiées tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="6d1f4-294">Si vous avez ajouté toutes les tâches, ils sont conservés dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="6d1f4-295">Schéma de données mises à jour toohello toucher les données existantes.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="6d1f4-296">Diffuser les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="6d1f4-296">Stream diagnostic logs</span></span>

<span data-ttu-id="6d1f4-297">Pendant l’exécution de hello application PHP dans Azure App Service, vous pouvez obtenir hello console journaux dirigée tooyour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="6d1f4-298">De cette façon, vous pouvez obtenir hello des messages de diagnostic mêmes toohelp vous déboguez des erreurs d’application.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="6d1f4-299">journal toostart de diffusion en continu, utilisez hello [la fin du journal de az webapp](/cli/azure/webapp/log#tail) commande.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="6d1f4-300">Une fois que le journal de diffusion en continu a démarré, actualiser application web Azure hello hello navigateur tooget certains types de trafic web.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="6d1f4-301">Vous pouvez maintenant voir dirigée toohello Terminal Server des journaux de console.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="6d1f4-302">Si vous ne voyez pas les journaux de la console, attendez 30 secondes et vérifiez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="6d1f4-303">journal toostop de diffusion en continu à tout moment, type `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="6d1f4-304">Une application PHP peut utiliser standard de hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="6d1f4-305">exemple d’application Hello utilise cette approche dans _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="6d1f4-306">Comme une infrastructure web, [Laravel utilise Monolog](https://laravel.com/docs/5.4/errors) en tant que fournisseur de journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="6d1f4-307">toosee tooget Monolog toooutput des messages toohello console, consultez [PHP : comment toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="6d1f4-308">Gérer l’application web Azure de hello</span><span class="sxs-lookup"><span data-stu-id="6d1f4-308">Manage hello Azure web app</span></span>

<span data-ttu-id="6d1f4-309">Accédez toohello [portail Azure](https://portal.azure.com) toomanage vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="6d1f4-310">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="6d1f4-312">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-312">You see your web app's Overview page.</span></span> <span data-ttu-id="6d1f4-313">Ici, vous pouvez effectuer des tâches de gestion de base (arrêter, démarrer, redémarrer, parcourir et supprimer).</span><span class="sxs-lookup"><span data-stu-id="6d1f4-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="6d1f4-314">menu de gauche Hello fournit des pages de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-314">hello left menu provides pages for configuring your app.</span></span>

![Page App Service du Portail Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6d1f4-316">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d1f4-316">Next steps</span></span>

<span data-ttu-id="6d1f4-317">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="6d1f4-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d1f4-318">Création d’une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6d1f4-319">Se connecter à un tooMySQL d’application PHP</span><span class="sxs-lookup"><span data-stu-id="6d1f4-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="6d1f4-320">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="6d1f4-321">Mettre à jour le modèle de données hello et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="6d1f4-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="6d1f4-322">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6d1f4-323">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="6d1f4-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="6d1f4-324">Avancer toolearn de didacticiel suivant toohello tooa l’application web de noms toomap DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="6d1f4-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d1f4-325">Mapper une tooAzure de nom DNS personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="6d1f4-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
