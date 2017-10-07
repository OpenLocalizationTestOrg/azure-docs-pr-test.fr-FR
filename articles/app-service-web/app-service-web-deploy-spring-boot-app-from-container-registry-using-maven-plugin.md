---
title: "aaaHow toouse hello Maven du plug-in pour les applications Web Azure toodeploy une application de démarrage du ressort dans le Registre de conteneur Azure tooAzure du Service d’applications"
description: "Ce didacticiel vous guidera cependant hello étapes toodeploy une application de démarrage du ressort dans le Registre de conteneur Azure tooAzure tooAzure du Service d’applications à l’aide d’un plug-in Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, une application de démarrage du ressort dans le Registre de conteneur Azure tooAzure du Service d’applications

Hello  **[Spring Framework]**  est une infrastructure open source populaire qui permet aux développeurs Java de créer des applications web, mobiles et API. Ce didacticiel utilise un exemple d’application créé à l’aide de [ressort démarrage], une approche pilotée par convention pour l’utilisation du ressort tooget démarrer rapidement.

Cet article explique comment toodeploy un tooAzure d’application exemple ressort démarrage Registre de conteneur, puis utiliser hello plug-in Maven pour les applications Web Azure toodeploy votre tooAzure d’application du Service d’applications.

> [!NOTE]
>
> Hello Maven les plug-in pour les applications Web Azure est actuellement disponible en version préliminaire. Pour l’instant, seule la publication FTP est pris en charge, bien que des fonctionnalités supplémentaires qui vont hello futures.
>

## <a name="prerequisites"></a>Composants requis

Commande toocomplete hello étapes décrites dans ce didacticiel, vous devez hello toohave suivant des conditions préalables :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Hello [Azure Interface de ligne de commande (CLI)].
* Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [client Git].
* Un [client Docker].

> [!NOTE]
>
> En raison des exigences de la virtualisation toohello de ce didacticiel, vous ne peut pas suivre les étapes de hello dans cet article sur un ordinateur virtuel ; Vous devez utiliser un ordinateur physique avec les fonctionnalités de virtualisation activées.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Cloner l’exemple hello ressort démarrage sur l’application web de Docker

Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.

1. Ouvrez une invite de commandes ou d’une fenêtre de terminal et créer un répertoire local de toohold votre application de démarrage du ressort et remplacez le répertoire toothat ; par exemple :
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hello du clone [démarrage ressort sur Docker mise en route] exemple de projet dans le répertoire hello créé ; par exemple :
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. Changer le projet toohello terminée Active ; par exemple :
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Générer le fichier JAR hello à l’aide de Maven ; par exemple :
   ```shell
   mvn clean package
   ```

1. Lorsque l’application hello web a été créée, démarrer l’application hello web à l’aide de Maven ; par exemple :
   ```shell
   mvn spring-boot:run
   ```

1. Tester l’application web hello en parcourant tooit localement à l’aide d’un navigateur web. Par exemple, vous pouvez utiliser hello commande suivante si vous avez curl disponible :
   ```shell
   curl http://localhost:8080
   ```

1. Vous devez voir hello message suivant s’affiche : **Hello World de Docker**

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-service-principal"></a>Créer un principal du service Azure

Dans cette section, vous créez Azure principal du service qui hello utilise de plug-in Maven lors du déploiement de votre tooAzure de conteneur.

1. Ouvrez une invite de commandes.

1. Connectez-vous à votre compte Azure à l’aide de hello CLI d’Azure :
   ```azurecli
   az login
   ```
   Suivez hello instructions toocomplete hello processus de connexion.

1. Créez un principal du service Azure :
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Où `uuuuuuuu` est le nom d’utilisateur hello et `pppppppp` hello de mot de passe de principal du service hello.

1. Azure répond avec JSON qui ressemble à hello l’exemple suivant :
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Vous allez utiliser les valeurs de hello à partir de cette réponse JSON lorsque vous configurez hello Maven plug-in toodeploy tooAzure de votre conteneur. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, et `tttttttt` sont des valeurs d’espace réservé, qui sont utilisées dans cet exemple toomake toomap plus facilement ces éléments de tootheir respectifs valeurs lorsque vous configurez votre Maven `settings.xml` fichier ensuite Bonjour section.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Créer un Registre de conteneur Azure à l’aide de hello CLI d’Azure

