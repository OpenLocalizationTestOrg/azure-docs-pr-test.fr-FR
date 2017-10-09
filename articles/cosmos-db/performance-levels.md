---
title: les niveaux de performance aaaDocumentDB API | Documents Microsoft
description: "Découvrez comment les niveaux de performance API DocumentDB vous activer débit tooreserve par conteneur."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Retrait des niveaux de performance S1, S2 et S3 hello

> [!IMPORTANT] 
> Hello S1, S2 et S3 niveaux de performance mentionnés dans cet article seront retirés et ne sont plus disponibles pour les nouveaux comptes d’API DocumentDB.
>

Cet article fournit une vue d’ensemble des niveaux de performance S1, S2 et S3 et explique comment les collections de hello qui utilisent ces niveaux de performance seront migrés toosingle les collections de partitions sur le 1er août 2017. Après avoir lu cet article, vous serez hello en mesure de tooanswer suivant questions :

- [Pourquoi les performances de S1, S2 et S3 hello niveaux sera mis hors service ?](#why-retired)
- [Comment partitionnées et les collections de partition unique comparé toohello S1, S2, S3 des niveaux de performances ?](#compare)
- [Que faire besoin d’accès ininterrompu à toodo tooensure toomy données ?](#uninterrupted-access)
- [Comment ma collection changera après la migration de hello ?](#collection-change)
- [Comment me facturation, modifié une fois que je suis toosingle migré les collections de partitions ?](#billing-change)
- [Que se passe-t-il si j’ai besoin de plus de 10 Go de stockage ?](#more-storage-needed)
- [Puis-je changer entre les niveaux de performance hello S1, S2 et S3 avant le 1er août 2017 ?](#change-before)
- [Comment serai-je informé de la migration de ma collection ?](#when-migrated)
- [Comment migrer à partir de hello S1, S2, S3 performances niveaux toosingle les collections de partitions sur mon propre ?](#migrate-diy)
- [Quelles sont les conséquences pour moi en tant que client Contrat Entreprise ?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Pourquoi les performances de S1, S2 et S3 hello niveaux sera mis hors service ?

les niveaux de performance S1, S2 et S3 Hello ne pas offre hello une souplesse qui offre des collections de l’API DocumentDB. Avec hello S1, S2, S3 les niveaux de performance, les deux hello débit et capacité de stockage ont été prédéfinis et n’offrait pas d’élasticité. Base de données Azure Cosmos propose désormais hello capacité toocustomize votre débit et stockage, vous offre davantage de flexibilité dans votre tooscale possibilité selon vos besoins.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Comment partitionnées et les collections de partition unique comparé toohello S1, S2, S3 des niveaux de performances ?

Hello tableau suivant compare les disponibles dans les collections de partitions uniques, les collections partitionnées et S1, S2, S3 les niveaux de performance options hello débit et de stockage. Voici un exemple pour la région Est des États-Unis 2 :

|   |Collection partitionnée|Collection à partition unique|S1|S2|S3|
|---|---|---|---|---|---|
|Débit maximal|Illimité|10 000 RU/s|250 RU/s|1 000 RU/s|2 500 RU/s|
|Débit minimal|2 500 RU/s|400 RU/s|250 RU/s|1 000 RU/s|2 500 RU/s|
|Stockage maximal|Illimité|10 Go|10 Go|10 Go|10 Go|
|Prix (mensuel)|Débit : 6 USD / 100 RU/s<br><br>Stockage : 0,25 USD/Go|Débit : 6 USD / 100 RU/s<br><br>Stockage : 0,25 USD/Go|25 USD|50 USD|100 USD|

Vous êtes un client Contrat Entreprise ? Si oui, voir [Quelles sont les conséquences pour moi en tant que client Contrat Entreprise ?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>Que faire besoin d’accès ininterrompu à toodo tooensure toomy données ?

Nothing, Cosmos DB gère migration hello pour vous. Si vous avez une collection S1, S2 ou S3, votre collection actuelle sera collection de partition unique tooa migrés sur le 31 juillet 2017. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Comment ma collection changera après la migration de hello ?

Si vous avez une collection S1, vous serez collection de partition unique tooa migré avec un débit de 400 ur/s. 400 ur/s est hello plus bas débit disponible avec les collections de partitions uniques. Toutefois, coût hello pour 400 ur/s dans une collection de partition unique est approximativement de hello identique vous ont été payant auprès de votre collection S1 de hello et 250 ur/s, donc vous ne payez pas pour hello très 150 tooyou d’ur/s disponibles.

Si vous avez une collection S2, vous serez collection de partition unique tooa migrés avec 1 K ur/s. Vous ne verrez pas modifier le niveau de débit tooyour.

Si vous avez une collection S3, vous serez collection de partition unique tooa migrés avec 2,5 K ur/s. Vous ne verrez pas modifier le niveau de débit tooyour.

Dans chacun de ces cas, après la migration de votre collection, vous est en mesure de toocustomize votre niveau de débit, ou mettre à l’échelle haut et bas en tant qu’utilisateurs de tooyour d’accès de faible latence tooprovide nécessaires. toochange le niveau de débit hello une fois que votre collection a migré, ouvrez simplement votre compte de base de données Cosmos Bonjour portail Azure et cliquez sur l’échelle, choisissez votre collection de puis ajuster au niveau du débit hello, comme indiqué dans hello suivant capture d’écran :

![Comment le débit tooscale dans hello portail Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Comment me facturation, modifié une fois que je suis collections de partitions uniques toohello migré ?

En supposant que vous avez 10 collections de S1, 1 Go de stockage pour chacune d’elles, dans la région États-Unis hello, et que vous migrez ces 10 S1 collections too10 unique les collections de partitions à 400 ur/s (minimaux hello). Votre facture se présentera comme suit si vous laissez les collections de partition unique 10 hello pendant un mois complet :

![Compare S1 tarification pour les collections de 10 too10 collections à l’aide de la tarification pour un regroupement de partition unique](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>Que se passe-t-il si j’ai besoin de plus de 10 Go de stockage ?

Si vous disposez d’une collection avec un niveau de performance S1, S2 ou S3 ou disposez d’une collection de partition unique, qui ont 10 Go de stockage disponible, vous pouvez utiliser hello Migration de données de base de données Cosmos outil toomigrate tooa de vos données partitionnées collection avec pratiquement stockage illimité. Pour plus d’informations sur les avantages de hello d’une collection partitionnée, consultez [de partitionnement et de mise à l’échelle dans la base de données Azure Cosmos](documentdb-partition-data.md). Pour plus d’informations sur la façon toomigrate vos S1, S2, S3 ou partition unique tooa partitionnée de collecte, consultez la section [migration à partir des collections de partition unique toopartitioned](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>Puis-je changer entre les niveaux de performance hello S1, S2 et S3 avant le 1er août 2017 ?

Seuls les comptes existants avec performances S1, S2 et S3 seront en mesure de toochange et modifier la hiérarchie des niveaux de performances via le portail de hello ou par programme. Par le 1er août 2017 hello S1, S2, et les niveaux de performance S3 ne sera plus disponibles. Si vous modifiez à partir de la collection de partition unique tooa S1, S3 ou S3, vous ne peut pas retourner toohello les niveaux de performance S1, S2 ou S3.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Comment serai-je informé de la migration de ma collection ?

migration de Hello aura lieu le 31 juillet 2017. Si vous avez une collection qui utilise hello S1, S2 ou S3 les niveaux de performance, équipe de base de données Cosmos hello vous contactera par courrier électronique avant de la migration de hello. Une fois la migration de hello est terminée, sur le 1er août 2017 hello portail Azure affichera que votre collection utilise la tarification Standard.

![Comment tooconfirm votre collection a migré de la tarification Standard toohello](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Comment migrer à partir de hello S1, S2, S3 performances niveaux toosingle les collections de partitions sur mon propre ?

Vous pouvez migrer à partir de hello S1, S2, et les collections de partitions toosingle à l’aide de hello portail Azure de niveaux de performance de S3 ou par programme. Cela à partir des options de débit flexible hello disponibles avec les collections de partition unique sur votre propre avant août 1 toobenefit ou nous ferons migrer vos collections pour vous sur le 31 juillet 2017.

**collections de partitions toosingle toomigrate à l’aide de hello portail Azure**

1. Bonjour [ **portail Azure**](https://portal.azure.com), cliquez sur **base de données Azure Cosmos**, puis sélectionnez hello Cosmos DB compte toomodify. 
 
    Si **base de données Azure Cosmos** n’est pas hello Jumpbar, cliquez sur >, faites défiler trop**bases de données**, sélectionnez **base de données Azure Cosmos**, puis sélectionnez le compte de DocumentDB hello.  

2. Menu de ressource hello, sous **conteneurs**, cliquez sur **échelle**, sélectionnez hello collection toomodify à partir de la liste déroulante de hello, puis cliquez sur **niveau tarifaire**. Les comptes utilisant un débit prédéfini ont un niveau tarifaire de S1, S2 ou S3.  Bonjour **choisir votre niveau tarifaire** panneau, cliquez sur **Standard** toochange définis par le toouser débit, puis cliquez sur **sélectionnez** toosave votre modification.

    ![Capture d’écran du Panneau de paramètres hello indiquant où toochange hello la valeur de débit](./media/performance-levels/change-performance-set-thoughput.png)

3. Dans hello **échelle** panneau, hello **niveau tarifaire** est modifié trop**Standard** et hello **(ur/s) de débit** s’affiche avec un valeur par défaut de 400. Débit de hello ensemble compris entre 400 et 10 000 [unités de requête ](request-units.md) /seconde (ur/s). Hello **estimée de facture mensuelle** bas hello hello page met automatiquement à jour tooprovide une estimation du coût mensuel de hello. 

    >[!IMPORTANT] 
    > Une fois que vous enregistrez vos modifications et que vous déplacez la tarification Standard toohello, vous ne pouvez pas restaurer toohello les niveaux de performance S1, S2 ou S3.

4. Cliquez sur **enregistrer** toosave vos modifications.

    Si vous déterminez que vous avez besoin d’un débit supérieur (plus de 10 000 unités de requête/s) ou d’une plus grande capacité de stockage (plus de 10 Go), vous pouvez créer une collection partitionnée. toomigrate une collection de tooa partitionnée de collection de partition unique, consultez [migration à partir des collections de partition unique toopartitioned](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > La modification de tooStandard S1, S2 ou S3 peut prendre jusqu'à too2 minutes.
    > 
    > 

**collections de partitions toosingle toomigrate à l’aide de hello .NET SDK**

Vous pouvez également modifier les niveaux de performances de vos collections via nos Kits SDK. Cette section couvre uniquement modifier les performances d’une collection de niveau à l’aide de notre [DocumentDB .NET API](documentdb-sdk-dotnet.md), mais le processus de hello est similaire à nos autres kits de développement logiciel.

Voici un extrait de code pour la modification hello collection débit too5, 000 unités de demande par seconde :
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Visitez [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview des exemples supplémentaires et en savoir plus sur nos méthodes offre :

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Quelles sont les conséquences pour moi en tant que client Contrat Entreprise ?

Les clients EA seront est protégé jusqu'à la fin de hello de leur contrat actuel.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la tarification et la gestion des données avec la base de données Azure Cosmos, Explorez ces ressources :

1.  [Partitioning data in Cosmos DB (Partitionnement des données dans Cosmos DB)](documentdb-partition-data.md). Comprendre la différence de hello entre le conteneur de la partition unique et conteneurs partitionnées, ainsi que des conseils sur l’implémentation d’un tooscale de stratégie de partitionnement en toute transparence.
2.  [Tarification Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). En savoir plus sur coût hello d’approvisionnement de débit et de consommation de stockage.
3.  [Unités de requête](request-units.md). Comprendre la consommation de débit pour les types d’opération différente, par exemple les requêtes de lecture, écriture, hello.
