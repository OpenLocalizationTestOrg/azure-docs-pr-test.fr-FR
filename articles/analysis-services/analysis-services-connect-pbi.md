---
title: aaaConnect tooAzure Analysis Services avec Power BI | Documents Microsoft
description: "Découvrez comment tooconnect tooan Azure Analysis Services server à l’aide de Power BI."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Se connecter avec Power BI

Une fois que vous avez créé un serveur dans Azure et déployé un modèle tabulaire de tooit, les utilisateurs de votre organisation sont tooconnect prêt et commencent à Explorer les données. 

> [!TIP]
> Être vraiment toouse hello version la plus récente de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Se connecter à Power BI Desktop

1. Dans Power BI Desktop, cliquez sur **Obtenir les données** > **Azure** > **Base de données Azure Analysis Services**.

2. Dans **serveur**, entrez le nom du serveur hello. 
    
    Être une URL complète que tooinclude hello. Par exemple, asazure://westcentralus.asazure.windows.net/advworks.

3. Dans **base de données**, si vous connaissez le nom hello de base de données de modèle tabulaire hello ou perspective que vous souhaitez tooconnect à coller ici. Sinon, vous pouvez laisser ce champ vide et sélectionner une base de données ou une perspective ultérieurement.

4. Laissez la valeur par défaut hello **connexion live** option, puis appuyez sur **Connect**. 

5. Entrez vos informations d’identification si elles vous sont demandées. 

6. Dans **Navigator**, développez hello serveur, puis sélectionnez le modèle de hello ou une perspective vous souhaitez tooconnect, puis à cliquer sur **connexion**. Cliquez sur un tooshow de modèle ou de perspective de tous les objets hello pour cette vue.

    modèle de Hello s’ouvre dans Power BI Desktop avec un rapport vierge en mode rapport. liste de champs Hello affiche tous les objets de modèle de non masqués. État de la connexion s’affiche dans le coin inférieur droit de hello.

## <a name="connect-in-power-bi-service"></a>Se connecter à Power BI Desktop (service)

1. Créez un fichier Power BI Desktop qui dispose d’un modèle de tooyour de connexion active sur votre serveur.
2. Dans [Power BI](https://powerbi.microsoft.com), cliquez sur **Obtenir les données** > **Fichiers**. Recherchez et sélectionnez votre fichier.



## <a name="see-also"></a>Voir aussi
[Se connecter tooAzure Analysis Services](analysis-services-connect.md)   
[Fournisseurs de données pour la connexion à Azure Analysis Services](analysis-services-data-providers.md)

