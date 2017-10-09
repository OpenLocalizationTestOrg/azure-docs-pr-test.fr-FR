---
title: aaaUse Hadoop Pig avec SSH sur un cluster HDInsight - Azure | Documents Microsoft
description: "Découvrez comment connecter tooa Hadoop basé sur Linux cluster avec SSH, puis utilisez hello Pig commande toorun Pig Latin instructions en mode interactif ou comme un traitement de la tâche."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Exécuter des travaux de Pig sur un cluster basé sur Linux avec hello commande de Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Découvrez comment toointeractively exécuter des travaux de Pig à partir d’un cluster de HDInsight de tooyour de connexion SSH. Hello langage de programmation Pig Latin permet des transformations toodescribe toohello appliqué d’entrée données tooproduce hello souhaité sortie.

> [!IMPORTANT]
> Hello étapes décrites dans ce document nécessitent un cluster HDInsight de basés sur Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="ssh"></a>Connexion avec SSH

Utiliser SSH tooconnect tooyour HDInsight cluster. exemple Hello connecte cluster tooa nommé **myhdinsight** en tant que compte hello nommé **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Si vous avez fourni une clé de certificat pour l’authentification SSH** lorsque vous avez créé le cluster HDInsight de hello, vous devrez peut-être l’emplacement de hello toospecify de clé privée de hello sur votre système client.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Si vous avez fourni un mot de passe pour l’authentification SSH** lorsque vous avez créé le cluster HDInsight de hello, fournir un mot de passe hello lorsque vous y êtes invité.

Pour en savoir plus sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Utilisez la commande de Pig hello

1. Une fois connecté, démarrez hello Pig interface de ligne de commande (CLI) à l’aide de hello de commande suivante :

        pig

    Après quelques instants, vous devriez voir une invite `grunt>` .

2. Entrez hello après l’instruction :

        LOGS = LOAD '/example/data/sample.log';

    Cette commande charge contenu hello du fichier d’exemple.log hello dans les journaux. Vous pouvez afficher le contenu hello du fichier de hello à l’aide de hello après l’instruction :

        DUMP LOGS;

3. Transformez ensuite les données de salutation en appliquant un niveau de journalisation de hello uniquement tooextract expression régulière à partir de chaque enregistrement à l’aide de hello après l’instruction :

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Vous pouvez utiliser **DUMP** tooview les données de salutation après la transformation de hello. Dans ce cas, utilisez `DUMP LEVELS;`.

4. Poursuivre l’application de transformations à l’aide des instructions de hello Bonjour tableau suivant :

    | Instruction Pig Latin | Les instruction hello |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Supprime les lignes qui contiennent une valeur null pour le niveau de journal hello et stocke les résultats hello dans `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Hello de groupes de lignes par niveau de journal et stocke les résultats de hello dans `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Crée un jeu de données qui contient chaque valeur unique au niveau journal et le nombre de fois où elle se produit. jeu de données Hello est stocké dans `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Trie les niveaux de journalisation hello par nombre (ordre décroissant) et le stocke dans `RESULT`. |

    > [!TIP]
    > Utilisez `DUMP` résultat de hello tooview de transformation hello après chaque étape.

5. Vous pouvez également enregistrer les résultats de hello d’une transformation à l’aide de hello `STORE` instruction. Par exemple, après l’instruction de hello enregistre hello `RESULT` toohello `/example/data/pigout` répertoire sur le stockage par défaut hello pour votre cluster :

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > les données de salutation sont stockées dans le répertoire spécifié de hello dans les fichiers nommés `part-nnnnn`. Si le répertoire de hello existe déjà, vous recevez une erreur.

6. tooexit hello des grunt à l’invite, entrez hello après l’instruction :

        QUIT;

### <a name="pig-latin-batch-files"></a>Fichiers de commandes Pig Latin

Vous pouvez également utiliser hello Pig commande toorun Latin Pig contenus dans un fichier.

1. Après avoir quitté l’invite de grunt hello, suivant de hello utilisez commande toopipe STDIN dans un fichier nommé `pigbatch.pig`. Ce fichier est créé dans le répertoire de base hello pour hello compte d’utilisateur SSH.

        cat > ~/pigbatch.pig

2. Tapez ou collez hello lignes suivantes, puis utilisez Ctrl + D, une fois.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Suivant de hello utilisez commande toorun hello `pigbatch.pig` fichier à l’aide des commandes de Pig hello.

        pig ~/pigbatch.pig

    Une fois le traitement par lots hello se termine, vous voyez hello suivant de sortie :

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Étapes suivantes

Pour obtenir des informations générales sur Pig dans HDInsight, consultez hello suivant du document :

* [Utilisation de Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md)

Pour plus d’informations sur les autres façons de toowork avec Hadoop dans HDInsight, consultez hello suivant des documents :

* [Utilisation de Hive avec Hadoop sur HDInsight](hdinsight-use-hive.md)
* [Utilisation de MapReduce avec Hadoop sur HDInsight](hdinsight-use-mapreduce.md)
