---
title: "Limites et quotas de mise à l’échelle dans votre laboratoire Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment mettre à l’échelle un laboratoire dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="6a531-103">Limites et quotas de mise à l’échelle dans votre laboratoire Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6a531-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="6a531-104">Lorsque vous travaillez dans DevTest Labs, vous pouvez remarquer un certain nombre de limites par défaut qui s’appliquent à certaines ressources Azure, ce qui peut affecter le service DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="6a531-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="6a531-105">Ces limites sont appelées **quotas**.</span><span class="sxs-lookup"><span data-stu-id="6a531-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="6a531-106">Le service DevTest Labs n’impose aucun quota.</span><span class="sxs-lookup"><span data-stu-id="6a531-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="6a531-107">Les quotas que vous pouvez rencontrer sont les contraintes par défaut de l’abonnement Azure global.</span><span class="sxs-lookup"><span data-stu-id="6a531-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="6a531-108">Vous pouvez utiliser chaque ressource Azure jusqu’à ce que vous ayez atteint son quota.</span><span class="sxs-lookup"><span data-stu-id="6a531-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="6a531-109">Chaque abonnement a des quotas distincts et l’utilisation est suivie par abonnement.</span><span class="sxs-lookup"><span data-stu-id="6a531-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="6a531-110">Par exemple, chaque abonnement possède un quota par défaut de 20 cœurs.</span><span class="sxs-lookup"><span data-stu-id="6a531-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="6a531-111">Par conséquent, si vous créez des machines virtuelles dans votre laboratoire avec quatre cœurs, vous pouvez uniquement créer cinq machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a531-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="6a531-112">La page [Abonnement Azure et limites de service](https://docs.microsoft.com/azure/azure-subscription-service-limits) dresse la liste des quotas les plus courants pour les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6a531-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="6a531-113">Les ressources couramment utilisées dans un laboratoire, et pour lesquelles vous pouvez rencontrer des quotas, incluent les noyaux de machine virtuelle, les adresses IP publiques, l’interface réseau, les disques managés, l’attribution de rôle RBAC et les circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6a531-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="6a531-114">Voir votre utilisation et les quotas</span><span class="sxs-lookup"><span data-stu-id="6a531-114">View your usage and quotas</span></span>
<span data-ttu-id="6a531-115">Ces étapes vous montrent comment afficher les quotas actuels de votre abonnement pour des ressources Azure spécifiques, ainsi que le pourcentage utilisé pour chaque quota.</span><span class="sxs-lookup"><span data-stu-id="6a531-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="6a531-116">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6a531-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="6a531-117">Sélectionnez **Autres services**, puis **Facturation** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="6a531-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="6a531-118">Dans le panneau Facturation, sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="6a531-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="6a531-119">Sélectionnez **Utilisation + quotas**.</span><span class="sxs-lookup"><span data-stu-id="6a531-119">Select **Usage + quotas**.</span></span>

   ![Bouton Utilisation et quotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="6a531-121">Le panneau Utilisation + quotas s’affiche. Il répertorie les différentes ressources disponibles dans cet abonnement et le pourcentage de quota utilisé par la ressource.</span><span class="sxs-lookup"><span data-stu-id="6a531-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Quotas et utilisation](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="6a531-123">Demander plus de ressources dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="6a531-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="6a531-124">Si vous atteignez le plafond d’un quota, la limite par défaut d’une ressource dans un abonnement peut être augmentée jusqu’à une limite maximale, comme décrit dans [Abonnement Azure et limites de service](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="6a531-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="6a531-125">Ces étapes vous montrent comment demander une augmentation du quota au moyen du [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6a531-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="6a531-126">Sélectionnez **Autres services**, **Facturation**, puis **Utilisation + quotas**.</span><span class="sxs-lookup"><span data-stu-id="6a531-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="6a531-127">Dans le panneau Utilisation + quotas, sélectionnez le bouton **Demander une augmentation**.</span><span class="sxs-lookup"><span data-stu-id="6a531-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![Bouton Demander une augmentation](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="6a531-129">Pour finaliser et envoyer la demande, remplissez les informations requises sous les trois onglets du formulaire **Nouvelle demande de support**.</span><span class="sxs-lookup"><span data-stu-id="6a531-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![Formulaire Demander une augmentation](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="6a531-131">La page [Understanding Azure Limits and Increases (Présentation des limites et des augmentations Azure)](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) vous explique plus en détail comment contacter le support Azure pour demander une augmentation du quota.</span><span class="sxs-lookup"><span data-stu-id="6a531-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="6a531-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a531-132">Next steps</span></span>
* <span data-ttu-id="6a531-133">Explorez la [Galerie de modèles de démarrage rapide d’Azure Resource Manager DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="6a531-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
