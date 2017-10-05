---
title: "Présentation de vos frais de service externe Azure | Microsoft Docs"
description: "En savoir plus sur la facturation des frais des services externes, anciennement appelés Marketplace, dans Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="68fd7-103">Présentation de la facturation de vos frais de service externe Azure</span><span class="sxs-lookup"><span data-stu-id="68fd7-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="68fd7-104">Les services externes étaient auparavant appelés Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="68fd7-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="68fd7-105">En règle générale, il s’agit de services publiés par des tiers et disponibles pour Azure, qui sont complètement intégrés à Azure.</span><span class="sxs-lookup"><span data-stu-id="68fd7-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="68fd7-106">Par exemple, ClearDB et SendGrid sont des services externes que vous pouvez acheter dans Azure, mais ils ne sont pas publiés par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="68fd7-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="68fd7-107">Lorsque vous configurez un nouveau service externe ou une ressource, un avertissement s’affiche :</span><span class="sxs-lookup"><span data-stu-id="68fd7-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Avertissement d’achat Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="68fd7-109">Les services externes sont publiés par des entreprises autres que Microsoft, mais parfois des produits Microsoft sont également classés en tant que services externes.</span><span class="sxs-lookup"><span data-stu-id="68fd7-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="68fd7-110">Facturation des services externes</span><span class="sxs-lookup"><span data-stu-id="68fd7-110">How external services are billed</span></span>
- <span data-ttu-id="68fd7-111">Les services externes sont facturés séparément.</span><span class="sxs-lookup"><span data-stu-id="68fd7-111">External services are billed separately.</span></span> <span data-ttu-id="68fd7-112">Ils sont traités comme des commandes individuelles au sein de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="68fd7-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="68fd7-113">La période de facturation pour chaque service est définie lorsque vous achetez le service.</span><span class="sxs-lookup"><span data-stu-id="68fd7-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="68fd7-114">À ne pas confondre avec la période de facturation de l’abonnement sous lequel vous l’avez acheté.</span><span class="sxs-lookup"><span data-stu-id="68fd7-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="68fd7-115">Vous recevez également des factures distinctes et votre carte de crédit est facturée séparément.</span><span class="sxs-lookup"><span data-stu-id="68fd7-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="68fd7-116">Chaque service externe possède un modèle de facturation différent.</span><span class="sxs-lookup"><span data-stu-id="68fd7-116">Each external service has a different billing model.</span></span> <span data-ttu-id="68fd7-117">Certains services sont facturés selon un mode de paiement à l’utilisation, tandis que d’autres utilisent un modèle de paiement mensuel.</span><span class="sxs-lookup"><span data-stu-id="68fd7-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="68fd7-118">Les services externes Azure nécessitent une carte de crédit. Vous ne pouvez pas acheter des services externes avec un paiement par facture.</span><span class="sxs-lookup"><span data-stu-id="68fd7-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="68fd7-119">Vous ne pouvez pas utiliser de crédits mensuels gratuits pour les services externes.</span><span class="sxs-lookup"><span data-stu-id="68fd7-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="68fd7-120">Si vous utilisez un abonnement Azure incluant des [crédits gratuits](https://azure.microsoft.com/pricing/spending-limits/), ceux-ci ne peuvent pas s’appliquer aux factures de services externes.</span><span class="sxs-lookup"><span data-stu-id="68fd7-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="68fd7-121">Utilisez une carte de crédit pour acheter des services externes.</span><span class="sxs-lookup"><span data-stu-id="68fd7-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="68fd7-122">Afficher les dépenses et l’historique du service externe dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="68fd7-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="68fd7-123">Vous pouvez afficher la liste des services externes dans chaque abonnement dans le [portail Azure](https://portal.azure.com/) :</span><span class="sxs-lookup"><span data-stu-id="68fd7-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="68fd7-124">Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’administrateur de compte.</span><span class="sxs-lookup"><span data-stu-id="68fd7-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="68fd7-125">Dans le menu Hub, sélectionnez **Abonnements**.</span><span class="sxs-lookup"><span data-stu-id="68fd7-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Sélection des abonnements dans le menu Hub](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="68fd7-127">Dans le panneau **Abonnements**, sélectionnez l’abonnement que vous souhaitez consulter, puis sélectionnez **Services externes**.</span><span class="sxs-lookup"><span data-stu-id="68fd7-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Sélectionnez un abonnement dans le panneau Facturation](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="68fd7-129">Chaque commande de service externe doit s’afficher avec le nom de l’éditeur, le niveau de service acheté, le nom donné à la ressource et le statut actuel de la commande.</span><span class="sxs-lookup"><span data-stu-id="68fd7-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="68fd7-130">Pour afficher les factures précédentes, sélectionnez un service externe.</span><span class="sxs-lookup"><span data-stu-id="68fd7-130">To see past bills, select an external service.</span></span>
   
    ![Sélectionnez un service externe](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="68fd7-132">De là, vous pouvez afficher les montants des factures précédentes avec la répartition des taxes.</span><span class="sxs-lookup"><span data-stu-id="68fd7-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Afficher l’historique de facturation des services externes](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="68fd7-134">Afficher les dépenses du service externe pour les clients de contrat Entreprise (EA)</span><span class="sxs-lookup"><span data-stu-id="68fd7-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="68fd7-135">Les clients de contrat Entreprise (EA) peuvent voir les dépenses du service externe et télécharger des rapports dans le portail EA.</span><span class="sxs-lookup"><span data-stu-id="68fd7-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="68fd7-136">Consultez la page sur [Azure Marketplace pour les clients EA](https://ea.azure.com/helpdocs/azureMarketplace) pour commencer.</span><span class="sxs-lookup"><span data-stu-id="68fd7-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="68fd7-137">Gérer les modes de paiement pour les commandes de service externe</span><span class="sxs-lookup"><span data-stu-id="68fd7-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="68fd7-138">Mettez à jour vos modes de paiement pour les commandes de service externe à partir du [Centre des comptes](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="68fd7-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="68fd7-139">Si vous avez acheté votre abonnement avec un compte professionnel ou scolaire, vous devez [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour modifier votre mode de paiement.</span><span class="sxs-lookup"><span data-stu-id="68fd7-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="68fd7-140">Connectez-vous au [Centre des comptes](https://account.windowsazure.com/) et [accédez à l’onglet **marketplace**](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="68fd7-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Sélectionnez marketplace dans le centre des comptes](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="68fd7-142">Sélectionnez le service externe à gérer</span><span class="sxs-lookup"><span data-stu-id="68fd7-142">Select the external service you want to manage</span></span>
   
    ![Sélectionnez le service externe à gérer](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="68fd7-144">Dans la partie droite de la page, cliquez sur **Modifier le mode de paiement**.</span><span class="sxs-lookup"><span data-stu-id="68fd7-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="68fd7-145">Ce lien vous dirige vers un autre portail pour gérer votre mode de paiement.</span><span class="sxs-lookup"><span data-stu-id="68fd7-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Résumé de la commande](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="68fd7-147">Cliquez sur **Modifier les informations** et suivez les instructions pour mettre à jour vos informations de paiement.</span><span class="sxs-lookup"><span data-stu-id="68fd7-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Sélectionnez Modifier les informations](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="68fd7-149">Annuler une commande de service externe</span><span class="sxs-lookup"><span data-stu-id="68fd7-149">Cancel an external service order</span></span>
<span data-ttu-id="68fd7-150">Si vous souhaitez annuler votre commande de service externe, supprimez la ressource dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68fd7-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Supprimer la ressource](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="68fd7-152">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="68fd7-152">Need help?</span></span> <span data-ttu-id="68fd7-153">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="68fd7-153">Contact support.</span></span>
<span data-ttu-id="68fd7-154">Si vous avez d’autres questions, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour obtenir une prise en charge rapide de votre problème.</span><span class="sxs-lookup"><span data-stu-id="68fd7-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

