---
title: "Créez une fonction qui s’exécute selon une planification dans Azure | Microsoft Docs"
description: "Apprenez à créer une fonction dans Azure, qui s’exécute selon une planification que vous définissez."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="1af77-103">Créez une fonction dans Azure, qui est déclenchée par un minuteur</span><span class="sxs-lookup"><span data-stu-id="1af77-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="1af77-104">Apprenez à créer une fonction dans Azure, qui s’exécute selon une planification que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="1af77-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Créer une Function App dans le Portail Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="1af77-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1af77-106">Prerequisites</span></span>

<span data-ttu-id="1af77-107">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1af77-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="1af77-108">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="1af77-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="1af77-109">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="1af77-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="1af77-111">Créez ensuite une fonction dans la nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="1af77-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="1af77-112">Créer une fonction déclenchée par un minuteur</span><span class="sxs-lookup"><span data-stu-id="1af77-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="1af77-113">Développez votre Function App, puis cliquez sur le bouton **+** en regard de **Fonctions**.</span><span class="sxs-lookup"><span data-stu-id="1af77-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="1af77-114">S’il s’agit de la première fonction de votre Function App, sélectionnez **Fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="1af77-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="1af77-115">Cela affiche l’ensemble complet des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="1af77-115">This displays the complete set of function templates.</span></span>

    ![Page de démarrage rapide des fonctions sur le portail Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="1af77-117">Sélectionnez le modèle **TimerTrigger** pour le langage de votre choix.</span><span class="sxs-lookup"><span data-stu-id="1af77-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="1af77-118">Utilisez ensuite les paramètres spécifiés dans le tableau :</span><span class="sxs-lookup"><span data-stu-id="1af77-118">Then use the settings as specified in the table:</span></span>

    ![Créez une fonction déclenchée par un minuteur dans le portail Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="1af77-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="1af77-120">Setting</span></span> | <span data-ttu-id="1af77-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="1af77-121">Suggested value</span></span> | <span data-ttu-id="1af77-122">Description</span><span class="sxs-lookup"><span data-stu-id="1af77-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="1af77-123">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="1af77-123">**Name your function**</span></span> | <span data-ttu-id="1af77-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="1af77-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="1af77-125">Définit le nom de votre fonction déclenchée par minuteur.</span><span class="sxs-lookup"><span data-stu-id="1af77-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="1af77-126">**[Planification](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="1af77-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="1af77-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="1af77-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="1af77-128">Un champ de six [expressions CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) qui planifie l’exécution de votre fonction chaque minute.</span><span class="sxs-lookup"><span data-stu-id="1af77-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="1af77-129">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1af77-129">Click **Create**.</span></span> <span data-ttu-id="1af77-130">Une fonction est créée dans le langage que vous avez choisi et s’exécute chaque minute.</span><span class="sxs-lookup"><span data-stu-id="1af77-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="1af77-131">Vérifiez l’exécution en consultant les informations de traçage écrites dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="1af77-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Fonctions de visionneuse du journal dans le Portail Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="1af77-133">À présent, vous pouvez modifier la planification de la fonction afin qu’elle s’exécute moins souvent, par exemple une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="1af77-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="1af77-134">Mise à jour de la planification du minuteur</span><span class="sxs-lookup"><span data-stu-id="1af77-134">Update the timer schedule</span></span>

1. <span data-ttu-id="1af77-135">Développez votre fonction et cliquez sur **Intégrer**.</span><span class="sxs-lookup"><span data-stu-id="1af77-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="1af77-136">Il s’agit de l’endroit où vous définissez les liaisons d’entrée et de sortie pour votre fonction, et où vous configurez la planification.</span><span class="sxs-lookup"><span data-stu-id="1af77-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="1af77-137">Entrez une nouvelle valeur de **Planification** de `0 0 */1 * * *`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1af77-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Les fonctions mettent à jour la planification du minuteur dans le Portail Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="1af77-139">Vous disposez maintenant d’une fonction qui s’exécute toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="1af77-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="1af77-140">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="1af77-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="1af77-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1af77-141">Next steps</span></span>

<span data-ttu-id="1af77-142">Vous avez créé une fonction qui s’exécute selon une planification.</span><span class="sxs-lookup"><span data-stu-id="1af77-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="1af77-143">Pour en savoir plus sur les déclencheurs de minuteur, consultez la page [Planifier l’exécution de code avec Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="1af77-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>