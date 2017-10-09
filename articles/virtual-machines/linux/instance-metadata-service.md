---
title: "aaaAzure Service de métadonnées de l’Instance pour les machines virtuelles Linux | Documents Microsoft"
description: "Interface rESTful tooget informations de Linux VM calcul, réseau et les événements de maintenance à venir."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="5f136-103">Service de métadonnées d’instances Azure pour machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="5f136-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="5f136-104">Hello Service de métadonnées de l’Instance Azure fournit des informations sur les instances de machine virtuelle qui peuvent être utilisé toomanage et configurer vos ordinateurs virtuels en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5f136-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="5f136-105">Cela inclut des informations telles que la référence (SKU), la configuration réseau et les événements de maintenance à venir.</span><span class="sxs-lookup"><span data-stu-id="5f136-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="5f136-106">Pour plus de détails sur le type des informations disponibles, voir [Catégories de métadonnées](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="5f136-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="5f136-107">Service de métadonnées de l’Instance d’Azure est un point de terminaison REST accessible tooall machines virtuelles IaaS créé via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="5f136-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="5f136-108">point de terminaison Hello est disponible sur une adresse IP non routable connue (`169.254.169.254`) qui sont accessibles uniquement à partir de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f136-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f136-109">Ce service est **généralement disponible** dans les régions Azure globales.</span><span class="sxs-lookup"><span data-stu-id="5f136-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="5f136-110">Il est en disponible en préversion publique pour le secteur public, la Chine et le cloud Azure allemand.</span><span class="sxs-lookup"><span data-stu-id="5f136-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="5f136-111">Elle reçoit régulièrement des mises à jour tooexpose nouvelles informations sur les instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f136-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="5f136-112">Cette page ne reflète hello à jour [des catégories de données](#instance-metadata-data-categories) disponibles.</span><span class="sxs-lookup"><span data-stu-id="5f136-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="5f136-113">Disponibilité du service</span><span class="sxs-lookup"><span data-stu-id="5f136-113">Service availability</span></span>
<span data-ttu-id="5f136-114">service de Hello est disponible dans toutes les régions Azure Global disponibles.</span><span class="sxs-lookup"><span data-stu-id="5f136-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="5f136-115">service de Hello est en version préliminaire publique dans les régions gouvernement, Chine ou Allemagne hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="5f136-116">Régions</span><span class="sxs-lookup"><span data-stu-id="5f136-116">Regions</span></span>                                        | <span data-ttu-id="5f136-117">Disponibilité ?</span><span class="sxs-lookup"><span data-stu-id="5f136-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="5f136-118">Toutes les régions Azure globales généralement disponibles</span><span class="sxs-lookup"><span data-stu-id="5f136-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="5f136-119">Mise à la disposition générale</span><span class="sxs-lookup"><span data-stu-id="5f136-119">Generally Available</span></span> 
[<span data-ttu-id="5f136-120">Azure Government</span><span class="sxs-lookup"><span data-stu-id="5f136-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="5f136-121">En préversion</span><span class="sxs-lookup"><span data-stu-id="5f136-121">In Preview</span></span> 
[<span data-ttu-id="5f136-122">Azure Chine</span><span class="sxs-lookup"><span data-stu-id="5f136-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="5f136-123">En préversion</span><span class="sxs-lookup"><span data-stu-id="5f136-123">In Preview</span></span>
[<span data-ttu-id="5f136-124">Azure Allemagne</span><span class="sxs-lookup"><span data-stu-id="5f136-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="5f136-125">En préversion</span><span class="sxs-lookup"><span data-stu-id="5f136-125">In Preview</span></span>

<span data-ttu-id="5f136-126">Cette table est mise à jour lorsque le service de hello devient disponible dans d’autres clouds Azure.</span><span class="sxs-lookup"><span data-stu-id="5f136-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="5f136-127">tootry out hello Service de métadonnées de l’Instance, créez une machine virtuelle à partir de [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou hello [portail Azure](http://portal.azure.com) Bonjour au-dessus des régions et suivez hello ci-après.</span><span class="sxs-lookup"><span data-stu-id="5f136-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="5f136-128">Usage</span><span class="sxs-lookup"><span data-stu-id="5f136-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="5f136-129">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="5f136-129">Versioning</span></span>
<span data-ttu-id="5f136-130">Hello Service de métadonnées de l’Instance est créée.</span><span class="sxs-lookup"><span data-stu-id="5f136-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="5f136-131">Les versions sont obligatoires et la version actuelle de hello est `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="5f136-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="5f136-132">Versions précédentes de l’aperçu des événements planifiés pris en charge {dernière} en tant que version d’api hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="5f136-133">Ce format n’est plus pris en charge et sera déconseillé dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="5f136-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="5f136-134">Au fur et à mesure que nous ajoutons des versions plus récentes, les versions antérieures sont toujours accessibles pour des questions de compatibilité si vos scripts ont des dépendances sur des formats de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5f136-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="5f136-135">Toutefois, notez que version(2017-03-01) version préliminaire actuelle de hello ne soient pas disponibles une fois que le service de hello est généralement disponible.</span><span class="sxs-lookup"><span data-stu-id="5f136-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="5f136-136">Utilisation d’en-têtes</span><span class="sxs-lookup"><span data-stu-id="5f136-136">Using headers</span></span>
<span data-ttu-id="5f136-137">Lorsque vous interrogez hello Service de métadonnées de l’Instance, vous devez fournir l’en-tête de hello `Metadata: true` demande de hello tooensure n’a pas été redirigée involontairement.</span><span class="sxs-lookup"><span data-stu-id="5f136-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="5f136-138">Récupération des métadonnées</span><span class="sxs-lookup"><span data-stu-id="5f136-138">Retrieving metadata</span></span>

<span data-ttu-id="5f136-139">Les métadonnées Instance sont disponibles pour l’exécution de machines virtuelles créées/gérées à l’aide [d’Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="5f136-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="5f136-140">Accéder à toutes les catégories de données pour une instance de machine virtuelle à l’aide de hello demande :</span><span class="sxs-lookup"><span data-stu-id="5f136-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="5f136-141">Toutes les requêtes de métadonnées d’instance respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="5f136-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="5f136-142">Sortie des données</span><span class="sxs-lookup"><span data-stu-id="5f136-142">Data output</span></span>
<span data-ttu-id="5f136-143">Par défaut, hello Service de métadonnées de l’Instance retourne des données au format JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="5f136-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="5f136-144">Toutefois, différentes API peuvent retourner des données dans des formats différents si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5f136-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="5f136-145">Hello tableau suivant est une référence d’autres API peut prendre en charge les formats de données.</span><span class="sxs-lookup"><span data-stu-id="5f136-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="5f136-146">API</span><span class="sxs-lookup"><span data-stu-id="5f136-146">API</span></span> | <span data-ttu-id="5f136-147">Format de données par défaut</span><span class="sxs-lookup"><span data-stu-id="5f136-147">Default Data Format</span></span> | <span data-ttu-id="5f136-148">Autres formats</span><span class="sxs-lookup"><span data-stu-id="5f136-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="5f136-149">/instance</span><span class="sxs-lookup"><span data-stu-id="5f136-149">/instance</span></span> | <span data-ttu-id="5f136-150">json</span><span class="sxs-lookup"><span data-stu-id="5f136-150">json</span></span> | <span data-ttu-id="5f136-151">texte</span><span class="sxs-lookup"><span data-stu-id="5f136-151">text</span></span>
<span data-ttu-id="5f136-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="5f136-152">/scheduledevents</span></span> | <span data-ttu-id="5f136-153">json</span><span class="sxs-lookup"><span data-stu-id="5f136-153">json</span></span> | <span data-ttu-id="5f136-154">Aucun</span><span class="sxs-lookup"><span data-stu-id="5f136-154">none</span></span>

<span data-ttu-id="5f136-155">tooaccess un format de réponse non-par défaut, spécifiez au format requis de hello comme un paramètre de chaîne de requête dans la demande hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="5f136-156">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5f136-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="5f136-157">Sécurité</span><span class="sxs-lookup"><span data-stu-id="5f136-157">Security</span></span>
<span data-ttu-id="5f136-158">point de terminaison de Service de métadonnées d’Instance Hello est accessible uniquement à partir de hello instance de machine virtuelle en cours d’exécution sur une adresse IP non routable.</span><span class="sxs-lookup"><span data-stu-id="5f136-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="5f136-159">En outre, toute demande avec un `X-Forwarded-For` en-tête est refusé par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="5f136-160">Nous avons besoin également les demandes toocontain un `Metadata: true` tooensure d’en-tête qui hello demande réelle a été directement prévu et ne fait pas partie de la redirection involontaire.</span><span class="sxs-lookup"><span data-stu-id="5f136-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="5f136-161">Error</span><span class="sxs-lookup"><span data-stu-id="5f136-161">Error</span></span>
<span data-ttu-id="5f136-162">S’il existe un élément de données introuvable ou une requête mal formée, hello Service de métadonnées de l’Instance retourne des erreurs HTTP standards.</span><span class="sxs-lookup"><span data-stu-id="5f136-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="5f136-163">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5f136-163">For example:</span></span>

<span data-ttu-id="5f136-164">Code d’état HTTP</span><span class="sxs-lookup"><span data-stu-id="5f136-164">HTTP Status Code</span></span> | <span data-ttu-id="5f136-165">Motif</span><span class="sxs-lookup"><span data-stu-id="5f136-165">Reason</span></span>
----------------|-------
<span data-ttu-id="5f136-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="5f136-166">200 OK</span></span> |
<span data-ttu-id="5f136-167">400 Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="5f136-167">400 Bad Request</span></span> | <span data-ttu-id="5f136-168">En-tête `Metadata: true` manquant</span><span class="sxs-lookup"><span data-stu-id="5f136-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="5f136-169">404 Introuvable</span><span class="sxs-lookup"><span data-stu-id="5f136-169">404 Not Found</span></span> | <span data-ttu-id="5f136-170">Hello n’utilise pas de l’élément demandé existe</span><span class="sxs-lookup"><span data-stu-id="5f136-170">hello requested element does't exist</span></span> 
<span data-ttu-id="5f136-171">405 Méthode non autorisée</span><span class="sxs-lookup"><span data-stu-id="5f136-171">405 Method Not Allowed</span></span> | <span data-ttu-id="5f136-172">Seules les demandes `GET` et `POST` sont prises en charge</span><span class="sxs-lookup"><span data-stu-id="5f136-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="5f136-173">429 Trop de demandes</span><span class="sxs-lookup"><span data-stu-id="5f136-173">429 Too Many Requests</span></span> | <span data-ttu-id="5f136-174">API de Hello prend actuellement en charge un maximum de 5 requêtes par seconde</span><span class="sxs-lookup"><span data-stu-id="5f136-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="5f136-175">500 Erreur de service</span><span class="sxs-lookup"><span data-stu-id="5f136-175">500 Service Error</span></span>     | <span data-ttu-id="5f136-176">Recommencez l’opération plus tard</span><span class="sxs-lookup"><span data-stu-id="5f136-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="5f136-177">Exemples</span><span class="sxs-lookup"><span data-stu-id="5f136-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="5f136-178">Toutes les réponses de l’API sont des chaînes JSON.</span><span class="sxs-lookup"><span data-stu-id="5f136-178">All API responses are JSON strings.</span></span> <span data-ttu-id="5f136-179">Tous les exemples de réponses suivants sont imprimés avec soin par souci de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="5f136-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="5f136-180">Récupération des informations réseau</span><span class="sxs-lookup"><span data-stu-id="5f136-180">Retrieving network information</span></span>

<span data-ttu-id="5f136-181">**Requête**</span><span class="sxs-lookup"><span data-stu-id="5f136-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="5f136-182">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="5f136-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="5f136-183">réponse de Hello est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="5f136-183">hello response is a JSON string.</span></span> <span data-ttu-id="5f136-184">Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="5f136-184">hello following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="5f136-185">Récupération de l’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="5f136-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="5f136-186">Récupération de toutes les métadonnées d’une instance</span><span class="sxs-lookup"><span data-stu-id="5f136-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="5f136-187">**Requête**</span><span class="sxs-lookup"><span data-stu-id="5f136-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="5f136-188">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="5f136-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="5f136-189">réponse de Hello est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="5f136-189">hello response is a JSON string.</span></span> <span data-ttu-id="5f136-190">Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="5f136-190">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="5f136-191">Récupération de métadonnées dans une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="5f136-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="5f136-192">**Requête**</span><span class="sxs-lookup"><span data-stu-id="5f136-192">**Request**</span></span>

<span data-ttu-id="5f136-193">Métadonnées de l’instance peuvent être récupérée dans Windows via hello PowerShell utilitaire `curl`:</span><span class="sxs-lookup"><span data-stu-id="5f136-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="5f136-194">Ou via hello `Invoke-RestMethod` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="5f136-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="5f136-195">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="5f136-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="5f136-196">réponse de Hello est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="5f136-196">hello response is a JSON string.</span></span> <span data-ttu-id="5f136-197">Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="5f136-197">hello following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="5f136-198">Catégories de données de métadonnées Instance</span><span class="sxs-lookup"><span data-stu-id="5f136-198">Instance metadata data categories</span></span>
<span data-ttu-id="5f136-199">Hello suivant des catégories de données est disponible via hello Service de métadonnées de l’Instance :</span><span class="sxs-lookup"><span data-stu-id="5f136-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="5f136-200">Données</span><span class="sxs-lookup"><span data-stu-id="5f136-200">Data</span></span> | <span data-ttu-id="5f136-201">Description</span><span class="sxs-lookup"><span data-stu-id="5f136-201">Description</span></span>
-----|------------
<span data-ttu-id="5f136-202">location</span><span class="sxs-lookup"><span data-stu-id="5f136-202">location</span></span> | <span data-ttu-id="5f136-203">Hello de région Azure VM s’exécute dans</span><span class="sxs-lookup"><span data-stu-id="5f136-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="5f136-204">name</span><span class="sxs-lookup"><span data-stu-id="5f136-204">name</span></span> | <span data-ttu-id="5f136-205">Nom de la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="5f136-205">Name of hello VM</span></span> 
<span data-ttu-id="5f136-206">offer</span><span class="sxs-lookup"><span data-stu-id="5f136-206">offer</span></span> | <span data-ttu-id="5f136-207">Fournissent des informations pour l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-207">Offer information for hello VM image.</span></span> <span data-ttu-id="5f136-208">Cette valeur est uniquement présente pour les images déployées à partir de la galerie d’images Azure.</span><span class="sxs-lookup"><span data-stu-id="5f136-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="5f136-209">publisher</span><span class="sxs-lookup"><span data-stu-id="5f136-209">publisher</span></span> | <span data-ttu-id="5f136-210">Serveur de publication de l’image de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="5f136-210">Publisher of hello VM image</span></span>
<span data-ttu-id="5f136-211">sku</span><span class="sxs-lookup"><span data-stu-id="5f136-211">sku</span></span> | <span data-ttu-id="5f136-212">Référence (SKU) spécifique pour l’image de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="5f136-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="5f136-213">version</span><span class="sxs-lookup"><span data-stu-id="5f136-213">version</span></span> | <span data-ttu-id="5f136-214">Version de l’image de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="5f136-214">Version of hello VM image</span></span> 
<span data-ttu-id="5f136-215">osType</span><span class="sxs-lookup"><span data-stu-id="5f136-215">osType</span></span> | <span data-ttu-id="5f136-216">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="5f136-216">Linux or Windows</span></span> 
<span data-ttu-id="5f136-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="5f136-217">platformUpdateDomain</span></span> |  <span data-ttu-id="5f136-218">[Domaine de mise à jour](manage-availability.md) hello machine virtuelle est en cours d’exécution dans</span><span class="sxs-lookup"><span data-stu-id="5f136-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="5f136-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="5f136-219">platformFaultDomain</span></span> | <span data-ttu-id="5f136-220">[Domaine d’erreur](manage-availability.md) hello machine virtuelle est en cours d’exécution dans</span><span class="sxs-lookup"><span data-stu-id="5f136-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="5f136-221">vmId</span><span class="sxs-lookup"><span data-stu-id="5f136-221">vmId</span></span> | <span data-ttu-id="5f136-222">[Identificateur unique](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) pour hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="5f136-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="5f136-223">vmSize</span></span> | [<span data-ttu-id="5f136-224">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-224">VM size</span></span>](sizes.md)
<span data-ttu-id="5f136-225">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="5f136-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="5f136-226">Adresse IPv4 locale de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="5f136-227">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5f136-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="5f136-228">Adresse IPv4 publique de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="5f136-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="5f136-229">subnet/address</span></span> | <span data-ttu-id="5f136-230">Adresse de sous-réseau de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-230">Subnet address of hello VM</span></span>
<span data-ttu-id="5f136-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="5f136-231">subnet/prefix</span></span> | <span data-ttu-id="5f136-232">Préfixe de sous-réseau, par exemple 24</span><span class="sxs-lookup"><span data-stu-id="5f136-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="5f136-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="5f136-233">ipv6/ipAddress</span></span> | <span data-ttu-id="5f136-234">Adresse IPv6 locale de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="5f136-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="5f136-235">macAddress</span></span> | <span data-ttu-id="5f136-236">Adresse MAC de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-236">VM mac address</span></span> 
<span data-ttu-id="5f136-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="5f136-237">scheduledevents</span></span> | <span data-ttu-id="5f136-238">Actuellement en préversion publique. Voir [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="5f136-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="5f136-239">Exemples de scénarios d’utilisation</span><span class="sxs-lookup"><span data-stu-id="5f136-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="5f136-240">Suivi de la machine virtuelle s’exécutant sur Azure</span><span class="sxs-lookup"><span data-stu-id="5f136-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="5f136-241">En tant qu’un fournisseur de services, vous pouvez avoir besoin de nombre de hello tootrack de machines virtuelles exécutant votre logiciel ou ont des agents nécessitant l’unicité de tootrack Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f136-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="5f136-242">toobe en mesure de tooget un ID unique pour une machine virtuelle, utilisez hello `vmId` champ à partir du Service de métadonnées de l’Instance.</span><span class="sxs-lookup"><span data-stu-id="5f136-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="5f136-243">**Requête**</span><span class="sxs-lookup"><span data-stu-id="5f136-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="5f136-244">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="5f136-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="5f136-245">Positionnement du domaine d’erreur/de mise à jour basé sur des conteneurs et des partitions de données</span><span class="sxs-lookup"><span data-stu-id="5f136-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="5f136-246">Pour certains scénarios, le positionnement des différents réplicas de données est de première importance.</span><span class="sxs-lookup"><span data-stu-id="5f136-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="5f136-247">Par exemple, [la sélection élective du réplica HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou l’emplacement du conteneur via une [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) nécessiter tooknow hello `platformFaultDomain` et `platformUpdateDomain` hello machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5f136-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="5f136-248">Vous pouvez interroger ces données directement via hello Service de métadonnées de l’Instance.</span><span class="sxs-lookup"><span data-stu-id="5f136-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="5f136-249">**Requête**</span><span class="sxs-lookup"><span data-stu-id="5f136-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="5f136-250">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="5f136-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="5f136-251">Obtenir plus d’informations sur hello VM au cours de la demande de support</span><span class="sxs-lookup"><span data-stu-id="5f136-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="5f136-252">Fournisseur de service, vous pouvez obtenir un appel de la prise en charge dans laquelle vous voulez tooknow plus d’informations sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="5f136-253">Demandant hello client tooshare hello calcul métadonnées peuvent fournir des informations de base pour tooknow professionnelle de hello prise en charge de type hello de machine virtuelle sur Azure.</span><span class="sxs-lookup"><span data-stu-id="5f136-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="5f136-254">**Requête**</span><span class="sxs-lookup"><span data-stu-id="5f136-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="5f136-255">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="5f136-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="5f136-256">réponse de Hello est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="5f136-256">hello response is a JSON string.</span></span> <span data-ttu-id="5f136-257">Hello suivant l’exemple de réponse est automatiquement imprimé pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="5f136-257">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="5f136-258">Exemples d’appel de service de métadonnées à l’aide de différentes langues à l’intérieur de hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="5f136-259">language</span><span class="sxs-lookup"><span data-stu-id="5f136-259">Language</span></span> | <span data-ttu-id="5f136-260">Exemple</span><span class="sxs-lookup"><span data-stu-id="5f136-260">Example</span></span> 
---------|----------------
<span data-ttu-id="5f136-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="5f136-261">Ruby</span></span>     | <span data-ttu-id="5f136-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="5f136-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="5f136-263">Go Lan</span><span class="sxs-lookup"><span data-stu-id="5f136-263">Go Lan</span></span>   | <span data-ttu-id="5f136-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="5f136-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="5f136-265">python</span><span class="sxs-lookup"><span data-stu-id="5f136-265">python</span></span>   | <span data-ttu-id="5f136-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="5f136-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="5f136-267">C++</span><span class="sxs-lookup"><span data-stu-id="5f136-267">C++</span></span>      | <span data-ttu-id="5f136-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="5f136-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="5f136-269">C#</span><span class="sxs-lookup"><span data-stu-id="5f136-269">C#</span></span>       | <span data-ttu-id="5f136-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="5f136-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="5f136-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="5f136-271">Javascript</span></span> | <span data-ttu-id="5f136-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="5f136-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="5f136-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f136-273">Powershell</span></span> | <span data-ttu-id="5f136-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="5f136-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="5f136-275">Bash</span><span class="sxs-lookup"><span data-stu-id="5f136-275">Bash</span></span>       | <span data-ttu-id="5f136-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="5f136-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="5f136-277">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="5f136-277">FAQ</span></span>
1. <span data-ttu-id="5f136-278">J’obtiens une erreur de hello `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="5f136-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="5f136-279">Qu’est-ce que cela signifie ?</span><span class="sxs-lookup"><span data-stu-id="5f136-279">What does this mean?</span></span>
   * <span data-ttu-id="5f136-280">Service de métadonnées de l’Instance de Hello nécessite des en-tête de hello `Metadata: true` toobe passé dans la demande hello.</span><span class="sxs-lookup"><span data-stu-id="5f136-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="5f136-281">Cet en-tête de passage dans l’appel REST hello permet toohello d’accès aux métadonnées de Service de l’Instance.</span><span class="sxs-lookup"><span data-stu-id="5f136-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="5f136-282">Pourquoi je n’obtiens pas les informations de calcul pour ma machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="5f136-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="5f136-283">Actuellement hello Service de métadonnées d’Instance prend uniquement en charge les instances créées avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f136-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="5f136-284">Bonjour future, nous pouvons ajouter prise en charge pour les machines virtuelles du Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="5f136-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="5f136-285">J’ai créé une machine virtuelle via Azure Resource Manager il y quelque temps déjà.</span><span class="sxs-lookup"><span data-stu-id="5f136-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="5f136-286">Pourquoi ne puis-je pas voir les informations de métadonnées de calcul ?</span><span class="sxs-lookup"><span data-stu-id="5f136-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="5f136-287">Pour les ordinateurs virtuels créés après septembre 2016, ajoutez un [balise](../../azure-resource-manager/resource-group-using-tags.md) toostart voir calcul métadonnées.</span><span class="sxs-lookup"><span data-stu-id="5f136-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="5f136-288">Pour les anciens VM (créée avant septembre 2016), ajouter/supprimer les données ou les extensions de métadonnées disques toohello VM toorefresh.</span><span class="sxs-lookup"><span data-stu-id="5f136-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="5f136-289">Pour quelle raison obtenez-vous erreur de hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="5f136-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="5f136-290">Renouvelez votre demande en fonction du système d’interruption exponentiel.</span><span class="sxs-lookup"><span data-stu-id="5f136-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="5f136-291">Si le problème de hello persiste, contactez le support Azure.</span><span class="sxs-lookup"><span data-stu-id="5f136-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="5f136-292">Où partager des commentaires/questions supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="5f136-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="5f136-293">Envoyez vos commentaires au site http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="5f136-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="5f136-294">Cela fonctionne-t-il pour l’instance de groupe de machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="5f136-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="5f136-295">Oui, le service de métadonnées est disponible pour les instances de groupe identique.</span><span class="sxs-lookup"><span data-stu-id="5f136-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="5f136-296">Comment obtenir un support technique pour le service de hello ?</span><span class="sxs-lookup"><span data-stu-id="5f136-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="5f136-297">prise en charge de tooget pour le service de hello, créer un problème de prise en charge dans le portail Azure pour hello où vous n’êtes pas en mesure de tooget réponse des métadonnées après plusieurs tentatives longues de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5f136-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Support des métadonnées d’instance](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="5f136-299">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f136-299">Next steps</span></span>

- <span data-ttu-id="5f136-300">En savoir plus sur hello [événements planifiés](scheduled-events.md) API **en version préliminaire publique** fournie par hello service de métadonnées de l’Instance.</span><span class="sxs-lookup"><span data-stu-id="5f136-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
