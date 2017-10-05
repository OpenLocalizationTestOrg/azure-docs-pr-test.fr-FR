---
title: "Gérer les captures de paquets avec Azure Network Watcher - PowerShell | Microsoft Docs"
description: "Cette page explique comment gérer la fonctionnalité de capture de paquets de Network Watcher à l’aide de PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="cc827-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc827-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="cc827-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="cc827-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="cc827-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc827-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="cc827-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cc827-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="cc827-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cc827-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="cc827-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="cc827-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="cc827-109">La fonctionnalité de capture des paquets Network Watcher vous permet de créer des sessions de capture afin d’effectuer le suivi du trafic en direction et en provenance d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc827-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="cc827-110">Les filtres sont fournis pour la session de capture afin de vous garantir que vous capturez uniquement le trafic souhaité.</span><span class="sxs-lookup"><span data-stu-id="cc827-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="cc827-111">La capture des paquets permet de diagnostiquer les anomalies réseau de manière proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="cc827-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="cc827-112">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="cc827-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="cc827-113">En déclenchant à distance des captures de paquets, cette fonctionnalité simplifie l’exécution manuelle de la capture de paquets sur l’ordinateur souhaité, ce qui permet d’économiser un temps précieux.</span><span class="sxs-lookup"><span data-stu-id="cc827-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="cc827-114">Cet article passe en revue les différentes tâches de gestion actuellement disponibles pour la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="cc827-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="cc827-115">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="cc827-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="cc827-116">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="cc827-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="cc827-117">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="cc827-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="cc827-118">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="cc827-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="cc827-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="cc827-119">Before you begin</span></span>

<span data-ttu-id="cc827-120">Cet article part du principe que vous disposez des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc827-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="cc827-121">Une instance de Network Watcher dans la région où vous souhaitez créer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cc827-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="cc827-122">Une machine virtuelle avec l’extension de capture de paquets activée.</span><span class="sxs-lookup"><span data-stu-id="cc827-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc827-123">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="cc827-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="cc827-124">Pour installer l’extension sur une machine virtuelle Windows, consultez la page [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Windows). Pour une machine virtuelle Linux, consultez la page [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Linux).</span><span class="sxs-lookup"><span data-stu-id="cc827-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="cc827-125">Installer une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cc827-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="cc827-126">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="cc827-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="cc827-127">Étape 2</span><span class="sxs-lookup"><span data-stu-id="cc827-127">Step 2</span></span>

<span data-ttu-id="cc827-128">L’exemple suivant récupère les informations d’extension nécessaires pour exécuter l’applet de commande `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="cc827-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="cc827-129">Cette applet de commande installe l’agent de capture de paquets sur la machine virtuelle invitée.</span><span class="sxs-lookup"><span data-stu-id="cc827-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="cc827-130">L’applet de commande `Set-AzureRmVMExtension` peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="cc827-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="cc827-131">Pour les machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="cc827-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="cc827-132">Pour les machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="cc827-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="cc827-133">L’exemple suivant est une réponse correcte après l’exécution d’applet de commande `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="cc827-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="cc827-134">Étape 3</span><span class="sxs-lookup"><span data-stu-id="cc827-134">Step 3</span></span>

<span data-ttu-id="cc827-135">Pour vous assurer que l’agent est installé, exécutez l’applet de commande `Get-AzureRmVMExtension` et transmettez-lui le nom de la machine virtuelle et le nom de l’extension.</span><span class="sxs-lookup"><span data-stu-id="cc827-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="cc827-136">L’exemple suivant montre la réponse à l’exécution de `Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="cc827-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="cc827-137">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cc827-137">Start a packet capture</span></span>

<span data-ttu-id="cc827-138">Une fois les étapes précédentes terminées, l’agent de capture de paquets est installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc827-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="cc827-139">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="cc827-139">Step 1</span></span>

<span data-ttu-id="cc827-140">L’étape suivante consiste à récupérer l’instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="cc827-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="cc827-141">Cette variable est transmise à l’applet de commande `New-AzureRmNetworkWatcherPacketCapture` lors de l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="cc827-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="cc827-142">Étape 2</span><span class="sxs-lookup"><span data-stu-id="cc827-142">Step 2</span></span>

