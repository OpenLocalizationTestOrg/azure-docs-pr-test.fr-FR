---
title: "captures de paquets d’aaaManage d’observateur de réseau Azure - API REST | Documents Microsoft"
description: "Cette page explique comment toomanage hello la fonctionnalité de capture de paquet de l’Observateur réseau à l’aide des API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="a1c60-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide de l’API REST Azure</span><span class="sxs-lookup"><span data-stu-id="a1c60-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a1c60-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="a1c60-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="a1c60-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1c60-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="a1c60-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a1c60-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="a1c60-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a1c60-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="a1c60-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="a1c60-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="a1c60-109">Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1c60-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="a1c60-110">Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="a1c60-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="a1c60-111">Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="a1c60-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="a1c60-112">Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="a1c60-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="a1c60-113">En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.</span><span class="sxs-lookup"><span data-stu-id="a1c60-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="a1c60-114">Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="a1c60-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="a1c60-115">**Obtenir une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="a1c60-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="a1c60-116">**Répertorier toutes les captures de paquets**</span><span class="sxs-lookup"><span data-stu-id="a1c60-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="a1c60-117">**Interroger le statut d’une capture de paquets hello**</span><span class="sxs-lookup"><span data-stu-id="a1c60-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="a1c60-118">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="a1c60-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="a1c60-119">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="a1c60-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="a1c60-120">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="a1c60-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="a1c60-121">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a1c60-121">Before you begin</span></span>

<span data-ttu-id="a1c60-122">Dans ce scénario, vous appelez toorun d’API Rest de l’Observateur réseau hello IP flux vérifier.</span><span class="sxs-lookup"><span data-stu-id="a1c60-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="a1c60-123">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1c60-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="a1c60-124">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="a1c60-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a1c60-125">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="a1c60-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="a1c60-126">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="a1c60-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="a1c60-127">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="a1c60-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a1c60-128">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="a1c60-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="a1c60-129">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a1c60-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="a1c60-130">Exécutez hello suivant script tooreturn une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a1c60-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="a1c60-131">Ces informations sont nécessaires pour démarrer une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="a1c60-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="a1c60-132">Hello suivant code a besoin de variables :</span><span class="sxs-lookup"><span data-stu-id="a1c60-132">hello following code needs variables:</span></span>

- <span data-ttu-id="a1c60-133">**ID d’abonnement** -id d’abonnement hello peut également être récupéré avec hello **Get-AzureRMSubscription** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a1c60-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="a1c60-134">**resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a1c60-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="a1c60-135">À partir de la sortie suivante de hello, id hello de machine virtuelle de hello est utilisé dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c60-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="a1c60-136">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="a1c60-136">Get a packet capture</span></span>

<span data-ttu-id="a1c60-137">exemple Hello obtient état hello d’une capture de paquet</span><span class="sxs-lookup"><span data-stu-id="a1c60-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="a1c60-138">Hello réponses suivantes sont des exemples d’une réponse de type retourné lors de l’interrogation État hello d’une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="a1c60-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="a1c60-139">Répertorier toutes les captures de paquets</span><span class="sxs-lookup"><span data-stu-id="a1c60-139">List all packet captures</span></span>

<span data-ttu-id="a1c60-140">Hello exemple ci-dessous obtient toutes les sessions de capture de paquets dans une région.</span><span class="sxs-lookup"><span data-stu-id="a1c60-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="a1c60-141">Bonjour réponse suivante est un exemple d’une réponse de type retourné lors de l’obtention de tous les paquets capture</span><span class="sxs-lookup"><span data-stu-id="a1c60-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="a1c60-142">Interroger l’état d’une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="a1c60-142">Query packet capture status</span></span>

<span data-ttu-id="a1c60-143">Hello exemple ci-dessous obtient toutes les sessions de capture de paquets dans une région.</span><span class="sxs-lookup"><span data-stu-id="a1c60-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="a1c60-144">Hello réponse suivante est un exemple d’une réponse de type retourné lors de l’interrogation État hello d’une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="a1c60-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="a1c60-145">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="a1c60-145">Start packet capture</span></span>

<span data-ttu-id="a1c60-146">Bonjour à l’exemple suivant crée une capture de paquets sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1c60-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="a1c60-147">exemple de Hello est paramétrable tooallow pour une grande souplesse pour la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="a1c60-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="a1c60-148">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="a1c60-148">Stop packet capture</span></span>

<span data-ttu-id="a1c60-149">Bonjour à l’exemple suivant arrête une capture de paquets sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1c60-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="a1c60-150">exemple de Hello est paramétrable tooallow pour une grande souplesse pour la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="a1c60-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="a1c60-151">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="a1c60-151">Delete packet capture</span></span>

<span data-ttu-id="a1c60-152">Bonjour à l’exemple suivant supprime une capture de paquets sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a1c60-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="a1c60-153">exemple de Hello est paramétrable tooallow pour une grande souplesse pour la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="a1c60-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="a1c60-154">Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage</span><span class="sxs-lookup"><span data-stu-id="a1c60-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1c60-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1c60-155">Next steps</span></span>

<span data-ttu-id="a1c60-156">Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a1c60-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a1c60-157">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="a1c60-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a1c60-158">Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a1c60-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="a1c60-159">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a1c60-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













