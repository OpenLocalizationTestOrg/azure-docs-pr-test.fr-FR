---
title: "Test de votre offre de modèle de solution pour Marketplace | Microsoft Docs"
description: "Découvrez comment tester votre offre de modèle de solution pour Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="91a12-103">Test de votre offre de modèle de solution en mode intermédiaire</span><span class="sxs-lookup"><span data-stu-id="91a12-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="91a12-104">Dans le cadre du déploiement dans un environnement intermédiaire, vous déployez votre offre dans un « bac à sable » (sandbox) privé dans lequel vous pouvez tester et vérifier ses fonctionnalités avant le lancement de sa production.</span><span class="sxs-lookup"><span data-stu-id="91a12-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="91a12-105">L'offre apparaît avec le statut Intermédiaire, comme pour un client l'ayant déployée.</span><span class="sxs-lookup"><span data-stu-id="91a12-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="91a12-106">Votre offre doit être certifiée pour passer en mode intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="91a12-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="91a12-107">Une fois que votre offre a le statut Intermédiaire, vous pouvez l’afficher et la tester dans le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="91a12-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="91a12-108">Suivez les étapes ci-dessous pour faire passer votre offre en mode Intermédiaire et la tester dans le [portail Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="91a12-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="91a12-109">Accédez au [portail de publication](https://publish.windowsazure.com) > **Modèles de solution** > votre offre > **Publier** > **Push to Staging (Déployer dans un environnement intermédiaire)**.</span><span class="sxs-lookup"><span data-stu-id="91a12-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="91a12-110">Fournissez la liste des abonnements Azure que vous utiliserez pour l'aperçu et le test de votre offre.</span><span class="sxs-lookup"><span data-stu-id="91a12-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="91a12-111">Connectez-vous au portail Azure en version préliminaire à l'aide de l'ID d'abonnement utilisé dans l'étape précédente.</span><span class="sxs-lookup"><span data-stu-id="91a12-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="91a12-112">Effectuez au moins une série de tests des points mentionnés ci-dessous dans le portail Azure en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="91a12-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="91a12-113">Assurez-vous que le contenu marketing s'affiche correctement sur Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="91a12-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="91a12-114">Réalisez un déploiement de bout en bout de la topologie.</span><span class="sxs-lookup"><span data-stu-id="91a12-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="91a12-115">Réalisez des tests de performances et de contrainte.</span><span class="sxs-lookup"><span data-stu-id="91a12-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="91a12-116">Assurez-vous que votre topologie respecte les meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="91a12-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91a12-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91a12-117">Next steps</span></span>
<span data-ttu-id="91a12-118">Si vous êtes satisfait des résultats, vous pouvez passer à la phase finale de publication de l’offre, **Étape 4** : [Déploiement de votre offre dans Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="91a12-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="91a12-119">Sinon, apportez les modifications nécessaires à votre offre et effectuez de nouveau une demande de certification.</span><span class="sxs-lookup"><span data-stu-id="91a12-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="91a12-120">En cas de modifications de contenus marketing, la certification n'est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="91a12-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="91a12-121">Consultez [Prise en main : Publier une offre dans Azure Marketplace](marketplace-publishing-getting-started.md) pour obtenir un guide sur toutes les tâches du serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="91a12-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

