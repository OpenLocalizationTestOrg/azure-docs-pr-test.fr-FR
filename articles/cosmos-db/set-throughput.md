---
title: "Approvisionner le débit pour Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment définir un débit approvisionné pour vos conteneurs, collections, graphes et tables Azure Cosmos DB."
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
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Définir le débit des conteneurs Azure Cosmos DB

Vous pouvez définir le débit de vos conteneurs Azure Cosmos DB dans le portail Azure ou à l’aide des SDK clients. 

Le tableau suivant répertorie les débits disponibles pour les conteneurs :

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

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a>Pour définir le débit à l’aide du portail Azure

1. Dans une nouvelle fenêtre, ouvrez le [portail Azure](https://portal.azure.com).
2. Dans la barre de gauche, cliquez sur **Azure Cosmos DB** ou sur **Plus de services** en bas, accédez à **Bases de données**, puis sélectionnez **Azure Cosmos DB**.
3. Sélectionnez votre compte Azure Cosmos DB.
4. Dans la nouvelle fenêtre, cliquez sur **Explorateur de données (préversion)** dans le menu de navigation.
5. Dans la nouvelle fenêtre, développez la base de données et le conteneur, puis cliquez sur **Scale & Settings** (Mise à l’échelle & paramètres).
6. Dans la nouvelle fenêtre, tapez la nouvelle valeur de débit dans la zone **Débit**, puis cliquez sur **Enregistrer**.

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a>Pour définir le débit à l’aide de l’API DocumentDB pour .NET

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Forum Aux Questions sur le débit

**Puis-je définir mon débit sur une valeur inférieure à 400 unités de demande/s ?**

Cette valeur de 400 unités de demande/s correspond au débit minimal disponible sur les collections à partition unique Cosmos DB (une valeur de 2 500 unités de demande/s correspond à la valeur minimale pour les collections partitionnées). Les unités de demande sont définies par intervalles de 100 unités de demande/s, mais le débit ne peut pas avoir la valeur 100 unités de demande/s ou toute valeur inférieure à 400 unités de demande/s. Si vous recherchez une méthode économique pour développer et tester Cosmos DB, vous pouvez utiliser gratuitement l’[Émulateur Azure Cosmos DB](local-emulator.md), que vous pouvez déployer localement sans frais. 

**Comment définir le débit à l’aide de l’API MongoDB ?**

Il n’existe aucune extension d’API MongoDB pour définir le débit. Nous vous recommandons d’utiliser l’API DocumentDB, comme indiqué dans [Pour définir le débit à l’aide de l’API DocumentDB pour .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’approvisionnement et la mise à l’échelle avec Cosmos DB, consultez [Partitioning and scaling with Cosmos DB (Partitionnement et mise à l’échelle avec Cosmos DB)](partition-data.md).
