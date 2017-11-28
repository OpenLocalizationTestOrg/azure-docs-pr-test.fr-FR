---
title: "Échantillonner des données dans des tables Hive Azure HDInsight | Microsoft Docs"
description: "Sous-échantillonnage de données dans des tables Hive Azure HDInsight (Hadoop)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="dfa3b-103">Échantillonner des données dans des tables Hive Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dfa3b-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="dfa3b-104">Dans cet article, nous décrivons à présent la procédure de sous-échantillonnage des données stockées dans des tables Hive Azure HDInsight à l'aide de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-104">In this article, we describe how to down-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="dfa3b-105">Nous abordons trois méthodes d’échantillonnage communément utilisées :</span><span class="sxs-lookup"><span data-stu-id="dfa3b-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="dfa3b-106">Échantillonnage aléatoire uniforme</span><span class="sxs-lookup"><span data-stu-id="dfa3b-106">Uniform random sampling</span></span>
* <span data-ttu-id="dfa3b-107">Échantillonnage aléatoire par groupe</span><span class="sxs-lookup"><span data-stu-id="dfa3b-107">Random sampling by groups</span></span>
* <span data-ttu-id="dfa3b-108">Échantillonnage stratifié</span><span class="sxs-lookup"><span data-stu-id="dfa3b-108">Stratified sampling</span></span>

<span data-ttu-id="dfa3b-109">Le **menu** ci-après pointe vers des rubriques qui expliquent comment échantillonner des données dans différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="dfa3b-110">**Pourquoi échantillonner vos données ?**</span><span class="sxs-lookup"><span data-stu-id="dfa3b-110">**Why sample your data?**</span></span>
<span data-ttu-id="dfa3b-111">Si vous prévoyez d’analyser un jeu de données volumineux, il est généralement recommandé de sous-échantillonner les données afin de réduire leur taille sous une forme plus facilement exploitable, mais toujours représentative.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="dfa3b-112">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="dfa3b-113">Son rôle dans le processus TDSP (Team Data Science Process) consiste à permettre le prototypage rapide des fonctions de traitement des données et des modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="dfa3b-114">Cette tâche d’échantillonnage est une étape du [processus TDSP (Team Data Science Process)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="dfa3b-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="dfa3b-115">Envoi de requêtes Hive</span><span class="sxs-lookup"><span data-stu-id="dfa3b-115">How to submit Hive queries</span></span>
<span data-ttu-id="dfa3b-116">Les requêtes Hive peuvent être envoyées à partir de console de ligne de commande Hadoop, sur le nœud principal du cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-116">Hive queries can be submitted from the Hadoop Command Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="dfa3b-117">Pour effectuer cette opération, connectez-vous au nœud principal du cluster Hadoop, ouvrez la console de ligne de commande Hadoop, puis soumettez les requêtes Hive à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="dfa3b-118">Pour plus d’informations sur la soumission de requêtes Hive dans la console de ligne de commande Hadoop, voir [Envoi de requêtes Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="dfa3b-118">For instructions on submitting Hive queries in the Hadoop Command Line console, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="dfa3b-119"><a name="uniform"></a> Échantillonnage aléatoire uniforme</span><span class="sxs-lookup"><span data-stu-id="dfa3b-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="dfa3b-120">Le terme « échantillonnage aléatoire uniforme » signifie que chaque ligne du jeu de données a la même chance d’être échantillonnée que les autres.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="dfa3b-121">Vous pouvez implémenter cette méthode en ajoutant un champ supplémentaire rand() au jeu de données dans la requête « select » interne et dans la requête « select » externe conditionnant ce champ aléatoire.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-121">This can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="dfa3b-122">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="dfa3b-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="dfa3b-123">Dans cet exemple, la chaîne `<sample rate, 0-1>` spécifie la proportion d’enregistrements que les utilisateurs veulent échantillonner.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <span data-ttu-id="dfa3b-124"><a name="group"></a> Échantillonnage aléatoire par groupe</span><span class="sxs-lookup"><span data-stu-id="dfa3b-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="dfa3b-125">Lorsque vous échantillonnez des données catégorielles, vous pouvez choisir d’inclure ou d’exclure toutes les instances d’une valeur spécifique d’une valeur catégorielle.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-125">When sampling categorical data, you may want to either include or exclude all of the instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="dfa3b-126">C’est ce que signifie le terme « échantillonnage par groupe ».</span><span class="sxs-lookup"><span data-stu-id="dfa3b-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="dfa3b-127">Par exemple, si vous disposez d’une valeur catégorielle « État », qui présente les valeurs NY, MA, CA, NJ, PA, etc., vous voulez que les enregistrements du même État soient toujours regroupés, qu’ils soient ou non échantillonnés.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of the same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="dfa3b-128">Voici un exemple de requête effectuant un échantillonnage par groupe :</span><span class="sxs-lookup"><span data-stu-id="dfa3b-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="dfa3b-129"><a name="stratified"></a>Échantillonnage stratifié</span><span class="sxs-lookup"><span data-stu-id="dfa3b-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="dfa3b-130">L’échantillonnage aléatoire est stratifié par rapport à une variable catégorielle lorsque les échantillons obtenus comportent des valeurs de cette catégorie qui existent dans la même proportion que dans la population parente à partir de laquelle les échantillons ont été obtenus.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have values of that categorical that are in the same ratio as in the parent population from which the samples were obtained.</span></span> <span data-ttu-id="dfa3b-131">En considérant le même exemple que ci-dessus, supposons que vos données comportent des sous-populations par État. Par exemple, NJ présente 100 observations, NY 60 observations et WA 300 observations.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-131">Using the same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="dfa3b-132">Si vous spécifiez un taux d’échantillonnage stratifié de 0,5, l’échantillon obtenu pour NJ, NY et WA sera respectivement d’environ 50, 30 et 150 observations.</span><span class="sxs-lookup"><span data-stu-id="dfa3b-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="dfa3b-133">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="dfa3b-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="dfa3b-134">Pour plus d’informations sur les méthodes d’échantillonnage plus élaborées qui sont disponibles dans Hive, consultez la page consacrée aux [méthodes d’échantillonnage dans le manuel du langage](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="dfa3b-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

