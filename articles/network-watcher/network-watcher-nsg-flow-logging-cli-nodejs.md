---
title: "aaaManage flux de groupe de sécurité réseau se connecte avec l’Observateur réseau de Azure - Azure CLI 1.0 | Documents Microsoft"
description: "Cette page explique le fonctionnement des journaux dans l’Observateur réseau de Azure avec Azure CLI 1.0 toomanage flux de groupe de sécurité réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a>Configuration des journaux des flux de groupe de sécurité réseau avec Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Journaux du groupe de sécurité réseau de flux sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau. Ces flux de journaux est écrits au format json et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.

Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux. Network Watcher utilise actuellement Azure CLI 1.0 pour la prise en charge d’interface CLI.

## <a name="register-insights-provider"></a>Inscription du fournisseur Insights

Dans l’ordre pour le flux de journalisation toowork hello avec succès, **Microsoft.Insights** fournisseur doit être enregistré. Si vous n’êtes pas sûr si hello **Microsoft.Insights** fournisseur est inscrit, hello exécution de script suivant.

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a>Activer les journaux des flux de groupe de sécurité réseau

les journaux de flux de tooenable commande Hello est présenté dans hello l’exemple suivant :

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a>Désactiver les journaux des flux de groupe de sécurité réseau

Hello utilisation suivant des journaux de flux toodisable exemple :

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a>Télécharger un journal de flux

emplacement de stockage Hello d’un journal de flux est définie lors de la création. Un tooaccess outil pratique ces compte de stockage de journaux enregistrés tooa est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/

Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Pour plus d’informations sur la structure hello du journal de hello visitez [journal vue d’ensemble des flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec les outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
