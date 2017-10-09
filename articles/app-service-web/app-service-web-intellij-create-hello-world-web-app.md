---
title: aaaCreate une application web Azure de base dans IntelliJ | Documents Microsoft
description: "Ce didacticiel vous montre comment toouse hello boîte à outils Azure pour IntelliJ toocreate, une application de Web Hello World pour Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Créer une application web Azure de base à l’aide dans IntelliJ
Ce didacticiel montre comment toocreate et déployer une base tooAzure d’application Hello World comme une application Web à l’aide de hello [Azure Toolkit pour IntelliJ]. Un exemple JSP de base est présenté par souci de simplicité, mais des étapes similaires conviennent également pour un servlet Java en ce qui concerne le déploiement d’Azure.

Lorsque vous avez terminé ce didacticiel, votre application doit ressembler similaire toohello suivant illustration lorsque vous l’affichez dans un navigateur web :

![Exemple de page web][01]

## <a name="prerequisites"></a>Composants requis
* JDK (Java Development Kit) version 1.8 ou ultérieure.
* IntelliJ IDEA édition Ultimate. Il peut être téléchargé à partir du site <https://www.jetbrains.com/idea/download/index.html>.
* Une distribution d’un serveur web ou d’un serveur d’applications basé sur Java, comme [Apache Tomcat] ou [Jetty].
* Un abonnement Azure, qui peut être obtenu à l’adresse <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello [Azure Toolkit pour IntelliJ]. Pour plus d’informations sur l’installation hello boîte à outils Azure, consultez [installation Bonjour Azure Toolkit pour IntelliJ].

## <a name="toocreate-a-hello-world-application"></a>toocreate une application Hello World
Tout d’abord, nous allons commencer par créer un projet Java.

1. Démarrer IntelliJ et cliquez sur hello **fichier** menu, puis cliquez sur **nouveau**, puis cliquez sur **projet**.
   
    ![Fichier Nouveau Projet][02]
2. Dans la boîte de dialogue Nouveau projet hello, sélectionnez **Java**, puis **Application Web**, puis cliquez sur **nouveau** tooadd un kit de développement du projet.
   
    ![Boîte de dialogue Nouveau projet][03a]
   
3. Bonjour sélectionner le répertoire de base pour la boîte de dialogue JDK, sélectionnez hello dossier où votre JDK est installé, puis cliquez sur **OK**. Cliquez sur **suivant** dans toocontinue de boîte de dialogue de nouveau projet hello.
   
    ![Spécifiez le répertoire de base du JDK][03b]
4. Pour des raisons de ce didacticiel, nommez le projet de hello **Java application Web sur Azure**, puis cliquez sur **Terminer**.
   
    ![Boîte de dialogue Nouveau projet][04]
5. Dans l’affichage de l’explorateur de projets d’IntelliJ, développez **Java-Web-App-On-Azure**, puis développez **web** et double-cliquez sur **index.jsp**.
   
    ![Page Ouvrir l’index][05c]
6. Lorsque votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez dans l’affichage du texte toodynamically **Hello World !** dans hello existant `<body>` élément. Votre mise à jour `<body>` contenu doit ressembler à hello l’exemple suivant :
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Enregistrez index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy votre tooan application conteneur d’application Web Azure
Il existe plusieurs façons par lequel vous pouvez déployer un tooAzure d’application web Java. Ce didacticiel décrit l’une de hello plus simple : votre application sera déployée tooan conteneur d’application Web Azure - aucun type de projet spécial ni les outils supplémentaires ne sont nécessaires. Hello JDK et hello web conteneur logiciel sera fourni pour vous par Azure, il est donc aucune tooupload besoin de votre propre ; Il vous suffit de votre application de Web Java. Par conséquent, les processus de publication hello pour votre application prendra secondes, pas les minutes.

Avant de publier votre application, vous devez tout d’abord tooconfigure vos paramètres de module. toodo utilisez donc hello comme suit :

1. Dans l’Explorateur de projet de IntelliJ, avec le bouton droit hello **Java application Web sur Azure** projet. Lorsque le menu contextuel de hello s’affiche, cliquez sur **ouvrir les paramètres du Module**.

    ![Ouvrir les paramètres du module][05a]