1. Ouvrez une invite de commandes.

1. Ouvrez une session dans tooyour compte Azure :
   ```azurecli
   az login
   ```

1. Créer des ressources Azure, que vous allez utiliser un groupe de ressources pour hello dans cet article :
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Remplacez `wingtiptoysresources` dans cet exemple par un nom unique pour votre groupe de ressources.

1. Créer un Registre de conteneur Azure privée dans le groupe de ressources hello pour votre application de démarrage du ressort : 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Remplacez `wingtiptoysregistry` dans cet exemple par un nom unique pour votre registre de conteneurs.

1. Récupérer le mot de passe hello pour votre Registre de conteneur :
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure répond avec votre mot de passe ; par exemple :
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Ajouter votre Registre de conteneur Azure et les paramètres du service Azure principal tooyour Maven

1. Ouvrez votre Maven `settings.xml` de fichiers dans un éditeur de texte ; ce fichier peut être dans un chemin d’accès comme hello exemple suivant :
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Ajouter des paramètres du Registre de conteneur Azure d’accès à partir de hello précédente section de cet article de toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Où :
   Élément | Description
   ---|---|---
   `<id>` | Contient le nom hello du Registre de votre conteneur Azure privée.
   `<username>` | Contient le nom hello du Registre de votre conteneur Azure privée.
   `<password>` | Contient le mot de passe hello récupéré à la section précédente de hello de cet article.

1. Ajoutez vos paramètres de principal du service Azure à partir d’une section précédente de cet article de toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Où :
   Élément | Description
   ---|---|---
   `<id>` | Spécifie un nom unique qui Maven utilise toolook vos paramètres de sécurité lorsque vous déployez votre tooAzure d’application web.
   `<client>` | Contient hello `appId` valeur à partir de votre principal de service.
   `<tenant>` | Contient hello `tenant` valeur à partir de votre principal de service.
   `<key>` | Contient hello `password` valeur à partir de votre principal de service.
   `<environment>` | Définit l’environnement de cloud computing Azure cible hello, qui est `AZURE` dans cet exemple. (Une liste complète des environnements est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation)

1. Enregistrez et fermez hello *settings.xml* fichier.

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Générer votre Docker image de conteneur et le Registre de conteneur Azure tooyour pousser

1. Accédez répertoire du projet pour votre application de démarrage du ressort, toohello terminée (par exemple) «*C:\SpringBoot\gs-spring-boot-docker\complete*« ou »*/users/robert/SpringBoot/gs-spring-boot-docker/complete*») et ouvrez hello *pom.xml* de fichiers avec un éditeur de texte.

1. Hello de mise à jour `<properties>` collection Bonjour *pom.xml* fichier avec la valeur hello du serveur de connexion pour votre Registre de conteneur Azure à partir de la section précédente de hello de ce didacticiel ; par exemple :

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Où :
   Élément | Description
   ---|---|---
   `<azure.containerRegistry>` | Spécifie le nom hello du Registre de votre conteneur Azure privée.
   `<docker.image.prefix>` | Spécifie l’URL hello de votre Registre de conteneur Azure privée, qui est dérivé en ajoutant «. azurecr.io « nom toohello du Registre de votre conteneur privé.

1. Vérifiez que `<plugin>` pour le plug-in de Docker hello dans votre *pom.xml* fichier contient des propriétés de correct hello pour hello adresse et du Registre nom du serveur à partir de l’étape précédente de hello dans ce didacticiel. Par exemple :

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Où :
   Élément | Description
   ---|---|---
   `<serverId>` | Spécifie la propriété hello qui contient le nom de votre Registre de conteneur Azure privée.
   `<registryUrl>` | Spécifie la propriété hello qui contient l’URL de hello du Registre de votre conteneur Azure privée.

1. Accédez répertoire du projet pour votre application de démarrage du ressort toohello s’est terminée et exécutez hello après application de commande toorebuild hello push hello conteneur tooyour Registre de conteneur Azure :

   ```
   mvn package docker:build -DpushImage 
   ```

