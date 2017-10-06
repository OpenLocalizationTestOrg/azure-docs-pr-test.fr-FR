---
title: "connectivité aaaCheck avec l’Observateur réseau de Azure - portail Azure | Documents Microsoft"
description: "Cette page explique comment vérifier des toouse connectivité avec l’Observateur réseau à l’aide de hello portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Vérifiez la connectivité avec l’Observateur réseau de Azure à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> - [Portail](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [API REST Azure](network-watcher-connectivity-rest.md)

Découvrez comment toouse connectivité tooverify si une connexion TCP directe à partir d’un tooa de machine virtuelle donné du point de terminaison peut être établie.

## <a name="before-you-begin"></a>Avant de commencer

Cet article suppose que vous avez hello suivant des ressources :

* Une instance de l’Observateur réseau dans la région de hello souhaité toocheck connectivité.

* Machines virtuelles toocheck la connectivité avec.

> [!IMPORTANT]
> La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`. Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Vérifiez la connectivité tooa virtual machine

Cet exemple vérifie l’ordinateur virtuel de destination de tooa connectivité via le port 80.

Accédez tooyour Observateur réseau et cliquez sur **vérification de la connectivité (version préliminaire)**. Sélectionnez la connectivité de toocheck hello machine virtuelle à partir de. Bonjour **Destination** section Choisissez **sélectionnez une machine virtuelle** et choisir la machine virtuelle appropriée de hello et tootest de port.

Une fois que vous cliquez sur **vérifier**, connectivité hello entre les machines virtuelles de hello sur port hello spécifié sont vérifiées. Dans l’exemple de hello, hello destination machine virtuelle est inaccessible, une liste de sauts sont affichés.

![Consulter les résultats de la connectivité d’une machine virtuelle][1]

## <a name="check-remote-endpoint-connectivity"></a>Vérifier la connectivité du point de terminaison distant

connectivité de hello toocheck et le point de terminaison distant latence tooa, choisissez hello **spécifier manuellement** case Bonjour **Destination** , d’entrée hello url et le port de hello et cliquez sur **vérifier** .  Cette opération est utilisée pour les points de terminaison distants comme des sites web et des points de terminaison de stockage.

![Consulter les résultats de la connectivité d’un site web][2]

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)

Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
