---
title: "environnement de Azure temps série Insights aaaAdd référence jeu de données tooyour | Documents Microsoft"
description: "Dans ce didacticiel, vous ajoutez l’environnement de temps série Insights tooyour référence de jeu de données"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="32d0c-103">Créer un jeu de données de référence pour votre environnement d’un aperçu en temps série à l’aide du portail de Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="32d0c-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="32d0c-104">Un jeu de données de référence est une collection d’éléments qui sont augmentés avec les événements hello à partir de votre source d’événements.</span><span class="sxs-lookup"><span data-stu-id="32d0c-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="32d0c-105">Le moteur d’entrée Time Series Insights joint un événement à partir de votre source d’événements à un élément dans votre jeu de données de référence.</span><span class="sxs-lookup"><span data-stu-id="32d0c-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="32d0c-106">Cet événement ajouté est ensuite disponible pour la requête.</span><span class="sxs-lookup"><span data-stu-id="32d0c-106">This augmented event is then available for query.</span></span> <span data-ttu-id="32d0c-107">Cette jointure est basée sur les clés hello définies dans votre jeu de données de référence.</span><span class="sxs-lookup"><span data-stu-id="32d0c-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="32d0c-108">Étapes tooadd un environnement de tooyour de jeu de données de référence</span><span class="sxs-lookup"><span data-stu-id="32d0c-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="32d0c-109">Connectez-vous à toohello [portail Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32d0c-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="32d0c-110">Cliquez sur « Toutes les ressources » dans le menu hello hello situé à gauche du portail de Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="32d0c-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="32d0c-111">Sélectionnez votre environnement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="32d0c-111">Select your Time Series Insights environment.</span></span>

    ![Créer le jeu de données de référence de temps série Insights hello](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="32d0c-113">Sélectionnez « Jeux de données de référence », puis cliquez sur « + Ajouter ».</span><span class="sxs-lookup"><span data-stu-id="32d0c-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Créer le jeu de données de la référence du temps série Insights hello - détails](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="32d0c-115">Spécifiez le nom hello du jeu de données de référence hello.</span><span class="sxs-lookup"><span data-stu-id="32d0c-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="32d0c-116">Spécifiez le nom de la clé hello et son type.</span><span class="sxs-lookup"><span data-stu-id="32d0c-116">Specify hello key name and its type.</span></span> <span data-ttu-id="32d0c-117">Ce nom et le type est toopick utilisé hello de propriété approprié à partir de l’événement hello dans votre source d’événement.</span><span class="sxs-lookup"><span data-stu-id="32d0c-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="32d0c-118">Par exemple, si vous fournissez le nom de la clé en tant que « DeviceId » et le type en tant que « String », puis hello un aperçu en temps série entrée moteur recherche une propriété portant le nom hello « DeviceId » de type « String » dans les événements entrants hello.</span><span class="sxs-lookup"><span data-stu-id="32d0c-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="32d0c-119">Vous pouvez fournir plusieurs toojoin clé avec les événements hello.</span><span class="sxs-lookup"><span data-stu-id="32d0c-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="32d0c-120">correspondance de nom de propriété Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="32d0c-120">hello property name match is case-sensitive.</span></span>

     ![Créer le jeu de données de la référence du temps série Insights hello - détails](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="32d0c-122">Cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="32d0c-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="32d0c-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32d0c-123">Next steps</span></span>

* <span data-ttu-id="32d0c-124">[Gérez les données de référence](time-series-insights-manage-reference-data-csharp.md) par programme.</span><span class="sxs-lookup"><span data-stu-id="32d0c-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="32d0c-125">Pour la référence d’API complète hello, consultez [API de données de référence](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span><span class="sxs-lookup"><span data-stu-id="32d0c-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
