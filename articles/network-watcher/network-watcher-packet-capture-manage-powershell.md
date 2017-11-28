---
title: "captures de paquets d’aaaManage d’observateur de réseau Azure - PowerShell | Documents Microsoft"
description: "Cette page explique comment les paquets hello de toomanage capturer la fonctionnalité de l’Observateur réseau à l’aide de PowerShell"
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
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="98a36-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="98a36-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="98a36-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="98a36-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="98a36-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98a36-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="98a36-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="98a36-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="98a36-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="98a36-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="98a36-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="98a36-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="98a36-109">Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="98a36-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="98a36-110">Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="98a36-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="98a36-111">Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="98a36-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="98a36-112">Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="98a36-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="98a36-113">En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.</span><span class="sxs-lookup"><span data-stu-id="98a36-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="98a36-114">Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="98a36-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="98a36-115">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="98a36-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="98a36-116">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="98a36-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="98a36-117">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="98a36-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="98a36-118">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="98a36-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="98a36-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="98a36-119">Before you begin</span></span>

<span data-ttu-id="98a36-120">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="98a36-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="98a36-121">Une instance de l’Observateur réseau dans la région de hello souhaité toocreate une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="98a36-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="98a36-122">Une machine virtuelle avec les paquets hello capturer extension activée.</span><span class="sxs-lookup"><span data-stu-id="98a36-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98a36-123">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="98a36-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="98a36-124">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="98a36-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="98a36-125">Installer une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="98a36-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="98a36-126">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="98a36-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="98a36-127">Étape 2</span><span class="sxs-lookup"><span data-stu-id="98a36-127">Step 2</span></span>

<span data-ttu-id="98a36-128">exemple suivant récupère hello informations d’extension Hello nécessaire toorun hello `Set-AzureRmVMExtension` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="98a36-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="98a36-129">Cette applet de commande installe l’agent de capture de paquets hello sur ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="98a36-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="98a36-130">Hello `Set-AzureRmVMExtension` applet de commande peut prendre plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="98a36-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="98a36-131">Pour les machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="98a36-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="98a36-132">Pour les machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="98a36-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="98a36-133">Bonjour exemple suivant est une réponse correcte après l’exécution de hello `Set-AzureRmVMExtension` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="98a36-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="98a36-134">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="98a36-134">Step 3</span></span>

<span data-ttu-id="98a36-135">tooensure qui hello agent est installé, exécutez hello `Get-AzureRmVMExtension` applet de commande et passer le nom d’ordinateur virtuel hello hello nom et extension.</span><span class="sxs-lookup"><span data-stu-id="98a36-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="98a36-136">Hello suivant l’exemple est un exemple de réponse hello en cours d’exécution`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="98a36-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="98a36-137">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="98a36-137">Start a packet capture</span></span>

<span data-ttu-id="98a36-138">Une fois hello étapes précédentes terminées, l’agent de capture de paquets hello est installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="98a36-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="98a36-139">Étape 1</span><span class="sxs-lookup"><span data-stu-id="98a36-139">Step 1</span></span>

<span data-ttu-id="98a36-140">étape suivante de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="98a36-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="98a36-141">Cette variable est passée toohello `New-AzureRmNetworkWatcherPacketCapture` applet de commande à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="98a36-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="98a36-142">Étape 2</span><span class="sxs-lookup"><span data-stu-id="98a36-142">Step 2</span></span>

<span data-ttu-id="98a36-143">Récupérez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="98a36-143">Retrieve a storage account.</span></span> <span data-ttu-id="98a36-144">Ce compte de stockage est un fichier de capture de paquets hello toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="98a36-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="98a36-145">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="98a36-145">Step 3</span></span>

<span data-ttu-id="98a36-146">Filtres peuvent être des données hello toolimit utilisé qui sont stockées par la capture des paquets hello.</span><span class="sxs-lookup"><span data-stu-id="98a36-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="98a36-147">Hello exemple suivant définit deux filtres.</span><span class="sxs-lookup"><span data-stu-id="98a36-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="98a36-148">Collecte d’un filtre sortant TCP le trafic uniquement à partir de l’adresse IP locale 10.0.0.3 toodestination ports 20, 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="98a36-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="98a36-149">deuxième filtre de Hello collecte uniquement le trafic UDP.</span><span class="sxs-lookup"><span data-stu-id="98a36-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="98a36-150">Plusieurs filtres peuvent être définis pour une même capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="98a36-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="98a36-151">Étape 4</span><span class="sxs-lookup"><span data-stu-id="98a36-151">Step 4</span></span>

<span data-ttu-id="98a36-152">Exécutez hello `New-AzureRmNetworkWatcherPacketCapture` applet de commande toostart hello paquet processus de capture, passer les valeurs hello requis récupérées Bonjour étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="98a36-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="98a36-153">exemple suivant Hello est sortie de hello attendu de l’exécution de hello `New-AzureRmNetworkWatcherPacketCapture` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="98a36-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="98a36-154">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="98a36-154">Get a packet capture</span></span>

<span data-ttu-id="98a36-155">En cours d’exécution hello `Get-AzureRmNetworkWatcherPacketCapture` applet de commande récupère l’état hello d’une capture de paquets en cours d’exécution ou terminé.</span><span class="sxs-lookup"><span data-stu-id="98a36-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="98a36-156">exemple Hello est sortie hello hello `Get-AzureRmNetworkWatcherPacketCapture` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="98a36-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="98a36-157">Hello exemple suivant est une fois la capture de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="98a36-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="98a36-158">Hello PacketCaptureStatus valeur avec un StopReason de TimeExceeded est arrêté.</span><span class="sxs-lookup"><span data-stu-id="98a36-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="98a36-159">Cette valeur indique que la capture des paquets hello a réussi et son exécution.</span><span class="sxs-lookup"><span data-stu-id="98a36-159">This value shows that hello packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="98a36-160">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="98a36-160">Stop a packet capture</span></span>

<span data-ttu-id="98a36-161">En exécutant hello `Stop-AzureRmNetworkWatcherPacketCapture` applet de commande, si une session de capture est en cours d’exécution, il est arrêté.</span><span class="sxs-lookup"><span data-stu-id="98a36-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="98a36-162">applet de commande Hello ne retourne pas de réponse lorsque s’exécutait sur une session de capture en cours d’exécution ou une session existante qui a déjà été arrêté.</span><span class="sxs-lookup"><span data-stu-id="98a36-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="98a36-163">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="98a36-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="98a36-164">Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="98a36-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="98a36-165">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="98a36-165">Download a packet capture</span></span>

<span data-ttu-id="98a36-166">Une fois terminé, votre session de capture de paquets hello capture fichier peut être téléchargé tooblob tooa ou stockage local sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="98a36-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="98a36-167">emplacement de stockage Hello de capture de paquets hello est définie lors de la création de la session de hello.</span><span class="sxs-lookup"><span data-stu-id="98a36-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="98a36-168">Un outil pratique de tooaccess ces fichiers de capture de compte de stockage tooa enregistré est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="98a36-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="98a36-169">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="98a36-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="98a36-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98a36-170">Next steps</span></span>

<span data-ttu-id="98a36-171">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="98a36-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="98a36-172">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="98a36-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














