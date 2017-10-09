---
title: "AAA « perspectives de créer de leçon du didacticiel 8 Azure Analysis Services | Documents Microsoft »"
description: "Décrit comment les perspectives toocreate dans hello projet du didacticiel Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Leçon 8 : Créer des perspectives

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous allez créer une perspective de ventes sur Internet. Une perspective correspond à un sous-ensemble visualisable d’un modèle qui fournit des points de vue précis, spécifiques à l’entreprise ou à l’application. Lorsqu’un utilisateur connecte tooa modèle à l’aide d’un point de vue, ils voient uniquement les objets de modèle (tables, colonnes, mesures, hiérarchies et KPI) en tant que champs définis dans cette perspective. toolearn, voir [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
objet de la table DimCustomer hello exclut les Hello perspective Internet Sales que vous créez dans cette leçon. Lorsque vous créez une perspective qui exclut certains objets de vue, cet objet existe toujours dans le modèle de hello. Cependant, ils ne s’affichent pas dans la liste de champs du client de création de rapports. Les colonnes et les mesures calculées, qu’elles soient ou non incluses dans une perspective, peuvent toujours effectuer des calculs à partir des données des objets exclus.  
  
objectif Hello de cette leçon est toodescribe comment toocreate perspectives et vous familiariser avec les outils de création du modèle tabulaire hello. Si vous développez ultérieurement des tables supplémentaires cette tooinclude modèle, vous pouvez créer des perspectives supplémentaires toodefine différents points de vue du modèle de hello, par exemple, l’inventaire et les ventes.  
  
Estimé temps toocomplete cette leçon : **cinq minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 7 : créer des indicateurs de Performance clés](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Créer des perspectives  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate une perspective Internet Sales  
  
1.  Cliquez sur hello **modèle** menu > **Perspectives** > **créer et gérer**.  
  
2.  Bonjour **Perspectives** boîte de dialogue, cliquez sur **nouvelle Perspective**.  
  
3.  Double-cliquez sur hello **nouvelle Perspective** en-tête de colonne, puis renommez **Internet Sales**.  
  
4.  Sélectionnez hello toutes les tables hello *sauf* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    Dans une prochaine leçon, vous utilisez hello analyser dans Excel fonctionnalité tootest cette perspective. Hello liste de champs de tableau croisé dynamique Excel inclut chaque table sauf la table DimCustomer de hello.  

## <a name="whats-next"></a>Et ensuite ?
[Leçon 9 : Créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
