---
title: aaaSchemas pour la validation XML - Azure Logic Apps | Documents Microsoft
description: "Valider des documents XML avec des schémas pour Azure Logic Apps et Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="36aec-103">Valider le code XML avec des schémas pour Azure Logic Apps et hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="36aec-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="36aec-104">Schémas de confirmer que vous recevez des documents XML hello sont valides et ont hello attendu de données dans un format prédéfini.</span><span class="sxs-lookup"><span data-stu-id="36aec-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="36aec-105">Les schémas aident également à valider les messages échangés dans un scénario d’entreprise à entreprise (B2B).</span><span class="sxs-lookup"><span data-stu-id="36aec-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="36aec-106">Ajout d’un schéma</span><span class="sxs-lookup"><span data-stu-id="36aec-106">Add a schema</span></span>

1. <span data-ttu-id="36aec-107">Bonjour portail Azure, sélectionnez **davantage de services**.</span><span class="sxs-lookup"><span data-stu-id="36aec-107">In hello Azure portal, select **More services**.</span></span>

    ![Portail Azure, « Plus de services »](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="36aec-109">Dans la zone de recherche de filtre hello, entrez **intégration**, puis sélectionnez **comptes d’intégration** à partir de la liste des résultats hello.</span><span class="sxs-lookup"><span data-stu-id="36aec-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Zone de recherche de filtre](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="36aec-111">Sélectionnez hello **compte d’intégration** où vous souhaitez le schéma de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="36aec-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Liste des comptes d’intégration](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="36aec-113">Choisissez hello **schémas** vignette.</span><span class="sxs-lookup"><span data-stu-id="36aec-113">Choose hello **Schemas** tile.</span></span>

    ![Exemple de compte d’intégration, « Schémas »](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="36aec-115">Ajout d’un fichier de schéma d’une taille inférieure à 2 Mo</span><span class="sxs-lookup"><span data-stu-id="36aec-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="36aec-116">Bonjour **schémas** panneau s’affiche (à partir de hello étapes précédentes), sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="36aec-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Panneau Schémas, « Ajouter »](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="36aec-118">Saisissez un nom pour votre schéma.</span><span class="sxs-lookup"><span data-stu-id="36aec-118">Enter a name for your schema.</span></span> <span data-ttu-id="36aec-119">Télécharger le fichier de schéma hello en sélectionnant hello dossier icône suivant toohello **schéma** boîte.</span><span class="sxs-lookup"><span data-stu-id="36aec-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="36aec-120">Après la fin du processus de téléchargement hello, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="36aec-120">After hello upload process completes, select **OK**.</span></span>

    ![Capture d’écran d’« Ajouter un schéma » avec « Fichier de petite taille » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="36aec-122">Ajouter un fichier de schéma supérieur à 2 Mo (haut too8 Mo maximum)</span><span class="sxs-lookup"><span data-stu-id="36aec-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="36aec-123">Ces étapes varient en fonction de niveau d’accès hello blob conteneur : **Public** ou **aucun accès anonyme**.</span><span class="sxs-lookup"><span data-stu-id="36aec-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="36aec-124">**toodetermine ce niveau d’accès**</span><span class="sxs-lookup"><span data-stu-id="36aec-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="36aec-125">Ouvrez **l’Explorateur de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="36aec-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="36aec-126">Sous **conteneurs d’objets Blob**, sélectionnez conteneur d’objets blob hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="36aec-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="36aec-127">Sélectionnez **Sécurité**, **Niveau d’accès**.</span><span class="sxs-lookup"><span data-stu-id="36aec-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="36aec-128">Si le niveau d’accès sécurité hello blob est **Public**, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="36aec-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Explorateur de stockage Azure, avec « Conteneurs d’objets Blob », « Sécurité » et « Public » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="36aec-130">Compte de stockage hello schéma tooyour de télécharger et copier hello URI.</span><span class="sxs-lookup"><span data-stu-id="36aec-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Compte de stockage avec l’URI mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="36aec-132">Dans **ajouter un schéma**, sélectionnez **d’un fichier volumineux**et fournir hello URI Bonjour **URI contenu** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="36aec-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Schémas, avec le bouton « Ajouter » et « Fichier volumineux » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="36aec-134">Si le niveau d’accès sécurité hello blob est **aucun accès anonyme**, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="36aec-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Explorateur de stockage Azure, avec « Conteneurs d’objets Blob », « Sécurité » et « No anonymous access » (Aucun accès anonyme) mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="36aec-136">Téléchargez le compte de stockage tooyour hello schéma.</span><span class="sxs-lookup"><span data-stu-id="36aec-136">Upload hello schema tooyour storage account.</span></span>

    ![Compte de stockage](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="36aec-138">Générer une signature d’accès partagé pour le schéma de hello.</span><span class="sxs-lookup"><span data-stu-id="36aec-138">Generate a shared access signature for hello schema.</span></span>

    ![Compte de stockage, avec l’onglet des signatures d’accès partagé mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="36aec-140">Dans **ajouter un schéma**, sélectionnez **d’un fichier volumineux**et fournissent l’URI de signature d’accès partagé hello Bonjour **URI contenu** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="36aec-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Schémas, avec le bouton « Ajouter » et « Fichier volumineux » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="36aec-142">Bonjour **schémas** Panneau de votre compte d’intégration, votre schéma nouvellement ajoutée doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="36aec-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Votre compte d’intégration, avec « Schémas » et hello nouveau schéma mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="36aec-144">Modification de schémas</span><span class="sxs-lookup"><span data-stu-id="36aec-144">Edit schemas</span></span>

1. <span data-ttu-id="36aec-145">Choisissez hello **schémas** vignette.</span><span class="sxs-lookup"><span data-stu-id="36aec-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="36aec-146">Après avoir hello **schémas** panneau s’ouvre, sélectionnez hello schéma que tooedit.</span><span class="sxs-lookup"><span data-stu-id="36aec-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="36aec-147">Sur hello **schémas** panneau, choisissez **modifier**.</span><span class="sxs-lookup"><span data-stu-id="36aec-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Panneau Schémas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="36aec-149">Fichier de schéma hello SELECT que vous souhaitez tooedit, puis sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="36aec-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Ouvrir le schéma fichier tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="36aec-151">Azure affiche un message qui hello schéma téléchargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="36aec-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="36aec-152">Suppression de schémas</span><span class="sxs-lookup"><span data-stu-id="36aec-152">Delete schemas</span></span>

1. <span data-ttu-id="36aec-153">Choisissez hello **schémas** vignette.</span><span class="sxs-lookup"><span data-stu-id="36aec-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="36aec-154">Après avoir hello **schémas** panneau s’ouvre, sélectionnez hello schéma de toodelete.</span><span class="sxs-lookup"><span data-stu-id="36aec-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="36aec-155">Sur hello **schémas** panneau, choisissez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="36aec-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Panneau Schémas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="36aec-157">tooconfirm que vous souhaitez toodelete hello sélectionné de schéma, choisissez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="36aec-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Message de confirmation « Supprimer le schéma »](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="36aec-159">Bonjour **schémas** panneau, liste de schéma hello actualise et n’inclut plus schéma hello que vous avez supprimé.</span><span class="sxs-lookup"><span data-stu-id="36aec-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Votre compte d’intégration, avec « Schémas » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="36aec-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36aec-161">Next steps</span></span>
* <span data-ttu-id="36aec-162">[En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration de hello entreprise").</span><span class="sxs-lookup"><span data-stu-id="36aec-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

