---
title: "Affichage des tendances de coût de laboratoire mensuelles estimées dans Azure DevTest Labs | Microsoft Docs"
description: "En savoir plus sur le graphique des tendances des coûts mensuels estimés Azure DevTest Labs."
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
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="12115-103">Affichage des tendances de coût de laboratoire mensuelles estimées dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="12115-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="12115-104">La fonctionnalité de gestion des coûts de DevTest Labs vous permet de suivre le coût de votre labo.</span><span class="sxs-lookup"><span data-stu-id="12115-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="12115-105">Cet article explique comment utiliser le graphique **Tendance des coûts mensuels estimés** pour afficher le coût estimé à ce jour pour le mois civil en cours, ainsi que le coût projeté pour la fin du mois civil en cours.</span><span class="sxs-lookup"><span data-stu-id="12115-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="12115-106">Dans cet article, vous allez apprendre à afficher le graphique de tendances de coût mensuelles estimées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12115-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="12115-107">Affichage du graphique Tendance des coûts mensuels estimés</span><span class="sxs-lookup"><span data-stu-id="12115-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="12115-108">Pour afficher le graphique Tendance des coûts mensuels estimés, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="12115-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="12115-109">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="12115-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="12115-110">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="12115-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="12115-111">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="12115-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="12115-112">Dans le panneau du laboratoire, sélectionnez **Paramètres de coût**.</span><span class="sxs-lookup"><span data-stu-id="12115-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="12115-113">Dans le panneau **Paramètres de coût**, sélectionnez **Tendances de coût de laboratoire**.</span><span class="sxs-lookup"><span data-stu-id="12115-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="12115-114">La capture d'écran suivante montre un exemple de graphique de coûts.</span><span class="sxs-lookup"><span data-stu-id="12115-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Graphique de coûts](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="12115-116">La valeur **Coût estimé** est le coût estimé à ce jour pour le mois calendaire en cours.</span><span class="sxs-lookup"><span data-stu-id="12115-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="12115-117">Le **Coût projeté** est le coût estimé pour le mois calendaire entier, calculé à l’aide du coût du laboratoire lors des cinq derniers jours.</span><span class="sxs-lookup"><span data-stu-id="12115-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="12115-118">Les montants des coûts sont arrondis à l’entier supérieur.</span><span class="sxs-lookup"><span data-stu-id="12115-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="12115-119">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="12115-119">For example:</span></span> 

* <span data-ttu-id="12115-120">5,01 est arrondi à 6</span><span class="sxs-lookup"><span data-stu-id="12115-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="12115-121">5,50 est arrondi à 6</span><span class="sxs-lookup"><span data-stu-id="12115-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="12115-122">5,99 est arrondi à 6</span><span class="sxs-lookup"><span data-stu-id="12115-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="12115-123">Comme indiqué au-dessus du graphique, les coûts que vous voyez dans le graphique sont les coûts *estimés* avec les tarifs de l’offre [Paiement à l'utilisation](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="12115-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="12115-124">Par ailleurs, les éléments suivants ne sont *pas* inclus dans le calcul des coûts :</span><span class="sxs-lookup"><span data-stu-id="12115-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="12115-125">Les abonnements CSP et Dreamspark ne sont pas pris en charge. En effet, Azure DevTest Labs utilise les [API de facturation Azure](../billing/billing-usage-rate-card-overview.md) pour calculer les coûts de laboratoire, et celles-ci ne prennent pas en charge les abonnements CSP et Dreamspark.</span><span class="sxs-lookup"><span data-stu-id="12115-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="12115-126">Les tarifs de votre offre.</span><span class="sxs-lookup"><span data-stu-id="12115-126">Your offer rates.</span></span> <span data-ttu-id="12115-127">Actuellement, nous ne sommes pas en mesure d'utiliser les tarifs de votre offre (affichés sous votre abonnement) que vous avez négociés avec Microsoft ou les partenaires Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12115-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="12115-128">Nous utilisons les tarifs du paiement à l'utilisation.</span><span class="sxs-lookup"><span data-stu-id="12115-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="12115-129">Vos taxes</span><span class="sxs-lookup"><span data-stu-id="12115-129">Your taxes</span></span>
* <span data-ttu-id="12115-130">Vos remises</span><span class="sxs-lookup"><span data-stu-id="12115-130">Your discounts</span></span>
* <span data-ttu-id="12115-131">Votre devise de facturation.</span><span class="sxs-lookup"><span data-stu-id="12115-131">Your billing currency.</span></span> <span data-ttu-id="12115-132">Actuellement, le coût du labo s'affiche uniquement dans la devise USD.</span><span class="sxs-lookup"><span data-stu-id="12115-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="12115-133">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="12115-133">Related blog posts</span></span>
* [<span data-ttu-id="12115-134">Two more things to keep your cost on track in DevTest Labs (Deux autres astuces pour maîtriser vos coûts dans DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="12115-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="12115-135">Why Cost Thresholds? (Pourquoi définir des seuils de coût ?)</span><span class="sxs-lookup"><span data-stu-id="12115-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="12115-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12115-136">Next steps</span></span>
<span data-ttu-id="12115-137">Voici quelques possibilités d’opérations pour la suite :</span><span class="sxs-lookup"><span data-stu-id="12115-137">Here are some things to try next:</span></span>

* <span data-ttu-id="12115-138">[Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md) : apprenez à définir les différentes stratégies utilisées pour gérer l’utilisation de votre laboratoire et de ses machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="12115-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="12115-139">[Créer une image personnalisée](devtest-lab-create-template.md) : quand vous créez une machine virtuelle, vous spécifiez une base, qui peut être soit une image personnalisée, soit une image Marketplace.</span><span class="sxs-lookup"><span data-stu-id="12115-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="12115-140">Cet article explique comment créer une image personnalisée à partir d’un fichier VHD.</span><span class="sxs-lookup"><span data-stu-id="12115-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="12115-141">[Configurer des images Marketplace](devtest-lab-configure-marketplace-images.md) : DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="12115-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="12115-142">Cet article explique comment spécifier, le cas échéant, les images Azure Marketplace pouvant être utilisées lors de la création de machines virtuelles dans un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="12115-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="12115-143">[Créer une machine virtuelle dans un laboratoire](devtest-lab-add-vm-with-artifacts.md) : montre comment créer une machine virtuelle à partir d’une image de base (personnalisée ou Marketplace) et comment utiliser des artefacts dans votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="12115-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

