---
title: "connectivité aaaCheck avec l’Observateur réseau de Azure - PowerShell | Documents Microsoft"
description: "Cette page explique comment tootest une connectivité avec l’Observateur réseau à l’aide de PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="01c6f-103">Vérifier la connectivité avec Azure Network Watcher à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="01c6f-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="01c6f-104">Portail</span><span class="sxs-lookup"><span data-stu-id="01c6f-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="01c6f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01c6f-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="01c6f-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="01c6f-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="01c6f-107">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="01c6f-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="01c6f-108">Découvrez comment toouse connectivité tooverify si une connexion TCP directe à partir d’un tooa de machine virtuelle donné du point de terminaison peut être établie.</span><span class="sxs-lookup"><span data-stu-id="01c6f-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="01c6f-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="01c6f-109">Before you begin</span></span>

<span data-ttu-id="01c6f-110">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="01c6f-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="01c6f-111">Une instance de l’Observateur réseau dans la région de hello souhaité toocheck connectivité.</span><span class="sxs-lookup"><span data-stu-id="01c6f-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="01c6f-112">Machines virtuelles toocheck la connectivité avec.</span><span class="sxs-lookup"><span data-stu-id="01c6f-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="01c6f-113">La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="01c6f-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="01c6f-114">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="01c6f-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="01c6f-115">Inscrire la fonction d’aperçu hello</span><span class="sxs-lookup"><span data-stu-id="01c6f-115">Register hello preview capability</span></span>

<span data-ttu-id="01c6f-116">Connectivité est actuellement en version préliminaire publique, toouse cette fonctionnalité, qu'il doit toobe inscrit.</span><span class="sxs-lookup"><span data-stu-id="01c6f-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="01c6f-117">toodo, exécution hello suivant l’exemple PowerShell :</span><span class="sxs-lookup"><span data-stu-id="01c6f-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="01c6f-118">l’inscription de hello tooverify a réussi, exécutez hello suivant l’exemple Powershell :</span><span class="sxs-lookup"><span data-stu-id="01c6f-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="01c6f-119">Si la fonctionnalité de hello a été inscrit correctement, sortie de hello doit correspondre au suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="01c6f-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="01c6f-120">Vérifiez la connectivité tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="01c6f-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="01c6f-121">Cet exemple vérifie l’ordinateur virtuel de destination de tooa connectivité via le port 80.</span><span class="sxs-lookup"><span data-stu-id="01c6f-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="01c6f-122">Exemple</span><span class="sxs-lookup"><span data-stu-id="01c6f-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="01c6f-123">Réponse</span><span class="sxs-lookup"><span data-stu-id="01c6f-123">Response</span></span>

<span data-ttu-id="01c6f-124">Hello suivant la réponse est à partir de l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="01c6f-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="01c6f-125">Dans cette réponse, hello `ConnectionStatus` est **inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="01c6f-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="01c6f-126">Vous pouvez voir que tous les hello sondes envoyées ayant échouées.</span><span class="sxs-lookup"><span data-stu-id="01c6f-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="01c6f-127">Échec de la connectivité de Hello au niveau de l’appliance virtuelle hello tooa échéance configurée par l’utilisateur `NetworkSecurityRule` nommé **UserRule_Port80**, configuré tooblock du trafic entrant sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="01c6f-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="01c6f-128">Ces informations peuvent être utilisées tooresearch les problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="01c6f-128">This information can be used tooresearch connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="01c6f-129">Valider les problèmes de routage</span><span class="sxs-lookup"><span data-stu-id="01c6f-129">Validate routing issues</span></span>

<span data-ttu-id="01c6f-130">exemple de Hello vérifie la connectivité entre un ordinateur virtuel et un point de terminaison distant.</span><span class="sxs-lookup"><span data-stu-id="01c6f-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="01c6f-131">Exemple</span><span class="sxs-lookup"><span data-stu-id="01c6f-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="01c6f-132">Réponse</span><span class="sxs-lookup"><span data-stu-id="01c6f-132">Response</span></span>

<span data-ttu-id="01c6f-133">Dans l’exemple suivant de hello, hello `ConnectionStatus` est affiché comme **inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="01c6f-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="01c6f-134">Bonjour `Hops` plus d’informations, vous pouvez voir sous `Issues` que le trafic de hello a été bloqué échéance tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="01c6f-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="01c6f-135">Vérifier la latence du site Web</span><span class="sxs-lookup"><span data-stu-id="01c6f-135">Check website latency</span></span>

<span data-ttu-id="01c6f-136">Hello exemple suivant vérifie le site Web du tooa hello connectivité.</span><span class="sxs-lookup"><span data-stu-id="01c6f-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="01c6f-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="01c6f-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="01c6f-138">Réponse</span><span class="sxs-lookup"><span data-stu-id="01c6f-138">Response</span></span>

<span data-ttu-id="01c6f-139">Bonjour suivant la réponse, vous pouvez voir hello `ConnectionStatus` affiche sous la forme **joignable**.</span><span class="sxs-lookup"><span data-stu-id="01c6f-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="01c6f-140">Lorsqu’une connexion est établie, les valeurs de latence sont fournies.</span><span class="sxs-lookup"><span data-stu-id="01c6f-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="01c6f-141">Vérifiez le point de terminaison de stockage de connectivité tooa</span><span class="sxs-lookup"><span data-stu-id="01c6f-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="01c6f-142">Bonjour à l’exemple suivant teste la connectivité de hello à partir d’un compte de stockage de blog de l’ordinateur virtuel tooa.</span><span class="sxs-lookup"><span data-stu-id="01c6f-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="01c6f-143">Exemple</span><span class="sxs-lookup"><span data-stu-id="01c6f-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="01c6f-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="01c6f-144">Response</span></span>

<span data-ttu-id="01c6f-145">Hello json suivant est hello exemple de réponse à partir de l’applet de commande précédente hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="01c6f-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="01c6f-146">Comme destination de hello est accessible, hello `ConnectionStatus` propriété s’affiche en tant que **joignable**.</span><span class="sxs-lookup"><span data-stu-id="01c6f-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="01c6f-147">Vous trouverez détails hello concernant le nombre de hello de blob de stockage hello sauts tooreach requis et la latence.</span><span class="sxs-lookup"><span data-stu-id="01c6f-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="01c6f-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01c6f-148">Next steps</span></span>

<span data-ttu-id="01c6f-149">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="01c6f-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="01c6f-150">Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont définis.</span><span class="sxs-lookup"><span data-stu-id="01c6f-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














