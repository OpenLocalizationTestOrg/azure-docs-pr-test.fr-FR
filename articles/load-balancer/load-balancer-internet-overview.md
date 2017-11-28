---
title: "aaaInternet faisant face à la vue d’ensemble du programme d’équilibrage de charge | Documents Microsoft"
description: "Présentation de l’équilibrage de charge accessible sur Internet et ses fonctionnalités. Fonctionnement de l’équilibrage de charge pour Azure avec des machines virtuelles et des services cloud."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="6c60d-104">Présentation de l’équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="6c60d-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="6c60d-105">Équilibrage de charge Azure mappe hello publique IP adresse et numéro de port du trafic toohello privé IP adresse et le port numéro entrant de machine virtuelle de hello et vice versa, pour le trafic de réponse hello à partir de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6c60d-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="6c60d-106">Règles d’équilibrage de charge permettent de toodistribute des types spécifiques de trafic entre plusieurs machines virtuelles ou services.</span><span class="sxs-lookup"><span data-stu-id="6c60d-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="6c60d-107">Par exemple, vous pouvez répartir la charge hello du trafic de demande web sur plusieurs serveurs web ou les rôles web.</span><span class="sxs-lookup"><span data-stu-id="6c60d-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="6c60d-108">Pour un service cloud qui contient des instances de rôles web ou des rôles de travail, vous pouvez définir un point de terminaison public dans le fichier de définition (.csdef) de service hello.</span><span class="sxs-lookup"><span data-stu-id="6c60d-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="6c60d-109">Hello *servicedefinition.csdef* fichier contient la configuration de point de terminaison hello et lorsque vous avez plusieurs instances de rôle pour un déploiement de rôle web ou de travail, équilibrage de charge hello sera installé pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="6c60d-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="6c60d-110">déploiement de cloud computing Hello moyen tooadd instances tooyour change hello nombre d’instances sur le fichier de configuration de service hello (.csfg).</span><span class="sxs-lookup"><span data-stu-id="6c60d-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="6c60d-111">Hello figure suivante illustre un point de terminaison avec équilibrage de charge pour le trafic web est partagé entre trois machines virtuelles pour hello public et privé le port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="6c60d-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="6c60d-112">Celles-ci sont incluses dans un jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="6c60d-112">These three virtual machines are in a load-balanced set.</span></span>

![exemple d’équilibrage de charge public](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="6c60d-114">Figure 1 : point de terminaison d’équilibrage de charge pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="6c60d-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="6c60d-115">Lorsque les clients Internet envoient des demandes de page web toohello une adresse IP publique du service de cloud hello sur le port TCP 80, hello équilibrage de charge Azure distribue les requêtes de hello entre hello trois machines virtuelles dans le jeu d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="6c60d-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="6c60d-116">Pour plus d’informations sur les algorithmes d’équilibrage de charge, consultez hello [page de vue d’ensemble d’équilibrage de charge](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="6c60d-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="6c60d-117">Par défaut, Azure Load Balancer répartit le trafic réseau équitablement sur plusieurs instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c60d-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="6c60d-118">Vous pouvez également configurer l’affinité de session. Pour plus d’informations, consultez [Mode de distribution d’équilibrage de charge](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="6c60d-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c60d-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c60d-119">Next steps</span></span>

<span data-ttu-id="6c60d-120">En savoir plus sur [équilibreur de charge interne](load-balancer-internal-overview.md) toobetter comprendre quel équilibreur de charge est plus adaptée à votre déploiement de cloud.</span><span class="sxs-lookup"><span data-stu-id="6c60d-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="6c60d-121">Vous pouvez également [commencer par créer un équilibreur de charge avec accès par Internet](load-balancer-get-started-internet-arm-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement spécifique de trafic réseau d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6c60d-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="6c60d-122">Si votre application doit tookeep connexions actives pour les serveurs situés derrière un équilibreur de charge, vous pouvez en savoir plus sur [les paramètres de délai d’expiration TCP pour un équilibrage de charge des temps d’inactivité](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="6c60d-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="6c60d-123">Il aidera toolearn sur le comportement des connexions inactives lorsque vous utilisez l’équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="6c60d-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
