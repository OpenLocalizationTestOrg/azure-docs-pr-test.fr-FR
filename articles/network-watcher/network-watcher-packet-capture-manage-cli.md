---
title: "Gérer les captures de paquets avec Azure Network Watcher - Azure CLI 2.0 | Microsoft Docs"
description: "Cette page explique comment gérer la fonctionnalité de capture de paquets de Network Watcher à l’aide d’Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="ad694-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ad694-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ad694-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ad694-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="ad694-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad694-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="ad694-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ad694-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="ad694-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ad694-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="ad694-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="ad694-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="ad694-109">La fonctionnalité de capture des paquets Network Watcher vous permet de créer des sessions de capture afin d’effectuer le suivi du trafic en direction et en provenance d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ad694-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="ad694-110">Les filtres sont fournis pour la session de capture afin de vous garantir que vous capturez uniquement le trafic souhaité.</span><span class="sxs-lookup"><span data-stu-id="ad694-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="ad694-111">La capture des paquets permet de diagnostiquer les anomalies réseau de manière proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="ad694-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="ad694-112">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="ad694-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="ad694-113">En déclenchant à distance des captures de paquets, cette fonctionnalité simplifie l’exécution manuelle de la capture de paquets sur l’ordinateur souhaité, ce qui permet d’économiser un temps précieux.</span><span class="sxs-lookup"><span data-stu-id="ad694-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="ad694-114">Dans cet article, notre CLI nouvelle génération, Azure CLI 2.0, est utilisée pour le modèle de déploiement de gestion des ressources. Celle-ci est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="ad694-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="ad694-115">Pour exécuter la procédure indiquée dans cet article, vous devez [installer l’interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ad694-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="ad694-116">Cet article passe en revue les différentes tâches de gestion actuellement disponibles pour la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="ad694-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="ad694-117">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="ad694-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="ad694-118">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="ad694-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="ad694-119">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="ad694-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="ad694-120">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="ad694-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="ad694-121">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ad694-121">Before you begin</span></span>

<span data-ttu-id="ad694-122">Cet article part du principe que vous disposez des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="ad694-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="ad694-123">Une instance de Network Watcher dans la région où vous souhaitez créer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="ad694-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="ad694-124">Une machine virtuelle avec l’extension de capture de paquets activée.</span><span class="sxs-lookup"><span data-stu-id="ad694-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad694-125">La capture de paquets nécessite l’exécution d’un agent sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ad694-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="ad694-126">L’Agent est installé en tant qu’extension.</span><span class="sxs-lookup"><span data-stu-id="ad694-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="ad694-127">Pour obtenir des instructions sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="ad694-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="ad694-128">Installer une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ad694-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="ad694-129">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="ad694-129">Step 1</span></span>

<span data-ttu-id="ad694-130">Exécutez l’applet de commande `az vm extension set` pour installer l’agent de capture de paquets sur la machine virtuelle invitée.</span><span class="sxs-lookup"><span data-stu-id="ad694-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="ad694-131">Pour les machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="ad694-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="ad694-132">Pour les machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="ad694-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="ad694-133">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ad694-133">Step 2</span></span>

<span data-ttu-id="ad694-134">Pour vous assurer que l’agent est installé, exécutez l’applet de commande `vm extension get` et transmettez-lui le groupe de ressources ainsi que le nom de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ad694-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="ad694-135">Vérifiez la liste obtenue afin de vous assurer que l’agent est bien installé.</span><span class="sxs-lookup"><span data-stu-id="ad694-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="ad694-136">L’exemple suivant montre la réponse à l’exécution de `az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="ad694-136">The following sample is an example of the response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="ad694-137">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="ad694-137">Start a packet capture</span></span>

<span data-ttu-id="ad694-138">Une fois les étapes précédentes terminées, l’agent de capture de paquets est installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ad694-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="ad694-139">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="ad694-139">Step 1</span></span>

<span data-ttu-id="ad694-140">L’étape suivante consiste à récupérer l’instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="ad694-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="ad694-141">Le nom du Network Watcher est transmis à l’applet de commande `az network watcher show` à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="ad694-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="ad694-142">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ad694-142">Step 2</span></span>

<span data-ttu-id="ad694-143">Récupérez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ad694-143">Retrieve a storage account.</span></span> <span data-ttu-id="ad694-144">Ce compte de stockage permet de stocker le fichier de capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="ad694-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="ad694-145">Étape 3</span><span class="sxs-lookup"><span data-stu-id="ad694-145">Step 3</span></span>

<span data-ttu-id="ad694-146">Des filtres peuvent être utilisés pour limiter les données stockées par la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="ad694-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="ad694-147">L’exemple suivant présente la configuration d’une capture de paquets à l’aide de plusieurs filtres.</span><span class="sxs-lookup"><span data-stu-id="ad694-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="ad694-148">Les trois premiers filtres collectent le trafic TCP sortant uniquement à partir de l’adresse IP locale 10.0.0.3 vers les ports de destination 20, 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="ad694-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="ad694-149">Le dernier filtre collecte uniquement le trafic UDP.</span><span class="sxs-lookup"><span data-stu-id="ad694-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="ad694-150">L’exemple suivant est la sortie attendue de l’exécution de l’applet de commande `az network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="ad694-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="ad694-151">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="ad694-151">Get a packet capture</span></span>

<span data-ttu-id="ad694-152">L’exécution de l’applet de commande `az network watcher packet-capture show` extrait le statut d’une capture de paquets en cours d’exécution ou terminée.</span><span class="sxs-lookup"><span data-stu-id="ad694-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="ad694-153">L’exemple suivant présente la sortie de l’applet de commande `az network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="ad694-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="ad694-154">L’exemple suivant est postérieur à la capture.</span><span class="sxs-lookup"><span data-stu-id="ad694-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="ad694-155">La valeur PacketCaptureStatus est Stopped, et la valeur StopReason est TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="ad694-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="ad694-156">Cela indique que la capture de paquets a réussi et s’est correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="ad694-156">This value shows that the packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="ad694-157">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="ad694-157">Stop a packet capture</span></span>

<span data-ttu-id="ad694-158">Lors de l’exécution de l’applet de commande `az network watcher packet-capture stop`, toute session de capture en cours est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="ad694-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="ad694-159">L’applet de commande ne retourne aucune réponse lorsqu’elle est exécutée dans une session de capture en cours d’exécution ou dans une session existante déjà arrêtée.</span><span class="sxs-lookup"><span data-stu-id="ad694-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="ad694-160">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="ad694-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="ad694-161">La suppression d’une capture de paquets ne supprime pas le fichier dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ad694-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="ad694-162">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="ad694-162">Download a packet capture</span></span>

<span data-ttu-id="ad694-163">Une fois votre session de capture de paquets terminée, le fichier de capture peut être téléchargé vers le stockage d’objets blob ou dans un fichier local sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ad694-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="ad694-164">L’emplacement de stockage de la capture de paquets est défini lors de la création de la session.</span><span class="sxs-lookup"><span data-stu-id="ad694-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="ad694-165">L’explorateur de stockage Microsoft Azure est un outil très pratique pour accéder à ces fichiers de capture enregistrés dans un compte de stockage. Vous pouvez le télécharger ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="ad694-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="ad694-166">Si un compte de stockage est spécifié, les fichiers de capture de paquets sont enregistrés dans un compte de stockage à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="ad694-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="ad694-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad694-167">Next steps</span></span>

<span data-ttu-id="ad694-168">Découvrez comment automatiser les captures de paquets avec des alertes de machine virtuelle en consultant [Create an alert triggered packet capture (Créer une capture de paquets déclenchée par alerte)](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="ad694-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="ad694-169">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ad694-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
