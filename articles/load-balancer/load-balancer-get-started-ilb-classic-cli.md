---
title: "aaaCreate un interne l’équilibrage de charge - CLI d’Azure classic | Documents Microsoft"
description: "Découvrez comment un équilibreur de charge interne à l’aide de toocreate hello CLI d’Azure dans le modèle de déploiement classique de hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Prise en main la création d’un équilibreur de charge interne (classique) à l’aide de hello CLI d’Azure

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Services cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate un équilibreur de charge interne défini pour les machines virtuelles

toocreate un équilibreur de charge interne défini et hello serveurs qui y enverront leur tooit le trafic, vous devez procéder comme suit de hello :

1. Créer une instance d’interne l’équilibrage de charge qui sera le point de terminaison hello d’entrant trafic toobe équilibrée entre les serveurs hello d’un jeu d’équilibrage de la charge.
2. Ajoutez les machines virtuelles toohello qui recevront le trafic entrant de hello correspondantes des points de terminaison.
3. Configurez les serveurs hello qui enverront hello trafic toobe à charge équilibrée toosend leur trafic toohello adresse IP virtuelle (VIP) de l’instance d’équilibrage de charge interne hello.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Créer par étapes un équilibreur de charge interne à l’aide de l’interface de ligne de commande CLI

Ce guide montre comment toocreate un équilibreur de charge interne selon hello scénario ci-dessus.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **configuration azure mode** mode commande tooswitch tooclassic, comme indiqué ci-dessous.

    ```azurecli
    azure config mode asm
    ```

    Sortie attendue :

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Création d'un point de terminaison et d'un jeu d'équilibrage de charge

scénario de Hello suppose hello des machines virtuelles « DB1 » et « DB2 » dans un service cloud appelé « mytestcloud ». Ces deux machines virtuelles utilisent un réseau virtuel appelé mon « testvnet » avec un sous-réseau « sous-réseau-1 ».

Ce guide créera un jeu d'équilibrage de charge en utilisant le port 1433 comme port privé et 1433 comme port local.

Il s’agit d’un scénario courant où vous avez des machines virtuelles SQL sur l’utilisation de back-end hello que ne sera pas exposé un serveurs de base de données de charge interne équilibrage tooguarantee hello directement à l’aide d’une adresse IP publique.

### <a name="step-1"></a>Étape 1

Créer un jeu d’équilibrage de charge interne avec `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Pour plus d'informations, consultez `azure service internal-load-balancer --help` .

Vous pouvez vérifier les propriétés de l’équilibrage de charge interne hello à l’aide de la commande hello `azure service internal-load-balancer list` *nom du service cloud*.

Cet exemple suit un exemple de sortie de hello :

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Étape 2

Vous configurez équilibreur de charge interne hello définir lorsque vous ajoutez le premier point de terminaison hello. Vous allez associer hello point de terminaison, de machines virtuelles et de sonde port toohello équilibreur de charge interne défini dans cette étape.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Étape 3 :

Vérifiez la configuration de hello d’équilibrage de charge avec `azure vm show` *nom d’ordinateur virtuel*

```azurecli
azure vm show DB1
```

résultat de Hello sera :

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Création d'un point de terminaison de Bureau à distance pour une machine virtuelle

Vous pouvez créer un trafic réseau de tooforward point de terminaison Bureau à distance à partir d’un port local tooa de port public pour un ordinateur virtuel spécifique à l’aide de `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Suppression d’une machine virtuelle de l’équilibreur de charge

Vous pouvez supprimer un ordinateur virtuel à partir d’un équilibreur de charge interne défini par la suppression du point de terminaison hello associé. Une fois que le point de terminaison hello est supprimé, hello virtual machine n’appartiennent à équilibrage de charge toohello définie plus.

À l’aide d’exemple hello ci-dessus, vous pouvez supprimer le point de terminaison de hello créé pour l’ordinateur virtuel « DB1 » à partir de l’équilibreur de charge interne « ilbset » en à l’aide de la commande hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Pour plus d'informations, consultez `azure vm endpoint --help` .

## <a name="next-steps"></a>Étapes suivantes

[Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source](load-balancer-distribution-mode.md)

[Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
