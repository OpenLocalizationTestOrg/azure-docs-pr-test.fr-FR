---
title: aaaManage logic apps dans Visual Studio - Azure Logic Apps | Documents Microsoft
description: "Gestion d’applications logiques et d’autres ressources à l’aide de Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Gestion de vos applications logiques à l’aide de Visual Studio Cloud Explorer

Bien que hello [portail Azure](https://portal.azure.com/) offre un excellent moyen de vous toodesign et gérer Azure Logic Apps, vous pouvez utiliser Visual Studio Cloud Explorer pour la gestion de nombreuses ressources Azure, y compris les applications de la logique. Visual Studio Cloud Explorer vous permet de parcourir, de gérer, de modifier et de télécharger des applications logiques publiées. Les tâches de gestion incluent notamment l’activation, la désactivation et l’affichage de l’historique des exécutions. 

Avant de pouvoir accéder à vos applications logiques et les gérer dans Visual Studio, installez et configurez ces outils Visual Studio pour Azure Logic Apps. 

## <a name="prerequisites"></a>Composants requis

* [Visual Studio 2015 ou Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Web toohello d’accès lorsque vous utilisez le concepteur incorporé hello

## <a name="install-visual-studio-tools-for-logic-apps"></a>Installer les outils Visual Studio pour Logic Apps

Après avoir installé les composants requis de hello, téléchargez et installez les outils d’applications logique hello Azure pour Visual Studio.

1. Ouvrez Visual Studio. Sur hello **outils** menu, sélectionnez **Extensions et mises à jour**.
2. Développez hello **Online** catégorie, vous pouvez rechercher en ligne Bonjour galerie Visual Studio.
3. Parcourez les résultats ou recherchez **Logic Apps** jusqu’à ce que vous trouviez **Outils Azure Logic Apps pour Visual Studio**.
4. toodownload et installer une extension hello, cliquez sur **télécharger**.
5. Redémarrez Visual Studio après l’installation.

> [!NOTE]
> hello de toodownload Azure logique applications Tools pour Visual Studio accéder directement, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Recherche d’applications logiques dans Cloud Explorer

1.  tooopen Cloud Explorer, sur hello **vue** menu, choisissez **Cloud Explorer**.
2.  Recherchez votre application logique, par groupe de ressources ou par type de ressource. 

    * Si vous y accédez par type de ressource, sélectionnez votre abonnement Azure, développez hello **Logic Apps** section et sélectionnez votre application logique. 
    * Si vous y accédez par groupe de ressources, développez le groupe de ressources hello où votre application logique et sélectionnez votre application logique.

    les commandes tooview pour votre application logique, avec le bouton droit de votre application logique, ou bas hello du Cloud Explorer, choisissez hello **Actions** menu.

    ![Accès à votre application logique](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Modifier votre application logique avec le Concepteur d’applications logiques

À partir du Cloud Explorer, vous pouvez ouvrir une application actuellement déployé logique Bonjour même concepteur que vous utilisez dans hello portail Azure. 

* tooedit votre application logique, dans l’Explorateur de Cloud, avec le bouton droit de votre application logique, puis sélectionnez **ouvert avec l’éditeur d’application logique**. 

* toopublish votre toohello mises à jour le cloud, choisissez **publier**. 

* toostart une nouvelle exécution, choisissez **exécuter un déclencheur**.

![Concepteur Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

À partir du concepteur hello, vous pouvez également **télécharger** une application logique. Cette action est la définition de la logique d’application hello automatiquement et enregistre la définition de hello sous la forme d’un modèle de déploiement Azure Resource Manager. Vous pouvez ajouter ce projet de déploiement modèle tooyour groupe de ressources Azure.

## <a name="browse-your-logic-app-run-history"></a>Parcourir votre historique des exécutions d’une application logique

hello tooview l’historique de votre application logique, d’exécution avec le bouton droit de votre application logique, puis sélectionnez **ouvrir l’historique d’exécution**. tooreorder votre historique d’exécution basée sur n’importe quel en-tête de colonne de hello indiqué, sélectionnez Propriétés hello.

![Historique d’exécution](media/logic-apps-manage-from-vs/runs.png)

hello tooshow l’historique d’une instance d’exécution pour pouvoir consulter hello exécuter des résultats, y compris les entrées de hello et des sorties à partir de chaque étape, double-cliquez sur un des hello exécuter des instances.

![Exécution des résultats de l’historique, des entrées et des sorties](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Étapes suivantes

* [Créez votre première application logique](logic-apps-create-a-logic-app.md)
* [Concevoir, créer et déployer des applications logiques dans Visual Studio](logic-apps-deploy-from-vs.md)
* [Afficher des exemples et des scénarios courants](logic-apps-examples-and-scenarios.md)
* [Vidéo : Automatisez vos processus métiers avec Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Vidéo : Intégrez vos systèmes à Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
