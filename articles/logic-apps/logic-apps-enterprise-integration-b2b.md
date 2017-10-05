---
title: "Créer des solutions B2B - Azure Logic Apps | Microsoft Docs"
description: "Recevoir des données dans des applications logiques à l’aide des fonctionnalités B2B dans Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="6ff09-103">Recevoir des données dans des applications logiques à l’aide des fonctionnalités B2B dans Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6ff09-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="6ff09-104">Après avoir créé un compte d’intégration comportant des partenaires et des contrats, vous êtes prêt à créer un workflow interentreprises (B2B) pour votre application logique avec [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ff09-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ff09-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6ff09-105">Prerequisites</span></span>

<span data-ttu-id="6ff09-106">Pour utiliser les actions AS2 et X12, vous devez disposer d’un compte Enterprise Integration.</span><span class="sxs-lookup"><span data-stu-id="6ff09-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="6ff09-107">Découvrez [comment créer un compte Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="6ff09-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="6ff09-108">Créer une application logique avec des connecteurs B2B</span><span class="sxs-lookup"><span data-stu-id="6ff09-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="6ff09-109">Suivez ces étapes pour créer une application logique B2B qui utilise les actions AS2 et X12 pour recevoir des données d’un partenaire commercial :</span><span class="sxs-lookup"><span data-stu-id="6ff09-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="6ff09-110">Créez une application logique, puis [liez-la à votre compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="6ff09-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="6ff09-111">Ajoutez un déclencheur **Requête - Lors de la réception d’une requête HTTP** à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="6ff09-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="6ff09-112">Pour ajouter l’action **Decode AS2**, sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6ff09-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="6ff09-113">Pour filtrer toutes les actions et obtenir celle que vous souhaitez utiliser, entrez le mot **as2** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="6ff09-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="6ff09-114">Sélectionnez l’action **AS2 - Decode AS2 message**.</span><span class="sxs-lookup"><span data-stu-id="6ff09-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="6ff09-115">Ajoutez le **corps** que vous souhaitez utiliser comme entrée.</span><span class="sxs-lookup"><span data-stu-id="6ff09-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="6ff09-116">Dans cet exemple, sélectionnez le corps de la demande HTTP qui a déclenché l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6ff09-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="6ff09-117">Ou entrez une expression qui saisit les en-têtes dans le champ **EN-TÊTES** :</span><span class="sxs-lookup"><span data-stu-id="6ff09-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="6ff09-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="6ff09-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="6ff09-119">Ajoutez les **en-têtes** requis pour AS2, que vous pouvez trouver dans les en-têtes de requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ff09-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="6ff09-120">Dans cet exemple, sélectionnez les en-têtes de la requête HTTP qui déclenche l’application logique.</span><span class="sxs-lookup"><span data-stu-id="6ff09-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="6ff09-121">Ajoutez maintenant l’action du message Decode X12.</span><span class="sxs-lookup"><span data-stu-id="6ff09-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="6ff09-122">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6ff09-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="6ff09-123">Pour filtrer toutes les actions et obtenir celle que vous souhaitez utiliser, entrez le mot **x12** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="6ff09-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="6ff09-124">Sélectionnez l’action **X12 - Decode X12 message**.</span><span class="sxs-lookup"><span data-stu-id="6ff09-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="6ff09-125">Vous devez maintenant spécifier l’entrée de cette action.</span><span class="sxs-lookup"><span data-stu-id="6ff09-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="6ff09-126">Cette entrée est le résultat de l’action AS2 précédente.</span><span class="sxs-lookup"><span data-stu-id="6ff09-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="6ff09-127">Le contenu réel du message est dans un objet JSON encodé au format Base64. Vous devez donc spécifier une expression comme entrée.</span><span class="sxs-lookup"><span data-stu-id="6ff09-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="6ff09-128">Entrez l’expression suivante dans le champ de saisie **X12 FLAT FILE MESSAGE TO DECODE** (MESSAGE DE FICHIER PLAT X12 À DÉCODER) :</span><span class="sxs-lookup"><span data-stu-id="6ff09-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="6ff09-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="6ff09-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="6ff09-130">Ajoutez des étapes permettant de décoder les données X12 provenant d’un partenaire commercial et de générer des éléments dans un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="6ff09-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="6ff09-131">Pour informer le partenaire de la réception des données, vous pouvez renvoyer une réponse contenant l’élément AS2 Message Disposition Notification (MDN) dans une action Response HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ff09-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="6ff09-132">Pour ajouter l’action **Response**, sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="6ff09-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="6ff09-133">Pour filtrer toutes les actions et obtenir celle que vous souhaitez utiliser, entrez le mot **response** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="6ff09-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="6ff09-134">Sélectionner l’action **Response**.</span><span class="sxs-lookup"><span data-stu-id="6ff09-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="6ff09-135">Pour accéder à l’élément MDN à partir de la sortie de l’action **Decode X12 message**, définissez le champ de réponse **CORPS** à l’aide de l’expression suivante :</span><span class="sxs-lookup"><span data-stu-id="6ff09-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="6ff09-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="6ff09-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="6ff09-137">Enregistrez votre travail.</span><span class="sxs-lookup"><span data-stu-id="6ff09-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="6ff09-138">Vous avez maintenant terminé la configuration de votre application logique B2B.</span><span class="sxs-lookup"><span data-stu-id="6ff09-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="6ff09-139">Dans une application réelle, vous souhaiterez peut-être stocker les données X12 décodées dans une application métier ou un magasin de données.</span><span class="sxs-lookup"><span data-stu-id="6ff09-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="6ff09-140">Pour vous connecter à vos propres applications métier puis utiliser ces API dans votre application logique, vous pouvez ajouter des actions supplémentaires ou écrire des API personnalisées.</span><span class="sxs-lookup"><span data-stu-id="6ff09-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="6ff09-141">Fonctionnalités et cas d’usage</span><span class="sxs-lookup"><span data-stu-id="6ff09-141">Features and use cases</span></span>

* <span data-ttu-id="6ff09-142">Les actions de codage et de décodage AS2 et X12 permettent d’échanger des données entre les partenaires commerciaux à l’aide de protocoles standard dans les applications logiques.</span><span class="sxs-lookup"><span data-stu-id="6ff09-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="6ff09-143">Pour échanger des données avec des partenaires commerciaux, vous pouvez utiliser AS2 et X12 ensemble ou de façon isolée.</span><span class="sxs-lookup"><span data-stu-id="6ff09-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="6ff09-144">Les actions B2B facilitent la création de partenaires et de contrats dans votre compte d’intégration et leur utilisation dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="6ff09-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="6ff09-145">En étendant votre application logique avec d’autres actions, vous pouvez envoyer et recevoir des données vers et depuis d’autres applications et services tels que SalesForce.</span><span class="sxs-lookup"><span data-stu-id="6ff09-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="6ff09-146">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="6ff09-146">Learn more</span></span>
[<span data-ttu-id="6ff09-147">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="6ff09-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
