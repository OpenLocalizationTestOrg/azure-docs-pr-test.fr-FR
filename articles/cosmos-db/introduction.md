---
title: aaaIntroduction tooAzure Cosmos DB | Documents Microsoft
description: "En savoir plus sur Azure Cosmos DB. Cette base de données multimodèle distribuée à l’échelle mondiale est conçue pour offrir une faible latence, une scalabilité élastique et une haute disponibilité."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>Bienvenue tooAzure Cosmos DB

Azure Cosmos DB est un service de base de données multimodèle mondialement distribué de Microsoft. À d’un simple clic hello, base de données Azure Cosmos vous permet de tooelastically et indépendamment débit de la mise à l’échelle et de stockage entre plusieurs régions géographiques de Azure. Il offre des garanties en termes de débit, de latence, de disponibilité et de cohérence avec des [contrats SLA complets](https://aka.ms/acdbsla), ce qu’aucun autre service de base de données ne peut offrir.

![Azure Cosmos DB est le service de base de données distribué mondialement de Microsoft qui propose une augmentation de la taille des instances, une faible latence, cinq modèles de cohérence et des contrats SLA offrant des garanties complètes](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Les solutions qui profitent des avantages de Azure Cosmos DB

N’importe quel [web, mobile, jeux et applications de IoT](use-cases.md) qui ont besoin de toohandle des quantités massives de lectures et écritures sur un [global](distribute-data-globally.md) l’échelle avec un temps de réponse faibles pour une grande variété de données tire parti de Azure Cosmos DB [garantie](https://azure.microsoft.com/support/legal/sla/cosmos-db/) disponibilité, un débit élevé, une latence faible et cohérence ajustables.

## <a name="key-capabilities"></a>Fonctionnalités clés
Comme un service de base de données distribuée globalement, base de données Azure Cosmos fournit hello suivant toohelp fonctionnalités vous générez des applications évolutives, très réactives :

* **Une distribution mondiale clé en main**
    * Vous pouvez [distribuer vos données](distribute-data-globally.md) nombre tooany de [régions Azure](https://azure.microsoft.com/regions/), avec hello [d’un simple clic](tutorial-global-distribution-documentdb.md). Ainsi, vous tooput vos données où vos utilisateurs, assurez latence minimale hello tooyour clients. 
    * À l’aide de DB Azure Cosmos multihébergement API, application hello toujours sait où hello plus proche de la région est et envoie les demandes toohello le plus proche du centre de données. Tout ceci est possible sans aucune modification de configuration, vous définissez votre région d’écriture et que plusieurs régions de lecture que vous le souhaitez et hello rest est traitée pour vous.

* **Plusieurs modèles de données et API populaires pour la consultation et l’interrogation des données**
    * Hello séquence d’enregistrement atom (ARS) données en fonction du modèle de base de données Azure Cosmos sur en mode natif prend en charge plusieurs modèles de données, y compris mais non limité toodocument, graphique, clé-valeur, table et les modèles de données en colonnes.
    * API pour hello suivant des modèles de données est pris en charge avec les kits de développement logiciel disponibles dans plusieurs langues :
        * [API DocumentDB](documentdb-introduction.md)
        * [API MongoDB](mongodb-introduction.md)
        * [API de table](table-introduction.md)
        * [API de graphique (Gremlin)](graph-introduction.md)
        * Des modèles de données supplémentaires seront bientôt disponibles 

* **Mettre à l’échelle le débit et le stockage de façon élastique et à la demande, dans le monde entier**
    * Faites évoluer facilement le débit de la base de données avec une granularité [par seconde](request-units.md) et modifiez-le à tout moment. 
    * Mettre à l’échelle de la taille de stockage [en toute transparence et automatiquement](partition-data.md) toohandle vos exigences de taille aujourd'hui et pour toujours.

* **Créer des applications hautement réactives et stratégiques**
    * Base de données Azure Cosmos garantit à faible latence de bout en bout à hello clients de tooits 99e centile. 
    * Pour un article de base de connaissances 1 classique, Cosmos DB garantit la latence de bout en bout de lectures sous 10 ms et écritures indexées sous 15 ms à 99e centile de hello, hello dans même région Azure. temps de latence médian de Hello sont nettement plus faible (inférieure à 5 ms).

* **Assurer une disponibilité en continu**
    * Disponibilité de 99,99 % dans une même région.
    * Déployer le nombre de tooany de [régions Azure](https://azure.microsoft.com/regions) pour une disponibilité élevée.
    * [Simulez la défaillance](regional-failover.md) d’une ou plusieurs régions avec comme garantie l’absence de perte de données. 

* **Écrire des applications distribuées de manière globale, hello bonne façon**
    * Cinq [modèles de cohérence](consistency-levels.md) les modèles fournissent un éventail de cohérence de type SQL forte tous hello cohérence éventuelle de façon semblable à tooNoSQL et chaque élément entre les deux. 
  
* **Garantie de remboursement**
    * Vos données sont accessibles rapidement ou vous êtes remboursé. 
    * [Contrats SLA](https://aka.ms/acdbsla) pour la disponibilité, la latence, le débit et la cohérence. 

* **Aucune gestion de schéma ou d’index de base de données**
    * Vous ne devez plus conserver le schéma et les index de base de données synchronisés avec le schéma de l’application. Les schémas ne sont plus utilisés. 
    * Moteur de base de données Azure Cosmos DB est entièrement indépendant du schéma, elle indexe automatiquement toutes les données hello il résultants sans nécessiter de schéma ou d’index et sert les requêtes extrêmement rapides. 

* **Faible coût total de possession**
    * Cinq fois tooten [plus rentable](https://aka.ms/cosmos-db-tco-paper) qu’une solution non gérée.
    * Prix trois fois moins élevé que DynamoDB.

## <a name="capability-comparison"></a>Comparaison des fonctionnalités

Base de données Cosmos Azure fournit des fonctionnalités de meilleures de hello de bases de données relationnelles et non relationnelles.

| Fonctionnalités | Bases de données relationnelles   | Bases de données non relationnelles (NoSQL) |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Diffusion mondiale | Non | Non | Oui, la distribution clé en main est disponible avec les API multihébergement dans plus de 30 régions.|
| Mise à l’échelle horizontale | Non | Oui | Oui, vous pouvez mettre le stockage et le débit à l’échelle indépendamment. | 
| Garanties de latence | Non | Oui | Oui, la latence de 99 % des lectures est inférieure à 10 ms et celle des écritures est inférieure à 15 ms. | 
| Haute disponibilité | Non | Oui | Oui, Cosmos DB est toujours activé, dispose de compromis, et fournit des options pour les basculements manuels et automatiques.|
| Modèle de données + API | Relationnel + SQL | Multi-modèle + API OSS | Multi-modèle + SQL + API OSS (autres fonctionnalités disponibles prochainement) |
| Contrats SLA | Oui | Non | Oui, les contrats SLA sont complets en termes de latence, de débit, de cohérence et de disponibilité. |


## <a name="next-steps"></a>Étapes suivantes
Bien démarrer avec Azure Cosmos DB grâce à l’un de nos guides de démarrage rapide :

* [Bien démarrer avec l’API DocumentDB d’Azure Cosmos DB](create-documentdb-dotnet.md)
* [Bien démarrer avec l’API MongoDB d’Azure Cosmos DB](create-mongodb-nodejs.md)
* [Bien démarrer avec l’API Graph d’Azure Cosmos DB](create-graph-dotnet.md)
* [Bien démarrer avec l’API Table d’Azure Cosmos DB](create-table-dotnet.md)
