---
title: "les scripts aaaExtend U-SQL avec Python dans Azure données Lake Analytique | Documents Microsoft"
description: "Découvrez comment toorun Python code scripts U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="38021-103">Didacticiel : Bien démarrer avec l’extension de U-SQL avec Python</span><span class="sxs-lookup"><span data-stu-id="38021-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="38021-104">Les Extensions de Python pour U-SQL permettent aux développeurs tooperform parallèle massif l’exécution de code Python.</span><span class="sxs-lookup"><span data-stu-id="38021-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="38021-105">Hello, l’exemple suivant illustre les étapes de base hello :</span><span class="sxs-lookup"><span data-stu-id="38021-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="38021-106">Hello d’utilisation `REFERENCE ASSEMBLY` extensions Python instruction tooenable hello Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="38021-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="38021-107">À l’aide de hello `REDUCE` hello de toopartition opération d’entrée de données sur une clé</span><span class="sxs-lookup"><span data-stu-id="38021-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="38021-108">extensions Python pour U-SQL Hello incluent un réducteur intégré (`Extension.Python.Reducer`) qui exécute le code Python sur chaque réducteur de toohello sommets affecté</span><span class="sxs-lookup"><span data-stu-id="38021-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="38021-109">Hello script U-SQL contient le code Python hello incorporé qui a une fonction appelée `usqlml_main` qui accepte un pandas trame de données comme entrée et retourne une trame de données en tant que sortie pandas.</span><span class="sxs-lookup"><span data-stu-id="38021-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="38021-110">Intégration de Python à U-SQL</span><span class="sxs-lookup"><span data-stu-id="38021-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="38021-111">Types de données</span><span class="sxs-lookup"><span data-stu-id="38021-111">Datatypes</span></span>

* <span data-ttu-id="38021-112">Les colonnes numériques et de chaîne de U-SQL sont converties telles quelles-entre Pandas et U-SQL</span><span class="sxs-lookup"><span data-stu-id="38021-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="38021-113">Les valeurs NULL U-SQL sont tooand converti à partir de Pandas `NA` valeurs</span><span class="sxs-lookup"><span data-stu-id="38021-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="38021-114">Schémas</span><span class="sxs-lookup"><span data-stu-id="38021-114">Schemas</span></span>

* <span data-ttu-id="38021-115">Les vecteurs d’index dans Pandas ne sont pas pris en charge dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="38021-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="38021-116">Toutes les trames de données d’entrée dans la fonction de Python hello toujours ont un index numérique de 64 bits comprise entre 0 et le nombre de hello de lignes moins 1.</span><span class="sxs-lookup"><span data-stu-id="38021-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="38021-117">Les jeux de données U-SQL ne peut pas avoir de noms de colonnes dupliqués</span><span class="sxs-lookup"><span data-stu-id="38021-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="38021-118">Les noms de colonnes de jeux de données U-SQL qui ne sont pas des chaînes.</span><span class="sxs-lookup"><span data-stu-id="38021-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="38021-119">Versions de Python</span><span class="sxs-lookup"><span data-stu-id="38021-119">Python Versions</span></span>
<span data-ttu-id="38021-120">Seul Python 3.5.1 (compilé pour Windows) est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="38021-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="38021-121">Modules Python standard</span><span class="sxs-lookup"><span data-stu-id="38021-121">Standard Python modules</span></span>
<span data-ttu-id="38021-122">Tous les modules de Python standards hello sont inclus.</span><span class="sxs-lookup"><span data-stu-id="38021-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="38021-123">Modules Python supplémentaires</span><span class="sxs-lookup"><span data-stu-id="38021-123">Additional Python modules</span></span>
<span data-ttu-id="38021-124">Outre hello bibliothèques Python standard, plusieurs bibliothèques python couramment utilisées sont incluses :</span><span class="sxs-lookup"><span data-stu-id="38021-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="38021-125">Messages d’exception</span><span class="sxs-lookup"><span data-stu-id="38021-125">Exception Messages</span></span>
<span data-ttu-id="38021-126">Actuellement, une exception dans le code Python apparaît comme un échec de vertex générique.</span><span class="sxs-lookup"><span data-stu-id="38021-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="38021-127">Messages d’erreur hello travail U-SQL affiche Bonjour future, message d’exception hello Python.</span><span class="sxs-lookup"><span data-stu-id="38021-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="38021-128">Limitations de taille d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="38021-128">Input and Output size limitations</span></span>
<span data-ttu-id="38021-129">Chaque sommet a une quantité limitée de mémoire assignée tooit.</span><span class="sxs-lookup"><span data-stu-id="38021-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="38021-130">Actuellement, cette limite est de 6 Go pour une mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="38021-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="38021-131">Étant donné que hello trames de données d’entrée et de sortie doit exister dans la mémoire dans le code Python hello, taille totale hello hello entrée et sortie ne peut pas dépasser 6 Go.</span><span class="sxs-lookup"><span data-stu-id="38021-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="38021-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="38021-132">See also</span></span>
* [<span data-ttu-id="38021-133">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38021-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="38021-134">Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38021-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="38021-135">Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure</span><span class="sxs-lookup"><span data-stu-id="38021-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

