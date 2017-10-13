---
title: "Créer une offre dans Azure Stack | Microsoft Docs"
description: "En tant qu’administrateur cloud, apprenez à créer une offre pour vos utilisateurs dans Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 269a6106f657536ba74be366f842b2f9cd86c5dc
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="726b9-103">Créer une offre dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="726b9-103">Create an offer in Azure Stack</span></span>

<span data-ttu-id="726b9-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="726b9-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="726b9-105">Les [offres](azure-stack-key-features.md) sont des groupes d’un ou plusieurs plans que les fournisseurs proposent à l’achat ou à l’abonnement aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="726b9-105">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span> <span data-ttu-id="726b9-106">Ce document montre comment créer une offre comprenant le [plan créé](azure-stack-create-plan.md) à la dernière étape.</span><span class="sxs-lookup"><span data-stu-id="726b9-106">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="726b9-107">Cette offre donne aux abonnés la possibilité d’approvisionner des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="726b9-107">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="726b9-108">Connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external) > cliquez sur **Nouveau** > **Plans + offres clients** > **Offre**.</span><span class="sxs-lookup"><span data-stu-id="726b9-108">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="726b9-109">Sur le panneau **Nouvelle offre**, renseignez le **Nom d’affichage** et le **Nom de la ressource**, puis sélectionnez un **Groupe de ressources** nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="726b9-109">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="726b9-110">Le nom d’affichage est le nom convivial de l’offre ; c’est la seule information sur l’offre que les utilisateurs verront au moment de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="726b9-110">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="726b9-111">Par conséquent, veillez à utiliser un nom intuitif qui aide l’utilisateur à comprendre en quoi elle consiste.</span><span class="sxs-lookup"><span data-stu-id="726b9-111">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="726b9-112">Seul l’administrateur peut voir le nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="726b9-112">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="726b9-113">Il s’agit du nom que les administrateurs utilisent pour gérer l’offre en tant que ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="726b9-113">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="726b9-114">Cliquez sur **Plans de base** et, sur le panneau **Plan**, sélectionnez les plans que vous souhaitez inclure à l’offre, puis cliquez sur **Sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="726b9-114">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="726b9-115">Cliquez sur **Créer** pour créer l’offre.</span><span class="sxs-lookup"><span data-stu-id="726b9-115">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="726b9-116">Cliquez sur **Toutes les ressources**, recherchez votre nouvelle offre, cliquez dessus, puis sur **Changer d’état** et enfin sur **Public**.</span><span class="sxs-lookup"><span data-stu-id="726b9-116">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="726b9-117">Les offres doivent être rendues publiques pour permettre aux utilisateurs d’avoir une vue d’ensemble lors de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="726b9-117">Offers must be made public for users to get the full view when subscribing.</span></span> <span data-ttu-id="726b9-118">Les offres peuvent être :</span><span class="sxs-lookup"><span data-stu-id="726b9-118">Offers can be:</span></span>

* <span data-ttu-id="726b9-119">**Public** : ils sont visibles pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="726b9-119">**Public**: Visible to users.</span></span>
* <span data-ttu-id="726b9-120">**Privé** : visibles uniquement par les administrateurs cloud.</span><span class="sxs-lookup"><span data-stu-id="726b9-120">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="726b9-121">Utile lors de l’élaboration du plan ou de l’offre, ou si l’administrateur cloud souhaite approuver tous les abonnements.</span><span class="sxs-lookup"><span data-stu-id="726b9-121">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="726b9-122">**Retiré**: ils sont fermés aux nouveaux abonnés.</span><span class="sxs-lookup"><span data-stu-id="726b9-122">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="726b9-123">L’administrateur cloud peut utiliser cet état pour empêcher tout abonnement futur, sans que cela affecte les abonnés actuels.</span><span class="sxs-lookup"><span data-stu-id="726b9-123">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="726b9-124">Les modifications apportées à l’offre ne sont pas immédiatement visibles par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="726b9-124">Changes to the offer are not immediately visible to the user.</span></span> <span data-ttu-id="726b9-125">Vous risquez d’avoir à vous déconnecter puis à vous reconnecter pour voir le nouvel abonnement dans le « sélecteur d’abonnement » lors de la création de ressources ou de groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="726b9-125">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="726b9-126">Vous pouvez également créer des offres, des plans et des quotas par défaut avec PowerShell, comme l’explique le [Lisez-moi de l’administrateur de services fédérés Azure Stack](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="726b9-126">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="726b9-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="726b9-127">Next steps</span></span>
[<span data-ttu-id="726b9-128">S’abonner à une offre et mettre en service une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="726b9-128">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
