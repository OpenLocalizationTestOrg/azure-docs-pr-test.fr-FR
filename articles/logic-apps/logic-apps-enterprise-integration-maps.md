---
title: aaaTransform XML avec XSLT mappages - Azure Logic Apps | Documents Microsoft
description: "Ajouter que XSLT mappe des données XML tootransform avec Azure Logic Apps et hello Pack d’intégration Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="b4c29-103">Ajouter des mappages de conversion des données XML</span><span class="sxs-lookup"><span data-stu-id="b4c29-103">Add maps for XML data transform</span></span>

<span data-ttu-id="b4c29-104">Enterprise integration utilise maps tootransform XML des données entre les formats.</span><span class="sxs-lookup"><span data-stu-id="b4c29-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="b4c29-105">Un mappage est un document XML qui définit les données de salutation dans un document qui doit être transformé en un autre format.</span><span class="sxs-lookup"><span data-stu-id="b4c29-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="b4c29-106">Pourquoi utiliser des mappages ?</span><span class="sxs-lookup"><span data-stu-id="b4c29-106">Why use maps?</span></span>

<span data-ttu-id="b4c29-107">Supposons que vous recevez régulièrement B2B commandes ou des factures à partir d’un client qui utilise le format YYYMMDD hello pour les dates.</span><span class="sxs-lookup"><span data-stu-id="b4c29-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="b4c29-108">Toutefois, dans votre organisation, vous stockez les dates au format MMDDYYY hello.</span><span class="sxs-lookup"><span data-stu-id="b4c29-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="b4c29-109">Vous pouvez utiliser un mappage trop*transformer* format de date YYYMMDD hello en hello MMDDYYY avant le stockage des détails de commande ou une facture hello dans votre base de données de l’activité client.</span><span class="sxs-lookup"><span data-stu-id="b4c29-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="b4c29-110">Comment créer un mappage ?</span><span class="sxs-lookup"><span data-stu-id="b4c29-110">How do I create a map?</span></span>

<span data-ttu-id="b4c29-111">Vous pouvez créer des projets d’intégration de BizTalk avec hello [Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration de hello entreprise") pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b4c29-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="b4c29-112">Vous pouvez ensuite créer un fichier de mappage d’intégration qui vous permet de représenter graphiquement les éléments entre les deux fichiers de schéma XML.</span><span class="sxs-lookup"><span data-stu-id="b4c29-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="b4c29-113">Après avoir créé ce projet, vous disposerez d’un document XSLT.</span><span class="sxs-lookup"><span data-stu-id="b4c29-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="b4c29-114">Comment ajouter un mappage ?</span><span class="sxs-lookup"><span data-stu-id="b4c29-114">How do I add a map?</span></span>

1. <span data-ttu-id="b4c29-115">Bonjour portail Azure, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="b4c29-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="b4c29-116">Dans la zone de recherche de filtre hello, entrez **intégration**, puis sélectionnez **comptes d’intégration** à partir de la liste des résultats hello.</span><span class="sxs-lookup"><span data-stu-id="b4c29-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="b4c29-117">Sélectionnez le compte d’intégration hello où vous souhaitez que le plan de hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b4c29-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="b4c29-118">Sélectionnez hello **cartes** vignette.</span><span class="sxs-lookup"><span data-stu-id="b4c29-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="b4c29-119">Une fois que le panneau de mappages hello s’ouvre, choisissez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b4c29-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="b4c29-120">Entrez un **nom** pour votre mappage.</span><span class="sxs-lookup"><span data-stu-id="b4c29-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="b4c29-121">mappage de hello tooupload fichier, choisissez l’icône de dossier hello sur le côté droit de hello Hello **carte** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="b4c29-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="b4c29-122">Après la fin du processus de téléchargement hello, choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4c29-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="b4c29-123">Une fois Azure ajoute le compte d’intégration tooyour hello carte, vous obtenez un message à l’écran qui affiche si votre fichier de mappage a été ajoutée ou non.</span><span class="sxs-lookup"><span data-stu-id="b4c29-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="b4c29-124">Une fois que vous obtenez ce message, choisissez hello **cartes** vignette afin que vous puissiez afficher hello qui vient d’être ajouté de mappage.</span><span class="sxs-lookup"><span data-stu-id="b4c29-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="b4c29-125">Comment modifier un mappage ?</span><span class="sxs-lookup"><span data-stu-id="b4c29-125">How do I edit a map?</span></span>

<span data-ttu-id="b4c29-126">Vous devez télécharger un nouveau fichier de mappage avec les modifications hello que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b4c29-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="b4c29-127">Vous pouvez tout d’abord télécharger carte hello pour la modification.</span><span class="sxs-lookup"><span data-stu-id="b4c29-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="b4c29-128">tooupload un nouveau mappage qui remplace le mappage existant de hello, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="b4c29-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="b4c29-129">Choisissez hello **cartes** vignette.</span><span class="sxs-lookup"><span data-stu-id="b4c29-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="b4c29-130">Une fois le panneau de mappages hello s’ouvre, sélectionnez hello mappage que tooedit.</span><span class="sxs-lookup"><span data-stu-id="b4c29-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="b4c29-131">Sur hello **cartes** panneau, choisissez **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="b4c29-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="b4c29-132">Dans le sélecteur de fichier hello, sélectionnez le fichier de mappage de hello que vous souhaitez tooupload, puis sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="b4c29-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="b4c29-133">Comment toodelete une carte ?</span><span class="sxs-lookup"><span data-stu-id="b4c29-133">How toodelete a map?</span></span>

1. <span data-ttu-id="b4c29-134">Choisissez hello **cartes** vignette.</span><span class="sxs-lookup"><span data-stu-id="b4c29-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="b4c29-135">Une fois le panneau de mappages hello s’ouvre, sélectionnez le mappage hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="b4c29-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="b4c29-136">Choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b4c29-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="b4c29-137">Confirmer la carte de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="b4c29-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="b4c29-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b4c29-138">Next Steps</span></span>
* [<span data-ttu-id="b4c29-139">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="b4c29-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")  
* [<span data-ttu-id="b4c29-140">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="b4c29-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  
* [<span data-ttu-id="b4c29-141">En savoir plus sur les transformations</span><span class="sxs-lookup"><span data-stu-id="b4c29-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Découvrez les transformations d’intégration d’entreprise")  