2. Lorsque la boîte de dialogue hello Structure de projet s’affiche :

   a. Cliquez sur **artefacts** dans la liste des hello **les paramètres de projet**.
   b. Modifier le nom hello artefact Bonjour **nom** zone afin qu’il ne contient pas un espace blanc ou des caractères spéciaux ; cela est nécessaire car hello nom sera utilisé dans hello identificateur de ressource uniforme (URI).
   c. Hello de modification **Type** trop**Application Web : Archive**.
   d. Cliquez sur **OK** boîte de dialogue tooclose hello Structure de projet.

    ![Ouvrir les paramètres du module][05b]

Lorsque vous avez configuré vos paramètres de module, vous pouvez publier votre tooAzure d’application à l’aide de hello comme suit :

1. Dans l’Explorateur de projet de IntelliJ, avec le bouton droit hello **Java application Web sur Azure** projet. Menu contextuel de hello, sélectionnez **Azure**, puis cliquez sur **publier en tant qu’application Web Azure...**
   
    ![Menu contextuel de publication Azure][06]
2. Si vous n’êtes pas déjà inscrit dans Azure à partir de IntelliJ, vous serez invité à toosign à votre compte Azure. (Si vous avez plusieurs comptes Azure, certaines des invites hello pendant le processus de connexion hello peuvent s’afficher plusieurs fois, même si elles apparaissent toobe hello identiques. Dans ce cas, continuer toofollow hello signe dans les instructions.)
   
    ![Boîte de dialogue de connexion à Azure][07]
3. Une fois que vous êtes connecté à votre compte Azure, hello **gérer les abonnements** boîte de dialogue affiche une liste des abonnements qui sont associés à vos informations d’identification. (S’il existe plusieurs abonnements répertoriés et vous souhaitez toowork avec seulement un sous-ensemble spécifique, vous pouvez désactiver éventuellement abonnements hello vous ne souhaitez pas toouse.) Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.
   
    ![Gérer les abonnements][08]
4. Hello lorsque **tooAzure conteneur d’application Web de déployer** boîte de dialogue s’affiche, elle affiche tous les conteneurs de l’application Web que vous avez créé précédemment ; si vous n’avez pas créé tous les conteneurs, liste de hello sera vide.
   
    ![Conteneurs d’applications][09]
