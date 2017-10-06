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
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="ccfcd-104">Faire expirer les données dans des collections de base de données Azure Cosmos automatiquement avec le temps toolive</span><span class="sxs-lookup"><span data-stu-id="ccfcd-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="ccfcd-105">Les applications peuvent générer et stocker de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="ccfcd-106">Certaines de ces données, telles que les données d’événement générées par la machine, les journaux et les informations de session utilisateur, sont utiles uniquement pendant une certaine période.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="ccfcd-107">Une fois que les données de salutation devient toohello en surplus les besoins de l’application hello est sécurisé toopurge ces données et réduire les besoins en stockage hello d’une application.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="ccfcd-108">Par « time toolive » ou la durée de vie, base de données Microsoft Azure Cosmos fournit des documents de toohave de capacité hello purgés automatiquement à partir de la base de données hello après une période de temps.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="ccfcd-109">durée par défaut de Hello toolive peut être définie au niveau de collection hello et être substituée par document.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="ccfcd-110">Une fois la TTL définie, soit en tant que valeur par défaut de la collection, soit au niveau du document, Cosmos DB supprime automatiquement les documents existant une fois cette période (en secondes) écoulée depuis leur dernière modification.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="ccfcd-111">Temps toolive dans la base de données Cosmos utilise un décalage par rapport à lors de la dernière modification du document hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="ccfcd-112">toodo cette celle-ci utilise hello `_ts` champ qui existe sur tous les documents.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="ccfcd-113">champ de _ts Hello est de style unix époque timestamp représentant hello date et heure.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="ccfcd-114">Hello `_ts` est mis à jour chaque fois qu’un document est modifié.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="ccfcd-115">Comportement de la TTL</span><span class="sxs-lookup"><span data-stu-id="ccfcd-115">TTL behavior</span></span>
<span data-ttu-id="ccfcd-116">fonctionnalité de durée de vie Hello est contrôlée par les propriétés de durée de vie à deux niveaux - niveau de la collection hello et au niveau du document hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="ccfcd-117">les valeurs Hello sont définies en secondes et sont traités comme un delta de hello `_ts` la dernière modification de ce document hello à.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="ccfcd-118">DefaultTTL pour collection de hello</span><span class="sxs-lookup"><span data-stu-id="ccfcd-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="ccfcd-119">Si des documents manquants (ou ensemble toonull), ne sont pas supprimés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="ccfcd-120">S’il est présent et la valeur de hello est « -1 » = infinie – documents n’expirent pas par défaut</span><span class="sxs-lookup"><span data-stu-id="ccfcd-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="ccfcd-121">S’il est présent et la valeur de hello est un nombre (« n ») : documents expirent le « n » secondes après la dernière modification</span><span class="sxs-lookup"><span data-stu-id="ccfcd-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="ccfcd-122">Durée de vie pour les documents hello :</span><span class="sxs-lookup"><span data-stu-id="ccfcd-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="ccfcd-123">Propriété est applicable uniquement si DefaultTTL est présent pour la collection de parents hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="ccfcd-124">Remplace la valeur de DefaultTTL de hello pour collection de parents hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="ccfcd-125">Dès que le document de hello a expiré (`ttl`  +  `_ts` > = heure actuelle du serveur), document de hello est marqué comme « expiré ».</span><span class="sxs-lookup"><span data-stu-id="ccfcd-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="ccfcd-126">Aucune opération ne sera autorisée sur ces documents après cette heure, et ils seront exclus des résultats des requêtes effectuées hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="ccfcd-127">documents de Hello sont physiquement supprimées dans le système de hello et sont supprimés en arrière-plan de hello façon opportuniste ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="ccfcd-128">Cela ne prend pas [unités de demande (RUs)](request-units.md) de budget de collection hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="ccfcd-129">Hello ci-dessus logique peut être affichée dans hello suivant la matrice :</span><span class="sxs-lookup"><span data-stu-id="ccfcd-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="ccfcd-130">DefaultTTL manquant/non défini dans la collection de hello</span><span class="sxs-lookup"><span data-stu-id="ccfcd-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="ccfcd-131">DefaultTTL = -1 sur la collection</span><span class="sxs-lookup"><span data-stu-id="ccfcd-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="ccfcd-132">DefaultTTL = « n » sur la collection</span><span class="sxs-lookup"><span data-stu-id="ccfcd-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="ccfcd-133">TTL manquante sur le document</span><span class="sxs-lookup"><span data-stu-id="ccfcd-133">TTL Missing on document</span></span> |<span data-ttu-id="ccfcd-134">Nothing toooverride au niveau du document, car le document de hello et collection ont aucun concept de durée de vie.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="ccfcd-135">Aucun document de cette collection n’expire.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="ccfcd-136">Hello dans cette collection expirent lorsque n de l’intervalle est écoulé.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="ccfcd-137">TTL = -1 sur le document</span><span class="sxs-lookup"><span data-stu-id="ccfcd-137">TTL = -1 on document</span></span> |<span data-ttu-id="ccfcd-138">Nothing toooverride au niveau du document hello depuis ne définit pas de collection de hello hello propriété DefaultTTL un document peut substituer.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="ccfcd-139">Durée de vie d’un document est non interprétée par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="ccfcd-140">Aucun document de cette collection n’expire.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="ccfcd-141">document Hello avec TTL =-1 dans cette collection n’expirera jamais.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="ccfcd-142">Tous les autres documents expirent après l’intervalle « n ».</span><span class="sxs-lookup"><span data-stu-id="ccfcd-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="ccfcd-143">TTL = n sur le document</span><span class="sxs-lookup"><span data-stu-id="ccfcd-143">TTL = n on document</span></span> |<span data-ttu-id="ccfcd-144">Nothing toooverride au niveau du document hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="ccfcd-145">Durée de vie d’un document dans non interprétées par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="ccfcd-146">document Hello TTL = n va expirer après n intervalle, en secondes.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="ccfcd-147">D’autres documents héritent de l’intervalle -1 et n’expirent jamais.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="ccfcd-148">document Hello TTL = n va expirer après n intervalle, en secondes.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="ccfcd-149">Autres documents héritent des « n » l’intervalle de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="ccfcd-150">Configuration de la TTL</span><span class="sxs-lookup"><span data-stu-id="ccfcd-150">Configuring TTL</span></span>
<span data-ttu-id="ccfcd-151">Par défaut, le temps toolive est désactivée par défaut dans toutes les collections de base de données Cosmos et sur tous les documents.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="ccfcd-152">Activation de la TTL</span><span class="sxs-lookup"><span data-stu-id="ccfcd-152">Enabling TTL</span></span>
<span data-ttu-id="ccfcd-153">tooenable durée de vie sur une collection ou documents hello dans une collection, vous devez tooset hello DefaultTTL propriété un tooeither collection -1 ou un nombre positif différent de zéro.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="ccfcd-154">Définition des moyens de trop 1 DefaultTTL hello que par défaut, tous les documents dans la collection de hello seront trouvera indéfiniment mais hello Cosmos DB service, surveillez cette collection pour les documents qui ont remplacé cette valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="ccfcd-155">Configuration de la TTL par défaut sur une collection</span><span class="sxs-lookup"><span data-stu-id="ccfcd-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="ccfcd-156">Vous êtes tooconfigure en mesure d’un délai par défaut toolive à un niveau de la collection.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="ccfcd-157">tooset hello TTL sur une collection, vous devez tooprovide un nombre positif différent de zéro qui indique la période de hello, en secondes, tooexpire tous les documents dans la collection de hello après hello dernière modification de l’horodatage du document de hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="ccfcd-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="ccfcd-158">Ou bien, vous pouvez définir hello par défaut trop-1, ce qui implique que tous les documents sont insérés dans la collection de toohello indéfiniment par défaut.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="ccfcd-159">Définition de la TTL sur un document</span><span class="sxs-lookup"><span data-stu-id="ccfcd-159">Setting TTL on a document</span></span>
<span data-ttu-id="ccfcd-160">En outre toosetting durée de vie par défaut sur un regroupement vous pouvez définir durée de vie spécifique à un niveau du document.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="ccfcd-161">Cette opération remplacera par défaut de hello de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="ccfcd-162">tooset hello durée de vie d’un document, vous devez tooprovide un nombre positif différent de zéro qui indique hello période, en secondes, le document de hello tooexpire après hello dernière modification de l’horodatage du document de hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="ccfcd-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="ccfcd-163">Si un document ne comporte aucun champ de durée de vie, puis hello par défaut de la collection de hello s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="ccfcd-164">Si la durée de vie est désactivée au niveau de collection hello, champ de durée de vie hello de hello sera ignoré jusqu'à ce que la durée de vie est activée sur la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="ccfcd-165">Voici un extrait de code montrant comment tooset hello d’expiration de durée de vie d’un document :</span><span class="sxs-lookup"><span data-stu-id="ccfcd-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

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


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="ccfcd-166">Extension de la TTL sur un document existant</span><span class="sxs-lookup"><span data-stu-id="ccfcd-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="ccfcd-167">Vous pouvez réinitialiser hello durée de vie d’un document par toute opération d’écriture sur le document de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="ccfcd-168">Cette opération définira hello `_ts` toohello heure actuelle et hello du compte à rebours toohello document d’expiration, telle que définie par hello `ttl`, commencera à nouveau.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="ccfcd-169">Si vous le souhaitez toochange hello `ttl` d’un document, vous pouvez mettre à jour les champs hello comme vous pouvez le faire avec n’importe quel autre champ définissable.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="ccfcd-170">Suppression de la TTL d’un document</span><span class="sxs-lookup"><span data-stu-id="ccfcd-170">Removing TTL from a document</span></span>
<span data-ttu-id="ccfcd-171">Si une durée de vie a été définie sur un document et que vous ne voulez plus que tooexpire de document, puis vous pouvez extraire hello du document, supprimez le champ de durée de vie hello et remplacer document hello sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="ccfcd-172">Lorsque le champ de durée de vie hello est supprimé à partir du document de hello, valeur par défaut de hello de collection de hello est appliquée.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="ccfcd-173">toostop un document à partir de la date d’expiration et ne hérite pas de collection de hello, vous devez tooset hello TTL valeur trop-1.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="ccfcd-174">Désactivation de la TTL</span><span class="sxs-lookup"><span data-stu-id="ccfcd-174">Disabling TTL</span></span>
<span data-ttu-id="ccfcd-175">toodisable TTL entièrement sur une collection et un arrière-plan de hello arrêt du processus de recherche des documents ayant expirés, propriété DefaultTTL hello collection de hello doit être supprimée.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="ccfcd-176">La suppression de cette propriété est différente de la définition de trop-1.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="ccfcd-177">Définition de nouveaux documents trop-1 signifie ajouté toohello collection se trouvera indéfiniment, mais vous pouvez la remplacer sur des documents spécifiques dans la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="ccfcd-178">Suppression de cette propriété entièrement à partir de la collection de hello signifie qu’aucun document n’expire, même si les documents qui ont le substituer explicitement une valeur par défaut précédente.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="ccfcd-179">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="ccfcd-179">FAQ</span></span>
<span data-ttu-id="ccfcd-180">**Quel est le coût de la TTL ?**</span><span class="sxs-lookup"><span data-stu-id="ccfcd-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="ccfcd-181">Il n’existe aucun coût supplémentaire de toosetting une durée de vie d’un document.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="ccfcd-182">**Combien de temps faut-il toodelete mon document une fois hello TTL ?**</span><span class="sxs-lookup"><span data-stu-id="ccfcd-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="ccfcd-183">les documents Hello ont expiré immédiatement une fois hello durée de vie est activé et n’est plus accessible via CRUD ou les API de requête.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="ccfcd-184">**La TTL d’un document a-t-elle un impact sur les frais d’unités de requête ?**</span><span class="sxs-lookup"><span data-stu-id="ccfcd-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="ccfcd-185">Non, il n’y a aucun impact sur les frais d’unités de requête pour les suppressions de documents ayant expiré par le biais de la durée de vie dans Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="ccfcd-186">**Fonctionnalité de durée de vie hello seulement s’applique tooentire documents ou puis-je expirer la fonctionnalité les valeurs de propriété de document individuel ?**</span><span class="sxs-lookup"><span data-stu-id="ccfcd-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="ccfcd-187">Durée de vie s’applique toohello ensemble du document.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="ccfcd-188">Si vous souhaitez que tooexpire uniquement une partie d’un document, puis il est recommandée que vous extrayez partie de hello hello principal du document dans tooa de document « lié » distinct et ensuite utilisez TTL sur ce document extrait.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="ccfcd-189">**Fonctionnalité de durée de vie hello a-t-il des exigences d’indexation spécifiques ?**</span><span class="sxs-lookup"><span data-stu-id="ccfcd-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="ccfcd-190">Oui.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-190">Yes.</span></span> <span data-ttu-id="ccfcd-191">la collection Hello doit comporter [l’indexation de jeu de stratégie](indexing-policies.md) tooeither cohérente ou Lazy.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="ccfcd-192">La tentative de tooset DefaultTTL sur une collection à l’indexation de jeu tooNone entraîne une erreur, ainsi que lors de la tentative de tooturn désactiver l’indexation dans une collection ayant un DefaultTTL est déjà défini.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccfcd-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ccfcd-193">Next steps</span></span>
<span data-ttu-id="ccfcd-194">toolearn savoir plus sur la base de données Azure Cosmos, consultez toohello service [ *documentation* ](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span><span class="sxs-lookup"><span data-stu-id="ccfcd-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

