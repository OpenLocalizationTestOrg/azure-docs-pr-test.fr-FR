---
title: "aaaDeploy une application de Web démarrage ressort sur Linux dans le Service de conteneur Azure | Documents Microsoft"
description: "Ce didacticiel vous guide cependant hello étapes toodeploy une application de démarrage du ressort comme une application web de Linux sur Microsoft Azure."
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
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Déployer une application de démarrage du ressort sur Linux Bonjour Service de conteneur Azure

Hello  **[Spring Framework]**  est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes.

**[client Docker]**  solutions en open source qui permet aux développeurs d’automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.

Ce didacticiel vous guide à l’aide de Docker toodevelop et déployer un hôte Linux de démarrage du ressort application tooa Bonjour [Azure conteneur de Service (ACS)].

## <a name="prerequisites"></a>Composants requis

Commande toocomplete hello étapes décrites dans ce didacticiel, vous devez hello toohave suivant des conditions préalables :

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

Hello étapes suivantes vous guident étapes hello toocreate requis une application web de démarrage du ressort simple et de le tester localement.

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

1. Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans le répertoire hello créé ; par exemple :
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Changer le projet toohello terminée Active ; par exemple :
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Générer le fichier JAR hello à l’aide de Maven ; par exemple :
   ```
   mvn package
   ```

1. Une fois que l’application hello web a été créée, modifier le répertoire toohello `target` répertoire dans lequel le fichier JAR hello se trouve et démarrer l’application web hello ; par exemple :
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Tester l’application web hello en parcourant tooit localement à l’aide d’un navigateur web. Par exemple, si vous avez curl disponible et vous configuré hello Tomcat server toorun sur le port 80 :
   ```
   curl http://localhost
   ```

1. Vous devez voir hello message suivant s’affiche : **Docker de Hello World !**

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Créer un toouse de Registre de conteneur Azure comme un Registre Docker privé

Hello étapes suivantes vous guident à l’aide de hello toocreate portail Azure un Registre de conteneur Azure.

