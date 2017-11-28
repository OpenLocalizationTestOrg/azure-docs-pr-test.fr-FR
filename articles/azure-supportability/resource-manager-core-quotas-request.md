---
title: "Demandes d’augmentation du quota de base d’Azure Resource Manager | Microsoft Docs"
description: "Demandes d’augmentation du quota de base d’Azure Resource Manager"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="dd5ff-103">Demandes d’augmentation du quota de base de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd5ff-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="dd5ff-104">Les quotas de base de Resource Manager sont appliqués au niveau de la région et de la famille de références (SKU).</span><span class="sxs-lookup"><span data-stu-id="dd5ff-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="dd5ff-105">Pour en savoir plus sur la façon dont les quotas sont appliqués, consultez la page [Abonnement Azure et limites, quotas et contraintes de service](http://aka.ms/quotalimits).</span><span class="sxs-lookup"><span data-stu-id="dd5ff-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="dd5ff-106">Pour en savoir plus sur les familles de références, vous pouvez comparer le coût et les performances sur la page [Tarification des machines virtuelles](http://aka.ms/pricingcompute).</span><span class="sxs-lookup"><span data-stu-id="dd5ff-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="dd5ff-107">Pour demander une augmentation, créez un cas de prise en charge de quota de cœurs dans le portail Azure, [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd5ff-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="dd5ff-108">Découvrez comment [créer une demande de support](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd5ff-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="dd5ff-109">Dans la nouvelle page de demande de support, sélectionnez le type de problème « Quota » et le type de quota « Cœurs ».</span><span class="sxs-lookup"><span data-stu-id="dd5ff-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Panneau Informations de base du quota](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="dd5ff-111">Sélectionnez le modèle de déploiement « Resource Manager » et sélectionnez un emplacement.</span><span class="sxs-lookup"><span data-stu-id="dd5ff-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Panneau Problème de quota](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="dd5ff-113">Sélectionnez les familles de références qui nécessitent une augmentation.</span><span class="sxs-lookup"><span data-stu-id="dd5ff-113">Select the SKU Families that require an increase.</span></span>

    ![Série de références sélectionnée](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="dd5ff-115">Entrez les nouvelles limites que vous souhaitez appliquer à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="dd5ff-115">Enter the new limits you would like on the subscription.</span></span>

    ![Nouvelle demande de quota de référence](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="dd5ff-117">Pour supprimer une ligne, désactivez la case de la référence dans la liste déroulante de la famille de références ou cliquez sur l’icône de fermeture « x ».</span><span class="sxs-lookup"><span data-stu-id="dd5ff-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="dd5ff-118">Après avoir entré le quota de votre choix pour chaque famille de références, cliquez sur « Suivant » sur la page de l’étape Problème pour poursuivre la création de demande de support.</span><span class="sxs-lookup"><span data-stu-id="dd5ff-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
