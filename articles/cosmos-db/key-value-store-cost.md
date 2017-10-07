---
title: "aaaAzure DB Cosmos en tant que valeur de clé magasin : vue d’ensemble des coûts | Documents Microsoft"
description: "Découvrez hello faible coût d’à l’aide de la base de données Azure Cosmos en tant qu’un magasin de valeur de clé."
keywords: "magasin de valeurs de clés"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure Cosmos DB comme magasin de valeurs de clés – Synthèse des coûts

Azure Cosmos DB est un service de base de données multi-modèles, distribué dans le monde entier, qui permet de créer facilement des applications à grande échelle et à haute disponibilité. Par défaut, base de données Azure Cosmos indexe automatiquement toutes les données hello que résultants, efficacement. Vous pouvez ainsi créer des requêtes [SQL](documentdb-sql-query.md) (et [JavaScript](programming.md)) rapides et cohérentes sur n’importe quel type de données. 

Cet article décrit le coût de hello de base de données Azure Cosmos simple écriture et lorsqu’il est utilisé comme un magasin de clé/valeur des opérations de lecture. Les opérations d’écriture incluent des insertions, des remplacements, des suppressions et des upserts de documents. Outre ce qui garantit la haute disponibilité de 99,99 %, les offres de base de données Azure Cosmos garantie < latence de 10 ms pour les lectures et < latence à 15 ms pour hello (indexé) écrit respectivement 99e centile de hello. 

## <a name="why-we-use-request-units-rus"></a>Pourquoi utiliser des unités de requête (RU) ?

Les performances de base de données Cosmos Azure sont basé sur hello approvisionné [unités de demande](request-units.md) (RU) pour la partition de hello. Hello de configuration est une deuxième granularité et est acheté dans RUs par seconde et RUs/min ([pas confondue avec hello toutes les heures de facturation le toobe](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs doivent être considérées comme une devise qui simplifie le provisionnement de hello du débit requis pour l’application hello. Nos clients n’ont pas de toothink de différencier les lire et écrire des unités de capacité. modèle seule devise de Hello de RUs crée l’efficacité de capacité de hello configuré tooshare entre les lectures et écritures. Ce modèle de capacité déployée permet hello service tooprovide un débit prévisible et cohérent, garantie d’une latence faible et une haute disponibilité. Enfin, nous utilisons un débit toomodel RU, mais chaque RU approvisionné a également un nombre défini de ressources (mémoire, Core). Les unités de requête par seconde ne correspondent pas uniquement à des opérations d’E/S par seconde.

Comme un système de base de données distribuée globalement, Cosmos DB est hello uniquement le service Azure qui fournit un contrat SLA sur la latence, le débit et la cohérence dans la disponibilité de toohigh d’ajout. débit Hello que vous approvisionner est appliqué tooeach des régions hello associé à votre compte de base de données de base de données Cosmos. Pour les lectures, Cosmos DB offre plusieurs bien défini [niveaux de cohérence](consistency-levels.md) pour vous toochoose à partir de. 

Hello montre le tableau suivant hello nombre RUs requis tooperform lecture et écriture des transactions en fonction de la taille du document de 1 Ko et 100 Kbits/s.

|Taille de l’élément|1 lecture|1 écriture|
|-------------|------|-------|
|1 Ko|1 unité de requête|5 unités de requête|
|100 Ko|10 unités de requête|50 unités de requête|

## <a name="cost-of-reads-and-writes"></a>Coût des lectures et écritures

Si vous configurez les 1 000 ur/s, cela les montants too3.6m ur/heure et présente un coût de 0,08 $ pour hello heure (hello des États-Unis et en Europe). Pour un document d’une taille de 1 Ko, vous pouvez donc consommer 3,6 millions de lectures ou 0,72 million d’écritures (3,6 millions d’unités de requête/5) en utilisant le débit approvisionné. Toomillion normalisée lit et écrit, hello coût serait $0,022 /m lectures (0,08 $ / 3,6) et $0.111/ m écrit (0,08 $ / 0,72). coût d’Hello millions devient minimale comme indiqué dans le tableau hello ci-dessous.

|Taille de l’élément|1 million de lectures|1 million d’écritures|
|-------------|-------|--------|
|1 Ko|0,022 $|0,111 $|
|100 Ko|0,222 $|1,111 $|


Plupart des objets blob de base hello ou objet magasins des frais de services 0,40 $ par million de transaction de lecture et de 5 $ par million d’écriture transaction. Si l’utilisation optimale, Cosmos DB peut être % too98 moins chère que ces autres solutions (pour les transactions de 1 Ko).

## <a name="next-steps"></a>Étapes suivantes

Consultez régulièrement cette rubrique pour obtenir de nouveaux articles sur l’optimisation de l’approvisionnement des ressources Azure Cosmos DB. Dans hello en attendant, vous pouvez toouse libre notre [calculatrice de RU](https://www.documentdb.com/capacityplanner).

