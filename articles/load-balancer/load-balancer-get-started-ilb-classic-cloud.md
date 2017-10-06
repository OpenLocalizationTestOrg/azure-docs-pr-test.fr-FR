---
title: "aaaCreate un équilibreur de charge interne pour les Services de Cloud Azure | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide de PowerShell dans le modèle de déploiement classique de hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Prise en main de la création d’un équilibreur de charge interne (Classic) pour les services cloud

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Services cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Configurer l’équilibreur de charge interne pour les services cloud

L’équilibreur de charge interne est pris en charge pour les machines virtuelles et les services cloud. Un point de terminaison de programme d’équilibrage de charge interne créé dans un service cloud qui est en dehors d’un réseau virtuel régional est accessibles uniquement dans le service de cloud computing hello.

configuration d’équilibrage de charge interne Hello a toobe défini pendant la création de hello du premier déploiement de hello dans le service cloud hello, comme indiqué dans l’exemple hello ci-dessous.

> [!IMPORTANT]
> Étapes d’un hello toorun requis ci-dessous est toohave un réseau virtuel déjà créé pour le déploiement de cloud hello. Vous devez hello réseau virtuel nom et le sous-réseau nom toocreate hello équilibrage de charge interne.

### <a name="step-1"></a>Étape 1

Ouvrez le fichier de configuration de service hello (.cscfg) pour votre déploiement de cloud dans Visual Studio et ajouter hello suivant hello de toocreate section équilibrage de charge interne sous hello dernière »`</Role>`« élément de configuration du réseau hello.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Vous allez ajouter les valeurs hello pour hello réseau configuration fichier tooshow aspect. Dans l’exemple de hello, supposons que vous avez créé un réseau virtuel appelé « test_vnet » avec un sous-réseau 10.0.0.0/24 appelé test_subnet et une adresse IP statique 10.0.0.4. équilibrage de charge Hello sera nommé testLB.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Pour plus d’informations sur le schéma de programme d’équilibrage de charge hello, consultez [équilibrage de charge ajouter](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Étape 2

Modifier hello service (.csdef) de définition fichier tooadd points de terminaison toohello équilibrage de charge interne. moment de Hello une instance de rôle est créée, le fichier de définition de service hello ajoute toohello d’instances de rôle hello équilibrage de charge interne.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Suite hello les mêmes valeurs à partir de l’exemple hello ci-dessus, vous allez ajouter le fichier de définition de service hello valeurs toohello.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

le trafic réseau de Hello sera équilibrée à l’aide d’équilibrage de charge hello testLB utilise le port 80 pour les demandes entrantes, envoi tooworker instances de rôle également sur le port 80.

## <a name="next-steps"></a>Étapes suivantes

[Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source](load-balancer-distribution-mode.md)

[Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

