---
title: connecteur aaaDropbox dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooDropbox toomanage vos fichiers. Vous pouvez exécuter différentes actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="d8e13-105">Prise en main connecteur d’échange hello</span><span class="sxs-lookup"><span data-stu-id="d8e13-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="d8e13-106">Se connecter tooDropbox toomanage vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="d8e13-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="d8e13-107">Vous pouvez exécuter différentes actions, comme charger, mettre à jour, obtenir et supprimer des fichiers dans Dropbox.</span><span class="sxs-lookup"><span data-stu-id="d8e13-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="d8e13-108">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="d8e13-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="d8e13-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8e13-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="d8e13-110">Se connecter tooDropbox</span><span class="sxs-lookup"><span data-stu-id="d8e13-110">Connect tooDropbox</span></span>
<span data-ttu-id="d8e13-111">Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="d8e13-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="d8e13-112">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="d8e13-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d8e13-113">Par exemple, dans l’ordre tooconnect tooDropbox, vous devez un échange *connexion*.</span><span class="sxs-lookup"><span data-stu-id="d8e13-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="d8e13-114">toocreate une connexion, vous aurez besoin des informations d’identification de hello tooprovide que vous utilisez normalement le service de hello tooaccess à que vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d8e13-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="d8e13-115">Par conséquent, dans l’exemple d’échange hello, vous devez tooyour des informations d’identification hello compte Dropbox dans l’ordre toocreate hello connexion tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="d8e13-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> <span data-ttu-id="d8e13-116">[Apprenez-en davantage sur les connexions]().</span><span class="sxs-lookup"><span data-stu-id="d8e13-116">[Learn more about connections]()</span></span>

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="d8e13-117">Créer un tooDropbox de connexion</span><span class="sxs-lookup"><span data-stu-id="d8e13-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="d8e13-118">Utiliser un déclencheur Dropbox</span><span class="sxs-lookup"><span data-stu-id="d8e13-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="d8e13-119">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="d8e13-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="d8e13-120">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d8e13-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d8e13-121">Dans cet exemple, nous allons utiliser hello **lorsqu’un fichier est créé** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="d8e13-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="d8e13-122">Lorsque ce déclencheur se produit, nous appellerons hello **obtenir le contenu du fichier à l’aide du chemin d’accès** action d’échange.</span><span class="sxs-lookup"><span data-stu-id="d8e13-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="d8e13-123">Entrez *dropbox* dans la zone de recherche hello sur le concepteur hello Logic Apps, puis sélectionnez hello **Dropbox - lors de la création d’un fichier** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="d8e13-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="d8e13-124">Sélectionnez hello le dossier dans lequel la création du fichier tootrack.</span><span class="sxs-lookup"><span data-stu-id="d8e13-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="d8e13-125">Sélectionnez... (identifiées dans la zone de hello rouge) et parcourir toohello dossier tooselect pour déclencheur de hello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d8e13-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="d8e13-126">Utiliser une action Dropbox</span><span class="sxs-lookup"><span data-stu-id="d8e13-126">Use a Dropbox action</span></span>
<span data-ttu-id="d8e13-127">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="d8e13-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d8e13-128">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d8e13-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d8e13-129">Maintenant que hello déclencheur a été ajouté, suivez ces étapes de tooadd une action qui obtiennent le contenu hello du nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="d8e13-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="d8e13-130">Sélectionnez **+ nouvelle étape** action de hello tooadd vous aimeriez tootake lorsqu’un nouveau fichier est créé.</span><span class="sxs-lookup"><span data-stu-id="d8e13-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="d8e13-131">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="d8e13-131">Select **Add an action**.</span></span> <span data-ttu-id="d8e13-132">Cette zone de recherche hello s’ouvre dans laquelle vous pouvez rechercher n’importe quelle action vous aimeriez tootake.</span><span class="sxs-lookup"><span data-stu-id="d8e13-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="d8e13-133">Entrez *dropbox* toosearch pour tooDropbox connexes d’actions.</span><span class="sxs-lookup"><span data-stu-id="d8e13-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="d8e13-134">Sélectionnez **Dropbox - le contenu du fichier Get à l’aide du chemin d’accès** comme hello action tootake lorsqu’un nouveau fichier est créé dans hello sélectionné de dossier Dropbox.</span><span class="sxs-lookup"><span data-stu-id="d8e13-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="d8e13-135">bloc de contrôle d’action Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d8e13-135">hello action control block opens.</span></span> <span data-ttu-id="d8e13-136">Vous est demandée tooauthorize votre tooaccess d’application logique votre Dropbox compte si vous le n'avez pas fait précédemment.</span><span class="sxs-lookup"><span data-stu-id="d8e13-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="d8e13-137">Sélectionnez... (situé à droite de hello Hello **chemin d’accès du fichier** contrôle) et de parcourir le chemin d’accès du fichier toohello toouse voulue.</span><span class="sxs-lookup"><span data-stu-id="d8e13-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="d8e13-138">Ou, utilisez hello **chemin d’accès du fichier** toospeed de jeton de votre création d’une logique d’application.</span><span class="sxs-lookup"><span data-stu-id="d8e13-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="d8e13-139">Enregistrez votre travail et créer un nouveau fichier dans Dropbox tooactivate votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="d8e13-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="d8e13-140">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="d8e13-140">Connector-specific details</span></span>

<span data-ttu-id="d8e13-141">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="d8e13-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d8e13-142">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="d8e13-142">More connectors</span></span>
<span data-ttu-id="d8e13-143">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d8e13-143">Go back toohello [APIs list](apis-list.md).</span></span>
