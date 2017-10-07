---
title: "Vérifiez que le trafic d’aaaVerify le transfert IP de l’Observateur réseau Azure - portail Azure | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Vérifiez si le trafic est autorisé ou refusé tooor à partir d’une machine virtuelle avec IP flux vérifier un composant de l’Observateur de réseau Azure

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST Azure](network-watcher-check-ip-flow-verify-rest.md)


Vérifiez que les flux IP est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel. la validation de Hello peut être exécutée pour le trafic entrant ou sortant. Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou une autre ressource. Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau. Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau ou une instance existante de l’Observateur réseau. scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.

## <a name="scenario"></a>Scénario

Ce scénario utilise tooverify d’IP de flux de vérifier si un ordinateur virtuel peut communiquer avec l’ordinateur de tooanother sur le port 443. Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic. toolearn en savoir plus sur l’IP de flux de vérifier, visitez [flux vérifier la vue d’ensemble IP](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Exécuter la vérification des flux IP

Accédez tooyour Observateur réseau et cliquez sur **les flux IP vérifier**. Sélectionnez hello virtual machine et l’interface réseau du trafic tooverify à partir de. Entrez les informations de filtrage supplémentaires, puis cliquez sur **Vérifier**.

Une fois que vous cliquez sur **vérifier**, flux hello en fonction de critères hello vous avez fourni est activée. résultat de Hello est **accès autorisé** ou **accès refusé**. Si l’accès est refusé, hello du groupe de sécurité réseau (NSG) et règle de sécurité qui bloquent le trafic est fournie. Si le refus hello du trafic est le comportement attendu, règle de hello a réussi.

> [!NOTE]
> Les flux IP vérifier requiert que la ressource de machine virtuelle hello est allouée.

Comme vous pouvez voir à partir de hello suivant l’image, le trafic HTTPS hello a été autorisé.

![vue d’ensemble Vérification du flux IP][1]

Comme indiqué dans hello suivant l’image, le trafic est modifié tooinbound et hello entrant too123 de port modifié. Le trafic est maintenant refusé, le message de salutation « Accès refusé » est fourni avec hello groupe et sécurité règle de sécurité réseau qui refusent le trafic de hello.

![résultats du flux IP][2]

## <a name="next-steps"></a>Étapes suivantes

Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont définis.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













