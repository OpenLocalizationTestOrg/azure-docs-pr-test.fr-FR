---
title: Annulation de votre abonnement Azure | Microsoft Docs
description: "Décrit comment annuler votre abonnement Azure, par exemple l’abonnement d’essai gratuit"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a><span data-ttu-id="16282-103">Annuler votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="16282-103">Cancel your subscription for Azure</span></span>

<span data-ttu-id="16282-104">Vous pouvez annuler votre abonnement Azure en tant qu’[administrateur de compte](billing-subscription-transfer.md#whoisaa).</span><span class="sxs-lookup"><span data-stu-id="16282-104">You can cancel your Azure subscription as the [Account Administrator](billing-subscription-transfer.md#whoisaa).</span></span> <span data-ttu-id="16282-105">Après l’annulation de l’abonnement, vous n’avez plus accès aux ressources ni aux services Azure.</span><span class="sxs-lookup"><span data-stu-id="16282-105">After you cancel the subscription, your access to Azure services and resources ends.</span></span>

<span data-ttu-id="16282-106">Avant d’annuler votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="16282-106">Before you cancel your subscription:</span></span>

* <span data-ttu-id="16282-107">Sauvegardez vos données.</span><span class="sxs-lookup"><span data-stu-id="16282-107">Back up your data.</span></span> <span data-ttu-id="16282-108">Par exemple, si vous stockez des données dans le stockage Azure ou SQL, téléchargez une copie.</span><span class="sxs-lookup"><span data-stu-id="16282-108">For example, if you're storing data in Azure storage or SQL, download a copy.</span></span> <span data-ttu-id="16282-109">Si vous avez une machine virtuelle, enregistrez une image localement.</span><span class="sxs-lookup"><span data-stu-id="16282-109">If you have a virtual machine, save an image of it locally.</span></span>
* <span data-ttu-id="16282-110">Arrêtez les services.</span><span class="sxs-lookup"><span data-stu-id="16282-110">Shut down your services.</span></span> <span data-ttu-id="16282-111">Accédez à la [page de ressources du portail de gestion](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources) et **arrêtez** les machines virtuelles, les applications ou autres services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="16282-111">Go to the [resources page in the management portal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), and **Stop** any running virtual machines, applications, or other services.</span></span>
* <span data-ttu-id="16282-112">Envisagez de migrer vos données.</span><span class="sxs-lookup"><span data-stu-id="16282-112">Consider migrating your data.</span></span> <span data-ttu-id="16282-113">Consultez la page [Déplacer des ressources vers un nouveau groupe de ressources ou un nouvel abonnement](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="16282-113">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="16282-114">Si vous annulez un [plan de support Azure](https://azure.microsoft.com/support/plans/), vous êtes facturé chaque mois jusqu’à la fin de la période de 6 mois.</span><span class="sxs-lookup"><span data-stu-id="16282-114">If you cancel a paid [Azure Support plan](https://azure.microsoft.com/support/plans/), you are still billed monthly for the rest of the 6-months term.</span></span>

## <a name="cancel-subscription-using-the-azure-portal"></a><span data-ttu-id="16282-115">Annuler l’abonnement à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="16282-115">Cancel subscription using the Azure portal</span></span>

1. <span data-ttu-id="16282-116">Sélectionnez votre abonnement sur la [page Abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="16282-116">Select your subscription from the [Subscriptions page](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

1. <span data-ttu-id="16282-117">Sélectionnez l’abonnement à annuler, puis cliquez sur **Annuler l’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="16282-117">Select the subscription that you want to cancel and click **Cancel subscription**.</span></span>

    ![Capture d’écran qui montre le bouton Annuler](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. <span data-ttu-id="16282-119">Suivez les invites et terminez l’annulation.</span><span class="sxs-lookup"><span data-stu-id="16282-119">Follow prompts and finish cancellation.</span></span>

## <a name="cancel-subscription-using-the-azure-account-center"></a><span data-ttu-id="16282-120">Annuler l’abonnement à l’aide du Centre des comptes Azure</span><span class="sxs-lookup"><span data-stu-id="16282-120">Cancel subscription using the Azure Account Center</span></span>

1. <span data-ttu-id="16282-121">Connectez-vous au [Centre des comptes Azure](https://account.windowsazure.com/subscriptions) en tant qu’administrateur de compte.</span><span class="sxs-lookup"><span data-stu-id="16282-121">Sign in to the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

1. <span data-ttu-id="16282-122">Sous **Cliquez sur un abonnement pour consulter les détails et l’utilisation**, sélectionnez l’abonnement que vous souhaitez annuler.</span><span class="sxs-lookup"><span data-stu-id="16282-122">Under **Click a subscription to view details and usage**, select the subscription that you want to cancel.</span></span>

    ![Capture d’écran montrant un exemple d’abonnement sélectionné](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. <span data-ttu-id="16282-124">Dans la partie droite de la page, cliquez sur **Annuler l’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="16282-124">On the right side of the page, select **Cancel Subscription**.</span></span>

    ![Capture d’écran montrant le bouton Annuler l’abonnement](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. <span data-ttu-id="16282-126">Sélectionnez **Oui, annulez mon abonnement**.</span><span class="sxs-lookup"><span data-stu-id="16282-126">Select **Yes, cancel my subscription**.</span></span>

    ![Capture d’écran qui montre la boîte de dialogue Annuler](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. <span data-ttu-id="16282-128">Cliquez sur </span><span class="sxs-lookup"><span data-stu-id="16282-128">Click</span></span> ![Bouton de symbole de coche](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) <span data-ttu-id="16282-130">pour fermer la boîte de dialogue et revenir à votre page d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="16282-130">to close the dialog window and return to your subscription page.</span></span>

## <a name="what-happens-after-i-cancel-my-subscription"></a><span data-ttu-id="16282-131">Que se passe-t-il après l’annulation de mon abonnement ?</span><span class="sxs-lookup"><span data-stu-id="16282-131">What happens after I cancel my subscription?</span></span>

<span data-ttu-id="16282-132">Une fois que vous l’annulez, la facturation s’arrête immédiatement.</span><span class="sxs-lookup"><span data-stu-id="16282-132">Once you cancel, billing is stopped immediately.</span></span> <span data-ttu-id="16282-133">Toutefois, 10 minutes maximum peuvent être nécessaires pour que l’annulation apparaisse dans le portail.</span><span class="sxs-lookup"><span data-stu-id="16282-133">However, it can take up to 10 minutes for the cancellation show in the portal.</span></span>

<span data-ttu-id="16282-134">Une fois ce délai passé, vos services sont désactivés.</span><span class="sxs-lookup"><span data-stu-id="16282-134">After that, your services are disabled.</span></span> <span data-ttu-id="16282-135">Cela signifie que vos machines virtuelles et les adresses IP temporaires sont libérées et que le stockage est en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="16282-135">That means your virtual machines are deallocated, temporary IP addresses are freed, and storage is read-only.</span></span>

<span data-ttu-id="16282-136">À moins que vous n’utilisiez un essai gratuit ou que vous disposiez de crédits, vous êtes facturé pour tous les frais d’utilisation en suspens générés entre votre dernier cycle de facturation et la date d’annulation.</span><span class="sxs-lookup"><span data-stu-id="16282-136">Unless you’re on a Free Trial or have credits available, you’re billed for any outstanding usage charges generated between your last billing cycle and the cancellation date.</span></span> <span data-ttu-id="16282-137">Vous obtenez votre dernière facture à la fin du cycle de facturation.</span><span class="sxs-lookup"><span data-stu-id="16282-137">You get your last bill at the end of the billing cycle.</span></span>

<span data-ttu-id="16282-138">Une fois votre abonnement annulé, nous attendons 90 jours avant de supprimer définitivement vos données au cas où vous deviez y accéder ou changiez d’avis.</span><span class="sxs-lookup"><span data-stu-id="16282-138">After you cancel your subscription, we wait 90 days before permanently deleting your data in case you need to access it or you change your mind.</span></span> <span data-ttu-id="16282-139">Nous ne vous facturons pas la conservation des données.</span><span class="sxs-lookup"><span data-stu-id="16282-139">We don't charge you for retaining the data.</span></span> <span data-ttu-id="16282-140">Pour en savoir plus, consultez [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409) (Centre de gestion de la confidentialité de Microsoft - Comment nous gérons vos données).</span><span class="sxs-lookup"><span data-stu-id="16282-140">To learn more, see [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span></span>

## <a name="reactivate-subscription"></a><span data-ttu-id="16282-141">Réactivation de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="16282-141">Reactivate subscription</span></span>

<span data-ttu-id="16282-142">Si vous annulez par inadvertance votre abonnement de paiement à l’utilisation, vous pouvez [le réactiver dans le Centre des comptes](billing-subscription-become-disable.md).</span><span class="sxs-lookup"><span data-stu-id="16282-142">If you cancel your Pay-As-You-Go subscription accidentally, you can [reactivate it in the Accounts Center](billing-subscription-become-disable.md).</span></span>

<span data-ttu-id="16282-143">Si votre abonnement n’est pas un abonnement de paiement à l’utilisation, contactez le support dans les 90 jours suivant l’annulation pour réactiver votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="16282-143">If your subscription is not Pay-As-You-Go, contact support within 90 days of cancellation to reactivate your subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="16282-144">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="16282-144">Need help?</span></span> <span data-ttu-id="16282-145">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="16282-145">Contact support.</span></span>

<span data-ttu-id="16282-146">Si vous avez d’autres questions, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour obtenir une prise en charge rapide de votre problème.</span><span class="sxs-lookup"><span data-stu-id="16282-146">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
