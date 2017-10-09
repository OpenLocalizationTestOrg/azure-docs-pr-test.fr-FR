---
title: "captures de paquets d’aaaManage d’observateur de réseau Azure - Azure CLI 1.0 | Documents Microsoft"
description: "Cette page explique comment toomanage hello la fonctionnalité de capture de paquet de l’Observateur réseau à l’aide d’Azure CLI 1.0"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="19e13-103">Gérer les captures de paquets avec Azure Network Watcher à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="19e13-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="19e13-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="19e13-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="19e13-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19e13-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="19e13-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="19e13-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="19e13-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="19e13-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="19e13-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="19e13-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="19e13-109">Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="19e13-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="19e13-110">Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="19e13-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="19e13-111">Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive.</span><span class="sxs-lookup"><span data-stu-id="19e13-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="19e13-112">Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="19e13-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="19e13-113">En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.</span><span class="sxs-lookup"><span data-stu-id="19e13-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="19e13-114">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="19e13-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="19e13-115">Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.</span><span class="sxs-lookup"><span data-stu-id="19e13-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="19e13-116">**Démarrer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="19e13-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="19e13-117">**Arrêter une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="19e13-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="19e13-118">**Supprimer une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="19e13-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="19e13-119">**Télécharger une capture de paquets**</span><span class="sxs-lookup"><span data-stu-id="19e13-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="19e13-120">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="19e13-120">Before you begin</span></span>

<span data-ttu-id="19e13-121">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="19e13-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="19e13-122">Une instance de l’Observateur réseau dans la région de hello souhaité toocreate une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="19e13-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="19e13-123">Une machine virtuelle avec les paquets hello capturer extension activée.</span><span class="sxs-lookup"><span data-stu-id="19e13-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e13-124">Capture des paquets nécessite une toobe de l’agent en cours d’exécution sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="19e13-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="19e13-125">Hello, l’Agent est installé en tant qu’extension.</span><span class="sxs-lookup"><span data-stu-id="19e13-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="19e13-126">Pour obtenir des instructions sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="19e13-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="19e13-127">Installer une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="19e13-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="19e13-128">Étape 1</span><span class="sxs-lookup"><span data-stu-id="19e13-128">Step 1</span></span>

<span data-ttu-id="19e13-129">Exécutez hello `azure vm extension set` agent de capture de paquet applet de commande tooinstall hello sur ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="19e13-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="19e13-130">Pour les machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="19e13-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="19e13-131">Pour les machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="19e13-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="19e13-132">Étape 2</span><span class="sxs-lookup"><span data-stu-id="19e13-132">Step 2</span></span>

