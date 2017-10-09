---
title: "aaaDeploy un toohello d’Application de démarrage du ressort du Service d’applications Azure | Documents Microsoft"
description: "Ce didacticiel vous guide les développeurs via hello étapes toodeploy hello ressort démarrage route web application tooAzure du Service d’applications."
services: app-service\web
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
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Déployer un toohello ressort démarrage Application Azure App Service

Hello  **[Spring Framework]**  une solution open source qui permet aux développeurs Java de créer des applications d’entreprise, et l’autre des projets courants de plus de hello qui s’appuie sur cette plateforme [Ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonomes.

Ce didacticiel vous aidera à cependant création exemple hello ressort démarrage prise en main d’application web et les déployer trop[Azure App Service].

### <a name="prerequisites"></a>Composants requis

Dans l’ordre toocomplete hello étapes décrites dans ce didacticiel, vous toohave hello éléments suivants sont nécessaires :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un [JDK (Java Developer Kit)] à jour.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [client Git].

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Créer hello ressort démarrage prise en main de l’application web

Hello étapes suivantes vous guidera à travers les étapes de hello toocreate requis une application web de démarrage du ressort simple et de le tester localement.

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

1. Hello du clone [ressort démarrage prise en main] exemple de projet dans l’annuaire hello vous venez de créer ; par exemple :
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Changer le projet toohello terminée Active ; par exemple :
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Générer le fichier JAR hello à l’aide de Maven ; par exemple :
   ```
   mvn package
   ```

1. Une fois que l’application hello web a été créée, modifiez le fichier JAR de toohello active et démarrer l’application hello web ; par exemple :
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Tester l’application web hello en parcourant toohttp://localhost:8080 à l’aide d’un navigateur web, ou utilisez la syntaxe hello comme hello l’exemple suivant, si vous avez curl disponible :
   ```
   curl http://localhost:8080
   ```

1. Vous devez voir hello message suivant s’affiche : **Greetings de démarrage du ressort !**

   ![Parcourir l’exemple d’application][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Créer une application web Azure à utiliser avec Java

Hello suit sera vous guident tout hello étapes toocreate une application Web Azure, configurer les paramètres requis de hello pour Java et configurer vos informations d’identification FTP.

1. Parcourir toohello [portail Azure] et connectez-vous.

1. Une fois que vous êtes connecté à votre compte sur hello portail Azure, cliquez sur icône du menu hello pour **des Services d’application**:
   
   ![Portail Azure][AZ01]

1. Hello lorsque **des Services d’application** page s’affiche, cliquez sur **+ ajouter** toocreate un nouveau Service d’application.

   ![Créer un App Service][AZ02]

1. Lors de la liste de hello des modèles d’application web s’affiche, cliquez sur lien hello hello base l’application Web Microsoft.

   ![Modèles d’application web][AZ03]

1. Lorsque la page d’informations hello pour le modèle d’application Web hello s’affiche, cliquez sur **créer**.

   ![Créer une application web][AZ04]

1. Indiquez un nom unique pour votre application web et spécifiez les éventuels paramètres supplémentaires, puis cliquez sur **Créer**.

   ![Créer les paramètres d’une application web][AZ05]

1. Une fois que votre application web a été créée, cliquez sur icône du menu hello pour **des Services d’application**, puis cliquez sur votre application web de nouvellement créé :

   ![Répertorier les applications web][AZ06]

1. Lorsque votre application web s’affiche, spécifiez une version Java hello à l’aide de hello comme suit :

   a. Cliquez sur hello **paramètres de l’Application** élément de menu.

   b. Choisissez **Java 8** pour une version Java hello.

   c. Choisissez **plus récent** pour la version de Java secondaire hello.

   d. Choisissez **les plus récents Tomcat 8.5** pour le conteneur de hello web. (Ce conteneur n'est pas réellement utilisé ; Azure utilise conteneur hello à partir de votre application de démarrage du ressort.)

   e. Cliquez sur **Save**.

   ![Paramètres de l’application][AZ07]

1. Spécifier vos informations d’identification de déploiement FTP à l’aide de hello comme suit :

   a. Cliquez sur hello **informations d’identification de déploiement** élément de menu.

   b. Spécifiez votre nom d’utilisateur et votre mot de passe.

   c. Cliquez sur **Save**.

   ![Spécifier les informations d’identification de déploiement][AZ08]

1. Récupérer les informations de connexion FTP à l’aide de hello comme suit :

   a. Cliquez sur hello **informations d’identification de déploiement** élément de menu.

   b. Copiez vos nom d’utilisateur complet de FTP et les URL et les enregistrer pour la section suivante de hello de ce didacticiel.

   ![URL et informations d’identification FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Déployer votre tooAzure d’application de web ressort démarrage

Hello suit vous guidera hello étapes toodeploy votre tooAzure d’application de web ressort démarrage.

1. Ouvrez un éditeur de texte tel que le bloc-notes de Windows et collez hello après le texte dans un nouveau document, puis enregistrer le fichier hello sous *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Après avoir enregistré hello *web.config* tooyour système de fichiers, connecter tooyour l’application web via FTP à l’aide des URL de hello, nom d’utilisateur et mot de passe de hello précédant la section de ce didacticiel. Par exemple :
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Modification hello répertoire distant toohello dossier racine de votre application web, (qui est à */site/wwwroot*), puis copiez le fichier JAR hello à partir de votre application de démarrage du ressort et hello *web.config* précédemment. Par exemple :
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Après avoir déployé votre JAR et *web.config* fichiers tooyour web app, vous devez toorestart votre application web à l’aide de hello portail Azure :

   ![][AZ10]

1. Tester l’application web hello en parcourant les URL de l’application tooyour web à l’aide d’un navigateur web, ou utilisez la syntaxe hello comme hello l’exemple suivant, si vous avez curl disponible :
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Vous devez voir hello message suivant s’affiche : **Greetings de démarrage du ressort !**

   ![Parcourir l’exemple d’application][SB02]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation des applications de démarrage du ressort sur Azure, consultez hello suivant des articles :

* [Déployer une Application de démarrage ressort sur Linux Bonjour Service de conteneur Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Déployer une Application de démarrage ressort sur un Kubernetes Cluster Bonjour Service de conteneur Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur les tooAzure d’applications web depoying à l’aide de FTP, consultez [déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S].

Pour plus d’informations sur l’exemple de projet de démarrage du ressort hello, consultez [ressort démarrage prise en main].

Pour avec prise en main de vos propres applications ressort démarrage, consultez hello **ressort Initializr** à https://start.spring.io/.

Pour plus d’informations sur la configuration de paramètres supplémentaires pour votre application web, consultez [Configurer des applications web dans Azure App Service].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Configurer des applications web dans Azure App Service]: /azure/app-service-web/web-sites-configure
[déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Ressort démarrage]: http://projects.spring.io/spring-boot/
[ressort démarrage prise en main]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
