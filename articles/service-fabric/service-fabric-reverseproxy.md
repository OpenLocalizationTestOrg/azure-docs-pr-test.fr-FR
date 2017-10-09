---
title: "aaaAzure l’infrastructure de Service de proxy inverse | Documents Microsoft"
description: "Utilisez le proxy inverse de l’architecture de Service pour toomicroservices de communication de l’intérieur et extérieur cluster de hello."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="973a8-103">Proxy inverse dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="973a8-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="973a8-104">les adresses de proxy inverse Hello qui est intégrée à Azure Service Fabric microservices Cluster Service Fabric hello qui expose les points de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="973a8-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="973a8-105">Modèle de communication des microservices</span><span class="sxs-lookup"><span data-stu-id="973a8-105">Microservices communication model</span></span>
<span data-ttu-id="973a8-106">En général, Microservices dans l’infrastructure de Service s’exécutent sur un sous-ensemble d’ordinateurs virtuels dans un cluster de hello et pouvez déplacer à partir d’un ordinateur virtuel tooanother pour diverses raisons.</span><span class="sxs-lookup"><span data-stu-id="973a8-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="973a8-107">Par conséquent, les points de terminaison hello pour microservices peuvent changer dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="973a8-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="973a8-108">Hello modèle classique toocommunicate toohello microservice est la suivante de hello résoudre boucle :</span><span class="sxs-lookup"><span data-stu-id="973a8-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="973a8-109">Résoudre l’emplacement du service hello initialement par le biais de service d’affectation de noms de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="973a8-110">Se connecter toohello service.</span><span class="sxs-lookup"><span data-stu-id="973a8-110">Connect toohello service.</span></span>
3. <span data-ttu-id="973a8-111">Déterminer la cause de hello d’échecs de connexion et les résoudre à nouveau l’emplacement du service hello lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="973a8-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="973a8-112">Ce processus implique généralement l’habillage des bibliothèques côté client communication dans une boucle de tentatives qui implémente des stratégies de résolution, puis réessayez de service hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="973a8-113">Pour plus d’informations, consultez la page [Se connecter et communiquer avec les services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="973a8-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="973a8-114">Communication à l’aide de proxy inverse de hello</span><span class="sxs-lookup"><span data-stu-id="973a8-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="973a8-115">proxy inverse de Hello dans l’infrastructure de Service s’exécute sur tous les nœuds hello cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="973a8-116">Il exécute le processus de résolution d’ensemble du service hello pour un client et transmet ensuite la demande du client hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="973a8-117">Par conséquent, les clients qui s’exécutent sur le cluster de hello peuvent utiliser n’importe quel service cible de côté client HTTP communication bibliothèques tootalk toohello à l’aide de proxy inverse de hello que s’exécute localement sur hello même nœud.</span><span class="sxs-lookup"><span data-stu-id="973a8-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Communications internes][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="973a8-119">Atteindre microservices à partir du cluster en dehors de hello</span><span class="sxs-lookup"><span data-stu-id="973a8-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="973a8-120">modèle de communication externe par défaut Hello pour microservices est un modèle d’abonnement dans lequel chaque service ne sont pas accessibles directement à partir de clients externes.</span><span class="sxs-lookup"><span data-stu-id="973a8-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="973a8-121">[Équilibrage de charge Azure](../load-balancer/load-balancer-overview.md), qui est une limite réseau entre les clients externes et de microservices exécute traduction d’adresses réseau et de points de terminaison IP : port toointernal demande des transferts externe.</span><span class="sxs-lookup"><span data-stu-id="973a8-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="973a8-122">toomake clients de tooexternal directement accessibles de point de terminaison d’un microservice, vous devez d’abord configurer équilibrage de charge de port tooeach tooforward le trafic qui hello service utilise dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="973a8-123">En outre, la plupart des microservices, en particulier avec état microservices, ne live sur tous les nœuds du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="973a8-124">Hello microservices pouvez déplacer entre les nœuds de basculement.</span><span class="sxs-lookup"><span data-stu-id="973a8-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="973a8-125">Dans ce cas, équilibrage de charge ne peut pas déterminer efficacement d’emplacement de hello du nœud cible de hello de hello réplicas toowhich, il doit transférer le trafic.</span><span class="sxs-lookup"><span data-stu-id="973a8-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="973a8-126">Atteindre microservices via le proxy inverse hello du cluster de hello externe</span><span class="sxs-lookup"><span data-stu-id="973a8-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="973a8-127">Au lieu de configurer le port hello des services individuels dans l’équilibrage de charge, vous pouvez configurer simplement hello port proxy inverse de hello dans l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="973a8-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="973a8-128">Cette configuration permet aux clients en dehors du cluster de hello de contacter les services à l’intérieur de hello cluster à l’aide de proxy inverse de hello sans configuration supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="973a8-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Communications externes][0]

