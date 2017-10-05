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
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Didacticiel : Bien démarrer avec l’extension de U-SQL avec Python

Les extensions de Python pour U-SQL permettent aux développeurs d’effectuer une exécution parallèle massive de code Python. L'exemple suivant illustre les étapes de base :

* Utilisation de l’instruction `REFERENCE ASSEMBLY` pour activer les extensions Python pour le script U-SQL
* Utilisation de l’opération `REDUCE` pour partitionner les données d’entrée sur une clé
* Les extensions de Python pour U-SQL comprennent un réducteur intégré (`Extension.Python.Reducer`) qui exécute le code Python sur chaque vertex affecté au réducteur
* Le script U-SQL contient le code Python incorporé qui a une fonction appelée `usqlml_main` qui accepte un tableau de données Pandas en tant qu’entrée et retourne un tableau de données Pandas en tant que sortie.

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

## <a name="how-python-integrates-with-u-sql"></a>Intégration de Python à U-SQL

### <a name="datatypes"></a>Types de données

* Les colonnes numériques et de chaîne de U-SQL sont converties telles quelles-entre Pandas et U-SQL
* Les valeurs null de U-SQL sont converties en valeurs Pandas `NA` et à vice versa

### <a name="schemas"></a>Schémas

* Les vecteurs d’index dans Pandas ne sont pas pris en charge dans U-SQL. Tous les tableaux de données d’entrée dans la fonction Python ont toujours un index numérique de 64 bits compris entre 0 et le nombre de lignes moins 1. 
* Les jeux de données U-SQL ne peut pas avoir de noms de colonnes dupliqués
* Les noms de colonnes de jeux de données U-SQL qui ne sont pas des chaînes. 

### <a name="python-versions"></a>Versions de Python
Seul Python 3.5.1 (compilé pour Windows) est pris en charge. 

### <a name="standard-python-modules"></a>Modules Python standard
Tous les modules Python standard sont inclus.

### <a name="additional-python-modules"></a>Modules Python supplémentaires
Outre les bibliothèques Python standard, plusieurs bibliothèques python couramment utilisées sont incluses :

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Messages d’exception
Actuellement, une exception dans le code Python apparaît comme un échec de vertex générique. À l’avenir, les messages d’erreur de tâches U-SQL afficheront le message d’exception Python.

### <a name="input-and-output-size-limitations"></a>Limitations de taille d’entrée et de sortie
Chaque vertex possède une quantité limitée de mémoire qui lui est assignée. Actuellement, cette limite est de 6 Go pour une mise à jour automatique. Étant donné que les tableaux de données d’entrée et de sortie doivent exister dans la mémoire dans le code Python, la taille totale de l’entrée et de la sortie ne peut pas dépasser 6 Go.

## <a name="see-also"></a>Voir aussi
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure](data-lake-analytics-use-window-functions.md)

