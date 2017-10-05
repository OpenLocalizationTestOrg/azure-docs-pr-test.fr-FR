---
title: "Gérer les captures de paquets avec Azure Network Watcher - Azure CLI 1.0 | Microsoft Docs"
description: "Cette page explique comment gérer la fonctionnalité de capture de paquets de Network Watcher à l’aide d’Azure CLI 1.0"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="94764-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="94764-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="94764-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="94764-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="94764-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94764-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="94764-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="94764-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="94764-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94764-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="94764-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="94764-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="94764-109">La fonctionnalité de capture des paquets Network Watcher vous permet de créer des sessions de capture afin d’effectuer le suivi du trafic en direction et en provenance d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94764-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="94764-110">Les filtres sont fournis pour la session de capture afin de vous garantir que vous capturez uniquement le trafic souhaité.</span><span class="sxs-lookup"><span data-stu-id="94764-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="94764-111">La capture des paquets permet de diagnostiquer les anomalies réseau de manière proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="94764-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="94764-112">Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.</span><span class="sxs-lookup"><span data-stu-id="94764-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="94764-113">En déclenchant à distance des captures de paquets, cette fonctionnalité simplifie l’exécution manuelle de la capture de paquets sur l’ordinateur souhaité, ce qui permet d’économiser un temps précieux.</span><span class="sxs-lookup"><span data-stu-id="94764-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="94764-114">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="94764-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="94764-115">Cet article passe en revue les différentes tâches de gestion actuellement disponibles pour la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="94764-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="94764-116">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="94764-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="94764-117">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="94764-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="94764-118">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="94764-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="94764-119">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="94764-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="94764-120">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="94764-120">Before you begin</span></span>

<span data-ttu-id="94764-121">Cet article part du principe que vous disposez des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="94764-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="94764-122">Une instance de Network Watcher dans la région où vous souhaitez créer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="94764-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="94764-123">Une machine virtuelle avec l’extension de capture de paquets activée.</span><span class="sxs-lookup"><span data-stu-id="94764-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94764-124">La capture de paquets nécessite l’exécution d’un agent sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94764-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="94764-125">L’Agent est installé en tant qu’extension.</span><span class="sxs-lookup"><span data-stu-id="94764-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="94764-126">Pour obtenir des instructions sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="94764-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="94764-127">Installer une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="94764-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="94764-128">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="94764-128">Step 1</span></span>

<span data-ttu-id="94764-129">Exécutez l’applet de commande `azure vm extension set` pour installer l’agent de capture de paquets sur la machine virtuelle invitée.</span><span class="sxs-lookup"><span data-stu-id="94764-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="94764-130">Pour les machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="94764-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="94764-131">Pour les machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="94764-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="94764-132">Étape 2</span><span class="sxs-lookup"><span data-stu-id="94764-132">Step 2</span></span>

<span data-ttu-id="94764-133">Pour vous assurer que l’agent est installé, exécutez l’applet de commande `vm extension get` et transmettez-lui le groupe de ressources ainsi que le nom de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94764-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="94764-134">Vérifiez la liste obtenue afin de vous assurer que l’agent est bien installé.</span><span class="sxs-lookup"><span data-stu-id="94764-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="94764-135">L’exemple suivant montre la réponse à l’exécution de `azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="94764-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="94764-136">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="94764-136">Start a packet capture</span></span>

<span data-ttu-id="94764-137">Une fois les étapes précédentes terminées, l’agent de capture de paquets est installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94764-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="94764-138">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="94764-138">Step 1</span></span>

<span data-ttu-id="94764-139">L’étape suivante consiste à récupérer l’instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="94764-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="94764-140">Cette variable est transmise à l’applet de commande `network watcher show` lors de l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="94764-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="94764-141">Étape 2</span><span class="sxs-lookup"><span data-stu-id="94764-141">Step 2</span></span>

