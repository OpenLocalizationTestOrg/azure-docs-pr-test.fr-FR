---
title: "S’abonner à une offre | Microsoft Docs"
description: "Découvrez comment vous abonner à une offre en qualité de locataire."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 7f3f8683-ef09-4838-92ed-41f2fddbbbed
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/03/2017
ms.author: erikje
ms.openlocfilehash: 3cd87ebe9827249d32f15b5de0ad8521d0282c47
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="10bdc-103">S’abonner à une offre</span><span class="sxs-lookup"><span data-stu-id="10bdc-103">Subscribe to an offer</span></span>
<span data-ttu-id="10bdc-104">Maintenant que vous avez [créé une offre](azure-stack-create-offer.md), vérifiez que vos locataires peuvent créer un abonnement.</span><span class="sxs-lookup"><span data-stu-id="10bdc-104">Now that you've [created an offer](azure-stack-create-offer.md), test that your tenants can create a subscription.</span></span>

1. <span data-ttu-id="10bdc-105">[Connectez-vous](azure-stack-connect-azure-stack.md) au portail des locataires Azure Stack (https://portal.local.azurestack.external) et cliquez sur **Obtenir un abonnement**.</span><span class="sxs-lookup"><span data-stu-id="10bdc-105">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack tenant portal (https://portal.local.azurestack.external) and click **Get a Subscription**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="10bdc-106">Dans le champ **Nom d’affichage**, tapez un nom pour votre abonnement, cliquez sur **Offre**, cliquez sur l’une des offres du panneau **Choisir une offre**, puis sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="10bdc-106">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="10bdc-107">Pour afficher l’abonnement que vous avez créé, cliquez sur **Autres services**, sur **Abonnements**, puis sur votre nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="10bdc-107">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="10bdc-108">Une fois que vous êtes abonné à une offre, actualisez le portail pour voir les services qui font partie du nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="10bdc-108">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

## <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="10bdc-109">S’abonner à un plan additionnel</span><span class="sxs-lookup"><span data-stu-id="10bdc-109">Subscribe to an add-on plan</span></span>
<span data-ttu-id="10bdc-110">Si l’offre a un plan additionnel, les locataires peuvent l’ajouter à leur abonnement à tout moment.</span><span class="sxs-lookup"><span data-stu-id="10bdc-110">If the offer has an add-on plan, tenants can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="10bdc-111">Dans le portail des locataires, sélectionnez **Autres services** > **Abonnements**.</span><span class="sxs-lookup"><span data-stu-id="10bdc-111">In the tenant portal, select **More services** > **Subscriptions**.</span></span>

2. <span data-ttu-id="10bdc-112">Cliquez sur l’abonnement > sur le bouton **Ajouter un plan**, puis sélectionnez le plan additionnel.</span><span class="sxs-lookup"><span data-stu-id="10bdc-112">Click on the subscription > **Add Plan** button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="10bdc-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10bdc-113">Next steps</span></span>
[<span data-ttu-id="10bdc-114">Approvisionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="10bdc-114">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
