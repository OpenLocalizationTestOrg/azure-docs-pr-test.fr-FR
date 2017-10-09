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
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a>Gérer les captures de paquets avec Azure Network Watcher à l’aide d’Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [API REST Azure](network-watcher-packet-capture-manage-rest.md)

Capture de paquets de l’Observateur réseau vous permet de toocreate capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel. Les filtres sont fournies pour tooensure de session de capture hello que vous capturer le trafic hello seulement que vous le souhaitez. Capture des paquets permet des anomalies de réseau toodiagnose proactive et réactive. Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore. En étant en mesure de tooremotely déclencheur paquet captures, cette fonctionnalité facilite hello de l’exécution d’une capture de paquets sur l’ordinateur souhaité hello, qui permet d’économiser un temps précieux et manuellement.

Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.

Cet article passe en revue hello différentes tâches de gestion qui sont actuellement disponibles pour la capture des paquets.

- [**Démarrer une capture de paquets**](#start-a-packet-capture)
- [**Arrêter une capture de paquets**](#stop-a-packet-capture)
- [**Supprimer une capture de paquets**](#delete-a-packet-capture)
- [**Télécharger une capture de paquets**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Avant de commencer

Cet article suppose que vous avez hello suivant des ressources :

- Une instance de l’Observateur réseau dans la région de hello souhaité toocreate une capture de paquets
- Une machine virtuelle avec les paquets hello capturer extension activée.

> [!IMPORTANT]
> Capture des paquets nécessite une toobe de l’agent en cours d’exécution sur l’ordinateur virtuel de hello. Hello, l’Agent est installé en tant qu’extension. Pour obtenir des instructions sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](../virtual-machines/windows/extensions-features.md).

## <a name="install-vm-extension"></a>Installer une extension de machine virtuelle

### <a name="step-1"></a>Étape 1

Exécutez hello `azure vm extension set` agent de capture de paquet applet de commande tooinstall hello sur ordinateur virtuel hello.

Pour les machines virtuelles Windows :

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

Pour les machines virtuelles Linux :

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a>Étape 2

tooensure qui hello agent est installé, exécutez hello `vm extension get` applet de commande et lui passer de groupe de ressources hello et nom d’ordinateur virtuel. Vérifiez que hello résultant liste tooensure hello agent est installé.

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

Hello suivant l’exemple est un exemple de réponse hello en cours d’exécution`azure vm extension get`

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a>Démarrer une capture de paquets

Une fois hello étapes précédentes terminées, l’agent de capture de paquets hello est installé sur l’ordinateur virtuel de hello.

### <a name="step-1"></a>Étape 1

étape suivante de Hello est instance de l’Observateur réseau tooretrieve hello. Cette variable est passée toohello `network watcher show` applet de commande à l’étape 4.

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a>Étape 2

Récupérez un compte de stockage. Ce compte de stockage est un fichier de capture de paquets hello toostore utilisé.

```azurecli
azure storage account list
```

### <a name="step-3"></a>Étape 3 :

Filtres peuvent être des données hello toolimit utilisé qui sont stockées par la capture des paquets hello. Hello exemple suivant configure une capture de paquets avec plusieurs filtres.  Hello tout d’abord trois filtres collecter le trafic TCP sortant uniquement à partir de l’adresse IP locale 10.0.0.3 toodestination ports 20, 80 et 443.  dernier filtre de Hello collecte uniquement le trafic UDP.

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

Plusieurs filtres peuvent être définis pour une même capture de paquets. Si vous utilisez une structure de filtre complexes, il est mieux toouse filtres comme une erreur de syntaxe de tooavoid fichier json. Utilisez par exemple, l’indicateur de hello »-r » (au lieu de «-f ») et passez l’emplacement hello d’un fichier json contenant hello suivant filtres :

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


exemple suivant Hello est sortie de hello attendu de l’exécution de hello `network watcher packet-capture create` applet de commande.

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

## <a name="get-a-packet-capture"></a>Obtenir une capture de paquets

En cours d’exécution hello `network watcher packet-capture show` applet de commande récupère l’état hello d’une capture de paquets en cours d’exécution ou terminé.

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

exemple Hello est sortie hello hello `network watcher packet-capture show` applet de commande. Hello exemple suivant est une fois la capture de hello est terminée. Hello PacketCaptureStatus valeur avec un StopReason de TimeExceeded est arrêté. Cette valeur indique que la capture des paquets hello a réussi et son exécution.

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

## <a name="stop-a-packet-capture"></a>Arrêter une capture de paquets

En exécutant hello `network watcher packet-capture stop` applet de commande, si une session de capture est en cours d’exécution, il est arrêté.

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> applet de commande Hello ne retourne pas de réponse lorsque s’exécutait sur une session de capture en cours d’exécution ou une session existante qui a déjà été arrêté.

## <a name="delete-a-packet-capture"></a>Supprimer une capture de paquets

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> Suppression d’une capture de paquets ne supprime pas le fichier hello hello compte de stockage.

## <a name="download-a-packet-capture"></a>Télécharger une capture de paquets

Une fois terminé, votre session de capture de paquets hello capture fichier peut être téléchargé tooblob tooa ou stockage local sur hello machine virtuelle. emplacement de stockage Hello de capture de paquets hello est définie lors de la création de la session de hello. Un outil pratique de tooaccess ces fichiers de capture de compte de stockage tooa enregistré est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/

Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)

Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
