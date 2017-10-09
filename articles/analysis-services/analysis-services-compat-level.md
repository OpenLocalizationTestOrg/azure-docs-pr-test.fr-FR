---
title: "niveau de compatibilité de modèle aaaData dans Azure Analysis Services | Documents Microsoft"
description: "Présentation du niveau de compatibilité des modèles de données tabulaires."
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
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Niveau de compatibilité pour les modèles tabulaires Analysis Services

*Niveau de compatibilité* fait référence à des comportements spécifiques aux toorelease dans Analysis Services moteur de hello. Niveau de compatibilité toohello modifications qu’il coïncide avec les versions principales de SQL Server. Ces modifications sont également implémentées dans parité de toomaintain Azure Analysis Services entre les deux plateformes. Les modifications du niveau de compatibilité affectent également les fonctionnalités disponibles dans vos modèles tabulaires. Par exemple, DirectQuery et les métadonnées de l’objet sous forme de tableau ont des implémentations différentes en fonction du niveau de compatibilité hello. 

Azure Analysis Services prend en charge les niveaux de compatibilité hello 1200 et 1400 les modèles tabulaires.

niveau de compatibilité plus récent Hello est 1400. Ce niveau coïncide avec SQL Server 2017 Analysis Services. Principales fonctionnalités hello 1400 au niveau de compatibilité sont les suivantes :

*  Nouvelle infrastructure pour la connectivité de données et l’importation dans les modèles tabulaires avec prise en charge des API TOM et des scripts TMSL. Cette nouvelle fonctionnalité permet la prise en charge de sources de données supplémentaires, comme le stockage blob Azure.
*  Fonctionnalités de transformation de données et de mashup des données à l’aide d’expressions Obtenir les données et M.
*  Les mesures prennent en charge une propriété Lignes de détails avec une expression DAX. Cette propriété Active les outils clients tels que toodrill Microsoft Excel toodetailed des données à partir d’un rapport. Par exemple, lorsque les utilisateurs consultent le total des ventes pour une région ou le mois, ils peuvent afficher les détails de la commande hello associé. 
*  Sécurité au niveau de l’objet de table et de colonne noms en outre toohello des données au sein de celles-ci.
*  Prise en charge améliorée des hiérarchies déséquilibrées.
*  Amélioration des performances et de la surveillance.
  
## <a name="set-compatibility-level"></a>Définir le niveau de compatibilité 
 Lorsque vous créez un nouveau projet de modèle tabulaire dans SSDT, vous pouvez spécifier le niveau de compatibilité hello sur hello **Générateur de modèles tabulaires** boîte de dialogue. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Si vous sélectionnez hello **ne plus afficher ce message** option, tous les projets suivants utilisent niveau de compatibilité de hello vous avez spécifié comme valeur par défaut hello. Vous pouvez modifier le niveau de compatibilité par défaut hello dans SSDT sous **outils** > **Options**.  
  
 tooupgrade un projet de modèle tabulaire existant dans SSDT, jeu hello **le niveau de compatibilité** propriété hello modèle **propriétés** fenêtre. Gardez à l’esprit, la mise à niveau le niveau de compatibilité hello est irréversible.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Vérifier le niveau de compatibilité d’une base de données de modèles tabulaires dans SQL Server Management Studio 
 Dans SSMS, cliquez sur le nom de base de données hello > **propriétés** > **le niveau de compatibilité**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Vérifier le niveau de compatibilité pris en charge pour un serveur dans SSMS  
 Dans SSMS, cliquez sur le nom du serveur hello > **propriétés** > **pris en charge un niveau de compatibilité**.  
  
 Cette propriété spécifie hello plus haut niveau de compatibilité d’une base de données qui s’exécutent sur serveur hello (à l’exception de la version préliminaire). Hello pris en charge le niveau de compatibilité ne peut pas être modifié.  

## <a name="next-steps"></a>Étapes suivantes
  [Créer un modèle dans le portail Azure](analysis-services-create-model-portal.md)   
  [Gérer Analysis Services](analysis-services-manage.md)  
