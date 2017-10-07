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
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Créer une application web Java et MySQL dans Azure

Ce didacticiel vous montre comment toocreate Java web application dans Azure et le connecter tooa base de données MySQL. Lorsque vous avez terminé, une application [Spring Boot](https://projects.spring.io/spring-boot/) stockera des données dans [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) s’exécutant sous [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Application Java s’exécutant dans Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

Ce tutoriel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Création d’une base de données MySQL dans Azure
> * Se connecter à une base de données exemple application toohello
> * Déployer hello application tooAzure
> * Mettre à jour et redéployer l’application hello
> * Diffusion des journaux de diagnostic à partir d’Azure
> * Analyser l’application hello Bonjour portail Azure


## <a name="prerequisites"></a>Composants requis

1. [Téléchargement et installation de Git](https://git-scm.com/)
1. [Téléchargez et installez hello Java JDK de 7 ou version ultérieure](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [Téléchargement, installation et démarrage de MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Préparation du MySQL local 

Dans cette étape, vous créez une base de données dans un serveur MySQL local à utiliser dans le test application hello localement sur votre ordinateur.

### <a name="connect-toomysql-server"></a>Se connecter tooMySQL server

Dans une fenêtre de terminal, connectez-vous tooyour local MySQL server. Vous pouvez utiliser cette fenêtre de terminal de toorun toutes les commandes hello dans ce didacticiel.

```bash
mysql -u root -p
```

Si vous êtes invité à entrer un mot de passe, entrez le mot de passe hello pour hello `root` compte. Si vous avez oublié votre mot de passe du compte racine, consultez [MySQL : comment tooReset hello mot de passe racine](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Si la commande est exécutée correctement, votre serveur MySQL est déjà en cours d’exécution. Dans le cas contraire, assurez-vous que votre serveur MySQL local est démarrée par hello suivant [les étapes de post-installation MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Créer une base de données 

Bonjour `mysql` invite, créer une base de données et une table pour hello choses.

```sql
CREATE DATABASE tododb;
```

Quittez votre connexion au serveur en tapant `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Créer et exécuter l’exemple d’application hello 

Dans cette étape, vous clonez l’exemple d’application de démarrage du ressort, configurez la base de données MySQL locale toouse hello et exécutez sur votre ordinateur. 

### <a name="clone-hello-sample"></a>Exemple hello de clone

Dans la fenêtre de terminal hello, accédez à tooa utilisation dépôt d’exemples hello active et clone. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Configurer la base de données de MySQL hello application toouse hello

Hello de mise à jour `spring.datasource.password` et la valeur de *spring-boot-mysql-todo/src/main/resources/application.properties* avec hello même mot de passe racine utilisé invite de MySQL tooopen hello :

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Générer et exécuter l’exemple hello

Générer et exécuter l’exemple hello à l’aide du wrapper de Maven hello inclus dans le référentiel de hello :

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Dans l’exemple hello en action, ouvrez votre toosee toohttp://localhost:8080 de navigateur. Lorsque vous ajoutez la liste des tâches de toohello, utilisez hello SQL suivant des commandes hello MySQL tooview invite hello présentes dans MySQL.

```SQL
use testdb;
select * from todo_item;
```

Arrêter l’application hello en appuyant sur `Ctrl` + `C` Bonjour Terminal Server. 

## <a name="create-an-azure-mysql-database"></a>Création d’une base de données Azure MySQL

Dans cette étape, vous allez créer un [base de données Azure pour MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/install-azure-cli). Vous configurez toouse d’application exemple hello cette base de données ultérieurement dans le didacticiel de hello.

Hello utilisation Azure CLI 2.0 dans un fenêtre de terminal toocreate hello des ressources nécessaires toohost votre application Java dans Azure app service. Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique où les ressources associées comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources dans la région Europe du Nord hello :

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

Vous pouvez utiliser pour les valeurs possibles hello toosee `--location`, utilisez hello [Liste emplacements az app service](/cli/azure/appservice#list-locations) commande.

### <a name="create-a-mysql-server"></a>Création d’un serveur MySQL

Créer un serveur de base de données Azure pour MySQL (version préliminaire) avec hello [az mysql server créer](/cli/azure/mysql/server#create) commande.    
Remplacez par votre propre nom de serveur MySQL unique dans lequel vous consultez hello `<mysql_server_name>` espace réservé. Ce nom fait partie du nom d’hôte de votre serveur MySQL `<mysql_server_name>.mysql.database.azure.com`, par conséquent, il doit toobe global unique. Remplacez également `<admin_user>` et `<admin_password>` par vos propres valeurs.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Lorsque le serveur MySQL de hello est créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

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

### <a name="configure-server-firewall"></a>Configuration d’un pare-feu de serveur

Créer une règle de pare-feu pour votre client de tooallow MySQL server connexions à l’aide de hello [az mysql server-règle de pare-feu créer](/cli/azure/mysql/server/firewall-rule#create) commande. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure Database pour MySQL (version préliminaire) ne permet pas encore les connexions automatiques à partir des services Azure. Comme les adresses IP dans Azure sont attribuées dynamiquement, il est mieux tooenable toutes les adresses IP pour maintenant. Service de hello continue son aperçu, meilleures méthodes pour la sécurisation de votre base de données seront activés.

## <a name="configure-hello-azure-mysql-database"></a>Configurer la base de données MySQL de Azure hello

Dans la fenêtre de terminal hello sur votre ordinateur, connectez-vous toohello MySQL server dans Azure. Utilisez la valeur hello spécifiée précédemment pour `<admin_user>` et `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Créer une base de données 

Bonjour `mysql` invite, créer une base de données et une table pour hello choses.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Création d’un utilisateur avec des autorisations

Créer un utilisateur de base de données et de lui donner tous les privilèges Bonjour `tododb` base de données. Remplacez les espaces réservés de hello `<Javaapp_user>` et `<Javaapp_password>` avec votre propre nom d’application unique.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Quittez votre connexion au serveur en tapant `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Déployer hello exemple tooAzure du Service d’applications

Créer un plan de Service d’application Azure avec hello **libre** tarification à l’aide de hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande CLI. un plan de Hello définit hello ressources physiques utilisées toohost vos applications. Toutes les applications affectées tooan un plan de partagent ces ressources, ce qui vous toosave coût lors de l’hébergement de plusieurs applications. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Lorsque le plan de hello est prêt, hello Qu'azure CLI montre similaire de sortie toohello l’exemple suivant :

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

### <a name="create-an-azure-web-app"></a>Création d’une application web Azure

 Hello d’utilisation [az webapp créer](/cli/azure/appservice/web#create) toocreate de commande CLI une définition d’application web Bonjour `myAppServicePlan` plan App Service. définition d’application web Hello fournit à votre application un tooaccess URL et configure plusieurs options toodeploy tooAzure de votre code. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Hello de substitution `<app_name>` espace réservé avec votre propre nom d’application unique. Ce nom unique fait partie du nom de domaine par défaut hello pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure. Vous pouvez mapper une application web de domaine personnalisé nom entrée toohello avant de vous exposez tooyour utilisateurs.

Lors de la définition d’application web hello est prête, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant : 

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

### <a name="configure-java"></a>Configurer Java 

Configuration de hello Java runtime dont votre application a besoin par hello [mise à jour du fichier config web app service az](/cli/azure/appservice/web/config#update) commande.

Hello commande suivante configure hello web application toorun sur une récente Java JDK de 8 et [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Configurer la base de données de SQL Azure hello application toouse hello

Avant d’exécuter l’exemple d’application hello, définir les paramètres de l’application sur hello web application toouse hello Azure base de données MySQL que vous avez créé dans Azure. Ces propriétés sont toohello exposé à l’application web en tant que variables d’environnement et remplacent les valeurs de hello définies dans application.properties hello à l’intérieur de hello empaquetée web app. 

Définir les paramètres de l’application à l’aide de [az webapp configuration appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) Bonjour CLI :

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

### <a name="get-ftp-deployment-credentials"></a>Obtention des informations d’identification de déploiement FTP 
Vous pouvez déployer votre application tooAzure service d’applications de différentes manières, notamment FTP, local Git, GitHub, Visual Studio Team Services et BitBucket. Pour cet exemple, FTP toodeploy hello. Fichier WAR créé précédemment sur votre ordinateur local de tooAzure du Service d’applications.

toodetermine les informations d’identification les toopass le long dans un toohello commande ftp application Web, utilisez [az app service web de déploiement liste-publication-profils](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) commande : 

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

### <a name="upload-hello-app-using-ftp"></a>Télécharger l’application hello à l’aide de FTP

Utilisez votre hello de toodeploy outil FTP favori. Toohello de fichier WAR */site/wwwroot/webapps* dossier sur l’adresse du serveur hello provenant de hello `URL` champ dans la commande précédente hello. Supprimer le répertoire de l’application hello existant par défaut (racine) et remplacez hello existants dans ROOT.war hello. Fichier WAR intégré hello plus haut dans le didacticiel de hello.

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

### <a name="test-hello-web-app"></a>Application de test hello web

Parcourir trop`http://<app_name>.azurewebsites.net/` et ajouter quelques tâches toohello. 

![Application Java s’exécutant dans Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Félicitations !** Vous exécutez une application Java pilotée par les données dans Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Redéploiement et application hello de mise à jour

Mettre à jour hello application tooinclude une colonne supplémentaire dans la liste de tâches hello pour quel élément de hello jour a été créée. Démarrage du ressort gère sans modifier vos enregistrements de base de données existante en tant que les modifications du modèle de données hello schéma de base de données mise à jour hello pour vous.

1. Sur votre système local, ouvrez *src/main/java/com/example/fabrikam/TodoItem.java* et ajoutez suivant de hello importe toohello classe :   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Ajouter un `String` propriété `timeCreated` trop*src/main/java/com/example/fabrikam/TodoItem.java*, l’initialiser avec un horodateur de création de l’objet. Ajouter des accesseurs Get/Set pour hello nouvelle `timeCreated` propriété lorsque vous modifiez ce fichier.

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

3. Mise à jour *src/main/java/com/example/fabrikam/TodoDemoController.java* avec une ligne Bonjour `updateTodo` méthode tooset hello horodateur :

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Ajouter la prise en charge pour le nouveau champ de hello dans le modèle de Thymeleaf hello. Mise à jour *src/main/resources/templates/index.html* avec un nouvel en-tête de table pour hello timestamp et une nouvelle valeur hello toodisplay champ timestamp hello dans chaque ligne de données de table.

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

5. Régénérer l’application hello :

    ```bash
    mvnw clean package 
    ```

6. FTP hello mis à jour. WAR comme précédemment, supprimer des domaines existants de hello *site/wwwroot/WebApp/ROOT* active et *ROOT.war*, puis télécharger hello mis à jour. Fichier WAR comme ROOT.war. 

Lorsque vous actualisez l’application hello, un **créé** colonne est maintenant visible. Lorsque vous ajoutez une nouvelle tâche, application hello remplir automatiquement hello timestamp. Vos tâches existantes restent inchangées et de travailler avec l’application hello même si hello sous-jacente du modèle de données a changé. 

![Mise à jour d’application Java avec une nouvelle colonne](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Diffuser les journaux de diagnostic 

Pendant que votre application Java s’exécute dans Azure App Service, vous pouvez obtenir les console hello journaux transmis directement tooyour Terminal Server. De cette façon, vous pouvez obtenir hello des messages de diagnostic mêmes toohelp vous déboguez des erreurs d’application.

journal toostart de diffusion en continu, utilisez hello [la fin du journal de az webapp](/cli/azure/appservice/web/log#tail) commande.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Gérer votre application web Azure

Accédez à toohello toosee portail Azure hello web app, que vous avez créé.

toodo, connectez-vous trop[https://portal.azure.com](https://portal.azure.com).

Dans le menu de gauche hello, cliquez sur **du Service d’applications**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-java-mysql/access-portal.png)

Par défaut, les lames de votre application web montre hello **vue d’ensemble** page. Cette page propose un aperçu de votre application. Ici, vous pouvez également effectuer des tâches de gestion (arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). onglets Hello sur le côté gauche de hello du Panneau de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.

![Panneau App Service sur le portail Azure](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Ces onglets dans le panneau de hello affichent hello de nombreuses fonctionnalités, vous pouvez ajouter l’application web tooyour. Hello suivant liste vous donne quelques possibilités de hello :
* Mapper un nom DNS personnalisé
* Lier un certificat SSL personnalisé
* Configurer le déploiement continu
* Montée en puissance et augmentation de la taille des instances
* Ajouter une authentification utilisateur

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous ne devez pas ces ressources pour un autre didacticiel (consultez [étapes](#next)), vous pouvez les supprimer en exécutant hello de commande suivante : 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Étapes suivantes

> [!div class="checklist"]
> * Création d’une base de données MySQL dans Azure
> * Se connecter à un toohello d’application exemple Java MySQL
> * Déployer hello application tooAzure
> * Mettre à jour et redéployer l’application hello
> * Diffusion des journaux de diagnostic à partir d’Azure
> * Gérer l’application hello Bonjour portail Azure

Avancer toolearn de didacticiel suivant toohello toohello application de noms toomap DNS personnalisé.

> [!div class="nextstepaction"] 
> [Mapper une tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md)
