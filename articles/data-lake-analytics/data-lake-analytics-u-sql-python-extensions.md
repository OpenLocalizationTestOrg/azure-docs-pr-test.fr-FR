---
title: Extension de scripts U-SQL avec Python dans Azure Data Lake Analytics | Microsoft Docs
description: "Découvrez comment exécuter un code Python dans des scripts U-SQL"
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
ms.openlocfilehash: d18ef1f747aee2fa01cef9891432d0461031ee4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="f4350-103">Didacticiel : Bien démarrer avec l’extension de U-SQL avec Python</span><span class="sxs-lookup"><span data-stu-id="f4350-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="f4350-104">Les extensions de Python pour U-SQL permettent aux développeurs d’effectuer une exécution parallèle massive de code Python.</span><span class="sxs-lookup"><span data-stu-id="f4350-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="f4350-105">L'exemple suivant illustre les étapes de base :</span><span class="sxs-lookup"><span data-stu-id="f4350-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="f4350-106">Utilisation de l’instruction `REFERENCE ASSEMBLY` pour activer les extensions Python pour le script U-SQL</span><span class="sxs-lookup"><span data-stu-id="f4350-106">Use the `REFERENCE ASSEMBLY` statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="f4350-107">Utilisation de l’opération `REDUCE` pour partitionner les données d’entrée sur une clé</span><span class="sxs-lookup"><span data-stu-id="f4350-107">Using the `REDUCE` operation to partition the input data on a key</span></span>
* <span data-ttu-id="f4350-108">Les extensions de Python pour U-SQL comprennent un réducteur intégré (`Extension.Python.Reducer`) qui exécute le code Python sur chaque vertex affecté au réducteur</span><span class="sxs-lookup"><span data-stu-id="f4350-108">The Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="f4350-109">Le script U-SQL contient le code Python incorporé qui a une fonction appelée `usqlml_main` qui accepte un tableau de données Pandas en tant qu’entrée et retourne un tableau de données Pandas en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="f4350-109">The U-SQL script contains the embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

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
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="f4350-110">Intégration de Python à U-SQL</span><span class="sxs-lookup"><span data-stu-id="f4350-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="f4350-111">Types de données</span><span class="sxs-lookup"><span data-stu-id="f4350-111">Datatypes</span></span>

* <span data-ttu-id="f4350-112">Les colonnes numériques et de chaîne de U-SQL sont converties telles quelles-entre Pandas et U-SQL</span><span class="sxs-lookup"><span data-stu-id="f4350-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="f4350-113">Les valeurs null de U-SQL sont converties en valeurs Pandas `NA` et à vice versa</span><span class="sxs-lookup"><span data-stu-id="f4350-113">U-SQL Nulls are converted to and from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="f4350-114">Schémas</span><span class="sxs-lookup"><span data-stu-id="f4350-114">Schemas</span></span>

* <span data-ttu-id="f4350-115">Les vecteurs d’index dans Pandas ne sont pas pris en charge dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f4350-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="f4350-116">Tous les tableaux de données d’entrée dans la fonction Python ont toujours un index numérique de 64 bits compris entre 0 et le nombre de lignes moins 1.</span><span class="sxs-lookup"><span data-stu-id="f4350-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="f4350-117">Les jeux de données U-SQL ne peut pas avoir de noms de colonnes dupliqués</span><span class="sxs-lookup"><span data-stu-id="f4350-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="f4350-118">Les noms de colonnes de jeux de données U-SQL qui ne sont pas des chaînes.</span><span class="sxs-lookup"><span data-stu-id="f4350-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="f4350-119">Versions de Python</span><span class="sxs-lookup"><span data-stu-id="f4350-119">Python Versions</span></span>
<span data-ttu-id="f4350-120">Seul Python 3.5.1 (compilé pour Windows) est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f4350-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="f4350-121">Modules Python standard</span><span class="sxs-lookup"><span data-stu-id="f4350-121">Standard Python modules</span></span>
<span data-ttu-id="f4350-122">Tous les modules Python standard sont inclus.</span><span class="sxs-lookup"><span data-stu-id="f4350-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="f4350-123">Modules Python supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f4350-123">Additional Python modules</span></span>
<span data-ttu-id="f4350-124">Outre les bibliothèques Python standard, plusieurs bibliothèques python couramment utilisées sont incluses :</span><span class="sxs-lookup"><span data-stu-id="f4350-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="f4350-125">Messages d’exception</span><span class="sxs-lookup"><span data-stu-id="f4350-125">Exception Messages</span></span>
<span data-ttu-id="f4350-126">Actuellement, une exception dans le code Python apparaît comme un échec de vertex générique.</span><span class="sxs-lookup"><span data-stu-id="f4350-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="f4350-127">À l’avenir, les messages d’erreur de tâches U-SQL afficheront le message d’exception Python.</span><span class="sxs-lookup"><span data-stu-id="f4350-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="f4350-128">Limitations de taille d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="f4350-128">Input and Output size limitations</span></span>
<span data-ttu-id="f4350-129">Chaque vertex possède une quantité limitée de mémoire qui lui est assignée.</span><span class="sxs-lookup"><span data-stu-id="f4350-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="f4350-130">Actuellement, cette limite est de 6 Go pour une mise à jour automatique.</span><span class="sxs-lookup"><span data-stu-id="f4350-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="f4350-131">Étant donné que les tableaux de données d’entrée et de sortie doivent exister dans la mémoire dans le code Python, la taille totale de l’entrée et de la sortie ne peut pas dépasser 6 Go.</span><span class="sxs-lookup"><span data-stu-id="f4350-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4350-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f4350-132">See also</span></span>
* [<span data-ttu-id="f4350-133">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f4350-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f4350-134">Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4350-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="f4350-135">Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure</span><span class="sxs-lookup"><span data-stu-id="f4350-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

