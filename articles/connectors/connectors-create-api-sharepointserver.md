---
title: aaaUse hello connecteur du serveur SharePoint dans vos applications logiques | Documents Microsoft
description: Prise en main Bonjour Bonjour SharePoint Server Connector dans vos applications logiques
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
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="c1099-103">Prise en main connecteur de SharePoint hello</span><span class="sxs-lookup"><span data-stu-id="c1099-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="c1099-104">Hello connecteur SharePoint fournit un toowork de façon avec les listes sur SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c1099-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="c1099-105">Commencez par créer une application logique. Pour cela, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c1099-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="c1099-106">Créer un tooSharePoint de connexion</span><span class="sxs-lookup"><span data-stu-id="c1099-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="c1099-107">toouse hello connecteur de SharePoint, vous commencez par créer un **connexion** puis fournissez les informations de hello pour ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="c1099-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="c1099-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="c1099-108">Property</span></span> | <span data-ttu-id="c1099-109">Requis</span><span class="sxs-lookup"><span data-stu-id="c1099-109">Required</span></span> | <span data-ttu-id="c1099-110">Description</span><span class="sxs-lookup"><span data-stu-id="c1099-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1099-111">Jeton</span><span class="sxs-lookup"><span data-stu-id="c1099-111">Token</span></span> |<span data-ttu-id="c1099-112">Oui</span><span class="sxs-lookup"><span data-stu-id="c1099-112">Yes</span></span> |<span data-ttu-id="c1099-113">Fournir les informations d’identification SharePoint</span><span class="sxs-lookup"><span data-stu-id="c1099-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="c1099-114">tooconnect trop**SharePoint**, entrez votre tooSharePoint d’identité (nom d’utilisateur et mot de passe, informations d’identification de carte à puce, etc.).</span><span class="sxs-lookup"><span data-stu-id="c1099-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="c1099-115">Une fois que vous avez été authentifié, vous pouvez passer le connecteur de SharePoint toouse hello dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="c1099-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="c1099-116">Tandis que sur le Concepteur de hello de votre application logique, suivez ces toosign étapes dans une connexion SharePoint toocreate hello **connexion** pour une utilisation dans votre application logique :</span><span class="sxs-lookup"><span data-stu-id="c1099-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="c1099-117">Entrez SharePoint dans la zone de recherche hello et attendre que toutes les entrées avec SharePoint dans le nom de hello hello recherche tooreturn :</span><span class="sxs-lookup"><span data-stu-id="c1099-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![Configurer SharePoint][1]  
2. <span data-ttu-id="c1099-119">Sélectionner **SharePoint - Quand un fichier est créé**</span><span class="sxs-lookup"><span data-stu-id="c1099-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="c1099-120">Sélectionnez **connecter tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="c1099-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="c1099-121">![Configurer SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="c1099-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="c1099-122">Fournissez votre toosign d’informations d’identification SharePoint dans tooauthenticate avec SharePoint</span><span class="sxs-lookup"><span data-stu-id="c1099-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![Configurer SharePoint][3]     
5. <span data-ttu-id="c1099-124">Une fois l’authentification de hello est terminée, vous serez redirigé tooyour logique application toocomplete par la configuration de SharePoint **lorsqu’un fichier est créé** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c1099-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="c1099-125">![Configurer SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="c1099-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="c1099-126">Vous pouvez ensuite ajouter d’autres déclencheurs et les actions que vous devez toocomplete votre application logique.</span><span class="sxs-lookup"><span data-stu-id="c1099-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="c1099-127">Enregistrez votre travail en sélectionnant **enregistrer** sur la barre de menus hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c1099-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="c1099-128">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="c1099-128">Connector-specific details</span></span>

<span data-ttu-id="c1099-129">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="c1099-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c1099-130">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="c1099-130">More connectors</span></span>
<span data-ttu-id="c1099-131">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c1099-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
