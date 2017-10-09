---
title: "une application web Azure de base à l’aide d’aaaCreate Eclipse | Documents Microsoft"
description: "Ce didacticiel vous montre comment toouse hello boîte à outils Azure pour Eclipse toocreate, une application de Web Hello World pour Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Créer une application web Azure de base à l’aide d’Eclipse
Ce didacticiel montre comment toocreate et déployer une base tooAzure d’application Hello World comme une application Web à l’aide de hello [boîte à outils Azure pour Eclipse]. Un exemple JSP de base est présenté par souci de simplicité, mais des étapes similaires conviennent également pour un servlet Java en ce qui concerne le déploiement d’Azure.

Lorsque vous avez terminé ce didacticiel, votre application doit ressembler similaire toohello suivant illustration lorsque vous l’affichez dans un navigateur web :

![Version préliminaire de l’application Hello World][01]

## <a name="prerequisites"></a>Composants requis
* JDK (Java Development Kit) version 1.8 ou ultérieure.
* IDE (environnement de développement intégré) Eclipse pour développeurs Java EE, Luna ou ultérieur. Vous pouvez le télécharger à l’adresse suivante : <http://www.eclipse.org/downloads/>.
* Une distribution d’un serveur web ou d’un serveur d’applications basé sur Java, comme [Apache Tomcat] ou [Jetty].
* Un abonnement Azure, qui peut être obtenu à l’adresse <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello [boîte à outils Azure pour Eclipse]. Pour plus d’informations sur l’installation hello boîte à outils Azure, consultez [installation hello boîte à outils Azure pour Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate une application Hello World
Tout d’abord, nous allons commencer par créer un projet Java.

1. Démarrez Eclipse et au menu de hello cliquez sur **fichier**, cliquez sur **nouveau**, puis cliquez sur **projet Web dynamique**. (Si vous ne voyez pas **projet Web dynamique** répertorié comme un projet disponible après avoir cliqué sur **fichier** et **nouveau**, puis hello suivant : cliquez sur **fichier**, cliquez sur **nouveau**, cliquez sur **projet...** , développez **Web**, cliquez sur **projet Web dynamique**, puis cliquez sur **suivant**.)
2. Pour des raisons de ce didacticiel, nommez le projet de hello **MyWebApp**. Votre écran apparaîtra similaire toohello suivantes :
   
    ![Création d’un nouveau projet Web dynamique][02]
3. Cliquez sur **Terminer**.
4. Dans la vue Explorateur de projets d’Eclipse, développez **MyWebApp**. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.
5. Bonjour **nouveau fichier JSP** boîte de dialogue, le nom de fichier hello **index.jsp**, conservez le dossier parent hello **MyWebApp/WebContent**, puis cliquez sur **suivant**.
6. Bonjour **sélectionner un modèle JSP** boîte de dialogue, pour les besoins de ce didacticiel, sélectionnez **nouveau fichier JSP (html)**, puis cliquez sur **Terminer**.
7. Lorsque votre fichier index.jsp s’ouvre dans Eclipse, ajoutez dans l’affichage du texte toodynamically **Hello World !** dans hello existant `<body>` élément. Votre mise à jour `<body>` contenu doit ressembler à hello l’exemple suivant :
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Enregistrez index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy votre tooan application conteneur d’application Web Azure
Il existe plusieurs façons par lequel vous pouvez déployer un tooAzure d’application web Java. Ce didacticiel décrit l’une de hello plus simple : votre application sera déployée tooan conteneur d’application Web Azure - aucun type de projet spécial ni les outils supplémentaires ne sont nécessaires. Hello JDK et hello web conteneur logiciel sera fourni pour vous par Azure, il est donc aucune tooupload besoin de votre propre ; Il vous suffit de votre application de Web Java. Par conséquent, les processus de publication hello pour votre application prendra secondes, pas les minutes.

1. Dans l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur **MyWebApp**.
2. Dans le menu contextuel de hello, sélectionnez **Azure**, puis cliquez sur **publier en tant qu’application Web Azure...**
   
    ![Publish as Azure Web App][03]
   
    Pendant que votre projet d’application web est sélectionnée dans l’Explorateur de projets de hello, vous pouvez également cliquer hello **publier** bouton de liste déroulante sur la barre d’outils hello et sélectionnez **publier en tant qu’application Web Azure** à partir de là :
   
    ![Publish as Azure Web App][14]
3. Si vous n’êtes pas déjà inscrit dans Azure à partir d’Eclipse, vous serez invité à toosign à votre compte Azure :
   
    ![Boîte de dialogue Connexion à Azure][04]
   
    Si vous avez plusieurs comptes Azure, certaines des invites hello pendant hello connectez-vous processus peut s’afficher plusieurs fois, même si elles apparaissent toobe hello identiques. Dans ce cas, continuez suivant hello des instructions de connexion.
4. Une fois que vous êtes connecté à votre compte Azure, hello **gérer les abonnements** boîte de dialogue affiche une liste des abonnements qui sont associés à vos informations d’identification. S’il existe plusieurs abonnements répertoriés et vous souhaitez toowork avec seulement un sous-ensemble spécifique, vous pouvez éventuellement désactiver hello ceux que vous ne souhaitez pas que toouse. Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.
   
    ![Boîte de dialogue Gestion des abonnements][05]
5. Hello lorsque **tooAzure conteneur d’application Web de déployer** boîte de dialogue s’affiche, elle affiche tous les conteneurs de l’application Web que vous avez créé précédemment ; si vous n’avez pas créé tous les conteneurs, liste de hello sera vide.
   
    ![Déployer la boîte de dialogue tooAzure conteneur d’application Web][06]
6. Si vous n’avez créé un conteneur d’application Web Azure avant ou si vous souhaitez que toopublish votre conteneur tooa application, utilisez hello comme suit. Sinon, sélectionnez un conteneur d’application Web existant et ignorer toostep 7 ci-dessous.
   
   1. Cliquez sur **New...**
      
       ![Déployer la boîte de dialogue tooAzure conteneur d’application Web][15]
   2. Hello **nouveau conteneur d’application Web** boîte de dialogue s’affiche :
      
       ![Boîte de dialogue Nouveau conteneur d’application web][07a]
   3. Entrez un **nom DNS** pour votre conteneur d’application Web ; Ceci va former le nom DNS hello feuille de l’URL de l’hôte hello pour votre application web dans Azure. (Notez que nom hello doit être disponible et se conformer exigences d’affectation de noms de l’application Web tooAzure.)
   4. Bonjour **Web conteneur** menu déroulant, logiciel approprié de hello Sélectionnez pour votre application.
      
       Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9. Une distribution récente du logiciel de hello sélectionné sera fournie par Azure, et elle s’exécute sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.
   5. Bonjour **abonnement** menu déroulant, sélectionnez hello abonnement toouse pour ce déploiement.
   6. Bonjour **groupe de ressources** menu déroulant, sélectionnez hello groupe de ressources avec laquelle vous souhaitez tooassociate votre application Web. (Les groupes de Ressources azure permet de vous toogroup les ressources associées ensemble afin que, par exemple, ils peuvent être supprimés ensemble.)
      
       Vous pouvez sélectionner un groupe de ressources existant (si vous en avez) et skip g de toostep ci-dessous ou hello utilisation suivant ces étapes toocreate un groupe de ressources :
      
      * Cliquez sur **New...**
      * Hello **nouveau groupe de ressources** boîte de dialogue s’affiche :
        
          ![Boîte de dialogue Nouveau groupe de ressources][08]
      * Bonjour de hello **nom** zone de texte, spécifiez un nom pour votre nouveau groupe de ressources.
      * Bonjour de hello **région** menu déroulant, emplacement pour votre groupe de ressources de centre de données Azure approprié de hello select.
      * FACULTATIF : Par défaut, une distribution récente de Java 8 est déployée par Azure automatiquement conteneur d’application web tooyour en tant que votre machine virtuelle Java. Toutefois, vous pouvez spécifier une version différente et la distribution de hello JVM si votre application Web est nécessaire. toospecify hello JDK pour votre application Web, cliquez sur hello **JDK** et sélectionnez une des options suivantes de hello :
        
        * **Déployer la valeur par défaut de hello JDK offerte par le service d’applications Web Azure**: cette option déploiera une distribution récente de Java 8.
        * **Déployer le JDK disponible sur Azure 3e partie**: cette option vous permet de toochoose à partir de la liste de hello de JDK qui sont fournies par Microsoft Azure.
        * **Déployer mon propre JDK à partir de cet emplacement de téléchargement**: cette option vous permet de toospecify votre propre distribution JDK, qui doit être empaquetée comme un fichier .zip et téléchargé tooeither un emplacement de téléchargement disponible publiquement ou un stockage Azure de compte pour lequel vous avoir accès.
          
          ![Boîte de dialogue Nouveau conteneur d’application web][07b]
   7. Cliquez sur **OK**.
   8. Hello **du Plan App Service** menu déroulant répertorie les plans de service d’application hello associés hello groupe de ressources que vous avez sélectionné. (Les Plans app Service spécifient les informations comme emplacement de hello de votre application Web, hello niveau tarifaire et taille d’instance de calcul hello. Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)
      
       Vous pouvez sélectionner un Plan de Service application existant (si vous en avez) et ignorer h toostep ci-dessous ou utilisez hello suivant ces toocreate étapes un nouveau Plan App Service :
      
      * Cliquez sur **New...**
      * Hello **nouveau du Plan App Service** boîte de dialogue s’affiche :
        
          ![Boîte de dialogue Nouveau plan App Service][09]
      * Bonjour de hello **nom** zone de texte, spécifiez un nom pour votre nouveau Plan App Service.
      * Bonjour de hello **emplacement** menu déroulant, emplacement pour le plan de hello centre de données Azure approprié de hello select.
      * Bonjour de hello **niveau tarifaire** menu déroulant, sélectionnez hello approprié de tarification pour le plan de hello. À des fins de test, vous pouvez choisir **Free**(Gratuit).
      * Bonjour de hello **taille de l’Instance** menu déroulant, taille de l’instance appropriée sélectionnez hello pour le plan de hello. À des fins de test, vous pouvez choisir **Small**(Petite).
   9. Une fois que vous avez effectué toutes les hello étapes ci-dessus, boîte de dialogue nouveau conteneur d’application Web hello doit ressembler à hello après l’illustration :
      
       ![Boîte de dialogue Nouveau conteneur d’application web][10]
   10. Cliquez sur **OK** création de hello toocomplete de votre conteneur d’application Web.
       
        Attendez quelques secondes pour la liste de hello Web App conteneurs toobe hello actualisé, et votre conteneur d’application web de nouvellement créé doit maintenant être sélectionné dans la liste de hello.
7. Vous êtes maintenant déploiement initial de hello prêt toocomplete de tooAzure de votre application Web :
   
    ![Déployer la boîte de dialogue tooAzure conteneur d’application Web][11]
   
    Cliquez sur **OK** toodeploy votre toohello d’application Java sélectionné conteneur de l’application Web.
   
    Par défaut, votre application sera déployée en tant que sous-répertoire hello du serveur d’applications. Si vous voulez qu’elle toobe déployé en tant qu’application de racine hello, vérifiez hello **déployer tooroot** case à cocher avant de cliquer sur **OK**.
8. Ensuite, vous devez voir hello **journal des activités Azure** vue, ce qui indique l’état du déploiement de votre application Web hello.
   
    ![Journaux d’activité][12]
   
    Hello du déploiement de votre application Web de tooAzure doit durer quelques secondes seulement toocomplete. Lorsque vous êtes prêt application, vous verrez un lien nommé **publié** Bonjour **état** colonne. Lorsque vous cliquez sur le lien de hello, il vous prendra page d’accueil de l’application Web de tooyour déployé.

## <a name="updating-your-web-app"></a>Mise à jour de votre application web
La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :

* Vous pouvez mettre à jour le déploiement hello d’une application de Web Java existante.
* Vous pouvez publier un toohello d’application Java supplémentaire même conteneur d’application Web.

Dans les deux cas, les processus hello sont identique et ne prend que quelques secondes :

1. Dans l’Explorateur de projets Eclipse hello, cliquez sur l’application Java hello que vous souhaitez tooupdate ou que vous ajoutez tooan existant de conteneur d’application Web.
2. Menu contextuel de hello, sélectionnez **Azure** , puis **publier en tant qu’application Web Azure...**
3. Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît. Sélectionnez hello un choix toopublish ou de publier votre Java application tooand, cliquez à nouveau **OK**.

Quelques secondes plus tard, hello **journal des activités Azure** vue affiche votre déploiement de mises à jour en tant que **publié** et vous sera en mesure de tooverify votre application mis à jour dans un navigateur web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Démarrage, arrêt ou redémarrage d’une application web existante
toostart ou arrêter un conteneur d’application Web Azure existant, (y compris toutes les applications de Java hello déployé qu’elle contient), vous pouvez utiliser des hello **Explorateur Azure** vue.

Si hello **Explorateur Azure** affichage n’est pas déjà ouvert, vous pouvez l’ouvrir en cliquant sur ensuite **fenêtre** menu d’Eclipse, puis cliquez sur **afficher la vue**, puis **autres...** , puis **Azure**, puis cliquez sur **Explorateur Azure**. Si vous n’avez pas précédemment connecté, il vous invite toodo donc.

Hello lorsque **Explorateur Azure** s’affiche, utilisez, suivez ces étapes toostart ou arrêter votre application Web : 

1. Développez hello **Azure** nœud.
2. Développez hello **Web Apps** nœud. 
3. Avec le bouton hello souhaité application Web.
4. Lorsque le menu contextuel de hello s’affiche, cliquez sur **Démarrer**, **arrêter**, ou **redémarrer**. Notez que les options de menu hello sont sensibles au contexte, donc vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.
   
    ![Arrêt d’une application web existante][13]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :

* [boîte à outils Azure pour Eclipse]
  * [installation hello boîte à outils Azure pour Eclipse]
  * *Créer une application web « Hello World » pour Azure dans Eclipse (cet article)*
  * [Nouveautés dans hello boîte à outils Azure pour Eclipse]
* [Kit de ressources Azure pour IntelliJ]
  * [Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]
  * [Créer une application web « Hello World » pour Azure dans IntelliJ]
  * [Nouveautés dans hello Azure Toolkit pour IntelliJ]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].

Pour plus d’informations sur la création d’applications Web Azure, consultez hello [vue d’ensemble des applications Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[installation hello boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nouveautés dans hello boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nouveautés dans hello Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[vue d’ensemble des applications Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
