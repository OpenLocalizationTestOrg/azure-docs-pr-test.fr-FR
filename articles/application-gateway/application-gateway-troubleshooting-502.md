---
title: erreurs de Azure Application passerelle passerelle incorrecte (502) aaaTroubleshoot | Documents Microsoft
description: "Découvrez comment les erreurs tootroubleshoot 502 de passerelle d’Application"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="21cea-103">Résolution des erreurs de passerelle incorrecte dans Application Gateway</span><span class="sxs-lookup"><span data-stu-id="21cea-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="21cea-104">Découvrez comment les erreurs (502) passerelle incorrecte de tootroubleshoot reçu lors de l’utilisation de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="21cea-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="21cea-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="21cea-105">Overview</span></span>

<span data-ttu-id="21cea-106">Après avoir configuré une passerelle d’application, une des erreurs hello que les utilisateurs peuvent rencontrer est « Erreur de serveur : 502 - serveur Web a reçu une réponse non valide en tant que passerelle ou proxy ».</span><span class="sxs-lookup"><span data-stu-id="21cea-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="21cea-107">Cette erreur peut se produire en raison de toohello suivant raisons principales :</span><span class="sxs-lookup"><span data-stu-id="21cea-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="21cea-108">Le [pool principal d’Azure Application Gateway n’est pas configuré ou est vide](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="21cea-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="21cea-109">Aucun des machines virtuelles de hello ou des instances dans [ensemble d’échelle de machine virtuelle sont intègres](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="21cea-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="21cea-110">Machines virtuelles ou des instances de l’ensemble d’échelle de machine virtuelle principale sont [sonde d’intégrité de par défaut ne répond pas toohello](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="21cea-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="21cea-111">[Configuration non valide ou incorrecte des sondes d’intégrité personnalisées](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="21cea-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="21cea-112">[Problèmes de connectivité ou d’expiration](#request-time-out) des requêtes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="21cea-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="21cea-113">Pool d’adresses principal vide</span><span class="sxs-lookup"><span data-stu-id="21cea-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="21cea-114">Cause :</span><span class="sxs-lookup"><span data-stu-id="21cea-114">Cause</span></span>

<span data-ttu-id="21cea-115">Si hello passerelle d’Application n’a pas de machines virtuelles ou ensemble d’échelle de machine virtuelle configurée dans un pool d’adresses de serveur principal hello, il ne peut pas acheminer une demande du client et lève une erreur de passerelle incorrecte.</span><span class="sxs-lookup"><span data-stu-id="21cea-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="21cea-116">Solution</span><span class="sxs-lookup"><span data-stu-id="21cea-116">Solution</span></span>

<span data-ttu-id="21cea-117">Assurez-vous que le pool d’adresses principal hello n’est pas vide.</span><span class="sxs-lookup"><span data-stu-id="21cea-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="21cea-118">Vous pouvez pour cela utiliser PowerShell, l’interface de ligne de commande ou le portail.</span><span class="sxs-lookup"><span data-stu-id="21cea-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="21cea-119">sortie de Hello de hello précédant l’applet de commande doit contenir un pool d’adresses de serveur principal non vide.</span><span class="sxs-lookup"><span data-stu-id="21cea-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="21cea-120">Dans l’exemple suivant, la commande retourne deux pools configurés avec un nom de domaine complet ou des adresses IP pour les machines virtuelles de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="21cea-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="21cea-121">Hello état de configuration de hello BackendAddressPool doit être 'Succeeded'.</span><span class="sxs-lookup"><span data-stu-id="21cea-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="21cea-122">BackendAddressPoolsText :</span><span class="sxs-lookup"><span data-stu-id="21cea-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="21cea-123">Instances non intègres dans BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="21cea-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="21cea-124">Cause :</span><span class="sxs-lookup"><span data-stu-id="21cea-124">Cause</span></span>

<span data-ttu-id="21cea-125">Si toutes les instances de hello de BackendAddressPool sont défectueux, passerelle d’Application n’ont pas de toute demande d’utilisateur principal tooroute à.</span><span class="sxs-lookup"><span data-stu-id="21cea-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="21cea-126">Cela peut également être le cas de hello lorsque les instances de serveur principal sont sains, mais n’ont pas d’application hello requis déployée.</span><span class="sxs-lookup"><span data-stu-id="21cea-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="21cea-127">Solution</span><span class="sxs-lookup"><span data-stu-id="21cea-127">Solution</span></span>

<span data-ttu-id="21cea-128">Assurez-vous que les instances de hello sont intègres, application hello est correctement configurée.</span><span class="sxs-lookup"><span data-stu-id="21cea-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="21cea-129">Vérifiez si les instances de serveur principal de hello sont toorespond en mesure de commande ping tooa à partir d’une autre machine virtuelle dans hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="21cea-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="21cea-130">Si configuré avec un point de terminaison public, assurez-vous que l’application web navigateur demande toohello est utilisable.</span><span class="sxs-lookup"><span data-stu-id="21cea-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="21cea-131">Problèmes avec la sonde d’intégrité par défaut</span><span class="sxs-lookup"><span data-stu-id="21cea-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="21cea-132">Cause :</span><span class="sxs-lookup"><span data-stu-id="21cea-132">Cause</span></span>

<span data-ttu-id="21cea-133">502 erreurs peuvent également être fréquentes indicateurs hello sonde d’intégrité par défaut est tooreach n’a pas pu machines virtuelles du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="21cea-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="21cea-134">Lorsqu’une instance de la passerelle d’Application est configurée, il configure automatiquement un tooeach de sonde d’intégrité par défaut BackendAddressPool à l’aide des propriétés de hello BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="21cea-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="21cea-135">Aucun utilisateur d’entrée est obligatoire tooset cette sonde.</span><span class="sxs-lookup"><span data-stu-id="21cea-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="21cea-136">Plus précisément, lorsqu’une règle d’équilibrage de charge est configurée, une association est établie entre BackendHttpSetting et BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="21cea-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="21cea-137">Une sonde est configurée pour chacune de ces associations lance la passerelle d’Application une instance de tooeach de connexion de contrôle d’intégrité réguliers dans hello BackendAddressPool port hello spécifié dans l’élément de BackendHttpSetting hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="21cea-138">Tableau suivant répertorie les valeurs hello associés de sonde de contrôle d’intégrité par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="21cea-139">Propriétés de la sonde</span><span class="sxs-lookup"><span data-stu-id="21cea-139">Probe property</span></span> | <span data-ttu-id="21cea-140">Valeur</span><span class="sxs-lookup"><span data-stu-id="21cea-140">Value</span></span> | <span data-ttu-id="21cea-141">Description</span><span class="sxs-lookup"><span data-stu-id="21cea-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21cea-142">URL de sonde</span><span class="sxs-lookup"><span data-stu-id="21cea-142">Probe URL</span></span> |<span data-ttu-id="21cea-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="21cea-143">http://127.0.0.1/</span></span> |<span data-ttu-id="21cea-144">Chemin d'accès de l'URL</span><span class="sxs-lookup"><span data-stu-id="21cea-144">URL path</span></span> |
| <span data-ttu-id="21cea-145">Intervalle</span><span class="sxs-lookup"><span data-stu-id="21cea-145">Interval</span></span> |<span data-ttu-id="21cea-146">30</span><span class="sxs-lookup"><span data-stu-id="21cea-146">30</span></span> |<span data-ttu-id="21cea-147">Intervalle d’analyse en secondes</span><span class="sxs-lookup"><span data-stu-id="21cea-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="21cea-148">Délai d’attente</span><span class="sxs-lookup"><span data-stu-id="21cea-148">Time-out</span></span> |<span data-ttu-id="21cea-149">30</span><span class="sxs-lookup"><span data-stu-id="21cea-149">30</span></span> |<span data-ttu-id="21cea-150">Délai d’expiration de l’analyse en secondes</span><span class="sxs-lookup"><span data-stu-id="21cea-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="21cea-151">Seuil de défaillance sur le plan de l’intégrité</span><span class="sxs-lookup"><span data-stu-id="21cea-151">Unhealthy threshold</span></span> |<span data-ttu-id="21cea-152">3</span><span class="sxs-lookup"><span data-stu-id="21cea-152">3</span></span> |<span data-ttu-id="21cea-153">Nombre de tentatives d’analyse</span><span class="sxs-lookup"><span data-stu-id="21cea-153">Probe retry count.</span></span> <span data-ttu-id="21cea-154">serveur principal de Hello est marquée vers le bas après que le nombre d’échecs de sonde consécutifs hello a atteint le seuil de défaillance hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="21cea-155">Solution</span><span class="sxs-lookup"><span data-stu-id="21cea-155">Solution</span></span>

* <span data-ttu-id="21cea-156">Assurez-vous qu’un site par défaut est configuré et qu’il écoute sur le port 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="21cea-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="21cea-157">Si BackendHttpSetting spécifie un port autre que 80, le site par défaut de hello doit être toolisten configuré sur ce port.</span><span class="sxs-lookup"><span data-stu-id="21cea-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="21cea-158">Hello appel toohttp://127.0.0.1:port doit retourner un code de résultat HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="21cea-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="21cea-159">Cela doit être retourné dans le délai d’attente de 30 secondes hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="21cea-160">Assurez-vous que le port configuré est ouvert et qu’il n’y a aucune règles de pare-feu ou les groupes de sécurité réseau Azure, qui bloquent le trafic entrant ou sortant sur le port hello configuré.</span><span class="sxs-lookup"><span data-stu-id="21cea-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="21cea-161">Si les machines virtuelles Azure classiques ou le Service Cloud est utilisé avec le nom de domaine complet ou l’adresse IP publique, vérifiez hello correspondantes [point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) est ouvert.</span><span class="sxs-lookup"><span data-stu-id="21cea-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="21cea-162">Si hello machine virtuelle est configurée via le Gestionnaire de ressources Azure et se trouve en dehors de hello réseau virtuel où la passerelle d’Application est déployée, [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) doit être configuré accès tooallow sur hello souhaité de port.</span><span class="sxs-lookup"><span data-stu-id="21cea-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="21cea-163">Problèmes avec la sonde d’intégrité personnalisée</span><span class="sxs-lookup"><span data-stu-id="21cea-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="21cea-164">Cause :</span><span class="sxs-lookup"><span data-stu-id="21cea-164">Cause</span></span>

<span data-ttu-id="21cea-165">Sondes d’intégrité personnalisés permettent de tester le comportement par défaut de toohello davantage de flexibilité.</span><span class="sxs-lookup"><span data-stu-id="21cea-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="21cea-166">Lorsque vous utilisez des sondes personnalisés, les utilisateurs peuvent configurer intervalle d’analyse hello, l’URL de hello et tootest de chemin d’accès et combien tooaccept d’échecs de réponse avant de marquer l’instance du pool de back-end hello comme étant défectueux.</span><span class="sxs-lookup"><span data-stu-id="21cea-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="21cea-167">Hello propriétés supplémentaires suivantes est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="21cea-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="21cea-168">Propriétés de la sonde</span><span class="sxs-lookup"><span data-stu-id="21cea-168">Probe property</span></span> | <span data-ttu-id="21cea-169">Description</span><span class="sxs-lookup"><span data-stu-id="21cea-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21cea-170">Nom</span><span class="sxs-lookup"><span data-stu-id="21cea-170">Name</span></span> |<span data-ttu-id="21cea-171">Nom de la sonde de hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-171">Name of hello probe.</span></span> <span data-ttu-id="21cea-172">Ce nom est sonde de toohello toorefer utilisés dans les paramètres HTTP du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="21cea-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="21cea-173">Protocole</span><span class="sxs-lookup"><span data-stu-id="21cea-173">Protocol</span></span> |<span data-ttu-id="21cea-174">Protocole utilisé sonde de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="21cea-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="21cea-175">Sonde de Hello utilise le protocole de hello définie dans les paramètres HTTP hello principal</span><span class="sxs-lookup"><span data-stu-id="21cea-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="21cea-176">Host</span><span class="sxs-lookup"><span data-stu-id="21cea-176">Host</span></span> |<span data-ttu-id="21cea-177">Hôte toosend hello de sonde à nom.</span><span class="sxs-lookup"><span data-stu-id="21cea-177">Host name toosend hello probe.</span></span> <span data-ttu-id="21cea-178">S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="21cea-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="21cea-179">Ce nom est différent du nom d’hôte de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="21cea-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="21cea-180">Chemin</span><span class="sxs-lookup"><span data-stu-id="21cea-180">Path</span></span> |<span data-ttu-id="21cea-181">Chemin d’accès relatif de sonde de hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-181">Relative path of hello probe.</span></span> <span data-ttu-id="21cea-182">chemin d’accès valide de Hello commence à partir de '/'.</span><span class="sxs-lookup"><span data-stu-id="21cea-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="21cea-183">Sonde de Hello est envoyé trop\<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\></span><span class="sxs-lookup"><span data-stu-id="21cea-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="21cea-184">Intervalle</span><span class="sxs-lookup"><span data-stu-id="21cea-184">Interval</span></span> |<span data-ttu-id="21cea-185">Intervalle d’analyse en secondes.</span><span class="sxs-lookup"><span data-stu-id="21cea-185">Probe interval in seconds.</span></span> <span data-ttu-id="21cea-186">Il s’agit d’intervalle de temps hello entre deux analyses consécutives.</span><span class="sxs-lookup"><span data-stu-id="21cea-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="21cea-187">Délai d’attente</span><span class="sxs-lookup"><span data-stu-id="21cea-187">Time-out</span></span> |<span data-ttu-id="21cea-188">Délai d’expiration de l’analyse en secondes.</span><span class="sxs-lookup"><span data-stu-id="21cea-188">Probe time-out in seconds.</span></span> <span data-ttu-id="21cea-189">Si une réponse valide n’est pas reçue dans ce délai, la sonde de hello est marquée comme ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="21cea-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="21cea-190">Seuil de défaillance sur le plan de l’intégrité</span><span class="sxs-lookup"><span data-stu-id="21cea-190">Unhealthy threshold</span></span> |<span data-ttu-id="21cea-191">Nombre de tentatives d’analyse</span><span class="sxs-lookup"><span data-stu-id="21cea-191">Probe retry count.</span></span> <span data-ttu-id="21cea-192">serveur principal de Hello est marquée vers le bas après que le nombre d’échecs de sonde consécutifs hello a atteint le seuil de défaillance hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="21cea-193">Solution</span><span class="sxs-lookup"><span data-stu-id="21cea-193">Solution</span></span>

<span data-ttu-id="21cea-194">Valider ce hello que sonde d’intégrité personnalisé est correctement configuré en tant que hello tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="21cea-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="21cea-195">En outre toohello précédente étapes de dépannage Vérifiez également les hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="21cea-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="21cea-196">Vérifiez cette sonde hello est spécifié correctement conformément à hello [guide](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="21cea-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="21cea-197">Si la passerelle d’Application est configurée pour un site unique, par hello de valeur par défaut hôte nom doit être spécifié sous la forme '127.0.0.1', à moins que sinon configurés dans une sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="21cea-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="21cea-198">Vérifiez qu’un appel toohttp : / /\<hôte\>:\<port\>\<chemin d’accès\> retourne un code de résultat HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="21cea-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="21cea-199">Assurez-vous que l’intervalle, délai d’expiration et UnhealtyThreshold sont dans une plage acceptable hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="21cea-200">Si à l’aide de HTTPS sonde, assurez-vous que ce serveur principal de hello ne nécessite pas SNI en configurant un certificat de secours sur le serveur principal de hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="21cea-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="21cea-201">Assurez-vous que l’intervalle de délai d’attente et UnhealtyThreshold sont dans une plage acceptable hello.</span><span class="sxs-lookup"><span data-stu-id="21cea-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="21cea-202">Délai d’expiration de la demande</span><span class="sxs-lookup"><span data-stu-id="21cea-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="21cea-203">Cause :</span><span class="sxs-lookup"><span data-stu-id="21cea-203">Cause</span></span>

<span data-ttu-id="21cea-204">Lors de la réception d’une demande de l’utilisateur, passerelle d’Application s’applique hello configuré règles toohello demande et l’achemine instance du pool de back-end tooa.</span><span class="sxs-lookup"><span data-stu-id="21cea-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="21cea-205">Il attend un intervalle de temps de réponse à partir de l’instance de serveur principal hello configurable.</span><span class="sxs-lookup"><span data-stu-id="21cea-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="21cea-206">Par défaut, cet intervalle est de **30 secondes**.</span><span class="sxs-lookup"><span data-stu-id="21cea-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="21cea-207">Si Application Gateway ne reçoit pas de réponse de l’application principale dans cet intervalle, la demande de l’utilisateur renverra une erreur 502.</span><span class="sxs-lookup"><span data-stu-id="21cea-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="21cea-208">Solution</span><span class="sxs-lookup"><span data-stu-id="21cea-208">Solution</span></span>

<span data-ttu-id="21cea-209">Passerelle d’application permet aux utilisateurs tooconfigure ce paramètre via BackendHttpSetting, ce qui peut être ensuite appliqués toodifferent pools.</span><span class="sxs-lookup"><span data-stu-id="21cea-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="21cea-210">Les pools de serveurs principaux peuvent avoir des paramètres BackendHttpSetting différents et, par conséquent, des délais d’attente différents.</span><span class="sxs-lookup"><span data-stu-id="21cea-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="21cea-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21cea-211">Next steps</span></span>

<span data-ttu-id="21cea-212">Si hello étapes précédentes ne résolvent pas hello problème, ouvrez un [ticket de support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="21cea-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