1. FACULTATIF : Parcourir toohello [portail Azure] et vérifiez qu’il existe une image de conteneur Docker nommée **gs-spring-démarrage-docker** dans le Registre de conteneur.

   ![Vérification du conteneur dans le portail Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Personnaliser votre pom.xml, puis créez et déployez votre tooAzure de conteneur

Ouvrez hello `pom.xml` de fichiers pour votre application de démarrage du ressort dans un éditeur de texte et recherchez hello `<plugin>` , élément pour `azure-webapp-maven-plugin`. Cet élément doit ressembler à hello l’exemple suivant :

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in de hello Maven et une description détaillée de chacun de ces éléments est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation. Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :

Élément | Description
---|---|---
`<version>` | Spécifie la version de hello de hello [Maven les plug-in pour les applications Web Azure]. Vous devez vérifier la version de hello répertoriée dans hello [référentiel Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que vous utilisez hello version la plus récente.
`<authentication>` | Spécifie les informations d’authentification hello pour Azure, qui dans cet exemple contient un `<serverId>` élément contenant `azure-auth`; Maven utilise ce toolook valeur des valeurs de principal de service Azure hello dans votre Maven *settings.xml* fichier que vous avez définie dans une section précédente de cet article.
`<resourceGroup>` | Spécifie le groupe de ressources cible hello, qui est `wingtiptoysresources` dans cet exemple. groupe de ressources Hello sera créé au cours du déploiement s’il n’existe pas.
`<appName>` | Spécifie le nom de la cible hello pour votre application web. Dans cet exemple, le nom de la cible hello est `maven-linux-app-${maven.build.timestamp}`, où hello `${maven.build.timestamp}` suffixe est ajouté dans ce conflit de tooavoid exemple. (vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application hello ; hello timestamp est facultative.)
`<region>` | Spécifie la région cible hello, qui, dans cet exemple est `westus`. (Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)
`<containerSettings>` | Spécifie les propriétés hello qui contiennent le nom de hello et l’URL de votre conteneur.
`<appSettings>` | Spécifie des paramètres uniques pour Maven toouse lors du déploiement de votre tooAzure d’application web. Dans cet exemple, un `<property>` élément contient une paire nom/valeur des éléments enfants qui spécifient le port hello pour votre application.

> [!NOTE]
>
> numéro de port Hello paramètres toochange hello dans cet exemple ne sont nécessaires lorsque vous modifiez le port de hello à partir de la valeur par défaut hello.
>

1. À partir d’invite de commandes hello ou fenêtre de Terminal Server que vous utilisiez précédemment, régénérez le fichier JAR hello à l’aide de Maven si vous avez apporté les modifications de toohello *pom.xml* fichier ; par exemple :
   ```shell
   mvn clean package
   ```

1. Déployer votre tooAzure d’application web à l’aide de Maven ; par exemple :
   ```shell
   mvn azure-webapp:deploy
   ```

Maven déploierez votre tooAzure d’application web ; Si l’application hello web n’existe pas déjà, il sera créé.

> [!NOTE]
>
> Si la région hello que vous spécifiez dans hello `<region>` élément de votre *pom.xml* fichier n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un toohello similaire erreur l’exemple suivant :
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Si cela se produit, vous pouvez spécifier qu'une autre région et exécutez de nouveau hello Maven commande toodeploy votre application.
>
>

Lorsque votre site web a été déployée, vous serez en mesure de toomanage à l’aide de hello [portail Azure].

* Votre application web s’affichera dans **App Services** :

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* Et hello URL pour votre application web s’afficheront dans hello **vue d’ensemble** pour votre application web :

   ![Détermination des URL hello pour votre application web][AP02]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello diverses technologies abordées dans cet article, consultez hello suivant des articles :

* [Maven les plug-in pour les applications Web Azure]

* [Connectez-vous à tooAzure de hello CLI d’Azure](/azure/xplat-cli-connect)

* [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Référence des paramètres Maven](https://maven.apache.org/settings.html)

* [Plug-in Docker pour Maven]

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Maven les plug-in pour les applications Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[Plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[ressort démarrage]: http://projects.spring.io/spring-boot/
[démarrage ressort sur Docker mise en route]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
