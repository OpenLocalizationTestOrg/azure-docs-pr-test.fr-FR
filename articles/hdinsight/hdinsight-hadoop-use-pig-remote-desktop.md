---
title: "aaaUse Hadoop Pig avec le Bureau à distance dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello instructions de Pig Latin Pig commande toorun à partir d’un bureau à distance connexion tooa basé sur Windows de cluster Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Exécution de tâches Pig depuis une connexion Bureau à distance
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Ce document fournit une procédure pas à pas pour l’utilisation d’instructions hello Pig commandes toorun Pig Latin d’un cluster de basés sur Windows de HDInsight de tooa connexion Bureau à distance. Pig Latin vous permet de toocreate MapReduce applications en décrivant les transformations de données, plutôt que mapper et réduire des fonctions.

> [!IMPORTANT]
> Bureau à distance n’est disponible sur les clusters HDInsight utilisent Windows comme système d’exploitation de hello. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Pour HDInsight 3.4 ou supérieure, consultez [utilisez Pig avec HDInsight et SSH](hdinsight-hadoop-use-pig-ssh.md) pour plus d’informations sur l’exécution de manière interactive Pig travaux directement sur hello de cluster à partir d’une ligne de commande.

## <a id="prereq"></a>Configuration requise
toocomplete hello étapes décrites dans cet article, vous devez suivant de hello.

* un cluster HDInsight basé sur Windows (Hadoop sur HDInsight)
* Un ordinateur client avec Windows 10, Windows 8 ou Windows 7

## <a id="connect"></a>Connexion avec le Bureau à distance
Activer le Bureau à distance pour le cluster HDInsight de hello, puis connecter tooit en suivant les instructions de hello sur [connecter clusters tooHDInsight à l’aide du protocole RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Utilisez la commande de Pig hello
1. Une fois que vous avez une connexion Bureau à distance, démarrer hello **ligne de commande Hadoop** en utilisant l’icône de hello sur le bureau de hello.
2. Utilisez hello toostart hello Pig commande suivante :

        %pig_home%\bin\pig

    Une invite `grunt>` s’affiche.
3. Entrez hello après l’instruction :

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Cette commande charge contenu hello du fichier d’exemple.log hello dans les fichiers de journaux hello. Vous pouvez afficher le contenu hello du fichier de hello à l’aide de hello de commande suivante :

        DUMP LOGS;
4. Transformer les données de hello en appliquant un niveau de journalisation de hello uniquement tooextract expression régulière à partir de chaque enregistrement :

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Vous pouvez utiliser **DUMP** tooview les données de salutation après la transformation de hello. Dans ce cas, `DUMP LEVELS;`.
5. Continuer l’application de transformations à l’aide de hello suivant les instructions. Utilisez `DUMP` résultat de hello tooview de transformation hello après chaque étape.

    <table>
    <tr>
    <th>Instruction</th><th>Résultat</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>Supprime les lignes qui contiennent une valeur null pour le niveau de journal hello et stocke les résultats de hello dans FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>Hello de groupes de lignes par niveau de journal et stocke des résultats de hello dans GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>Crée un jeu de données qui contient chaque valeur unique au niveau journal et le nombre de fois où elle se produit. Ces informations sont stockées dans FREQUENCIES</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>Les niveaux de journalisation hello par nombre (ordre décroissant) et stocke des commandes dans les résultats</td>
    </tr>
    </table>
6.Vous pouvez également enregistrer les résultats de hello d’une transformation à l’aide de hello `STORE` instruction. Par exemple, hello commande suivante enregistre hello `RESULT` toohello **/example/data/pigout** répertoire dans le conteneur de stockage par défaut hello pour votre cluster :

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > les données de salutation sont stockées dans le répertoire spécifié de hello dans les fichiers nommés **partie-nnnnn**. Si le répertoire de hello existe déjà, vous recevrez un message d’erreur.
   >
   >
7. tooexit hello des grunt à l’invite, entrez hello après l’instruction.

        QUIT;

### <a name="pig-latin-batch-files"></a>Fichiers de commandes Pig Latin
Vous pouvez également utiliser hello Pig commande toorun Latin Pig qui est contenue dans un fichier.

1. Après avoir quitté l’invite de grunt hello, ouvrez **bloc-notes** et créer un nouveau fichier nommé **pigbatch.pig** Bonjour **PIG_HOME %** active.
2. Type ou à la suite de hello coller des lignes en hello **pigbatch.pig** de fichier, puis enregistrez-le :

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Hello utilisation suivant toorun hello **pigbatch.pig** fichier à l’aide de la commande de pig hello.

        pig %PIG_HOME%\pigbatch.pig

    Lors de la tâche hello est terminée, vous devez voir hello suivant de sortie, qui doit être hello de même que lorsque vous avez utilisé `DUMP RESULT;` dans les étapes précédentes hello :

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Résumé
Comme vous pouvez le voir, hello commande de Pig vous permet de toointeractively exécuter des opérations de MapReduce ou exécuter des travaux Pig Latin qui est stockés dans un fichier de commandes.

## <a id="nextsteps"></a>Étapes suivantes
Pour obtenir des informations générales sur Pig dans HDInsight :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)

Pour plus d’informations sur d’autres méthodes de travail avec Hadoop sur HDInsight :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)
