---
title: "Découvrez comment utiliser le connecteur Twitter dans les applications logiques | Microsoft Docs"
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="29343-103">Prise en main du connecteur Twitter</span><span class="sxs-lookup"><span data-stu-id="29343-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="29343-104">Le connecteur Twitter vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="29343-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="29343-105">publier et recevoir des tweets ;</span><span class="sxs-lookup"><span data-stu-id="29343-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="29343-106">accéder à des fils d’actualités, des amis et des abonnés ;</span><span class="sxs-lookup"><span data-stu-id="29343-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="29343-107">exécuter la totalité des actions et des déclencheurs décrits ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="29343-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="29343-108">Pour utiliser [n’importe quel connecteur](apis-list.md), vous devez commencer par créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="29343-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="29343-109">Vous pouvez démarrer maintenant en [créant une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="29343-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="29343-110">Se connecter à Twitter</span><span class="sxs-lookup"><span data-stu-id="29343-110">Connect to Twitter</span></span>
<span data-ttu-id="29343-111">Pour que votre application logique puisse accéder à un service, vous devez commencer par créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="29343-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="29343-112">Une [connexion](connectors-overview.md) permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="29343-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="29343-113">Créer une connexion à Twitter</span><span class="sxs-lookup"><span data-stu-id="29343-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="29343-114">Utiliser un déclencheur Twitter</span><span class="sxs-lookup"><span data-stu-id="29343-114">Use a Twitter trigger</span></span>
<span data-ttu-id="29343-115">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="29343-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="29343-116">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="29343-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="29343-117">Dans cet exemple, nous allons vous indiquer comment utiliser le déclencheur **When a new tweet is posted** (Quand un nouveau tweet est publié) pour rechercher #Seattle et, si le texte #Seattle est trouvé, pour mettre à jour un fichier dans Dropbox avec le texte du tweet.</span><span class="sxs-lookup"><span data-stu-id="29343-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="29343-118">Dans un contexte d’entreprise, vous pourriez rechercher le nom de votre société et mettre à jour une base de données SQL avec le texte du tweet.</span><span class="sxs-lookup"><span data-stu-id="29343-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="29343-119">Entrez *twitter* dans la zone de recherche du concepteur d’applications logiques, puis sélectionnez le déclencheur **Twitter - When a new tweet is posted** (Twitter - Quand un nouveau tweet est publié).</span><span class="sxs-lookup"><span data-stu-id="29343-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="29343-120">![Image de déclencheur Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="29343-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="29343-121">Entrez *#Seattle* dans le contrôle **Search Text** (Texte de recherche).</span><span class="sxs-lookup"><span data-stu-id="29343-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="29343-122">![Image de déclencheur Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="29343-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="29343-123">À ce stade, votre application logique a été configurée avec un déclencheur qui lance une série d’autres déclencheurs et actions dans le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="29343-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="29343-124">Pour qu’une application logique soit fonctionnelle, elle doit contenir au moins un déclencheur et une action.</span><span class="sxs-lookup"><span data-stu-id="29343-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="29343-125">Suivez la procédure décrite ci-après pour ajouter une action.</span><span class="sxs-lookup"><span data-stu-id="29343-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="29343-126">Ajouter une condition</span><span class="sxs-lookup"><span data-stu-id="29343-126">Add a condition</span></span>
<span data-ttu-id="29343-127">Étant donné que nous sommes uniquement intéressés par les tweets publiés par des utilisateurs disposant de plus de 50 abonnés, nous devons commencer par ajouter à l’application logique une condition confirmant le nombre d’abonnés.</span><span class="sxs-lookup"><span data-stu-id="29343-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="29343-128">Sélectionnez **+ Nouvelle étape** pour ajouter l’action à exécuter quand le texte #Seattle est trouvé dans un nouveau tweet.</span><span class="sxs-lookup"><span data-stu-id="29343-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="29343-129">![Image d’action Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="29343-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="29343-130">Sélectionnez le lien **Ajouter une condition**.</span><span class="sxs-lookup"><span data-stu-id="29343-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="29343-131">![Image de condition Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="29343-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="29343-132">Cette opération ouvre le contrôle **Condition** qui vous permet de sélectionner des conditions telles que *est égal à*, *est inférieur à*, *est supérieur à*, *contient*, etc.</span><span class="sxs-lookup"><span data-stu-id="29343-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="29343-133">![Image de condition Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="29343-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="29343-134">Sélectionnez le contrôle **Choisir une valeur**.</span><span class="sxs-lookup"><span data-stu-id="29343-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="29343-135">Dans ce contrôle, vous pouvez sélectionner une ou plusieurs des propriétés des actions ou déclencheurs précédents en tant que valeur dont la condition sera évaluée comme étant vraie ou fausse.</span><span class="sxs-lookup"><span data-stu-id="29343-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="29343-136">![Image de condition Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="29343-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="29343-137">Sélectionnez le bouton **...** pour développer la liste de propriétés et visualiser toutes les propriétés disponibles.</span><span class="sxs-lookup"><span data-stu-id="29343-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="29343-138">![Image de condition Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="29343-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="29343-139">Sélectionnez la propriété **Followers count** (Nombre d’abonnés).</span><span class="sxs-lookup"><span data-stu-id="29343-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="29343-140">![Image de condition Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="29343-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="29343-141">Notez que la propriété Followers count (Nombre d’abonnés) figure désormais dans le contrôle de valeur.</span><span class="sxs-lookup"><span data-stu-id="29343-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Image de condition Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="29343-143">Sélectionnez **est supérieur à** dans la liste des opérateurs.</span><span class="sxs-lookup"><span data-stu-id="29343-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="29343-144">![Image de condition Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="29343-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="29343-145">Entrez 50 en tant qu’opérande pour l’opérateur *est supérieur à*.</span><span class="sxs-lookup"><span data-stu-id="29343-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="29343-146">La condition est à présent ajoutée.</span><span class="sxs-lookup"><span data-stu-id="29343-146">The condition is now added.</span></span> <span data-ttu-id="29343-147">Enregistrez votre travail à l’aide du lien **Enregistrer** dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="29343-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="29343-148">![Image de condition Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="29343-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="29343-149">Utiliser une action Twitter</span><span class="sxs-lookup"><span data-stu-id="29343-149">Use a Twitter action</span></span>
<span data-ttu-id="29343-150">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="29343-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="29343-151">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="29343-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="29343-152">Une fois le déclencheur ajouté, procédez comme suit pour ajouter une action qui publiera un nouveau tweet avec le contenu des tweets trouvés par le déclencheur.</span><span class="sxs-lookup"><span data-stu-id="29343-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="29343-153">Pour les besoins de cette procédure pas à pas, seuls les tweets émanant d’utilisateurs disposant de plus de 50 abonnés seront publiés.</span><span class="sxs-lookup"><span data-stu-id="29343-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="29343-154">À l’étape suivante, vous allez ajouter une action Twitter qui publiera un tweet en utilisant certaines des propriétés de chaque tweet ayant été publié par un utilisateur comptant plus de 50 abonnés.</span><span class="sxs-lookup"><span data-stu-id="29343-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="29343-155">Sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="29343-155">Select **Add an action**.</span></span> <span data-ttu-id="29343-156">Cette opération ouvre le contrôle de recherche qui vous permet de rechercher d’autres actions et déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="29343-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="29343-157">![Image de condition Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="29343-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="29343-158">Entrez *twitter* dans la zone de recherche, puis sélectionnez l’action **Twitter - Post a tweet** (Twitter - Publier un tweet).</span><span class="sxs-lookup"><span data-stu-id="29343-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="29343-159">Cette opération ouvre le contrôle **Post a tweet** (Publier un tweet) dans lequel vous entrerez tous les détails concernant le tweet en cours de publication.</span><span class="sxs-lookup"><span data-stu-id="29343-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="29343-160">![Image d’action Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="29343-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="29343-161">Sélectionnez le contrôle **Tweet text** (Texte du tweet).</span><span class="sxs-lookup"><span data-stu-id="29343-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="29343-162">Toutes les sorties des actions et déclencheurs précédents dans l’application logique sont désormais visibles.</span><span class="sxs-lookup"><span data-stu-id="29343-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="29343-163">Vous pouvez sélectionner les actions et déclencheurs de votre choix et les utiliser comme partie du texte du nouveau tweet.</span><span class="sxs-lookup"><span data-stu-id="29343-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="29343-164">![Image d’action Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="29343-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="29343-165">Sélectionnez **Nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29343-165">Select **User name**</span></span>   
5. <span data-ttu-id="29343-166">Entrez *dit :* dans le contrôle du texte du tweet.</span><span class="sxs-lookup"><span data-stu-id="29343-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="29343-167">Effectuez cette opération immédiatement après avoir sélectionné le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29343-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="29343-168">Sélectionnez *Tweet text* (Texte du tweet).</span><span class="sxs-lookup"><span data-stu-id="29343-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="29343-169">![Image d’action Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="29343-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="29343-170">Enregistrez votre travail et envoyez un tweet avec le mot-dièse #Seattle pour activer votre workflow.</span><span class="sxs-lookup"><span data-stu-id="29343-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="29343-171">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="29343-171">Connector-specific details</span></span>

<span data-ttu-id="29343-172">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="29343-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="29343-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29343-173">Next steps</span></span>
[<span data-ttu-id="29343-174">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="29343-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

