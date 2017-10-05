---
title: Testez votre offre de machine virtuelle pour Marketplace | Microsoft Docs
description: "Découvrez comment tester votre offre de machine virtuelle pour Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="41cc0-103">Test de votre offre de machine virtuelle pour Azure Marketplace en mode intermédiaire</span><span class="sxs-lookup"><span data-stu-id="41cc0-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="41cc0-104">Dans le cadre du déploiement dans un environnement intermédiaire, vous déployez votre référence SKU dans un « bac à sable » (sandbox) privé dans lequel vous pouvez tester et vérifier ses fonctionnalités avant son déploiement dans Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41cc0-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="41cc0-105">La référence apparaît avec le statut Intermédiaire, comme pour un client l’ayant déployée.</span><span class="sxs-lookup"><span data-stu-id="41cc0-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="41cc0-106">Votre image de machine virtuelle doit être certifiée pour passer en mode Intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="41cc0-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="41cc0-107">Étape 1 : déployez votre offre dans un environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="41cc0-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="41cc0-108">Dans l'onglet **Publish**, cliquez sur **Push to Staging**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![dessin](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="41cc0-110">Si le portail de publication vous signale des erreurs, corrigez-les.</span><span class="sxs-lookup"><span data-stu-id="41cc0-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="41cc0-111">Dans la boîte de dialogue **Who can access your staged offer?** , saisissez la liste des abonnements Azure que vous allez utiliser pour afficher un aperçu de votre offre dans le [portail Azure en version préliminaire](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41cc0-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41cc0-112">Dans le cas de machines virtuelles et de modèles de solutions, veuillez **ne pas** mettre sur liste approuvée des abonnements de type CSP, DreamSpark ou Azure dans Open.</span><span class="sxs-lookup"><span data-stu-id="41cc0-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="41cc0-113">Dans le cas de machines virtuelles, lorsque vous cliquez sur le bouton **DÉPLOYER DANS UN ENVIRONNEMENT INTERMÉDIAIRE**, les étapes suivantes sont effectuées en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="41cc0-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="41cc0-114">Vous pourrez voir la progression de chaque étape sous l’onglet PUBLIER du portail de publication.</span><span class="sxs-lookup"><span data-stu-id="41cc0-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="41cc0-115">Vous devez vérifier cette page à intervalles réguliers (jusqu’à ce que l’état affiche EN MODE INTERMÉDIAIRE) en cas d’apparition d’informations d’échec nécessitant une correction de votre part.</span><span class="sxs-lookup"><span data-stu-id="41cc0-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="41cc0-116">Dans un premier temps, votre demande de déploiement dans un environnement intermédiaire est transmise à l’équipe de certification, qui valide le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="41cc0-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="41cc0-117">Toutefois, si votre demande ne contient que des modifications d’ordre marketing, l’étape de certification est ignorée.</span><span class="sxs-lookup"><span data-stu-id="41cc0-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="41cc0-118">Une fois la certification terminée, la réplication de l’offre commence sur tous les centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="41cc0-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="41cc0-119">En règle générale, il faut 24 à 48 heures pour que la réplication soit complète, mais elle peut prendre jusqu’à une semaine selon la taille du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="41cc0-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="41cc0-120">Toutefois, si votre demande ne contient que des modifications d’ordre marketing, la réplication est plus rapide.</span><span class="sxs-lookup"><span data-stu-id="41cc0-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="41cc0-121">Une fois la réplication terminée, l’offre sera répertoriée sur le [portail Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41cc0-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="41cc0-122">À ce stade, l’état devient EN MODE INTERMÉDIAIRE dans le portail de publication.</span><span class="sxs-lookup"><span data-stu-id="41cc0-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="41cc0-123">Une offre en mode intermédiaire est visible dans le [portail Azure](http:/portal.azure.com) en utilisant uniquement le(s) identifiant(s) de messagerie associé(s) à l’abonnement avec lequel l’offre est mise en mode intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="41cc0-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="41cc0-124">Connectez-vous au [portail Azure en version préliminaire](https://portal.azure.com) à l'aide de l'un des abonnements Azure répertoriés dans l'étape précédente.</span><span class="sxs-lookup"><span data-stu-id="41cc0-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="41cc0-125">Recherchez votre offre et validez vos points d'image de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="41cc0-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="41cc0-126">Assurez-vous que le contenu marketing s’affiche correctement sur Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41cc0-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="41cc0-127">Déploiement de bout en bout de l'image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41cc0-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="41cc0-129">Votre offre restera en mode Intermédiaire jusqu’à ce que vous informiez Microsoft au moyen du portail de publication [onglet **Publier** > cliquez sur le bouton **« Demander une approbation pour lancer la production »**] que vous êtes prêt à lancer la production.</span><span class="sxs-lookup"><span data-stu-id="41cc0-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="41cc0-130">À ce stade, il est souhaitable que les membres de votre équipe procèdent à des vérifications en vue de la préparation du listing de votre offre.</span><span class="sxs-lookup"><span data-stu-id="41cc0-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="41cc0-131">La plateforme intermédiaire est conçue pour tester l’offre en mode Aperçu par l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="41cc0-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="41cc0-132">Nous déconseillons fortement d’utiliser cette plateforme à des fins commerciales.</span><span class="sxs-lookup"><span data-stu-id="41cc0-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="41cc0-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41cc0-133">Next steps</span></span>
<span data-ttu-id="41cc0-134">Maintenant que votre offre est en mode Intermédiaire et que vous avez testé sa fonctionnalité et son contenu marketing, vous pouvez passer à la phase de publication finale, **Étape 4**: [déploiement de votre offre sur Marketplace](marketplace-publishing-push-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="41cc0-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="41cc0-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="41cc0-135">See also</span></span>
* [<span data-ttu-id="41cc0-136">Mise en route : publication d’une offre dans Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="41cc0-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

