---
title: "Gérer les captures de paquets avec Azure Network Watcher - API REST | Microsoft Docs"
description: "Cette page explique comment gérer la fonctionnalité de capture de paquets de Network Watcher à l’aide de l’API REST Azure"
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
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="edfd9-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide de l’API REST Azure</span><span class="sxs-lookup"><span data-stu-id="edfd9-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="edfd9-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="edfd9-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="edfd9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="edfd9-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="edfd9-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="edfd9-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="edfd9-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="edfd9-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="edfd9-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="edfd9-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="edfd9-109">La fonctionnalité de capture des paquets Network Watcher vous permet de créer des sessions de capture afin d’effectuer le suivi du trafic en direction et en provenance d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="edfd9-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="edfd9-110">Les filtres sont fournis pour la session de capture afin de vous garantir que vous capturez uniquement le trafic souhaité.</span><span class="sxs-lookup"><span data-stu-id="edfd9-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="edfd9-111">La capture des paquets permet de diagnostiquer les anomalies réseau de manière proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="edfd9-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="edfd9-112">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="edfd9-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="edfd9-113">En déclenchant à distance des captures de paquets, cette fonctionnalité simplifie l’exécution manuelle de la capture de paquets sur l’ordinateur souhaité, ce qui permet d’économiser un temps précieux.</span><span class="sxs-lookup"><span data-stu-id="edfd9-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="edfd9-114">Cet article passe en revue les différentes tâches de gestion actuellement disponibles pour la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="edfd9-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="edfd9-115">**Obtenir une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="edfd9-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="edfd9-116">**Répertorier toutes les captures de paquets**</span><span class="sxs-lookup"><span data-stu-id="edfd9-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="edfd9-117">**Interroger l’état d’une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="edfd9-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="edfd9-118">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="edfd9-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="edfd9-119">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="edfd9-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="edfd9-120">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="edfd9-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="edfd9-121">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="edfd9-121">Before you begin</span></span>

<span data-ttu-id="edfd9-122">Dans ce scénario, vous appelez l’API REST Network Watcher pour exécuter la vérification des flux IP.</span><span class="sxs-lookup"><span data-stu-id="edfd9-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="edfd9-123">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edfd9-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="edfd9-124">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="edfd9-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="edfd9-125">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="edfd9-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="edfd9-126">La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="edfd9-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="edfd9-127">Pour installer l’extension sur une machine virtuelle Windows, consultez la page [Extension de machine virtuelle Agent Network Watcher pour Windows](../virtual-machines/windows/extensions-nwa.md). Pour une machine virtuelle Linux, consultez la page [Extension de machine virtuelle Agent Network Watcher pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="edfd9-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="edfd9-128">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="edfd9-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="edfd9-129">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="edfd9-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="edfd9-130">Exécutez le script suivant pour renvoyer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="edfd9-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="edfd9-131">Ces informations sont nécessaires pour démarrer une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="edfd9-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="edfd9-132">Le code suivant requiert des variables :</span><span class="sxs-lookup"><span data-stu-id="edfd9-132">The following code needs variables:</span></span>

- <span data-ttu-id="edfd9-133">**subscriptionId** - L’ID d’abonnement peut également être récupéré avec l’applet de commande **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="edfd9-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="edfd9-134">**resourceGroupName** - Le nom d’un groupe de ressources qui contient les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="edfd9-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="edfd9-135">À partir de la sortie suivante, l’ID de la machine virtuelle est utilisé dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="edfd9-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="edfd9-136">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="edfd9-136">Get a packet capture</span></span>

<span data-ttu-id="edfd9-137">L’exemple suivant obtient l’état d’une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="edfd9-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="edfd9-138">Les réponses ci-après sont des exemples de réponses classiques renvoyées lors de l’interrogation de l’état d’une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="edfd9-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="edfd9-139">Répertorier toutes les captures de paquets</span><span class="sxs-lookup"><span data-stu-id="edfd9-139">List all packet captures</span></span>

<span data-ttu-id="edfd9-140">L’exemple suivant obtient toutes les sessions de capture de paquets dans une région.</span><span class="sxs-lookup"><span data-stu-id="edfd9-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="edfd9-141">La réponse ci-après est un exemple de réponse classique renvoyée lors de l’obtention de toutes les captures de paquets.</span><span class="sxs-lookup"><span data-stu-id="edfd9-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="edfd9-142">Interroger l’état d’une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="edfd9-142">Query packet capture status</span></span>

<span data-ttu-id="edfd9-143">L’exemple suivant obtient toutes les sessions de capture de paquets dans une région.</span><span class="sxs-lookup"><span data-stu-id="edfd9-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="edfd9-144">La réponse ci-après est un exemple de réponse classique renvoyée lors de l’interrogation de l’état d’une capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="edfd9-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="edfd9-145">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="edfd9-145">Start packet capture</span></span>

<span data-ttu-id="edfd9-146">L’exemple suivant crée une capture de paquets sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="edfd9-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="edfd9-147">L’exemple est paramétré pour permettre une certaine flexibilité dans la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="edfd9-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="edfd9-148">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="edfd9-148">Stop packet capture</span></span>

<span data-ttu-id="edfd9-149">L’exemple suivant arrête une capture de paquets sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="edfd9-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="edfd9-150">L’exemple est paramétré pour permettre une certaine flexibilité dans la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="edfd9-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="edfd9-151">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="edfd9-151">Delete packet capture</span></span>

<span data-ttu-id="edfd9-152">L’exemple suivant supprime une capture de paquets d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="edfd9-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="edfd9-153">L’exemple est paramétré pour permettre une certaine flexibilité dans la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="edfd9-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="edfd9-154">La suppression d’une capture de paquets ne supprime pas le fichier du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="edfd9-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="edfd9-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="edfd9-155">Next steps</span></span>

<span data-ttu-id="edfd9-156">Pour obtenir des instructions de téléchargement des fichiers à partir des comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="edfd9-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="edfd9-157">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="edfd9-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="edfd9-158">Pour en savoir plus sur l’explorateur de stockage, cliquez sur le lien suivant : [Microsoft Azure Storage Explorer](http://storageexplorer.com/) (Explorateur de stockage Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="edfd9-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="edfd9-159">Découvrez comment automatiser les captures de paquets avec des alertes de machine virtuelle en consultant [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md) (Utiliser la capture de paquets pour surveiller un réseau de manière proactive avec Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="edfd9-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













