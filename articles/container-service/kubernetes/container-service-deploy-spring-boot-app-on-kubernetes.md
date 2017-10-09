---
title: "aaaDeploy une application de démarrage ressort sur Kubernetes dans le Service de conteneur Azure | Documents Microsoft"
description: "Ce didacticiel vous guidera cependant hello étapes toodeploy une application de démarrage du ressort dans un cluster Kubernetes sur Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Déployer une Application de démarrage ressort sur un Kubernetes Cluster Bonjour Service de conteneur Azure

Hello  **[Spring Framework]**  est une infrastructure open source populaire qui permet aux développeurs Java de créer des applications web, mobiles et API. Ce didacticiel utilise un exemple d’application créé à l’aide de [ressort démarrage], une approche pilotée par convention pour l’utilisation du ressort tooget démarrer rapidement.

**[Kubernetes]**  et  **[client Docker]**  solutions en open source qui aident les développeurs sont automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications en cours d’exécution dans des conteneurs.

Ce didacticiel vous guide si la combinaison de ces deux technologies populaires, open source de toodevelop et déployer un tooMicrosoft d’application de démarrage du ressort Azure. Plus spécifiquement, vous utilisez  *[ressort démarrage]*  pour le développement d’applications,  *[Kubernetes]*  pour le déploiement de conteneur et hello [Conteneur de Service (ACS) de azure] toohost votre application.

### <a name="prerequisites"></a>Composants requis

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Hello [Azure Interface de ligne de commande (CLI)].
* Un [JDK (Java Developer Kit)] à jour.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [client Git].
* Un [client Docker].

> [!NOTE]
>
> En raison des exigences de la virtualisation toohello de ce didacticiel, vous ne peut pas suivre les étapes de hello dans cet article sur un ordinateur virtuel ; Vous devez utiliser un ordinateur physique avec les fonctionnalités de virtualisation activées.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Créer hello ressort démarrage sur Docker prise en main d’application web

Hello suit vous guide dans la création d’une application web de démarrage du ressort et le tester localement.

1. Ouvrez une invite de commandes et créer un répertoire local de toohold votre application, puis accédez au répertoire toothat ; par exemple :
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans l’annuaire de hello.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Changer le projet Active toohello s’est terminée.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Utilisez Maven toobuild et exécution hello, exemple d’application.
   ```
   mvn package spring-boot:run
   ```

1. Application web, test hello en parcourant toohttp://localhost:8080 ou avec les éléments suivants de hello `curl` commande :
   ```
   curl http://localhost:8080
   ```

1. Vous devez voir hello message suivant s’affiche : **Hello World de Docker**

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Créer un Registre de conteneur Azure à l’aide de hello CLI d’Azure

1. Ouvrez une invite de commandes.

1. Ouvrez une session dans tooyour compte Azure :
   ```azurecli
   az login
   ```

1. Créer un groupe de ressources pour hello ressources Azure utilisés dans ce didacticiel.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Créer un Registre de conteneur Azure privée dans le groupe de ressources hello. didacticiel de Hello transmet hello, exemple d’application en tant que Docker image toothis Registre dans les étapes ultérieures. Remplacez `wingtiptoysregistry` par un nom unique pour votre registre.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Push de votre Registre de conteneur d’application toohello

1. Parcourir le répertoire de configuration toohello pour votre installation Maven (valeur par défaut ~/.m2/ ou C:\Users\username\.m2) et ouvrez hello *settings.xml* fichier avec un éditeur de texte.

1. Récupérer un mot de passe hello pour votre Registre de conteneur de hello CLI d’Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Ajouter votre tooa Registre de conteneur Azure id et mot de passe nouveau `<server>` collection Bonjour *settings.xml* fichier.
Hello `id` et `username` sont nom hello du Registre de hello. Hello d’utilisation `password` valeur à partir de la commande précédente hello (sans guillemets).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Accédez répertoire du projet pour votre application de démarrage du ressort toohello terminée (par exemple, «*C:\SpringBoot\gs-spring-boot-docker\complete*« ou »*/users/robert/SpringBoot/gs-spring-boot-docker / complète*») et ouvrez hello *pom.xml* fichier avec un éditeur de texte.

1. Hello de mise à jour `<properties>` collection Bonjour *pom.xml* fichier avec la valeur hello du serveur de connexion pour votre Registre de conteneur Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Hello de mise à jour `<plugins>` collection Bonjour *pom.xml* de fichiers afin que hello `<plugin>` contient hello adresse et du Registre nom du serveur pour votre Registre de conteneur Azure.

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Accédez répertoire du projet pour votre application de démarrage du ressort toohello s’est terminée et exécutez les hello suivant commande toobuild hello Docker conteneur et push hello image toohello du Registre :

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Vous pouvez recevoir un message d’erreur est similaire tooone suivants de hello lorsque Maven pousse hello image tooAzure :
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Si vous obtenez cette erreur, ouvrez une session dans tooAzure à partir de la ligne de commande Docker hello.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Envoyez ensuite votre conteneur :
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Créer un Cluster de Kubernetes sur ACS à l’aide de hello CLI d’Azure

1. Créez un cluster Kubernetes dans Azure Container Service. Hello de commande suivant crée un *kubernetes* cluster Bonjour *wingtiptoys-kubernetes* ressource groupe avec *wingtiptoys-containerservice* en tant que cluster de hello nom, et *wingtiptoys-kubernetes* en tant que préfixe DNS hello :
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Cette commande peut prendre un certain temps toocomplete.

