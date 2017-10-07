---
title: aaaAzure Service Fabric plug-in Eclipse | Documents Microsoft
description: "Prise en main hello Service Fabric plug-in d’Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Plug-in Service Fabric pour le développement d’applications Java sous Eclipse
Eclipse est un des hello plus largement utilisé intégré (IDE) des environnements de développement pour les développeurs Java. Dans cet article, nous décrivons comment tooset de votre toowork d’environnement de développement Eclipse avec Azure Service Fabric. Découvrez comment créer une application Service Fabric tooinstall hello plug-in, l’infrastructure de Service et déployer votre cluster Service Fabric application tooa local ou distant Service Fabric dans Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Installer ou mettre à jour hello Service Fabric plug-in Eclipse Neon
Vous pouvez installer un plug-in Service Fabric sur Eclipse. Hello plug-in vous permet de simplifier les processus hello de génération et de déploiement des services de Java.

1.  Assurez-vous d’avoir hello dernière version d’Eclipse Neon et la version la plus récente de Buildship hello (1.0.17 ou une version ultérieure) installé :
    -   versions de hello toocheck des composants installés, dans Eclipse Neon, accédez trop**aide** > **détails de l’Installation**.
    -   tooupdate Buildship, consultez [Eclipse Buildship : Eclipse Plug-ins pour Gradle][buildship-update].
    -   toocheck pour et installer les mises à jour pour Eclipse Neon, sont trop**aide** > **mises à jour**.

2.  tooinstall hello Service Fabric plug-in dans Eclipse Neon, accédez trop**aide** > **installer le nouveau logiciel**.
  1.    Bonjour **travailler avec** , entrez **http://dl.microsoft.com/eclipse**.
  2.    Cliquez sur **Add**.

         ![Plug-in Service Fabric pour Eclipse Neon][sf-eclipse-plugin-install]
  3.    Sélectionnez hello Service Fabric plug-in, puis cliquez sur **suivant**.
  4.    Complétez les étapes d’installation hello et puis acceptez le contrat de licence logiciel Microsoft hello.

Si vous avez déjà hello Service Fabric plug-in installé, assurez-vous que vous avez la version la plus récente hello. toocheck pour les mises à jour disponibles, accédez trop**aide** > **détails de l’Installation**. Dans la liste de hello des plug-ins installés, sélectionnez le Service Fabric, puis cliquez sur **mise à jour**. Les mises à jour disponibles seront installées.

> [!NOTE]
> Si l’installation ou la mise à jour de hello Service Fabric plug-in est lente, il peut être en raison du paramètre d’Eclipse tooan. Eclipse collecte des métadonnées sur tous les sites de tooupdate de modifications qui sont inscrits avec votre instance d’Eclipse. toospeed processus hello de vérification et l’installation d’une mise à jour du plug-in de l’infrastructure de Service, accédez trop**Sites logiciels disponibles**. Désactivez les cases à cocher hello pour tous les sites à l’exception de hello celle qui pointe l’emplacement du plug-in du Service Fabric toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Créer une application Service Fabric dans Eclipse

1.  Dans Eclipse Neon, accédez trop**fichier** > **nouveau** > **autres**. Sélectionnez **Projet Service Fabric**, puis cliquez sur **Suivant**.

    ![Nouveau projet Service Fabric, page 1][create-application/p1]

2.  Saisissez un nom pour votre projet, puis cliquez sur **Suivant**.

    ![Nouveau projet Service Fabric, page 2][create-application/p2]

3.  Dans la liste hello des modèles, sélectionnez **modèle de Service**. Sélectionnez votre type de modèle de service (acteur, sans état, conteneur ou binaire invité), puis cliquez sur **Suivant**.

    ![Nouveau projet Service Fabric, page 3][create-application/p3]

4.  Entrez le nom du service hello et les détails du service, puis cliquez sur **Terminer**.

    ![Nouveau projet Service Fabric, page 4][create-application/p4]

5. Lorsque vous créez votre premier projet de Service Fabric Bonjour **ouvrir une Perspective associés** boîte de dialogue, cliquez sur **Oui**.

    ![Nouveau projet Service Fabric, page 5][create-application/p5]

