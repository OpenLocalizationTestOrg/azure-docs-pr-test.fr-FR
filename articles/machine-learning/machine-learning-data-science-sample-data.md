---
title: "données aaaSample dans Azure, SQL Server, les conteneurs d’objets blob et tables de la ruche | Documents Microsoft"
description: "Comment les données de tooexplore stockées dans diverses enviromnents Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="7bdb2-103"><a name="heading"></a>Échantillonner des données dans des conteneurs d'objets blob Azure, SQL Server et des tables Hive</span><span class="sxs-lookup"><span data-stu-id="7bdb2-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="7bdb2-104">Ce document lie tootopics couvre comment toosample les données stockées dans un des trois emplacements Azure :</span><span class="sxs-lookup"><span data-stu-id="7bdb2-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="7bdb2-105">**données de conteneurs d’objets blob Azure** sont échantillonnées par le biais de leur téléchargement par programmation, puis de leur échantillonnage à l’aide d’un exemple de code Python.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="7bdb2-106">**Les données de SQL Server** sont échantillonnées à l’aide de SQL et hello langage de programmation Python.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="7bdb2-107">**tables Hive** sont échantillonnées à l’aide de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="7bdb2-108">suivant de Hello **menu** liens toohello rubriques qui décrivent comment toosample des données à partir de chacun de ces environnements de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="7bdb2-109">Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="7bdb2-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="7bdb2-110">**Pourquoi échantillonner des données ?**</span><span class="sxs-lookup"><span data-stu-id="7bdb2-110">**Why sample data?**</span></span>

<span data-ttu-id="7bdb2-111">Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="7bdb2-112">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="7bdb2-113">Son rôle dans hello Cortana Analytique processus est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="7bdb2-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

