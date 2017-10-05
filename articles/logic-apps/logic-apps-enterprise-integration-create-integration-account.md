---
title: "Créer, lier, supprimer ou déplacer un compte d’intégration dans Azure Logic Apps | Microsoft Docs"
description: "Comment créer un compte d’intégration et l’associer à vos applications logiques"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="15b22-103">Qu’est-ce qu'un compte d’intégration ?</span><span class="sxs-lookup"><span data-stu-id="15b22-103">What is an integration account?</span></span>

<span data-ttu-id="15b22-104">Un compte d’intégration permet aux applications Enterprise Integration de gérer des artefacts, y compris des schémas, des mappages, des certificats, des partenaires et des contrats.</span><span class="sxs-lookup"><span data-stu-id="15b22-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="15b22-105">Toutes les applications d’intégration que vous créez utilisent un compte d’intégration pour accéder à ces schémas, mappages, certificats, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="15b22-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="15b22-106">Création d’un compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="15b22-106">Create an integration account</span></span>

1.  <span data-ttu-id="15b22-107">Connectez-vous au [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="15b22-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="15b22-108">Dans le menu de gauche, cliquez sur **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="15b22-108">From the left menu, select **More services**.</span></span>

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="15b22-110">Dans la zone de recherche, entrez « intégration » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="15b22-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="15b22-111">Sélectionnez **Comptes d’intégration** dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="15b22-111">In the results list, select **Integration Accounts**.</span></span>

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="15b22-113">En haut de la page, choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="15b22-113">At the top of the page, choose **Add**.</span></span>

    ![Choisir Ajouter](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="15b22-115">Nommez votre compte d’intégration et sélectionnez l’abonnement Azure que vous voulez utiliser.</span><span class="sxs-lookup"><span data-stu-id="15b22-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="15b22-116">Vous pouvez créer un **groupe de ressources** ou sélectionner un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="15b22-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="15b22-117">Sélectionnez un **Emplacement** pour l’hébergement de votre compte d’intégration et un **Niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="15b22-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="15b22-118">Une fois ces opérations effectuées, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="15b22-118">When you're ready, choose **Create**.</span></span>

    ![Indiquez les détails de votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="15b22-120">Azure configure votre compte d’intégration à l’emplacement sélectionné en moins d’une minute.</span><span class="sxs-lookup"><span data-stu-id="15b22-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="15b22-121">Actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="15b22-121">Refresh the page.</span></span> <span data-ttu-id="15b22-122">Votre nouveau compte d’intégration apparaît désormais dans la liste.</span><span class="sxs-lookup"><span data-stu-id="15b22-122">You see your new integration account listed.</span></span>

    ![Votre nouveau compte d’intégration apparaît](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="15b22-124">Ensuite, liez le compte d’intégration que vous venez de créer à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="15b22-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="15b22-125">Lier un compte d’intégration à une application logique</span><span class="sxs-lookup"><span data-stu-id="15b22-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="15b22-126">Pour que vos applications logiques puissent accéder à des mappages, des schémas, des contrats et autres artefacts de votre compte d’intégration, liez le compte d’intégration à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="15b22-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="15b22-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15b22-127">Prerequisites</span></span>

* <span data-ttu-id="15b22-128">Un compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="15b22-128">An integration account</span></span>
* <span data-ttu-id="15b22-129">Une application logique</span><span class="sxs-lookup"><span data-stu-id="15b22-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="15b22-130">Vérifiez que votre compte d’intégration et votre application logique se trouvent dans le *même emplacement Azure* avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="15b22-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="15b22-131">Dans le portail Azure, sélectionnez votre application logique, puis vérifiez son emplacement.</span><span class="sxs-lookup"><span data-stu-id="15b22-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Sélectionnez votre application logique, vérifiez l’emplacement](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="15b22-133">Sous **Paramètres**, sélectionnez **Compte d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="15b22-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Sélectionner « Compte d’intégration »](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="15b22-135">Dans la liste **Sélectionner un compte d’intégration**, sélectionnez le compte d’intégration que vous souhaitez lier à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="15b22-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="15b22-136">Pour terminer la liaison, choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="15b22-136">To finish linking, choose **Save**.</span></span>

    ![Sélectionnez votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="15b22-138">Une notification indique que votre compte d’intégration a été lié à votre application logique et que tous les artefacts de votre compte d’intégration sont désormais disponibles pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="15b22-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Votre application logique est liée à votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="15b22-140">Maintenant que votre compte d’intégration est lié à votre application logique, vous pouvez utiliser les connecteurs B2B dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="15b22-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="15b22-141">Parmi les connecteurs B2B les plus courants figurent la validation XML, et l’encodage et le décodage de fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="15b22-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="15b22-142">Supprimez votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="15b22-142">Delete your integration account</span></span>

1. <span data-ttu-id="15b22-143">Sélectionnez **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="15b22-143">Select **More services**.</span></span>

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="15b22-145">Dans la zone de recherche, entrez « intégration » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="15b22-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="15b22-146">Sélectionnez **Comptes d’intégration** dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="15b22-146">In the results list, select **Integration Accounts**.</span></span>

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="15b22-148">Sélectionnez le compte d’intégration que vous voulez supprimer.</span><span class="sxs-lookup"><span data-stu-id="15b22-148">Select the integration account that you want to delete.</span></span>

    ![Sélectionner un compte d’intégration à supprimer](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="15b22-150">Dans le menu, choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="15b22-150">On the menu, choose **Delete**.</span></span>

    ![Choisir « Supprimer »](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="15b22-152">Confirmez la suppression du compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="15b22-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="15b22-153">Déplacer votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="15b22-153">Move your integration account</span></span>

<span data-ttu-id="15b22-154">Pour déplacer un compte d’intégration vers un autre abonnement ou groupe de ressources Azure, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="15b22-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15b22-155">Quand vous déplacez un compte d’intégration, vous devez mettre à jour tous les scripts pour qu’ils utilisent les nouveaux ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="15b22-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="15b22-156">Sélectionnez **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="15b22-156">Select **More services**.</span></span>

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="15b22-158">Dans la zone de recherche, entrez « intégration » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="15b22-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="15b22-159">Sélectionnez **Comptes d’intégration** dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="15b22-159">In the results list, select **Integration Accounts**.</span></span>

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="15b22-161">Sélectionnez le compte d’intégration que vous voulez déplacer.</span><span class="sxs-lookup"><span data-stu-id="15b22-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="15b22-162">Sous **Paramètres**, choisissez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="15b22-162">Under **Settings**, choose **Properties**.</span></span>

    ![Sélectionner un compte d’intégration à déplacer.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="15b22-165">Modifiez le groupe de ressources ou l’abonnement Azure associé à votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="15b22-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Sélectionner Modifier le groupe de ressources ou Modifier l’abonnement](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="15b22-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15b22-167">Next Steps</span></span>
* [<span data-ttu-id="15b22-168">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="15b22-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  

