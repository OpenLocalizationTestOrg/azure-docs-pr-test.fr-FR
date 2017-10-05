---
title: "Charger des données dans des environnements de stockage Azure à des fins d’analyse | Microsoft Docs"
description: "Déplacer des données vers et depuis un stockage Azure Blob"
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
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="5a004-103">Charger des données dans des environnements de stockage à des fins d’analyse</span><span class="sxs-lookup"><span data-stu-id="5a004-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="5a004-104">Le processus Team Data Science nécessite que les données soient reçues ou chargées dans différents environnements de stockage pour y être traitées ou analysées de la façon la plus appropriée à chaque étape du processus.</span><span class="sxs-lookup"><span data-stu-id="5a004-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="5a004-105">Les destinations de données couramment utilisées pour le traitement sont le stockage d’objets blob Azure, les bases de données SQL Azure, SQL Server sur machine virtuelle Azure, HDInsight (Hadoop) et Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a004-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="5a004-106">Ce **menu** pointe vers des rubriques qui décrivent comment recevoir les données dans les environnements cibles où les données sont stockées et traitées.</span><span class="sxs-lookup"><span data-stu-id="5a004-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="5a004-107">Les besoins techniques et ceux de l’entreprise, ainsi que l’emplacement initial, le format et la taille de vos données déterminent l’environnement cible dans lequel les données doivent être reçues pour atteindre les objectifs de votre analyse.</span><span class="sxs-lookup"><span data-stu-id="5a004-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="5a004-108">Il n’est pas rare pour un scénario d’exiger le déplacement des données entre plusieurs environnements pour arriver à effectuer les différentes tâches nécessaires pour construire un modèle prédictif.</span><span class="sxs-lookup"><span data-stu-id="5a004-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="5a004-109">Cette suite de tâches peut par exemple inclure l’exploration des données, leur prétraitement, leur nettoyage, l’échantillonnage et l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="5a004-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