1. Installer `kubectl` à l’aide de hello CLI d’Azure. Les utilisateurs Linux peuvent avoir tooprefix cette commande avec `sudo` , car il déploie hello Kubernetes CLI trop`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Télécharger les informations de configuration de cluster hello vous pouvez de gérer votre cluster à partir de l’interface web hello Kubernetes et `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Déployer hello image tooyour Kubernetes cluster

Ce didacticiel déploie à l’aide d’application hello `kubectl`, puis vous autoriser le déploiement de hello tooexplore via l’interface web hello Kubernetes.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Déployer avec l’interface web hello Kubernetes

1. Ouvrez une invite de commandes.

1. Ouvrez le site Web de configuration hello pour votre cluster Kubernetes dans votre navigateur par défaut :
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Lorsque le site Web de configuration hello Kubernetes s’ouvre dans votre navigateur, cliquez sur le lien de hello trop**déployer une application en conteneur**:

   ![Site web de configuration Kubernetes][KB01]

1. Hello lorsque **déployer une application en conteneur** page s’affiche, spécifiez hello options suivantes :

   a. Sélectionnez **Spécifier les détails de l’application ci-dessous**.

   b. Entrez votre nom d’application de démarrage du ressort pour hello **nom de l’application**; par exemple : «*gs-spring-démarrage-docker*».

   c. Entrez votre image de conteneur et du serveur de connexion à partir de précédemment pour hello **image de conteneur**; par exemple : «*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*».

   d. Choisissez **externe** pour hello **Service**.

   e. Spécifiez les ports internes et externes dans hello **Port** et **cible port** zones de texte.

   ![Site web de configuration Kubernetes][KB02]


1. Cliquez sur **déployer** conteneur de hello toodeploy.

   ![Déployer le conteneur][KB05]

1. Une fois que votre application a été déployée, vous verrez votre application Spring Boot répertoriée sous **Services**.

   ![Services Kubernetes][KB06]

1. Si vous cliquez sur le lien hello pour **points de terminaison externes**, vous pouvez voir votre application ressort démarrage en cours d’exécution sur Azure.

   ![Services Kubernetes][KB07]

   ![Parcourir l’exemple d’application sur Azure][SB02]


### <a name="deploy-with-kubectl"></a>Déployer avec kubectl

1. Ouvrez une invite de commandes.

1. Exécuter votre conteneur dans le cluster de Kubernetes hello à l’aide de hello `kubectl run` commande. Donnez un nom de service pour votre application dans Kubernetes et le nom de l’image complète hello. Par exemple :
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   Dans cette commande :

   * nom du conteneur Hello `gs-spring-boot-docker` est spécifié immédiatement après hello `run` commande

   * Hello `--image` paramètre spécifie hello combinées de serveur de connexion et le nom de l’image en tant que`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Exposer votre cluster Kubernetes en externe à l’aide de hello `kubectl expose` commande. Spécifiez le nom de votre service, hello publique TCP port utilisé tooaccess hello application et le port de cible interne hello écouté par votre application. Par exemple :
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   Dans cette commande :

   * nom du conteneur Hello `gs-spring-boot-docker` est spécifié immédiatement après hello `expose deployment` commande

   * Hello `--type` paramètre spécifie que le cluster hello utilise l’équilibrage de charge

   * Hello `--port` paramètre spécifie le port TCP 80 hello publics. Vous accéder à application hello sur ce port.

   * Hello `--target-port` paramètre spécifie hello interne le port TCP 8080. équilibrage de charge Hello transfère application tooyour de demandes sur ce port.

1. Une fois que l’application hello est déployée toohello cluster, une adresse IP externe hello de requête et l’ouvrir dans votre navigateur web :

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Parcourir l’exemple d’application sur Azure][SB02]


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation de démarrage du ressort sur Azure, consultez hello suivant des articles :

* [Déployer un toohello ressort démarrage Application Azure App Service](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Déployer une application de démarrage du ressort sur Linux Bonjour Service de conteneur Azure](container-service-deploy-spring-boot-app-on-linux.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur hello ressort démarrage sur l’exemple de projet Docker, consultez [démarrage ressort sur Docker mise en route].

Hello suivant liens fournit des informations supplémentaires sur la création d’applications de démarrage du ressort :

* Pour plus d’informations sur la création d’une application de démarrage du ressort simple, consultez hello ressort Initializr à https://start.spring.io/.

Hello liens suivants fournissent des informations supplémentaires sur l’utilisation de Kubernetes avec Azure :

* [Prise en main d’un cluster Kubernetes dans Container Service](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [À l’aide de hello Kubernetes web l’interface utilisateur avec le Service de conteneur Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Plus d’informations sur l’utilisation d’une interface de ligne Kubernetes est disponible dans hello **kubectl** guide de l’utilisateur à <https://kubernetes.io/docs/user-guide/kubectl/>.

site Web de Kubernetes Hello comporte plusieurs articles qui traitent de l’utilisation d’images dans les registres privés :

* [Configuration des comptes de service pour des pods]
* [Espaces de noms]
* [Extraction d’une image à partir d’un registre privé]

Pour obtenir des exemples supplémentaires pour comment toouse personnalisé Docker images avec Azure, consultez [à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux].

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Conteneur de Service (ACS) de azure]: https://azure.microsoft.com/services/container-service/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configuration des comptes de service pour des pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Espaces de noms]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extraction d’une image à partir d’un registre privé]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
