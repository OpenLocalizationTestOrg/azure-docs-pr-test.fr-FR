---
title: "aaaTroubleshoot passerelle de réseau virtuel Azure et des connexions - Azure CLI 1.0 | Documents Microsoft"
description: "Cette page explique comment toouse hello Observateur de réseau Azure dépanner Azure CLI 1.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>Résoudre des problèmes liés à la passerelle de réseau virtuel et aux connexions Azure à l’aide de l’Azure CLI 1.0 d’Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portail](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure. Il permet notamment de résoudre les problèmes liés aux ressources. Résolution des problèmes de ressource peuvent être appelée via le portail de hello, PowerShell, CLI ou API REST. Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.

Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux. 

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](/network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Vue d'ensemble

Résolution des problèmes de ressource permet de hello résoudre les problèmes qui surviennent avec les connexions et les passerelles de réseau virtuel. Lorsqu’une demande est faite tooresource résolution des problèmes, les journaux sont en cours interrogées et inspecté. Lors de l’inspection est terminée, les résultats de hello sont retournés. Demandes de résolution des problèmes sont à long terme des ressources des demandes, ce qui peut prendre plusieurs minutes tooreturn un résultat. journaux de Hello à partir de la résolution des problèmes sont stockés dans un conteneur sur un compte de stockage spécifié.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Récupérer une connexion de passerelle de réseau virtuel

Dans cet exemple, la résolution des problèmes liés aux ressources s’effectue sur une connexion. Vous pouvez également la transférer à une passerelle de réseau virtuel. Hello applet de commande suivante répertorie les connexions vpn hello dans un groupe de ressources.

```azurecli
azure network vpn-connection list -g resourceGroupName
```

Vous pouvez également exécuter hello commande toosee les connexions hello dans un abonnement.

```azurecli
azure network vpn-connection list -s subscription
```

Une fois que vous avez nom hello de connexion de hello, vous pouvez exécuter cette commande tooget son Id de ressource :

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>Créez un compte de stockage.

Résolution des problèmes de ressource retourne des données concernant la santé de ressource de hello hello, il enregistre également les journaux tooa stockage compte toobe révisé. À cette étape, nous créons un compte de stockage. Si vous disposez déjà d’un compte de stockage existant, vous pouvez l’utiliser.

1. Créer le compte de stockage hello

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. Obtenir les clés de compte de stockage hello

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. Créer un conteneur de hello

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Procéder à la résolution des problèmes liés aux ressources Network Watcher

Résolution de ressources avec hello `network watcher troubleshoot` applet de commande. Nous transmettons le groupe de ressources hello applet de commande hello et Id de compte de stockage hello hello hello nom Hello Observateur réseau, hello Id de connexion de hello, Bonjour chemin d’accès toohello blob toostore Bonjour résoudre les résultats dans.

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

Une fois que vous exécutez applet de commande hello, Observateur réseau passe en revue hello tooverify hello contrôle d’intégrité. Il retourne les résultats hello toohello shell et stocke les journaux des résultats de hello hello compte de stockage spécifié.

## <a name="understanding-hello-results"></a>Présentation des résultats de hello

texte d’action Hello fournit des indications générales sur la façon dont tooresolve hello problème. Si le problème de hello peut entreprendre une action, un lien est fourni avec des instructions supplémentaires. Dans le cas de hello où il n’existe pas d’instructions supplémentaires, réponse de hello fournit hello url tooopen un cas de prise en charge.  Pour plus d’informations sur les propriétés de hello de réponse de hello et ce qui est inclus, visitez [vue d’ensemble de la résolution de l’Observateur réseau](network-watcher-troubleshoot-overview.md)

Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). L’explorateur de stockage peut aussi être utilisé. Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)

## <a name="next-steps"></a>Étapes suivantes

Si les paramètres ont été modifiés qu’arrêter la connectivité VPN, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui peuvent être en question.
