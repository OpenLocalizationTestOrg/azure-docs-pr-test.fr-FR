---
title: "aaaCreate, link, supprimer ou déplacer un compte d’intégration dans les applications Azure logique | Documents Microsoft"
description: "Comment toocreate une intégration de compte et le lier tooyour logique applications"
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
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="fe55e-103">Qu’est-ce qu'un compte d’intégration ?</span><span class="sxs-lookup"><span data-stu-id="fe55e-103">What is an integration account?</span></span>

<span data-ttu-id="fe55e-104">Un compte d’intégration permet applications d’intégration enterprise toomanage artefacts, y compris des schémas, des mappages, des certificats, des partenaires et des accords.</span><span class="sxs-lookup"><span data-stu-id="fe55e-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="fe55e-105">N’importe quelle application d’intégration que vous créez utilise un tooaccess de compte de l’intégration de ces schémas, mappages, certificats et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="fe55e-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="fe55e-106">Création d’un compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="fe55e-106">Create an integration account</span></span>

1.  <span data-ttu-id="fe55e-107">Connectez-vous à toohello [portail Azure](http://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="fe55e-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="fe55e-108">Dans le menu de gauche hello, sélectionnez **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-108">From hello left menu, select **More services**.</span></span>

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="fe55e-110">Dans la zone de recherche de hello, tapez « intégration » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="fe55e-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="fe55e-111">Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="fe55e-113">En hello haut hello, choisissez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-113">At hello top of hello page, choose **Add**.</span></span>

    ![Choisir Ajouter](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="fe55e-115">Nom de votre compte d’intégration et le sélectionnez hello abonnement Azure que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="fe55e-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="fe55e-116">Vous pouvez créer un **groupe de ressources** ou sélectionner un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="fe55e-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="fe55e-117">Sélectionnez un **Emplacement** pour l’hébergement de votre compte d’intégration et un **Niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="fe55e-118">Une fois ces opérations effectuées, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-118">When you're ready, choose **Create**.</span></span>

    ![Indiquez les détails de votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="fe55e-120">Azure configure votre compte d’intégration dans emplacement hello sélectionné, qui doit se terminer dans la minute.</span><span class="sxs-lookup"><span data-stu-id="fe55e-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="fe55e-121">Actualisez la page de hello.</span><span class="sxs-lookup"><span data-stu-id="fe55e-121">Refresh hello page.</span></span> <span data-ttu-id="fe55e-122">Votre nouveau compte d’intégration apparaît désormais dans la liste.</span><span class="sxs-lookup"><span data-stu-id="fe55e-122">You see your new integration account listed.</span></span>

    ![Votre nouveau compte d’intégration apparaît](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="fe55e-124">Ensuite, liez compte d’intégration hello cette application logique créé tooyour vous.</span><span class="sxs-lookup"><span data-stu-id="fe55e-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="fe55e-125">Lier une application de la logique de l’intégration compte tooa</span><span class="sxs-lookup"><span data-stu-id="fe55e-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="fe55e-126">toogive toomaps, schémas, des contrats et autres artefacts dans votre compte d’intégration, application logique de lien hello intégration compte tooyour accéder à vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="fe55e-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fe55e-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fe55e-127">Prerequisites</span></span>

* <span data-ttu-id="fe55e-128">Un compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="fe55e-128">An integration account</span></span>
* <span data-ttu-id="fe55e-129">Une application logique</span><span class="sxs-lookup"><span data-stu-id="fe55e-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="fe55e-130">Assurez-vous que votre application de compte et la logique d’intégration sont Bonjour *même emplacement* avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="fe55e-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="fe55e-131">Bonjour portail Azure, sélectionnez votre application de la logique et vérifier l’emplacement de l’application de votre logique.</span><span class="sxs-lookup"><span data-stu-id="fe55e-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Sélectionnez votre application logique, vérifiez l’emplacement](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="fe55e-133">Sous **Paramètres**, sélectionnez **Compte d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Sélectionner « Compte d’intégration »](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="fe55e-135">À partir de hello **sélectionner un compte d’intégration** liste, sélectionnez hello intégration compte toolink tooyour logique application.</span><span class="sxs-lookup"><span data-stu-id="fe55e-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="fe55e-136">toofinish liant, choisissez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-136">toofinish linking, choose **Save**.</span></span>

    ![Sélectionnez votre compte d’intégration](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="fe55e-138">Vous recevez une notification qui affiche votre intégration compte est lié tooyour logique application, et que tous les artefacts de votre compte d’intégration sont maintenant disponibles tooyour logique application.</span><span class="sxs-lookup"><span data-stu-id="fe55e-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Votre application logique est liée tooyour compte d’intégration](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="fe55e-140">Maintenant que votre compte d’intégration est lié tooyour logique application, vous pouvez utiliser des connecteurs de hello B2B dans vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="fe55e-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="fe55e-141">Parmi les connecteurs B2B les plus courants figurent la validation XML, et l’encodage et le décodage de fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="fe55e-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="fe55e-142">Supprimez votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="fe55e-142">Delete your integration account</span></span>

1. <span data-ttu-id="fe55e-143">Sélectionnez **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-143">Select **More services**.</span></span>

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="fe55e-145">Dans la zone de recherche de hello, tapez « intégration » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="fe55e-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="fe55e-146">Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="fe55e-148">Sélectionnez le compte d’intégration hello que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="fe55e-148">Select hello integration account that you want toodelete.</span></span>

    ![Sélectionnez toodelete de compte d’intégration](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="fe55e-150">Dans le menu de hello, choisissez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-150">On hello menu, choose **Delete**.</span></span>

    ![Choisir « Supprimer »](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="fe55e-152">Confirmez votre compte d’intégration hello toodelete choice.</span><span class="sxs-lookup"><span data-stu-id="fe55e-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="fe55e-153">Déplacer votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="fe55e-153">Move your integration account</span></span>

<span data-ttu-id="fe55e-154">toomove un tooanother de compte d’intégration Azure abonnement ou groupe de ressources, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="fe55e-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe55e-155">Une fois que vous déplacez un compte d’intégration, vous devez mettre à jour tous les scripts toouse hello nouveaux ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="fe55e-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="fe55e-156">Sélectionnez **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-156">Select **More services**.</span></span>

    ![Sélectionnez « Plus de services »](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="fe55e-158">Dans la zone de recherche de hello, tapez « intégration » pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="fe55e-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="fe55e-159">Dans la liste des résultats hello, sélectionnez **comptes d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtrer sur « intégration », sélectionner « Comptes d’intégration »](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="fe55e-161">Sélectionnez le compte d’intégration hello que vous souhaitez toomove.</span><span class="sxs-lookup"><span data-stu-id="fe55e-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="fe55e-162">Sous **Paramètres**, choisissez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="fe55e-162">Under **Settings**, choose **Properties**.</span></span>

    ![Sélectionnez toomove de compte d’intégration.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="fe55e-165">Modifier le groupe de ressources hello ou un abonnement Azure qui est associé à votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="fe55e-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Sélectionner Modifier le groupe de ressources ou Modifier l’abonnement](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="fe55e-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe55e-167">Next Steps</span></span>
* [<span data-ttu-id="fe55e-168">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="fe55e-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  

