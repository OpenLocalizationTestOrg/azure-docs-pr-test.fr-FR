---
title: "Schémas de validation XML - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="02354-103">Valider des documents XML avec des schémas pour Azure Logic Apps et Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="02354-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="02354-104">Les schémas confirment que les documents XML que vous recevez sont valides et contiennent les données attendues dans un format prédéfini.</span><span class="sxs-lookup"><span data-stu-id="02354-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="02354-105">Les schémas aident également à valider les messages échangés dans un scénario d’entreprise à entreprise (B2B).</span><span class="sxs-lookup"><span data-stu-id="02354-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="02354-106">Ajout d’un schéma</span><span class="sxs-lookup"><span data-stu-id="02354-106">Add a schema</span></span>

1. <span data-ttu-id="02354-107">Dans le portail Azure, cliquez sur **Plus de services**.</span><span class="sxs-lookup"><span data-stu-id="02354-107">In the Azure portal, select **More services**.</span></span>

    ![Portail Azure, « Plus de services »](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="02354-109">Entrez **intégration** dans la zone de recherche de filtre et sélectionnez **Integration Accounts** (Comptes d’intégration) dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="02354-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Zone de recherche de filtre](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="02354-111">Sélectionnez le **compte d’intégration** auquel vous souhaitez ajouter le schéma.</span><span class="sxs-lookup"><span data-stu-id="02354-111">Select the **integration account** where you want to add the schema.</span></span>

    ![Liste des comptes d’intégration](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="02354-113">Choisissez la mosaïque **Schémas**.</span><span class="sxs-lookup"><span data-stu-id="02354-113">Choose the **Schemas** tile.</span></span>

    ![Exemple de compte d’intégration, « Schémas »](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="02354-115">Ajout d’un fichier de schéma d’une taille inférieure à 2 Mo</span><span class="sxs-lookup"><span data-stu-id="02354-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="02354-116">Dans le panneau **Schémas** qui s’affiche (après les étapes précédentes), sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="02354-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Panneau Schémas, « Ajouter »](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="02354-118">Saisissez un nom pour votre schéma.</span><span class="sxs-lookup"><span data-stu-id="02354-118">Enter a name for your schema.</span></span> <span data-ttu-id="02354-119">Téléchargez le fichier de schéma en sélectionnant l’icône de dossier à côté de la zone **Schéma**.</span><span class="sxs-lookup"><span data-stu-id="02354-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="02354-120">Une fois le processus de téléchargement terminé, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="02354-120">After the upload process completes, select **OK**.</span></span>

    ![Capture d’écran d’« Ajouter un schéma » avec « Fichier de petite taille » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="02354-122">Ajout d’un fichier de schéma d’une taille supérieure à 2 Mo (jusqu’à un maximum de 8 Mo)</span><span class="sxs-lookup"><span data-stu-id="02354-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="02354-123">Ces étapes varient selon le niveau d’accès du conteneur d’objets blob : **Public** ou **No anonymous access** (Aucun accès anonyme).</span><span class="sxs-lookup"><span data-stu-id="02354-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="02354-124">**Pour déterminer ce niveau d’accès**</span><span class="sxs-lookup"><span data-stu-id="02354-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="02354-125">Ouvrez **l’Explorateur de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="02354-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="02354-126">Sous **Conteneurs d’objets Blob**, sélectionnez le conteneur d’objets blob de votre choix.</span><span class="sxs-lookup"><span data-stu-id="02354-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="02354-127">Sélectionnez **Sécurité**, **Niveau d’accès**.</span><span class="sxs-lookup"><span data-stu-id="02354-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="02354-128">Si le niveau d’accès de sécurité d’objet blob est **Public**, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="02354-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Explorateur de stockage Azure, avec « Conteneurs d’objets Blob », « Sécurité » et « Public » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="02354-130">Téléchargez le schéma vers votre compte de stockage, puis copiez l’URI.</span><span class="sxs-lookup"><span data-stu-id="02354-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Compte de stockage avec l’URI mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="02354-132">Sélectionnez **Fichier volumineux** dans **Ajouter un schéma** et indiquez l’URI dans la zone de texte **URI du contenu**.</span><span class="sxs-lookup"><span data-stu-id="02354-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Schémas, avec le bouton « Ajouter » et « Fichier volumineux » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="02354-134">Si le niveau de sécurité de l’accès aux objets blob est défini sur **Pas d’accès anonyme**.</span><span class="sxs-lookup"><span data-stu-id="02354-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Explorateur de stockage Azure, avec « Conteneurs d’objets Blob », « Sécurité » et « No anonymous access » (Aucun accès anonyme) mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="02354-136">Téléchargez le schéma vers votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="02354-136">Upload the schema to your storage account.</span></span>

    ![Compte de stockage](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="02354-138">Générez un URI de signature d’accès partagé pour le schéma.</span><span class="sxs-lookup"><span data-stu-id="02354-138">Generate a shared access signature for the schema.</span></span>

    ![Compte de stockage, avec l’onglet des signatures d’accès partagé mis en surbrillance](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="02354-140">Sélectionnez **Fichier volumineux** dans **Ajouter un schéma** et indiquez l’URI de signature d’accès partagé dans la zone de texte **URI du contenu**.</span><span class="sxs-lookup"><span data-stu-id="02354-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Schémas, avec le bouton « Ajouter » et « Fichier volumineux » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="02354-142">Dans le panneau **Schémas** de votre compte d’intégration, votre nouveau schéma doit maintenant s’afficher.</span><span class="sxs-lookup"><span data-stu-id="02354-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Votre compte d’intégration, avec « Schémas » et le nouveau schéma mis en surbrillance](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="02354-144">Modification de schémas</span><span class="sxs-lookup"><span data-stu-id="02354-144">Edit schemas</span></span>

1. <span data-ttu-id="02354-145">Choisissez la mosaïque **Schémas**.</span><span class="sxs-lookup"><span data-stu-id="02354-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="02354-146">Dans le panneau **Schémas** qui s’affiche, sélectionnez le schéma que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="02354-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="02354-147">Dans le panneau **Schémas**, sélectionnez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="02354-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Panneau Schémas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="02354-149">Sélectionnez le fichier de schéma que vous souhaitez modifier, puis cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="02354-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Ouvrir le fichier de schéma à modifier](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="02354-151">Azure affiche un message indiquant que le schéma a été téléchargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="02354-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="02354-152">Suppression de schémas</span><span class="sxs-lookup"><span data-stu-id="02354-152">Delete schemas</span></span>

1. <span data-ttu-id="02354-153">Choisissez la mosaïque **Schémas**.</span><span class="sxs-lookup"><span data-stu-id="02354-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="02354-154">Dans le panneau **Schémas** qui s’affiche, sélectionnez le schéma que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="02354-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="02354-155">Dans le panneau **Schémas**, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="02354-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Panneau Schémas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="02354-157">Pour confirmer que vous souhaitez supprimer le schéma sélectionné, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="02354-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![Message de confirmation « Supprimer le schéma »](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="02354-159">Dans le panneau **Schémas**, la liste des schémas est actualisée et n’inclut plus le schéma que vous avez supprimé.</span><span class="sxs-lookup"><span data-stu-id="02354-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![Votre compte d’intégration, avec « Schémas » mis en surbrillance](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="02354-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02354-161">Next steps</span></span>
* <span data-ttu-id="02354-162">[En savoir plus sur Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "En savoir plus sur Enterprise Integration Pack").</span><span class="sxs-lookup"><span data-stu-id="02354-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

