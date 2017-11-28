---
title: "Visualisation et dépannage de travaux Stream Analytics | Microsoft Docs"
description: "Découvrez comment visualiser un pipeline de tâches Stream Analytics pour le dépannage en libre-service à l’aide de la fonctionnalité de diagramme de diagnostic."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="f52cb-103">Visualisation et dépannage de travaux Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f52cb-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="f52cb-104">Dans Stream Analytics, comme dans d’autres technologies de cloud, la résolution des problèmes implique parfois d’étudier la raison pour laquelle une tâche ne produit pas la sortie attendue (ou même aucune sortie).</span><span class="sxs-lookup"><span data-stu-id="f52cb-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="f52cb-105">Dans cet esprit, Stream Analytics permet de visualiser une tâche de streaming.</span><span class="sxs-lookup"><span data-stu-id="f52cb-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="f52cb-106">Il est également utile en tant qu’outil de modélisation pour aider les personnes ayant besoin de documenter tout leur travail.</span><span class="sxs-lookup"><span data-stu-id="f52cb-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="f52cb-107">Dans le volet de visualisation, les entrées sont visibles, ainsi que la requête en cours d’exécution et toutes les sorties configurées.</span><span class="sxs-lookup"><span data-stu-id="f52cb-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="f52cb-108">Les problèmes liés à la connectivité ou à la configuration peuvent alors être plus évidents, et il peut également être utile d’afficher une représentation visuelle de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f52cb-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="f52cb-109">Utilisation de l’outil de diagramme de diagnostic</span><span class="sxs-lookup"><span data-stu-id="f52cb-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="f52cb-110">Pour accéder à ce visualiseur, cliquez simplement sur le bouton « Diagramme de diagnostic » dans le panneau « Paramètres » de la de la tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="f52cb-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="f52cb-112">Chaque entrée et sortie ont un code de couleur pour indiquer l’état actuel de ce composant, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f52cb-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="f52cb-114">Lorsque l’utilisateur souhaite consulter les étapes intermédiaires de sa requête pour comprendre les modèles de flux de données au sein d’une tâche, l’outil de visualisation fournit une vue de la répartition des étapes de la requête et de la séquence de flux.</span><span class="sxs-lookup"><span data-stu-id="f52cb-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="f52cb-115">Cliquez sur chaque étape de requête pour afficher la section correspondante dans un volet d’édition de requête, comme illustré.</span><span class="sxs-lookup"><span data-stu-id="f52cb-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="f52cb-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f52cb-117">Next steps</span></span>
* [<span data-ttu-id="f52cb-118">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f52cb-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f52cb-119">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f52cb-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f52cb-120">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f52cb-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f52cb-121">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f52cb-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f52cb-122">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f52cb-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

