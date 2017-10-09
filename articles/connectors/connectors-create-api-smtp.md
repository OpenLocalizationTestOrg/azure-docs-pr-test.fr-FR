---
title: connecteur aaaSMTP dans Azure Logic Apps | Documents Microsoft
description: "Créez des applications logiques avec Azure App Service. Se connecter tooSMTP toosend e-mail."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="384c0-104">Prise en main connecteur hello</span><span class="sxs-lookup"><span data-stu-id="384c0-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="384c0-105">Se connecter tooSMTP toosend e-mail.</span><span class="sxs-lookup"><span data-stu-id="384c0-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="384c0-106">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="384c0-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="384c0-107">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="384c0-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="384c0-108">Se connecter tooSMTP</span><span class="sxs-lookup"><span data-stu-id="384c0-108">Connect tooSMTP</span></span>
<span data-ttu-id="384c0-109">Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="384c0-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="384c0-110">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="384c0-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="384c0-111">Par exemple, tooconnect tooSMTP, vous devez d’abord un SMTP *connexion*.</span><span class="sxs-lookup"><span data-stu-id="384c0-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="384c0-112">toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess vous vous connectez à.</span><span class="sxs-lookup"><span data-stu-id="384c0-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="384c0-113">Par conséquent, dans l’exemple de hello SMTP, entrez tooSMTP de la connexion utilisateur connexion informations toocreate hello, adresse du serveur SMTP et nom de connexion tooyour hello informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="384c0-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="384c0-114">Créer un tooSMTP de connexion</span><span class="sxs-lookup"><span data-stu-id="384c0-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="384c0-115">Utiliser un déclencheur SMTP</span><span class="sxs-lookup"><span data-stu-id="384c0-115">Use an SMTP trigger</span></span>
<span data-ttu-id="384c0-116">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="384c0-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="384c0-117">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="384c0-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="384c0-118">Dans cet exemple, étant donné que SMTP n’a pas un déclencheur qui lui sont propres, nous allons utiliser hello **Salesforce - lors de la création d’un objet** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="384c0-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="384c0-119">Ce déclencheur s’active lorsqu’un objet est créé dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="384c0-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="384c0-120">Dans notre exemple, nous allons la définir telle sorte que chaque fois qu’un nouveau prospect est créé dans Salesforce, un *envoyer un courrier électronique* action se produit via le connecteur hello SMTP avec une notification de prospect hello en cours de création.</span><span class="sxs-lookup"><span data-stu-id="384c0-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="384c0-121">Entrez *salesforce* dans la zone de recherche de hello sur le Concepteur d’applications hello logique, puis sélectionnez hello **Salesforce - lors de la création d’un objet** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="384c0-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="384c0-122">Hello **lorsqu’un objet est créé** contrôle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="384c0-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="384c0-123">Sélectionnez hello **Type d’objet** puis sélectionnez *entraîner* à partir de la liste de hello d’objets.</span><span class="sxs-lookup"><span data-stu-id="384c0-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="384c0-124">Lors de cette étape, vous indiquez que vous créez un déclencheur qui informe votre application logique de la création d’un prospect dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="384c0-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="384c0-125">déclencheur de Hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="384c0-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="384c0-126">Utiliser une action SMTP</span><span class="sxs-lookup"><span data-stu-id="384c0-126">Use an SMTP action</span></span>
<span data-ttu-id="384c0-127">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="384c0-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="384c0-128">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="384c0-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="384c0-129">Maintenant que hello déclencheur a été ajouté, suivez ces étapes tooadd un SMTP l’action qui se produit lorsqu’un nouveau prospect est créé dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="384c0-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="384c0-130">Sélectionnez **+ nouvelle étape** action de hello tooadd vous aimeriez tootake lors de la création d’un nouveau prospect.</span><span class="sxs-lookup"><span data-stu-id="384c0-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="384c0-131">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="384c0-131">Select **Add an action**.</span></span> <span data-ttu-id="384c0-132">Cette zone de recherche hello s’ouvre dans laquelle vous pouvez rechercher n’importe quelle action vous aimeriez tootake.</span><span class="sxs-lookup"><span data-stu-id="384c0-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="384c0-133">Entrez *smtp* toosearch pour tooSMTP connexes d’actions.</span><span class="sxs-lookup"><span data-stu-id="384c0-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="384c0-134">Sélectionnez **SMTP - envoyer un courrier électronique** comme hello action tootake lors de la création de prospect hello.</span><span class="sxs-lookup"><span data-stu-id="384c0-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="384c0-135">bloc de contrôle d’action Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="384c0-135">hello action control block opens.</span></span> <span data-ttu-id="384c0-136">Vous devez tooestablish votre connexion smtp dans le bloc de concepteur hello si vous le n'avez pas fait précédemment.</span><span class="sxs-lookup"><span data-stu-id="384c0-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="384c0-137">Entrez vos informations de messagerie de votre choix dans hello **SMTP - envoyer un courrier électronique** bloc.</span><span class="sxs-lookup"><span data-stu-id="384c0-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="384c0-138">Enregistrez votre travail dans l’ordre tooactivate votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="384c0-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="384c0-139">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="384c0-139">Connector-specific details</span></span>

<span data-ttu-id="384c0-140">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="384c0-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="384c0-141">Autres connecteurs</span><span class="sxs-lookup"><span data-stu-id="384c0-141">More connectors</span></span>
<span data-ttu-id="384c0-142">Revenir en arrière toohello [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="384c0-142">Go back toohello [APIs list](apis-list.md).</span></span>