5. Si vous n’avez créé un conteneur d’application Web Azure avant ou si vous souhaitez que toopublish votre conteneur tooa application, utilisez hello comme suit. Sinon, sélectionnez un conteneur d’application Web existant et ignorer toostep 6 ci-dessous.
   
   1. Cliquez sur **+**
      
       ![Ajouter un conteneur d’application][10]
   2. Hello **nouveau conteneur d’application Web** boîte de dialogue s’affiche, qui sera utilisé pour hello ensuite plusieurs étapes.
      
       ![Nouveau conteneur d’application][11a]
   3. Entrez un **nom DNS** pour votre conteneur d’application Web ; Ceci va former le nom DNS hello feuille de l’URL de l’hôte hello pour votre application web dans Azure. Notez ce nom hello doit être disponible et se conformer exigences d’affectation de noms de l’application Web tooAzure.
   4. Bonjour **Web conteneur** menu déroulant, logiciel approprié de hello Sélectionnez pour votre application.
      
       Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9. Une distribution récente du logiciel de hello sélectionné sera fournie par Azure, et elle s’exécute sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.
   5. Bonjour **abonnement** menu déroulant, sélectionnez hello abonnement toouse pour ce déploiement.
   6. Bonjour **groupe de ressources** menu déroulant, sélectionnez hello groupe de ressources avec laquelle vous souhaitez tooassociate votre application Web. (Les groupes de Ressources azure permet de vous toogroup les ressources associées ensemble afin que, par exemple, ils peuvent être supprimés ensemble.)
      
       Vous pouvez sélectionner un groupe de ressources existant (si vous en avez) et g toostep de skip ci-dessous ou utilisez hello suite étapes toocreate un groupe de ressources :
      
      * Sélectionnez  **&lt; &lt; créer le nouveau groupe de ressources &gt; &gt;**  Bonjour **groupe de ressources** menu déroulant.
      * Hello **nouveau groupe de ressources** boîte de dialogue s’affiche :
        
          ![Nouveau groupe de ressources][12]
      * Bonjour de hello **nom** zone de texte, spécifiez un nom pour votre nouveau groupe de ressources.
      * Bonjour de hello **région** menu déroulant, emplacement pour votre groupe de ressources de centre de données Azure approprié de hello select.
      * Cliquez sur **OK**.
   7. Hello **du Plan App Service** menu déroulant répertorie les plans de service d’application hello associés hello groupe de ressources que vous avez sélectionné. (Un Plan App Service spécifie les informations comme emplacement de hello de votre application Web, hello niveau tarifaire et taille d’instance de calcul hello. Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)
      
       Vous pouvez sélectionner un Plan de Service application existant (si vous en avez) et ignorer h toostep ci-dessous ou utilisez hello suivant toocreate étapes un nouveau Plan App Service :
      
      * Sélectionnez  **&lt; &lt; créer à nouveau un Plan App Service &gt; &gt;**  Bonjour **du Plan App Service** menu déroulant.
      * Hello **nouveau du Plan App Service** boîte de dialogue s’affiche :
        
          ![Nouveau plan App Service][13]
      * Bonjour de hello **nom** zone de texte, spécifiez un nom pour votre nouveau Plan App Service.
      * Bonjour de hello **emplacement** menu déroulant, emplacement pour le plan de hello centre de données Azure approprié de hello select.
      * Bonjour de hello **niveau tarifaire** menu déroulant, sélectionnez hello approprié de tarification pour le plan de hello. À des fins de test, vous pouvez choisir **Free**(Gratuit).
      * Bonjour de hello **taille de l’Instance** menu déroulant, taille de l’instance appropriée sélectionnez hello pour le plan de hello. À des fins de test, vous pouvez choisir **Small**(Petite).
      * Cliquez sur **OK**.
   8. (Facultatif) Par défaut, une distribution récente de Java 8 sera déployée automatiquement en tant que votre machine virtuelle Java par conteneur d’application web Azure tooyour. Toutefois, vous pouvez sélectionner une version différente et la distribution de hello JVM. toodo utilisez donc hello comme suit :
      
      * Cliquez sur hello **JDK** onglet Bonjour **nouveau conteneur d’application Web** boîte de dialogue.
      * Vous pouvez choisir une des options suivantes de hello :
        
        * Déployer la valeur par défaut de hello JDK qui est offert par Azure
        * Déployer un JDK tiers à partir d’une liste déroulante de JDK supplémentaires disponibles sur Azure
        * Déployer un JDK personnalisé, qui doit être empaqueté dans un fichier ZIP et accessible au public ou dans votre compte de stockage Azure
        
        ![Onglet JDK du nouveau conteneur d’application][11b]
   9. Une fois que vous avez effectué toutes les hello étapes ci-dessus, boîte de dialogue nouveau conteneur d’application Web hello doit ressembler à hello après l’illustration :
      
       ![Nouveau conteneur d’application][14]
   10. Cliquez sur **OK** création de hello toocomplete de votre conteneur d’application Web.
       
        Attendez quelques secondes pour la liste de hello Web App conteneurs toobe hello actualisé, et votre conteneur d’application web de nouvellement créé doit maintenant être sélectionné dans la liste de hello.
6. Vous êtes maintenant déploiement initial de hello prêt toocomplete de tooAzure de votre application Web ; Cliquez sur **OK** toodeploy votre toohello d’application Java sélectionné conteneur de l’application Web. Par défaut, votre application sera déployée en tant que sous-répertoire hello du serveur d’applications. Si vous voulez qu’elle toobe déployé en tant qu’application de racine hello, vérifiez hello **déployer tooroot** case à cocher avant de cliquer sur **OK**.
   
    ![Déployer tooAzure][15]
7. Ensuite, vous devez voir hello **journal des activités Azure** vue, ce qui indique l’état du déploiement de votre application Web hello.
   
    ![Indicateur de progression][16]
   
    Hello du déploiement de votre application Web de tooAzure doit durer quelques secondes seulement toocomplete. Lorsque vous êtes prêt application, vous verrez un lien nommé **publié** Bonjour **état** colonne. Lorsque vous cliquez sur le lien de hello, il vous faudra page d’accueil de l’application Web de tooyour déployé, ou vous pouvez utiliser les étapes de hello Bonjour suivant la section toobrowse tooyour l’application web.

