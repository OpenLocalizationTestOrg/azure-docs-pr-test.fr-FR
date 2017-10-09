---
title: "équilibrage de charge aaaCreate une connecté à Internet pour les services de cloud computing Azure | Documents Microsoft"
description: "Découvrez comment toocreate une connecté à Internet l’équilibrage de charge dans le modèle de déploiement classique pour les services de cloud"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Création d'un équilibreur de charge accessible sur Internet pour les services cloud

> [!div class="op_single_selector"]
> * [Portail Azure Classic](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique. Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure. Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article. Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).

Services de cloud computing sont automatiquement configurés avec un équilibrage de charge et peuvent être personnalisés via le modèle de service hello.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Créer un équilibreur de charge à l’aide du fichier de définition de service hello

Vous pouvez tirer parti des hello Azure SDK pour .NET 2.5 tooupdate votre service cloud. Paramètres de point de terminaison pour les services cloud sont effectuées dans hello [définition de service](https://msdn.microsoft.com/library/azure/gg557553.aspx) fichier .csdef.

Hello suivant montre comment un fichier servicedefinition.csdef pour un déploiement de cloud est configuré :

Vérification de l’extrait de code hello pour le fichier de .csdef hello généré par un déploiement de cloud computing, vous pouvez voir hello point de terminaison externe configuré toouse ports HTTP sur le port 10000 et 10001 10002.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Vérifier l'état d'intégrité de l'équilibrage de charge pour les services cloud

Hello Voici un exemple d’une sonde d’intégrité :

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Hello équilibrage de charge combine hello les informations de point de terminaison hello et hello de hello sonde toocreate une URL sous forme de hello de `http://{DIP of VM}:80/Probe.aspx` qui peut être utilisé tooquery hello intégrité service de hello.

Hello service détecte les sondes périodiques à partir de hello même adresse IP. Il s’agit de demande de sonde d’intégrité hello provenant d’hôte hello du nœud de hello où hello virtual machine est en cours d’exécution. service de Hello a toorespond avec un code d’état HTTP 200 pour tooassume d’équilibrage de charge hello que hello service est intègre. Tout autre état HTTP du code (par exemple 503) directement prend hello machine virtuelle hors rotation.

définition de sonde Hello contrôle également la fréquence hello de sonde de hello. Dans notre cas ci-dessus, équilibrage de charge hello est détection de point de terminaison hello toutes les 5 secondes. Si aucune réponse positive n’est reçue pour 10 secondes (deux intervalles de sondage), sonde de hello est supposée vers le bas, et extrait de la machine virtuelle de hello rotation. De même, si le service de hello est hors rotation et une réponse positive est reçue, le service de hello est remis toorotation immédiatement. Si le service de hello fluctue entre intègre corrects et incorrects, équilibrage de charge hello peut décider toodelay hello réintroduction de toorotation différé du service hello jusqu'à ce qu’il a été sain pour un nombre d’analyses par sondage.

Vérifiez le schéma de définition du service hello pour hello [sonde d’intégrité](https://msdn.microsoft.com/library/azure/jj151530.aspx) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

