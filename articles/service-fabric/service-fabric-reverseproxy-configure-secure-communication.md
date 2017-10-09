---
title: "aaaAzure Service Fabric inverser une communication sécurisée proxy | Documents Microsoft"
description: "Configurer la communication de bout en bout sécurisée de proxy inverse tooenable."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="2c03d-103">Connecter le service sécurisé tooa avec le proxy inverse hello</span><span class="sxs-lookup"><span data-stu-id="2c03d-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="2c03d-104">Cet article explique comment tooestablish sécuriser la connexion entre le proxy inverse de hello et services, permettant ainsi d’activer un canal sécurisé tooend de fin.</span><span class="sxs-lookup"><span data-stu-id="2c03d-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="2c03d-105">Connecter les services toosecure est pris en charge uniquement lorsque le proxy inverse est toolisten configuré sur le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2c03d-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="2c03d-106">Le reste du document de hello suppose que Hello cas.</span><span class="sxs-lookup"><span data-stu-id="2c03d-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="2c03d-107">Consultez trop[proxy dans Azure Service Fabric inverse](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) proxy inverse de tooconfigure hello dans Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2c03d-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="2c03d-108">Établissement d’une connexion sécurisée entre le proxy inverse hello et des services</span><span class="sxs-lookup"><span data-stu-id="2c03d-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="2c03d-109">Inverser le proxy de l’authentification tooservices :</span><span class="sxs-lookup"><span data-stu-id="2c03d-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="2c03d-110">Hello proxy inverse s’identifie en tooservices à l’aide de son certificat spécifié avec ***reverseProxyCertificate*** propriété Bonjour **Cluster** [section de ressources de type](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2c03d-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="2c03d-111">Les services peuvent implémenter des certificats d’hello hello logique tooverify présenté par le proxy inverse de hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="2c03d-112">services de Hello peuvent spécifier les détails du certificat client hello accepté en tant que paramètres de configuration dans le package de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="2c03d-113">Cela peut être lu lors de l’exécution et utilisé toovalidate hello certificat est présenté par un proxy inverse de hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="2c03d-114">Consultez trop[gérer les paramètres de l’application](service-fabric-manage-multiple-environment-app-configuration.md) paramètres de configuration tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="2c03d-115">Inverser la vérification de l’identité du service hello via certificat hello présenté par hello service de proxy :</span><span class="sxs-lookup"><span data-stu-id="2c03d-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="2c03d-116">validation du certificat de serveur tooperform de certificats hello présenté par les services de hello, proxy inverse prend en charge une des options suivantes de hello : None, ServiceCommonNameAndIssuer et ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="2c03d-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="2c03d-117">tooselect un de ces trois options, spécifiez hello **ApplicationCertificateValidationPolicy** dans la section de paramètres de hello d’élément passerelle/Http sous [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="2c03d-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="2c03d-118">Pour plus d’informations sur la configuration supplémentaire pour chacune de ces options, voir toohello la prochaine section.</span><span class="sxs-lookup"><span data-stu-id="2c03d-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="2c03d-119">Options de validation du certificat de service</span><span class="sxs-lookup"><span data-stu-id="2c03d-119">Service certificate validation options</span></span> 