<span data-ttu-id="cc827-143">Récupérez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc827-143">Retrieve a storage account.</span></span> <span data-ttu-id="cc827-144">Ce compte de stockage permet de stocker le fichier de capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="cc827-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="cc827-145">Étape 3</span><span class="sxs-lookup"><span data-stu-id="cc827-145">Step 3</span></span>

<span data-ttu-id="cc827-146">Des filtres peuvent être utilisés pour limiter les données stockées par la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="cc827-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="cc827-147">L’exemple suivant définit deux filtres.</span><span class="sxs-lookup"><span data-stu-id="cc827-147">The following example sets up two filters.</span></span>  <span data-ttu-id="cc827-148">Un filtre collecte le trafic TCP sortant uniquement à partir de l’adresse IP locale 10.0.0.3 vers les ports de destination 20, 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="cc827-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="cc827-149">Le second filtre collecte uniquement le trafic UDP.</span><span class="sxs-lookup"><span data-stu-id="cc827-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="cc827-150">Plusieurs filtres peuvent être définis pour une même capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="cc827-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="cc827-151">Étape 4</span><span class="sxs-lookup"><span data-stu-id="cc827-151">Step 4</span></span>

<span data-ttu-id="cc827-152">Exécutez l’applet de commande `New-AzureRmNetworkWatcherPacketCapture` pour démarrer le processus de capture de paquets, en transmettant les valeurs requises récupérées dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="cc827-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="cc827-153">L’exemple suivant est la sortie attendue de l’exécution de l’applet de commande `New-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="cc827-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="cc827-154">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cc827-154">Get a packet capture</span></span>

<span data-ttu-id="cc827-155">L’exécution de l’applet de commande `Get-AzureRmNetworkWatcherPacketCapture` extrait le statut d’une capture de paquets en cours d’exécution ou terminée.</span><span class="sxs-lookup"><span data-stu-id="cc827-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="cc827-156">L’exemple suivant présente la sortie de l’applet de commande `Get-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="cc827-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="cc827-157">L’exemple suivant est postérieur à la capture.</span><span class="sxs-lookup"><span data-stu-id="cc827-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="cc827-158">La valeur PacketCaptureStatus est Stopped, et la valeur StopReason est TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="cc827-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="cc827-159">Cela indique que la capture de paquets a réussi et s’est correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="cc827-159">This value shows that the packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="cc827-160">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cc827-160">Stop a packet capture</span></span>

<span data-ttu-id="cc827-161">Lors de l’exécution de l’applet de commande `Stop-AzureRmNetworkWatcherPacketCapture`, toute session de capture en cours est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="cc827-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="cc827-162">L’applet de commande ne retourne aucune réponse lorsqu’elle est exécutée dans une session de capture en cours d’exécution ou dans une session existante déjà arrêtée.</span><span class="sxs-lookup"><span data-stu-id="cc827-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="cc827-163">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cc827-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="cc827-164">La suppression d’une capture de paquets ne supprime pas le fichier dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc827-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="cc827-165">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cc827-165">Download a packet capture</span></span>

<span data-ttu-id="cc827-166">Une fois votre session de capture de paquets terminée, le fichier de capture peut être téléchargé vers le stockage d’objets blob ou dans un fichier local sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc827-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="cc827-167">L’emplacement de stockage de la capture de paquets est défini lors de la création de la session.</span><span class="sxs-lookup"><span data-stu-id="cc827-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="cc827-168">L’explorateur de stockage Microsoft Azure est un outil très pratique pour accéder à ces fichiers de capture enregistrés dans un compte de stockage. Vous pouvez le télécharger ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="cc827-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="cc827-169">Si un compte de stockage est spécifié, les fichiers de capture de paquets sont enregistrés dans un compte de stockage à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="cc827-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="cc827-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc827-170">Next steps</span></span>

<span data-ttu-id="cc827-171">Découvrez comment automatiser les captures de paquets avec des alertes de machine virtuelle en consultant [Create an alert triggered packet capture (Créer une capture de paquets déclenchée par alerte)](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="cc827-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="cc827-172">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cc827-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














