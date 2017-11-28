---
title: "Décodage EDIFACT B2B Logic Apps contenant un segment UNH2.5 - Azure Logic Apps | Documents Microsoft"
description: "Décodage EDIFACT B2B contenant un segment UNH2.5 - Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="90a5e-103">Gérer les documents EDIFACT contenant un segment UNH2.5</span><span class="sxs-lookup"><span data-stu-id="90a5e-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="90a5e-104">Lorsque UNH2.5 est présent dans le document EDIFACT, il est utilisé pour la recherche de schéma.</span><span class="sxs-lookup"><span data-stu-id="90a5e-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="90a5e-105">Exemple : le champ UNH est **EAN008** dans le message EDIFACT</span><span class="sxs-lookup"><span data-stu-id="90a5e-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="90a5e-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="90a5e-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="90a5e-107">Étapes à suivre pour gérer le message</span><span class="sxs-lookup"><span data-stu-id="90a5e-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="90a5e-108">Mettre à jour le schéma</span><span class="sxs-lookup"><span data-stu-id="90a5e-108">Update the schema</span></span>
2. <span data-ttu-id="90a5e-109">Vérifier les paramètres de l’accord</span><span class="sxs-lookup"><span data-stu-id="90a5e-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="90a5e-110">Mettre à jour le schéma</span><span class="sxs-lookup"><span data-stu-id="90a5e-110">Update the schema</span></span>
<span data-ttu-id="90a5e-111">Pour traiter le message, vous devez déployer un schéma avec le nom de nœud racine UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="90a5e-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="90a5e-112">Pour l’exemple donné, le nom racine du schéma est **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="90a5e-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="90a5e-113">Pour chaque D03B_ORDERS avec un autre segment UNH2.5, vous devez déployer un schéma individuel.</span><span class="sxs-lookup"><span data-stu-id="90a5e-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="90a5e-114">Ajouter un schéma à l’accord EDIFACT</span><span class="sxs-lookup"><span data-stu-id="90a5e-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="90a5e-115">Décodage EDIFACT</span><span class="sxs-lookup"><span data-stu-id="90a5e-115">EDIFACT Decode</span></span>
<span data-ttu-id="90a5e-116">Pour décoder le message entrant, configurez le schéma EDIFACT dans les paramètres de réception de l’accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="90a5e-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="90a5e-117">Ajouter le schéma au compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="90a5e-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="90a5e-118">Configurez le schéma EDIFACT dans les paramètres de réception de l’accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="90a5e-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="90a5e-119">Sélectionnez un accord EDIFACT et cliquez sur **Modifier au format JSON**.</span><span class="sxs-lookup"><span data-stu-id="90a5e-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="90a5e-120">Ajoutez la valeur UNH2.5 dans l’accord de réception **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png).</span><span class="sxs-lookup"><span data-stu-id="90a5e-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="90a5e-121">Encodage EDIFACT</span><span class="sxs-lookup"><span data-stu-id="90a5e-121">EDIFACT Encode</span></span>
<span data-ttu-id="90a5e-122">Pour encoder le message entrant, configurez le schéma EDIFACT dans les paramètres d’envoi de l’accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="90a5e-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="90a5e-123">Ajouter le schéma au compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="90a5e-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="90a5e-124">Configurez le schéma EDIFACT dans les paramètres d’envoi de l’accord EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="90a5e-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="90a5e-125">Sélectionnez un accord EDIFACT et cliquez sur **Modifier au format JSON**.</span><span class="sxs-lookup"><span data-stu-id="90a5e-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="90a5e-126">Ajoutez la valeur UNH2.5 dans l’accord d’envoi **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="90a5e-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="90a5e-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90a5e-127">Next Steps</span></span>
* [<span data-ttu-id="90a5e-128">En savoir plus sur les contrats de compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="90a5e-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  