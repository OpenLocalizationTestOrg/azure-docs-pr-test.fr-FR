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
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Didacticiel : Bien démarrer avec l’extension de U-SQL avec Python

Les Extensions de Python pour U-SQL permettent aux développeurs tooperform parallèle massif l’exécution de code Python. Hello, l’exemple suivant illustre les étapes de base hello :

* Hello d’utilisation `REFERENCE ASSEMBLY` extensions Python instruction tooenable hello Script U-SQL
* À l’aide de hello `REDUCE` hello de toopartition opération d’entrée de données sur une clé
* extensions Python pour U-SQL Hello incluent un réducteur intégré (`Extension.Python.Reducer`) qui exécute le code Python sur chaque réducteur de toohello sommets affecté
* Hello script U-SQL contient le code Python hello incorporé qui a une fonction appelée `usqlml_main` qui accepte un pandas trame de données comme entrée et retourne une trame de données en tant que sortie pandas.

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

## <a name="how-python-integrates-with-u-sql"></a>Intégration de Python à U-SQL

### <a name="datatypes"></a>Types de données

* Les colonnes numériques et de chaîne de U-SQL sont converties telles quelles-entre Pandas et U-SQL
* Les valeurs NULL U-SQL sont tooand converti à partir de Pandas `NA` valeurs

### <a name="schemas"></a>Schémas

* Les vecteurs d’index dans Pandas ne sont pas pris en charge dans U-SQL. Toutes les trames de données d’entrée dans la fonction de Python hello toujours ont un index numérique de 64 bits comprise entre 0 et le nombre de hello de lignes moins 1. 
* Les jeux de données U-SQL ne peut pas avoir de noms de colonnes dupliqués
* Les noms de colonnes de jeux de données U-SQL qui ne sont pas des chaînes. 

### <a name="python-versions"></a>Versions de Python
Seul Python 3.5.1 (compilé pour Windows) est pris en charge. 

### <a name="standard-python-modules"></a>Modules Python standard
Tous les modules de Python standards hello sont inclus.

### <a name="additional-python-modules"></a>Modules Python supplémentaires
Outre hello bibliothèques Python standard, plusieurs bibliothèques python couramment utilisées sont incluses :

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Messages d’exception
Actuellement, une exception dans le code Python apparaît comme un échec de vertex générique. Messages d’erreur hello travail U-SQL affiche Bonjour future, message d’exception hello Python.

### <a name="input-and-output-size-limitations"></a>Limitations de taille d’entrée et de sortie
Chaque sommet a une quantité limitée de mémoire assignée tooit. Actuellement, cette limite est de 6 Go pour une mise à jour automatique. Étant donné que hello trames de données d’entrée et de sortie doit exister dans la mémoire dans le code Python hello, taille totale hello hello entrée et sortie ne peut pas dépasser 6 Go.

## <a name="see-also"></a>Voir aussi
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure](data-lake-analytics-use-window-functions.md)

