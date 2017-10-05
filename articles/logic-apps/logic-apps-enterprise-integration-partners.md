---
title: "Création de partenaires pour les messages d’entreprise à entreprise (B2B) - Azure Logic Apps | Microsoft Docs"
description: "Découvrez comment ajouter des partenaires à votre compte d’intégration avec Enterprise Integration Pack et Logic Apps"
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
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="8a16b-103">Ajout ou mise à jour des partenaires dans les contrats d’entreprise à entreprise de votre flux de travail</span><span class="sxs-lookup"><span data-stu-id="8a16b-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="8a16b-104">Les partenaires sont des entités qui participent aux transactions d’entreprise à entreprise (B2B) et qui échangent des messages entre eux.</span><span class="sxs-lookup"><span data-stu-id="8a16b-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="8a16b-105">Avant de pouvoir créer des partenaires qui vous représentent et qui représentent une autre organisation dans le cadre de ces transactions, vous devez partager des informations qui identifient et valident les messages envoyés par chacun.</span><span class="sxs-lookup"><span data-stu-id="8a16b-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="8a16b-106">Après avoir discuté de ces détails et quand vous serez prêt à initier cette relation commerciale, vous pouvez créer des partenaires dans votre compte d’intégration pour vous représenter, ainsi que l’organisation.</span><span class="sxs-lookup"><span data-stu-id="8a16b-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="8a16b-107">Quels rôles jouent les partenaires dans votre compte d’intégration ?</span><span class="sxs-lookup"><span data-stu-id="8a16b-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="8a16b-108">Pour définir les détails relatifs aux messages échangés entre les partenaires, vous pouvez créer des contrats entre ces partenaires.</span><span class="sxs-lookup"><span data-stu-id="8a16b-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="8a16b-109">Toutefois, avant de pouvoir créer un contrat, vous devez avoir ajouté au moins deux partenaires à votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="8a16b-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="8a16b-110">Votre organisation doit faire partie du contrat, en tant que **partenaire hôte**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="8a16b-111">L’autre partenaire, ou **partenaire invité**, représente l’organisation qui échange des messages avec votre organisation.</span><span class="sxs-lookup"><span data-stu-id="8a16b-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="8a16b-112">Le partenaire invité peut être une autre entreprise ou même un service au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="8a16b-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="8a16b-113">Après avoir ajouté ces partenaires, vous pouvez créer un contrat.</span><span class="sxs-lookup"><span data-stu-id="8a16b-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="8a16b-114">Les paramètres de réception et d’envoi sont basés du point de vue du partenaire hébergé.</span><span class="sxs-lookup"><span data-stu-id="8a16b-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="8a16b-115">Par exemple, les paramètres de réception dans un contrat déterminent la façon dont le partenaire hébergé reçoit les messages envoyés à partir d’un partenaire invité.</span><span class="sxs-lookup"><span data-stu-id="8a16b-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="8a16b-116">De même, les paramètres d’envoi du contrat indiquent la façon dont le partenaire hébergé envoie des messages au partenaire invité.</span><span class="sxs-lookup"><span data-stu-id="8a16b-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="8a16b-117">Création d’un partenaire</span><span class="sxs-lookup"><span data-stu-id="8a16b-117">How to create a partner?</span></span>

1. <span data-ttu-id="8a16b-118">Dans le portail Azure, sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="8a16b-119">Entrez **intégration** dans la zone de recherche de filtre et sélectionnez **Comptes d’intégration** dans la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="8a16b-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="8a16b-120">Sélectionnez le compte d’intégration dans lequel vous souhaitez ajouter vos partenaires.</span><span class="sxs-lookup"><span data-stu-id="8a16b-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="8a16b-121">Sélectionnez la mosaïque **Partenaires**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="8a16b-122">Dans le panneau Partenaires, choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="8a16b-123">Entrez un nom pour votre partenaire, puis sélectionnez un **qualificateur**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="8a16b-124">Enfin, entrez une **valeur** pour identifier les documents qui entrent dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="8a16b-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="8a16b-125">Sélectionnez l’icône de notification en forme de *cloche* pour afficher la progression du processus de création du partenaire.</span><span class="sxs-lookup"><span data-stu-id="8a16b-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="8a16b-126">Pour vérifier que vos nouveaux partenaires ont été correctement ajoutés, sélectionnez la mosaïque **Partenaires**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="8a16b-127">Une fois la mosaïque Partenaires sélectionnée, le nouveau partenaire doit également se trouver dans le panneau Partenaires.</span><span class="sxs-lookup"><span data-stu-id="8a16b-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="8a16b-128">Comment modifier des partenaires existants dans votre compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="8a16b-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="8a16b-129">Sélectionnez la mosaïque **Partenaires**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="8a16b-130">Une fois le panneau Partenaires ouvert, sélectionnez le partenaire à modifier.</span><span class="sxs-lookup"><span data-stu-id="8a16b-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="8a16b-131">Sur la mosaïque **Mettre à jour le partenaire**, apportez les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="8a16b-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="8a16b-132">Une fois que vous avez terminé, sélectionnez **Enregistrer**. Si vous souhaitez annuler vos modifications, cliquez sur **Abandonner**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="8a16b-133">Suppression d’un partenaire</span><span class="sxs-lookup"><span data-stu-id="8a16b-133">How to delete a partner</span></span>

1. <span data-ttu-id="8a16b-134">Sélectionnez la mosaïque **Partenaires**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="8a16b-135">Une fois le panneau Partenaires ouvert, sélectionnez le partenaire à supprimer.</span><span class="sxs-lookup"><span data-stu-id="8a16b-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="8a16b-136">Choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="8a16b-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="8a16b-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a16b-137">Next steps</span></span>
* [<span data-ttu-id="8a16b-138">En savoir plus sur les contrats</span><span class="sxs-lookup"><span data-stu-id="8a16b-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  

