---
title: "aaaAzure exemple de Script CLI - nom d’hôte hello Get, les ports et les clés de Cache Redis Azure | Documents Microsoft"
description: "Exemple de Script CLI Azure - le nom d’hôte de Get hello, les ports et les clés d’une instance de Cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Obtenir le nom d’hôte hello, les ports et les clés Azure Redis cache

Dans ce scénario, vous découvrez utilisation des clés, les ports et le nom d’hôte de tooretrieve hello instance de Cache Redis Azure tooconnect tooan.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant le nom d’hôte de commandes tooretrieve hello, les clés et les ports d’une instance de Cache Redis Azure. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Récupérer les détails d’une instance du Cache Redis Azure. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Récupérer les clés d’accès pour une instance du Cache Redis Azure. |


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de Cache Redis Azure Bonjour [documentation du Cache Redis Azure](../cli-samples.md).
