---
title: "aaaLearn comment toouse hello dans les applications de la logique d’un connecteur Twitter | Documents Microsoft"
description: "Vue d’ensemble du connecteur Twitter avec les paramètres d’API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="e7a65-103">Prise en main connecteur de Twitter hello</span><span class="sxs-lookup"><span data-stu-id="e7a65-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="e7a65-104">Avec le connecteur de Twitter hello, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="e7a65-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="e7a65-105">publier et recevoir des tweets ;</span><span class="sxs-lookup"><span data-stu-id="e7a65-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="e7a65-106">accéder à des fils d’actualités, des amis et des abonnés ;</span><span class="sxs-lookup"><span data-stu-id="e7a65-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="e7a65-107">Effectuez l’une des hello autres actions et les déclencheurs décrites ci-dessous</span><span class="sxs-lookup"><span data-stu-id="e7a65-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="e7a65-108">toouse [n’importe quel connecteur](apis-list.md), vous devez tout d’abord toocreate une application logique.</span><span class="sxs-lookup"><span data-stu-id="e7a65-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="e7a65-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e7a65-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="e7a65-110">Se connecter tooTwitter</span><span class="sxs-lookup"><span data-stu-id="e7a65-110">Connect tooTwitter</span></span>
<span data-ttu-id="e7a65-111">Avant que votre application logique peut accéder à n’importe quel service, vous devez tout d’abord toocreate un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="e7a65-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="e7a65-112">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="e7a65-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="e7a65-113">Créer un tooTwitter de connexion</span><span class="sxs-lookup"><span data-stu-id="e7a65-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="e7a65-114">Utiliser un déclencheur Twitter</span><span class="sxs-lookup"><span data-stu-id="e7a65-114">Use a Twitter trigger</span></span>
<span data-ttu-id="e7a65-115">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="e7a65-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="e7a65-116">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e7a65-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="e7a65-117">Dans cet exemple, je vous indiquent comment toouse hello **lors de la validation d’un tweet nouvelle** déclencher toosearch pour #Seattle et, si #Seattle est trouvée, mettre à jour un fichier dans l’échange avec texte hello tweet de hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="e7a65-118">Dans un exemple d’entreprise, vous pourriez Rechercher nom hello de votre société et mettre à jour une base de données SQL avec texte hello tweet de hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="e7a65-119">Entrez *twitter* dans la zone de recherche de hello sur le Concepteur d’applications hello logique, puis sélectionnez hello **Twitter - lors de la validation d’un tweet nouvelle** déclencheur</span><span class="sxs-lookup"><span data-stu-id="e7a65-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="e7a65-120">![Image de déclencheur Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="e7a65-121">Entrez *#Seattle* Bonjour **rechercher du texte** contrôle</span><span class="sxs-lookup"><span data-stu-id="e7a65-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="e7a65-122">![Image de déclencheur Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="e7a65-123">À ce stade, votre application logique a été configurée avec un déclencheur qui commence une série de hello autres déclencheurs et les actions dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="e7a65-124">Pour un toobe application logique fonctionnelle, il doit contenir au moins un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="e7a65-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="e7a65-125">Suivez les étapes de hello de hello suivant section tooadd une action.</span><span class="sxs-lookup"><span data-stu-id="e7a65-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="e7a65-126">Ajouter une condition</span><span class="sxs-lookup"><span data-stu-id="e7a65-126">Add a condition</span></span>
<span data-ttu-id="e7a65-127">Étant donné que nous intéresse uniquement tweet d’utilisateurs avec plus de 50 utilisateurs, une condition qui confirme que le nombre de hello imposait doit d’abord être ajoutée toohello logique application.</span><span class="sxs-lookup"><span data-stu-id="e7a65-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="e7a65-128">Sélectionnez **+ nouvelle étape** action de hello tooadd vous aimeriez tootake quand #Seattle se trouve dans un tweet nouveau</span><span class="sxs-lookup"><span data-stu-id="e7a65-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="e7a65-129">![Image d’action Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="e7a65-130">Sélectionnez hello **ajouter une condition** lien.</span><span class="sxs-lookup"><span data-stu-id="e7a65-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="e7a65-131">![Image de condition Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="e7a65-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="e7a65-132">Cette opération ouvre hello **Condition** contrôle où vous pouvez vérifier des conditions telles que *est égal à*, *est inférieur à*, *est supérieur à*, *contient*, etc..</span><span class="sxs-lookup"><span data-stu-id="e7a65-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="e7a65-133">![Image de condition Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="e7a65-134">Sélectionnez hello **choisir une valeur** contrôle.</span><span class="sxs-lookup"><span data-stu-id="e7a65-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="e7a65-135">Dans ce contrôle, vous pouvez sélectionner une ou plusieurs des propriétés de hello à partir des actions précédentes ou les déclencheurs en tant que valeur hello dont la condition sera évaluée tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="e7a65-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="e7a65-136">![Image de condition Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="e7a65-137">Sélectionnez hello **...**  liste de hello tooexpand de propriétés afin de voir toutes les propriétés de hello qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="e7a65-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="e7a65-138">![Image de condition Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="e7a65-139">Sélectionnez hello **nombre de suivis** propriété.</span><span class="sxs-lookup"><span data-stu-id="e7a65-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="e7a65-140">![Image de condition Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="e7a65-141">Notez que les suivis hello propriété count est présent dans le contrôle de valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Image de condition Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="e7a65-143">Sélectionnez **est supérieur à** à partir de la liste des opérateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="e7a65-144">![Image de condition Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="e7a65-145">Entrez 50 comme hello opérande pour hello *est supérieur à* opérateur.</span><span class="sxs-lookup"><span data-stu-id="e7a65-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="e7a65-146">Hello condition est maintenant ajoutée.</span><span class="sxs-lookup"><span data-stu-id="e7a65-146">hello condition is now added.</span></span> <span data-ttu-id="e7a65-147">Enregistrez votre travail à l’aide de hello **enregistrer** lien dans le menu hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e7a65-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="e7a65-148">![Image de condition Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="e7a65-149">Utiliser une action Twitter</span><span class="sxs-lookup"><span data-stu-id="e7a65-149">Use a Twitter action</span></span>
<span data-ttu-id="e7a65-150">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="e7a65-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="e7a65-151">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e7a65-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="e7a65-152">Maintenant que vous avez ajouté un déclencheur, suivez ces étapes de tooadd une action qui publie un tweet nouveau contenu hello de tweet hello trouvés par le déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="e7a65-153">Pour les besoins de hello de cette procédure pas à pas uniquement des tweets d’utilisateurs avec plus de 50 suivis seront publiées.</span><span class="sxs-lookup"><span data-stu-id="e7a65-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="e7a65-154">Dans l’étape suivante de hello, vous allez ajouter une action Twitter qui publie un tweet à l’aide de certaines des propriétés de hello de chaque tweet qui a été validé par un utilisateur qui a plus de 50 suivis.</span><span class="sxs-lookup"><span data-stu-id="e7a65-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="e7a65-155">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="e7a65-155">Select **Add an action**.</span></span> <span data-ttu-id="e7a65-156">Contrôle de recherche hello dans laquelle vous pouvez rechercher d’autres actions et les déclencheurs s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e7a65-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="e7a65-157">![Image de condition Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="e7a65-158">Entrez *twitter* dans la zone de recherche hello, puis sélectionnez hello **Twitter - valider un tweet** action.</span><span class="sxs-lookup"><span data-stu-id="e7a65-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="e7a65-159">Cette opération ouvre hello **valider un tweet** contrôler où vous devrez entrer tous les détails pour tweet hello en cours de publication.</span><span class="sxs-lookup"><span data-stu-id="e7a65-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="e7a65-160">![Image d’action Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="e7a65-161">Sélectionnez hello **tweetez-texte** contrôle.</span><span class="sxs-lookup"><span data-stu-id="e7a65-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="e7a65-162">Toutes les sorties à partir des actions précédentes et des déclencheurs dans l’application logique de hello sont désormais visibles.</span><span class="sxs-lookup"><span data-stu-id="e7a65-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="e7a65-163">Vous pouvez sélectionner une de ces et les utiliser en tant que partie du texte de tweet hello de tweet de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="e7a65-164">![Image d’action Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="e7a65-165">Sélectionnez **Nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="e7a65-165">Select **User name**</span></span>   
5. <span data-ttu-id="e7a65-166">Entrez *indique :* dans le contrôle de texte tweet hello.</span><span class="sxs-lookup"><span data-stu-id="e7a65-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="e7a65-167">Effectuez cette opération immédiatement après avoir sélectionné le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e7a65-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="e7a65-168">Sélectionnez *Tweet text* (Texte du tweet).</span><span class="sxs-lookup"><span data-stu-id="e7a65-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="e7a65-169">![Image d’action Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="e7a65-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="e7a65-170">Enregistrez votre travail et envoyer un tweet avec hello #Seattle #sqlhelp tooactivate votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="e7a65-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="e7a65-171">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="e7a65-171">Connector-specific details</span></span>

<span data-ttu-id="e7a65-172">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="e7a65-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e7a65-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7a65-173">Next steps</span></span>
[<span data-ttu-id="e7a65-174">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="e7a65-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

