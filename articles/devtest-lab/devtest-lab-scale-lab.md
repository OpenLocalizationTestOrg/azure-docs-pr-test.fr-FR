---
title: aaaScale quotas et limites dans votre laboratoire dans Azure DevTest Labs | Documents Microsoft
description: "Découvrez comment tooscale un laboratoire dans Azure DevTest Labs"
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="bf526-103">Limites et quotas de mise à l’échelle dans votre laboratoire Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bf526-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="bf526-104">Lorsque vous travaillez dans DevTest Labs, vous pouvez remarquer qu’il existe certaine toosome de limites par défaut des ressources Azure, ce qui peuvent affecter les services de DevTest Labs hello.</span><span class="sxs-lookup"><span data-stu-id="bf526-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="bf526-105">Ces limites sont visées tooas **quotas**.</span><span class="sxs-lookup"><span data-stu-id="bf526-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="bf526-106">Hello service de DevTest Labs n’impose des quotas.</span><span class="sxs-lookup"><span data-stu-id="bf526-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="bf526-107">Des quotas, que vous pouvez rencontrer sont contraintes par défaut de hello abonnement global Azure.</span><span class="sxs-lookup"><span data-stu-id="bf526-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="bf526-108">Vous pouvez utiliser chaque ressource Azure jusqu’à ce que vous ayez atteint son quota.</span><span class="sxs-lookup"><span data-stu-id="bf526-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="bf526-109">Chaque abonnement a des quotas distincts et l’utilisation est suivie par abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf526-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="bf526-110">Par exemple, chaque abonnement possède un quota par défaut de 20 cœurs.</span><span class="sxs-lookup"><span data-stu-id="bf526-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="bf526-111">Par conséquent, si vous créez des machines virtuelles dans votre laboratoire avec quatre cœurs, vous pouvez uniquement créer cinq machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bf526-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="bf526-112">[Abonnement Azure et les limites de Service](https://docs.microsoft.com/azure/azure-subscription-service-limits) répertorie certaines des quotas plus courants de hello pour les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="bf526-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="bf526-113">Hello plus couramment utilisés dans un laboratoire de ressources, et pour lequel vous pouvez rencontrer quotas, incluent cœurs de l’ordinateur virtuel, les adresses IP publiques, interface réseau, disques gérés, attribution de rôle RBAC et circuits ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bf526-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="bf526-114">Voir votre utilisation et les quotas</span><span class="sxs-lookup"><span data-stu-id="bf526-114">View your usage and quotas</span></span>
<span data-ttu-id="bf526-115">Ces étapes expliquent comment tooview hello quotas actuelles dans votre abonnement pour les ressources Azure spécifiques et toosee le pourcentage de chaque quota que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="bf526-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="bf526-116">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bf526-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="bf526-117">Sélectionnez **plus Services**, puis sélectionnez **facturation** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="bf526-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="bf526-118">Dans le panneau de facturation hello, sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf526-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="bf526-119">Sélectionnez **Utilisation + quotas**.</span><span class="sxs-lookup"><span data-stu-id="bf526-119">Select **Usage + quotas**.</span></span>

   ![Bouton Utilisation et quotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="bf526-121">Hello utilisation + quotas panneau s’affiche, qui répertorie les différentes ressources disponibles dans ce pourcentage d’abonnement et hello de quota hello qui est utilisé par la ressource.</span><span class="sxs-lookup"><span data-stu-id="bf526-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Quotas et utilisation](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="bf526-123">Demander plus de ressources dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="bf526-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="bf526-124">Si vous atteignez une limite de quota, hello par défaut d’une ressource dans un abonnement peut être augmenter de limite maximale de tooa, comme décrit dans [abonnement Azure et limites de Service](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="bf526-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="bf526-125">Ces étapes vous indiquent comment toorequest un quota augmenter via hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bf526-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="bf526-126">Sélectionnez **Autres services**, **Facturation**, puis **Utilisation + quotas**.</span><span class="sxs-lookup"><span data-stu-id="bf526-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="bf526-127">Dans l’utilisation de hello + Panneau de quotas, sélectionnez hello **demande augmenter** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf526-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Bouton Demander une augmentation](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="bf526-129">toocomplete et soumettre la demande de hello, remplissez les informations de hello requis sur tous les trois onglets de hello **nouveau prend en charge la demande** formulaire.</span><span class="sxs-lookup"><span data-stu-id="bf526-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Formulaire Demander une augmentation](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="bf526-131">[Comprendre les limites de Azure et augmentent](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fournit plus d’informations sur le contact de support Azure toorequest un quota augmentation.</span><span class="sxs-lookup"><span data-stu-id="bf526-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="bf526-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf526-132">Next steps</span></span>
* <span data-ttu-id="bf526-133">Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="bf526-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
