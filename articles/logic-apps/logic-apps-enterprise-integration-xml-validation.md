---
title: aaaValidate XML - Azure Logic Apps | Documents Microsoft
description: "Valider le code XML avec des schémas pour les scénarios Azure Logic Apps et B2B à l’aide de hello Pack d’intégration Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="e11a9-103">Valider des messages XML pour l’intégration d’entreprise</span><span class="sxs-lookup"><span data-stu-id="e11a9-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="e11a9-104">Souvent dans les scénarios B2B, les partenaires hello dans un accord doivent vous assurer qu’ils échangent des messages de type hello sont valides avant que le traitement des données puisse démarrer.</span><span class="sxs-lookup"><span data-stu-id="e11a9-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="e11a9-105">Vous pouvez valider des documents par rapport à un schéma prédéfini à l’aide de connecteur de Validation XML hello utilisez hello Bonjour Pack d’intégration Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e11a9-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="e11a9-106">Valider un document avec le connecteur de Validation XML hello</span><span class="sxs-lookup"><span data-stu-id="e11a9-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="e11a9-107">Créer une application logique, et [lier le compte d’intégration hello application toohello](../logic-apps/logic-apps-enterprise-integration-accounts.md "savoir toolink une application de la logique de l’intégration compte tooa") qui a hello schéma toouse pour la validation des données XML.</span><span class="sxs-lookup"><span data-stu-id="e11a9-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="e11a9-108">Ajouter un **demande - HTTP lors de la demande est reçue** application logique de tooyour déclencheur.</span><span class="sxs-lookup"><span data-stu-id="e11a9-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="e11a9-109">tooadd hello **Validation XML** action, choisissez **ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="e11a9-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="e11a9-110">toofilter tous hello toohello actions une que vous le souhaitez, entrez *xml* dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="e11a9-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="e11a9-111">Choisissez **Validation XML**.</span><span class="sxs-lookup"><span data-stu-id="e11a9-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="e11a9-112">toospecify hello contenu XML que vous souhaitez toovalidate, sélectionnez **contenu**.</span><span class="sxs-lookup"><span data-stu-id="e11a9-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="e11a9-113">Sélectionnez body est dupliquée hello hello contenu que vous souhaitez toovalidate.</span><span class="sxs-lookup"><span data-stu-id="e11a9-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="e11a9-114">toospecify hello schéma toouse pour la validation de hello précédente *contenu* d’entrée, choisissez **nom de schéma**.</span><span class="sxs-lookup"><span data-stu-id="e11a9-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="e11a9-115">Enregistrez votre travail </span><span class="sxs-lookup"><span data-stu-id="e11a9-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="e11a9-116">Vous avez maintenant terminé de configurer votre connecteur de validation.</span><span class="sxs-lookup"><span data-stu-id="e11a9-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="e11a9-117">Dans une application réelle, vous pourriez toostore des données de hello validé dans une application de (LOB) de line-of-business comme SalesForce.</span><span class="sxs-lookup"><span data-stu-id="e11a9-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="e11a9-118">toosend hello sortie validée tooSalesforce, ajoutez une action.</span><span class="sxs-lookup"><span data-stu-id="e11a9-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="e11a9-119">tootest votre action de validation, rendre un point de terminaison demande toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="e11a9-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e11a9-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e11a9-120">Next steps</span></span>
[<span data-ttu-id="e11a9-121">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="e11a9-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")   

