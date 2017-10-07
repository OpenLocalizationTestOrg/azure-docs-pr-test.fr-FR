---
title: "aaaDeploy tooAzure du Service d’applications avec Jenkins Plugin | Documents Microsoft"
description: "Découvrez comment toodeploy de plug-in Azure App Service Jenkins toouse Java web tooAzure app dans Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Déployer tooAzure du Service d’applications avec le plug-in de Jenkins 
toodeploy un tooAzure d’application web Java, vous pouvez utiliser CLI d’Azure dans [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) ou vous pouvez utiliser de hello [plug-in Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service). Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Configurer Jenkins toodeploy tooAzure du Service d’applications via FTP 
> * Configurer Jenkins toodeploy tooAzure du Service d’applications sur Linux avec Docker 

## <a name="create-and-configure-jenkins-instance"></a>Créer et configurer l’instance Jenkins
Si vous n’avez pas déjà un maître de Jenkins, commencer par hello [modèle de Solution](install-jenkins-solution-template.md), ce qui inclut JDK8 et hello suivant plug-ins requis :

* [Plug-in du client Git Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Informations d’identification Azure](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1

Vous pouvez utiliser hello toodeploy de plug-in du Service d’applications Web App dans toutes les langues (par exemple, c#, PHP, Java et node.js, etc.) sont pris en charge par le Service d’applications Azure. Dans ce didacticiel, nous utilisons hello exemple d’application Java, [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample). toofork hello référentiel tooyour propre compte GitHub, cliquez sur hello **branchement** bouton dans le coin supérieur droit de hello.  

Java JDK et Maven sont requis pour la création de projet de Java hello. Veillez à qu'installer les composants hello dans master de Jenkins hello ou agent de machine virtuelle hello si vous utilisez un seul pour l’intégration continue. 

tooinstall, connectez-vous en instance de Jenkins toohello à l’aide de SSH et exécutez hello suivant les commandes :

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Pour le déploiement de tooApp Service sur Linux, vous devez également tooinstall Docker sur master de Jenkins hello ou un agent de machine virtuelle hello utilisé pour la build. Consultez l’article de toothis tooinstall Docker : https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Ajouter des informations d’identification de service Azure principal tooJenkins

Un principal du service Azure est nécessaire toodeploy tooAzure. 

<ol>
<li>Utilisez [CLI d’Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ou [portail Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate un principal du service Azure</li>
<li>Dans le tableau de bord hello Jenkins, cliquez sur **informations d’identification -> système ->**. Cliquez sur **Informations d’identification globales (sans restriction)**.</li>
<li>Cliquez sur **ajouter les informations d’identification** tooadd un principal de service Microsoft Azure en remplissant hello ID d’abonnement, ID de Client, question secrète du Client et OAuth 2.0 Token Endpoint. Fournissez l’ID, **mySp**, à utiliser dans les étapes ultérieures.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Plug-in Azure App Service

V1.0 de plug-in du Service d’applications Azure prend en charge le déploiement continu tooAzure application Web via :

* Git et FTP
* Docker pour application web sur Linux

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Configurer Jenkins toodeploy application Web via FTP à l’aide du tableau de bord hello Jenkins

toodeploy votre tooAzure de project Web App, vous pouvez télécharger vos artefacts de build (par exemple, les fichier .war dans Java) à l’aide de Git ou FTP.

Avant de configurer la tâche hello dans Jenkins, vous devez un plan de Service d’applications Azure et une application Web pour l’application de Java hello en cours d’exécution.


1. Créer un plan de Service d’application Azure avec hello **libre** tarification à l’aide de hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande CLI. un plan de Hello définit hello ressources physiques utilisées toohost vos applications. Toutes les applications affectées tooan un plan de partagent ces ressources, ce qui vous toosave coût lors de l’hébergement de plusieurs applications.
2. Créez une application web. Vous pouvez soit hello utilisation [portail Azure](/azure/app-service-web/web-sites-configure) ou utilisez hello suit commande Az CLI :
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Assurez-vous que vous définissez configuration hello Java runtime dont votre application a besoin. Hello suivant commande CLI d’Azure configure hello web application toorun sur une récente Java JDK de 8 et [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Configurer la tâche de Jenkins hello


1. Créer un nouveau projet **freestyle** dans le tableau de bord Jenkins
2. Configurer **gestion du Code Source** toouse votre branche local de [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) en fournissant hello **URL du référentiel**. Par exemple : http://github.com/&lt;votreID>/javawebappsample.
3. Ajoutez un projet de hello Build étape toobuild à l’aide de Maven. Pour ce faire, ajoutez une étape **Exécuter un interpréteur de commandes**. Pour cet exemple, nous avons besoin d’un fichier étape supplémentaire toorename hello *.war dans tooROOT.war du dossier cible.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Ajoutez une action post-build en sélectionnant **Publier une application web Azure**.
5. Approvisionnement, « mySp » principal du service Azure hello stockées dans l’étape précédente.
6. Dans **Configuration de l’application** , choisissez hello ressource groupe et l’application web dans votre abonnement. plug-in Hello détecte automatiquement si hello application Web est Windows ou Linux. Pour une application Web basée sur Windows, l’option hello « Publier les fichiers » est présentée.
7. Remplir dans les fichiers de hello souhaité toodeploy (par exemple, un war package si vous utilisez Java.) Les répertoires source et cible sont facultatifs. paramètres de Hello permettent les dossiers source et cible toospecify lors du téléchargement de fichiers. L’application web Java sur Azure est exécutée sur un serveur Tomcat. Ainsi, vous chargez votre package war dans le dossier webapps. Pour cet exemple, définissez **répertoire Source** trop « cible » et fournir des applications « Web » pour **répertoire cible**.
8. Si vous souhaitez que le connecteur de tooa toodeploy autre que de production, vous pouvez également définir **emplacement** nom.
9. Enregistrer le projet de hello et générez-le. Votre application web est déployée tooAzure lors de la build est terminée.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Déployer l’application Web via FTP à l’aide du pipeline Jenkins

plug-in Hello est compatible avec le pipeline. Vous pouvez consulter l’exemple tooa dans le référentiel GitHub de hello.

1. Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile_ftp_plugin**. Cliquez sur hello crayon icône tooedit ce groupe de ressources de fichier tooupdate hello et le nom de votre application web sur la ligne 11 et 12 respectivement.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Modifier la ligne 14 tooupdate d’identification de votre instance de Jenkins.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Créer un pipeline Jenkins

1. Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.
2. Fournissez un nom pour le travail de hello et sélectionnez **Pipeline**. Cliquez sur **OK**.
3. Cliquez sur hello **Pipeline** onglet suivant.
4. Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.
5. Pour **SCM**, sélectionnez **Git**. Entrez hello GitHub URL pour votre référentiel RAMIFIÉ : https :&lt;votre dépôt RAMIFIÉ > .git
6. Mise à jour **chemin d’accès du Script** trop « Jenkinsfile_ftp_plugin »
7. Cliquez sur **enregistrer** et la tâche d’exécution hello.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Configurer Jenkins toodeploy application Web sur Linux avec Docker

Outre Git/FTP, l’application web sur Linux prend en charge le déploiement à l’aide de Docker. toodeploy à l’aide de Docker, vous devez tooprovide un fichier Dockerfile par les packages de votre application web avec le runtime du service dans une image docker. Plug-in hello génère des images de hello, il transmet le Registre de docker tooa, puis déploie l’application web de hello image tooyour.

L’application web sur Linux prend également en charge les méthodes traditionnelles telles que Git et FTP, mais uniquement pour les langages intégrés (.NET Core, Node.js, PHP et Ruby). Pour d’autres langues, vous devez toopackage votre exécution de code et le service de l’application ensemble dans une image docker et utilisez docker toodeploy.

Avant de configurer la tâche hello dans Jenkins, vous devez un service d’application Azure sur Linux. Un Registre de conteneur est également nécessaire toostore et gérer vos images de conteneur Docker privés. Vous pouvez utiliser DockerHub ; nous utilisons Azure Container Registry pour cet exemple.

* Vous pouvez suivre les étapes de hello [ici](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate une application Web sur Linux 
* Registre de conteneur Azure est géré [Docker Registre] service (https://docs.docker.com/registry/) en fonction de hello 2.0 de Registre Docker open source. Suivez les étapes de hello [ici] (/ azure/container-registry/container-registry-get-started-azure-cli) pour plus d’informations sur la façon de toodo donc. Vous pouvez également utiliser DockerHub.

### <a name="toodeploy-using-docker"></a>toodeploy à l’aide de docker :

1. Créez un nouveau projet freestyle dans le tableau de bord Jenkins.
2. Configurer **gestion du Code Source** toouse votre branche local de [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) en fournissant hello **URL du référentiel**. Par exemple : http://github.com/&lt;votre_id>/javawebappsample.
Ajoutez un projet de hello Build étape toobuild à l’aide de Maven. Faire en ajoutant une **exécuter shell** et ajoutez hello ligne dans **commande**:    
```bash
mvn clean package
```

3. Ajoutez une action post-build en sélectionnant **Publier une application web Azure**.
4. Fournissez, **mySp**, principal du service Azure hello stockée dans l’étape précédente en tant qu’informations d’identification Azure.
5. Dans **Configuration de l’application** , choisissez le groupe de ressources hello et une application web de Linux dans votre abonnement.
6. Choisissez Publier via Docker.
7. Renseignez le chemin **Dockerfile**. Vous pouvez conserver la valeur par défaut hello « / Dockerfile » pour **URL de Registre Docker**, fournissez au format hello https://&lt;myRegistry >. azurecr.io si vous utilisez le Registre de conteneur Azure. Laissez ce champ vide si vous utilisez DockerHub.
8. Pour **informations d’identification du Registre**, ajouter des informations d’identification de hello pour hello Registre de conteneur Azure. Vous pouvez obtenir hello userid et password par hello suivant des commandes CLI d’Azure en cours d’exécution. Hello première commande active compte d’administrateur hello.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Hello du nom de l’image docker et de balise dans **avancé** onglet sont facultatifs. Par défaut, le nom de l’image est obtenue à partir de l’image de hello nom que vous avez configuré dans la balise d’Azure hello portail (dans le paramètre de conteneur Docker.) est généré à partir de $BUILD_NUMBER. Assurez-vous que vous spécifiez le nom de l’image hello dans des portails Azure ou fournissez une valeur pour **Image Docker** dans **avancé** onglet. Pour cet exemple, indiquez « &lt;votreRegistre>.azurecr.io/calculator » pour **Image Docker** et ne renseignez pas **Balise d’image Docker**.
10. Notez que le déploiement échoue si vous utilisez le paramètre Image Docker prédéfini. Assurez-vous de que modifier docker config toouse personnalisée dans le paramètre de conteneur Docker dans le portail Azure. Pour l’image intégrée, utilisez toodeploy de méthode de téléchargement de fichier.
11. Méthode de téléchargement toofile similaire, vous pouvez choisir un autre emplacement autre que de production.
12. Enregistrez et générez le projet de hello. Vous voyez votre image de conteneur est transmise tooyour Registre et de l’application web est déployée.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>Déployer tooWeb application sur Linux avec Docker à l’aide du pipeline de Jenkins

1. Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile_container_plugin**. Cliquez sur hello crayon icône tooedit ce groupe de ressources de fichier tooupdate hello et le nom de votre application web sur la ligne 11 et 12 respectivement.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Modifier la ligne 13 tooyour conteneur Registre serveur    
```java
def registryServer = '<registryURL>'
```    

3. Modifier la ligne 16 tooupdate d’identification de votre instance Jenkins    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Créer un pipeline Jenkins    

1. Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.
2. Fournissez un nom pour le travail de hello et sélectionnez **Pipeline**. Cliquez sur **OK**.
3. Cliquez sur hello **Pipeline** onglet suivant.
4. Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.
5. Pour **SCM**, sélectionnez **Git**.
6. Entrez hello GitHub URL pour votre référentiel RAMIFIÉ : https :&lt;votre dépôt RAMIFIÉ > .git</li>
Mise à jour 7, **chemin d’accès du Script** trop « Jenkinsfile_container_plugin »
8. Cliquez sur **enregistrer** et la tâche d’exécution hello.

## <a name="verify-your-web-app"></a>Vérifier votre application web

1. le fichier WAR tooverify hello est déployé avec succès l’application web tooyour. Ouvrez un navigateur web.
2. Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping vous consultez :    
     Bienvenue dans l’application Web de tooJava !!! La mise à jour est effectuée !
   Sun Jun 17 16:39:10 UTC 2017
3. Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y        
    ![Calculatrice : ajouter](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Pour App Service sur Linux

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

Dans ce didacticiel, vous utilisez hello Azure App Service plug-in toodeploy tooAzure.

Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Configurer Jenkins toodeploy Azure App Service via FTP 
> * Configurer Jenkins toodeploy tooAzure du Service d’applications sur Linux avec Docker 
