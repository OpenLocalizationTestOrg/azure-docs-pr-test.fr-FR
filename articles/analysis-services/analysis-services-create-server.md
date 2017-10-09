---
title: aaaCreate un serveur Analysis Services dans Azure | Documents Microsoft
description: "Découvrez comment toocreate un serveur Analysis Services instance dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Création d’un serveur Azure Analysis Services dans le portail Azure
Cet article vous guide lors du processus de création d’une ressource de serveur Analysis Services dans votre abonnement Azure.

## <a name="before-you-begin"></a>Avant de commencer
toocomplete ce démarrage rapide, vous devez :

* **Abonnement Azure**: visitez [d’évaluation gratuite Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un compte.
* **Azure Active Directory** : votre abonnement doit être associé à un locataire Azure Active Directory. Et bien, vous devez toobe tooAzure connecté avec un compte dans Azure Active Directory. Les comptes Microsoft ne sont pas pris en charge. toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).
* **Groupe de ressources** : utilisez un groupe de ressources existant ou [créez-en un](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> La création d’un serveur peut donner lieu à un nouveau service facturable. toolearn, voir [Analysis Services tarification](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate un serveur dans le portail Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).  
2. Cliquez sur **+ Nouveau** > **Données + analyse** > **Analysis Services**.
3. Bonjour **Analysis Services** panneau, renseignez les champs hello requis, puis appuyez sur **créer**.
   
    ![Créer un serveur](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Nom du serveur**: Type d’un serveur de hello tooreference nom unique utilisé.
   * **Abonnement**: sélectionnez l’abonnement hello facture de ce serveur à.
   * **Groupe de ressources**: ces conteneurs sont conçu toohelp vous gérez une collection de ressources Azure. toolearn, voir [groupes de ressources](../azure-resource-manager/resource-group-overview.md).
   * **Emplacement**: ordinateurs hôtes emplacement de centre de données Azure ce hello serveur. Choisissez l’emplacement le plus proche de votre plus grande base d’utilisateurs.
   * **Niveau de tarification** : sélectionnez un niveau de tarification. Les modèles tabulaires des too400 Go sont pris en charge. toolearn, voir [tarification Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Cliquez sur **Créer**.

La création prend généralement moins d’une minute, souvent quelques secondes seulement. Si vous avez sélectionné **ajouter tooPortal**, accédez à toosee de portail tooyour votre nouveau serveur. Naviguer trop**davantage de services** > **Analysis Services** toosee si votre serveur est prêt.

 ![tableau de bord](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez créé votre serveur, vous pouvez [déployer un modèle](analysis-services-deploy.md) tooit à l’aide de SSDT ou SSMS.

Si un modèle de déploiement tooyour serveur connecte à des sources de données tooon local, vous devez tooinstall une [passerelle de données locale](analysis-services-gateway.md) sur un ordinateur de votre réseau.

