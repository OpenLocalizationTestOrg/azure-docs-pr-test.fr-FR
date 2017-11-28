---
title: "partenaires aaaCreate pour les messages de l’entreprise-entreprise (B2B) - Azure Logic Apps | Documents Microsoft"
description: "Découvrez comment l’intégration de tooyour tooadd partenaires compte avec hello Pack d’intégration Enterprise et Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="2c343-103">Ajout ou mise à jour des partenaires dans les contrats d’entreprise à entreprise de votre flux de travail</span><span class="sxs-lookup"><span data-stu-id="2c343-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="2c343-104">Les partenaires sont des entités qui participent aux transactions d’entreprise à entreprise (B2B) et qui échangent des messages entre eux.</span><span class="sxs-lookup"><span data-stu-id="2c343-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="2c343-105">Avant de pouvoir créer des partenaires qui vous représentent et qui représentent une autre organisation dans le cadre de ces transactions, vous devez partager des informations qui identifient et valident les messages envoyés par chacun.</span><span class="sxs-lookup"><span data-stu-id="2c343-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="2c343-106">Une fois que vous présentent ces détails et que vous êtes prêt toostart votre relation commerciale, vous pouvez créer des partenaires dans votre toorepresent de compte d’intégration vous à la fois.</span><span class="sxs-lookup"><span data-stu-id="2c343-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="2c343-107">Quels rôles jouent les partenaires dans votre compte d’intégration ?</span><span class="sxs-lookup"><span data-stu-id="2c343-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="2c343-108">toodefine plus d’informations sur les messages hello échangés entre partenaires, vous créez des accords entre les partenaires.</span><span class="sxs-lookup"><span data-stu-id="2c343-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="2c343-109">Toutefois, avant de pouvoir créer un accord, vous devez avoir ajouté le compte d’au moins deux serveurs partenaires d’intégration tooyour.</span><span class="sxs-lookup"><span data-stu-id="2c343-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="2c343-110">Votre organisation doit faire partie du contrat de hello hello **partenaire hôte**.</span><span class="sxs-lookup"><span data-stu-id="2c343-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="2c343-111">Hello autre partenaire, ou **partenaire invité** représente hello organisation qui échange des messages avec votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2c343-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="2c343-112">partenaire invité de Hello peut être une autre société, ou même un service de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2c343-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="2c343-113">Après avoir ajouté ces partenaires, vous pouvez créer un contrat.</span><span class="sxs-lookup"><span data-stu-id="2c343-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="2c343-114">Réception et paramètres d’envoi sont orientés hello point de vue de hello Hosted partenaire.</span><span class="sxs-lookup"><span data-stu-id="2c343-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="2c343-115">Par exemple, hello paramètres de réception dans un accord déterminent comment les partenaires hello hébergé reçoit les messages envoyés à partir d’un partenaire invité.</span><span class="sxs-lookup"><span data-stu-id="2c343-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="2c343-116">De même, les paramètres d’envoi hello sur l’accord de hello indiquent comment les partenaires hello hébergé envoie partenaire de messages toohello invité.</span><span class="sxs-lookup"><span data-stu-id="2c343-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="2c343-117">Comment toocreate un partenaire ?</span><span class="sxs-lookup"><span data-stu-id="2c343-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="2c343-118">Bonjour portail Azure, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="2c343-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="2c343-119">Dans la zone de recherche de filtre hello, entrez **intégration**, puis sélectionnez **comptes d’intégration** dans la liste des résultats hello.</span><span class="sxs-lookup"><span data-stu-id="2c343-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="2c343-120">Sélectionnez le compte d’intégration hello où vous souhaitez tooadd vos partenaires.</span><span class="sxs-lookup"><span data-stu-id="2c343-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="2c343-121">Sélectionnez hello **partenaires** vignette.</span><span class="sxs-lookup"><span data-stu-id="2c343-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="2c343-122">Dans le panneau de partenaires hello, choisissez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2c343-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="2c343-123">Entrez un nom pour votre partenaire, puis sélectionnez un **qualificateur**.</span><span class="sxs-lookup"><span data-stu-id="2c343-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="2c343-124">Enfin, vous devez entrer un **valeur** toohelp identifier des documents qui entrent dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="2c343-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="2c343-125">progression de hello toosee pour votre processus de création de partenaire, sélectionnez hello *représentant une cloche* icône de notification.</span><span class="sxs-lookup"><span data-stu-id="2c343-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="2c343-126">tooconfirm vos nouveaux partenaires a été correctement ajouté, sélectionnez hello **partenaires** vignette.</span><span class="sxs-lookup"><span data-stu-id="2c343-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="2c343-127">Une fois que vous sélectionnez la vignette de partenaires hello, vous verrez également partenaires nouvellement ajoutés dans le panneau de partenaires hello.</span><span class="sxs-lookup"><span data-stu-id="2c343-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="2c343-128">Comment des partenaires de tooedit existant dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="2c343-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="2c343-129">Sélectionnez hello **partenaires** vignette.</span><span class="sxs-lookup"><span data-stu-id="2c343-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="2c343-130">Une fois le panneau de partenaires hello s’ouvre, sélectionnez partenaire hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="2c343-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="2c343-131">Sur hello **partenaire de mise à jour** vignette, apportez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="2c343-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="2c343-132">Une fois que vous avez terminé, choisissez **enregistrer**, ou sélectionnez de vos modifications, toocancel **ignorer**.</span><span class="sxs-lookup"><span data-stu-id="2c343-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="2c343-133">Comment toodelete un partenaire</span><span class="sxs-lookup"><span data-stu-id="2c343-133">How toodelete a partner</span></span>

1. <span data-ttu-id="2c343-134">Sélectionnez hello **partenaires** vignette.</span><span class="sxs-lookup"><span data-stu-id="2c343-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="2c343-135">Une fois le panneau de partenaire hello s’ouvre, sélectionnez partenaire hello que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="2c343-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="2c343-136">Choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2c343-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="2c343-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c343-137">Next steps</span></span>
* [<span data-ttu-id="2c343-138">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="2c343-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  

