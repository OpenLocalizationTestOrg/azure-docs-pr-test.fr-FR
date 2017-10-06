---
title: solutions aaaCreate B2B - Azure Logic Apps | Documents Microsoft
description: "Recevoir des données dans les applications de la logique à l’aide des fonctionnalités de hello B2B Bonjour Pack d’intégration Enterprise"
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
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="f5a51-103">Recevoir des données dans les applications logique avec les fonctionnalités de B2B hello Bonjour Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="f5a51-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="f5a51-104">Après avoir créé un compte d’intégration qui a des partenaires et des accords, vous êtes prêt toocreate un workflow toobusiness (B2B) d’entreprise pour votre application logique avec hello [Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5a51-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5a51-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f5a51-105">Prerequisites</span></span>

<span data-ttu-id="f5a51-106">toouse hello AS2 et X12 actions, vous devez disposer d’un compte d’intégration d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="f5a51-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="f5a51-107">En savoir plus [comment toocreate une intégration compte](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f5a51-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="f5a51-108">Créer une application logique avec des connecteurs B2B</span><span class="sxs-lookup"><span data-stu-id="f5a51-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="f5a51-109">Suivez ces étapes toocreate un B2B logique application utilise hello AS2 et X12 données de tooreceive d’actions à partir d’un partenaire commercial :</span><span class="sxs-lookup"><span data-stu-id="f5a51-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="f5a51-110">Créer une application logique, puis [lier votre compte d’intégration application tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f5a51-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="f5a51-111">Ajouter un **demande - HTTP lors de la demande est reçue** application logique de tooyour déclencheur.</span><span class="sxs-lookup"><span data-stu-id="f5a51-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="f5a51-112">tooadd hello **AS2 de décoder** action, sélectionnez **ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="f5a51-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="f5a51-113">toofilter tous les toohello actions une que vous le souhaitez, entrez le mot de hello **as2** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="f5a51-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="f5a51-114">Sélectionnez hello **AS2 - message AS2 de décoder** action.</span><span class="sxs-lookup"><span data-stu-id="f5a51-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="f5a51-115">Ajouter hello **corps** que vous souhaitez toouse en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="f5a51-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="f5a51-116">Dans cet exemple, sélectionnez hello le corps de requête HTTP de hello que déclencheurs hello application logique.</span><span class="sxs-lookup"><span data-stu-id="f5a51-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="f5a51-117">Ou entrez une expression qui transmet les en-têtes hello Bonjour **en-têtes** champ :</span><span class="sxs-lookup"><span data-stu-id="f5a51-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="f5a51-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="f5a51-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="f5a51-119">Ajouter hello requis **en-têtes** pour AS2, que vous pouvez trouver dans les en-têtes de demande hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5a51-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="f5a51-120">Dans cet exemple, sélectionnez les en-têtes de requête HTTP de hello hello cette application de la logique de déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="f5a51-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="f5a51-121">À présent ajouter l’action du message Decode X12 hello.</span><span class="sxs-lookup"><span data-stu-id="f5a51-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="f5a51-122">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="f5a51-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="f5a51-123">toofilter tous les toohello actions une que vous le souhaitez, entrez le mot de hello **x12** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="f5a51-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="f5a51-124">Sélectionnez hello **X12-décoder X12 message** action.</span><span class="sxs-lookup"><span data-stu-id="f5a51-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="f5a51-125">Maintenant, vous devez spécifier hello toothis d’entrée action.</span><span class="sxs-lookup"><span data-stu-id="f5a51-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="f5a51-126">Cette entrée est sortie hello à partir de l’action de AS2 hello précédente.</span><span class="sxs-lookup"><span data-stu-id="f5a51-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="f5a51-127">Hello contenu réel du message est dans un objet JSON et encodage base64, vous devez spécifier une expression en tant qu’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="f5a51-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="f5a51-128">Entrez hello expression Bonjour suivante **X12 plats tooDECODE MESSAGE de fichier** champ d’entrée :</span><span class="sxs-lookup"><span data-stu-id="f5a51-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="f5a51-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="f5a51-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="f5a51-130">Maintenant ajouter des étapes, les données de salutation X12 toodecode reçu hello partenaire commercial et les éléments dans un objet JSON de sortie.</span><span class="sxs-lookup"><span data-stu-id="f5a51-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="f5a51-131">partenaire hello toonotify hello de données a été reçu, vous pouvez envoyer une réponse contenant hello AS2 Notification MDN (Message Disposition) dans une Action de réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5a51-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="f5a51-132">tooadd hello **réponse** action, choisissez **ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="f5a51-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="f5a51-133">toofilter tous les toohello actions une que vous le souhaitez, entrez le mot de hello **réponse** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="f5a51-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="f5a51-134">Sélectionnez hello **réponse** action.</span><span class="sxs-lookup"><span data-stu-id="f5a51-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="f5a51-135">tooaccess hello MDN à partir de la sortie de hello Hello **message de décodage X12** action, réponse hello **corps** champ avec cette expression :</span><span class="sxs-lookup"><span data-stu-id="f5a51-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="f5a51-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="f5a51-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="f5a51-137">Enregistrez votre travail.</span><span class="sxs-lookup"><span data-stu-id="f5a51-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="f5a51-138">Vous avez maintenant terminé la configuration de votre application logique B2B.</span><span class="sxs-lookup"><span data-stu-id="f5a51-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="f5a51-139">Dans une application réelle, vous souhaiterez toostore hello décodée X12 les données dans un magasin de données ou d’application (LOB) de line-of-business.</span><span class="sxs-lookup"><span data-stu-id="f5a51-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="f5a51-140">tooconnect vos propres applications métier et utilisez ces API dans votre application logique, vous pouvez ajouter d’autres actions ou écrire des API personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f5a51-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="f5a51-141">Fonctionnalités et cas d’usage</span><span class="sxs-lookup"><span data-stu-id="f5a51-141">Features and use cases</span></span>

* <span data-ttu-id="f5a51-142">X12 Hello AS2 décoder et encoder les actions permettent d’échanger des données entre les partenaires commerciaux à l’aide de protocoles standard dans les applications de la logique.</span><span class="sxs-lookup"><span data-stu-id="f5a51-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="f5a51-143">tooexchange des données avec des partenaires commerciaux, vous pouvez utiliser AS2 et X12 avec ou sans eux.</span><span class="sxs-lookup"><span data-stu-id="f5a51-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="f5a51-144">actions de B2B Hello vous aider à créer facilement des partenaires et des accords dans votre compte d’intégration et de les utiliser dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="f5a51-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="f5a51-145">En étendant votre application logique avec d’autres actions, vous pouvez envoyer et recevoir des données vers et depuis d’autres applications et services tels que SalesForce.</span><span class="sxs-lookup"><span data-stu-id="f5a51-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f5a51-146">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="f5a51-146">Learn more</span></span>
[<span data-ttu-id="f5a51-147">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="f5a51-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
