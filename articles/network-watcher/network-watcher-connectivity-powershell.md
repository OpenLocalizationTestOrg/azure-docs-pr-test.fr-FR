---
title: "Vérifier la connectivité avec Azure Network Watcher - PowerShell | Microsoft Docs"
description: "Cette page explique comment tester la connectivité avec Network Watcher à l’aide de PowerShell"
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
ms.openlocfilehash: a8f936cd23838759dc30b04688d3c6544e4895cc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="3963c-103">Vérifier la connectivité avec Azure Network Watcher à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3963c-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3963c-104">Portail</span><span class="sxs-lookup"><span data-stu-id="3963c-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="3963c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3963c-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="3963c-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3963c-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="3963c-107">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="3963c-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="3963c-108">Découvrez comment utiliser la connectivité pour vérifier si une connexion TCP directe entre une machine virtuelle et un point de terminaison donné peut être établie.</span><span class="sxs-lookup"><span data-stu-id="3963c-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3963c-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3963c-109">Before you begin</span></span>

<span data-ttu-id="3963c-110">Cet article part du principe que vous disposez des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="3963c-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="3963c-111">Une instance de Network Watcher dans la région où vous souhaitez vérifier la connectivité.</span><span class="sxs-lookup"><span data-stu-id="3963c-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="3963c-112">Des machines virtuelles avec lesquelles vérifier la connectivité.</span><span class="sxs-lookup"><span data-stu-id="3963c-112">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="3963c-113">La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="3963c-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="3963c-114">Pour installer l’extension sur une machine virtuelle Windows, consultez la page [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Windows). Pour une machine virtuelle Linux, consultez la page [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Linux).</span><span class="sxs-lookup"><span data-stu-id="3963c-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="3963c-115">Inscrire la fonction de version préliminaire</span><span class="sxs-lookup"><span data-stu-id="3963c-115">Register the preview capability</span></span>

<span data-ttu-id="3963c-116">La connectivité est actuellement en préversion publique. Pour l’utiliser, cette fonctionnalité doit être inscrite.</span><span class="sxs-lookup"><span data-stu-id="3963c-116">Connectivity is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="3963c-117">Pour ce faire, exécutez l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="3963c-117">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="3963c-118">Pour vérifier que l’inscription s’est bien déroulée, exécutez l’exemple Powershell suivant :</span><span class="sxs-lookup"><span data-stu-id="3963c-118">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="3963c-119">Si la fonctionnalité a été correctement inscrite, vous devez obtenir la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="3963c-119">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="3963c-120">Vérifier la connectivité à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3963c-120">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="3963c-121">Cet exemple vérifie la connectivité à une machine virtuelle de destination sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="3963c-121">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="3963c-122">Exemple</span><span class="sxs-lookup"><span data-stu-id="3963c-122">Example</span></span>

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

### <a name="response"></a><span data-ttu-id="3963c-123">Réponse</span><span class="sxs-lookup"><span data-stu-id="3963c-123">Response</span></span>

<span data-ttu-id="3963c-124">La réponse suivante est tirée de l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="3963c-124">The following response is from the previous example.</span></span>  <span data-ttu-id="3963c-125">Dans cette réponse, `ConnectionStatus` est **Inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="3963c-125">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="3963c-126">Vous pouvez constater que toutes les sondes envoyées ont échoué.</span><span class="sxs-lookup"><span data-stu-id="3963c-126">You can see that all the probes sent failed.</span></span> <span data-ttu-id="3963c-127">La connectivité a échoué au niveau de l’appliance virtuelle en raison de `NetworkSecurityRule`, configuré par l’utilisateur et nommé **UserRule_Port80**, destiné à bloquer le trafic entrant sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="3963c-127">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="3963c-128">Ces informations peuvent être utilisées pour mener des recherches sur les problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="3963c-128">This information can be used to research connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="3963c-129">Valider les problèmes de routage</span><span class="sxs-lookup"><span data-stu-id="3963c-129">Validate routing issues</span></span>

<span data-ttu-id="3963c-130">Cet exemple vérifie la connectivité entre une machine virtuelle et un point de terminaison distant.</span><span class="sxs-lookup"><span data-stu-id="3963c-130">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="3963c-131">Exemple</span><span class="sxs-lookup"><span data-stu-id="3963c-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="3963c-132">Réponse</span><span class="sxs-lookup"><span data-stu-id="3963c-132">Response</span></span>

<span data-ttu-id="3963c-133">Dans l’exemple suivant, `ConnectionStatus` est **Inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="3963c-133">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="3963c-134">Dans les informations relatives à `Hops`, vous pouvez constater sous `Issues` que le trafic a été bloqué par `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="3963c-134">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span> 

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

## <a name="check-website-latency"></a><span data-ttu-id="3963c-135">Vérifier la latence du site Web</span><span class="sxs-lookup"><span data-stu-id="3963c-135">Check website latency</span></span>

<span data-ttu-id="3963c-136">L’exemple suivant vérifie la connectivité à un site Web.</span><span class="sxs-lookup"><span data-stu-id="3963c-136">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="3963c-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="3963c-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="3963c-138">Réponse</span><span class="sxs-lookup"><span data-stu-id="3963c-138">Response</span></span>

<span data-ttu-id="3963c-139">Dans la réponse suivante, vous pouvez constater que `ConnectionStatus` apparaît **Joignable**.</span><span class="sxs-lookup"><span data-stu-id="3963c-139">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="3963c-140">Lorsqu’une connexion est établie, les valeurs de latence sont fournies.</span><span class="sxs-lookup"><span data-stu-id="3963c-140">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="3963c-141">Vérifier la connectivité à un point de terminaison de stockage</span><span class="sxs-lookup"><span data-stu-id="3963c-141">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="3963c-142">L’exemple suivant teste la connectivité entre une machine virtuelle et un compte de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="3963c-142">The following example tests the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="3963c-143">Exemple</span><span class="sxs-lookup"><span data-stu-id="3963c-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="3963c-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="3963c-144">Response</span></span>

<span data-ttu-id="3963c-145">Le code json suivant est un exemple de réponse tiré de l’exécution de la cmdlet précédente.</span><span class="sxs-lookup"><span data-stu-id="3963c-145">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="3963c-146">Comme la destination est joignable, la propriété `ConnectionStatus` apparaît **Joignable**.</span><span class="sxs-lookup"><span data-stu-id="3963c-146">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="3963c-147">Les détails concernant le nombre de tronçons nécessaires pour accéder à l’objet blob de stockage et la latence vous sont fournis.</span><span class="sxs-lookup"><span data-stu-id="3963c-147">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3963c-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3963c-148">Next steps</span></span>

<span data-ttu-id="3963c-149">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3963c-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="3963c-150">Si le trafic est bloqué alors qu’il ne devrait pas l’être, consultez [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin de surveiller le groupe de sécurité réseau et les règles de sécurité définis.</span><span class="sxs-lookup"><span data-stu-id="3963c-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<!-- Image references -->














