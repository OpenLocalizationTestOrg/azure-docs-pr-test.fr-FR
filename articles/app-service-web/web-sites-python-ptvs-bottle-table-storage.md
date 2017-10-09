---
title: aaaBottle et stockage de Table Azure sur Windows Azure avec 2.2 des outils Python pour Visual Studio
description: "Découvrez comment toouse hello outils Python pour Visual Studio toocreate, une application d’eau qui stocke les données dans le stockage Table Azure et déployer hello web application tooAzure App Service Web Apps."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Bottle et stockage de tables Azure sur Azure avec Python Tools 2.2 pour Visual Studio
Dans ce didacticiel, nous allons utiliser [outils Python pour Visual Studio] toocreate simple interroge l’application web à l’aide d’un des exemples de modèles de PTVS hello. Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=GJXDGaEPy94).

application web de sondages Hello définit une abstraction pour son espace de stockage, afin que vous pouvez facilement basculer entre les différents types de référentiels (en mémoire, stockage de tables Azure, MongoDB).

Vous allez apprendre comment toocreate un stockage Azure de compte, comment tooconfigure hello web application toouse stockage de tables Azure et toopublish hello web application trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Consultez hello [centre de développement Python] autres articles qui couvrent le développement de Azure App Service Web Apps avec PTVS à l’aide d’eau, ballon Django web et infrastructures, avec les services MongoDB, stockage de tables Azure, MySQL et base de données SQL. Alors que cet article se concentre sur le Service d’applications, les étapes de hello sont similaires lors du développement [Azure Cloud Services].

## <a name="prerequisites"></a>Composants requis
* Visual Studio 2015
* [Python Tools 2.2 pour Visual Studio]
* [2.2 des outils Python pour Visual Studio exemples VSIX]
* [Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]
* [Python 2.7 32 bits] ou [Python 3.4 32 bits]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="create-hello-project"></a>Créer hello projet
Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle. Nous allons créer un environnement virtuel et installer les packages requis. Puis nous exécuterons application hello localement à l’aide de référentiel de hello par défaut en mémoire.

1. Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.
2. Hello des modèles de projet à partir de hello [2.2 des outils Python pour Visual Studio exemples VSIX] sont disponibles sous **Python**, **exemples**. Sélectionnez **interroge Bottle Web projet** et cliquez sur OK toocreate hello projet.
   
     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. Vous serez invité à tooinstall les packages externes. Sélectionnez **Installer dans un environnement virtuel**.
   
     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. Sélectionnez **Python 2.7** ou **Python 3.4** comme interpréteur de base hello.
   
     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. Vérifier que l’application hello fonctionne en appuyant sur `F5`. Par défaut, application hello utilise un référentiel en mémoire qui ne nécessite aucune configuration. Toutes les données sont perdues lorsque hello web server est arrêté.
6. Cliquez sur **Créer un exemple de sondage**, puis sur un sondage et un vote.
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Création d’un compte de stockage Azure
toouse des opérations de stockage, vous devez un compte de stockage Azure. Pour en créer un, procédez comme suit :

