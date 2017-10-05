---
title: "Gestion des métadonnées d’artefact de compte d’intégration - Azure Logic Apps | Microsoft Docs"
description: "Ajout ou suppression de métadonnées d’artefact à partir de comptes d’intégration pour Azure Logic Apps"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="b19a7-103">Gestion de métadonnées d’artefact dans des comptes d’intégration pour des applications logiques</span><span class="sxs-lookup"><span data-stu-id="b19a7-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="b19a7-104">Vous pouvez définir des métadonnées personnalisées pour les artefacts dans les comptes d’intégration et récupérer ces métadonnées pendant l’exécution pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b19a7-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="b19a7-105">Par exemple, vous pouvez spécifier des métadonnées pour les artefacts tels que des partenaires, des contrats, des schémas et mappages - tous stockent les métadonnées à l’aide de paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="b19a7-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="b19a7-106">Actuellement, les artefacts ne peuvent pas créer de métadonnées via l’interface utilisateur, mais vous pouvez utiliser l’API REST pour créer des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="b19a7-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="b19a7-107">Pour ajouter des métadonnées lorsque vous créez ou sélectionnez un partenaire, un accord ou un schéma dans le portail Azure, choisissez **Modifier au format JSON**.</span><span class="sxs-lookup"><span data-stu-id="b19a7-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="b19a7-108">Pour récupérer des métadonnées d’artefact dans des applications logiques, vous pouvez utiliser la fonctionnalité de Recherche d’artefact de compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="b19a7-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="b19a7-109">Ajoute de métadonnées à des artefacts dans des comptes d’intégration</span><span class="sxs-lookup"><span data-stu-id="b19a7-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="b19a7-110">Créez un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="b19a7-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="b19a7-111">Ajoutez un artefact à votre compte d’intégration, par exemple, un [partenaire](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), un [contrat](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements) ou un [schéma](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="b19a7-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="b19a7-112">Sélectionnez l’artefact. choisissez **Modifier au format JSON** et entrez les informations des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="b19a7-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Saisie des métadonnées](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="b19a7-114">Récupération des métadonnées à partir d’artefacts pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="b19a7-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="b19a7-115">Créez une [application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b19a7-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="b19a7-116">Créez un [lien de votre application logique vers votre compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="b19a7-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="b19a7-117">Dans le Concepteur d’application logique, ajoutez un déclencheur comme *Request* ou *HTTP* à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b19a7-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="b19a7-118">Choisissez **Étape suivante** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="b19a7-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="b19a7-119">Recherchez *Intégration*, puis recherchez et sélectionnez **Compte d’intégration - Recherche d’artefact de compte d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="b19a7-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Sélectionner Recherche d’artefact de compte d’intégration](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="b19a7-121">Sélectionnez le **type d’artefact** et indiquez son **nom**.</span><span class="sxs-lookup"><span data-stu-id="b19a7-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Sélectionner le type d’artefact et spécifiez son nom](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="b19a7-123">Exemple : récupération des métadonnées du partenaire</span><span class="sxs-lookup"><span data-stu-id="b19a7-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="b19a7-124">Les métadonnées du partenaire ont ces détails `routingUrl` :</span><span class="sxs-lookup"><span data-stu-id="b19a7-124">Partner metadata has these `routingUrl` details:</span></span>

![Rechercher des métadonnées de « routingURL » de partenaire](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="b19a7-126">Dans votre application logique, ajoutez votre déclencheur, une action **Compte d’intégration - Recherche d’artefact de compte d’intégration** pour votre partenaire et une requête **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="b19a7-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Ajouter un déclencheur, une recherche d’artefact et « HTTP » à votre application logique](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="b19a7-128">Pour récupérer l’URI, passez en mode Code pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b19a7-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="b19a7-129">La définition de votre application logique doit ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="b19a7-129">Your logic app definition should look like this example:</span></span>

    ![Recherche](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="b19a7-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b19a7-131">Next steps</span></span>
* [<span data-ttu-id="b19a7-132">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="b19a7-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  
