---
title: "captures de paquets d’aaaManage d’observateur de réseau Azure - Azure CLI 2.0 | Documents Microsoft"
description: "Cette page explique comment toomanage hello la fonctionnalité de capture de paquet de l’Observateur réseau à l’aide d’Azure CLI 2.0"
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="9d96a-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d96a-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9d96a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9d96a-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="9d96a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d96a-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="9d96a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9d96a-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="9d96a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d96a-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="9d96a-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="9d96a-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="9d96a-109">Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d96a-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="9d96a-110">Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9d96a-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="9d96a-111">Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="9d96a-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="9d96a-112">Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="9d96a-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="9d96a-113">En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.</span><span class="sxs-lookup"><span data-stu-id="9d96a-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="9d96a-114">Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="9d96a-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="9d96a-115">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9d96a-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="9d96a-116">Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="9d96a-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="9d96a-117">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="9d96a-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="9d96a-118">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="9d96a-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="9d96a-119">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="9d96a-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="9d96a-120">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="9d96a-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="9d96a-121">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9d96a-121">Before you begin</span></span>

<span data-ttu-id="9d96a-122">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="9d96a-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="9d96a-123">Une instance de l’Observateur réseau dans la région de hello souhaité toocreate une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="9d96a-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="9d96a-124">Une machine virtuelle avec les paquets hello capturer extension activée.</span><span class="sxs-lookup"><span data-stu-id="9d96a-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d96a-125">Capture des paquets nécessite une toobe de l’agent en cours d’exécution sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="9d96a-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="9d96a-126">Hello, l’Agent est installé en tant qu’extension.</span><span class="sxs-lookup"><span data-stu-id="9d96a-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="9d96a-127">Pour obtenir des instructions sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="9d96a-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="9d96a-128">Installer une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9d96a-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="9d96a-129">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9d96a-129">Step 1</span></span>

<span data-ttu-id="9d96a-130">Exécutez hello `az vm extension set` agent de capture de paquet applet de commande tooinstall hello sur ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="9d96a-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="9d96a-131">Pour les machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="9d96a-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="9d96a-132">Pour les machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="9d96a-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="9d96a-133">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9d96a-133">Step 2</span></span>

<span data-ttu-id="9d96a-134">tooensure qui hello agent est installé, exécutez hello `vm extension get` applet de commande et lui passer de groupe de ressources hello et nom d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d96a-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="9d96a-135">Vérifiez que hello résultant liste tooensure hello agent est installé.</span><span class="sxs-lookup"><span data-stu-id="9d96a-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="9d96a-136">Hello suivant l’exemple est un exemple de réponse hello en cours d’exécution`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="9d96a-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="9d96a-137">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="9d96a-137">Start a packet capture</span></span>

<span data-ttu-id="9d96a-138">Une fois hello étapes précédentes terminées, l’agent de capture de paquets hello est installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="9d96a-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="9d96a-139">Étape 1</span><span class="sxs-lookup"><span data-stu-id="9d96a-139">Step 1</span></span>

<span data-ttu-id="9d96a-140">étape suivante de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="9d96a-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="9d96a-141">Nom de section de hello Observateur réseau est passé toohello `az network watcher show` applet de commande à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="9d96a-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="9d96a-142">Étape 2</span><span class="sxs-lookup"><span data-stu-id="9d96a-142">Step 2</span></span>

<span data-ttu-id="9d96a-143">Récupérez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9d96a-143">Retrieve a storage account.</span></span> <span data-ttu-id="9d96a-144">Ce compte de stockage est un fichier de capture de paquets hello toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="9d96a-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="9d96a-145">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="9d96a-145">Step 3</span></span>

<span data-ttu-id="9d96a-146">Filtres peuvent être des données hello toolimit utilisé qui sont stockées par la capture des paquets hello.</span><span class="sxs-lookup"><span data-stu-id="9d96a-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="9d96a-147">Hello exemple suivant configure une capture de paquets avec plusieurs filtres.</span><span class="sxs-lookup"><span data-stu-id="9d96a-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="9d96a-148">Hello tout d’abord trois filtres collecter le trafic TCP sortant uniquement à partir de l’adresse IP locale 10.0.0.3 toodestination ports 20, 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="9d96a-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="9d96a-149">dernier filtre de Hello collecte uniquement le trafic UDP.</span><span class="sxs-lookup"><span data-stu-id="9d96a-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="9d96a-150">exemple suivant Hello est sortie de hello attendu de l’exécution de hello `az network watcher packet-capture create` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9d96a-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="9d96a-151">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="9d96a-151">Get a packet capture</span></span>

<span data-ttu-id="9d96a-152">En cours d’exécution hello `az network watcher packet-capture show` applet de commande récupère l’état hello d’une capture de paquets en cours d’exécution ou terminé.</span><span class="sxs-lookup"><span data-stu-id="9d96a-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="9d96a-153">exemple Hello est sortie hello hello `az network watcher packet-capture show` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9d96a-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="9d96a-154">Hello exemple suivant est une fois la capture de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="9d96a-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="9d96a-155">Hello PacketCaptureStatus valeur avec un StopReason de TimeExceeded est arrêté.</span><span class="sxs-lookup"><span data-stu-id="9d96a-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="9d96a-156">Cette valeur indique que la capture des paquets hello a réussi et son exécution.</span><span class="sxs-lookup"><span data-stu-id="9d96a-156">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="9d96a-157">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="9d96a-157">Stop a packet capture</span></span>

<span data-ttu-id="9d96a-158">En exécutant hello `az network watcher packet-capture stop` applet de commande, si une session de capture est en cours d’exécution, il est arrêté.</span><span class="sxs-lookup"><span data-stu-id="9d96a-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="9d96a-159">applet de commande Hello ne retourne pas de réponse lorsque s’exécutait sur une session de capture en cours d’exécution ou une session existante qui a déjà été arrêté.</span><span class="sxs-lookup"><span data-stu-id="9d96a-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="9d96a-160">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="9d96a-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="9d96a-161">Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9d96a-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="9d96a-162">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="9d96a-162">Download a packet capture</span></span>

<span data-ttu-id="9d96a-163">Une fois terminé, votre session de capture de paquets hello capture fichier peut être téléchargé tooblob tooa ou stockage local sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9d96a-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="9d96a-164">emplacement de stockage Hello de capture de paquets hello est définie lors de la création de la session de hello.</span><span class="sxs-lookup"><span data-stu-id="9d96a-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="9d96a-165">Un outil pratique de tooaccess ces fichiers de capture de compte de stockage tooa enregistré est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="9d96a-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="9d96a-166">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="9d96a-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="9d96a-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d96a-167">Next steps</span></span>

<span data-ttu-id="9d96a-168">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="9d96a-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="9d96a-169">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9d96a-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
