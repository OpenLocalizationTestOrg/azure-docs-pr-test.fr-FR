---
title: "Faire expirer des données dans Cosmos DB avec la durée de vie | Documents Microsoft"
description: "Avec la TTL, Microsoft Azure Cosmos DB offre la possibilité de vider automatiquement les documents du système après une période déterminée."
services: cosmos-db
documentationcenter: 
keywords: "durée de vie"
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
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="2d016-104">Faire expirer des données dans des collections Cosmos DB automatiquement avec la durée de vie</span><span class="sxs-lookup"><span data-stu-id="2d016-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="2d016-105">Les applications peuvent générer et stocker de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="2d016-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="2d016-106">Certaines de ces données, telles que les données d’événement générées par la machine, les journaux et les informations de session utilisateur, sont utiles uniquement pendant une certaine période.</span><span class="sxs-lookup"><span data-stu-id="2d016-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="2d016-107">Une fois les données trop nombreuses par rapport aux besoins de l’application, vous pouvez les vider et réduire les besoins de stockage d’une application.</span><span class="sxs-lookup"><span data-stu-id="2d016-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="2d016-108">Avec la « durée de vie » (TTL, Time to Live), Microsoft Azure Cosmos DB offre la possibilité de vider automatiquement les documents de la base de données après une période déterminée.</span><span class="sxs-lookup"><span data-stu-id="2d016-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="2d016-109">La durée de vie par défaut peut être définie au niveau de la collection et être substituée par document.</span><span class="sxs-lookup"><span data-stu-id="2d016-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="2d016-110">Une fois la TTL définie, soit en tant que valeur par défaut de la collection, soit au niveau du document, Cosmos DB supprime automatiquement les documents existant une fois cette période (en secondes) écoulée depuis leur dernière modification.</span><span class="sxs-lookup"><span data-stu-id="2d016-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="2d016-111">Dans Cosmos DB, la durée de vie utilise un décalage par rapport au moment où le document a été modifié pour la dernière fois.</span><span class="sxs-lookup"><span data-stu-id="2d016-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="2d016-112">Pour ce faire, il utilise le champ `_ts` qui existe sur tous les documents.</span><span class="sxs-lookup"><span data-stu-id="2d016-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="2d016-113">Le champ _ts est un horodateur d’époque de style Unix représentant la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="2d016-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="2d016-114">Le champ `_ts` est mis à jour à chaque modification d’un document.</span><span class="sxs-lookup"><span data-stu-id="2d016-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="2d016-115">Comportement de la TTL</span><span class="sxs-lookup"><span data-stu-id="2d016-115">TTL behavior</span></span>
<span data-ttu-id="2d016-116">La fonction TTL est contrôlée par les propriétés TTL à deux niveaux : au niveau de la collection et au niveau du document.</span><span class="sxs-lookup"><span data-stu-id="2d016-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="2d016-117">Les valeurs sont définies en secondes et sont traitées en tant qu’écart par rapport à l’horodatage de dernière modification du document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="2d016-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="2d016-118">DefaultTTL pour la collection</span><span class="sxs-lookup"><span data-stu-id="2d016-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="2d016-119">Si ce paramètre est manquant (ou a la valeur null), les documents ne sont pas supprimés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2d016-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="2d016-120">Si ce paramètre est présent et a la valeur « -1 » (infinie), les documents n’expirent pas par défaut.</span><span class="sxs-lookup"><span data-stu-id="2d016-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="2d016-121">Si ce paramètre est présent et que sa valeur est un nombre (« n »), les documents expirent « n » secondes après la dernière modification.</span><span class="sxs-lookup"><span data-stu-id="2d016-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="2d016-122">TTL pour les documents :</span><span class="sxs-lookup"><span data-stu-id="2d016-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="2d016-123">La propriété s’applique uniquement si le paramètre DefaultTTL est présent pour la collection parente.</span><span class="sxs-lookup"><span data-stu-id="2d016-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="2d016-124">Elle remplace la valeur DefaultTTL de la collection parente.</span><span class="sxs-lookup"><span data-stu-id="2d016-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="2d016-125">Dès que le document a expiré (`ttl` + `_ts` >= heure actuelle du serveur), le document est marqué comme « expiré ».</span><span class="sxs-lookup"><span data-stu-id="2d016-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="2d016-126">Aucune opération n’est autorisée sur ces documents une fois ce délai écoulé, et les documents sont exclus des résultats de toutes les requêtes effectuées.</span><span class="sxs-lookup"><span data-stu-id="2d016-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="2d016-127">Les documents sont physiquement supprimés du système et sont supprimés en arrière-plan de façon opportuniste ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="2d016-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="2d016-128">Ceci ne consomme aucune [unité de requête](request-units.md) du budget de la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="2d016-129">La logique ci-dessus peut être représentée dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="2d016-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="2d016-130">DefaultTTL manquante/non définie sur la collection</span><span class="sxs-lookup"><span data-stu-id="2d016-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="2d016-131">DefaultTTL = -1 sur la collection</span><span class="sxs-lookup"><span data-stu-id="2d016-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="2d016-132">DefaultTTL = « n » sur la collection</span><span class="sxs-lookup"><span data-stu-id="2d016-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="2d016-133">TTL manquante sur le document</span><span class="sxs-lookup"><span data-stu-id="2d016-133">TTL Missing on document</span></span> |<span data-ttu-id="2d016-134">Rien à substituer au niveau du document, car aucun concept de TTL n’existe pour le document et la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="2d016-135">Aucun document de cette collection n’expire.</span><span class="sxs-lookup"><span data-stu-id="2d016-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="2d016-136">Les documents de cette collection expireront une fois l’intervalle n écoulé.</span><span class="sxs-lookup"><span data-stu-id="2d016-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="2d016-137">TTL = -1 sur le document</span><span class="sxs-lookup"><span data-stu-id="2d016-137">TTL = -1 on document</span></span> |<span data-ttu-id="2d016-138">Rien à substituer au niveau du document, car la collection ne définit pas la propriété DefaultTTL qu’un document peut substituer.</span><span class="sxs-lookup"><span data-stu-id="2d016-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="2d016-139">La TTL sur un document n’est pas interprétée par le système.</span><span class="sxs-lookup"><span data-stu-id="2d016-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="2d016-140">Aucun document de cette collection n’expire.</span><span class="sxs-lookup"><span data-stu-id="2d016-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="2d016-141">Le document avec TTL=-1 dans cette collection n’expire jamais.</span><span class="sxs-lookup"><span data-stu-id="2d016-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="2d016-142">Tous les autres documents expirent après l’intervalle « n ».</span><span class="sxs-lookup"><span data-stu-id="2d016-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="2d016-143">TTL = n sur le document</span><span class="sxs-lookup"><span data-stu-id="2d016-143">TTL = n on document</span></span> |<span data-ttu-id="2d016-144">Rien à substituer au niveau du document.</span><span class="sxs-lookup"><span data-stu-id="2d016-144">Nothing to override at the document level.</span></span> <span data-ttu-id="2d016-145">La TTL sur un document n’est pas interprétée par le système.</span><span class="sxs-lookup"><span data-stu-id="2d016-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="2d016-146">Le document avec TTL = n expire après l’intervalle n, en secondes.</span><span class="sxs-lookup"><span data-stu-id="2d016-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="2d016-147">D’autres documents héritent de l’intervalle -1 et n’expirent jamais.</span><span class="sxs-lookup"><span data-stu-id="2d016-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="2d016-148">Le document avec TTL = n expire après l’intervalle n, en secondes.</span><span class="sxs-lookup"><span data-stu-id="2d016-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="2d016-149">D’autres documents héritent de l’intervalle « n » de la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="2d016-150">Configuration de la TTL</span><span class="sxs-lookup"><span data-stu-id="2d016-150">Configuring TTL</span></span>
<span data-ttu-id="2d016-151">Par défaut, la durée de vie est désactivée dans toutes les collections Cosmos DB et sur tous les documents.</span><span class="sxs-lookup"><span data-stu-id="2d016-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="2d016-152">Activation de la TTL</span><span class="sxs-lookup"><span data-stu-id="2d016-152">Enabling TTL</span></span>
<span data-ttu-id="2d016-153">Pour activer la TTL sur une collection ou sur les documents d’une collection, vous devez définir la propriété DefaultTTL d’une collection sur -1 ou un nombre positif non nul.</span><span class="sxs-lookup"><span data-stu-id="2d016-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="2d016-154">Si vous définissez DefaultTTL sur -1, tous les documents de la collection auront une durée de vie infinie par défaut. Cependant, le service Cosmos DB doit alors surveiller la collection afin d’identifier les documents pour lesquels cette valeur par défaut a été remplacée.</span><span class="sxs-lookup"><span data-stu-id="2d016-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="2d016-155">Configuration de la TTL par défaut sur une collection</span><span class="sxs-lookup"><span data-stu-id="2d016-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="2d016-156">Vous pouvez configurer une durée de vie par défaut au niveau de la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="2d016-157">Pour définir la durée de vie sur une collection, vous devez fournir un nombre positif non nul qui indique, en secondes, le délai d’expiration de tous les documents de la collection après l’horodatage de dernière modification du document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="2d016-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="2d016-158">Vous pouvez également définir la valeur par défaut sur -1, ce qui implique que tous les documents insérés dans la collection auront une durée de vie infinie par défaut.</span><span class="sxs-lookup"><span data-stu-id="2d016-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="2d016-159">Définition de la TTL sur un document</span><span class="sxs-lookup"><span data-stu-id="2d016-159">Setting TTL on a document</span></span>
<span data-ttu-id="2d016-160">En plus de définir une TTL par défaut sur une collection, vous pouvez définir une TTL spécifique au niveau d’un document.</span><span class="sxs-lookup"><span data-stu-id="2d016-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="2d016-161">Cela remplace la valeur par défaut de la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="2d016-162">Pour définir la durée de vie sur un document, vous devez fournir un nombre positif non nul qui indique, en secondes, le délai d’expiration du document après l’horodatage de dernière modification du document (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="2d016-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="2d016-163">Si un document n’a pas de champ TTL, la valeur par défaut de la collection s’applique.</span><span class="sxs-lookup"><span data-stu-id="2d016-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="2d016-164">Si la TTL est désactivée au niveau de la collection, le champ TTL du document sera ignoré jusqu’à ce que la TTL soit de nouveau activée sur la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="2d016-165">Voici un extrait de code montrant comment définir la date d’expiration de la durée de vie dans un document :</span><span class="sxs-lookup"><span data-stu-id="2d016-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="2d016-166">Extension de la TTL sur un document existant</span><span class="sxs-lookup"><span data-stu-id="2d016-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="2d016-167">Vous pouvez réinitialiser la TTL d’un document en effectuant une opération d’écriture quelconque sur le document.</span><span class="sxs-lookup"><span data-stu-id="2d016-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="2d016-168">Cela définit le champ `_ts` selon l’heure actuelle. Le compte à rebours jusqu’à l’expiration du document, tel que défini par la `ttl`, recommence.</span><span class="sxs-lookup"><span data-stu-id="2d016-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="2d016-169">Si vous souhaitez modifier la `ttl` d’un document, vous pouvez mettre à jour le champ comme n’importe quel autre champ définissable.</span><span class="sxs-lookup"><span data-stu-id="2d016-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="2d016-170">Suppression de la TTL d’un document</span><span class="sxs-lookup"><span data-stu-id="2d016-170">Removing TTL from a document</span></span>
<span data-ttu-id="2d016-171">Si une TTL a été définie sur un document et que vous ne souhaitez plus que ce document expire, vous pouvez extraire le document, supprimer le champ TTL et replacer le document sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="2d016-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="2d016-172">Lorsque le champ TTL est supprimé du document, la valeur par défaut de la collection est appliquée.</span><span class="sxs-lookup"><span data-stu-id="2d016-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="2d016-173">Pour éviter qu’un document n’expire et n’hérite de la collection, vous devez définir la valeur de TTL sur -1.</span><span class="sxs-lookup"><span data-stu-id="2d016-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="2d016-174">Désactivation de la TTL</span><span class="sxs-lookup"><span data-stu-id="2d016-174">Disabling TTL</span></span>
<span data-ttu-id="2d016-175">Pour désactiver la TTL entièrement sur une collection et arrêter la recherche de documents expirés par le processus en arrière-plan, vous devez supprimer la propriété DefaultTTL de la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="2d016-176">Supprimer cette propriété ne revient pas à la définir sur -1.</span><span class="sxs-lookup"><span data-stu-id="2d016-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="2d016-177">Si vous la définissez sur -1, les nouveaux documents ajoutés à la collection auront une durée de vie infinie. Cependant, vous pouvez la remplacer sur des documents spécifiques de la collection.</span><span class="sxs-lookup"><span data-stu-id="2d016-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="2d016-178">Si vous supprimez cette propriété de la collection entièrement, aucun document n’expirera, même si une valeur par défaut précédente a été explicitement remplacée sur certains documents.</span><span class="sxs-lookup"><span data-stu-id="2d016-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="2d016-179">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="2d016-179">FAQ</span></span>
<span data-ttu-id="2d016-180">**Quel est le coût de la TTL ?**</span><span class="sxs-lookup"><span data-stu-id="2d016-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="2d016-181">La définition d’une TTL sur un document n’entraîne aucun coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="2d016-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="2d016-182">**Combien de temps faut-il pour supprimer un document une fois la TTL activée ?**</span><span class="sxs-lookup"><span data-stu-id="2d016-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="2d016-183">Les documents expirent immédiatement quand la durée de vie est activée, et ils ne sont pas accessibles par le biais des opérations CRUD ou des API de requête.</span><span class="sxs-lookup"><span data-stu-id="2d016-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="2d016-184">**La TTL d’un document a-t-elle un impact sur les frais d’unités de requête ?**</span><span class="sxs-lookup"><span data-stu-id="2d016-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="2d016-185">Non, il n’y a aucun impact sur les frais d’unités de requête pour les suppressions de documents ayant expiré par le biais de la durée de vie dans Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2d016-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="2d016-186">**La fonctionnalité TTL s’applique-t-elle uniquement à des documents entiers, ou puis-je faire expirer des valeurs de propriété de document individuelles ?**</span><span class="sxs-lookup"><span data-stu-id="2d016-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="2d016-187">La TTL s’applique à l’ensemble du document.</span><span class="sxs-lookup"><span data-stu-id="2d016-187">TTL applies to the entire document.</span></span> <span data-ttu-id="2d016-188">Si vous souhaitez faire expirer uniquement une partie d’un document, il est recommandé d’extraire la partie du document principal dans un document distinct « lié », puis d’utiliser la durée de vie sur ce document extrait.</span><span class="sxs-lookup"><span data-stu-id="2d016-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="2d016-189">**La fonction TTL impose-t-elle des exigences d’indexation spécifiques ?**</span><span class="sxs-lookup"><span data-stu-id="2d016-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="2d016-190">Oui.</span><span class="sxs-lookup"><span data-stu-id="2d016-190">Yes.</span></span> <span data-ttu-id="2d016-191">La collection doit avoir une [stratégie d’indexation](indexing-policies.md) définie sur Différée ou Cohérente.</span><span class="sxs-lookup"><span data-stu-id="2d016-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="2d016-192">Une erreur se produira si vous tentez de définir le paramètre DefaultTTL sur une collection dont l’indexation est définie sur Aucune et si vous essayez de désactiver l’indexation sur une collection dont le paramètre DefaultTTL est déjà défini.</span><span class="sxs-lookup"><span data-stu-id="2d016-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d016-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d016-193">Next steps</span></span>
<span data-ttu-id="2d016-194">Pour en savoir plus sur Azure Cosmos DB, consultez la page de [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) du service.</span><span class="sxs-lookup"><span data-stu-id="2d016-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

