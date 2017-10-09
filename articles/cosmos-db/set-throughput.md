---
title: "débit aaaProvision pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment tooset mis en service le débit de votre base de données Azure Cosmos containsers, collections, graphiques et les tables."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Définir le débit des conteneurs Azure Cosmos DB

Vous pouvez définir le débit pour les conteneurs de votre base de données Azure Cosmos Bonjour portail Azure ou à l’aide de hello kits de développement logiciel client. 

Hello tableau suivant répertorie le débit hello disponible pour les conteneurs :

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Conteneur à partition unique</strong></p></td>
            <td valign="top"><p><strong>Conteneur partitionné</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Débit minimal</p></td>
            <td valign="top"><p>400 unités de demande par seconde</p></td>
            <td valign="top"><p>2 500 unités de requête par seconde</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Débit maximal</p></td>
            <td valign="top"><p>10 000 unités de demande par seconde</p></td>
            <td valign="top"><p>Illimité</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>débit de hello tooset à l’aide de hello portail Azure

1. Dans une nouvelle fenêtre, ouvrez hello [portail Azure](https://portal.azure.com).
2. Dans la barre de gauche hello, cliquez sur **base de données Azure Cosmos**, ou cliquez sur **plus Services** au bas de hello, puis faites défiler trop**bases de données**, puis cliquez sur **base de données Azure Cosmos**.
3. Sélectionnez votre compte Azure Cosmos DB.
4. Dans la nouvelle fenêtre de hello, cliquez sur **Explorateur de données (version préliminaire)** dans le menu de navigation hello.
5. Dans la nouvelle fenêtre de hello, votre base de données et le conteneur, puis cliquez sur **échelle & paramètres**.
6. Dans la nouvelle fenêtre de hello, tapez Bonjour nouvelle valeur de débit Bonjour **débit** zone, puis cliquez sur **enregistrer**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>débit de hello tooset à l’aide de hello API DocumentDB pour .NET

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Forum Aux Questions sur le débit

**Puis-je définir mon accessible sans de débit à 400 ur/s ?**

400 ur/s est le débit minimal de hello sont disponible sur les collections de partitions uniques Cosmos DB (2500 ur/s est hello minimale pour les collections partitionnées). Demander des unités sont définis dans des intervalles de 100 ur/s, mais le débit ne peut pas être défini too100 ur/s ou toute valeur inférieure à 400 ur/s. Si vous avez besoin d’une méthode économique de toodevelop et Cosmos de base de données de test, vous pouvez utiliser hello libre [Azure Cosmos DB émulateur](local-emulator.md), que vous pouvez déployer localement sans frais. 

**Comment définir le débit à l’aide de hello MongoDB API ?**

Il n’existe aucun débit de tooset extension MongoDB API. Hello recommandation est toouse hello API DocumentDB, comme indiqué dans [débit de hello tooset à l’aide de hello API DocumentDB pour .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur la configuration et de cours planète à l’échelle avec Cosmos DB, consultez [de partitionnement et de mise à l’échelle avec Cosmos DB](partition-data.md).
