---
title: "aaaVisualize et résoudre les tâches de flux de données Analytique | Documents Microsoft"
description: "Découvrez comment toovisualize une tâche de flux de données Analytique de pipeline pour le dépannage à l’aide de la fonctionnalité de diagramme hello diagnostics de libre-service."
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
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="a3b59-103">Visualisation et dépannage de travaux Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3b59-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="a3b59-104">Dans le flux de données Analytique, comme avec d’autres technologies de nuage, résolution des problèmes sont parfois toolook nécessaire en raison pour laquelle une tâche ne produit pas de sortie de hello attendu (ou de sortie d’ailleurs).</span><span class="sxs-lookup"><span data-stu-id="a3b59-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="a3b59-105">Dans cet esprit, flux de données Analytique fournit une fonctionnalité hello pour visualiser un travail de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a3b59-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="a3b59-106">Cela est également utile comme outil de modélisation et a hello autre avantage pour celles qui nécessitent une documentation de leur travail.</span><span class="sxs-lookup"><span data-stu-id="a3b59-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="a3b59-107">Dans la visualisation de hello entrées hello de panneau de configuration sont visibles, ainsi que la requête hello en cours d’exécution, et ensuite toutes les sorties hello configuré.</span><span class="sxs-lookup"><span data-stu-id="a3b59-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="a3b59-108">Problèmes de connectivité ou de configuration peuvent deviennent plus évidents et il peut également être utile toosee une représentation visuelle de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="a3b59-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="a3b59-109">À l’aide des outils de diagramme de diagnostic hello</span><span class="sxs-lookup"><span data-stu-id="a3b59-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="a3b59-110">tooaccess ce visualiseur, cliquez simplement sur hello bouton « Diagramme de diagnostic » dans hello panneau « Paramètres » de hello de tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="a3b59-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="a3b59-112">Chaque entrée et la sortie sont codée par couleur tooindicate hello état actuel de ce composant, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a3b59-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="a3b59-114">Lorsque l’utilisateur hello veut toolook requête intermédiaire étapes toounderstand hello données flux modèles à l’intérieur d’un travail, outil de visualisation hello fournit une vue de répartition hello de requête de hello dans ses étapes et la séquence de flux de hello.</span><span class="sxs-lookup"><span data-stu-id="a3b59-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="a3b59-115">En cliquant sur chaque étape de requête affiche la section correspondante de hello dans une requête de modification de volet, comme illustré.</span><span class="sxs-lookup"><span data-stu-id="a3b59-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="a3b59-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3b59-117">Next steps</span></span>
* [<span data-ttu-id="a3b59-118">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="a3b59-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a3b59-119">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3b59-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a3b59-120">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3b59-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a3b59-121">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3b59-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a3b59-122">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3b59-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

