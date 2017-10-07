---
title: "aaaHow tooview liées à des ressources de données dans Azure Data Catalog | Documents Microsoft"
description: "Cet article explique comment tooview associés à des ressources de données d’une ressource de données sélectionnée dans Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Comment tooview associées à des ressources de données dans Azure Data Catalog ?
Azure Data Catalog vous permet de tooview données actifs tooa connexes sélectionné données actif et affichage des relations entre elles. 

## <a name="supported-data-sources"></a>Sources de données prises en charge 
Lorsque vous inscrivez des ressources de données à partir de hello les sources de données suivantes, Azure Data Catalog enregistre automatiquement les métadonnées sur les relations de jointure entre les ressources de données hello sélectionné. 

- SQL Server
- Base de données SQL Azure
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Afficher les ressources de données associées
ressources de données tooview sont le jeu de données connexes tooa sélectionné, utilisez hello **relations** onglet comme indiqué dans hello suivant image : 

![Azure Data Catalog - Afficher les ressources de données associées](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

Dans cet exemple, il existe deux relations pour hello sélectionné **ProductSubcategory** ressource de données : 

- Colonne ProductSubcategoryID de la table Product de hello a une relation de clé étrangère avec la colonne ProductSubcategoryID de la table ProductSubcategory de hello sélectionné. 
- Colonne ProductCategoryID de table ProductSubCategory de hello a une relation de clé étrangère avec la colonne ProductCategoryID de table ProductCategory de hello sélectionné.

> [!NOTE]
> Notez la direction hello de flèche hello dans l’arborescence de relations hello.  

toosee plus d’informations, telles que nom complet de hello de colonne de hello, déplacez la souris de hello sur et vous voyez un toohello similaire de fenêtre contextuelle suit l’image : 

![Azure Data Catalog - Menu contextuel Relation](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude des relations entre des ressources qui ont déjà été inscrit, réinscrivez ces ressources.

## <a name="next-steps"></a>Étapes suivantes
- [Comment les ressources de données toomanage](data-catalog-how-to-manage.md)
