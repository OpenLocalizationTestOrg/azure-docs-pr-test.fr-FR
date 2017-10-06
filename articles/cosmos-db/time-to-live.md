---
title: "aaaExpire des données dans la base de données Azure Cosmos avec heure toolive | Documents Microsoft"
description: "Avec la durée de vie, base de données Microsoft Azure Cosmos fournit des documents de toohave de capacité hello purgés automatiquement à partir du système de hello après une période de temps."
services: cosmos-db
documentationcenter: 
keywords: heure toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Faire expirer les données dans des collections de base de données Azure Cosmos automatiquement avec le temps toolive
Les applications peuvent générer et stocker de grandes quantités de données. Certaines de ces données, telles que les données d’événement générées par la machine, les journaux et les informations de session utilisateur, sont utiles uniquement pendant une certaine période. Une fois que les données de salutation devient toohello en surplus les besoins de l’application hello est sécurisé toopurge ces données et réduire les besoins en stockage hello d’une application.

Par « time toolive » ou la durée de vie, base de données Microsoft Azure Cosmos fournit des documents de toohave de capacité hello purgés automatiquement à partir de la base de données hello après une période de temps. durée par défaut de Hello toolive peut être définie au niveau de collection hello et être substituée par document. Une fois la TTL définie, soit en tant que valeur par défaut de la collection, soit au niveau du document, Cosmos DB supprime automatiquement les documents existant une fois cette période (en secondes) écoulée depuis leur dernière modification.

Temps toolive dans la base de données Cosmos utilise un décalage par rapport à lors de la dernière modification du document hello. toodo cette celle-ci utilise hello `_ts` champ qui existe sur tous les documents. champ de _ts Hello est de style unix époque timestamp représentant hello date et heure. Hello `_ts` est mis à jour chaque fois qu’un document est modifié. 

## <a name="ttl-behavior"></a>Comportement de la TTL
fonctionnalité de durée de vie Hello est contrôlée par les propriétés de durée de vie à deux niveaux - niveau de la collection hello et au niveau du document hello. les valeurs Hello sont définies en secondes et sont traités comme un delta de hello `_ts` la dernière modification de ce document hello à.

1. DefaultTTL pour collection de hello
   
   * Si des documents manquants (ou ensemble toonull), ne sont pas supprimés automatiquement.
   * S’il est présent et la valeur de hello est « -1 » = infinie – documents n’expirent pas par défaut
   * S’il est présent et la valeur de hello est un nombre (« n ») : documents expirent le « n » secondes après la dernière modification
2. Durée de vie pour les documents hello : 
   
   * Propriété est applicable uniquement si DefaultTTL est présent pour la collection de parents hello.
   * Remplace la valeur de DefaultTTL de hello pour collection de parents hello.

Dès que le document de hello a expiré (`ttl`  +  `_ts` > = heure actuelle du serveur), document de hello est marqué comme « expiré ». Aucune opération ne sera autorisée sur ces documents après cette heure, et ils seront exclus des résultats des requêtes effectuées hello. documents de Hello sont physiquement supprimées dans le système de hello et sont supprimés en arrière-plan de hello façon opportuniste ultérieurement. Cela ne prend pas [unités de demande (RUs)](request-units.md) de budget de collection hello.

Hello ci-dessus logique peut être affichée dans hello suivant la matrice :

|  | DefaultTTL manquant/non défini dans la collection de hello | DefaultTTL = -1 sur la collection | DefaultTTL = « n » sur la collection |
| --- |:--- |:--- |:--- |
| TTL manquante sur le document |Nothing toooverride au niveau du document, car le document de hello et collection ont aucun concept de durée de vie. |Aucun document de cette collection n’expire. |Hello dans cette collection expirent lorsque n de l’intervalle est écoulé. |
| TTL = -1 sur le document |Nothing toooverride au niveau du document hello depuis ne définit pas de collection de hello hello propriété DefaultTTL un document peut substituer. Durée de vie d’un document est non interprétée par le système de hello. |Aucun document de cette collection n’expire. |document Hello avec TTL =-1 dans cette collection n’expirera jamais. Tous les autres documents expirent après l’intervalle « n ». |
| TTL = n sur le document |Nothing toooverride au niveau du document hello. Durée de vie d’un document dans non interprétées par le système de hello. |document Hello TTL = n va expirer après n intervalle, en secondes. D’autres documents héritent de l’intervalle -1 et n’expirent jamais. |document Hello TTL = n va expirer après n intervalle, en secondes. Autres documents héritent des « n » l’intervalle de collection de hello. |

## <a name="configuring-ttl"></a>Configuration de la TTL
Par défaut, le temps toolive est désactivée par défaut dans toutes les collections de base de données Cosmos et sur tous les documents.

