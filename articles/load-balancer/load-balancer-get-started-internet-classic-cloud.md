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
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="a0240-103">Création d'un équilibreur de charge accessible sur Internet pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="a0240-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0240-104">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="a0240-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="a0240-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0240-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="a0240-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a0240-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="a0240-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a0240-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a0240-108">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique.</span><span class="sxs-lookup"><span data-stu-id="a0240-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a0240-109">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="a0240-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="a0240-110">Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="a0240-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="a0240-111">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="a0240-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="a0240-112">Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a0240-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="a0240-113">Services de cloud computing sont automatiquement configurés avec un équilibrage de charge et peuvent être personnalisés via le modèle de service hello.</span><span class="sxs-lookup"><span data-stu-id="a0240-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="a0240-114">Créer un équilibreur de charge à l’aide du fichier de définition de service hello</span><span class="sxs-lookup"><span data-stu-id="a0240-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="a0240-115">Vous pouvez tirer parti des hello Azure SDK pour .NET 2.5 tooupdate votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="a0240-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="a0240-116">Paramètres de point de terminaison pour les services cloud sont effectuées dans hello [définition de service](https://msdn.microsoft.com/library/azure/gg557553.aspx) fichier .csdef.</span><span class="sxs-lookup"><span data-stu-id="a0240-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="a0240-117">Hello suivant montre comment un fichier servicedefinition.csdef pour un déploiement de cloud est configuré :</span><span class="sxs-lookup"><span data-stu-id="a0240-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="a0240-118">Vérification de l’extrait de code hello pour le fichier de .csdef hello généré par un déploiement de cloud computing, vous pouvez voir hello point de terminaison externe configuré toouse ports HTTP sur le port 10000 et 10001 10002.</span><span class="sxs-lookup"><span data-stu-id="a0240-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="a0240-119">Vérifier l'état d'intégrité de l'équilibrage de charge pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="a0240-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="a0240-120">Hello Voici un exemple d’une sonde d’intégrité :</span><span class="sxs-lookup"><span data-stu-id="a0240-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="a0240-121">Hello équilibrage de charge combine hello les informations de point de terminaison hello et hello de hello sonde toocreate une URL sous forme de hello de `http://{DIP of VM}:80/Probe.aspx` qui peut être utilisé tooquery hello intégrité service de hello.</span><span class="sxs-lookup"><span data-stu-id="a0240-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="a0240-122">Hello service détecte les sondes périodiques à partir de hello même adresse IP.</span><span class="sxs-lookup"><span data-stu-id="a0240-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="a0240-123">Il s’agit de demande de sonde d’intégrité hello provenant d’hôte hello du nœud de hello où hello virtual machine est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a0240-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="a0240-124">service de Hello a toorespond avec un code d’état HTTP 200 pour tooassume d’équilibrage de charge hello que hello service est intègre.</span><span class="sxs-lookup"><span data-stu-id="a0240-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="a0240-125">Tout autre état HTTP du code (par exemple 503) directement prend hello machine virtuelle hors rotation.</span><span class="sxs-lookup"><span data-stu-id="a0240-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="a0240-126">définition de sonde Hello contrôle également la fréquence hello de sonde de hello.</span><span class="sxs-lookup"><span data-stu-id="a0240-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="a0240-127">Dans notre cas ci-dessus, équilibrage de charge hello est détection de point de terminaison hello toutes les 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="a0240-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="a0240-128">Si aucune réponse positive n’est reçue pour 10 secondes (deux intervalles de sondage), sonde de hello est supposée vers le bas, et extrait de la machine virtuelle de hello rotation.</span><span class="sxs-lookup"><span data-stu-id="a0240-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="a0240-129">De même, si le service de hello est hors rotation et une réponse positive est reçue, le service de hello est remis toorotation immédiatement.</span><span class="sxs-lookup"><span data-stu-id="a0240-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="a0240-130">Si le service de hello fluctue entre intègre corrects et incorrects, équilibrage de charge hello peut décider toodelay hello réintroduction de toorotation différé du service hello jusqu'à ce qu’il a été sain pour un nombre d’analyses par sondage.</span><span class="sxs-lookup"><span data-stu-id="a0240-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="a0240-131">Vérifiez le schéma de définition du service hello pour hello [sonde d’intégrité](https://msdn.microsoft.com/library/azure/jj151530.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a0240-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0240-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0240-132">Next steps</span></span>

[<span data-ttu-id="a0240-133">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="a0240-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="a0240-134">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="a0240-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a0240-135">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="a0240-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

