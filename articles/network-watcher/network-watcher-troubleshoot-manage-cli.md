---
title: "aaaTroubleshoot connexions - Azure CLI 2.0 et la passerelle de réseau virtuel Azure | Documents Microsoft"
description: "Cette page explique comment toouse hello Observateur de réseau Azure dépanner Azure CLI 2.0"
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
ms.openlocfilehash: 389e86f247722412a1d0e2e722dbf80bb7cff291
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-20"></a>Résoudre des problèmes liés à la passerelle de réseau virtuel et aux connexions à l’aide de l’Azure CLI 2.0 d’Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portail](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure. Il permet notamment de résoudre les problèmes liés aux ressources. Résolution des problèmes de ressource peuvent être appelée via le portail de hello, PowerShell, CLI ou API REST. Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.

Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.

les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Vue d'ensemble

Résolution des problèmes de ressource permet de hello résoudre les problèmes qui surviennent avec les connexions et les passerelles de réseau virtuel. Lorsqu’une demande est faite tooresource résolution des problèmes, les journaux sont en cours interrogées et inspecté. Lors de l’inspection est terminée, les résultats de hello sont retournés. Demandes de résolution des problèmes sont à long terme des ressources des demandes, ce qui peut prendre plusieurs minutes tooreturn un résultat. journaux de Hello à partir de la résolution des problèmes sont stockés dans un conteneur sur un compte de stockage spécifié.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Récupérer une connexion de passerelle de réseau virtuel

Dans cet exemple, la résolution des problèmes liés aux ressources s’effectue sur une connexion. Vous pouvez également la transférer à une passerelle de réseau virtuel. Hello applet de commande suivante répertorie les connexions vpn hello dans un groupe de ressources.

```azurecli
az network vpn-connection list --resource-group resourceGroupName
```

Une fois que vous avez nom hello de connexion de hello, vous pouvez exécuter cette commande tooget son Id de ressource :

```azurecli
az network vpn-connection show --resource-group resourceGroupName --ids vpnConnectionIds
```

## <a name="create-a-storage-account"></a>Créez un compte de stockage.

Résolution des problèmes de ressource retourne des données concernant la santé de ressource de hello hello, il enregistre également les journaux tooa stockage compte toobe révisé. À cette étape, nous créons un compte de stockage. Si vous disposez déjà d’un compte de stockage existant, vous pouvez l’utiliser.

1. Créer le compte de stockage hello

    ```azurecli
    az storage account create --name storageAccountName --location westcentralus --resource-group resourceGroupName --sku Standard_LRS
    ```

1. Obtenir les clés de compte de stockage hello

    ```azurecli
    az storage account keys list --resource-group resourcegroupName --account-name storageAccountName
    ```

1. Créer un conteneur de hello

    ```azurecli
    az storage container create --account-name storageAccountName --account-key {storageAccountKey} --name logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Procéder à la résolution des problèmes liés aux ressources Network Watcher

Résolution de ressources avec hello `az network watcher troubleshooting` applet de commande. Nous transmettons le groupe de ressources hello applet de commande hello et Id de compte de stockage hello hello hello nom Hello Observateur réseau, hello Id de connexion de hello, Bonjour chemin d’accès toohello blob toostore Bonjour résoudre les résultats dans.

```azurecli
az network watcher troubleshooting start --resource-group resourceGroupName --resource resourceName --resource-type {vnetGateway/vpnConnection} --storage-account storageAccountName  --storage-path https://{storageAccountName}.blob.core.windows.net/{containerName}
```

Une fois que vous exécutez applet de commande hello, Observateur réseau passe en revue hello tooverify hello contrôle d’intégrité. Il retourne les résultats hello toohello shell et stocke les journaux des résultats de hello hello compte de stockage spécifié.

## <a name="understanding-hello-results"></a>Présentation des résultats de hello

texte d’action Hello fournit des indications générales sur la façon dont tooresolve hello problème. Si le problème de hello peut entreprendre une action, un lien est fourni avec des instructions supplémentaires. Dans le cas de hello où il n’existe pas d’instructions supplémentaires, réponse de hello fournit hello url tooopen un cas de prise en charge.  Pour plus d’informations sur les propriétés de hello de réponse de hello et ce qui est inclus, visitez [vue d’ensemble de la résolution de l’Observateur réseau](network-watcher-troubleshoot-overview.md)

Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). L’explorateur de stockage peut aussi être utilisé. Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)

## <a name="next-steps"></a>Étapes suivantes

Si les paramètres ont été modifiés qu’arrêter la connectivité VPN, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui peuvent être en question.