<span data-ttu-id="94764-142">Récupérez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="94764-142">Retrieve a storage account.</span></span> <span data-ttu-id="94764-143">Ce compte de stockage permet de stocker le fichier de capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="94764-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="94764-144">Étape 3</span><span class="sxs-lookup"><span data-stu-id="94764-144">Step 3</span></span>

<span data-ttu-id="94764-145">Des filtres peuvent être utilisés pour limiter les données stockées par la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="94764-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="94764-146">L’exemple suivant présente la configuration d’une capture de paquets à l’aide de plusieurs filtres.</span><span class="sxs-lookup"><span data-stu-id="94764-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="94764-147">Les trois premiers filtres collectent le trafic TCP sortant uniquement à partir de l’adresse IP locale 10.0.0.3 vers les ports de destination 20, 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="94764-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="94764-148">Le dernier filtre collecte uniquement le trafic UDP.</span><span class="sxs-lookup"><span data-stu-id="94764-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="94764-149">Plusieurs filtres peuvent être définis pour une même capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="94764-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="94764-150">Si vous utilisez une structure de filtres complexe, il est préférable de recourir à des filtres de type fichier json pour éviter les erreurs de syntaxe.</span><span class="sxs-lookup"><span data-stu-id="94764-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="94764-151">Par exemple, utilisez l’indicateur « -r » (au lieu de « -f ») et transmettez l’emplacement d’un fichier json contenant les filtres suivants :</span><span class="sxs-lookup"><span data-stu-id="94764-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="94764-152">L’exemple suivant est la sortie attendue de l’exécution de l’applet de commande `network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="94764-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="94764-153">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="94764-153">Get a packet capture</span></span>

<span data-ttu-id="94764-154">L’exécution de l’applet de commande `network watcher packet-capture show` extrait le statut d’une capture de paquets en cours d’exécution ou terminée.</span><span class="sxs-lookup"><span data-stu-id="94764-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="94764-155">L’exemple suivant présente la sortie de l’applet de commande `network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="94764-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="94764-156">L’exemple suivant est postérieur à la capture.</span><span class="sxs-lookup"><span data-stu-id="94764-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="94764-157">La valeur PacketCaptureStatus est Stopped, et la valeur StopReason est TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="94764-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="94764-158">Cela indique que la capture de paquets a réussi et s’est correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="94764-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="94764-159">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="94764-159">Stop a packet capture</span></span>

<span data-ttu-id="94764-160">Lors de l’exécution de l’applet de commande `network watcher packet-capture stop`, toute session de capture en cours est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="94764-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="94764-161">L’applet de commande ne retourne aucune réponse lorsqu’elle est exécutée dans une session de capture en cours d’exécution ou dans une session existante déjà arrêtée.</span><span class="sxs-lookup"><span data-stu-id="94764-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="94764-162">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="94764-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="94764-163">La suppression d’une capture de paquets ne supprime pas le fichier dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="94764-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="94764-164">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="94764-164">Download a packet capture</span></span>

<span data-ttu-id="94764-165">Une fois votre session de capture de paquets terminée, le fichier de capture peut être téléchargé vers le stockage d’objets blob ou dans un fichier local sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94764-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="94764-166">L’emplacement de stockage de la capture de paquets est défini lors de la création de la session.</span><span class="sxs-lookup"><span data-stu-id="94764-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="94764-167">L’explorateur de stockage Microsoft Azure est un outil très pratique pour accéder à ces fichiers de capture enregistrés dans un compte de stockage. Vous pouvez le télécharger ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="94764-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="94764-168">Si un compte de stockage est spécifié, les fichiers de capture de paquets sont enregistrés dans un compte de stockage à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="94764-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="94764-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94764-169">Next steps</span></span>

<span data-ttu-id="94764-170">Découvrez comment automatiser les captures de paquets avec des alertes de machine virtuelle en consultant [Create an alert triggered packet capture (Créer une capture de paquets déclenchée par alerte)](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="94764-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="94764-171">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="94764-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
