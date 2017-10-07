---
title: "aaaCreate une côté Internet l’équilibrage de charge - Azure PowerShell classique | Documents Microsoft"
description: "Découvrez comment toocreate une connecté à Internet l’équilibrage de charge en mode classique, à l’aide de PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Création d'un équilibreur de charge accessible sur Internet (classique) dans PowerShell

> [!div class="op_single_selector"]
> * [portail Azure Classic](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique. Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure. Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article. Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Configurer de l'équilibrage de charge à l'aide de PowerShell

tooset d’un équilibrage de charge à l’aide de powershell, suivez les étapes de hello ci-dessous :

1. Si vous n’avez jamais utilisé Azure PowerShell, consultez [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez les instructions de hello tous les toohello de façon hello fin toosign dans Azure et sélectionnez votre abonnement.
2. Après avoir créé un ordinateur virtuel, vous pouvez utiliser tooadd d’applets de commande PowerShell un ordinateur virtuel de charge équilibrage tooa dans hello même service cloud.

Bonjour exemple suivant, vous allez ajouter un jeu d’équilibrage de charge appelé « batterie de serveurs » toocloud ordinateurs « mytestcloud » (ou myctestcloud.cloudapp.net), ajout de points de terminaison hello pour hello toovirtual d’équilibrage de charge de service nommé « web1 » et « web2 ». équilibrage de charge Hello reçoit le trafic réseau sur le port 80 et équilibre la charge entre les machines virtuelles de hello définis par le point de terminaison local hello (dans ce cas le port 80) à l’aide de TCP.

### <a name="step-1"></a>Étape 1

Créer un point de terminaison à charge équilibrée web1 « hello première machine virtuelle »

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Étape 2

Créer un autre point de terminaison pour hello deuxième machine virtuelle « web2 » à l’aide de hello même charger nom du jeu d’équilibrage

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Supprimez une machine virtuelle de l’équilibreur de charge

Vous pouvez utiliser Remove-AzureEndpoint tooremove un point de terminaison de machine virtuelle à partir de l’équilibrage de charge hello

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également [commencer par créer un équilibrage de charge interne](load-balancer-get-started-ilb-classic-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement de trafic réseau d’équilibrage de charge spécifique.

Si votre application doit tookeep connexions actives pour les serveurs situés derrière un équilibreur de charge, vous pouvez en savoir plus sur [les paramètres de délai d’expiration TCP pour un équilibrage de charge des temps d’inactivité](load-balancer-tcp-idle-timeout.md). Il aidera toolearn sur le comportement des connexions inactives lorsque vous utilisez l’équilibrage de charge Azure.
