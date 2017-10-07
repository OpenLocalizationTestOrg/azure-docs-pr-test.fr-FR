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
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="c705c-103">Création d'un équilibreur de charge accessible sur Internet (classique) dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="c705c-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c705c-104">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="c705c-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="c705c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c705c-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="c705c-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c705c-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="c705c-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="c705c-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="c705c-108">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique.</span><span class="sxs-lookup"><span data-stu-id="c705c-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="c705c-109">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="c705c-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="c705c-110">Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="c705c-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="c705c-111">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c705c-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="c705c-112">Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c705c-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="c705c-113">Configurer de l'équilibrage de charge à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c705c-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="c705c-114">tooset d’un équilibrage de charge à l’aide de powershell, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c705c-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="c705c-115">Si vous n’avez jamais utilisé Azure PowerShell, consultez [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez les instructions de hello tous les toohello de façon hello fin toosign dans Azure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="c705c-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="c705c-116">Après avoir créé un ordinateur virtuel, vous pouvez utiliser tooadd d’applets de commande PowerShell un ordinateur virtuel de charge équilibrage tooa dans hello même service cloud.</span><span class="sxs-lookup"><span data-stu-id="c705c-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="c705c-117">Bonjour exemple suivant, vous allez ajouter un jeu d’équilibrage de charge appelé « batterie de serveurs » toocloud ordinateurs « mytestcloud » (ou myctestcloud.cloudapp.net), ajout de points de terminaison hello pour hello toovirtual d’équilibrage de charge de service nommé « web1 » et « web2 ».</span><span class="sxs-lookup"><span data-stu-id="c705c-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="c705c-118">équilibrage de charge Hello reçoit le trafic réseau sur le port 80 et équilibre la charge entre les machines virtuelles de hello définis par le point de terminaison local hello (dans ce cas le port 80) à l’aide de TCP.</span><span class="sxs-lookup"><span data-stu-id="c705c-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="c705c-119">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c705c-119">Step 1</span></span>

<span data-ttu-id="c705c-120">Créer un point de terminaison à charge équilibrée web1 « hello première machine virtuelle »</span><span class="sxs-lookup"><span data-stu-id="c705c-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="c705c-121">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c705c-121">Step 2</span></span>

<span data-ttu-id="c705c-122">Créer un autre point de terminaison pour hello deuxième machine virtuelle « web2 » à l’aide de hello même charger nom du jeu d’équilibrage</span><span class="sxs-lookup"><span data-stu-id="c705c-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="c705c-123">Supprimez une machine virtuelle de l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="c705c-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="c705c-124">Vous pouvez utiliser Remove-AzureEndpoint tooremove un point de terminaison de machine virtuelle à partir de l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="c705c-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="c705c-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c705c-125">Next steps</span></span>

<span data-ttu-id="c705c-126">Vous pouvez également [commencer par créer un équilibrage de charge interne](load-balancer-get-started-ilb-classic-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement de trafic réseau d’équilibrage de charge spécifique.</span><span class="sxs-lookup"><span data-stu-id="c705c-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="c705c-127">Si votre application doit tookeep connexions actives pour les serveurs situés derrière un équilibreur de charge, vous pouvez en savoir plus sur [les paramètres de délai d’expiration TCP pour un équilibrage de charge des temps d’inactivité](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="c705c-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="c705c-128">Il aidera toolearn sur le comportement des connexions inactives lorsque vous utilisez l’équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="c705c-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