> [!NOTE]
>
> Si vous souhaitez toouse hello CLI d’Azure au lieu de hello portail Azure, suivez les étapes de hello dans [créer un Registre de conteneur Docker privé à l’aide de hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Parcourir toohello [portail Azure] et connectez-vous.

   Une fois que vous avez connecté compte tooyour sur hello portail Azure, vous pouvez suivre les étapes de hello Bonjour [créer un Registre de conteneur Docker privé à l’aide de hello portail Azure] article, qui sont paraphrase Bonjour comme suit pour hello exploration d’opportunité.

1. Cliquez sur icône du menu hello pour **+ nouveau**, puis cliquez sur **conteneurs**, puis cliquez sur **Registre de conteneur Azure**.
   
   ![Créer un registre de conteneurs Azure][AR01]

1. Lorsque la page d’informations hello pour le modèle de Registre de conteneur Azure hello s’affiche, cliquez sur **créer**. 

   ![Créer un registre de conteneurs Azure][AR02]

1. Hello lorsque **Registre de conteneur créer** page s’affiche, entrez votre **nom de Registre** et **groupe de ressources**, choisissez **activer** pour Hello **utilisateur Admin**, puis cliquez sur **créer**.

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. Une fois votre Registre de conteneur a été créé, accédez de Registre de conteneur tooyour Bonjour portail Azure, puis cliquez sur **clés d’accès**. Prenez note du nom d’utilisateur hello et un mot de passe pour les étapes suivantes de hello.

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Configurer Maven toouse vos clés d’accès de Registre de conteneur Azure

1. Parcourir le répertoire de configuration toohello pour votre installation Maven et ouvrez hello *settings.xml* fichier avec un éditeur de texte.

1. Ajouter des paramètres du Registre de conteneur Azure d’accès à partir de la section précédente de hello de ce didacticiel toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Accédez répertoire du projet pour votre application de démarrage du ressort, toohello terminée (par exemple : «*C:\SpringBoot\gs-spring-boot-docker\complete*« ou »*/users/robert/SpringBoot/gs-spring-boot-docker / complète*») et ouvrez hello *pom.xml* fichier avec un éditeur de texte.

1. Hello de mise à jour `<properties>` collection Bonjour *pom.xml* fichier avec la valeur hello du serveur de connexion pour votre Registre de conteneur Azure à partir de la section précédente de hello de ce didacticiel ; par exemple :

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Hello de mise à jour `<plugins>` collection Bonjour *pom.xml* de fichiers afin que hello `<plugin>` contient hello adresse et du Registre nom du serveur pour votre Registre de conteneur Azure à partir de la section précédente de hello de ce didacticiel. Par exemple :

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

1. Accédez répertoire du projet pour votre application de démarrage du ressort toohello s’est terminée et exécutez hello après application de commande toorebuild hello push hello conteneur tooyour Registre de conteneur Azure :

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Lorsque vous transmettez vos tooAzure de conteneur Docker, vous pouvez recevoir un message d’erreur est similaire tooone de hello suivant même si votre conteneur Docker a été créé avec succès :
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Dans ce cas, vous devrez peut-être toosign dans tooyour compte Azure à partir de la ligne de commande Docker hello ; par exemple :
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Vous pouvez ensuite distribuer votre conteneur à partir de la ligne de commande hello ; par exemple :
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Créer une application web sur Linux sur Azure App Service en utilisant votre image de conteneur

1. Parcourir toohello [portail Azure] et connectez-vous.

1. Cliquez sur icône du menu hello pour **+ nouveau**, puis cliquez sur **Web + Mobile**, puis cliquez sur **l’application Web sur Linux**.
   
   ![Créer une application web Bonjour portail Azure][LX01]

1. Hello lorsque **l’application Web sur Linux** page s’affiche, entrez hello informations suivantes :

   a. Entrez un nom unique pour hello **nom de l’application**; par exemple : «*wingtiptoyslinux*. »

   b. Choisissez votre **abonnement** à partir de la liste déroulante de hello.

   c. Sélectionnez un existant **groupe de ressources**, ou spécifiez un nom de toocreate un groupe de ressources.

   d. Cliquez sur **configurer conteneur** et entrez hello informations suivantes :

      * Choisissez **Registre privé**.

      * **Image et étiquette facultative** : spécifiez le nom de votre conteneur utilisé plus haut, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* »

      * **URL du serveur**: spécifiez l’URL du registre déclaré plus haut, par exemple : « *https://wingtiptoysregistry.azurecr.io* »

      * **Nom d’utilisateur de connexion** et **Mot de passe** : spécifiez vos informations d’identification de connexion des **clés d’accès** que vous avez utilisées dans les étapes précédentes.
   
   e. Une fois que vous avez entré toutes hello au-dessus des informations, cliquez sur **OK**.

   ![Configurer les paramètres de l’application web][LX02]

1. Cliquez sur **Créer**.

> [!NOTE]
>
> Azure mappera automatiquement serveur Internet demandes tooembedded Tomcat qui s’exécute sur des ports standard hello de 80 ou 8080. Toutefois, si vous avez configuré votre toorun du serveur Tomcat incorporée sur un port personnalisé, vous devez tooadd une application web de variable tooyour environnement qui définit le port hello pour votre serveur Tomcat incorporé. toodo utilisez donc hello comme suit :
>
> 1. Parcourir toohello [portail Azure] et connectez-vous.
> 
> 2. Cliquez sur icône hello **des Services d’application**. (Consultez l’article #1 dans l’image hello ci-dessous.)
>
> 3. Sélectionnez votre application web à partir de la liste de hello. (Élément #2 dans l’image hello ci-dessous).
>
> 4. Cliquez sur **Paramètres de l’application**. (Élément #3 dans l’image hello ci-dessous).
>
> 5. Bonjour **paramètres de l’application** section, ajoutez une nouvelle variable d’environnement nommée **PORT** et entrez votre numéro de port personnalisé pour la valeur de hello. (Élément #4 dans l’image hello ci-dessous).
>
> 6. Cliquez sur **Enregistrer**. (Article #5 image hello ci-dessous.)
>
> ![L’enregistrement d’un numéro de port personnalisé Bonjour portail Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :

* [Déployer un toohello ressort démarrage Application Azure App Service](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Déployer une Application de démarrage ressort sur un Kubernetes Cluster Bonjour Service de conteneur Azure](container-service-deploy-spring-boot-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur hello ressort démarrage sur l’exemple de projet Docker, consultez [démarrage ressort sur Docker mise en route].

Pour avec prise en main de vos propres applications ressort démarrage, consultez hello **ressort Initializr** à https://start.spring.io/.

Pour plus d’informations sur la prise en main de la création d’une application de démarrage du ressort simple, consultez hello ressort Initializr à https://start.spring.io/.

Pour obtenir des exemples supplémentaires pour comment toouse personnalisé Docker images avec Azure, consultez [à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux].

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure conteneur de Service (ACS)]: https://azure.microsoft.com/services/container-service/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[créer un Registre de conteneur Docker privé à l’aide de hello portail Azure]: /azure/container-registry/container-registry-get-started-portal
[à l’aide d’une image Docker personnalisée pour l’application Web Azure sous Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
