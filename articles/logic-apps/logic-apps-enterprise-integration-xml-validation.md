---
title: Valider des messages XML - Azure Logic Apps | Microsoft Docs
description: "Validez des messages XML avec des schémas dans Azure Logic Apps et dans des scénarios B2B à l’aide d’Enterprise Integration Pack"
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
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="9ec9d-103">Valider des messages XML pour l’intégration d’entreprise</span><span class="sxs-lookup"><span data-stu-id="9ec9d-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="9ec9d-104">Souvent, dans les scénarios B2B, les partenaires dans un contrat doivent s’assurer que les messages qu’ils échangent sont valides avant le début du traitement des données.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="9ec9d-105">Vous pouvez utiliser le connecteur XML Validation dans Enterprise Integration Pack pour valider les documents par rapport à un schéma prédéfini.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="9ec9d-106">Valider un document avec le connecteur XML Validation</span><span class="sxs-lookup"><span data-stu-id="9ec9d-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="9ec9d-107">Créez une application logique et [liez-la à votre compte d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md "Découvrez comment lier un compte d’intégration à une application logique") qui contient le schéma que celui que vous voulez utiliser pour valider les données XML.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="9ec9d-108">Ajoutez un déclencheur **Requête - Lors de la réception d’une requête HTTP** à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="9ec9d-109">Pour ajouter l’action **Validation XML** choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="9ec9d-110">Pour filtrer toutes les actions et obtenir celle que vous souhaitez utiliser, entrez *xml* dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="9ec9d-111">Choisissez **Validation XML**.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="9ec9d-112">Pour spécifier le contenu XML que vous souhaitez valider, sélectionnez **CONTENU**.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="9ec9d-113">Sélectionnez la balise body comme contenu à valider.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="9ec9d-114">Pour spécifier le schéma que vous souhaitez utiliser pour la validation de la précédente entrée de *contenu*, choisissez **NOM DU SCHÉMA**.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="9ec9d-115">Enregistrez votre travail </span><span class="sxs-lookup"><span data-stu-id="9ec9d-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="9ec9d-116">Vous avez maintenant terminé de configurer votre connecteur de validation.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="9ec9d-117">Dans une application réelle, vous souhaiterez peut-être stocker les données validées dans une application métier telle que Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="9ec9d-118">Pour envoyer la sortie validée à Salesforce, ajoutez une action.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="9ec9d-119">Pour tester votre action de validation, envoyez une demande au point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="9ec9d-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ec9d-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ec9d-120">Next steps</span></span>
[<span data-ttu-id="9ec9d-121">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="9ec9d-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack")   

