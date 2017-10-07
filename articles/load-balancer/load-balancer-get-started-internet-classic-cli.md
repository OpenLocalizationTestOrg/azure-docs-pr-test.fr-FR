---
title: "aaaCreate une côté Internet l’équilibrage de charge - CLI d’Azure classic | Documents Microsoft"
description: "Découvrez comment toocreate un équilibrage de charge exposés à Internet à l’aide de modèle de déploiement classique hello CLI d’Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a>Commencer à créer un Internet faisant face à l’équilibrage de charge (classiques) Bonjour CLI d’Azure

> [!div class="op_single_selector"]
> * [portail Azure Classic](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique. Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure. Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article. Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a>Création par étapes d’un équilibreur de charge accessible sur Internet à l’aide de l’interface de ligne de commande CLI

Ce guide montre comment toocreate un équilibrage de charge d’Internet selon hello scénario ci-dessus.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **configuration azure mode** mode commande tooswitch tooclassic, comme indiqué ci-dessous.

    ```azurecli
    azure config mode asm
    ```

    Sortie attendue :

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Création d'un point de terminaison et d'un jeu d'équilibrage de charge

scénario de Hello suppose que les ordinateurs virtuels hello « web1 » et « web2 » ont été créés.
Ce guide crée un ensemble d’équilibreurs de charge à l’aide du port 80 comme port public et du port 80 comme port local. Un port de la sonde est également configuré sur le port 80 et équilibrage de charge nommé hello définie « lbset ».

### <a name="step-1"></a>Étape 1

Créer le premier point de terminaison hello et à l’aide de l’équilibrage de charge `azure network vm endpoint create` pour l’ordinateur virtuel « web1 ».

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a>Étape 2

Ajoutez un deuxième ensemble d’équilibrage de charge de l’ordinateur virtuel « web2 » toohello.

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a>Étape 3 :

Vérifiez la configuration de hello d’équilibrage de charge avec `azure vm show` .

```azurecli
azure vm show web1
```

résultat de Hello sera :

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Création d'un point de terminaison de Bureau à distance pour une machine virtuelle

Vous pouvez créer un trafic réseau de tooforward point de terminaison Bureau à distance à partir d’un port local tooa de port public pour un ordinateur virtuel spécifique à l’aide de `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Suppression d’une machine virtuelle de l’équilibreur de charge

Vous avez toohello de point de terminaison associé toodelete hello jeu d’équilibrage de charge de la machine virtuelle de hello. Une fois que le point de terminaison hello est supprimé, équilibrage de charge toohello définie plus n’appartient pas hello virtual machine.

Avec exemple hello ci-dessus, vous pouvez supprimer le point de terminaison hello créé pour l’ordinateur virtuel « web1 » à partir de l’équilibrage de charge « lbset » à l’aide de la commande hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> Vous pouvez Explorer plusieurs options toomanage points de terminaison à l’aide de la commande hello`azure vm endpoint --help`

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