- <span data-ttu-id="2c03d-120">**Aucun**: proxy inverse ignore la vérification du certificat de service proxy hello et établit une connexion sécurisée hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="2c03d-121">Il s’agit par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-121">This is hello default behavior.</span></span>
<span data-ttu-id="2c03d-122">Spécifiez hello **ApplicationCertificateValidationPolicy** avec la valeur **aucun** dans la section des paramètres d’élément de la passerelle/Http hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="2c03d-123">**ServiceCommonNameAndIssuer**: proxy inverse vérifie le certificat de hello présenté par le service hello basé sur le nom commun du certificat et l’empreinte numérique de l’émetteur immédiate : spécifiez hello **ApplicationCertificateValidationPolicy**  avec la valeur **ServiceCommonNameAndIssuer** dans la section des paramètres d’élément de la passerelle/Http hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="2c03d-124">la liste hello toospecify de nom commun de service et les empreintes numériques de l’émetteur, ajoutez un **passerelle/Http/ServiceCommonNameAndIssuer** élément sous fabricSettings, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2c03d-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="2c03d-125">Plusieurs paires d’empreinte numérique de l’émetteur et de nom commun du certificat peuvent être ajoutés dans l’élément de tableau de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="2c03d-126">Si proxy inverse du point de terminaison hello se connecte toopresents un certificat qui est commun empreinte numérique du nom et de l’émetteur correspond à une des valeurs hello spécifiés ici, le canal SSL est établi.</span><span class="sxs-lookup"><span data-stu-id="2c03d-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="2c03d-127">Sur les détails du certificat échec toomatch hello, proxy inverse échoue demande du client hello avec un code d’état 502 (passerelle incorrecte).</span><span class="sxs-lookup"><span data-stu-id="2c03d-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="2c03d-128">ligne d’état HTTP de Hello contient également une expression de hello « Certificat SSL non valide ».</span><span class="sxs-lookup"><span data-stu-id="2c03d-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- <span data-ttu-id="2c03d-129">**ServiceCertificateThumbprints**: proxy inverse vérifiera le certificat de service proxy hello en fonction de son empreinte.</span><span class="sxs-lookup"><span data-stu-id="2c03d-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="2c03d-130">Vous pouvez choisir toogo cet itinéraire lorsque les services de hello sont configurés avec des certificats auto-signés : spécifiez hello **ApplicationCertificateValidationPolicy** avec la valeur **ServiceCertificateThumbprints**dans la section des paramètres d’élément de la passerelle/Http hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="2c03d-131">Spécifiez également les empreintes numériques de hello avec un **ServiceCertificateThumbprints** entrée sous la section Paramètres de l’élément de la passerelle/Http.</span><span class="sxs-lookup"><span data-stu-id="2c03d-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="2c03d-132">Plusieurs empreintes numériques peuvent être spécifiés comme une liste séparée par des virgules dans le champ de valeur hello, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2c03d-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="2c03d-133">Si l’empreinte numérique hello hello du certificat de serveur est répertorié dans cette entrée de configuration, le proxy inverse réussit connexion SSL de hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="2c03d-134">Sinon, elle met fin à la connexion de hello et échoue hello demande du client avec un 502 (passerelle incorrecte).</span><span class="sxs-lookup"><span data-stu-id="2c03d-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="2c03d-135">ligne d’état HTTP de Hello contient également une expression de hello « Certificat SSL non valide ».</span><span class="sxs-lookup"><span data-stu-id="2c03d-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="2c03d-136">Logique de sélection du point de terminaison quand les services exposent des points de terminaison sécurisés et non sécurisés</span><span class="sxs-lookup"><span data-stu-id="2c03d-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="2c03d-137">Service Fabric prend en charge la configuration de plusieurs points de terminaison pour un service.</span><span class="sxs-lookup"><span data-stu-id="2c03d-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="2c03d-138">Voir [Spécifier des ressources dans un manifeste de service](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2c03d-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="2c03d-139">Proxy inverse sélectionne l’une des hello points de terminaison tooforward hello demande selon hello **ListenerName** paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="2c03d-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="2c03d-140">S’il n’est pas spécifié, choisir n’importe quel point de terminaison à partir de la liste de points de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="2c03d-141">Maintenant, il peut s’agir d’un point de terminaison HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2c03d-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="2c03d-142">Il peut y avoir des scénarios/exigences où vous souhaitez toooperate de proxy inverse hello en « seul mode sécurisé », c'est-à-dire</span><span class="sxs-lookup"><span data-stu-id="2c03d-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="2c03d-143">Vous ne souhaitez pas hello proxy inverse sécurisé tooforward demandes toounsecured points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="2c03d-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="2c03d-144">Cela peut être obtenue en spécifiant hello **SecureOnlyMode** entrée de configuration avec la valeur **true** dans la section des paramètres d’élément de la passerelle/Http hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> <span data-ttu-id="2c03d-145">En **SecureOnlyMode**, si le client a spécifié un **ListenerName** correspondant tooan HTTP(unsecured) point de terminaison, le proxy inverse échoue demande hello avec un code d’état 404 (introuvable) de HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c03d-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="2c03d-146">Configuration de l’authentification de certificat client via le proxy inverse hello</span><span class="sxs-lookup"><span data-stu-id="2c03d-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="2c03d-147">Terminaison SSL se produit au proxy inverse de hello et toutes les données de certificat de client hello est perdue.</span><span class="sxs-lookup"><span data-stu-id="2c03d-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="2c03d-148">Pour hello services tooperform authentification par certificat client, définissez hello **ForwardClientCertificate** définition dans la section Paramètres de hello d’élément de la passerelle/Http.</span><span class="sxs-lookup"><span data-stu-id="2c03d-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="2c03d-149">Lorsque **ForwardClientCertificate** est défini trop**false**, inverser proxy ne nécessite pas de certificat de client hello pendant la négociation SSL avec le client de hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="2c03d-150">Il s’agit par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="2c03d-151">Lorsque **ForwardClientCertificate** est défini trop**true**, inverser les requêtes de proxy pour le certificat du client hello pendant la négociation SSL avec le client de hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="2c03d-152">Puis transmettra les client hello des données de certificat dans un en-tête HTTP personnalisé nommé **X-Client-certificat**.</span><span class="sxs-lookup"><span data-stu-id="2c03d-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="2c03d-153">valeur d’en-tête Hello est la chaîne de format PEM hello codé en base64 du certificat du client hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="2c03d-154">service de Hello peut réussir/échec demande hello avec le code d’état approprié après avoir inspecté les données de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="2c03d-155">Si le client de hello ne présente pas un certificat, proxy inverse transfère un en-tête vide et laissez les cas de hello hello service handle.</span><span class="sxs-lookup"><span data-stu-id="2c03d-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="2c03d-156">Le proxy inverse est un simple redirecteur.</span><span class="sxs-lookup"><span data-stu-id="2c03d-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="2c03d-157">Il n’exécute aucune validation de certificat du client hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2c03d-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c03d-158">Next steps</span></span>
* <span data-ttu-id="2c03d-159">Consultez trop[configurer les services de proxy inverse tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) exemples de modèle pour le Gestionnaire de ressources Azure tooconfigure un proxy inverse sécurisée avec les options de validation de certificat de service différent hello.</span><span class="sxs-lookup"><span data-stu-id="2c03d-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="2c03d-160">Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2c03d-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="2c03d-161">Appels de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="2c03d-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="2c03d-162">API Web qui utilise OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2c03d-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="2c03d-163">Gérer les certificats de cluster</span><span class="sxs-lookup"><span data-stu-id="2c03d-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
