---
title: "aaaExecute hello CLI d’Azure avec Jenkins | Documents Microsoft"
description: "Découvrez comment toouse CLI d’Azure toodeploy Java web tooAzure d’application dans le Pipeline de Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Déployer tooAzure du Service d’applications avec Jenkins et hello CLI d’Azure
toodeploy un tooAzure d’application web Java, vous pouvez utiliser CLI d’Azure dans [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/). Dans ce didacticiel, vous créez un pipeline CI/CD sur une machine virtuelle Azure et apprenez notamment comment :

> [!div class="checklist"]
> * Créer une machine virtuelle Jenkins
> * Configurer Jenkins
> * Créer une application web dans Azure
> * Préparer un dépôt GitHub
> * Créer un pipeline Jenkins
> * Exécuter le pipeline de hello et vérifiez que l’application web hello

Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. version de hello toofind, exécutez `az --version`. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Créer et configurer l’instance Jenkins
Si vous n’avez pas déjà un maître de Jenkins, commencer par hello [modèle de Solution](install-jenkins-solution-template.md), qui inclut la hello requis [informations d’identification Azure](https://plugins.jenkins.io/azure-credentials) plug-in par défaut. 

plug-in des informations d’identification Azure Hello vous permet d’informations d’identification toostore Microsoft Azure service principales de Jenkins. Dans la version 1.2, nous avons ajouté la prise en charge de hello ce Jenkins Pipeline peut obtenir des informations d’identification Azure hello. 

Vérifiez que vous disposez de la version 1.2 ou d’une version ultérieure :
* Dans le tableau de bord hello Jenkins, cliquez sur **Jenkins de gérer -> Gestionnaire de plug-in ->** et recherchez **informations d’identification Azure**. 
* Mettre à jour des plug-in hello si la version de hello est antérieure à la version 1.2.

Java JDK et Maven sont également requis dans master de Jenkins hello. tooinstall, connectez-vous dans master tooJenkins à l’aide de SSH, puis réexécutez hello suivant de commandes :
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Ajouter des informations d’identification de service Azure principal tooJenkins

Informations d’identification Azure sont nécessaire tooexecute CLI d’Azure.

* Dans le tableau de bord hello Jenkins, cliquez sur **informations d’identification -> système ->**. Cliquez sur **Informations d’identification globales (sans restriction)**.
* Cliquez sur **ajouter les informations d’identification** tooadd un [principal du service Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en remplissant hello ID d’abonnement, ID de Client, question secrète du Client et OAuth 2.0 Token Endpoint. Fournissez un ID qui sera utilisé dans une étape ultérieure.

![Ajout d’informations d'identification](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Créer un Service d’application Azure pour le déploiement d’application web Java hello

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

## <a name="prepare-a-github-repository"></a>Préparer un dépôt GitHub
Ouvrez hello [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) référentiel. toofork hello référentiel tooyour propre compte GitHub, cliquez sur hello **branchement** bouton dans le coin supérieur droit de hello.

* Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile**. Cliquez sur hello crayon icône tooedit ce groupe de ressources de fichier tooupdate hello et le nom de votre application web sur la ligne 20 et 21 respectivement.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Modifier les informations d’identification ligne 23 tooupdate dans votre instance Jenkins

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Créer un pipeline Jenkins
Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**. 

* Fournissez un nom pour le travail de hello et sélectionnez **Pipeline**. Cliquez sur **OK**.
* Cliquez sur hello **Pipeline** onglet suivant. 
* Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.
* Pour **SCM**, sélectionnez **Git**.
* Entrez hello GitHub URL pour votre référentiel RAMIFIÉ : https :\<votre dépôt RAMIFIÉ\>.git
* Cliquez sur **Enregistrer**.

## <a name="test-your-pipeline"></a>Tester votre pipeline
* Accédez pipeline toohello vous avez créé, cliquez sur **générer maintenant**
* Une build doit réussir en quelques secondes, et vous pouvez toohello build et cliquez sur **la sortie de Console** détails de hello toosee

## <a name="verify-your-web-app"></a>Vérifier votre application web
le fichier WAR tooverify hello est déployé avec succès l’application web tooyour. Ouvrez un navigateur web :

* Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping  
Vous voyez :

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y

![Calculatrice : ajouter](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Déployer tooAzure application Web sur Linux
Maintenant que vous savez comment toouse CLI d’Azure dans votre Jenkins de pipeline, vous pouvez modifier hello script toodeploy tooan Azure Web App sur Linux.

Web application sur Linux prend en charge un déploiement différemment toodo hello, qui est toouse Docker. toodeploy, vous devez tooprovide un fichier Dockerfile par les packages de votre application web avec le runtime du service dans une image Docker. plug-in Hello ensuite générer l’image de hello, poussez-le du Registre de tooa Docker et déployer l’application web de hello image tooyour.

* Suivez les étapes de hello [ici](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate une application Web de Azure en cours d’exécution sur Linux.
* Installer Docker sur votre instance de Jenkins en suivant les instructions de hello dans ce [article](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Créer un conteneur de Registre Bonjour portail Azure à l’aide des étapes de hello [ici](/azure/container-registry/container-registry-get-started-azure-cli).
* Dans hello même [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) référentiel vous dupliquée, modifier hello **Jenkinsfile2** fichier :
    * Ligne de 18-21, mettre à jour les noms de toohello de votre groupe de ressources, une application web et un ACR respectivement. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Ligne 24, mise à jour \<azsrvprincipal\> tooyour d’identification
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Créer un pipeline Jenkins comme vous l’avez fait lors du déploiement d’application web de tooAzure dans Windows, cette fois, utilisez **Jenkinsfile2** à la place.
* Exécutez votre nouveau travail.
* tooverify, dans Azure CLI, exécutez :

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Vous obtenez hello suivant des résultats :
    
    ```
    [
    "calculator"
    ]
    ```
    
    Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping. Vous voyez le message de type hello : 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y
    
## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez configuré un pipeline de Jenkins extrait de code source de hello dans le référentiel GitHub. Exécute Maven toobuild un fichier war, puis utilise Azure CLI toodeploy tooAzure du Service d’applications. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer une machine virtuelle Jenkins
> * Configurer Jenkins
> * Créer une application web dans Azure
> * Préparer un dépôt GitHub
> * Créer un pipeline Jenkins
> * Exécuter le pipeline de hello et vérifiez que l’application web hello
