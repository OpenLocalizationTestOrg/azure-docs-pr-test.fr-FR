---
title: "procédures pas à pas pour la science des aaaHDInsight Hadoop données à l’aide de la ruche sur Azure | Documents Microsoft"
description: "Exemples de hello processus de science des données équipe présentant hello utilisent de ruche sur analytique prédictive de toodo Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="84b5b-103">Guides de la science des données HDInsight Hadoop avec Hive sur Azure</span><span class="sxs-lookup"><span data-stu-id="84b5b-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="84b5b-104">Ces procédures pas à pas utiliser Hive avec un analytique de prédictive toodo de cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="84b5b-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="84b5b-105">Elles suivent les étapes hello hello processus de science des données équipe.</span><span class="sxs-lookup"><span data-stu-id="84b5b-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="84b5b-106">Pour une vue d’ensemble de hello processus de science des données équipe, consultez [processus de science des données](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84b5b-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="84b5b-107">Pour une introduction tooAzure HDInsight, consultez [Introduction tooAzure HDInsight, hello technologique Hadoop et des clusters Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="84b5b-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="84b5b-108">Données supplémentaires pour la science des procédures pas à pas qui s’exécutent hello équipe données science des processus sont regroupés par hello **plateforme** qu’ils utilisent :</span><span class="sxs-lookup"><span data-stu-id="84b5b-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="84b5b-109">Prédire les pourboires laissés aux taxis avec Hive et HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="84b5b-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="84b5b-110">Hello [utilisez HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) procédure pas à pas utilise des données à partir de New York taxi toopredict :</span><span class="sxs-lookup"><span data-stu-id="84b5b-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="84b5b-111">si un pourboire sera laissé ;</span><span class="sxs-lookup"><span data-stu-id="84b5b-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="84b5b-112">distribution Hello des montants de Conseil</span><span class="sxs-lookup"><span data-stu-id="84b5b-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="84b5b-113">scénario de Hello est implémentée à l’aide de la ruche avec une [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="84b5b-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="84b5b-114">Vous découvrez comment toostore, Explorer et fonctionnalité données d’ingénierie à rebours à partir d’un voyage de taxi NYC publiquement disponible et les prix de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="84b5b-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="84b5b-115">Vous utilisez Azure Machine Learning toobuild et déployez des modèles de hello.</span><span class="sxs-lookup"><span data-stu-id="84b5b-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="84b5b-116">Prédire les clics publicitaires avec Hive et HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="84b5b-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="84b5b-117">Hello [utilisez Azure HDInsight Hadoop Clusters sur un jeu de données de 1 to](machine-learning-data-science-process-hive-criteo-walkthrough.md) procédure pas à pas utilise un disponible publiquement [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) cliquez sur toopredict du jeu de données si une info-bulle est payée et hello gamme de quantités attendu.</span><span class="sxs-lookup"><span data-stu-id="84b5b-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="84b5b-118">scénario de Hello est implémentée à l’aide de la ruche avec une [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Explorer, ingénieur de fonctionnalité et vers le bas des exemples de données.</span><span class="sxs-lookup"><span data-stu-id="84b5b-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="84b5b-119">Elle utilise Azure Machine Learning toobuild, l’apprentissage et score d’un modèle de classification binaire prédire si un utilisateur clique sur une publication.</span><span class="sxs-lookup"><span data-stu-id="84b5b-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="84b5b-120">procédure pas à pas Hello conclut montrant comment toopublish un de ces modèles comme un service Web.</span><span class="sxs-lookup"><span data-stu-id="84b5b-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="84b5b-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84b5b-121">Next steps</span></span>

<span data-ttu-id="84b5b-122">Pour en savoir plus sur les composants clés hello qui composent hello processus de science des données de Team, consultez [vue d’ensemble du processus de science des données équipe](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84b5b-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="84b5b-123">Pour une présentation du cycle de vie de processus de science des données équipe hello que vous pouvez utiliser toostructure vos projets de science des données, consultez [cycle de vie des processus de science des données équipe](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="84b5b-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="84b5b-124">cycle de vie Hello décrit les étapes de hello, à partir du début toofinish, que les projets suivent généralement lorsqu’elles sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="84b5b-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

