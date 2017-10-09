---
title: aaaUse hello Slack connecteur dans vos applications Azure logique | Documents Microsoft
description: Se connecter tooSlack dans vos applications logiques
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
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="e2b87-103">Prise en main connecteur de marge hello</span><span class="sxs-lookup"><span data-stu-id="e2b87-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="e2b87-104">Slack est un outil de communication collaboratif qui centralise toutes les communications de votre équipe dans un seul emplacement que vous pouvez consulter instantanément, où que vous vous trouviez.</span><span class="sxs-lookup"><span data-stu-id="e2b87-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="e2b87-105">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e2b87-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="e2b87-106">Créer un tooSlack de connexion</span><span class="sxs-lookup"><span data-stu-id="e2b87-106">Create a connection tooSlack</span></span>
<span data-ttu-id="e2b87-107">connecteur de marge hello toouse, tout d’abord créer un **connexion** puis fournissez les informations de hello pour ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="e2b87-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="e2b87-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="e2b87-108">Property</span></span> | <span data-ttu-id="e2b87-109">Requis</span><span class="sxs-lookup"><span data-stu-id="e2b87-109">Required</span></span> | <span data-ttu-id="e2b87-110">Description</span><span class="sxs-lookup"><span data-stu-id="e2b87-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2b87-111">Jeton</span><span class="sxs-lookup"><span data-stu-id="e2b87-111">Token</span></span> |<span data-ttu-id="e2b87-112">Oui</span><span class="sxs-lookup"><span data-stu-id="e2b87-112">Yes</span></span> |<span data-ttu-id="e2b87-113">Fournir les informations d’identification de Slack</span><span class="sxs-lookup"><span data-stu-id="e2b87-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="e2b87-114">Suivez ces étapes toosign en marge et la configuration de hello complète de hello Slack **connexion** dans votre application logique :</span><span class="sxs-lookup"><span data-stu-id="e2b87-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="e2b87-115">Sélectionnez **Périodicité**</span><span class="sxs-lookup"><span data-stu-id="e2b87-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="e2b87-116">Sélectionnez une **Fréquence** et entrez un **Intervalle**</span><span class="sxs-lookup"><span data-stu-id="e2b87-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="e2b87-117">Sélectionnez **Ajouter une action**</span><span class="sxs-lookup"><span data-stu-id="e2b87-117">Select **Add an action**</span></span>  
   <span data-ttu-id="e2b87-118">![Configurer Slack][1]</span><span class="sxs-lookup"><span data-stu-id="e2b87-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="e2b87-119">Entrez une marge dans la zone de recherche hello et hello recherche tooreturn attendre que toutes les entrées avec une marge de nom de hello</span><span class="sxs-lookup"><span data-stu-id="e2b87-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="e2b87-120">Sélectionnez **Slack - Publier un message**</span><span class="sxs-lookup"><span data-stu-id="e2b87-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="e2b87-121">Sélectionnez **connecter tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="e2b87-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="e2b87-122">![Configurer Slack][2]</span><span class="sxs-lookup"><span data-stu-id="e2b87-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="e2b87-123">Fournissez votre toosign les informations d’identification Slack dans l’application de hello tooauthorize</span><span class="sxs-lookup"><span data-stu-id="e2b87-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Configurer Slack][3]  
8. <span data-ttu-id="e2b87-125">Vous serez page de connexion redirigé tooyour organisation.</span><span class="sxs-lookup"><span data-stu-id="e2b87-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="e2b87-126">**Autoriser** marge toointeract avec votre application logique :</span><span class="sxs-lookup"><span data-stu-id="e2b87-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="e2b87-127">![Configurer Slack][5]</span><span class="sxs-lookup"><span data-stu-id="e2b87-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="e2b87-128">Une fois l’autorisation de hello terminée, vous serez redirigé tooyour logique application toocomplete il en configurant hello **marge - obtenir tous les messages** section.</span><span class="sxs-lookup"><span data-stu-id="e2b87-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="e2b87-129">Ajouter les autres déclencheurs et actions dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="e2b87-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="e2b87-130">![Configurer Slack][6]</span><span class="sxs-lookup"><span data-stu-id="e2b87-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="e2b87-131">Enregistrez votre travail en sélectionnant **enregistrer** sur la barre de menus hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e2b87-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="e2b87-132">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="e2b87-132">Connector-specific details</span></span>

<span data-ttu-id="e2b87-133">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="e2b87-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e2b87-134">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="e2b87-134">More connectors</span></span>
<span data-ttu-id="e2b87-135">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e2b87-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