<span data-ttu-id="19e13-133">tooensure qui hello agent est installé, exécutez hello `vm extension get` applet de commande et lui passer de groupe de ressources hello et nom d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="19e13-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="19e13-134">Vérifiez que hello résultant liste tooensure hello agent est installé.</span><span class="sxs-lookup"><span data-stu-id="19e13-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="19e13-135">Hello suivant l’exemple est un exemple de réponse hello en cours d’exécution`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="19e13-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="19e13-136">Démarrer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="19e13-136">Start a packet capture</span></span>

<span data-ttu-id="19e13-137">Une fois hello étapes précédentes terminées, l’agent de capture de paquets hello est installé sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="19e13-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="19e13-138">Étape 1</span><span class="sxs-lookup"><span data-stu-id="19e13-138">Step 1</span></span>

<span data-ttu-id="19e13-139">étape suivante de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="19e13-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="19e13-140">Cette variable est passée toohello `network watcher show` applet de commande à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="19e13-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="19e13-141">Étape 2</span><span class="sxs-lookup"><span data-stu-id="19e13-141">Step 2</span></span>

<span data-ttu-id="19e13-142">Récupérez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="19e13-142">Retrieve a storage account.</span></span> <span data-ttu-id="19e13-143">Ce compte de stockage est un fichier de capture de paquets hello toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="19e13-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="19e13-144">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="19e13-144">Step 3</span></span>

<span data-ttu-id="19e13-145">Filtres peuvent être des données hello toolimit utilisé qui sont stockées par la capture des paquets hello.</span><span class="sxs-lookup"><span data-stu-id="19e13-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="19e13-146">Hello exemple suivant configure une capture de paquets avec plusieurs filtres.</span><span class="sxs-lookup"><span data-stu-id="19e13-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="19e13-147">Hello tout d’abord trois filtres collecter le trafic TCP sortant uniquement à partir de l’adresse IP locale 10.0.0.3 toodestination ports 20, 80 et 443.</span><span class="sxs-lookup"><span data-stu-id="19e13-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="19e13-148">dernier filtre de Hello collecte uniquement le trafic UDP.</span><span class="sxs-lookup"><span data-stu-id="19e13-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="19e13-149">Plusieurs filtres peuvent être définis pour une même capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="19e13-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="19e13-150">Si vous utilisez une structure de filtre complexes, il est mieux toouse filtres comme une erreur de syntaxe de tooavoid fichier json.</span><span class="sxs-lookup"><span data-stu-id="19e13-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="19e13-151">Utilisez par exemple, l’indicateur de hello »-r » (au lieu de «-f ») et passez l’emplacement hello d’un fichier json contenant hello suivant filtres :</span><span class="sxs-lookup"><span data-stu-id="19e13-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="19e13-152">exemple suivant Hello est sortie de hello attendu de l’exécution de hello `network watcher packet-capture create` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="19e13-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="19e13-153">Obtenir une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="19e13-153">Get a packet capture</span></span>

<span data-ttu-id="19e13-154">En cours d’exécution hello `network watcher packet-capture show` applet de commande récupère l’état hello d’une capture de paquets en cours d’exécution ou terminé.</span><span class="sxs-lookup"><span data-stu-id="19e13-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="19e13-155">exemple Hello est sortie hello hello `network watcher packet-capture show` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="19e13-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="19e13-156">Hello exemple suivant est une fois la capture de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="19e13-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="19e13-157">Hello PacketCaptureStatus valeur avec un StopReason de TimeExceeded est arrêté.</span><span class="sxs-lookup"><span data-stu-id="19e13-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="19e13-158">Cette valeur indique que la capture des paquets hello a réussi et son exécution.</span><span class="sxs-lookup"><span data-stu-id="19e13-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="19e13-159">Arrêter une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="19e13-159">Stop a packet capture</span></span>

<span data-ttu-id="19e13-160">En exécutant hello `network watcher packet-capture stop` applet de commande, si une session de capture est en cours d’exécution, il est arrêté.</span><span class="sxs-lookup"><span data-stu-id="19e13-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="19e13-161">applet de commande Hello ne retourne pas de réponse lorsque s’exécutait sur une session de capture en cours d’exécution ou une session existante qui a déjà été arrêté.</span><span class="sxs-lookup"><span data-stu-id="19e13-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="19e13-162">Supprimer une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="19e13-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="19e13-163">Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="19e13-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="19e13-164">Télécharger une capture de paquets</span><span class="sxs-lookup"><span data-stu-id="19e13-164">Download a packet capture</span></span>

<span data-ttu-id="19e13-165">Une fois terminé, votre session de capture de paquets hello capture fichier peut être téléchargé tooblob tooa ou stockage local sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19e13-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="19e13-166">emplacement de stockage Hello de capture de paquets hello est définie lors de la création de la session de hello.</span><span class="sxs-lookup"><span data-stu-id="19e13-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="19e13-167">Un outil pratique de tooaccess ces fichiers de capture de compte de stockage tooa enregistré est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="19e13-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="19e13-168">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="19e13-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="19e13-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19e13-169">Next steps</span></span>

<span data-ttu-id="19e13-170">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="19e13-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="19e13-171">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="19e13-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
