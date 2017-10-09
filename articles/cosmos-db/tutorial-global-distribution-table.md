---
title: "didacticiel de distribution globale aaaAzure Cosmos DB pour l’API de Table | Documents Microsoft"
description: "Découvrez comment à l’aide de distribution globale de base de données Azure Cosmos toosetup hello des API de Table."
services: cosmos-db
keywords: distribution mondiale, Table
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>À l’aide de distribution globale de base de données Azure Cosmos toosetup comment hello des API de Table

Dans cet article, nous montrons comment toouse hello distribution globale de base de données Azure Cosmos toosetup portail Azure et connectez-vous à l’aide de hello API (version préliminaire) de la Table.

Cet article traite des hello tâches suivantes : 

> [!div class="checklist"]
> * Configurer la distribution globale à l’aide de hello portail Azure
> * Configurer la distribution globale à l’aide de hello [API de Table](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Connexion tooa la région préférée à l’aide de hello API de Table

Dans l’avantage de tootake d’ordre de [distribution globale](distribute-data-globally.md), les applications clientes peuvent spécifier hello classés de liste de préférence des régions toobe utilisé tooperform les opérations de document. Cela est possible en définissant les hello `TablePreferredLocations` valeur de configuration dans la configuration de l’application hello pour l’aperçu de hello SDK Azure Storage. Selon la configuration du compte de base de données Azure Cosmos hello, disponibilité régionale actuelle hello liste de préférence spécifié, hello la plupart des point de terminaison optimale est sélectionnée par hello SDK Azure Storage tooperform écrire et opérations de lecture.

Hello `TablePreferredLocations` doit contenir une liste séparée par des virgules des emplacements (multihébergement) par défaut pour les lectures. Chaque instance de client peut spécifier un sous-ensemble de ces régions dans l’ordre de hello préféré pour les lectures de faible latence. les régions Hello doivent être nommées à l’aide de leurs [afficher les noms des](https://msdn.microsoft.com/library/azure/gg441293.aspx), par exemple, `West US`.

Toutes les lectures seront envoyés toohello première disponible région Bonjour `TablePreferredLocations` liste. En cas de demande de hello, client de hello échouer la région de hello liste toohello suivante et ainsi de suite.

Hello SDK tente uniquement tooread de régions hello spécifié dans `TablePreferredLocations`. Ainsi, par exemple, si hello compte de base de données est disponible dans trois régions, mais les clients hello spécifie uniquement deux des hello régions non-écriture pour `TablePreferredLocations`, alors aucune lecture ne sera pris en charge en dehors de la région d’écriture hello, même dans les cas de hello de basculement.

Hello Kit de développement logiciel enverra automatiquement région pour l’écriture de toutes les écritures toohello actuelle.

Si hello `TablePreferredLocations` propriété n’est pas définie, toutes les demandes seront pris en charge à partir de la zone d’écriture en cours hello.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

C’est ici que s’achève ce didacticiel. Vous pouvez apprendre comment toomanage hello la cohérence de votre compte de réplication globale en lisant [niveaux de cohérence dans la base de données Azure Cosmos](consistency-levels.md). Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Azure Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Configurer la distribution globale à l’aide de hello portail Azure
> * Configurer la distribution globale à l’aide de hello APIs DocumentDB

Vous pouvez maintenant toolearn de didacticiel suivant toohello comment toodevelop localement à l’aide de hello émulateur local de base de données Azure Cosmos.

> [!div class="nextstepaction"]
> [Développer localement avec l’émulateur de hello](local-emulator.md)
