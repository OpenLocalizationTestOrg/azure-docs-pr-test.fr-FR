---
title: "Vue d’ensemble du service de métadonnées Instance Azure | Microsoft Docs"
description: "Interface RESTful permettant d’obtenir des informations sur le calcul, le réseau et les événements de maintenance à venir de la machine virtuelle."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="e5243-103">Service de métadonnées d’instance Azure</span><span class="sxs-lookup"><span data-stu-id="e5243-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="e5243-104">Le service de métadonnées d’instance Azure fournit des informations sur les instances de machine virtuelle en cours d’exécution qui peuvent être utilisées pour gérer et configurer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e5243-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="e5243-105">Cela inclut des informations telles que la référence (SKU), la configuration réseau et les événements de maintenance à venir.</span><span class="sxs-lookup"><span data-stu-id="e5243-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="e5243-106">Pour plus de détails sur le type des informations disponibles, voir [Catégories de métadonnées](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="e5243-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="e5243-107">Le service de métadonnées d’instance d’Azure est un point de terminaison REST accessible à toutes les machines virtuelles IaaS créées via [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="e5243-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="e5243-108">Le point de terminaison est disponible à une adresse IP non routable bien connue (`169.254.169.254`) accessible uniquement à partir de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e5243-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="e5243-109">Informations importantes</span><span class="sxs-lookup"><span data-stu-id="e5243-109">Important information</span></span>

<span data-ttu-id="e5243-110">Ce service est **généralement disponible** dans les régions Azure globales.</span><span class="sxs-lookup"><span data-stu-id="e5243-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="e5243-111">Il est en disponible en préversion publique pour le secteur public, la Chine et le cloud Azure allemand.</span><span class="sxs-lookup"><span data-stu-id="e5243-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="e5243-112">Il reçoit régulièrement des mises à jour pour exposer de nouvelles informations sur les instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e5243-112">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="e5243-113">Cette page ne reflète les [catégories de données](#instance-metadata-data-categories) à jour disponibles.</span><span class="sxs-lookup"><span data-stu-id="e5243-113">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="e5243-114">Disponibilité des services</span><span class="sxs-lookup"><span data-stu-id="e5243-114">Service Availability</span></span>
<span data-ttu-id="e5243-115">Le service est disponible dans toutes les régions Azure globales disponibles.</span><span class="sxs-lookup"><span data-stu-id="e5243-115">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="e5243-116">Il est en disponible en préversion publique dans les régions Secteur public, Chine et Allemagne.</span><span class="sxs-lookup"><span data-stu-id="e5243-116">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="e5243-117">Régions</span><span class="sxs-lookup"><span data-stu-id="e5243-117">Regions</span></span>                                        | <span data-ttu-id="e5243-118">Disponibilité ?</span><span class="sxs-lookup"><span data-stu-id="e5243-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="e5243-119">Toutes les régions Azure globales généralement disponibles</span><span class="sxs-lookup"><span data-stu-id="e5243-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="e5243-120">Mise à la disposition générale</span><span class="sxs-lookup"><span data-stu-id="e5243-120">Generally Available</span></span> 
[<span data-ttu-id="e5243-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="e5243-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="e5243-122">En préversion</span><span class="sxs-lookup"><span data-stu-id="e5243-122">In Preview</span></span> 
[<span data-ttu-id="e5243-123">Azure Chine</span><span class="sxs-lookup"><span data-stu-id="e5243-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="e5243-124">En préversion</span><span class="sxs-lookup"><span data-stu-id="e5243-124">In Preview</span></span>
[<span data-ttu-id="e5243-125">Azure Allemagne</span><span class="sxs-lookup"><span data-stu-id="e5243-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="e5243-126">En préversion</span><span class="sxs-lookup"><span data-stu-id="e5243-126">In Preview</span></span>

<span data-ttu-id="e5243-127">Ce tableau est mis à jour lorsque le service devient disponible dans d’autres clouds Azure.</span><span class="sxs-lookup"><span data-stu-id="e5243-127">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="e5243-128">Pour tester le service de métadonnées d’instance, créez une machine virtuelle à partir d’[Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou du [portail Azure](http://portal.azure.com) dans les régions ci-dessus, puis suivez les exemples ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e5243-128">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="e5243-129">Usage</span><span class="sxs-lookup"><span data-stu-id="e5243-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="e5243-130">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="e5243-130">Versioning</span></span>
<span data-ttu-id="e5243-131">Le service de métadonnées Instance fait l’objet d’une gestion de version.</span><span class="sxs-lookup"><span data-stu-id="e5243-131">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="e5243-132">Les versions sont obligatoires et la version actuelle est `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="e5243-132">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="e5243-133">Les préversions précédentes des événements planifiés prenaient en charge {dernière version} en tant que version de l’api.</span><span class="sxs-lookup"><span data-stu-id="e5243-133">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="e5243-134">Ce format n’est plus pris en charge et sera déconseillé à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="e5243-134">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="e5243-135">Au fur et à mesure que nous ajoutons des versions plus récentes, les versions antérieures sont toujours accessibles pour des questions de compatibilité si vos scripts ont des dépendances sur des formats de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e5243-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="e5243-136">Notez cependant que la préversion actuelle (2017-03-01) ne sera peut-être pas disponible lors de la mise à la disposition générale du service.</span><span class="sxs-lookup"><span data-stu-id="e5243-136">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="e5243-137">Utilisation d'en-têtes</span><span class="sxs-lookup"><span data-stu-id="e5243-137">Using Headers</span></span>
<span data-ttu-id="e5243-138">Quand vous interrogez le service de métadonnées d’instance, vous devez fournir l’en-tête `Metadata: true` pour garantir que la demande n’a pas été redirigée involontairement.</span><span class="sxs-lookup"><span data-stu-id="e5243-138">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="e5243-139">Récupération des métadonnées</span><span class="sxs-lookup"><span data-stu-id="e5243-139">Retrieving metadata</span></span>

<span data-ttu-id="e5243-140">Les métadonnées Instance sont disponibles pour l’exécution de machines virtuelles créées/gérées à l’aide [d’Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="e5243-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="e5243-141">Accédez à toutes les catégories de données pour une instance de machine virtuelle à l’aide de la demande suivante :</span><span class="sxs-lookup"><span data-stu-id="e5243-141">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="e5243-142">Toutes les requêtes de métadonnées d’instance respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="e5243-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="e5243-143">Sortie des données</span><span class="sxs-lookup"><span data-stu-id="e5243-143">Data output</span></span>
<span data-ttu-id="e5243-144">Par défaut, le service de métadonnées d’instance retourne des données au format JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="e5243-144">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="e5243-145">Toutefois, différentes API peuvent retourner des données dans des formats différents si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e5243-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="e5243-146">Le tableau suivant répertorie les autres formats de données que les API peuvent prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="e5243-146">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="e5243-147">API</span><span class="sxs-lookup"><span data-stu-id="e5243-147">API</span></span> | <span data-ttu-id="e5243-148">Format de données par défaut</span><span class="sxs-lookup"><span data-stu-id="e5243-148">Default Data Format</span></span> | <span data-ttu-id="e5243-149">Autres formats</span><span class="sxs-lookup"><span data-stu-id="e5243-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="e5243-150">/instance</span><span class="sxs-lookup"><span data-stu-id="e5243-150">/instance</span></span> | <span data-ttu-id="e5243-151">json</span><span class="sxs-lookup"><span data-stu-id="e5243-151">json</span></span> | <span data-ttu-id="e5243-152">texte</span><span class="sxs-lookup"><span data-stu-id="e5243-152">text</span></span>
<span data-ttu-id="e5243-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="e5243-153">/scheduledevents</span></span> | <span data-ttu-id="e5243-154">json</span><span class="sxs-lookup"><span data-stu-id="e5243-154">json</span></span> | <span data-ttu-id="e5243-155">Aucun</span><span class="sxs-lookup"><span data-stu-id="e5243-155">none</span></span>

<span data-ttu-id="e5243-156">Pour accéder à un format de réponse autre que le format par défaut, spécifiez le format demandé en tant que paramètre de chaîne de requête dans la demande.</span><span class="sxs-lookup"><span data-stu-id="e5243-156">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="e5243-157">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e5243-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="e5243-158">Sécurité</span><span class="sxs-lookup"><span data-stu-id="e5243-158">Security</span></span>
<span data-ttu-id="e5243-159">Le point de terminaison du service de métadonnées d’instance est accessible uniquement à partir de l’instance de machine virtuelle active sur une adresse IP non routable.</span><span class="sxs-lookup"><span data-stu-id="e5243-159">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="e5243-160">En outre, toute demande contenant un en-tête `X-Forwarded-For` est rejetée par le service.</span><span class="sxs-lookup"><span data-stu-id="e5243-160">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="e5243-161">Nous exigeons également que toute demande contienne un en-tête `Metadata: true` garantissant que la demande est réellement intentionnelle et ne fait pas partie d’une redirection involontaire.</span><span class="sxs-lookup"><span data-stu-id="e5243-161">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="e5243-162">Error</span><span class="sxs-lookup"><span data-stu-id="e5243-162">Error</span></span>
<span data-ttu-id="e5243-163">S’il existe un élément de données introuvable ou une requête mal formée, le service de métadonnées d’instance retourne des erreurs HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="e5243-163">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="e5243-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e5243-164">For example:</span></span>

<span data-ttu-id="e5243-165">Code d’état HTTP</span><span class="sxs-lookup"><span data-stu-id="e5243-165">HTTP Status Code</span></span> | <span data-ttu-id="e5243-166">Motif</span><span class="sxs-lookup"><span data-stu-id="e5243-166">Reason</span></span>
----------------|-------
<span data-ttu-id="e5243-167">200 OK</span><span class="sxs-lookup"><span data-stu-id="e5243-167">200 OK</span></span> |
<span data-ttu-id="e5243-168">400 Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="e5243-168">400 Bad Request</span></span> | <span data-ttu-id="e5243-169">En-tête `Metadata: true` manquant</span><span class="sxs-lookup"><span data-stu-id="e5243-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="e5243-170">404 Introuvable</span><span class="sxs-lookup"><span data-stu-id="e5243-170">404 Not Found</span></span> | <span data-ttu-id="e5243-171">L’élément demandé n’existe pas</span><span class="sxs-lookup"><span data-stu-id="e5243-171">The requested element does't exist</span></span> 
<span data-ttu-id="e5243-172">405 Méthode non autorisée</span><span class="sxs-lookup"><span data-stu-id="e5243-172">405 Method Not Allowed</span></span> | <span data-ttu-id="e5243-173">Seules les demandes `GET` et `POST` sont prises en charge</span><span class="sxs-lookup"><span data-stu-id="e5243-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="e5243-174">429 Trop de demandes</span><span class="sxs-lookup"><span data-stu-id="e5243-174">429 Too Many Requests</span></span> | <span data-ttu-id="e5243-175">L’API prend actuellement en charge un maximum de 5 requêtes par seconde</span><span class="sxs-lookup"><span data-stu-id="e5243-175">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="e5243-176">500 Erreur de service</span><span class="sxs-lookup"><span data-stu-id="e5243-176">500 Service Error</span></span>     | <span data-ttu-id="e5243-177">Recommencez l’opération plus tard</span><span class="sxs-lookup"><span data-stu-id="e5243-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="e5243-178">Exemples</span><span class="sxs-lookup"><span data-stu-id="e5243-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="e5243-179">Toutes les réponses de l’API sont des chaînes JSON.</span><span class="sxs-lookup"><span data-stu-id="e5243-179">All API responses are JSON strings.</span></span> <span data-ttu-id="e5243-180">Tous les exemples de réponses suivants sont imprimés avec soin par souci de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="e5243-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="e5243-181">Récupération des informations réseau</span><span class="sxs-lookup"><span data-stu-id="e5243-181">Retrieving network information</span></span>

<span data-ttu-id="e5243-182">**Requête**</span><span class="sxs-lookup"><span data-stu-id="e5243-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="e5243-183">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e5243-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="e5243-184">La réponse est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="e5243-184">The response is a JSON string.</span></span> <span data-ttu-id="e5243-185">L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="e5243-185">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="e5243-186">Récupération de l’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="e5243-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="e5243-187">Récupération de toutes les métadonnées d’une instance</span><span class="sxs-lookup"><span data-stu-id="e5243-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="e5243-188">**Requête**</span><span class="sxs-lookup"><span data-stu-id="e5243-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="e5243-189">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e5243-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="e5243-190">La réponse est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="e5243-190">The response is a JSON string.</span></span> <span data-ttu-id="e5243-191">L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="e5243-191">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="e5243-192">Récupération de métadonnées dans une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="e5243-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="e5243-193">**Requête**</span><span class="sxs-lookup"><span data-stu-id="e5243-193">**Request**</span></span>

<span data-ttu-id="e5243-194">Les métadonnées d’instance peuvent être récupérées dans Windows via l’utilitaire Powershell `curl` :</span><span class="sxs-lookup"><span data-stu-id="e5243-194">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="e5243-195">Ou via l’applet de commande `Invoke-RestMethod` :</span><span class="sxs-lookup"><span data-stu-id="e5243-195">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="e5243-196">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e5243-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="e5243-197">La réponse est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="e5243-197">The response is a JSON string.</span></span> <span data-ttu-id="e5243-198">L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="e5243-198">The following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="e5243-199">Catégories de données de métadonnées Instance</span><span class="sxs-lookup"><span data-stu-id="e5243-199">Instance metadata data categories</span></span>
<span data-ttu-id="e5243-200">Les catégories de données suivantes sont disponibles via le service de métadonnées d’instance :</span><span class="sxs-lookup"><span data-stu-id="e5243-200">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="e5243-201">Données</span><span class="sxs-lookup"><span data-stu-id="e5243-201">Data</span></span> | <span data-ttu-id="e5243-202">Description</span><span class="sxs-lookup"><span data-stu-id="e5243-202">Description</span></span>
-----|------------
<span data-ttu-id="e5243-203">location</span><span class="sxs-lookup"><span data-stu-id="e5243-203">location</span></span> | <span data-ttu-id="e5243-204">Région Azure dans laquelle la machine virtuelle est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="e5243-204">Azure Region the VM is running in</span></span>
<span data-ttu-id="e5243-205">name</span><span class="sxs-lookup"><span data-stu-id="e5243-205">name</span></span> | <span data-ttu-id="e5243-206">Nom de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-206">Name of the VM</span></span> 
<span data-ttu-id="e5243-207">offer</span><span class="sxs-lookup"><span data-stu-id="e5243-207">offer</span></span> | <span data-ttu-id="e5243-208">Offrent des informations pour l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e5243-208">Offer information for the VM image.</span></span> <span data-ttu-id="e5243-209">Cette valeur est uniquement présente pour les images déployées à partir de la galerie d’images Azure.</span><span class="sxs-lookup"><span data-stu-id="e5243-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="e5243-210">publisher</span><span class="sxs-lookup"><span data-stu-id="e5243-210">publisher</span></span> | <span data-ttu-id="e5243-211">Éditeur de l’image de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-211">Publisher of the VM image</span></span>
<span data-ttu-id="e5243-212">sku</span><span class="sxs-lookup"><span data-stu-id="e5243-212">sku</span></span> | <span data-ttu-id="e5243-213">Référence (SKU) spécifique pour l’image de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-213">Specific SKU for the VM image</span></span>  
<span data-ttu-id="e5243-214">version</span><span class="sxs-lookup"><span data-stu-id="e5243-214">version</span></span> | <span data-ttu-id="e5243-215">Version de l’image de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-215">Version of the VM image</span></span> 
<span data-ttu-id="e5243-216">osType</span><span class="sxs-lookup"><span data-stu-id="e5243-216">osType</span></span> | <span data-ttu-id="e5243-217">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="e5243-217">Linux or Windows</span></span> 
<span data-ttu-id="e5243-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="e5243-218">platformUpdateDomain</span></span> |  <span data-ttu-id="e5243-219">[Domaine de mise à jour](virtual-machines-windows-manage-availability.md) dans lequel la machine virtuelle est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="e5243-219">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="e5243-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="e5243-220">platformFaultDomain</span></span> | <span data-ttu-id="e5243-221">[Domaine par défaut](virtual-machines-windows-manage-availability.md) dans lequel la machine virtuelle est en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="e5243-221">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="e5243-222">vmId</span><span class="sxs-lookup"><span data-stu-id="e5243-222">vmId</span></span> | <span data-ttu-id="e5243-223">[Identificateur unique](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="e5243-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="e5243-224">vmSize</span></span> | [<span data-ttu-id="e5243-225">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="e5243-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="e5243-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="e5243-227">Adresse IPv4 locale de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-227">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="e5243-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e5243-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="e5243-229">Adresse IPv4 publique de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-229">Public IPv4 address of the VM</span></span>
<span data-ttu-id="e5243-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="e5243-230">subnet/address</span></span> | <span data-ttu-id="e5243-231">Adresse de sous-réseau de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-231">Subnet address of the VM</span></span>
<span data-ttu-id="e5243-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="e5243-232">subnet/prefix</span></span> | <span data-ttu-id="e5243-233">Préfixe de sous-réseau, par exemple 24</span><span class="sxs-lookup"><span data-stu-id="e5243-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="e5243-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="e5243-234">ipv6/ipAddress</span></span> | <span data-ttu-id="e5243-235">Adresse IPv6 locale de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-235">Local IPv6 address of the VM</span></span>
<span data-ttu-id="e5243-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="e5243-236">macAddress</span></span> | <span data-ttu-id="e5243-237">Adresse MAC de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-237">VM mac address</span></span> 
<span data-ttu-id="e5243-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="e5243-238">scheduledevents</span></span> | <span data-ttu-id="e5243-239">Actuellement en préversion publique. Voir [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="e5243-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="e5243-240">Exemples de scénarios d’utilisation</span><span class="sxs-lookup"><span data-stu-id="e5243-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="e5243-241">Suivi de la machine virtuelle s’exécutant sur Azure</span><span class="sxs-lookup"><span data-stu-id="e5243-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="e5243-242">En tant que fournisseur de service, vous aurez peut-être besoin de suivre le nombre de machines virtuelles s’exécutant sur votre logiciel ou de disposer d’agents effectuant le suivi de l’unicité de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e5243-242">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="e5243-243">Pour pouvoir obtenir un ID unique pour une machine virtuelle, utilisez le champ `vmId` du service de métadonnées d’instance.</span><span class="sxs-lookup"><span data-stu-id="e5243-243">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="e5243-244">**Requête**</span><span class="sxs-lookup"><span data-stu-id="e5243-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="e5243-245">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e5243-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="e5243-246">Positionnement des conteneurs, partitions de données en fonction du domaine par défaut/de mise à jour</span><span class="sxs-lookup"><span data-stu-id="e5243-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="e5243-247">Pour certains scénarios, le positionnement des différents réplicas de données est de première importance.</span><span class="sxs-lookup"><span data-stu-id="e5243-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="e5243-248">Par exemple, pour le [positionnement du réplica HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou pour le positionnement des conteneurs via un [orchestrateur](https://kubernetes.io/docs/user-guide/node-selection/), vous devez connaître les domaines `platformFaultDomain` et `platformUpdateDomain` sur lesquels la machine virtuelle s’exécute.</span><span class="sxs-lookup"><span data-stu-id="e5243-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="e5243-249">Vous pouvez interroger ces données directement via le service de métadonnées d’instance.</span><span class="sxs-lookup"><span data-stu-id="e5243-249">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="e5243-250">**Requête**</span><span class="sxs-lookup"><span data-stu-id="e5243-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="e5243-251">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e5243-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="e5243-252">Obtenir plus d’informations sur la machine virtuelle pour le dossier de support</span><span class="sxs-lookup"><span data-stu-id="e5243-252">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="e5243-253">En tant que fournisseur de services, vous recevrez peut-être un appel du support pour lequel vous devrez connaître les informations de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e5243-253">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="e5243-254">Demandez au client de partager les métadonnées de calcul afin que l’équipe du support dispose des informations de base concernant le type de machine virtuelle sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e5243-254">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="e5243-255">**Requête**</span><span class="sxs-lookup"><span data-stu-id="e5243-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="e5243-256">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e5243-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="e5243-257">La réponse est une chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="e5243-257">The response is a JSON string.</span></span> <span data-ttu-id="e5243-258">L’exemple de réponse suivant est imprimé avec soin par souci de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="e5243-258">The following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="e5243-259">Exemples d’appels du service de métadonnées utilisant différents langages à l’intérieur de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5243-259">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="e5243-260">Langage</span><span class="sxs-lookup"><span data-stu-id="e5243-260">Language</span></span> | <span data-ttu-id="e5243-261">Exemple</span><span class="sxs-lookup"><span data-stu-id="e5243-261">Example</span></span> 
---------|----------------
<span data-ttu-id="e5243-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="e5243-262">Ruby</span></span>     | <span data-ttu-id="e5243-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="e5243-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="e5243-264">Go Lan</span><span class="sxs-lookup"><span data-stu-id="e5243-264">Go Lan</span></span>   | <span data-ttu-id="e5243-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="e5243-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="e5243-266">python</span><span class="sxs-lookup"><span data-stu-id="e5243-266">python</span></span>   | <span data-ttu-id="e5243-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="e5243-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="e5243-268">C++</span><span class="sxs-lookup"><span data-stu-id="e5243-268">C++</span></span>      | <span data-ttu-id="e5243-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="e5243-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="e5243-270">C#</span><span class="sxs-lookup"><span data-stu-id="e5243-270">C#</span></span>       | <span data-ttu-id="e5243-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="e5243-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="e5243-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="e5243-272">Javascript</span></span> | <span data-ttu-id="e5243-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="e5243-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="e5243-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5243-274">Powershell</span></span> | <span data-ttu-id="e5243-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="e5243-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="e5243-276">Bash</span><span class="sxs-lookup"><span data-stu-id="e5243-276">Bash</span></span>       | <span data-ttu-id="e5243-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="e5243-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="e5243-278">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="e5243-278">FAQ</span></span>
1. <span data-ttu-id="e5243-279">J’obtiens l’erreur `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="e5243-279">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="e5243-280">Qu’est-ce que cela signifie ?</span><span class="sxs-lookup"><span data-stu-id="e5243-280">What does this mean?</span></span>
   * <span data-ttu-id="e5243-281">Le service de métadonnées d’instance requiert que l’en-tête `Metadata: true` soit transmis dans cette demande.</span><span class="sxs-lookup"><span data-stu-id="e5243-281">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="e5243-282">La transmission de cet en-tête dans l’appel REST permet d’accéder au service de métadonnées d’instance.</span><span class="sxs-lookup"><span data-stu-id="e5243-282">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="e5243-283">Pourquoi je n’obtiens pas les informations de calcul pour ma machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="e5243-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="e5243-284">Actuellement, le service de métadonnées d’instance prend uniquement en charge les instances créées avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5243-284">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="e5243-285">À l’avenir, il se peut que nous ajoutions la prise en charge de machines virtuelles du service cloud.</span><span class="sxs-lookup"><span data-stu-id="e5243-285">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="e5243-286">J’ai créé une machine virtuelle via Azure Resource Manager il y quelque temps déjà.</span><span class="sxs-lookup"><span data-stu-id="e5243-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="e5243-287">Pourquoi ne puis-je pas voir les informations de métadonnées de calcul ?</span><span class="sxs-lookup"><span data-stu-id="e5243-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="e5243-288">Pour les machines virtuelles créées après septembre 2016, ajoutez une [balise](../azure-resource-manager/resource-group-using-tags.md) pour commencer à voir les métadonnées de calcul.</span><span class="sxs-lookup"><span data-stu-id="e5243-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="e5243-289">Pour une machine virtuelle plus ancienne (créée avant septembre 2016), ajoutez/supprimez des extensions ou des disques de données à la machine virtuelle pour actualiser les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="e5243-289">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="e5243-290">Pourquoi l’erreur `500 Internal Server Error` ?</span><span class="sxs-lookup"><span data-stu-id="e5243-290">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="e5243-291">Renouvelez votre demande en fonction du système d’interruption exponentiel.</span><span class="sxs-lookup"><span data-stu-id="e5243-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="e5243-292">Si le problème persiste, contactez le support Azure.</span><span class="sxs-lookup"><span data-stu-id="e5243-292">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="e5243-293">Où partager des commentaires/questions supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="e5243-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="e5243-294">Envoyez vos commentaires au site http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e5243-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="e5243-295">Cela fonctionne-t-il pour l’instance de groupe de machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="e5243-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="e5243-296">Oui, le service de métadonnées est disponible pour les instances de groupe identique.</span><span class="sxs-lookup"><span data-stu-id="e5243-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="e5243-297">Comment obtenir un support technique pour le service ?</span><span class="sxs-lookup"><span data-stu-id="e5243-297">How do I get support for the service?</span></span>
   * <span data-ttu-id="e5243-298">Pour obtenir un support technique pour le service, créez un problème de support dans le portail Azure pour la machine virtuelle sur laquelle vous ne pouvez pas obtenir de réponse de métadonnées après plusieurs tentatives longues.</span><span class="sxs-lookup"><span data-stu-id="e5243-298">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Support des métadonnées d’instance](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="e5243-300">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5243-300">Next Steps</span></span>

- <span data-ttu-id="e5243-301">En savoir plus sur l’API [scheduledevents](virtual-machines-scheduled-events.md) en **préversion publique** fournie par le service de métadonnées d’instance.</span><span class="sxs-lookup"><span data-stu-id="e5243-301">Learn more about the [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by the Instance Metadata Service.</span></span>