1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).
2. Cliquez sur hello **nouveau** icône en haut de hello à gauche de hello Portal, puis cliquez sur **données + stockage** > **compte de stockage**.  Cliquez sur hello **créer** bouton, puis donnez un nom unique à compte de stockage hello et créer un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md) pour celle-ci.
   
      ![Création rapide](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    Lorsque le compte de stockage hello a été créé, hello **Notifications** un vert clignote en bouton **réussite** et panneau du compte de stockage hello est ouvert tooshow qu’il appartient toohello nouvelle ressource groupe que vous avez créé.
3. Cliquez sur hello **clés d’accès** partie dans le panneau du compte de stockage hello. Prenez note du nom du compte hello et key1.
   
      ![Clés](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    Nous devons cette tooconfigure informations votre projet dans la section suivante de hello.

## <a name="configure-hello-project"></a>Configurer hello projet
Dans cette section, nous allons configurer notre compte de stockage application toouse hello que nous venons de créer. Ensuite, nous allons exécuter application hello localement.

1. Dans Visual Studio, cliquez avec le bouton droit sur le nœud de votre projet dans l’Explorateur de solutions, puis sélectionnez **Propriétés**. Cliquez sur hello **déboguer** onglet.
   
     ![Paramètres de débogage du projet](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Définir les valeurs des variables d’environnement requises par l’application hello dans hello **déboguer la commande de serveur**, **environnement**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Ceci permettra de définir les variables d’environnement hello lorsque vous **démarrer le débogage**. Si vous souhaitez hello variables toobe définie lorsque vous **démarrer sans débogage**, hello ensemble sous les mêmes valeurs **exécuter une commande de serveur** également.
   
   Vous pouvez également définir des variables d’environnement à l’aide de hello le panneau de configuration Windows. Il s’agit d’une meilleure option si vous souhaitez tooavoid stocke des informations d’identification dans le code source / fichier de projet. Notez que vous devez toorestart Visual Studio pour l’application de hello nouvel environnement valeurs toobe toohello disponible.
3. code Hello qui implémente le référentiel de stockage de Table Azure hello se trouve dans **models/azuretablestorage.py**. Consultez hello [documentation] pour plus d’informations sur la façon de toouse Service de Table à partir de Python.
4. Exécutez l’application hello avec `F5`. Les interrogations sont créées avec **créer des sondages exemple** et données hello soumises par le vote seront sérialisées dans le stockage Table Azure.
   
   > [!NOTE]
   > Hello environnement virtuel de Python 2.7 peut provoquer un arrêt de l’exception dans Visual Studio.  Appuyez sur `F5` toocontinue chargement hello web projet.
   > 
   > 
5. Parcourir toohello **sur** tooverify page qui hello d’application à l’aide de hello **Azure Table Storage** référentiel.
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Explorer hello stockage de Table Azure
Il est facile tooview et modifier des tables de stockage à l’aide de l’Explorateur de Cloud dans Visual Studio. Dans cette section, nous allons utiliser contenu de hello tooview de l’Explorateur de serveurs de tables d’application interroge hello.

> [!NOTE]
> Cela nécessite toobe Microsoft Azure Tools installé, qui sont disponible dans le cadre de hello [Azure SDK pour .NET].
> 
> 

1. Ouvrez **Cloud Explorer**. Développez **Comptes de stockage**, votre compte de stockage, puis **Tables**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Double-cliquez sur hello **interroge** ou **choix** contenu de hello tooview de table hello dans une fenêtre de document, ainsi que d’ajouter/supprimer/modifier des entités de table.
   
     ![Résultats de la requête de table](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publier hello web application tooAzure du Service d’applications
Hello Kit de développement .NET Azure fournit un moyen simple de toodeploy votre tooAzure d’application web du Service d’applications.

1. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **publier**.
   
     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Cliquez sur **Microsoft Azure Web Apps**.
3. Cliquez sur **nouveau** toocreate une application web.
4. Renseignez hello suivant des champs, cliquez sur **créer**.
   
   * **Nom de l’application web**
   * **Plan App Service**
   * **Groupe de ressources**
   * **Région**
   * Laissez **serveur de base de données** défini trop**aucune base de données**
5. Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.
6. Votre navigateur web s’ouvre automatiquement toohello publié web app. Si vous y accédez toohello sur la page, vous verrez qu’il utilise hello **In-Memory** référentiel, pas hello **Azure Table Storage** référentiel.
   
   C’est parce que les variables d’environnement hello ne sont pas définies sur l’instance d’applications Web hello dans Azure App Service, afin d’utiliser les valeurs par défaut hello spécifiés dans **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Configurer l’instance d’applications Web hello
Dans cette section, nous allons configurer les variables d’environnement pour l’instance d’applications Web hello.

1. Dans [Azure Portal], ouvrez le panneau de l’application hello web en cliquant sur **Parcourir** > **des Services d’application** > nom de votre application web.
2. Dans le volet de votre application web, cliquez sur **Tous les paramètres**, puis cliquez sur **Paramètres de l'application**.
3. Faites défiler vers le bas toohello **paramètres de l’application** section et définir des valeurs hello pour **référentiel\_nom**, **stockage\_nom** et  **STOCKAGE\_clé** comme décrit dans hello **projet hello de configurer** section ci-dessus.
   
     ![Paramètres de l'application](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Cliquez sur **Save**(Enregistrer). Une fois que vous avez reçu des notifications de hello que les modifications de hello ont été appliquées, cliquez sur **Parcourir** à partir du panneau principal de l’application hello Web.
5. Vous devez voir le travail d’application hello web comme prévu, à l’aide de hello **Azure Table Storage** référentiel.
   
   Félicitations !
   
     ![Navigateur web](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur les outils Python pour Visual Studio, d’eau et le stockage Table.

* [Documentation relative à Python Tools for Visual Studio]
  * [Projets web]
  * [Projets de service cloud]
  * [Débogage à distance sur Microsoft Azure]
* [Documentation relative à Bottle]
* [Azure Storage]
* [Kit de développement logiciel (SDK) Azure pour Python]
* [Comment tooUse hello Service de stockage de Table à partir de Python]

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentation]:../cosmos-db/table-storage-how-to-use-python.md
[Comment tooUse hello Service de stockage de Table à partir de Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK pour .NET]: http://azure.microsoft.com/downloads/
[outils Python pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[2.2 des outils Python pour Visual Studio exemples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Documentation relative à Bottle]: http://bottlepy.org/docs/dev/index.html
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Kit de développement logiciel (SDK) Azure pour Python]: https://github.com/Azure/azure-sdk-for-python
