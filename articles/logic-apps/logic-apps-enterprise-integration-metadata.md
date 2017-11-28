---
title: "aaaManage intégration de métadonnées de l’artefact - compte Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="46dd6-103">Gestion de métadonnées d’artefact dans des comptes d’intégration pour des applications logiques</span><span class="sxs-lookup"><span data-stu-id="46dd6-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="46dd6-104">Vous pouvez définir des métadonnées personnalisées pour les artefacts dans les comptes d’intégration et récupérer ces métadonnées pendant l’exécution pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="46dd6-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="46dd6-105">Par exemple, vous pouvez spécifier des métadonnées pour les artefacts tels que des partenaires, des contrats, des schémas et mappages - tous stockent les métadonnées à l’aide de paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="46dd6-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="46dd6-106">Actuellement, les artefacts ne peut pas créer les métadonnées via l’interface utilisateur, mais vous pouvez utiliser les API REST toocreate métadonnées.</span><span class="sxs-lookup"><span data-stu-id="46dd6-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="46dd6-107">métadonnées tooadd lorsque vous créez ou sélectionnez un partenaire, un accord ou un schéma Bonjour portail Azure, choisissez **modifier en tant que JSON**.</span><span class="sxs-lookup"><span data-stu-id="46dd6-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="46dd6-108">métadonnées d’artefact tooretrieve dans les applications de la logique, vous pouvez utiliser fonctionnalité d’intégration compte artefact recherche hello.</span><span class="sxs-lookup"><span data-stu-id="46dd6-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="46dd6-109">Ajouter des métadonnées tooartifacts dans les comptes d’intégration</span><span class="sxs-lookup"><span data-stu-id="46dd6-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="46dd6-110">Créez un [compte d’intégration](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="46dd6-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="46dd6-111">Ajouter un compte d’intégration tooyour artefact, par exemple, un [partenaire](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [accord](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), ou [schéma](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="46dd6-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="46dd6-112">Sélectionnez l’artefact de hello, choisissez **modifier en tant que JSON**et entrez les informations de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="46dd6-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Saisie des métadonnées](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="46dd6-114">Récupération des métadonnées à partir d’artefacts pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="46dd6-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="46dd6-115">Créez une [application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="46dd6-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="46dd6-116">Créer un [lien à partir de votre compte d’intégration logique application tooyour](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="46dd6-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="46dd6-117">Dans le Concepteur d’application logique, ajouter un déclencheur comme *demande* ou *HTTP* tooyour logique application.</span><span class="sxs-lookup"><span data-stu-id="46dd6-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="46dd6-118">Choisissez **Étape suivante** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="46dd6-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="46dd6-119">Recherchez *Intégration*, puis recherchez et sélectionnez **Compte d’intégration - Recherche d’artefact de compte d’intégration**.</span><span class="sxs-lookup"><span data-stu-id="46dd6-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Sélectionner Recherche d’artefact de compte d’intégration](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="46dd6-121">Sélectionnez hello **le Type d’artefact**et fournir hello **nom de l’objet**.</span><span class="sxs-lookup"><span data-stu-id="46dd6-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Sélectionner le type d’artefact et spécifiez son nom](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="46dd6-123">Exemple : récupération des métadonnées du partenaire</span><span class="sxs-lookup"><span data-stu-id="46dd6-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="46dd6-124">Les métadonnées du partenaire ont ces détails `routingUrl` :</span><span class="sxs-lookup"><span data-stu-id="46dd6-124">Partner metadata has these `routingUrl` details:</span></span>

![Rechercher des métadonnées de « routingURL » de partenaire](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="46dd6-126">Dans votre application logique, ajoutez votre déclencheur, une action **Compte d’intégration - Recherche d’artefact de compte d’intégration** pour votre partenaire et une requête **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="46dd6-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Ajouter le déclencheur, la recherche de l’artefact et application de « HTTP » tooyour logique](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="46dd6-128">tooretrieve hello URI, accédez tooCode affichage pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="46dd6-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="46dd6-129">La définition de votre application logique doit ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="46dd6-129">Your logic app definition should look like this example:</span></span>

    ![Recherche](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="46dd6-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46dd6-131">Next steps</span></span>
* [<span data-ttu-id="46dd6-132">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="46dd6-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  
