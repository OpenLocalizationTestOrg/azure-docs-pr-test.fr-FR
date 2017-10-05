---
title: "Échantillonner des données dans des conteneurs d’objets blob Azure, SQL Server et des tables Hive | Microsoft Docs"
description: "Comment explorer les données stockées dans différents environnements Azure."
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="b0863-103"><a name="heading"></a>Échantillonner des données dans des conteneurs d'objets blob Azure, SQL Server et des tables Hive</span><span class="sxs-lookup"><span data-stu-id="b0863-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="b0863-104">Ce document contient des liens vers des rubriques qui expliquent comment échantillonner les données stockées dans l’un des trois emplacements Azure :</span><span class="sxs-lookup"><span data-stu-id="b0863-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="b0863-105">**données de conteneurs d’objets blob Azure** sont échantillonnées par le biais de leur téléchargement par programmation, puis de leur échantillonnage à l’aide d’un exemple de code Python.</span><span class="sxs-lookup"><span data-stu-id="b0863-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="b0863-106">**données SQL Server** sont échantillonnées à l’aide de SQL et du langage de programmation Python.</span><span class="sxs-lookup"><span data-stu-id="b0863-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="b0863-107">**tables Hive** sont échantillonnées à l’aide de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="b0863-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="b0863-108">Le **menu** ci-dessous dirige vers les rubriques qui expliquent comment échantillonner des données dans chacun de ces environnements de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b0863-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="b0863-109">Cette tâche d’échantillonnage est une étape du [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="b0863-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="b0863-110">**Pourquoi échantillonner des données ?**</span><span class="sxs-lookup"><span data-stu-id="b0863-110">**Why sample data?**</span></span>

<span data-ttu-id="b0863-111">Si vous prévoyez d’analyser un jeu de données volumineux, il est généralement recommandé de sous-échantillonner les données afin de réduire leur taille sous une forme plus facilement exploitable, mais toujours représentative.</span><span class="sxs-lookup"><span data-stu-id="b0863-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="b0863-112">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="b0863-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="b0863-113">Son rôle dans le processus Cortana Analytics consiste à permettre le prototypage rapide des fonctions de traitement des données et des modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="b0863-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