6.  Votre nouveau projet ressemble à ceci :

    ![Nouveau projet Service Fabric, page 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Créer et déployer une application Service Fabric dans Eclipse

1.  Cliquez avec le bouton droit de la souris sur votre nouvelle application Service Fabric, puis sélectionnez **Service Fabric**.

    ![Menu contextuel Service Fabric][publish/RightClick]

2. Dans le sous-menu de hello, activez l’option hello :
    -   application de hello toobuild sans nettoyage, cliquez sur **Application Build**.
    -   toodo une génération complète de l’application hello, cliquez sur **régénérer l’Application**.
    -   application de hello tooclean d’artefacts générés, cliquez sur **propre Application**.

3.  Dans ce menu, vous pouvez également déployer, annuler le déploiement et publier votre application :
    -   cluster local de tooyour toodeploy, cliquez sur **déployer l’Application**.
    -   Bonjour **publier l’Application** boîte de dialogue, sélectionnez un profil de publication :
        -  **Local.json**
        -  **Cloud.json**

     Ces fichiers JavaScript Objet Notation (JSON) stockent des informations (par exemple, les points de terminaison de connexion et les informations de sécurité) qui est tooyour tooconnect requis local ou cloud (Azure).

  ![Menu Publier de Service Fabric][publish/Publish]

Une autre façon toodeploy votre application de Service Fabric est à l’aide d’Eclipse exécutée les configurations.

  1.    Accédez trop**exécuter** > **les Configurations de série**.
  2.    Sous **Gradle projet**, sélectionnez hello **ServiceFabricDeployer** exécuter la configuration.
  3.    Dans le volet de droite de hello sur hello **Arguments** onglet, pour **publishProfile**, sélectionnez **local** ou **cloud**.  valeur par défaut Hello est **local**. tooa toodeploy à distance ou le cluster du cloud, sélectionnez **cloud**.
  4.    tooensure que les informations correctes hello sont remplies Bonjour des profils de publication, modifiez **Local.json** ou **Cloud.json** en fonction des besoins. Vous pouvez ajouter ou mettre à jour les détails du point de terminaison et les informations d’identification de sécurité.
  5.    Vérifiez que **du répertoire de travail** pointe application toohello vous souhaitez toodeploy. toochange hello application, cliquez sur hello **espace de travail** bouton, puis sélectionnez application hello.
  6.    Cliquez sur **Appliquer**, puis sur **Exécuter**.

Votre application est générée et déployée en quelques instants. Vous pouvez surveiller l’état du déploiement hello dans Service Fabric Explorer.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Ajouter un tooyour de service Service Fabric application Service Fabric

tooadd une application Service Fabric Service Fabric service tooan existante, procédez comme hello comme suit :

1.  Projet de hello contextuel vous voulez tooadd un service, puis cliquez sur **Service Fabric**.

    ![Ajouter un service Service Fabric, page 1][add-service/p1]

2.  Cliquez sur **ajouter un Service Service Fabric**, et hello complète des étapes tooadd un projet toohello de service.
3.  Modèle de service hello Sélectionnez votre choix tooadd tooyour projet, puis cliquez sur **suivant**.

    ![Ajouter un service Service Fabric, page 2][add-service/p2]

4.  Entrez le nom du service hello (et autres détails, si nécessaire), puis cliquez sur hello **ajouter un Service** bouton.  

    ![Ajouter un service Service Fabric, page 3][add-service/p3]

5.  Une fois que le service de hello est ajouté, structure globale de votre projet recherche similaire toohello suivant du projet :

    ![Ajouter un service Service Fabric, page 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Modifier les versions de manifeste de votre application Java Service Fabric

versions de manifeste tooedit, cliquez avec le bouton droit sur le projet de hello, accédez trop**Service Fabric** et sélectionnez **modifier les Versions de manifeste...**  à partir de la liste déroulante du menu hello. Dans l’Assistant de hello, vous pouvez mettre à jour hello des versions manifeste manifeste d’application manifeste, service et hello pour **Code**, **Config** et **données** packages.

Si vous activez l’option de hello **mettre à jour automatiquement les applications et les versions de service** et ensuite mettre à jour une version, les versions de manifeste hello puis seront automatiquement mis à jour. toogive, par exemple, vous tout d’abord sélectionnez hello de la case à cocher, puis version hello de mise à jour de **Code** version 0.0.0 too0.0.1 et cliquez sur **Terminer**, puis de version du manifeste et manifeste d’application de service version sera automatiquement mis à jour too0.0.1.

## <a name="upgrade-your-service-fabric-java-application"></a>Mettre à niveau votre application Java Service Fabric

Pour un scénario de mise à niveau, par exemple vous avez créé hello **App1** projet à l’aide de hello Service Fabric plug-in Eclipse. Avoir déployé à l’aide de toocreate de plug-in hello une application nommée **fabric : / App1Application**. type d’application Hello est **App1AppicationType**, et la version de l’application hello est 1.0. Maintenant, vous souhaitez que tooupgrade votre application sans interrompre la disponibilité.

Tout d’abord, apporter des modifications tooyour application, puis reconstruire hello modifié service. Hello de mise à jour modifié le fichier manifeste du service (ServiceManifest.xml) avec les versions hello mis à jour pour hello service (et de Code, configuration ou données, selon le cas). En outre, modifier le manifeste de l’application hello (ApplicationManifest.xml) avec le numéro de version hello mis à jour pour l’application hello et hello service modifié.  

tooupgrade votre application à l’aide d’Eclipse Neon, vous pouvez créer un profil de configuration d’exécution en double. Ensuite, utilisez tooupgrade votre application en fonction des besoins.

1.  Accédez trop**exécuter** > **les Configurations de série**. Dans le volet gauche de hello, cliquez sur hello petite flèche toohello gauche **Gradle projet**.
2.  Cliquez avec le bouton droit de la souris sur **ServiceFabricDeployer**, puis sélectionnez **Dupliquer**. Entrez un nouveau nom pour cette configuration, par exemple, **ServiceFabricUpgrader**.
3.  Dans le panneau droit hello, sur hello **Arguments** , modifiez **- ipconfig /release = 'déployer'** trop**- ipconfig /release = 'mise à niveau'**, puis cliquez sur **appliquer**.

Ce processus crée et enregistre un profil de configuration d’exécution vous pouvez utiliser à n’importe quel tooupgrade de temps à votre application. Il obtient également la dernière version de type application mis à jour hello à partir du fichier manifeste d’application hello.

mise à niveau des applications Hello prend quelques minutes. Vous pouvez surveiller la mise à niveau des applications de hello dans Service Fabric Explorer.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migration d’ancien toobe d’applications Java de l’infrastructure de Service utilisé avec Maven
Nous avons déplacé récemment bibliothèques Service Fabric Java à partir du référentiel de tooMaven Service Fabric Java SDK. Alors que hello nouvelles applications générer à l’aide d’Eclipse, génère les plus récentes des projets mis à jour (qui seront en mesure de toowork avec Maven), vous pouvez mettre à jour votre Service Fabric existant sans état ou les applications Java acteur, qui utilisaient l’hello Service Fabric Java SDK versions antérieures, toouse hello Service Fabric dépendances Java à partir de Maven. Suivez les étapes de hello mentionnés [ici](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure votre ancienne application fonctionne avec Maven.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
