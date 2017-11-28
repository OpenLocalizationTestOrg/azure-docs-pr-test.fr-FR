---
title: Utiliser le connecteur Slack dans vos applications logiques Azure | Microsoft Docs
description: "Se connecter à Slack dans vos applications logiques"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="178f1-103">Prise en main du connecteur Slack</span><span class="sxs-lookup"><span data-stu-id="178f1-103">Get started with the Slack connector</span></span>
<span data-ttu-id="178f1-104">Slack est un outil de communication collaboratif qui centralise toutes les communications de votre équipe dans un seul emplacement que vous pouvez consulter instantanément, où que vous vous trouviez.</span><span class="sxs-lookup"><span data-stu-id="178f1-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="178f1-105">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="178f1-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="178f1-106">Créer une connexion à Slack</span><span class="sxs-lookup"><span data-stu-id="178f1-106">Create a connection to Slack</span></span>
<span data-ttu-id="178f1-107">Pour utiliser le connecteur Slack, vous devez créer une **connexion** , puis fournir les détails de ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="178f1-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="178f1-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="178f1-108">Property</span></span> | <span data-ttu-id="178f1-109">Requis</span><span class="sxs-lookup"><span data-stu-id="178f1-109">Required</span></span> | <span data-ttu-id="178f1-110">Description</span><span class="sxs-lookup"><span data-stu-id="178f1-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="178f1-111">Jeton</span><span class="sxs-lookup"><span data-stu-id="178f1-111">Token</span></span> |<span data-ttu-id="178f1-112">Oui</span><span class="sxs-lookup"><span data-stu-id="178f1-112">Yes</span></span> |<span data-ttu-id="178f1-113">Fournir les informations d’identification de Slack</span><span class="sxs-lookup"><span data-stu-id="178f1-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="178f1-114">Suivez ces étapes pour vous connecter à Slack et terminer la configuration de la **connexion** à Slack dans votre application logique :</span><span class="sxs-lookup"><span data-stu-id="178f1-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="178f1-115">Sélectionnez **Périodicité**</span><span class="sxs-lookup"><span data-stu-id="178f1-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="178f1-116">Sélectionnez une **Fréquence** et entrez un **Intervalle**</span><span class="sxs-lookup"><span data-stu-id="178f1-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="178f1-117">Sélectionnez **Ajouter une action**</span><span class="sxs-lookup"><span data-stu-id="178f1-117">Select **Add an action**</span></span>  
   <span data-ttu-id="178f1-118">![Configurer Slack][1]</span><span class="sxs-lookup"><span data-stu-id="178f1-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="178f1-119">Entrez Slack dans la zone de recherche et attendez que la recherche renvoie toutes les entrées contenant Slack dans leur nom</span><span class="sxs-lookup"><span data-stu-id="178f1-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="178f1-120">Sélectionnez **Slack - Publier un message**</span><span class="sxs-lookup"><span data-stu-id="178f1-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="178f1-121">Sélectionnez **Se connecter à Slack** :</span><span class="sxs-lookup"><span data-stu-id="178f1-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="178f1-122">![Configurer Slack][2]</span><span class="sxs-lookup"><span data-stu-id="178f1-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="178f1-123">Entrer vos informations d’identification Slack pour vous connecter et autoriser l’application</span><span class="sxs-lookup"><span data-stu-id="178f1-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Configurer Slack][3]  
8. <span data-ttu-id="178f1-125">Vous êtes redirigé vers la page de connexion de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="178f1-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="178f1-126">**Autorisez** Slack à interagir avec votre application logique :</span><span class="sxs-lookup"><span data-stu-id="178f1-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="178f1-127">![Configurer Slack][5]</span><span class="sxs-lookup"><span data-stu-id="178f1-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="178f1-128">Une fois l’autorisation terminée, vous serez redirigé vers votre application logique pour la terminer en configurant la section **Slack - Obtenir tous les messages** .</span><span class="sxs-lookup"><span data-stu-id="178f1-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="178f1-129">Ajouter les autres déclencheurs et actions dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="178f1-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="178f1-130">![Configurer Slack][6]</span><span class="sxs-lookup"><span data-stu-id="178f1-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="178f1-131">Enregistrez votre travail en sélectionnant **Enregistrer** sur la barre de menu supérieure.</span><span class="sxs-lookup"><span data-stu-id="178f1-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="178f1-132">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="178f1-132">Connector-specific details</span></span>

<span data-ttu-id="178f1-133">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="178f1-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="178f1-134">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="178f1-134">More connectors</span></span>
<span data-ttu-id="178f1-135">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="178f1-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
