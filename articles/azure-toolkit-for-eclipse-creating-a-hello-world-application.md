---
title: aaaCreate un Service Cloud Hello World pour Azure dans Eclipse
description: "Découvrez comment une application Hello World simple à l’aide de toocreate hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Créer un service cloud « Hello World » pour Azure dans Eclipse
Hello étapes suivantes vous montrent comment toocreate et déployer une base tooAzure d’application JSP à l’aide de hello boîte à outils Azure pour Eclipse. Un exemple JSP est présenté par souci de simplicité, mais des étapes très similaires conviennent également pour un servlet Java en ce qui concerne le déploiement d’Azure.

application Hello ressemblera similaire toohello suivantes :

![][ic600360]

## <a name="prerequisites"></a>Composants requis
* JDK (Java Development Kit) version 1.7 ou ultérieure.
* IDE (environnement de développement intégré) Eclipse pour développeurs Java EE, Indigo ou ultérieur, Vous pouvez le télécharger à l’adresse suivante : <http://www.eclipse.org/downloads/>.
* Distribution d’un serveur web ou d’un serveur d’applications basé sur Java, tel qu’Apache Tomcat, GlassFish, JBoss Application Server, Jetty ou IBM® WebSphere® Application Server Liberty Core.
* Un abonnement Azure, qui peut être obtenu à l’adresse <http://azure.microsoft.com/pricing/purchase-options/>.
* Hello boîte à outils Azure pour Eclipse. Pour plus d’informations, consultez [installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate une application Hello World
Tout d’abord, nous allons commencer par créer un projet Java.

1. Démarrez Eclipse et au menu de hello cliquez sur **fichier**, cliquez sur **nouveau**, puis cliquez sur **projet Web dynamique**. (Si vous ne voyez pas **projet Web dynamique** répertorié comme un projet disponible après avoir cliqué sur **fichier**, **nouveau**, puis hello suivant : cliquez sur **fichier**, cliquez sur **nouveau**, cliquez sur **projet...** , développez **Web**, cliquez sur **projet Web dynamique**, puis cliquez sur **suivant**.)

1. Pour des raisons de ce didacticiel, nommez le projet de hello **MyHelloWorld**. (Assurez-vous vous utilisez ce nom, les étapes suivantes de ce didacticiel attendent votre toobe de fichier WAR nommé MyHelloWorld). Votre écran apparaîtra similaire toohello suivantes :

   ![][ic589576]

1. Cliquez sur **Terminer**.

1. Dans la vue Explorateur de projets d’Eclipse, développez **MyHelloWorld**. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.

1. Bonjour **nouveau fichier JSP** boîte de dialogue, le nom de fichier hello **index.jsp**. Conservez le dossier parent hello **MyHelloWorld/WebContent**, comme indiqué dans les éléments suivants de hello :

   ![][ic659262]

1. Bonjour **sélectionner un modèle JSP** boîte de dialogue, pour les besoins de ce didacticiel, sélectionnez **nouveau fichier JSP (html)** et cliquez sur **Terminer**.

1. Lorsque le fichier de hello index.jsp s’ouvre dans Eclipse, ajoutez dans l’affichage du texte toodynamically **Hello World !** dans hello existant `<body>` élément. Votre mise à jour `<body>` le contenu doit apparaître comme suit de hello :
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Enregistrez index.jsp.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy votre application tooAzure, les hello moyen simple et rapide
Dès que vous avez un tootest de prêt d’application web Java, vous pouvez utiliser hello suivant tootry raccourci il expire directement sur hello Azure cloud.

1. Dans l’Explorateur de projets d’Eclipse, cliquez sur **MyHelloWorld**.

2. Dans la barre d’outils de hello Eclipse, cliquez sur hello **publier** bouton déroulant, puis cliquez sur **publier en tant que Service Cloud Azure**

   ![][publishDropdownButton]

3. Si vous publiez ce tooAzure d’application pour hello première fois et que vous n’avez créé un projet de déploiement Azure pour cette application avant, un projet de déploiement Azure créé automatiquement. Vous devez voir hello suivant à l’invite, qui répertorie également hello JDK package serveur d’applications et qui sera automatiquement déployé toorun votre application.

   ![][ic789598]
   
   Cette approche de raccourci permet un tootest rapidement et facilement votre application dans Azure sans avoir tooconfigure le JDK est différent de valeurs par défaut hello ou un serveur spécifiques. Si vous êtes satisfait des valeurs par défaut hello, vous pouvez cliquer sur **OK** toocontinue avec hello comme suit.
   Toutefois, si vous souhaitez toochange hello JDK ou toouse de serveur d’applications pour votre application, vous pouvez faire ultérieurement en modifiant un projet de déploiement Azure hello qui a été créé automatiquement pour vous, ou vous pouvez cliquer sur **Annuler** maintenant et en lecture Hello **les projets de déploiement sur Azure section** de ce didacticiel.

4. Bonjour **publier tooAzure** boîte de dialogue :

   1. S’il n’y aucun tooselect abonnements Bonjour **abonnement** liste encore, suivez ces étapes tooimport vos informations d’abonnement :
      1. Cliquez sur **Importer à partir du fichier PUBLISH-SETTINGS**.
      2. Bonjour **importation des informations d’abonnement** boîte de dialogue, cliquez sur **télécharger le fichier PUBLISH-SETTINGS**. Si vous n’êtes pas encore connecté à votre compte Azure, vous serez invité à toolog dans. Ensuite, vous êtes invité à entrer toosave Azure publier le fichier de paramètres. Enregistrez-le tooyour les ordinateur local.
      3. Toujours en hello **importation des informations d’abonnement** boîte de dialogue, cliquez sur hello **Parcourir** bouton, hello sélectionnez Publier le fichier de paramètres que vous avez enregistré localement à l’étape précédente de hello, puis cliquez sur  **Ouvrez**. Votre écran doit ressembler similaire toohello suivantes :![][ic644267]
      4. Cliquez sur **OK**.
   2. Pour **abonnement**, sélectionnez l’abonnement hello que vous souhaitez utiliser pour votre déploiement.
   3. Pour **compte de stockage**, sélectionnez le compte de stockage hello que vous souhaitez toouse, ou cliquez sur **nouveau** toocreate un compte de stockage.
   4. Pour **nom du Service**, sélectionnez le service de cloud hello que vous souhaitez toouse, ou cliquez sur **nouveau** toocreate un nouveau service cloud.
   5. Pour **système d’exploitation cible**, sélectionnez hello version du système d’exploitation de hello que toouse pour votre déploiement.
   6. Dans **Environnement cible**, pour les besoins de ce didacticiel, sélectionnez **Intermédiaire**. (Lorsque vous êtes le site de production tooyour toodeploy prêt, vous allez modifier cela trop**Production**.)
   7. Facultatif : Vérifiez que **remplacer le déploiement précédent** est activée si vous souhaitez que votre nouveau tooautomatically de déploiement remplacer hello déploiement précédent. Lorsque vous activez cette option, vous ne serez pas les problèmes de « 409 conflit » lors de la publication toohello même emplacement.
      Notez que hello **publier tooAzure** boîte de dialogue contient une section pour **l’accès à distance**. Par défaut, l’accès à distance n’est pas activé, et nous ne l’activerons pas pour cet exemple. tooenable l’accès à distance, vous devez entrer un toouse de nom et mot de passe utilisateur lors de la connexion à distance. Pour plus d’informations sur l’accès à distance, consultez la page [Activation de l’accès à distance pour les déploiements Azure dans Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Votre **publier tooAzure** boîte de dialogue similaire toohello suivantes :![][ic719488]

5. Cliquez sur **publier** environnement intermédiaire de toohello toopublish.

   Lorsque le message tooperform une génération complète, cliquez sur **Oui**. Cette opération peut prendre plusieurs minutes avant que la première génération de hello.
   Un **journal des activités Azure** s’affiche dans la section des vues Eclipse avec onglets.
   ![][ic719489]Vous pouvez utiliser ce journal, mais aussi hello **Console** afficher, la progression de hello toosee de votre déploiement. Une autre solution consiste à toolog dans toohello [portail de gestion Azure][Azure Management Portal]et utilisez hello **Services de cloud computing** section État de hello toomonitor.

6. Lorsque votre déploiement est déployé, hello **journal des activités Azure** présentent l’état de **publié**. Cliquez sur **publié**, comme indiqué dans hello suivant image et que votre navigateur seront ouvre à une instance de votre déploiement.

   ![][ic719490]

Comme il s’agit d’un tooa déploiement environnement intermédiaire, nom DNS de hello sera hello forme http://&lt;*guid*&gt;. cloudapp.net et l’URL de hello contiendra DNS hello plus un suffixe pour votre application. Par exemple, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (hello **MyHelloWorld** partie respecte la casse.) Vous pouvez également voir hello DNS nom si vous cliquez sur le nom du déploiement hello dans hello portail Azure Platform Management (dans la partie de Services de cloud computing hello hello du portail de gestion).

Bien que cette procédure pas à pas a été pour un toohello déploiement environnement intermédiaire, une déploiement tooproduction suit hello les mêmes étapes, à l’exception dans hello **publier tooAzure** boîte de dialogue, sélectionnez **Production** au lieu de **intermédiaire** pour hello **environnement cible**. Une déploiement tooproduction entraîne une URL basée sur le nom DNS de hello de votre choix, au lieu d’un GUID utilisé pour la mise en lots.

> [!WARNING]
> À ce stade, vous avez déployé votre cloud de toohello d’application Windows Azure. Toutefois, avant de continuer, sachez qu’une application déployée, même si elle n’est pas en cours d’exécution continue tooaccrue heures facturables pour votre abonnement. Il est donc extrêmement important de supprimer les déploiements non souhaités de votre abonnement Azure.
> 
> 

## <a name="about-azure-deployment-projects"></a>À propos des projets de déploiement Azure
Dans commande toodeploy un ou plusieurs tooAzure d’applications Java, un projet de déploiement Azure est nécessaire. Elle joue le rôle de hello Hello « package » dont vos applications ont besoin toobe encapsulé dans toobe commande publiée sur Azure.

Outre les informations de hello sur vos applications, un projet de déploiement Azure contient également des informations sur d’autres composants clés de votre déploiement, surtout : hello application server conteneur toorun votre application web et hello Java runtime toorun il sur. Azure prend en charge une large sélection d’environnements d’exécution Java et de serveurs d’applications Java parmi lesquels vous pouvez choisir.

Bien que l’exemple hello utilisé ici soit considérablement simplifié à des fins pédagogiques, un projet de déploiement Azure peut contenir également d’autres informations de configuration importantes qui vous permet de toocreate presque arbitrairement complexe, évolutive et hautement disponible, services de cloud computing d’à plusieurs niveaux avec vos applications. Vous pouvez activer l’**affinité de session (« sessions rémanentes »)**, la **mise en cache rapide**, le **déchargement SSL**, le **routage de pare-feu/port**, l’**accès à distance** et plusieurs autres fonctionnalités puissantes.

Si vous avez effectué hello précédente section de ce didacticiel (« toodeploy votre application tooAzure, les hello moyen simple et rapide »), vous voyez maintenant un nouveau projet de déploiement d’Azure dans hello Explorateur de projets générés automatiquement pour vous et nommé « **MyHelloWorld_onAzure**».

Vous pourriez également avoir commencé ce didacticiel en créant tout d’abord un projet de déploiement Azure vide et en ajoutant votre tooit ou les applications. Il est plus long processus, mais ce qui vous donne davantage de contrôle sur la configuration initiale à partir du début de hello hello.

toocreate un nouveau projet de déploiement d’Azure à partir de zéro, cliquez sur hello **nouveau projet de déploiement Azure** bouton ![][ic710876].

Indépendamment du fait que vous travaillez sur un projet de déploiement Azure existant, ou créer un à partir de zéro, vous sont en mesure de toochange ses paramètres de configuration et les composants, tels que hello JDK ou hello serveur d’applications, tout aussi facilement à tout moment.

toochange hello JDK, ou serveur d’applications hello ou liste des applications hello dans un projet de déploiement Azure existant :

1. Développez le nœud de projet hello (par exemple, **MyHelloWorld_onAzure**) dans l’Explorateur de projets de hello

2. Cliquez avec le bouton droit sur **WorkerRole1**

3. Développez hello **Azure** sous-menu dans le menu contextuel de hello

4. Cliquez sur **Configuration du serveur**

Indépendamment de si vous avez démarré ces étapes de configuration de serveur en modifiant un projet de déploiement Azure existant comme indiqué ci-dessus, ou créer un nouveau à partir de zéro, vous verrez hello même type de boîtes de dialogue qui vous tooconfigure votre JDK, votre serveur et application composants. toolearn plus de la façon dont les paramètres de hello toochange dans ces boîtes de dialogue, par exemple toochange hello JDK, hello du serveur d’applications et ajouter ou supprimer des applications dans un déploiement, consultez hello [propriétés de configuration de serveur] [ Server configuration properties] l’article.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Windows uniquement : toodeploy émulateur de calcul toohello de votre application

> [!NOTE]
> Hello émulateur Azure est disponible uniquement sur Windows. Ignorez cette section si vous utilisez un autre système d’exploitation.
> 
> 

Si vous avez créé un nouveau projet de déploiement Azure suit hello décrites plus haut, c'est-à-dire implicitement en publiant votre application tooAzure, hello JDK et les serveurs d’applications ont été configurés pour le cloud de hello, mais pas pour l’émulation locale. tooprepare votre projet de test dans l’émulateur local de hello, procédez comme suit :

1. Dans l’Explorateur de projets d’Eclipse, cliquez sur **MyHelloWorld_onAzure**.

2. Cliquez avec le bouton droit sur **WorkerRole1**.

3. Développez hello **Azure** sous-menu dans le menu contextuel de hello.

4. Cliquez sur **Configuration du serveur**.

5. Sur hello **JDK** onglet, vérifiez si hello toolkit a préconfigurée par défaut JDK local pour vous. Dans le cas contraire, ou si vous souhaitez hello toochange supposé par défaut, assurez-vous que hello **hello utilisez JDK à partir de ce chemin d’accès de fichier pour tester localement** case à cocher est activée et hello emplacement d’installation JDK que vous souhaitez toouse est spécifié. Si vous souhaitez toochange, cliquez sur hello **Parcourir** à l’aide du contrôle de navigation hello, sélectionnez l’emplacement du répertoire de hello JDK toouse hello.

6. Cliquez sur hello **Server** onglet.

7. Bonjour **le chemin d’accès au serveur Local** zone de texte en bas de hello de boîte de dialogue hello, entrez chemin hello d’un serveur installé localement qui correspond au type de hello et numéro de version principale du serveur hello sélectionné en haut de hello de boîte de dialogue hello sous Hello **déployer un serveur de ce type** case à cocher. Si vous souhaitez toouse un autre type ou la version majeure hello du serveur d’applications, modifiez d’abord sélection hello sous cette case à cocher.

8. Cliquez sur **OK**.

9. Dans la barre d’outils de hello Eclipse, cliquez sur hello **exécuter dans l’émulateur Azure** bouton, ![][ic710879]. Si hello **exécuter dans l’émulateur Azure** bouton n’est pas activé, vérifiez que **MyHelloWorld_onAzure** est sélectionné dans l’Explorateur de projets d’Eclipse et assurez-vous que l’Explorateur de projets d’Eclipse est comme hello fenêtre active. Cela sera tout d’abord démarrer une génération complète de votre projet, puis démarrez votre application de web Java dans l’émulateur de calcul hello. (Notez qu’en fonction des caractéristiques de performances de votre ordinateur, hello première génération peut prendre entre quelques secondes tooa quelques minutes, mais les générations suivantes recevez plus rapide.) Après la première étape de génération hello est terminée, vous serez invité par le contrôle de compte utilisateur (UAC) Windows tooallow toomake de cette commande change tooyour ordinateur. Cliquez sur **Oui**.

> [!IMPORTANT]
> Si vous ne voyez pas de vérification de hello UAC invite de commandes, hello barre des tâches Windows pour l’icône hello et commencez par cliquer sur elle. Parfois hello invite UAC n’apparaît pas comme une fenêtre au premier plan, mais est visible uniquement comme une icône de barre des tâches.
> 
> 

1. Examinez la sortie hello de hello compute emulator UI toodetermine s’il existe des problèmes avec votre projet. En fonction du contenu hello de votre déploiement, il peut prendre quelques minutes pour votre toobe application complètement démarré dans l’émulateur de calcul hello.

2. Démarrez votre navigateur et d’utiliser hello `http://localhost:8080/MyHelloWorld` en tant qu’adresse de hello (hello `MyHelloWorld` partie de hello URL respecte la casse). Vous devez voir votre l’application MyHelloWorld (sortie hello de index.jsp), les toohello similaire suivant l’image :

   ![][ic589579]

Lorsque vous êtes prêt toostop votre application de s’exécuter dans l’émulateur de calcul hello, dans la barre d’outils de hello Eclipse, cliquez sur hello **réinitialiser l’émulateur Azure** bouton, ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete votre déploiement
toodelete votre déploiement dans hello boîte à outils Azure pour Eclipse, assurez-vous que **MyHelloWorld_onAzure** est sélectionné dans l’Explorateur de projets d’Eclipse, assurez-vous de hello Explorateur de projets Eclipse a fenêtre actuelle hello concentrer, puis cliquez sur Hello **annuler la publication** bouton, ![][ic710883], dans la barre d’outils de hello Eclipse. (Vous pouvez le faire hello même opération en double-cliquant sur **MyHelloWorld_onAzure** dans l’Explorateur de projets d’Eclipse, en cliquant sur **Azure** , puis en cliquant sur **annuler le déploiement d’Azure Cloud**.) Cette action affiche hello **annuler la publication d’un projet Azure** boîte de dialogue.

![][ic719491]

Sélectionnez hello abonnement et le service cloud qui contient votre déploiement, le déploiement hello select que vous souhaitez toodelete, puis cliquez sur **annuler la publication**.

(Un autre toousing hello toolkit toodelete hello de déploiement est toouse hello **Services de cloud computing** section Hello portail de gestion Azure : accédez tooyour déploiement, sélectionnez-le, puis cliquez sur hello **supprimer** bouton. Cela arrête et ensuite supprimer, le déploiement de hello. Si vous souhaitez seulement le déploiement de hello toostop mais pas le supprimer, cliquez sur hello **arrêter** bouton au lieu de hello **supprimer** bouton, mais comme mentionné ci-dessus, si vous ne supprimez pas le déploiement hello, sera de frais facturables continuer tooaccrue pour votre déploiement même s’il est arrêté).

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Nouveautés dans hello boîte à outils Azure pour Eclipse][What's New in hello Azure Toolkit for Eclipse]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
