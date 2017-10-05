---
title: "Communication sécurisée avec le proxy inverse Azure Service Fabric | Microsoft Docs"
description: "Configurer le proxy inverse pour permettre la communication de bout en bout sécurisée."
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
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="13c77-103">Se connecter à un service sécurisé avec le proxy inverse</span><span class="sxs-lookup"><span data-stu-id="13c77-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="13c77-104">Cet article explique comment établir une connexion sécurisée entre le proxy inverse et les services, permettant ainsi un canal sécurisé de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="13c77-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="13c77-105">La connexion à des services sécurisés est prise en charge uniquement quand le proxy inverse est configuré pour écouter sur le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="13c77-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="13c77-106">Le reste du document suppose que c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="13c77-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="13c77-107">Reportez-vous à [Proxy inverse dans Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) pour configurer le proxy inverse dans Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="13c77-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="13c77-108">Établissement d’une connexion sécurisée entre le proxy inverse et les services</span><span class="sxs-lookup"><span data-stu-id="13c77-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="13c77-109">Authentification du proxy inverse auprès des services :</span><span class="sxs-lookup"><span data-stu-id="13c77-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="13c77-110">Le proxy inverse s’identifie auprès des services à l’aide de son certificat, spécifié avec la propriété ***reverseProxyCertificate*** dans la [section du type de ressource](../azure-resource-manager/resource-group-authoring-templates.md) du **cluster**.</span><span class="sxs-lookup"><span data-stu-id="13c77-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="13c77-111">Les services peuvent implémenter la logique qui vérifie le certificat présenté par le serveur proxy inverse.</span><span class="sxs-lookup"><span data-stu-id="13c77-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="13c77-112">Les services peuvent spécifier les détails du certificat client accepté en tant que paramètres de configuration dans le package de configuration.</span><span class="sxs-lookup"><span data-stu-id="13c77-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="13c77-113">Celui-ci peut être lu au moment de l’exécution et utilisé pour valider le certificat présenté par le proxy inverse.</span><span class="sxs-lookup"><span data-stu-id="13c77-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="13c77-114">Reportez-vous à [Gestion des paramètres d’application](service-fabric-manage-multiple-environment-app-configuration.md) pour ajouter les paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="13c77-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="13c77-115">Vérification par le proxy inverse de l’identité du service via le certificat présenté par le service :</span><span class="sxs-lookup"><span data-stu-id="13c77-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="13c77-116">Pour effectuer la validation de certificat de serveur des certificats présentés par les services, le proxy inverse prend en charge une des options suivantes : None, ServiceCommonNameAndIssuer et ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="13c77-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="13c77-117">Pour sélectionner une de ces trois options, spécifiez le paramètre **ApplicationCertificateValidationPolicy** dans la section parameters de l’élément ApplicationGateway/Http sous [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="13c77-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="13c77-118">Pour des informations complètes sur la configuration de chacune de ces options, reportez-vous à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="13c77-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="13c77-119">Options de validation du certificat de service</span><span class="sxs-lookup"><span data-stu-id="13c77-119">Service certificate validation options</span></span> 

- <span data-ttu-id="13c77-120">**None** : le proxy inverse ignore la vérification du certificat de service proxy et établit une connexion sécurisée.</span><span class="sxs-lookup"><span data-stu-id="13c77-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="13c77-121">Il s’agit du comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="13c77-121">This is the default behavior.</span></span>
<span data-ttu-id="13c77-122">Attribuez à **ApplicationCertificateValidationPolicy** la valeur **None** dans la section parameters de l’élément ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="13c77-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="13c77-123">**ServiceCommonNameAndIssuer** : le proxy inverse vérifie le certificat présenté par le service en fonction du nom commun du certificat et de l’empreinte de l’émetteur immédiate : attribuez à **ApplicationCertificateValidationPolicy** la valeur **ServiceCommonNameAndIssuer** dans la section parameters de l’élément ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="13c77-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="13c77-124">Pour spécifier la liste des empreintes de l’émetteur et de noms communs de service, ajoutez un élément **ApplicationGateway/Http/ServiceCommonNameAndIssuer** sous fabricSettings, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="13c77-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="13c77-125">Plusieurs paires empreinte d’émetteur/nom commun du certificat peuvent être ajoutées à l’élément de tableau parameters.</span><span class="sxs-lookup"><span data-stu-id="13c77-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="13c77-126">Si le proxy inverse du point de terminaison se connecte pour présenter un certificat dont le nom commun et l’empreinte de l’émetteur correspondent à l’une des valeurs spécifiées ici, un canal SSL est établi.</span><span class="sxs-lookup"><span data-stu-id="13c77-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="13c77-127">Si aucune des valeurs ne correspond aux détails du certificat, le proxy inverse fait échouer la demande du client avec un code d’état 502 (passerelle incorrecte).</span><span class="sxs-lookup"><span data-stu-id="13c77-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="13c77-128">La ligne d’état HTTP contient également l’expression « Certificat SSL non valide ».</span><span class="sxs-lookup"><span data-stu-id="13c77-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="13c77-129">**ServiceCertificateThumbprints** : le proxy inverse vérifie le certificat de service proxy en fonction de son empreinte.</span><span class="sxs-lookup"><span data-stu-id="13c77-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="13c77-130">Vous pouvez opter pour cette approche si les services sont configurés avec des certificats auto-signés : attribuez à **ApplicationCertificateValidationPolicy** la valeur **ServiceCertificateThumbprints** dans la section parameters de l’élément ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="13c77-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="13c77-131">Spécifiez également les empreintes avec une entrée **ServiceCertificateThumbprints** dans la section parameters de l’élément ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="13c77-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="13c77-132">Plusieurs empreintes peuvent être spécifiées sous forme de liste séparée par des virgules dans le champ value, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="13c77-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

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

<span data-ttu-id="13c77-133">Si l’empreinte du certificat de serveur est répertoriée dans cette entrée de configuration, le proxy inverse fait réussir la connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="13c77-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="13c77-134">Dans le cas contraire, il met fin à la connexion et fait échouer la demande du client avec un code 502 (passerelle incorrecte).</span><span class="sxs-lookup"><span data-stu-id="13c77-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="13c77-135">La ligne d’état HTTP contient également l’expression « Certificat SSL non valide ».</span><span class="sxs-lookup"><span data-stu-id="13c77-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="13c77-136">Logique de sélection du point de terminaison quand les services exposent des points de terminaison sécurisés et non sécurisés</span><span class="sxs-lookup"><span data-stu-id="13c77-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="13c77-137">Service Fabric prend en charge la configuration de plusieurs points de terminaison pour un service.</span><span class="sxs-lookup"><span data-stu-id="13c77-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="13c77-138">Voir [Spécifier des ressources dans un manifeste de service](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="13c77-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="13c77-139">Le proxy inverse sélectionne un des points de terminaison pour transférer la demande en fonction du paramètre de requête **ListenerName**.</span><span class="sxs-lookup"><span data-stu-id="13c77-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="13c77-140">Si ce paramètre n’est pas spécifié, il peut choisir n’importe quel point de terminaison dans la liste de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="13c77-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="13c77-141">Maintenant, il peut s’agir d’un point de terminaison HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="13c77-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="13c77-142">Certains scénarios ou exigences peuvent justifier le fonctionnement du proxy inverse en « mode sécurisé uniquement », situations dans lesquelles</span><span class="sxs-lookup"><span data-stu-id="13c77-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="13c77-143">vous ne souhaitez pas que le proxy inverse sécurisé transfère les demandes vers des points de terminaison non sécurisés.</span><span class="sxs-lookup"><span data-stu-id="13c77-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="13c77-144">Pour ce faire, vous pouvez spécifier l’entrée de configuration **SecureOnlyMode** avec la valeur **true** dans la section parameters de l’élément ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="13c77-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="13c77-145">En mode **SecureOnlyMode**, si le client a spécifié un **ListenerName** correspondant à un point de terminaison HTTP (non sécurisé), le proxy inverse fait échouer la demande avec un code d’état 404 HTTP (introuvable).</span><span class="sxs-lookup"><span data-stu-id="13c77-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="13c77-146">Configuration de l’authentification de certificat client par le biais du proxy inverse</span><span class="sxs-lookup"><span data-stu-id="13c77-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="13c77-147">L’arrêt SSL se produit au niveau du proxy inverse et toutes les données de certificat client sont perdues.</span><span class="sxs-lookup"><span data-stu-id="13c77-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="13c77-148">Pour que les services effectuent l’authentification du certificat client, définissez le paramètre **ForwardClientCertificate** dans la section parameters de l’élément ApplicationGateway/Http.</span><span class="sxs-lookup"><span data-stu-id="13c77-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="13c77-149">Quand **ForwardClientCertificate** est défini sur **false**, le proxy inverse ne demande pas le certificat client pendant la négociation SSL avec le client.</span><span class="sxs-lookup"><span data-stu-id="13c77-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="13c77-150">Il s’agit du comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="13c77-150">This is the default behavior.</span></span>

2. <span data-ttu-id="13c77-151">Quand **ForwardClientCertificate** est défini sur **true**, le proxy inverse demande le certificat du client pendant la négociation SSL avec le client.</span><span class="sxs-lookup"><span data-stu-id="13c77-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="13c77-152">Ensuite, il envoie les données du certificat client dans un en-tête HTTP personnalisé nommé **X-Client-Certificate**.</span><span class="sxs-lookup"><span data-stu-id="13c77-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="13c77-153">La valeur d’en-tête est la chaîne de format PEM encodée en base 64 du certificat du client.</span><span class="sxs-lookup"><span data-stu-id="13c77-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="13c77-154">Le service peut faire réussir ou échouer la demande avec le code d’état approprié après avoir inspecté les données du certificat.</span><span class="sxs-lookup"><span data-stu-id="13c77-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="13c77-155">Si le client ne présente pas un certificat, le proxy inverse transfère un en-tête vide et laisse le service gérer le cas.</span><span class="sxs-lookup"><span data-stu-id="13c77-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="13c77-156">Le proxy inverse est un simple redirecteur.</span><span class="sxs-lookup"><span data-stu-id="13c77-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="13c77-157">Il n’effectue aucune validation du certificat du client.</span><span class="sxs-lookup"><span data-stu-id="13c77-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="13c77-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13c77-158">Next steps</span></span>
* <span data-ttu-id="13c77-159">Reportez-vous à [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) (Configurer le proxy inverse pour se connecter à des services sécurisés) pour obtenir des exemples de modèles Azure Resource Manager illustrant la configuration du proxy inverse sécurisé avec les différentes options de validation de certificat de service.</span><span class="sxs-lookup"><span data-stu-id="13c77-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="13c77-160">Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="13c77-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="13c77-161">Appels de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="13c77-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="13c77-162">API Web qui utilise OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="13c77-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="13c77-163">Gérer les certificats de cluster</span><span class="sxs-lookup"><span data-stu-id="13c77-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
