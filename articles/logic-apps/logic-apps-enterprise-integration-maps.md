---
title: "Convertir des données XML avec des mappages XSLT - Azure Logic Apps | Microsoft Docs"
description: "Ajouter des mappages XSLT pour convertir des données XML avec Azure Logic Apps et Enterprise Integration Pack"
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
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="6970d-103">Ajouter des mappages de conversion des données XML</span><span class="sxs-lookup"><span data-stu-id="6970d-103">Add maps for XML data transform</span></span>

<span data-ttu-id="6970d-104">Enterprise Integration utilise des mappages pour convertir les données XML d’un format vers un autre.</span><span class="sxs-lookup"><span data-stu-id="6970d-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="6970d-105">Un mappage est un document XML qui définit les données d’un document qui doivent être converties dans un autre format.</span><span class="sxs-lookup"><span data-stu-id="6970d-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="6970d-106">Pourquoi utiliser des mappages ?</span><span class="sxs-lookup"><span data-stu-id="6970d-106">Why use maps?</span></span>

<span data-ttu-id="6970d-107">Imaginons que vous recevez régulièrement des commandes ou des factures B2B de la part d’un client qui utilise le format AAAMMJJ pour les dates.</span><span class="sxs-lookup"><span data-stu-id="6970d-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="6970d-108">Mais dans votre entreprise, les dates sont enregistrées au format MMJJAAA.</span><span class="sxs-lookup"><span data-stu-id="6970d-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="6970d-109">Vous pouvez utiliser un mappage pour *convertir* le format de date AAAMMJJ vers MMJJAAA avant d'enregistrer les détails de la commande ou de la facture dans votre base de données clients.</span><span class="sxs-lookup"><span data-stu-id="6970d-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="6970d-110">Comment créer un mappage ?</span><span class="sxs-lookup"><span data-stu-id="6970d-110">How do I create a map?</span></span>

<span data-ttu-id="6970d-111">Vous pouvez créer des projets d’intégration BizTalk grâce à [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "En savoir plus sur Enterprise Integration Pack") pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6970d-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="6970d-112">Vous pouvez ensuite créer un fichier de mappage d’intégration qui vous permet de représenter graphiquement les éléments entre les deux fichiers de schéma XML.</span><span class="sxs-lookup"><span data-stu-id="6970d-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="6970d-113">Après avoir créé ce projet, vous disposerez d’un document XSLT.</span><span class="sxs-lookup"><span data-stu-id="6970d-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="6970d-114">Comment ajouter un mappage ?</span><span class="sxs-lookup"><span data-stu-id="6970d-114">How do I add a map?</span></span>

1. <span data-ttu-id="6970d-115">Dans le portail Azure, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="6970d-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="6970d-116">Entrez **intégration** dans la zone de recherche de filtre et sélectionnez **Comptes d’intégration** dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="6970d-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="6970d-117">Sélectionnez le compte d’intégration auquel vous souhaitez ajouter le mappage.</span><span class="sxs-lookup"><span data-stu-id="6970d-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="6970d-118">Sélectionnez la mosaïque **Mappages**.</span><span class="sxs-lookup"><span data-stu-id="6970d-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="6970d-119">Une fois le panneau Mappages ouvert, choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6970d-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="6970d-120">Entrez un **nom** pour votre mappage.</span><span class="sxs-lookup"><span data-stu-id="6970d-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="6970d-121">Pour télécharger le fichier de mappage, sélectionnez l’icône de dossier située à droite de la zone de texte **Mappage**.</span><span class="sxs-lookup"><span data-stu-id="6970d-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="6970d-122">Une fois le processus de téléchargement terminé, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="6970d-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="6970d-123">Une fois qu’Azure ajoute le mappage à votre compte d’intégration, vous obtenez un message à l’écran qui indique si votre fichier de mappage a été ajouté ou non.</span><span class="sxs-lookup"><span data-stu-id="6970d-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="6970d-124">Une fois que vous obtenez ce message, choisissez la mosaïque **Mappages** pour pouvoir afficher le mappage ajouté.</span><span class="sxs-lookup"><span data-stu-id="6970d-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="6970d-125">Comment modifier un mappage ?</span><span class="sxs-lookup"><span data-stu-id="6970d-125">How do I edit a map?</span></span>

<span data-ttu-id="6970d-126">Vous devez télécharger un nouveau fichier de mappage intégrant les modifications souhaitées.</span><span class="sxs-lookup"><span data-stu-id="6970d-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="6970d-127">Vous pouvez d’abord télécharger le mappage pour modification.</span><span class="sxs-lookup"><span data-stu-id="6970d-127">You can first download the map for editing.</span></span>

<span data-ttu-id="6970d-128">Pour télécharger un nouveau mappage remplaçant un mappage existant, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6970d-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="6970d-129">Choisissez la mosaïque **Mappages**.</span><span class="sxs-lookup"><span data-stu-id="6970d-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="6970d-130">Dans le panneau Mappages qui s’affiche, sélectionnez le mappage que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="6970d-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="6970d-131">Dans le panneau **Mappage**, choisissez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="6970d-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="6970d-132">Dans le sélecteur de fichiers, sélectionnez le fichier de mappage que vous souhaitez télécharger, puis sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="6970d-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="6970d-133">Comment supprimer un mappage ?</span><span class="sxs-lookup"><span data-stu-id="6970d-133">How to delete a map?</span></span>

1. <span data-ttu-id="6970d-134">Choisissez la mosaïque **Mappages**.</span><span class="sxs-lookup"><span data-stu-id="6970d-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="6970d-135">Dans le panneau Mappages qui s’affiche, sélectionnez le mappage que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="6970d-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="6970d-136">Choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6970d-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="6970d-137">Confirmez que vous souhaitez supprimer le mappage.</span><span class="sxs-lookup"><span data-stu-id="6970d-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="6970d-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6970d-138">Next Steps</span></span>
* [<span data-ttu-id="6970d-139">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6970d-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack")  
* [<span data-ttu-id="6970d-140">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="6970d-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  
* [<span data-ttu-id="6970d-141">En savoir plus sur les transformations</span><span class="sxs-lookup"><span data-stu-id="6970d-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Découvrez les transformations d’intégration d’entreprise")  

