---
title: "aaaHow toouse hello Maven du plug-in pour les applications Web Azure toodeploy un tooAzure d’application de démarrage du ressort"
description: "Découvrez comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application de démarrage du ressort."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application de démarrage du ressort

Hello [Maven les plug-in pour les applications Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) pour [Apache Maven](http://maven.apache.org/) permet une intégration transparente du Service d’application Azure dans des projets Maven et simplifie les processus hello pour les développeurs toodeploy web apps tooAzure du Service d’applications.

Cet article montre comment utiliser hello plug-in Maven pour les applications Web Azure toodeploy un tooAzure d’application exemple ressort démarrage des Services d’application.

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

## <a name="clone-hello-sample-spring-boot-web-app"></a>Clone hello exemple ressort démarrage d’application web

Dans cette section, vous clonez une application Spring Boot terminée et vous la testez localement.

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

1. Hello du clone [ressort démarrage prise en main] exemple de projet dans le répertoire hello créé ; par exemple :
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Changer le projet toohello terminée Active ; par exemple :
   ```shell
   cd gs-spring-boot/complete
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

1. Vous devez voir hello message suivant s’affiche : **Greetings de démarrage du ressort !**

## <a name="create-an-azure-service-principal"></a>Créer un principal du service Azure

Dans cette section, vous créez Azure principal du service qui hello utilise de plug-in Maven lors du déploiement de votre tooAzure d’application web.

1. Ouvrez une invite de commandes.

1. Connectez-vous à votre compte Azure à l’aide de hello CLI d’Azure :
   ```shell
   az login
   ```
   Suivez hello instructions toocomplete hello processus de connexion.

1. Créez un principal du service Azure :
   ```shell
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
   > Vous allez utiliser les valeurs hello à partir de cette réponse JSON lorsque vous configurez hello Maven plug-in toodeploy votre tooAzure d’application web. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, et `tttttttt` sont des valeurs d’espace réservé, qui sont utilisées dans cet exemple toomake toomap plus facilement ces éléments de tootheir respectifs valeurs lorsque vous configurez votre Maven `settings.xml` fichier ensuite Bonjour section.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Configurer Maven toouse votre principal de service Azure

Dans cette section, vous utilisez les valeurs hello dans votre service Azure principal tooconfigure hello de l’authentification par Maven lors du déploiement de votre tooAzure d’application web.

1. Ouvrez votre Maven `settings.xml` de fichiers dans un éditeur de texte ; ce fichier peut être dans un chemin d’accès comme hello exemple suivant :
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Ajoutez vos paramètres de principal du service Azure à partir de la section précédente de hello de ce didacticiel toohello `<servers>` collection Bonjour *settings.xml* fichier ; par exemple :

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

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>FACULTATIF : Personnaliser votre pom.xml avant de déployer votre tooAzure d’application web

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
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in de hello Maven et une description détaillée de chacun de ces éléments est disponible dans hello [Maven les plug-in pour les applications Web Azure] documentation. Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :

Élément | Description
---|---|---
`<version>` | Spécifie la version de hello de hello [Maven les plug-in pour les applications Web Azure]. Vous devez vérifier la version de hello répertoriée dans hello [référentiel Central Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que vous utilisez hello version la plus récente.
`<authentication>` | Spécifie les informations d’authentification hello pour Azure, qui dans cet exemple contient un `<serverId>` élément contenant `azure-auth`; Maven utilise ce toolook valeur des valeurs de principal de service Azure hello dans votre Maven *settings.xml* fichier que vous avez définie dans une section précédente de cet article.
`<resourceGroup>` | Spécifie le groupe de ressources cible hello, qui est `maven-plugin` dans cet exemple. groupe de ressources Hello est créé au cours du déploiement, si elle n’existe pas déjà.
`<appName>` | Spécifie le nom de la cible hello pour votre application web. Dans cet exemple, le nom de la cible hello est `maven-web-app-${maven.build.timestamp}`, où hello `${maven.build.timestamp}` suffixe est ajouté dans ce conflit de tooavoid exemple. (vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application hello ; hello timestamp est facultative.)
`<region>` | Spécifie la région cible hello, qui, dans cet exemple est `westus`. (Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)
`<javaVersion>` | Spécifie la version du runtime Java hello pour votre application web. (Une liste complète est Bonjour [Maven les plug-in pour les applications Web Azure] documentation.)
`<deploymentType>` | Spécifie le type de déploiement de votre application web. Pour l’instant, seul `ftp` est pris en charge, bien que la prise en charge d’autres types de déploiement soit en cours de développement.
`<resources>` | Spécifie les ressources et les destinations de cibles qui Maven utilise lors du déploiement de votre tooAzure d’application web. Dans cet exemple, deux `<resource>` éléments spécifient que Maven déploient des fichiers JAR de hello pour votre application web et le hello *web.config* fichier de projet de démarrage du ressort hello.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Générer et déployer votre tooAzure d’application web

Une fois que vous avez configuré tous les paramètres de hello Bonjour précédant les sections de cet article, vous êtes prêt toodeploy votre tooAzure d’application web. toodo utilisez donc hello comme suit :

1. À partir d’invite de commandes hello ou fenêtre de Terminal Server que vous utilisiez précédemment, régénérez le fichier JAR hello à l’aide de Maven si vous avez apporté les modifications de toohello *pom.xml* fichier ; par exemple :
   ```shell
   mvn clean package
   ```

1. Déployer votre tooAzure d’application web à l’aide de Maven ; par exemple :
   ```shell
   mvn azure-webapp:deploy
   ```

Maven déploierez votre tooAzure d’application web ; Si l’application hello web n’existe pas déjà, il sera créé.

Lorsque votre site web a été déployée, vous serez en mesure de toomanage à l’aide de hello [portail Azure].

* Votre application web s’affichera dans **App Services** :

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* Et hello URL pour votre application web s’afficheront dans hello **vue d’ensemble** pour votre application web :

   ![Détermination des URL hello pour votre application web][AP02]

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

Pour plus d’informations sur hello diverses technologies abordées dans cet article, consultez hello suivant des articles :

* [Maven les plug-in pour les applications Web Azure]

* [Connectez-vous à tooAzure de hello CLI d’Azure](/azure/xplat-cli-connect)

* [Comment toouse hello plug-in Maven pour les applications Web Azure toodeploy, un tooAzure d’application ressort démarrage en conteneur](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Référence des paramètres Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Interface de ligne de commande (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[ressort démarrage prise en main]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven les plug-in pour les applications Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
