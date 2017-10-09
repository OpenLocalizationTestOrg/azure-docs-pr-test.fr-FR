---
title: aaaTest proposent de votre machine virtuelle pour hello Marketplace | Documents Microsoft
description: "Comprendre comment tootest votre machine virtuelle de l’image pour hello Azure Marketplace."
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
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="8aa9c-103">Tester votre offre de la machine virtuelle pour hello Azure Marketplace intermédiaire</span><span class="sxs-lookup"><span data-stu-id="8aa9c-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="8aa9c-104">Désigne un déploiement de votre référence (SKU) « bac à sable » où vous pouvez tester et valider ses fonctionnalités avant de le déployer toohello Marketplace privé de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="8aa9c-105">Hello référence (SKU) s’affiche dans la mise en lots comme il le ferait client tooa qui a déployé.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="8aa9c-106">Votre image de machine virtuelle doit être certifié toobe envoyée toostaging.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="8aa9c-107">Étape 1 : Push toostaging de votre offre</span><span class="sxs-lookup"><span data-stu-id="8aa9c-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="8aa9c-108">Sur hello **publier** , cliquez sur **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![dessin](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="8aa9c-110">Si le portail de publication de hello vous avertit de toutes les erreurs, corrigez-les.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="8aa9c-111">Bonjour **qui peut accéder à votre offre intermédiaire ?** boîte de dialogue, entrez la liste hello des abonnements Azure que vous allez utiliser toopreview votre offre Bonjour [portail Azure preview](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8aa9c-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8aa9c-112">Dans le cas de machines virtuelles et de modèles de solutions, veuillez **ne pas** mettre sur liste approuvée des abonnements de type CSP, DreamSpark ou Azure dans Open.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="8aa9c-113">En cas de Machines virtuelles, lorsque vous cliquez sur le bouton de hello **PUSH tooSTAGING**, effectuée derrière la scène de hello hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="8aa9c-114">Vous serez tooview en mesure de hello progression de chaque étape sous l’onglet Publier de hello Bonjour portail de publication.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="8aa9c-115">Vous devez vérifier cette page à intervalle régulier (jusqu'à ce que l’état de hello affiche intermédiaire) pour toutes les informations d’échec qui ont besoin de correction à partir de votre principal.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="8aa9c-116">Dans un premier temps votre demande de mise en lots passe équipe certification toohello est chargée de valider le disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="8aa9c-117">Toutefois, si votre demande a marketing uniquement les modifications, puis hello certification étape est ignorée.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="8aa9c-118">Une fois la certification de hello est terminée, la réplication de début offre de hello pour tous les hello centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="8aa9c-119">En règle générale, il prend 24-48hours pour hello réplication toocomplete mais peut prendre jusqu'à une semaine tooa selon la taille de hello du disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="8aa9c-120">Toutefois, si votre demande a marketing uniquement les modifications, la réplication hello est plus rapide.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="8aa9c-121">Lorsque la réplication hello est terminée, puis hello offre sera disponible dans hello [portail Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8aa9c-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="8aa9c-122">À ce hello temps état deviennent intermédiaire Bonjour portail de publication.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="8aa9c-123">Une offre intermédiaire est visible dans hello [portail Azure](http:/portal.azure.com) uniquement à l’aide d’identificateurs de messagerie hello associés abonnement hello avec quels hello offre soit préparée.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="8aa9c-124">Connectez-vous à toohello [portail Azure preview](https://portal.azure.com) à l’aide d’une des hello abonnements Azure sont répertoriés à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="8aa9c-125">Recherchez votre offre et validez vos points d'image de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="8aa9c-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="8aa9c-126">Assurez-vous que le contenu de marketing s’affiche correctement Bonjour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="8aa9c-127">Déploiement de bout en bout de l’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="8aa9c-129">Votre offre restent dans la mise en lots jusqu'à ce que vous informer Microsoft via le portail de publication de hello [**publier** onglet > cliquez sur le bouton de hello **« Demander l’approbation tooPush tooProduction »**] que vous êtes prêt toopush tooproduction.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="8aa9c-130">Il s’agit d’un toohave moment idéal tous les membres de votre équipe vérifier sur tous les éléments de la préparation de votre offre va répertoriées.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="8aa9c-131">Hello plate-forme intermédiaire est conçu pour test offre hello dans un mode Aperçu par le serveur de publication hello.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="8aa9c-132">Nous déconseillons fortement d’utiliser cette plateforme à des fins commerciales.</span><span class="sxs-lookup"><span data-stu-id="8aa9c-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8aa9c-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8aa9c-133">Next steps</span></span>
<span data-ttu-id="8aa9c-134">Maintenant que votre offre est « intermédiaire » et que vous avez testé ses fonctionnalités et contenu commercial, vous pouvez procéder à la publication finale toohello phase, **étape 4**: [déploiement votre toohello offre Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="8aa9c-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8aa9c-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8aa9c-135">See also</span></span>
* [<span data-ttu-id="8aa9c-136">Mise en route : comment toopublish une toohello offre Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8aa9c-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

