---
title: "aaaTroubleshoot passerelle de réseau virtuel Azure et des connexions - PowerShell | Documents Microsoft"
description: "Cette page explique comment résoudre des toouse hello Observateur de réseau Azure les applet de commande PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions par le biais de PowerShell d’Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portail](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure. Il permet notamment de résoudre les problèmes liés aux ressources. Résolution des problèmes de ressource peuvent être appelée via le portail de hello, PowerShell, CLI ou API REST. Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Vue d'ensemble

Résolution des problèmes de ressource permet de hello résoudre les problèmes qui surviennent avec les connexions et les passerelles de réseau virtuel. Lorsqu’une demande est faite tooresource résolution des problèmes, les journaux sont en cours interrogées et inspecté. Lors de l’inspection est terminée, les résultats de hello sont retournés. Demandes de résolution des problèmes sont à long terme des ressources des demandes, ce qui peut prendre plusieurs minutes tooreturn un résultat. journaux de Hello à partir de la résolution des problèmes sont stockés dans un conteneur sur un compte de stockage spécifié.

## <a name="troubleshoot-a-gateway-or-connection"></a>Résoudre les problèmes de passerelle ou de connexion

1. Accédez toohello [portail Azure](https://portal.azure.com) et cliquez sur **réseau** > **Observateur réseau** > **VPN Diagnostics**
2. Sélectionnez un **Abonnement**, un **Groupe de ressources** et un **Emplacement**.
3. Résolution des problèmes de ressource retourne des données concernant la santé de ressource de hello hello. Elle enregistre également compte de stockage tooa journaux appropriés toobe révisé. Cliquez sur **compte de stockage** tooselect un compte de stockage.
4. Sur hello **comptes de stockage** panneau, sélectionnez un compte de stockage existant ou cliquez sur **+ compte de stockage** toocreate un nouveau.
5. Sur hello **conteneurs** panneau, choisissez un conteneur existant ou cliquez sur **+ conteneur** toocreate un nouveau conteneur. Lorsque vous avez terminé, cliquez sur **Sélectionner**.
6. Sélectionnez tootroubleshoot de ressources de passerelle et la connexion hello et cliquez sur **démarrer la résolution des problèmes**

Si plusieurs ressources sont sélectionnées, la résolution des problèmes s’exécute simultanément sur les ressources de passerelle. Il ne peut pas être exécuté sur une connexion, et il est associé à la passerelle à hello même temps. Il est recommandé de passerelles de tootroubleshoot tout d’abord que la résolution des problèmes de connexion sont un processus plus long. Pendant l’exécution de Diagnostics du VPN sur un Bonjour ressource **état de résolution des problèmes** colonne présentent l’état de **en cours d’exécution**

Lorsque vous avez terminé, les modifications de colonnes état hello trop**sain** ou **défectueux**.

![résolution des problèmes terminée][2]

## <a name="understanding-hello-results"></a>Présentation des résultats de hello

Bonjour **détails** section de la fenêtre hello, hello **état** onglet affiche l’état de hello hello la résolution des problèmes dernière exécution sur les ressources hello sélectionné. Résultats du diagnostic de dernière hello sont les indiqué xx minutes après la dernière exécution de hello.

|Propriété  |Description  |
|---------|---------|
|Ressource     | Une ressource toohello du lien.        |
|Chemin de stockage     |  Compte de stockage toohello de chemin d’accès et conteneur qui contiennent les journaux hello (si les sont produites au cours de hello exécuter). Ce paramètre n’est pas conservé quand vous quittez le portail de hello.        |
|Résumé     | Résumé de l’intégrité des ressources hello.        |
|Détails     | Obtenir des informations détaillées sur l’intégrité des ressources hello.        |
|Dernière exécution     | Hello hello d’heure de dernière résolution des problèmes de temps a été exécuté.        |


Hello **Action** onglet fournit des indications générales sur la façon dont tooresolve hello problème. Si le problème de hello peut entreprendre une action, un lien est fourni avec des instructions supplémentaires. Dans le cas de hello où il n’existe pas d’instructions supplémentaires, réponse de hello fournit hello url tooopen un cas de prise en charge.  Pour plus d’informations sur les propriétés de hello de réponse de hello et ce qui est inclus, visitez [vue d’ensemble de la résolution de l’Observateur réseau](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Étapes suivantes

Si les paramètres ont été modifiés qu’arrêter la connectivité VPN, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui peuvent être en question.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
