---
title: "Présentation de l’équilibrage de charge accessible sur Internet | Microsoft Docs"
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
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="e647d-104">Présentation de l’équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="e647d-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="e647d-105">L’équilibreur de charge Azure mappe l’adresse IP publique et le numéro de port du trafic entrant à l’adresse IP privée et au numéro de port de la machine virtuelle (et inversement) pour le trafic de réponse de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e647d-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="e647d-106">Les règles d’équilibrage de charge vous permettent de distribuer des types spécifiques de trafic entre plusieurs machines virtuelles ou services.</span><span class="sxs-lookup"><span data-stu-id="e647d-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="e647d-107">Par exemple, vous pouvez répartir la charge du trafic des requêtes Web sur plusieurs serveurs ou rôles Web.</span><span class="sxs-lookup"><span data-stu-id="e647d-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="e647d-108">Pour un service cloud contenant des instances de rôles Web ou de rôles de travail, vous pouvez définir un point de terminaison public dans le fichier de définition de service (.csdef).</span><span class="sxs-lookup"><span data-stu-id="e647d-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="e647d-109">Le fichier *servicedefinition.csdef* contient la configuration de point de terminaison et lorsque vous avez plusieurs instances de rôle pour un déploiement de rôle Web ou de travail, l’équilibrage de charge sera configuré pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e647d-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="e647d-110">Pour ajouter des instances à votre déploiement de cloud, vous devez modifier le nombre d’instances dans le fichier de configuration de service (.csfg).</span><span class="sxs-lookup"><span data-stu-id="e647d-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="e647d-111">La figure suivante présente un point de terminaison à charge équilibrée pour le trafic Web partagé entre trois machines virtuelles pour les ports TCP public et privé 80.</span><span class="sxs-lookup"><span data-stu-id="e647d-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="e647d-112">Celles-ci sont incluses dans un jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="e647d-112">These three virtual machines are in a load-balanced set.</span></span>

![exemple d’équilibrage de charge public](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="e647d-114">Figure 1 : point de terminaison d’équilibrage de charge pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="e647d-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="e647d-115">Lorsque les clients Internet envoient des demandes de page Web à l’adresse IP publique du service cloud sur le port TCP 80, Azure Load Balancer distribue les demandes entre les trois machines virtuelles du jeu à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="e647d-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="e647d-116">Des informations supplémentaires sur l’algorithme de l’équilibreur de charge sont disponibles sur la [page de présentation de l’équilibreur de charge](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="e647d-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="e647d-117">Par défaut, Azure Load Balancer répartit le trafic réseau équitablement sur plusieurs instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e647d-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="e647d-118">Vous pouvez également configurer l’affinité de session. Pour plus d’informations, consultez [Mode de distribution d’équilibrage de charge](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="e647d-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e647d-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e647d-119">Next steps</span></span>

<span data-ttu-id="e647d-120">Vous pouvez consulter des informations sur [l’équilibreur de charge interne](load-balancer-internal-overview.md) pour mieux comprendre quel équilibreur de charge convient le mieux à votre déploiement de cloud.</span><span class="sxs-lookup"><span data-stu-id="e647d-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="e647d-121">Vous pouvez également [commencer par créer un équilibreur de charge avec accès par Internet](load-balancer-get-started-internet-arm-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement spécifique de trafic réseau d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e647d-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="e647d-122">Si votre application doit maintenir des connexions actives pour les serveurs situés derrière un équilibreur de charge, vous pouvez obtenir plus d’informations sur les [paramètres de délai d'expiration TCP pour un équilibrage de charge](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="e647d-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="e647d-123">Ainsi, vous en saurez plus sur le comportement d’une connexion inactive lorsque vous utilisez l'équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="e647d-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
