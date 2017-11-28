---
title: "Résolution des erreurs de passerelle incorrecte dans Azure Application Gateway (502) | Microsoft Docs"
description: "Découvrez comment résoudre les erreurs 502 dans Application Gateway"
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="08723-103">Résolution des erreurs de passerelle incorrecte dans Application Gateway</span><span class="sxs-lookup"><span data-stu-id="08723-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="08723-104">Découvrez comment résoudre les erreurs de passerelle incorrecte (502) reçues lors de l’utilisation d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="08723-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="08723-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="08723-105">Overview</span></span>

<span data-ttu-id="08723-106">Après avoir configuré une passerelle Application Gateway, les utilisateurs peuvent rencontrer l’erreur « Erreur serveur 502 : le serveur Web a reçu une réponse erronée lors de son utilisation en tant que passerelle ou serveur proxy ».</span><span class="sxs-lookup"><span data-stu-id="08723-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="08723-107">Cette erreur peut se produire pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="08723-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="08723-108">Le [pool principal d’Azure Application Gateway n’est pas configuré ou est vide](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="08723-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="08723-109">Aucune des machines virtuelles ou des instances du [groupe de machines virtuelles identiques](#unhealthy-instances-in-backendaddresspool) n’est intègre.</span><span class="sxs-lookup"><span data-stu-id="08723-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="08723-110">Les machines virtuelles principales ou les instances du groupe de machines virtuelles identiques [ne répondent pas à la sonde d’intégrité par défaut](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="08723-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="08723-111">[Configuration non valide ou incorrecte des sondes d’intégrité personnalisées](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="08723-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="08723-112">[Problèmes de connectivité ou d’expiration](#request-time-out) des requêtes d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08723-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="08723-113">Pool d’adresses principal vide</span><span class="sxs-lookup"><span data-stu-id="08723-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="08723-114">Cause :</span><span class="sxs-lookup"><span data-stu-id="08723-114">Cause</span></span>

<span data-ttu-id="08723-115">Si Application Gateway ne dispose d’aucune machine virtuelle ou de jeu de mise à l’échelle de machine virtuelle configuré(e) dans le pool d’adresses principal, il ne peut pas acheminer les demandes client et renvoie alors une erreur de passerelle incorrecte.</span><span class="sxs-lookup"><span data-stu-id="08723-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="08723-116">Solution</span><span class="sxs-lookup"><span data-stu-id="08723-116">Solution</span></span>

<span data-ttu-id="08723-117">Assurez-vous que le pool d’adresses principal n’est pas vide.</span><span class="sxs-lookup"><span data-stu-id="08723-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="08723-118">Vous pouvez pour cela utiliser PowerShell, l’interface de ligne de commande ou le portail.</span><span class="sxs-lookup"><span data-stu-id="08723-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="08723-119">L’applet de commande ci-dessus doit renvoyer un pool d’adresses principal non vide.</span><span class="sxs-lookup"><span data-stu-id="08723-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="08723-120">Dans l’exemple suivant, la commande retourne deux pools configurés avec un nom de domaine complet ou des adresses IP pour les machines virtuelles de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="08723-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="08723-121">L’approvisionnement de BackendAddressPool doit se trouver à l’état « Succeeded » (Réussi).</span><span class="sxs-lookup"><span data-stu-id="08723-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="08723-122">BackendAddressPoolsText :</span><span class="sxs-lookup"><span data-stu-id="08723-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="08723-123">Instances non intègres dans BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="08723-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="08723-124">Cause :</span><span class="sxs-lookup"><span data-stu-id="08723-124">Cause</span></span>

<span data-ttu-id="08723-125">Si aucune des instances de BackendAddressPool n’est intègre, Application Gateway ne disposera d’aucun serveur principal vers lequel acheminer la demande utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08723-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="08723-126">Cette situation peut se produire lorsque les instances de serveur principal sont intègres, mais que l’application requise n’est pas déployée.</span><span class="sxs-lookup"><span data-stu-id="08723-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="08723-127">Solution</span><span class="sxs-lookup"><span data-stu-id="08723-127">Solution</span></span>

<span data-ttu-id="08723-128">Assurez-vous que les instances sont intègres et que l’application est correctement configurée.</span><span class="sxs-lookup"><span data-stu-id="08723-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="08723-129">Vérifiez si les instances de serveur principal sont en mesure de répondre à une commande ping générée par une autre machine virtuelle résidant dans le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="08723-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="08723-130">Si vous utilisez un point de terminaison public, assurez-vous qu’une demande de navigateur à l’application web est accessible.</span><span class="sxs-lookup"><span data-stu-id="08723-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="08723-131">Problèmes avec la sonde d’intégrité par défaut</span><span class="sxs-lookup"><span data-stu-id="08723-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="08723-132">Cause :</span><span class="sxs-lookup"><span data-stu-id="08723-132">Cause</span></span>

<span data-ttu-id="08723-133">Les erreurs 502 peuvent également indiquer que la sonde d’intégrité par défaut n’est pas en mesure d’atteindre les machines virtuelles du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="08723-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="08723-134">Lorsqu’une instance Application Gateway est approvisionnée, elle configure automatiquement une sonde d’intégrité par défaut pour chaque BackendAddressPool à l’aide des propriétés de BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="08723-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="08723-135">La configuration de cette sonde d’intégrité ne nécessite aucune action de la part de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08723-135">No user input is required to set this probe.</span></span> <span data-ttu-id="08723-136">Plus précisément, lorsqu’une règle d’équilibrage de charge est configurée, une association est établie entre BackendHttpSetting et BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="08723-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="08723-137">Un contrôle par défaut est configuré pour chacune de ces associations et Application Gateway initie régulièrement une connexion de contrôle d’intégrité à chaque instance dans le BackendAddressPool au niveau du port spécifié dans l’élément BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="08723-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="08723-138">Le tableau suivant répertorie les valeurs associées à la sonde d’intégrité par défaut.</span><span class="sxs-lookup"><span data-stu-id="08723-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="08723-139">Propriétés de la sonde</span><span class="sxs-lookup"><span data-stu-id="08723-139">Probe property</span></span> | <span data-ttu-id="08723-140">Valeur</span><span class="sxs-lookup"><span data-stu-id="08723-140">Value</span></span> | <span data-ttu-id="08723-141">Description</span><span class="sxs-lookup"><span data-stu-id="08723-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08723-142">URL de sonde</span><span class="sxs-lookup"><span data-stu-id="08723-142">Probe URL</span></span> |<span data-ttu-id="08723-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="08723-143">http://127.0.0.1/</span></span> |<span data-ttu-id="08723-144">Chemin d'accès de l'URL</span><span class="sxs-lookup"><span data-stu-id="08723-144">URL path</span></span> |
| <span data-ttu-id="08723-145">Intervalle</span><span class="sxs-lookup"><span data-stu-id="08723-145">Interval</span></span> |<span data-ttu-id="08723-146">30</span><span class="sxs-lookup"><span data-stu-id="08723-146">30</span></span> |<span data-ttu-id="08723-147">Intervalle d’analyse en secondes</span><span class="sxs-lookup"><span data-stu-id="08723-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="08723-148">Délai d’attente</span><span class="sxs-lookup"><span data-stu-id="08723-148">Time-out</span></span> |<span data-ttu-id="08723-149">30</span><span class="sxs-lookup"><span data-stu-id="08723-149">30</span></span> |<span data-ttu-id="08723-150">Délai d’expiration de l’analyse en secondes</span><span class="sxs-lookup"><span data-stu-id="08723-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="08723-151">Seuil de défaillance sur le plan de l’intégrité</span><span class="sxs-lookup"><span data-stu-id="08723-151">Unhealthy threshold</span></span> |<span data-ttu-id="08723-152">3</span><span class="sxs-lookup"><span data-stu-id="08723-152">3</span></span> |<span data-ttu-id="08723-153">Nombre de tentatives d’analyse</span><span class="sxs-lookup"><span data-stu-id="08723-153">Probe retry count.</span></span> <span data-ttu-id="08723-154">Le serveur principal est marqué comme étant défectueux après que le nombre d’échecs consécutifs a atteint le seuil de défaillance.</span><span class="sxs-lookup"><span data-stu-id="08723-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="08723-155">Solution</span><span class="sxs-lookup"><span data-stu-id="08723-155">Solution</span></span>

* <span data-ttu-id="08723-156">Assurez-vous qu’un site par défaut est configuré et qu’il écoute sur le port 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="08723-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="08723-157">Si BackendHttpSetting spécifie un port autre que 80, le site par défaut doit être configuré pour écouter sur ce port.</span><span class="sxs-lookup"><span data-stu-id="08723-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="08723-158">L’appel à http://127.0.0.1:port doit renvoyer un code de résultat HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="08723-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="08723-159">Ce code doit être retourné dans un délai de 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="08723-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="08723-160">Vérifiez que le port configuré est ouvert et qu’aucune règle de pare-feu ou aucun groupe de sécurité réseau Azure ne bloque le trafic entrant ou sortant sur le port configuré.</span><span class="sxs-lookup"><span data-stu-id="08723-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="08723-161">Si vous utilisez des machines virtuelles Azure classiques ou un service cloud avec un nom de domaine complet ou une adresse IP publique, assurez-vous que le [point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) correspondant est ouvert.</span><span class="sxs-lookup"><span data-stu-id="08723-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="08723-162">Si la machine virtuelle est configuré via Azure Resource Manager et se trouve en dehors du réseau virtuel où est déployé Application Gateway, le [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) doit être configuré pour autoriser l’accès sur le port souhaité.</span><span class="sxs-lookup"><span data-stu-id="08723-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="08723-163">Problèmes avec la sonde d’intégrité personnalisée</span><span class="sxs-lookup"><span data-stu-id="08723-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="08723-164">Cause :</span><span class="sxs-lookup"><span data-stu-id="08723-164">Cause</span></span>

<span data-ttu-id="08723-165">Les sondes d’intégrité personnalisées apportent davantage de flexibilité au comportement de contrôle par défaut.</span><span class="sxs-lookup"><span data-stu-id="08723-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="08723-166">En utilisant des sondes personnalisées, les utilisateurs peuvent configurer l’intervalle d’analyse, l’URL et le chemin à tester ainsi que le nombre de réponses en échec autorisé avant que l’instance de pool principal soit marquée comme étant défectueuse.</span><span class="sxs-lookup"><span data-stu-id="08723-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="08723-167">Les propriétés supplémentaires suivantes sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="08723-167">The following additional properties are added.</span></span>

| <span data-ttu-id="08723-168">Propriétés de la sonde</span><span class="sxs-lookup"><span data-stu-id="08723-168">Probe property</span></span> | <span data-ttu-id="08723-169">Description</span><span class="sxs-lookup"><span data-stu-id="08723-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="08723-170">Name</span><span class="sxs-lookup"><span data-stu-id="08723-170">Name</span></span> |<span data-ttu-id="08723-171">Nom de la sonde.</span><span class="sxs-lookup"><span data-stu-id="08723-171">Name of the probe.</span></span> <span data-ttu-id="08723-172">Ce nom est utilisé pour désigner la sonde dans les paramètres HTTP du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="08723-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="08723-173">Protocole</span><span class="sxs-lookup"><span data-stu-id="08723-173">Protocol</span></span> |<span data-ttu-id="08723-174">Protocole utilisé pour envoyer la sonde.</span><span class="sxs-lookup"><span data-stu-id="08723-174">Protocol used to send the probe.</span></span> <span data-ttu-id="08723-175">La sonde utilise le protocole défini dans les paramètres HTTP du serveur principal</span><span class="sxs-lookup"><span data-stu-id="08723-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="08723-176">Host</span><span class="sxs-lookup"><span data-stu-id="08723-176">Host</span></span> |<span data-ttu-id="08723-177">Nom d’hôte pour l’envoi de la sonde.</span><span class="sxs-lookup"><span data-stu-id="08723-177">Host name to send the probe.</span></span> <span data-ttu-id="08723-178">S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="08723-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="08723-179">Ce nom est différent du nom d’hôte de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08723-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="08723-180">Chemin</span><span class="sxs-lookup"><span data-stu-id="08723-180">Path</span></span> |<span data-ttu-id="08723-181">Chemin relatif de la sonde.</span><span class="sxs-lookup"><span data-stu-id="08723-181">Relative path of the probe.</span></span> <span data-ttu-id="08723-182">Le chemin valide commence par « / ».</span><span class="sxs-lookup"><span data-stu-id="08723-182">The valid path starts from '/'.</span></span> <span data-ttu-id="08723-183">La sonde est envoyée à \<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\></span><span class="sxs-lookup"><span data-stu-id="08723-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="08723-184">Intervalle</span><span class="sxs-lookup"><span data-stu-id="08723-184">Interval</span></span> |<span data-ttu-id="08723-185">Intervalle d’analyse en secondes.</span><span class="sxs-lookup"><span data-stu-id="08723-185">Probe interval in seconds.</span></span> <span data-ttu-id="08723-186">Il s’agit de l’intervalle de temps qui s’écoule entre deux analyses consécutives.</span><span class="sxs-lookup"><span data-stu-id="08723-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="08723-187">Délai d’attente</span><span class="sxs-lookup"><span data-stu-id="08723-187">Time-out</span></span> |<span data-ttu-id="08723-188">Délai d’expiration de l’analyse en secondes.</span><span class="sxs-lookup"><span data-stu-id="08723-188">Probe time-out in seconds.</span></span> <span data-ttu-id="08723-189">Si aucune réponse valide n’est reçue dans le délai imparti, la sonde est marquée comme étant en échec.</span><span class="sxs-lookup"><span data-stu-id="08723-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="08723-190">Seuil de défaillance sur le plan de l’intégrité</span><span class="sxs-lookup"><span data-stu-id="08723-190">Unhealthy threshold</span></span> |<span data-ttu-id="08723-191">Nombre de tentatives d’analyse</span><span class="sxs-lookup"><span data-stu-id="08723-191">Probe retry count.</span></span> <span data-ttu-id="08723-192">Le serveur principal est marqué comme étant défectueux après que le nombre d’échecs consécutifs a atteint le seuil de défaillance.</span><span class="sxs-lookup"><span data-stu-id="08723-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="08723-193">Solution</span><span class="sxs-lookup"><span data-stu-id="08723-193">Solution</span></span>

<span data-ttu-id="08723-194">Vérifiez que la sonde d’intégrité personnalisée est correctement configurée (voir la table précédente).</span><span class="sxs-lookup"><span data-stu-id="08723-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="08723-195">Outre les étapes de dépannage précédentes, vérifiez également les points suivants :</span><span class="sxs-lookup"><span data-stu-id="08723-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="08723-196">Assurez-vous que la sonde est correctement spécifiée suivant les indications du [guide](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="08723-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="08723-197">Si Application Gateway est configuré pour un seul site, le nom d’hôte par défaut doit être spécifié sous la forme « 127.0.0.1 », sauf s’il est configuré d’une autre manière dans la sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="08723-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="08723-198">Assurez-vous qu’un appel à http://\<hôte\>:\<port\>\<chemin d’accès\> retourne un code de résultat HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="08723-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="08723-199">Assurez-vous que les paramètres Interval, Time-out et UnhealtyThreshold se trouvent dans la plage acceptable.</span><span class="sxs-lookup"><span data-stu-id="08723-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="08723-200">Si vous utilisez une sonde HTTPS, vérifiez que le serveur back-end ne nécessite pas SNI en configurant un certificat de secours sur le serveur back-end lui-même.</span><span class="sxs-lookup"><span data-stu-id="08723-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="08723-201">Assurez-vous que les paramètres Interval, Time-out et UnhealtyThreshold se trouvent dans la plage acceptable.</span><span class="sxs-lookup"><span data-stu-id="08723-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="08723-202">Délai d’expiration de la demande</span><span class="sxs-lookup"><span data-stu-id="08723-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="08723-203">Cause :</span><span class="sxs-lookup"><span data-stu-id="08723-203">Cause</span></span>

<span data-ttu-id="08723-204">À réception d’une demande de l’utilisateur, Application Gateway applique les règles configurées à la demande et achemine cette demande à une instance de pool principal.</span><span class="sxs-lookup"><span data-stu-id="08723-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="08723-205">Application Gateway observe un temps d’attente (configurable) pour recevoir une réponse de l’instance de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="08723-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="08723-206">Par défaut, cet intervalle est de **30 secondes**.</span><span class="sxs-lookup"><span data-stu-id="08723-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="08723-207">Si Application Gateway ne reçoit pas de réponse de l’application principale dans cet intervalle, la demande de l’utilisateur renverra une erreur 502.</span><span class="sxs-lookup"><span data-stu-id="08723-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="08723-208">Solution</span><span class="sxs-lookup"><span data-stu-id="08723-208">Solution</span></span>

<span data-ttu-id="08723-209">Application Gateway permet aux utilisateurs de configurer ce paramètre via BackendHttpSetting pour l’appliquer ensuite à différents pools.</span><span class="sxs-lookup"><span data-stu-id="08723-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="08723-210">Les pools de serveurs principaux peuvent avoir des paramètres BackendHttpSetting différents et, par conséquent, des délais d’attente différents.</span><span class="sxs-lookup"><span data-stu-id="08723-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="08723-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08723-211">Next steps</span></span>

<span data-ttu-id="08723-212">Si les étapes précédentes ne vous permettent pas de résoudre le problème, ouvrez un [ticket d’incident](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="08723-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

