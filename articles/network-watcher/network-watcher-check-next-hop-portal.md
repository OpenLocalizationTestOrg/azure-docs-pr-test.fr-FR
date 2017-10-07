---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - portail Azure | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver le hello de type de tronçon suivant est et l’adresse ip à l’aide de tronçon suivant hello portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide du portail de hello

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST Azure](network-watcher-check-next-hop-rest.md)

Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée. Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau. scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.

## <a name="scenario"></a>Scénario

scénario de Hello abordée dans cet article utilise toofind de tronçon suivant out de type hello du saut suivant et l’adresse IP pour une ressource. toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).

Dans ce scénario, vous allez :

* Récupérer le saut suivant de hello à partir d’un ordinateur virtuel.

## <a name="get-next-hop"></a>Obtenir le tronçon suivant

### <a name="step-1"></a>Étape 1

Accédez tooyour des ressources de l’Observateur réseau Bonjour portail Azure.

### <a name="step-2"></a>Étape 2

Cliquez sur **de tronçon suivant** hello volet de navigation, sélectionnez hello virtual machine et interface réseau, remplir hello les IP source et de destination, puis cliquez sur hello **de tronçon suivant** bouton.

> [!NOTE]
> Tronçon suivant requiert que les ressources d’ordinateur virtuel hello est allouée toorun.

![Vue d’ensemble de l’écran d’obtention du tronçon suivant][1]

### <a name="step-3"></a>Étape 3 :

Une fois la tâche hello est terminée, les résultats de hello sont fournies. Hello d’adresse IP et le type du saut suivant de périphérique hello est, s’affiche. Hello tableau suivant montre les valeurs retournées disponible hello dans le portail de hello.

**Type de tronçon suivant**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Aucun

Si un itinéraire personnalisé a été utilisé tooroute ce trafic, itinéraire défini par l’utilisateur de hello (UDR) est également affiché avec les résultats hello.

![Résultats d’obtention du tronçon suivant][2]

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














