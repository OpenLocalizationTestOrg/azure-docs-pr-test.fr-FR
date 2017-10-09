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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Créer une application web PHP et MySQL dans Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques. Ce didacticiel montre comment toocreate PHP application dans Azure web et le connecter tooa base de données MySQL. Une fois terminé, vous disposerez d’une application [Laravel](https://laravel.com/) s’exécutant dans Azure App Service Web Apps.

![Application PHP exécutée dans Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Création d’une base de données MySQL dans Azure
> * Se connecter à un tooMySQL d’application PHP
> * Déployer hello application tooAzure
> * Mettre à jour le modèle de données hello et redéployer l’application hello
> * Diffusion des journaux de diagnostic à partir d’Azure
> * Gérer l’application hello Bonjour portail Azure

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

* [Installez Git](https://git-scm.com/)
* [Installez PHP 5.6.4 ou version ultérieure](http://php.net/downloads.php)
* [Installez Composer](https://getcomposer.org/doc/00-intro.md)
* Activer hello suivant les besoins de Laravel les extensions PHP : OpenSSL, PDO-MySQL, Mbstring, Générateur de jetons, XML
* [Installez et démarrez MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Préparation du MySQL local

Dans cette étape, vous allez créer une base de données dans votre serveur MySQL local qui vous sera utile dans ce didacticiel.

### <a name="connect-toolocal-mysql-server"></a>Se connecter toolocal MySQL server

Dans une fenêtre de terminal, connectez-vous tooyour local MySQL server. Vous pouvez utiliser cette fenêtre de terminal de toorun toutes les commandes hello dans ce didacticiel.

```bash
mysql -u root -p
```

Si vous êtes invité à entrer un mot de passe, entrez le mot de passe hello pour hello `root` compte. Si vous avez oublié votre mot de passe du compte racine, consultez [MySQL : comment tooReset hello mot de passe racine](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Si la commande est exécutée correctement, votre serveur MySQL est en cours d’exécution. Dans le cas contraire, assurez-vous que votre serveur MySQL local est démarrée par hello suivant [les étapes de post-installation MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Créer une base de données locale

À hello `mysql` invite, créer une base de données.

```sql 
CREATE DATABASE sampledb;
```

Quittez votre connexion au serveur en tapant `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Créer une application PHP locale
Dans cette étape, vous allez créer un exemple d’application Laravel, configurer sa connexion à la base de données et l’exécuter localement. 

### <a name="clone-hello-sample"></a>Exemple hello de clone

Dans la fenêtre de terminal hello, `cd` répertoire de travail tooa.

Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`répertoire de tooyour cloné.
Installer les packages hello requis.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Configuration de la connexion MySQL

Dans la racine du référentiel hello, créez un fichier nommé *.env*. Hello copie suivant des variables dans hello *.env* fichier. Remplacez hello  _&lt;root_password >_ espace réservé avec mot de passe de l’utilisateur racine hello MySQL.

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

Pour plus d’informations sur la façon dont Laravel utilise hello _.env_ de fichiers, consultez [Configuration de l’environnement Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Exécuter les exemples hello localement

Exécutez [migrations de base de données Laravel](https://laravel.com/docs/5.4/migrations) toocreate hello tables des besoins de l’application hello. toosee les tables sont créées dans les migrations hello, recherchez Bonjour _base de données/migrations_ répertoire dans le référentiel Git de hello.

```bash
php artisan migrate
```

Générez une nouvelle clé d’application Laravel.

```bash
php artisan key:generate
```

Exécutez l’application hello.

```bash
php artisan serve
```

Accédez trop`http://localhost:8000` dans un navigateur. Ajouter quelques tâches dans la page de hello.

![PHP connecte correctement tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

toostop PHP, tapez `Ctrl + C` Bonjour Terminal Server.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Création de MySQL dans Azure

Dans cette étape, vous allez créer une base de données MySQL dans [Azure Database pour MySQL (Version préliminaire)](/azure/mysql). Ensuite, vous configurez hello PHP tooconnect toothis base de données.

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Création d’un serveur MySQL

Créer un serveur de base de données Azure pour MySQL (version préliminaire) avec hello [az mysql server créer](/cli/azure/mysql/server#create) commande.

Bonjour suivant de commande, remplacez le nom de votre serveur MySQL dans lequel vous consultez hello  _&lt;mysql_server_name >_ espace réservé (les caractères valides sont `a-z`, `0-9`, et `-`). Ce nom fait partie du nom d’hôte du serveur hello MySQL (`<mysql_server_name>.database.windows.net`), il doit toobe global unique.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Lorsque le serveur MySQL de hello est créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

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

### <a name="configure-server-firewall"></a>Configuration d’un pare-feu de serveur

Créer une règle de pare-feu pour votre client de tooallow MySQL server connexions à l’aide de hello [az mysql server-règle de pare-feu créer](/cli/azure/mysql/server/firewall-rule#create) commande.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Services de tooAzure uniquement les connexions actuellement ne limite pas la base de données Azure pour MySQL (version préliminaire). Comme les adresses IP dans Azure sont attribuées dynamiquement, il s’agit d’une meilleure tooenable toutes les adresses IP. service de Hello est en version préliminaire. Les meilleures méthodes de sécurisation de votre base de données sont planifiées.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Se connecter localement tooproduction MySQL server

Dans la fenêtre de terminal hello, connectez-vous toohello MySQL server dans Azure. Utilisez la valeur hello spécifiée précédemment pour  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Lors de l’invité à entrer un mot de passe, utilisez _tr0ngPa $$ w0rd !_, que vous avez spécifiés lors de la création de la base de données hello.

### <a name="create-a-production-database"></a>Création d’une base de données de production

À hello `mysql` invite, créer une base de données.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Création d’un utilisateur avec des autorisations

Créez un utilisateur de base de données appelé _phpappuser_ et lui donner tous les privilèges Bonjour `sampledb` base de données.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Quitter la connexion au serveur hello en tapant `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Connecter l’application tooAzure MySQL

Dans cette étape, vous vous connectez hello PHP application toohello base de données MySQL que vous avez créé dans la base de données Azure pour MySQL (version préliminaire).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Configurer la connexion de base de données hello

Dans la racine du référentiel hello, créez un _. env.production_ fichier et copiez hello suivant des variables dans celui-ci. Remplacez l’espace réservé de hello  _&lt;mysql_server_name >_.

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

Enregistrer les modifications de hello.

> [!TIP]
> toosecure vos informations de connexion MySQL, ce fichier sont déjà exclues de référentiel Git de hello (consultez _.gitignore_ dans la racine du référentiel hello). Une version ultérieure, vous découvrez comment les variables d’environnement tooconfigure dans tooyour tooconnect de Service d’applications de base de données dans la base de données Azure pour MySQL (version préliminaire). Avec les variables d’environnement, vous n’avez pas besoin hello *.env* fichier dans le Service d’applications.
>

### <a name="configure-ssl-certificate"></a>Configuration du certificat SSL

Par défaut, la base de données Azure pour MySQL applique les connexions SSL à partir des clients. tooconnect tooyour base de données MySQL dans Azure, vous devez utiliser un _.pem_ certificat SSL.

Ouvrez _config/database.php_ et ajoutez hello _sslmode_ et _options_ paramètres trop`connections.mysql`, comme indiqué dans hello suivant de code.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn comment toogenerate cela _certificate.pem_, consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> chemin d’accès Hello _/ssl/certificate.pem_ pointe tooan existant _certificate.pem_ fichier dans le référentiel Git de hello. Dans ce didacticiel, ce fichier est fourni pour des raisons pratiques. Il est préférable de ne pas valider vos certificats _.pem_ dans le contrôle de code source. 
>

### <a name="test-hello-application-locally"></a>Tester l’application hello localement

Exécuter les migrations de base de données Laravel avec _. env.production_ comme hello tables environnement fichier toocreate hello votre base de données MySQL dans la base de données Azure pour MySQL (version préliminaire). N’oubliez pas que _. env.production_ a base de données de MySQL hello connexion informations tooyour dans Azure.

```bash
php artisan migrate --env=production --force
```

_.env.production_ n’a pas encore de clé d’application valide. Générer un nouveau pour elle dans hello Terminal Server.

```bash
php artisan key:generate --env=production --force
```

Exécutez l’exemple d’application hello avec _. env.production_ en tant que fichier d’environnement hello.

```bash
php artisan serve --env=production
```

Accédez trop`http://localhost:8000`. Si le chargement de la page hello sans erreurs hello application PHP se connecte toohello de la base de données MySQL dans Azure.

Ajouter quelques tâches dans la page de hello.

![PHP connecte correctement tooAzure de base de données de MySQL (version préliminaire)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

toostop PHP, tapez `Ctrl + C` Bonjour Terminal Server.

### <a name="commit-your-changes"></a>Validation de vos modifications

Exécutez hello suivant toocommit de commandes Git vos modifications :

```bash
git add .
git commit -m "database.php updates"
```

Votre application est toobe prêt déployée.

## <a name="deploy-tooazure"></a>Déployer tooAzure

Dans cette étape, vous déployez hello PHP de connexion MySQL application tooAzure du Service d’applications.

### <a name="create-an-app-service-plan"></a>Créer un plan App Service

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Créer une application web

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Définir la version PHP hello

Version PHP hello Set qui hello application requiert à l’aide de hello [az webapp configuration défini](/cli/azure/webapp/config#set) commande.

Hello commande suivante définit hello PHP version too_7.0_.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Configuration des paramètres de la base de données

Comme indiqué précédemment, vous pouvez vous connecter à Azure MySQL tooyour de base de données à l’aide de variables d’environnement dans le Service d’applications.

Dans le Service d’application, vous définissez les variables d’environnement _paramètres de l’application_ à l’aide de hello [az webapp configuration appsettings défini](/cli/azure/webapp/config/appsettings#set) commande.

Hello commande suivante configure les paramètres de l’application hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, et `DB_PASSWORD`. Remplacez les espaces réservés de hello  _&lt;appname >_ et  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Vous pouvez utiliser hello PHP [getenv](http://www.php.net/manual/function.getenv.php) méthode tooaccess hello paramètres. Hello Laravel code utilise un [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper sur hello PHP `getenv`. Par exemple, les configuration MySQL hello dans _config/database.php_ ressemble à hello suivant de code :

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

### <a name="configure-laravel-environment-variables"></a>Configuration des variables d’environnement Laravel

Laravel a besoin d’une clé d’application dans App Service. Vous pouvez la configurer avec les paramètres d’application.

Utilisez `php artisan` toogenerate une nouvelle clé d’application sans l’enregistrer too_.env_.

```bash
php artisan key:generate --show
```

Définir une clé de l’application hello Bonjour du Service d’applications, application web à l’aide de hello [az webapp configuration appsettings défini](/cli/azure/webapp/config/appsettings#set) commande. Remplacez les espaces réservés de hello  _&lt;appname >_ et  _&lt;outputofphpartisankey : générer >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`Indique les informations débogage Laravel tooreturn hello déployé l’application web rencontre des erreurs. Lorsque vous exécutez une application de production, définissez-le trop`false`, qui est plus sécurisé.

### <a name="set-hello-virtual-application-path"></a>Le chemin d’accès de jeu hello application virtuelle

Définissez hello chemin d’accès virtuel pour l’application web de hello. Cette étape est requise car hello [cycle de vie des applications Laravel](https://laravel.com/docs/5.4/lifecycle) commence dans hello _public_ répertoire au lieu du répertoire racine de l’application hello. Autres infrastructures PHP dont du cycle de vie Démarrer dans le répertoire racine de hello peuvent fonctionner sans configuration manuelle de hello chemin d’accès virtuel.

Ensemble hello chemin d’accès virtuel à l’aide de hello [mise à jour de la ressource az](/cli/azure/resource#update) commande. Remplacez hello  _&lt;appname >_ espace réservé.

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

Par défaut, les points de Service d’applications Azure hello racine chemin d’accès virtuel (_/_) répertoire toohello Hello déployé les fichiers d’application (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Configuration d’un utilisateur de déploiement

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Configurer le déploiement Git local

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>TooAzure par émission de données à partir de Git

Ajouter un référentiel Git Azure tooyour à distance.

```bash
git remote add azure <paste_copied_url_here>
```

Push application PHP de toohello toodeploy distant Azure hello. Vous êtes invité au mot de passe hello fourni précédemment dans le cadre de la création de l’utilisateur du déploiement hello hello.

```bash
git push azure master
```

Au cours du déploiement, Azure App Service communique sa progression avec Git.

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
> Vous pouvez remarquer que le processus de déploiement hello installe [Composer](https://getcomposer.org/) packages à la fin de hello. Service de l’application ne s’exécute pas ces automatisations durant le déploiement de la valeur par défaut, donc ce dépôt d’exemples possède trois autres fichiers dans son tooenable du répertoire racine qu’il :
>
> - `.deployment`-Ce fichier indique du Service d’applications toorun `bash deploy.sh` en tant que script de déploiement personnalisé hello.
> - `deploy.sh`-hello du script de déploiement personnalisé. Si vous passez en revue le fichier de hello, vous verrez qu’il s’exécute `php composer.phar install` après `npm install`.
> - `composer.phar`-Gestionnaire de package de Composer hello.
>
> Vous pouvez utiliser cette approche tooadd n’importe quel ordinateur étape tooyour déploiement Git tooApp Service. Pour plus d'informations, consultez le [script de déploiement personnalisé](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).
>

### <a name="browse-toohello-azure-web-app"></a>Parcourir toohello Azure web app

Parcourir trop`http://<app_name>.azurewebsites.net` et ajouter quelques tâches toohello.

![Application PHP exécutée dans Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Félicitations, vous exécutez une application PHP orientée données dans Azure App Service.

## <a name="update-model-locally-and-redeploy"></a>Mettre à jour et redéployer un modèle localement

Dans cette étape, vous apportez une modification simple de toohello `task` données de modèle, hello webapp et puis publiez tooAzure de mise à jour hello.

Pour le scénario de tâches hello, vous modifiez application hello afin que vous pouvez marquer une tâche comme étant terminée.

### <a name="add-a-column"></a>Ajout d’une colonne

Bonjour terminal, accédez à racine toohello du référentiel Git de hello.

Générer une nouvelle migration de base de données pour hello `tasks` table :

```bash
php artisan make:migration add_complete_column --table=tasks
```

Cette commande indique hello de nom du fichier de migration hello qui est généré. Recherchez ce fichier dans _database/migrations_ et ouvrez-le.

Remplacez hello `up` méthode avec hello suivant de code :

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Hello code précédent ajoute une colonne booléenne Bonjour `tasks` table appelée `complete`.

Remplacez hello `down` méthode avec hello suivant le code d’action de restauration hello :

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

Bonjour Terminal Server, exécutez les Laravel de base de données migrations toomake hello modifications dans la base de données locale hello.

```bash
php artisan migrate
```

En fonction de hello [convention d’affectation de noms de Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modèle de hello `Task` (consultez _app/Task.php_) mappe toohello `tasks` table par défaut.

### <a name="update-application-logic"></a>Mise à jour de la logique d’application

Ouvrez hello *routes/web.php* fichier. application Hello définit ses itinéraires et la logique d’entreprise.

En bas de hello du fichier de hello, ajoutez un itinéraire avec hello suivant de code :

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

Hello code précédent crée un modèle de données de mise à jour simple toohello en basculant la valeur hello `complete`.

### <a name="update-hello-view"></a>Vue hello de mise à jour

Ouvrez hello *resources/views/tasks.blade.php* fichier. Recherche hello `<tr>` balise d’ouverture et remplacez-la par :

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Hello précédant le code change de couleur ligne hello selon que la tâche hello est terminée.

Dans la ligne suivante de hello, vous avez hello suivant de code :

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Remplacez toute ligne de hello hello suivant de code :

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

Hello code précédent ajoute bouton Envoyer hello qui fait référence à itinéraire hello que vous avez défini précédemment.

### <a name="test-hello-changes-locally"></a>Tester des modifications hello localement

À partir du répertoire racine de hello du référentiel Git de hello, exécutez le serveur de développement hello.

```bash
php artisan serve
```

toosee hello changement d’état de la tâche, accédez trop`http://localhost:8000` puis hello select case.

![Case à cocher ajouté tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

toostop PHP, tapez `Ctrl + C` Bonjour Terminal Server.

### <a name="publish-changes-tooazure"></a>Publier les modifications tooAzure

Bonjour Terminal Server, exécuter les migrations de base de données Laravel avec hello production chaîne connexion toomake hello modification Bonjour Azure de base de données.

```bash
php artisan migrate --env=production --force
```

Valider toutes les modifications de hello dans Git et puis envoyez tooAzure de modifications de code hello.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Une fois hello `git push` terminée, accédez toohello Azure web app et test hello nouvelles fonctionnalités.

![Les modifications de modèle et de la base de données publiées tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Si vous avez ajouté toutes les tâches, ils sont conservés dans la base de données hello. Schéma de données mises à jour toohello toucher les données existantes.

## <a name="stream-diagnostic-logs"></a>Diffuser les journaux de diagnostic

Pendant l’exécution de hello application PHP dans Azure App Service, vous pouvez obtenir hello console journaux dirigée tooyour Terminal Server. De cette façon, vous pouvez obtenir hello des messages de diagnostic mêmes toohelp vous déboguez des erreurs d’application.

journal toostart de diffusion en continu, utilisez hello [la fin du journal de az webapp](/cli/azure/webapp/log#tail) commande.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Une fois que le journal de diffusion en continu a démarré, actualiser application web Azure hello hello navigateur tooget certains types de trafic web. Vous pouvez maintenant voir dirigée toohello Terminal Server des journaux de console. Si vous ne voyez pas les journaux de la console, attendez 30 secondes et vérifiez à nouveau.

journal toostop de diffusion en continu à tout moment, type `Ctrl` + `C`.

> [!TIP]
> Une application PHP peut utiliser standard de hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console. exemple d’application Hello utilise cette approche dans _app/Http/routes.php_.
>
> Comme une infrastructure web, [Laravel utilise Monolog](https://laravel.com/docs/5.4/errors) en tant que fournisseur de journalisation hello. toosee tooget Monolog toooutput des messages toohello console, consultez [PHP : comment toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Gérer l’application web Azure de hello

Accédez toohello [portail Azure](https://portal.azure.com) toomanage vous avez créé l’application web hello.

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-php-mysql/access-portal.png)

Vous voyez apparaître la page Vue d’ensemble de votre application web. Ici, vous pouvez effectuer des tâches de gestion de base (arrêter, démarrer, redémarrer, parcourir et supprimer).

menu de gauche Hello fournit des pages de configuration de votre application.

![Page App Service du Portail Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Création d’une base de données MySQL dans Azure
> * Se connecter à un tooMySQL d’application PHP
> * Déployer hello application tooAzure
> * Mettre à jour le modèle de données hello et redéployer l’application hello
> * Diffusion des journaux de diagnostic à partir d’Azure
> * Gérer l’application hello Bonjour portail Azure

Avancer toolearn de didacticiel suivant toohello tooa l’application web de noms toomap DNS personnalisé.

> [!div class="nextstepaction"]
> [Mapper une tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md)