## <a name="enabling-ttl"></a>Activation de la TTL
tooenable durée de vie sur une collection ou documents hello dans une collection, vous devez tooset hello DefaultTTL propriété un tooeither collection -1 ou un nombre positif différent de zéro. Définition des moyens de trop 1 DefaultTTL hello que par défaut, tous les documents dans la collection de hello seront trouvera indéfiniment mais hello Cosmos DB service, surveillez cette collection pour les documents qui ont remplacé cette valeur par défaut.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Configuration de la TTL par défaut sur une collection
Vous êtes tooconfigure en mesure d’un délai par défaut toolive à un niveau de la collection. tooset hello TTL sur une collection, vous devez tooprovide un nombre positif différent de zéro qui indique la période de hello, en secondes, tooexpire tous les documents dans la collection de hello après hello dernière modification de l’horodatage du document de hello (`_ts`). Ou bien, vous pouvez définir hello par défaut trop-1, ce qui implique que tous les documents sont insérés dans la collection de toohello indéfiniment par défaut.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Définition de la TTL sur un document
En outre toosetting durée de vie par défaut sur un regroupement vous pouvez définir durée de vie spécifique à un niveau du document. Cette opération remplacera par défaut de hello de collection de hello.

* tooset hello durée de vie d’un document, vous devez tooprovide un nombre positif différent de zéro qui indique hello période, en secondes, le document de hello tooexpire après hello dernière modification de l’horodatage du document de hello (`_ts`).
* Si un document ne comporte aucun champ de durée de vie, puis hello par défaut de la collection de hello s’appliquent.
* Si la durée de vie est désactivée au niveau de collection hello, champ de durée de vie hello de hello sera ignoré jusqu'à ce que la durée de vie est activée sur la collection de hello.

Voici un extrait de code montrant comment tooset hello d’expiration de durée de vie d’un document :

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Extension de la TTL sur un document existant
Vous pouvez réinitialiser hello durée de vie d’un document par toute opération d’écriture sur le document de hello. Cette opération définira hello `_ts` toohello heure actuelle et hello du compte à rebours toohello document d’expiration, telle que définie par hello `ttl`, commencera à nouveau. Si vous le souhaitez toochange hello `ttl` d’un document, vous pouvez mettre à jour les champs hello comme vous pouvez le faire avec n’importe quel autre champ définissable.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Suppression de la TTL d’un document
Si une durée de vie a été définie sur un document et que vous ne voulez plus que tooexpire de document, puis vous pouvez extraire hello du document, supprimez le champ de durée de vie hello et remplacer document hello sur le serveur de hello. Lorsque le champ de durée de vie hello est supprimé à partir du document de hello, valeur par défaut de hello de collection de hello est appliquée. toostop un document à partir de la date d’expiration et ne hérite pas de collection de hello, vous devez tooset hello TTL valeur trop-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Désactivation de la TTL
toodisable TTL entièrement sur une collection et un arrière-plan de hello arrêt du processus de recherche des documents ayant expirés, propriété DefaultTTL hello collection de hello doit être supprimée. La suppression de cette propriété est différente de la définition de trop-1. Définition de nouveaux documents trop-1 signifie ajouté toohello collection se trouvera indéfiniment, mais vous pouvez la remplacer sur des documents spécifiques dans la collection de hello. Suppression de cette propriété entièrement à partir de la collection de hello signifie qu’aucun document n’expire, même si les documents qui ont le substituer explicitement une valeur par défaut précédente.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>Forum Aux Questions
**Quel est le coût de la TTL ?**

Il n’existe aucun coût supplémentaire de toosetting une durée de vie d’un document.

**Combien de temps faut-il toodelete mon document une fois hello TTL ?**

les documents Hello ont expiré immédiatement une fois hello durée de vie est activé et n’est plus accessible via CRUD ou les API de requête. 

**La TTL d’un document a-t-elle un impact sur les frais d’unités de requête ?**

Non, il n’y a aucun impact sur les frais d’unités de requête pour les suppressions de documents ayant expiré par le biais de la durée de vie dans Cosmos DB.

**Fonctionnalité de durée de vie hello seulement s’applique tooentire documents ou puis-je expirer la fonctionnalité les valeurs de propriété de document individuel ?**

Durée de vie s’applique toohello ensemble du document. Si vous souhaitez que tooexpire uniquement une partie d’un document, puis il est recommandée que vous extrayez partie de hello hello principal du document dans tooa de document « lié » distinct et ensuite utilisez TTL sur ce document extrait.

**Fonctionnalité de durée de vie hello a-t-il des exigences d’indexation spécifiques ?**

Oui. la collection Hello doit comporter [l’indexation de jeu de stratégie](indexing-policies.md) tooeither cohérente ou Lazy. La tentative de tooset DefaultTTL sur une collection à l’indexation de jeu tooNone entraîne une erreur, ainsi que lors de la tentative de tooturn désactiver l’indexation dans une collection ayant un DefaultTTL est déjà défini.

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la base de données Azure Cosmos, consultez toohello service [ *documentation* ](https://azure.microsoft.com/documentation/services/cosmos-db/) page.

