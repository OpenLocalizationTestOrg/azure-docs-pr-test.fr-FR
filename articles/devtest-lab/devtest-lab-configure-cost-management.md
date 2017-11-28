---
title: "aaaView hello mensuelles estimé du lab tendance du coût dans Azure DevTest Labs | Documents Microsoft"
description: "En savoir plus sur le graphique de tendances de coût estimé mensuel hello Azure DevTest Labs."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="25a84-103">Vue hello mensuelles estimé du lab tendance du coût dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="25a84-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="25a84-104">fonctionnalité de gestion des coûts Hello de DevTest Labs permet de suivre le coût de hello de votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="25a84-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="25a84-105">Cet article explique comment toouse hello **tendance du coût estimé mensuel** graphique tooview hello estimé coût-to-date du mois civil actuel et hello coût prévu de fin de mois pour hello mois actuel.</span><span class="sxs-lookup"><span data-stu-id="25a84-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="25a84-106">Dans cet article, vous découvrez comment tooview hello graphique de tendances de coût estimé mensuel Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25a84-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="25a84-107">Affichage graphique de tendance du coût estimé mensuel hello</span><span class="sxs-lookup"><span data-stu-id="25a84-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="25a84-108">tooview hello graphique de tendance du coût estimé mensuel, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="25a84-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="25a84-109">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="25a84-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="25a84-110">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="25a84-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="25a84-111">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="25a84-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="25a84-112">Dans le panneau de hello lab, sélectionnez **paramètres de coût**.</span><span class="sxs-lookup"><span data-stu-id="25a84-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="25a84-113">Sur du laboratoire hello **coût paramètres** panneau, sélectionnez **tendance du coût Lab**.</span><span class="sxs-lookup"><span data-stu-id="25a84-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="25a84-114">Hello capture d’écran suivante montre un exemple d’un graphique de coût.</span><span class="sxs-lookup"><span data-stu-id="25a84-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Graphique de coûts](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="25a84-116">Hello **coût estimé** valeur est hello estimé coût-to-date du mois civil actuel.</span><span class="sxs-lookup"><span data-stu-id="25a84-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="25a84-117">Hello **coût prévu** est hello coût estimé de hello entière mois actuel, calculée à l’aide coût de laboratoire hello pour hello précédentes cinq jours.</span><span class="sxs-lookup"><span data-stu-id="25a84-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="25a84-118">montants de coût Hello sont arrondis toohello nombre entier supérieur.</span><span class="sxs-lookup"><span data-stu-id="25a84-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="25a84-119">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="25a84-119">For example:</span></span> 

* <span data-ttu-id="25a84-120">5.01 arrondit too6</span><span class="sxs-lookup"><span data-stu-id="25a84-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="25a84-121">5.50 arrondit too6</span><span class="sxs-lookup"><span data-stu-id="25a84-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="25a84-122">5.99 arrondit too6</span><span class="sxs-lookup"><span data-stu-id="25a84-122">5.99 rounds up too6</span></span>

<span data-ttu-id="25a84-123">Comme il indique au-dessus du graphique de hello, les coûts de hello vous voyez dans le graphique de hello sont *estimé* coûte à l’aide de [paiement à l’utilisation](https://azure.microsoft.com/offers/ms-azr-0003p/) offrent des taux.</span><span class="sxs-lookup"><span data-stu-id="25a84-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="25a84-124">En outre, hello Voici les *pas* inclus dans le calcul du coût de hello :</span><span class="sxs-lookup"><span data-stu-id="25a84-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="25a84-125">Abonnements CSP et Dreamspark sont actuellement pas prises en charge Azure DevTest Labs utilise hello [API facturation Azure](../billing/billing-usage-rate-card-overview.md) lab de hello toocalculate coût, qui ne prend pas en charge les abonnements Dreamspark ou de fournisseur de services cryptographiques.</span><span class="sxs-lookup"><span data-stu-id="25a84-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="25a84-126">Les tarifs de votre offre.</span><span class="sxs-lookup"><span data-stu-id="25a84-126">Your offer rates.</span></span> <span data-ttu-id="25a84-127">Actuellement, nous ne sommes pas en mesure de toouse vos tarifs offre (affichées sous votre abonnement) que vous avez négocié avec Microsoft ou Microsoft partenaires.</span><span class="sxs-lookup"><span data-stu-id="25a84-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="25a84-128">Nous utilisons les tarifs du paiement à l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="25a84-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="25a84-129">Vos taxes</span><span class="sxs-lookup"><span data-stu-id="25a84-129">Your taxes</span></span>
* <span data-ttu-id="25a84-130">Vos remises</span><span class="sxs-lookup"><span data-stu-id="25a84-130">Your discounts</span></span>
* <span data-ttu-id="25a84-131">Votre devise de facturation.</span><span class="sxs-lookup"><span data-stu-id="25a84-131">Your billing currency.</span></span> <span data-ttu-id="25a84-132">Coût de laboratoire hello est affichée uniquement dans la devise USD.</span><span class="sxs-lookup"><span data-stu-id="25a84-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="25a84-133">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="25a84-133">Related blog posts</span></span>
* [<span data-ttu-id="25a84-134">Deux tookeep choses plus votre coût de la piste dans DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="25a84-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="25a84-135">Why Cost Thresholds? (Pourquoi définir des seuils de coût ?)</span><span class="sxs-lookup"><span data-stu-id="25a84-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="25a84-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="25a84-136">Next steps</span></span>
<span data-ttu-id="25a84-137">Voici certaines choses tootry suivant :</span><span class="sxs-lookup"><span data-stu-id="25a84-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="25a84-138">[Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md) -en savoir comment tooset hello différentes stratégies de toogovern comment votre laboratoire et ses ordinateurs virtuels sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="25a84-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="25a84-139">[Créer une image personnalisée](devtest-lab-create-template.md) : quand vous créez une machine virtuelle, vous spécifiez une base, qui peut être soit une image personnalisée, soit une image Marketplace.</span><span class="sxs-lookup"><span data-stu-id="25a84-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="25a84-140">Cet article explique comment toocreate personnalisé de l’image à partir d’un fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="25a84-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="25a84-141">[Configurer des images Marketplace](devtest-lab-configure-marketplace-images.md) : DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="25a84-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="25a84-142">Cet article explique comment toospecify qui, le cas échéant, les images Azure Marketplace peuvent être utilisés lors de la création de machines virtuelles dans un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="25a84-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="25a84-143">[Créer une machine virtuelle dans un laboratoire](devtest-lab-add-vm-with-artifacts.md) -illustre comment toocreate une machine virtuelle à partir d’une image de base (soit personnalisé ou Marketplace) et comment toowork des artefacts dans votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="25a84-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

