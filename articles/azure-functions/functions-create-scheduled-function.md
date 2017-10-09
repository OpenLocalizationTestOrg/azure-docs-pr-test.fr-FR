---
title: "aaaCreate une fonction qui s’exécute sur une planification dans Azure | Documents Microsoft"
description: "Découvrez comment toocreate une fonction dans Azure s’exécute selon une planification que vous définissez."
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
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="c312f-103">Créez une fonction dans Azure, qui est déclenchée par un minuteur</span><span class="sxs-lookup"><span data-stu-id="c312f-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="c312f-104">Découvrez comment toouse Azure fonctions toocreate une fonction qui s’exécute sur une planification que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="c312f-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Créer l’application de la fonction Bonjour portail Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="c312f-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c312f-106">Prerequisites</span></span>

<span data-ttu-id="c312f-107">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="c312f-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="c312f-108">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="c312f-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="c312f-109">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="c312f-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="c312f-111">Ensuite, créez une fonction dans hello une nouvelle application de fonction.</span><span class="sxs-lookup"><span data-stu-id="c312f-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="c312f-112">Créer une fonction déclenchée par un minuteur</span><span class="sxs-lookup"><span data-stu-id="c312f-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="c312f-113">Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**.</span><span class="sxs-lookup"><span data-stu-id="c312f-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="c312f-114">S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="c312f-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="c312f-115">Cela affiche le jeu complet de hello des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="c312f-115">This displays hello complete set of function templates.</span></span>

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="c312f-117">Sélectionnez hello **TimerTrigger** modèle pour le langage de votre choix.</span><span class="sxs-lookup"><span data-stu-id="c312f-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="c312f-118">Utilisez ensuite les paramètres de hello comme spécifié dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="c312f-118">Then use hello settings as specified in hello table:</span></span>

    ![Créer une fonction de minuteur déclenché Bonjour portail Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="c312f-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c312f-120">Setting</span></span> | <span data-ttu-id="c312f-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="c312f-121">Suggested value</span></span> | <span data-ttu-id="c312f-122">Description</span><span class="sxs-lookup"><span data-stu-id="c312f-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="c312f-123">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="c312f-123">**Name your function**</span></span> | <span data-ttu-id="c312f-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="c312f-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="c312f-125">Définit le nom hello de votre fonction de minuteur déclenché.</span><span class="sxs-lookup"><span data-stu-id="c312f-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="c312f-126">**[Planification](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="c312f-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="c312f-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="c312f-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="c312f-128">Un champ de six [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) qui planifie votre toorun fonction toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="c312f-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="c312f-129">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c312f-129">Click **Create**.</span></span> <span data-ttu-id="c312f-130">Une fonction est créée dans le langage que vous avez choisi et s’exécute chaque minute.</span><span class="sxs-lookup"><span data-stu-id="c312f-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="c312f-131">Vérifier l’exécution en consultant les informations de traçage écrites toohello journaux.</span><span class="sxs-lookup"><span data-stu-id="c312f-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Fonctions visionneuse du journal Bonjour portail Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="c312f-133">Maintenant, vous pouvez modifier la planification de la fonction hello afin qu’elle s’exécute moins souvent, par exemple une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="c312f-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="c312f-134">Planification de mise à jour hello du minuteur</span><span class="sxs-lookup"><span data-stu-id="c312f-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="c312f-135">Développez votre fonction et cliquez sur **Intégrer**.</span><span class="sxs-lookup"><span data-stu-id="c312f-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="c312f-136">Il s’agit où vous définissez l’entrée et de sortie liaisons de votre fonction et également définissez la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="c312f-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="c312f-137">Entrez une nouvelle valeur de **Planification** de `0 0 */1 * * *`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c312f-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Fonctions mettre à jour la planification du minuteur Bonjour portail Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="c312f-139">Vous disposez maintenant d’une fonction qui s’exécute toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="c312f-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="c312f-140">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="c312f-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="c312f-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c312f-141">Next steps</span></span>

<span data-ttu-id="c312f-142">Vous avez créé une fonction qui s’exécute selon une planification.</span><span class="sxs-lookup"><span data-stu-id="c312f-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="c312f-143">Pour en savoir plus sur les déclencheurs de minuteur, consultez la page [Planifier l’exécution de code avec Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="c312f-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>