> [!WARNING]
> <span data-ttu-id="973a8-130">Lorsque vous configurez un port de proxy inverse hello dans l’équilibrage de charge, toutes les microservices dans un cluster de hello qui exposent un point de terminaison HTTP sont adressables à partir de l’extérieur hello cluster.</span><span class="sxs-lookup"><span data-stu-id="973a8-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="973a8-131">Format d’URI pour l’adressage des services à l’aide de proxy inverse de hello</span><span class="sxs-lookup"><span data-stu-id="973a8-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="973a8-132">utilisations de proxy inverse Hello qu'une URI spécifique identificateur URI () format tooidentify hello partition toowhich hello entrants demande de service doit être transférée :</span><span class="sxs-lookup"><span data-stu-id="973a8-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="973a8-133">**HTTP (s) :** proxy inverse de hello peut être configuré tooaccept HTTP ou le trafic HTTPS.</span><span class="sxs-lookup"><span data-stu-id="973a8-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="973a8-134">Pour le transfert HTTPS, consultez trop[connecter tooa le service sécurisé avec le proxy inverse hello](service-fabric-reverseproxy-configure-secure-communication.md) une fois que vous avez toolisten le programme d’installation de proxy inverse sur HTTPS.</span><span class="sxs-lookup"><span data-stu-id="973a8-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="973a8-135">**Nom de domaine complet de cluster (nom de domaine complet) | adresse IP interne :** pour les clients externes, vous pouvez configurer le proxy inverse de hello afin qu’il soit accessible via le domaine du cluster hello, telles que mycluster.eastus.cloudapp.azure.com. Par défaut, le proxy inverse de hello s’exécute sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="973a8-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="973a8-136">Pour le trafic interne, le proxy inverse de hello peut être atteint sur localhost ou sur toutes les adresses IP internes de nœud, telle que 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="973a8-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="973a8-137">**Port :** port hello, telles que 19081, qui a été spécifié pour le proxy inverse de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="973a8-138">**ServiceInstanceName :** Voici nom qualifié complet de hello hello déployé des instances de service que vous essayez de tooreach sans hello « fabric : / « schéma.</span><span class="sxs-lookup"><span data-stu-id="973a8-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="973a8-139">Par exemple, tooreach hello *fabric : / myapp/myservice/* service, vous utiliseriez *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="973a8-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="973a8-140">nom de l’instance service Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="973a8-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="973a8-141">À l’aide d’une casse différente pour le nom de l’instance service hello dans les URL hello entraîne hello demandes toofail 404 (introuvable).</span><span class="sxs-lookup"><span data-stu-id="973a8-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="973a8-142">**Chemin d’accès de suffixe :** Voici hello URL du chemin d’accès réel, tel que *myapi/valeurs/ajouter/3*, service hello tooconnect à souhaitées.</span><span class="sxs-lookup"><span data-stu-id="973a8-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="973a8-143">**PartitionKey :** pour un service partitionné, il s’agit clé de partition calculée hello de partition hello que vous souhaitez tooreach.</span><span class="sxs-lookup"><span data-stu-id="973a8-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="973a8-144">Notez que cela est *pas* hello GUID ID de partition.</span><span class="sxs-lookup"><span data-stu-id="973a8-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="973a8-145">Ce paramètre n’est pas obligatoire pour les services qui utilisent le schéma de partition singleton hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="973a8-146">**PartitionKind :** schéma de partition de service hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="973a8-147">Il peut s’agir de Named ou Int64Range.</span><span class="sxs-lookup"><span data-stu-id="973a8-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="973a8-148">Ce paramètre n’est pas obligatoire pour les services qui utilisent le schéma de partition singleton hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="973a8-149">**ListenerName** hello des points de terminaison de service de hello sont sous forme de hello {« Points de terminaison » : {« Listener1 » : « Endpoint1 », « Listener2 » : « Endpoint2 »...}}.</span><span class="sxs-lookup"><span data-stu-id="973a8-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="973a8-150">Lorsque le service de hello expose plusieurs points de terminaison, il identifie le point de terminaison hello requête hello du client doit être transférée.</span><span class="sxs-lookup"><span data-stu-id="973a8-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="973a8-151">Cela peut être omis si le service de hello n'a qu’un seul écouteur.</span><span class="sxs-lookup"><span data-stu-id="973a8-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="973a8-152">**TargetReplicaSelector** spécifie comment réplica cible de hello ou une instance doit être sélectionné.</span><span class="sxs-lookup"><span data-stu-id="973a8-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="973a8-153">Lorsque le service cible de hello est avec état, hello TargetReplicaSelector peut s’agir de hello : 'PrimaryReplica', 'RandomSecondaryReplica' ou 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="973a8-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="973a8-154">Lorsque ce paramètre n’est pas spécifié, la valeur par défaut de la hello est 'PrimaryReplica'.</span><span class="sxs-lookup"><span data-stu-id="973a8-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="973a8-155">Lorsque le service cible de hello est sans état, le proxy inverse récupère une instance aléatoire de hello partition tooforward hello demande de service.</span><span class="sxs-lookup"><span data-stu-id="973a8-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="973a8-156">**Délai d’expiration :** cela spécifie le délai d’attente de hello pour demande de hello HTTP créée par le service de toohello hello proxy inverse pour le compte de demande du client hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="973a8-157">Hello par défaut est 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="973a8-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="973a8-158">Paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="973a8-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="973a8-159">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="973a8-159">Example usage</span></span>
<span data-ttu-id="973a8-160">Par exemple, prenons hello *fabric : / MyApp/MyService* service qui ouvre un écouteur HTTP sur hello suivant l’URL :</span><span class="sxs-lookup"><span data-stu-id="973a8-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="973a8-161">Voici des ressources hello pour le service de hello :</span><span class="sxs-lookup"><span data-stu-id="973a8-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="973a8-162">Si le service de hello utilise singleton hello schéma de partitionnement, hello *PartitionKey* et *PartitionKind* les paramètres de chaîne de requête ne sont pas requis, et est accessible à l’aide de passerelle hello en tant que service de hello :</span><span class="sxs-lookup"><span data-stu-id="973a8-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="973a8-163">En externe : `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="973a8-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="973a8-164">En interne : `http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="973a8-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="973a8-165">Si le service de hello utilise hello Int64 uniforme, schéma de partitionnement, hello *PartitionKey* et *PartitionKind* les paramètres de chaîne de requête doivent être utilisé tooreach une partition de service de hello :</span><span class="sxs-lookup"><span data-stu-id="973a8-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="973a8-166">En externe : `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="973a8-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="973a8-167">En interne : `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="973a8-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="973a8-168">ressources hello tooreach hello exposée par service, placez simplement le chemin d’accès de ressource hello après le nom du service hello dans hello URL :</span><span class="sxs-lookup"><span data-stu-id="973a8-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="973a8-169">En externe : `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="973a8-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="973a8-170">En interne : `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="973a8-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="973a8-171">Hello puis envoie l’URL du service toohello de ces demandes :</span><span class="sxs-lookup"><span data-stu-id="973a8-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="973a8-172">Traitement spécial des services de partage de port</span><span class="sxs-lookup"><span data-stu-id="973a8-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="973a8-173">Passerelle d’Application Azure tentatives tooresolve un service de traiter à nouveau, puis réessayez de demande de hello lorsqu’un service ne peut pas être atteint.</span><span class="sxs-lookup"><span data-stu-id="973a8-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="973a8-174">Il s’agit d’un avantage majeur de la passerelle d’Application, car le code client ne devez tooimplement sa propre résolution de noms de service et résoudre la boucle.</span><span class="sxs-lookup"><span data-stu-id="973a8-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="973a8-175">En général, lorsqu’un service ne peut pas être atteinte, l’instance de service hello ou réplica a déplacé tooa autre nœud dans le cadre de son cycle de vie normal.</span><span class="sxs-lookup"><span data-stu-id="973a8-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="973a8-176">Dans ce cas, passerelle d’Application peut recevoir un réseau connexion d’erreur indiquant qu’un point de terminaison est que sans ouvrir plus de temps sur hello résolu à l’origine d’adresse.</span><span class="sxs-lookup"><span data-stu-id="973a8-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="973a8-177">Toutefois, les instances de service ou réplicas peuvent partager un processus hôte, voire un port, lorsqu’ils sont hébergés par un serveur web basé sur HTTP.sys. Cela inclut :</span><span class="sxs-lookup"><span data-stu-id="973a8-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="973a8-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="973a8-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="973a8-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="973a8-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="973a8-180">Katana</span><span class="sxs-lookup"><span data-stu-id="973a8-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="973a8-181">Dans ce cas, il est probable que le serveur web hello est disponible dans le processus hôte de hello et répondre toorequests mais hello résolu l’instance de service ou le réplica n’est plus disponible sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="973a8-182">Dans ce cas, la passerelle de hello recevra une réponse HTTP 404 à partir du serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="973a8-183">Par conséquent, une réponse HTTP 404 a deux sens distincts :</span><span class="sxs-lookup"><span data-stu-id="973a8-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="973a8-184">Casse #1 : adresse du service hello est correcte, mais la ressource hello hello utilisateur demandé n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="973a8-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="973a8-185">Cas #2 : adresse du service hello est incorrect et ressource hello hello utilisateur demandée peut exister sur un autre nœud.</span><span class="sxs-lookup"><span data-stu-id="973a8-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="973a8-186">Hello premier cas est une erreur 404 HTTP normal, qui est considérée comme une erreur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="973a8-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="973a8-187">Toutefois, dans les cas de deuxième hello, utilisateur de hello a demandé une ressource qui existe.</span><span class="sxs-lookup"><span data-stu-id="973a8-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="973a8-188">Passerelle d’application a été toolocate impossible que car hello service lui-même a déplacé.</span><span class="sxs-lookup"><span data-stu-id="973a8-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="973a8-189">Application besoins tooresolve hello adresse de passerelle à nouveau et demande hello de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="973a8-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="973a8-190">Passerelle d’application doit donc un toodistinguish moyen entre ces deux cas.</span><span class="sxs-lookup"><span data-stu-id="973a8-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="973a8-191">toomake que distinction, un indicateur à partir du serveur de hello est requis.</span><span class="sxs-lookup"><span data-stu-id="973a8-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="973a8-192">Par défaut, la passerelle d’Application suppose cas #2 et tente de demande de hello tooresolve et émettre à nouveau.</span><span class="sxs-lookup"><span data-stu-id="973a8-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="973a8-193">tooApplication de cas #1 tooindicate passerelle, hello service doit retourner la hello suivant l’en-tête de réponse HTTP :</span><span class="sxs-lookup"><span data-stu-id="973a8-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="973a8-194">Cet en-tête de réponse HTTP indique une situation HTTP 404 normale dans le hello la ressource demandée n’existe pas, et la passerelle d’Application ne tente pas d’adresse du service tooresolve hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="973a8-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="973a8-195">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="973a8-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="973a8-196">Activer le proxy inverse via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="973a8-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="973a8-197">Portail Azure fournit un proxy inverse de tooenable option lors de la création d’un nouveau cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="973a8-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="973a8-198">Sous **cluster créer Service Fabric**, étape 2 : Configuration du Cluster, configuration du type de nœud, cochez les cases hello trop « Activer le proxy inverse ».</span><span class="sxs-lookup"><span data-stu-id="973a8-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="973a8-199">Pour la configuration de proxy inverse sécurisé, le certificat SSL peut être spécifié à l’étape 3 : sécurité, configurer les paramètres de sécurité de cluster, la case à cocher Sélectionner hello trop « Incluent un certificat SSL pour le proxy inverse » et entrez les détails du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="973a8-200">Activer le proxy inverse via les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="973a8-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="973a8-201">Vous pouvez utiliser hello [modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello inverse serveur proxy dans l’infrastructure de Service de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="973a8-202">Consultez trop[configurer le Proxy inverse HTTPS dans un cluster sécurisé](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) pour le Gestionnaire de ressources Azure tooconfigure un proxy inverse sécurisé avec une substitution de certificat de certificat et la gestion des exemples de modèle.</span><span class="sxs-lookup"><span data-stu-id="973a8-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="973a8-203">Vous obtenez tout d’abord, le modèle de hello pour le cluster de hello que vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="973a8-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="973a8-204">Vous pouvez utiliser des modèles d’exemple hello ou créer un modèle de gestionnaire de ressources personnalisé.</span><span class="sxs-lookup"><span data-stu-id="973a8-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="973a8-205">Ensuite, vous pouvez activer le proxy inverse de hello à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="973a8-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="973a8-206">Définir un port de proxy inverse de hello Bonjour [section paramètres](../azure-resource-manager/resource-group-authoring-templates.md) du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="973a8-207">Spécifiez le port de hello pour chacun des objets de type hello Bonjour **Cluster** [section de ressources de type](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="973a8-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="973a8-208">port de Hello est identifié par le nom du paramètre hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="973a8-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="973a8-209">tooaddress hello proxy inverse à partir de l’extérieur hello cluster Azure, configurez des règles d’équilibrage de charge Azure hello pour le port hello que vous avez spécifié à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="973a8-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="973a8-210">tooconfigure les certificats SSL sur le port proxy inverse de hello, hello ajouter hello certificat toohello ***reverseProxyCertificate*** propriété Bonjour **Cluster** [section de ressources de type](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="973a8-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="973a8-211">Prise en charge d’un certificat de proxy inverse est différent du certificat de cluster hello</span><span class="sxs-lookup"><span data-stu-id="973a8-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="973a8-212">Si le certificat de proxy inverse hello est différente de certificat hello qui sécurise le cluster de hello, puis hello précédemment spécifié certificat doit être installé sur l’ordinateur virtuel de hello et ajouté toohello liste de contrôle d’accès (ACL) afin que le Service Fabric peut y accéder.</span><span class="sxs-lookup"><span data-stu-id="973a8-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="973a8-213">Cela est possible dans hello **virtualMachineScaleSets** [section de ressources de type](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="973a8-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="973a8-214">Pour l’installation, ajoutez ce osProfile toohello de certificat.</span><span class="sxs-lookup"><span data-stu-id="973a8-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="973a8-215">section d’extension Hello du modèle de hello peut mettre à jour les certificats hello Bonjour ACL.</span><span class="sxs-lookup"><span data-stu-id="973a8-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="973a8-216">Lorsque vous utilisez des certificats qui sont différentes de hello cluster certificat tooenable hello proxy inverse sur un cluster existant, installez le certificat de proxy inverse hello et mettre à jour de hello ACL sur le cluster de hello avant d’activer le proxy inverse de hello.</span><span class="sxs-lookup"><span data-stu-id="973a8-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="973a8-217">Hello complète [modèle Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) déploiement à l’aide de paramètres hello mentionnés précédemment avant de commencer un proxy inverse de déploiement tooenable hello dans les étapes 1 à 4.</span><span class="sxs-lookup"><span data-stu-id="973a8-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="973a8-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="973a8-218">Next steps</span></span>
* <span data-ttu-id="973a8-219">Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="973a8-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="973a8-220">Transfert de service de toosecure HTTP avec le proxy inverse hello</span><span class="sxs-lookup"><span data-stu-id="973a8-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="973a8-221">Appels de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="973a8-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="973a8-222">API Web qui utilise OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="973a8-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="973a8-223">Communication WCF à l’aide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="973a8-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="973a8-224">Pour les options de configuration supplémentaires du proxy inverse, reportez-vous à la section ApplicationGateway/Http dans [Personnaliser les paramètres de cluster Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="973a8-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
