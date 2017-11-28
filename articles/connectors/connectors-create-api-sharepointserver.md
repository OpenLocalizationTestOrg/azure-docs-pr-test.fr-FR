---
title: Utiliser le connecteur SharePoint Server dans vos applications logiques | Microsoft Docs
description: "Commencer à utiliser le connecteur SharePoint Server dans vos applications logiques"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="9968f-103">Prise en main du connecteur SharePoint</span><span class="sxs-lookup"><span data-stu-id="9968f-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="9968f-104">Le connecteur SharePoint permet d’utiliser des listes dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9968f-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="9968f-105">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9968f-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="9968f-106">Créer une connexion à SharePoint</span><span class="sxs-lookup"><span data-stu-id="9968f-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="9968f-107">Pour utiliser le connecteur SharePoint, vous devez créer une **connexion** , puis fournir les détails de ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="9968f-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="9968f-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="9968f-108">Property</span></span> | <span data-ttu-id="9968f-109">Requis</span><span class="sxs-lookup"><span data-stu-id="9968f-109">Required</span></span> | <span data-ttu-id="9968f-110">Description</span><span class="sxs-lookup"><span data-stu-id="9968f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9968f-111">Jeton</span><span class="sxs-lookup"><span data-stu-id="9968f-111">Token</span></span> |<span data-ttu-id="9968f-112">Oui</span><span class="sxs-lookup"><span data-stu-id="9968f-112">Yes</span></span> |<span data-ttu-id="9968f-113">Fournir les informations d’identification SharePoint</span><span class="sxs-lookup"><span data-stu-id="9968f-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="9968f-114">Pour vous connecter à **SharePoint**, entrez votre identité (nom d’utilisateur et mot de passe, informations d’identification de la carte à puce, etc.) dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9968f-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="9968f-115">Une fois que vous avez été authentifié, vous pouvez utiliser le connecteur SharePoint dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9968f-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="9968f-116">Dans le Concepteur de votre application logique, procédez comme suit pour vous connecter à SharePoint afin de créer la **connexion** à utiliser dans votre application logique :</span><span class="sxs-lookup"><span data-stu-id="9968f-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="9968f-117">Entrez SharePoint dans la zone de recherche et attendez que la recherche renvoie toutes les entrées contenant SharePoint dans leur nom : </span><span class="sxs-lookup"><span data-stu-id="9968f-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![Configurer SharePoint][1]  
2. <span data-ttu-id="9968f-119">Sélectionner **SharePoint - Quand un fichier est créé**</span><span class="sxs-lookup"><span data-stu-id="9968f-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="9968f-120">Sélectionnez **Connexion à SharePoint** :</span><span class="sxs-lookup"><span data-stu-id="9968f-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="9968f-121">![Configurer SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="9968f-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="9968f-122">Entrez vos informations d’identification SharePoint pour vous connecter et vous authentifier auprès de SharePoint </span><span class="sxs-lookup"><span data-stu-id="9968f-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Configurer SharePoint][3]     
5. <span data-ttu-id="9968f-124">Une fois l’authentification terminée, vous serez redirigé vers votre application logique pour la terminer en configurant la boîte de dialogue **Quand un fichier est créé** de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9968f-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="9968f-125">![Configurer SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="9968f-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="9968f-126">Vous pouvez ensuite ajouter d’autres déclencheurs et actions dont vous avez besoin pour terminer votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9968f-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="9968f-127">Enregistrez votre travail en sélectionnant **Enregistrer** sur la barre de menu supérieure.</span><span class="sxs-lookup"><span data-stu-id="9968f-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="9968f-128">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="9968f-128">Connector-specific details</span></span>

<span data-ttu-id="9968f-129">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="9968f-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9968f-130">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="9968f-130">More connectors</span></span>
<span data-ttu-id="9968f-131">Revenir à la [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9968f-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
