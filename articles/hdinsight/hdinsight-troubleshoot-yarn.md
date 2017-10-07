---
title: "aaaTroubleshoot fils à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses aux questions de toocommon sur l’utilisation des fils de Apache Hadoop et Azure HDInsight."
keywords: "Azure HDInsight, YARN, FAQ, guide de dépannage, questions courantes"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Résoudre les problèmes YARN à l’aide d’Azure HDInsight

En savoir plus sur les questions hello et leurs résolutions lorsque vous travaillez avec des charges utiles Apache Hadoop fils dans Apache Ambari.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Comment créer une file d’attente YARN sur un cluster ?


### <a name="resolution-steps"></a>Étapes de résolution 

Utilisez hello ci-dessous les étapes dans Ambari toocreate une nouvelle file d’attente de fils, puis équilibrer allocation de capacité hello parmi toutes les files d’attente de hello. 

Dans cet exemple, deux files d’attente existantes (**par défaut** et **thriftsvr**) les deux sont modifiés à partir de 50 % la capacité too25 % capacité, qui offre une capacité de 50 % hello nouvelle file d’attente (spark).
| File d'attente | Capacity | Capacité maximale |
| --- | --- | --- | --- |
| default | 25% | 50% |
| thrftsvr | 25% | 50% |
| spark | 50% | 50% |

1. Sélectionnez hello **Ambari vues** icône et modèle de grille puis sélectionnez hello. Sélectionnez ensuite **YARN Queue Manager** (Gestionnaire de files d’attente YARN).

    ![Sélectionnez l’icône du mode de Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Sélectionnez hello **par défaut** file d’attente.

    ![Sélectionnez la file d’attente par défaut de hello](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Pourquoi **par défaut** file d’attente, modifiez hello **capacité** de 50 % too25 %. Pourquoi **thriftsvr** file d’attente, modifiez hello **capacité** too25 %.

    ![Modification hello capacité too25 % des files d’attente par défaut et thriftsvr hello](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. toocreate une nouvelle file d’attente, sélectionnez **ajouter une file d’attente**.

    ![Sélectionner Add Queue](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Nom hello nouvelle file d’attente.

    ![Nom de la file d’attente de hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Laissez hello **capacité** des valeurs à 50 %, puis sélectionnez hello **Actions** bouton.

    ![Sélectionnez le bouton d’Actions hello](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Sélectionnez **Save and Refresh Queues** (Enregistrer et actualiser les files d’attente).

    ![Sélectionner Save and Refresh Queues](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Ces modifications sont visibles immédiatement sur hello interface utilisateur du Planificateur de fils.

### <a name="additional-reading"></a>Documentation supplémentaire

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Comment télécharger les journaux YARN à partir d’un cluster ?


### <a name="resolution-steps"></a>Étapes de résolution 

1. Se connecter toohello HDInsight cluster à l’aide d’un client Secure Shell (SSH). Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-2).

2. toolist tous hello ID d’application des applications fils hello qui sont en cours d’exécution, exécutez hello de commande suivante :

    ```apache
    yarn top
    ```
    ID de Hello sont répertoriés dans hello **APPLICATIONID** colonne. Vous pouvez télécharger les journaux à partir de hello **APPLICATIONID** colonne.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. journaux de conteneur toodownload fils pour tous les maîtres d’application, utilisez hello de commande suivante :
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Cette commande crée un fichier journal nommé amlogs.txt. 

4. journaux conteneur toodownload fils seul maître application de la dernière hello, utilisez hello de commande suivante :

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Cette commande crée un fichier journal nommé latestamlogs.txt. 

4. journaux de conteneur toodownload fils pour hello première application deux formes de base, utilisez hello de commande suivante :

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Cette commande crée un fichier journal nommé first2amlogs.txt. 

5. utilisation de tous les journaux du conteneur des fils toodownload hello la commande suivante :

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Cette commande crée un fichier journal nommé logs.txt. 

6. toodownload hello fils conteneur journal pour un conteneur spécifique, hello utilisez commande suivante :

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Cette commande crée un fichier journal nommé containerlogs.txt.

### <a name="additional-reading-2"></a>Documentation supplémentaire

- [Se connecter tooHDInsight (Hadoop) à l’aide de SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Concepts et applications Apache Hadoop Yarn, en anglais)







