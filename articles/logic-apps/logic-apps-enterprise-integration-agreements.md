---
title: Contrats pour la communication B2B - Azure Logic Apps | Microsoft Docs
description: "Créer des contrats permettant aux partenaires de communiquer dans des scénarios B2B pour Azure Logic Apps et Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="7172a-103">Contrats de partenariat pour la communication B2B avec Azure Logic Apps et Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="7172a-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="7172a-104">Les contrats permettent à des entités métier de communiquer en toute transparence à l’aide de protocoles standard et constituent la pierre angulaire des communications Business-to-Business (B2B).</span><span class="sxs-lookup"><span data-stu-id="7172a-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="7172a-105">Lorsque des scénarios B2B sont activés pour des applications logiques avec Enterprise Integration Pack, un contrat est une organisation de communications conclue entre des partenaires commerciaux B2B.</span><span class="sxs-lookup"><span data-stu-id="7172a-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="7172a-106">Ce contrat est basé sur le type de communication que les partenaires souhaitent établir. Il est propre au protocole ou au transport.</span><span class="sxs-lookup"><span data-stu-id="7172a-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="7172a-107">L’intégration d’entreprise prend en charge ces normes de protocole/transport :</span><span class="sxs-lookup"><span data-stu-id="7172a-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="7172a-108">AS2</span><span class="sxs-lookup"><span data-stu-id="7172a-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="7172a-109">X12</span><span class="sxs-lookup"><span data-stu-id="7172a-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="7172a-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="7172a-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="7172a-111">Pourquoi utiliser des contrats ?</span><span class="sxs-lookup"><span data-stu-id="7172a-111">Why use agreements</span></span>

<span data-ttu-id="7172a-112">Voici quelques avantages communs lors de l’utilisation des contrats :</span><span class="sxs-lookup"><span data-stu-id="7172a-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="7172a-113">Permet à différentes organisations et entreprises d’échanger des informations dans un format reconnu.</span><span class="sxs-lookup"><span data-stu-id="7172a-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="7172a-114">Améliore l’efficacité des transactions B2B</span><span class="sxs-lookup"><span data-stu-id="7172a-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="7172a-115">Les accords sont faciles à créer, gérer et utiliser lors de la création d’applications d’intégration d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7172a-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="7172a-116">Comment créer des contrats ?</span><span class="sxs-lookup"><span data-stu-id="7172a-116">How to create agreements</span></span>

* [<span data-ttu-id="7172a-117">Créer un contrat AS2</span><span class="sxs-lookup"><span data-stu-id="7172a-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="7172a-118">Créer un contrat X12</span><span class="sxs-lookup"><span data-stu-id="7172a-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="7172a-119">Créer un contrat EDIFACT</span><span class="sxs-lookup"><span data-stu-id="7172a-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="7172a-120">Comment utiliser un contrat ?</span><span class="sxs-lookup"><span data-stu-id="7172a-120">How to use an agreement</span></span>

<span data-ttu-id="7172a-121">Vous pouvez créer des [applications logiques](logic-apps-what-are-logic-apps.md "En savoir plus sur les applications logiques") dotées de fonctionnalités B2B à l’aide d’un contrat que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="7172a-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="7172a-122">Comment modifier un contrat ?</span><span class="sxs-lookup"><span data-stu-id="7172a-122">How to edit an agreement</span></span>

<span data-ttu-id="7172a-123">Vous pouvez modifier n’importe quel contrat en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="7172a-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="7172a-124">Sélectionnez le compte d’intégration contenant le contrat que vous souhaitez mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="7172a-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="7172a-125">Choisissez la mosaïque **Contrats**.</span><span class="sxs-lookup"><span data-stu-id="7172a-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="7172a-126">Dans le panneau **Contrats**, sélectionnez le contrat.</span><span class="sxs-lookup"><span data-stu-id="7172a-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="7172a-127">Choisissez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="7172a-127">Choose **Edit**.</span></span> <span data-ttu-id="7172a-128">Apportez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="7172a-128">Make your changes.</span></span>

5. <span data-ttu-id="7172a-129">Pour enregistrer vos modifications, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7172a-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="7172a-130">Suppression d'un contrat</span><span class="sxs-lookup"><span data-stu-id="7172a-130">How to delete an agreement</span></span>

<span data-ttu-id="7172a-131">Vous pouvez supprimer n’importe quel contrat en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="7172a-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="7172a-132">Sélectionnez le compte d’intégration contenant le contrat que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="7172a-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="7172a-133">Choisissez la mosaïque **Contrats**.</span><span class="sxs-lookup"><span data-stu-id="7172a-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="7172a-134">Dans le panneau **Contrats**, sélectionnez le contrat.</span><span class="sxs-lookup"><span data-stu-id="7172a-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="7172a-135">Choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="7172a-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="7172a-136">Confirmez que vous souhaitez supprimer le contrat sélectionné.</span><span class="sxs-lookup"><span data-stu-id="7172a-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="7172a-137">Le panneau Contrats n’affiche plus le contrat supprimé.</span><span class="sxs-lookup"><span data-stu-id="7172a-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7172a-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7172a-138">Next steps</span></span>
* [<span data-ttu-id="7172a-139">Créer un contrat AS2</span><span class="sxs-lookup"><span data-stu-id="7172a-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
