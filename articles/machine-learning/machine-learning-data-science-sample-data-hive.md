---
title: "aaaSample des données dans les tables de la ruche de HDInsight Azure | Documents Microsoft"
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
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="3ac86-103">Échantillonner des données dans des tables Hive Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3ac86-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="3ac86-104">Dans cet article, nous décrivons comment toodown-exemples de données stockées dans les tables de la ruche HDInsight Azure à l’aide de requêtes Hive.</span><span class="sxs-lookup"><span data-stu-id="3ac86-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="3ac86-105">Nous abordons trois méthodes d’échantillonnage communément utilisées :</span><span class="sxs-lookup"><span data-stu-id="3ac86-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="3ac86-106">Échantillonnage aléatoire uniforme</span><span class="sxs-lookup"><span data-stu-id="3ac86-106">Uniform random sampling</span></span>
* <span data-ttu-id="3ac86-107">Échantillonnage aléatoire par groupe</span><span class="sxs-lookup"><span data-stu-id="3ac86-107">Random sampling by groups</span></span>
* <span data-ttu-id="3ac86-108">Échantillonnage stratifié</span><span class="sxs-lookup"><span data-stu-id="3ac86-108">Stratified sampling</span></span>

<span data-ttu-id="3ac86-109">suivant de Hello **menu** lie tootopics qui décrivent comment toosample des données à partir de différents environnements de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ac86-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="3ac86-110">**Pourquoi échantillonner vos données ?**</span><span class="sxs-lookup"><span data-stu-id="3ac86-110">**Why sample your data?**</span></span>
<span data-ttu-id="3ac86-111">Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille.</span><span class="sxs-lookup"><span data-stu-id="3ac86-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="3ac86-112">Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3ac86-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="3ac86-113">Son rôle dans hello processus de science des données équipe est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="3ac86-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="3ac86-114">Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="3ac86-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="3ac86-115">Comment les requêtes Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="3ac86-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="3ac86-116">Requêtes Hive peuvent être envoyés à partir de la console de ligne de commande Hadoop hello sur le nœud principal de hello du cluster Hadoop de hello.</span><span class="sxs-lookup"><span data-stu-id="3ac86-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="3ac86-117">toodo cela, ouvrez une session sur le nœud principal de hello du cluster Hadoop de hello, ouvrez hello console de ligne de commande Hadoop et soumettre des requêtes de ruche hello à partir de là.</span><span class="sxs-lookup"><span data-stu-id="3ac86-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="3ac86-118">Pour obtenir des instructions sur la soumission de requêtes Hive dans la console de ligne de commande Hadoop hello, consultez [comment tooSubmit requêtes Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="3ac86-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="3ac86-119"><a name="uniform"></a> Échantillonnage aléatoire uniforme</span><span class="sxs-lookup"><span data-stu-id="3ac86-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="3ac86-120">Échantillonnage aléatoire uniforme signifie que chaque ligne dans le jeu de données hello autant de chance d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="3ac86-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="3ac86-121">Cela peut être implémentée en ajoutant un jeu de données de champ supplémentaire rand() toohello dans la requête « select » interne de hello et dans hello la requête « select » externe cette condition sur un champ aléatoire.</span><span class="sxs-lookup"><span data-stu-id="3ac86-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="3ac86-122">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="3ac86-122">Here is an example query:</span></span>

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

<span data-ttu-id="3ac86-123">Ici, `<sample rate, 0-1>` spécifie la proportion de hello d’enregistrements que les utilisateurs de hello souhaitent toosample.</span><span class="sxs-lookup"><span data-stu-id="3ac86-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="3ac86-124"><a name="group"></a> Échantillonnage aléatoire par groupe</span><span class="sxs-lookup"><span data-stu-id="3ac86-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="3ac86-125">Lorsque les données catégoriques d’échantillonnage, vous pouvez tooeither inclure ou exclure toutes les instances de hello d’une valeur particulière d’une variable par catégorie.</span><span class="sxs-lookup"><span data-stu-id="3ac86-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="3ac86-126">C’est ce que signifie le terme « échantillonnage par groupe ».</span><span class="sxs-lookup"><span data-stu-id="3ac86-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="3ac86-127">Par exemple, si vous avez une variable catégorique « État », qui a des valeurs NY, MA, autorité de certification, NJ, PA, etc., vous souhaitez que les enregistrements de hello même état toujours être ensemble, si elles sont échantillonnées ou non.</span><span class="sxs-lookup"><span data-stu-id="3ac86-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="3ac86-128">Voici un exemple de requête effectuant un échantillonnage par groupe :</span><span class="sxs-lookup"><span data-stu-id="3ac86-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="3ac86-129"><a name="stratified"></a>Échantillonnage stratifié</span><span class="sxs-lookup"><span data-stu-id="3ac86-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="3ac86-130">Échantillonnage aléatoire est stratifié avec égard tooa variable catégorielle lorsque des échantillons hello obtenus ont des valeurs catégorielles qui qui se trouvent dans hello même rapport, comme le remplissage de parent hello à partir de quels hello exemples ont été obtenues.</span><span class="sxs-lookup"><span data-stu-id="3ac86-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="3ac86-131">À l’aide de hello même exemple que ci-dessus, supposons que vos données ont des alimentations sous-chemin par les États, par exemple NJ a 100 observations, NY a 60 observations, et WA a 300 observations.</span><span class="sxs-lookup"><span data-stu-id="3ac86-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="3ac86-132">Si vous spécifiez le taux de hello de stratifié d’échantillonnage toobe 0,5, puis hello échantillon obtenu doit avoir environ 50, 30 et 150 observations NJ NY et WA respectivement.</span><span class="sxs-lookup"><span data-stu-id="3ac86-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="3ac86-133">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="3ac86-133">Here is an example query:</span></span>

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


<span data-ttu-id="3ac86-134">Pour plus d’informations sur les méthodes d’échantillonnage plus élaborées qui sont disponibles dans Hive, consultez la page consacrée aux [méthodes d’échantillonnage dans le manuel du langage](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="3ac86-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

