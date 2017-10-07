---
title: "aaaDeploy tooAzure Analysis Services à l’aide de SSDT | Documents Microsoft"
description: "Découvrez comment toodeploy un tooan de modèle tabulaire Azure Analysis Services server à l’aide de SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Déployer un modèle à partir de SSDT
Une fois que vous avez créé un serveur dans votre abonnement Azure, vous êtes prêt toodeploy un tooit de base de données de modèle tabulaire. Vous pouvez utiliser SQL Server Data Tools (SSDT) toobuild et déployer un projet de modèle tabulaire sur lequel vous travaillez. 

## <a name="prerequisites"></a>Composants requis
tooget démarré, vous devez :

* **Serveur Analysis Services** dans Azure. toolearn, voir [créer un serveur Azure Analysis Services](analysis-services-create-server.md).
* **Projet de modèle tabulaire** dans SSDT ou un modèle tabulaire existant hello 1200 au niveau de compatibilité supérieur. Vous ne l’avez jamais fait ? Essayez de hello [didacticiel de modélisation tabulaire vente Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).
* **Passerelle locale** -si une ou plusieurs sources de données sont localement dans le réseau de votre organisation, vous devez tooinstall une [passerelle de données locale](analysis-services-gateway.md). passerelle de Hello est nécessaire pour la connexion à votre serveur dans le cloud de hello tooyour des données sources tooprocess et l’actualisation des données locales dans le modèle de hello.

> [!TIP]
> Avant de déployer, assurez-vous que vous pouvez traiter les données de salutation dans vos tables. Dans SSDT, cliquez sur **Modèle** > **Traiter** > **Traiter tout**. Si le traitement échoue, vous ne pourrez pas procéder au déploiement.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy un modèle tabulaire à partir de SSDT

1. Avant de déployer, vous devez le nom du serveur tooget hello. Dans **portail Azure** > serveur > **vue d’ensemble** > **nom du serveur**, copier le nom de serveur hello.
   
    ![Obtenir le nom du serveur dans Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. Dans SSDT > **l’Explorateur de solutions**, projet de hello avec le bouton droit > **propriétés**. Ensuite, dans **déploiement** > **Server** collez le nom du serveur hello.   
   
    ![Coller le nom du serveur dans la propriété du serveur de déploiement](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Propriétés**, puis cliquez sur **Déployer**. Vous pouvez être invité à toosign dans tooAzure.
   
    ![Déployer tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    État du déploiement s’affiche dans les deux fenêtres de sortie hello et déployer.
   
    ![état du déploiement](./media/analysis-services-deploy/aas-deploy-status.png)

C’est tout est tooit !


## <a name="troubleshooting"></a>Résolution des problèmes
Si le déploiement échoue lors du déploiement des métadonnées, il est probable, car SSDT n’a pas pu se connecter à tooyour server. Assurez-vous que vous pouvez vous connecter serveur tooyour à l’aide de SSMS. Vérifiez que hello propriété du serveur de déploiement pour le projet de hello est correct.

Si le déploiement échoue sur une table, il est probable, car votre serveur n’a pas pu se connecter de source de données tooa. Si votre source de données est locale dans le réseau de votre organisation, être tooinstall vraiment une [passerelle de données locale](analysis-services-gateway.md).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez votre serveur déployé tooyour de modèle tabulaire, vous êtes prêt tooconnect tooit. Vous pouvez [connecter tooit avec SSMS](analysis-services-manage.md) toomanage il. Et vous pouvez [se connecter à l’aide d’un outil client de tooit](analysis-services-connect.md) comme Power BI, Power BI Desktop, ou Excel et la création de rapports de début.

