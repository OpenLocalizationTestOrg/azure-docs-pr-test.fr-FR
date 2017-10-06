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
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Créer une application web Docker Python et PostgreSQL dans Azure

Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement. Ce didacticiel montre comment une base Python de Docker de toocreate web application dans Azure. Vous vous connecterez à cette base de données PostgreSQL tooa application. Ceci fait, vous disposerez d’une application Python Flask s’exécutant dans un conteneur Docker sur [Azure App Service Web Apps](app-service-web-overview.md).

![Application Docker Python Flask dans Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

Vous pouvez suivre les étapes de hello ci-dessous sur macOS. Les instructions de Linux et Windows sont même hello dans la plupart des cas, mais les différences hello ne sont pas détaillés dans ce didacticiel.
 
## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

1. [Installez Git](https://git-scm.com/)
1. [Installez Python](https://www.python.org/downloads/)
1. [Téléchargez et exécutez PostgreSQL](https://www.postgresql.org/download/)
1. [Installez Docker Community Edition](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Test de l’installation PostgreSQL locale et création d’une base de données

Ouvrez la fenêtre de terminal hello et exécutez `psql postgres` tooconnect tooyour local PostgreSQL serveur.

```bash
psql postgres
```

Si la connexion est établie, cela signifie que votre base de données PostgreSQL est en cours d’exécution. Dans le cas contraire, assurez-vous que votre base de données PostgresQL locale est démarré en suivant les étapes de hello à [téléchargements - PostgreSQL Core Distribution](https://www.postgresql.org/download/).

Créez une base de données appelée *eventregistration* et configurez un utilisateur de base de données nommé *manager* avec le mot de passe *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Type *\q* client de PostgreSQL tooexit hello. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Création d’une application Python Flask locale

Dans cette étape, vous définir un projet local Python ballon hello.

### <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Fenêtre de terminal ouverte hello et `CD` répertoire de travail tooa.  

Suivante d’exécution hello commandes tooclone hello exemple référentiel et passer toohello *initialapp de 0,1* release.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Cet exemple de référentiel contient une application [Flask](http://flask.pocoo.org/). 

### <a name="run-hello-application"></a>Exécutez l’application hello

> [!NOTE] 
> Dans une étape ultérieure vous simplifiez ce processus en générant un toouse de conteneur Docker avec la base de données de production hello.

Installer des packages hello requis et démarrer l’application hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Lors de l’application hello est entièrement chargée, vous voyez quelque chose de similaire toohello message suivant :

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Accédez toohttp://127.0.0.1:5000 dans un navigateur. Cliquez sur **S’inscrire** et créez un utilisateur de test.

![Application Python Flask s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

Hello, exemple d’application ballon stocke les données utilisateur dans la base de données hello. Si vous parvenez à l’inscription d’un utilisateur, votre application écrit les données toohello PostgreSQL base de données locale.

serveur de ballon hello toostop à tout moment, tapez Ctrl + C dans hello Terminal Server. 

## <a name="create-a-production-postgresql-database"></a>Création d’une base de données de production PostgreSQL

Dans cette étape, vous allez créer une base de données PostgreSQL dans Azure. Lorsque votre application est déployée tooAzure, il utilisera cette base de données du cloud.

### <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Vous êtes en train de ressources de cours toouse hello Azure CLI 2.0 toocreate hello nécessaire toohost votre application Python dans Azure App Service.  Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec hello [az groupe créer](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello exemple suivant crée un groupe de ressources dans la région ouest des États-Unis hello :

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Hello d’utilisation [Liste emplacements az appservice](/cli/azure/appservice#list-locations) les emplacements disponibles toolist de commande CLI d’Azure.

### <a name="create-an-azure-database-for-postgresql-server"></a>Créer un serveur Azure Database pour PostgreSQL

Créer un serveur de PostgreSQL avec hello [az postgres serveur créer](/cli/azure/documentdb#create) commande.

Bonjour suivant de commande, remplacez par un nom unique pour hello  *\<postgresql_name >* espace réservé et un nom d’utilisateur pour hello  *\<admin_username >* espace réservé . nom du serveur Hello est utilisé dans le cadre de votre point de terminaison PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), de sorte que le nom hello doit toobe unique sur tous les serveurs dans Azure. nom d’utilisateur Hello est pour le compte d’utilisateur admin hello initiale de la base de données. Vous êtes invité à toopick un mot de passe pour cet utilisateur.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Lorsque hello Azure de base de données PostgreSQL serveur est créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Créer une règle de pare-feu pour hello Azure de base de données PostgreSQL serveur

Exécutez hello suivant de base de données access toohello CLI d’Azure commande tooallow à partir de toutes les adresses IP.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hello CLI d’Azure confirme la création de règles de pare-feu hello avec toohello similaire de sortie l’exemple suivant :

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

## <a name="connect-your-python-flask-application-toohello-database"></a>Se connecter à votre base de données Python ballon application toohello

Dans cette étape, vous vous connectez votre application toohello base de données Azure de Python ballon exemple pour serveur PostgreSQL que vous avez créé.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Création d’une base de données vide et configuration d’un nouvel utilisateur de l’application de base de données

Créer un utilisateur de base de données access tooa seule base de données uniquement. Vous utiliserez ces tooavoid des informations d’identification donnant hello application complète toohello serveur d’accès.

Se connecter toohello de base de données (vous êtes invité à entrer votre mot de passe d’administrateur).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Créer des base de données hello et l’utilisateur à partir de hello PostgreSQL CLI.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Type *\q* client de PostgreSQL tooexit hello.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Tester l’application hello localement par rapport à la base de données Azure PostgreSQL hello 

Si vous revenez en maintenant toohello *application* dossier Hello cloner le référentiel Github, vous pouvez exécuter des applications de Python ballon hello en mettant à jour les variables d’environnement hello de base de données.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Lors de l’application hello est entièrement chargée, vous voyez quelque chose de similaire toohello message suivant :

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Accédez toohttp://127.0.0.1:5000 dans un navigateur. Cliquez sur **S’inscrire** et créez une inscription de test. Maintenant, vous écrivez toohello de données dans Azure.

![Application Python Flask s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Exécution de l’application hello à partir d’un conteneur Docker

Création d’image de conteneur Docker hello.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker affiche une confirmation que le conteneur de hello informatique créé avec succès.

```bash
Successfully built 7548f983a36b
```

Ajouter la base de données environnement variables tooan variable fichier d’environnement *db.env*. application Hello se connecte à base de données PostgreSQL toohello de production dans Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Exécuter l’application hello de conteneur Docker de hello. Bonjour commande suivante spécifie le fichier de variable d’environnement hello et mappe hello par défaut ballon port 5000 toolocal port 5000.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

sortie de Hello est toowhat similaires, vous avez vu plus haut. Toutefois, la migration de base de données initiale hello n’a plus besoin toobe effectuée et qu’elle est donc ignorée.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

base de données Hello contient déjà un enregistrement hello que vous avez créé précédemment.

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Télécharger le Registre de conteneur hello Docker conteneur tooa

Dans cette étape, vous téléchargez Registre de conteneur tooa hello Docker conteneur. Vous allez utiliser Azure Container Registry, mais vous pourriez aussi d’autres registres très répandus, comme Docker Hub.

### <a name="create-an-azure-container-registry"></a>Création d’un Azure Container Registry

Bonjour suivant commande toocreate un Registre de conteneur remplacer  *\<registry_name >* avec un nom de Registre de conteneur Azure unique de votre choix.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Sortie
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Récupérer les informations d’identification du Registre hello pour les poussées et les images Docker

informations d’identification du Registre tooshow, activer le mode d’administration tout d’abord.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Vous voyez deux mots de passe. Notez hello nom d’utilisateur et mot de passe premier hello.

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Télécharger votre tooAzure de conteneur Docker Registre de conteneur

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Déployer hello Docker Python ballon application tooAzure

Dans cette étape, vous déployez votre tooAzure d’application de la Python ballon lors du conteneur Docker du Service d’applications.

### <a name="create-an-app-service-plan"></a>Créer un plan App Service

Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello exemple suivant crée un plan de Service d’applications basés sur Linux nommé *myAppServicePlan* à l’aide de hello S1, niveau de tarification :

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Lorsque hello plan App Service est créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :

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

### <a name="create-a-web-app"></a>Créer une application web

Créer une application web Bonjour *myAppServicePlan* plan App Service avec hello [az webapp créer](/cli/azure/webapp#create) commande. 

fournit les application Hello web vous un hébergement toodeploy votre code et de l’espace fournit une URL pour vous tooview hello déployé l’application. Utilisez l’application web toocreate hello. 

Bonjour suivant de commande, remplacez hello  *\<nom_application >* espace réservé avec un nom d’application unique. Ce nom fait partie de l’URL par défaut de hello pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure App Service. 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant : 

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

### <a name="configure-hello-database-environment-variables"></a>Configurer les variables d’environnement hello de base de données

Plus haut dans le didacticiel de hello, vous avez défini de données PostgreSQL tooyour environnement variables tooconnect.

Dans le Service d’application, vous définissez les variables d’environnement _paramètres de l’application_ à l’aide de hello [az webapp configuration appsettings défini](/cli/azure/webapp/config#set) commande. 

Hello exemple suivant spécifie détails de connexion de base de données hello en tant que paramètres de l’application. Il utilise également hello *PORT* variable toomap PORT 5000 à partir de votre conteneur Docker tooreceive HTTP le trafic sur le PORT 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Configuation du déploiement du conteneur Docker 

AppService peut automatiquement télécharger et exécuter un conteneur Docker.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Chaque fois que vous mettez à jour le conteneur Docker de hello ou modifiez les paramètres de hello, redémarrez l’application hello. Le redémarrage permet de s’assurer que tous les paramètres sont appliqués et conteneur de dernière hello est extraite à partir du Registre de hello.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Parcourir toohello Azure web app 

Parcourir l’application web toohello déployé à l’aide de votre navigateur web. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> Hello web application prend plus de temps tooload parce que le conteneur de hello a toobe téléchargé et démarré après la modification de configuration du conteneur hello.

Vous voyez des invités précédemment enregistrées qui ont été enregistrées de base de données de production Azure toohello à l’étape précédente de hello.

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Félicitations !** Vous exécutez une application Python Flask basée sur un conteneur Docker dans Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Mettre à jour le modèle de données et redéployer

Dans cette étape, vous ajoutez nombre hello d’inscription d’événement de participants tooeach en mettant à jour le modèle d’invité hello.

Extraire hello *0,2-migration* mise en production avec hello git commande suivante :

```bash
git checkout tags/0.2-migration
```

Cette version a déjà été hello du modèle, les contrôleurs et les modifications nécessaires tooviews. Elle inclut également une migration de base de données générée via *alembic* (`flask db migrate`). Vous pouvez voir toutes les modifications apportées via hello git commande suivante :

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Tester vos modifications en local

Exécutez hello suivant de commandes tootest vos modifications localement par serveur de ballon hello en cours d’exécution.

Mac / Linux :
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Accédez à toohttp://127.0.0.1:5000 vos modifications de hello tooview navigateur. Créez une inscription de test.

![Application Python Flask basée sur un conteneur Docker s’exécutant localement](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Publier les modifications tooAzure

Générer la nouvelle image de docker hello, poussez-le Registre de conteneur toohello et redémarrez l’application hello.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Accédez tooyour Azure web app et essayer à nouveau de nouvelles fonctionnalités de hello. Créez un autre enregistrement d’événements.

```bash 
http://<app_name>.azurewebsites.net 
```

![Application Docker Python Flask dans Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Gérer votre application web Azure

Accédez toohello [portail Azure](https://portal.azure.com) toosee vous avez créé l’application web hello.

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

Par défaut, le portail de hello affiche de votre application web **vue d’ensemble** page. Cette page propose un aperçu de votre application. Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). onglets Hello sur le côté gauche de hello de page de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.

![Page App Service du Portail Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Étapes suivantes

Avancer toolearn de didacticiel suivant toohello tooyour l’application web de noms toomap DNS personnalisé.

> [!div class="nextstepaction"] 
> [Mapper une tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md)
