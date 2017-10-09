---
title: "aaaLogic B2B applications edifact décoder résoudre UNH2.5 - Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="a1adc-103">Comment toohandle EDIFACT documents ayant UNH2.5 segment</span><span class="sxs-lookup"><span data-stu-id="a1adc-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="a1adc-104">Lorsque UNH2.5 est présent dans le document de hello EDIFACT, il est utilisé pour la recherche de schéma.</span><span class="sxs-lookup"><span data-stu-id="a1adc-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="a1adc-105">Exemple : champ UNH de hello est **EAN008** dans le message de salutation EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a1adc-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="a1adc-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="a1adc-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="a1adc-107">Message de type hello toohandle toofollow étapes</span><span class="sxs-lookup"><span data-stu-id="a1adc-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="a1adc-108">Mettre à jour le schéma de hello</span><span class="sxs-lookup"><span data-stu-id="a1adc-108">Update hello schema</span></span>
2. <span data-ttu-id="a1adc-109">Vérifiez les paramètres de l’accord hello</span><span class="sxs-lookup"><span data-stu-id="a1adc-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="a1adc-110">Mettre à jour le schéma de hello</span><span class="sxs-lookup"><span data-stu-id="a1adc-110">Update hello schema</span></span>
<span data-ttu-id="a1adc-111">message de type hello tooprocess, vous devez toodeploy un schéma avec le nom de nœud racine hello UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="a1adc-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="a1adc-112">Pour obtenir un exemple, nom racine du schéma hello serait **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="a1adc-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="a1adc-113">Pour chaque D03B_ORDERS avec un segment UNH2.5 différent, vous devriez toodeploy un schéma individuel.</span><span class="sxs-lookup"><span data-stu-id="a1adc-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="a1adc-114">Ajouter un accord EDIFACT toohello schéma</span><span class="sxs-lookup"><span data-stu-id="a1adc-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="a1adc-115">Décodage EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a1adc-115">EDIFACT Decode</span></span>
<span data-ttu-id="a1adc-116">tooDecode hello message entrant, configurer hello schéma Bonjour EDIFACT les paramètres de réception de contrat</span><span class="sxs-lookup"><span data-stu-id="a1adc-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="a1adc-117">Ajouter le compte d’intégration hello schéma toohello</span><span class="sxs-lookup"><span data-stu-id="a1adc-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="a1adc-118">Configurer le schéma de hello Bonjour EDIFACT les paramètres de réception de contrat.</span><span class="sxs-lookup"><span data-stu-id="a1adc-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="a1adc-119">Sélectionnez un accord EDIFACT et cliquez sur **Modifier au format JSON**.</span><span class="sxs-lookup"><span data-stu-id="a1adc-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="a1adc-120">Ajouter la valeur UNH2.5 Bonjour accord de réception **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a1adc-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="a1adc-121">Encodage EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a1adc-121">EDIFACT Encode</span></span>
<span data-ttu-id="a1adc-122">tooEncode hello message entrant, configurer le schéma de hello dans les paramètres d’envoi hello EDIFACT accord</span><span class="sxs-lookup"><span data-stu-id="a1adc-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="a1adc-123">Ajouter le compte d’intégration hello schéma toohello</span><span class="sxs-lookup"><span data-stu-id="a1adc-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="a1adc-124">Configurer le schéma de hello dans les paramètres d’envoi un accord EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="a1adc-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="a1adc-125">Sélectionnez un accord EDIFACT et cliquez sur **Modifier au format JSON**.</span><span class="sxs-lookup"><span data-stu-id="a1adc-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="a1adc-126">Ajouter la valeur UNH2.5 Bonjour envoyer l’accord **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="a1adc-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1adc-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1adc-127">Next Steps</span></span>
* [<span data-ttu-id="a1adc-128">En savoir plus sur les contrats de compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="a1adc-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")  