## <a name="browsing-tooyour-web-app-on-azure"></a>Navigation tooyour application Web sur Azure
toobrowse tooyour application Web sur Azure, vous pouvez utiliser hello **Explorateur Azure** vue.

Si hello **Explorateur Azure** affichage n’est pas déjà ouvert, vous pouvez l’ouvrir en cliquant sur ensuite **vue** menu IntelliJ, puis cliquez sur **fenêtres Outil**, puis cliquez sur  **Service Explorateur**. Si vous n’avez pas précédemment connecté, il vous invite toodo donc.

Hello lorsque **Explorateur Azure** s’affiche, utilisez suivez ces tooyour de toobrowse comme application Web : 

1. Développez hello **Azure** nœud.
2. Développez hello **Web Apps** nœud. 
3. Avec le bouton hello souhaité application Web.
4. Lorsque le menu contextuel de hello s’affiche, cliquez sur **ouvrir dans le navigateur**.
   
    ![Parcourir l’application web][17]

## <a name="updating-your-web-app"></a>Mise à jour de votre application web
La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :

* Vous pouvez mettre à jour le déploiement hello d’une application de Web Java existante.
* Vous pouvez publier un toohello d’application Java supplémentaire même conteneur d’application Web.

Dans les deux cas, les processus hello sont identique et ne prend que quelques secondes :

1. Dans l’Explorateur de projets hello IntelliJ, cliquez sur application Java hello que vous souhaitez tooupdate ou que vous ajoutez tooan existant de conteneur d’application Web.
2. Menu contextuel de hello, sélectionnez **Azure** , puis **publier en tant qu’application Web Azure...**
3. Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît. Sélectionnez hello un choix toopublish ou de publier votre Java application tooand, cliquez à nouveau **OK**.

Quelques secondes plus tard, hello **journal des activités Azure** vue affiche votre déploiement de mises à jour en tant que **publié** et vous sera en mesure de tooverify votre application mis à jour dans un navigateur web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Démarrage, arrêt ou redémarrage d’une application web existante
toostart ou arrêter un conteneur d’application Web Azure existant, (y compris toutes les applications de Java hello déployé qu’elle contient), vous pouvez utiliser des hello **Explorateur Azure** vue.

Si hello **Explorateur Azure** affichage n’est pas déjà ouvert, vous pouvez l’ouvrir en cliquant sur ensuite **vue** menu IntelliJ, puis cliquez sur **fenêtres Outil**, puis cliquez sur  **Service Explorateur**. Si vous n’avez pas précédemment connecté, il vous invite toodo donc.

Hello lorsque **Explorateur Azure** s’affiche, utilisez, suivez ces étapes toostart ou arrêter votre application Web : 

1. Développez hello **Azure** nœud.
2. Développez hello **Web Apps** nœud. 
3. Avec le bouton hello souhaité application Web.
4. Lorsque le menu contextuel de hello s’affiche, cliquez sur **Démarrer**, **arrêter**, ou **redémarrer**. Notez que les options de menu hello sont sensibles au contexte, donc vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.
   
    ![Arrêter l’application Web][18]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :

* [boîte à outils Azure pour Eclipse]
  * [Lors de l’installation hello boîte à outils Azure pour Eclipse]
  * [Créer une application web « Hello World » pour Azure dans Eclipse]
  * [Nouveautés dans hello boîte à outils Azure pour Eclipse]
* [Azure Toolkit pour IntelliJ]
  * [installation Bonjour Azure Toolkit pour IntelliJ]
  * *Créer une application web « Hello World » pour Azure dans IntelliJ (cet article)*
  * [Nouveautés dans hello Azure Toolkit pour IntelliJ]

<a name="see-also"></a>

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].

Pour plus d’informations sur la création d’applications Web Azure, consultez hello [vue d’ensemble des applications Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[installation Bonjour Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nouveautés dans hello boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nouveautés dans hello Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[vue d’ensemble des applications Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
