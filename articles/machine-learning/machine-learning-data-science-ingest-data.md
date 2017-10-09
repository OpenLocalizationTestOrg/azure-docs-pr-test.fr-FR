---
title: "données aaaLoad dans des environnements de stockage Azure pour analytique | Documents Microsoft"
description: "Déplacer les données tooand à partir du stockage d’objets Blob Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="72dd2-103">Charger des données dans des environnements de stockage à des fins d’analyse</span><span class="sxs-lookup"><span data-stu-id="72dd2-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="72dd2-104">Hello, processus de science des données équipe requiert que données ingérées ou chargées dans une variété de stockage différents environnements toobe traité ou analysé de manière plus appropriée de hello dans chaque étape du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="72dd2-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="72dd2-105">Les destinations de données couramment utilisées pour le traitement sont le stockage d’objets blob Azure, les bases de données SQL Azure, SQL Server sur machine virtuelle Azure, HDInsight (Hadoop) et Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="72dd2-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="72dd2-106">Cela **menu** lie tootopics qui décrivent comment tooingest les données dans ces ciblent les environnements où les données de salutation sont stockées et traitées.</span><span class="sxs-lookup"><span data-stu-id="72dd2-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="72dd2-107">Technique et les besoins professionnels, ainsi que les emplacement initial de hello, mettre en forme et la taille de vos données détermineront les environnements cibles hello dans le hello données doivent toobe ingéré tooachieve hello objectifs de votre analyse.</span><span class="sxs-lookup"><span data-stu-id="72dd2-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="72dd2-108">Il n’est pas rare qu’un toobe de données toorequire scénario déplacé entre plusieurs environnements tooachieve hello diverses tâches, tooconstruct requis un modèle prédictif.</span><span class="sxs-lookup"><span data-stu-id="72dd2-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="72dd2-109">Cette suite de tâches peut par exemple inclure l’exploration des données, leur prétraitement, leur nettoyage, l’échantillonnage et l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="72dd2-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

