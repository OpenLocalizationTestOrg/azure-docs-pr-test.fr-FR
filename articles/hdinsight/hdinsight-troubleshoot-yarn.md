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
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="03ae2-104">Résoudre les problèmes YARN à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="03ae2-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="03ae2-105">En savoir plus sur les questions hello et leurs résolutions lorsque vous travaillez avec des charges utiles Apache Hadoop fils dans Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="03ae2-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="03ae2-106">Comment créer une file d’attente YARN sur un cluster ?</span><span class="sxs-lookup"><span data-stu-id="03ae2-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="03ae2-107">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="03ae2-107">Resolution steps</span></span> 

<span data-ttu-id="03ae2-108">Utilisez hello ci-dessous les étapes dans Ambari toocreate une nouvelle file d’attente de fils, puis équilibrer allocation de capacité hello parmi toutes les files d’attente de hello.</span><span class="sxs-lookup"><span data-stu-id="03ae2-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="03ae2-109">Dans cet exemple, deux files d’attente existantes (**par défaut** et **thriftsvr**) les deux sont modifiés à partir de 50 % la capacité too25 % capacité, qui offre une capacité de 50 % hello nouvelle file d’attente (spark).</span><span class="sxs-lookup"><span data-stu-id="03ae2-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="03ae2-110">File d'attente</span><span class="sxs-lookup"><span data-stu-id="03ae2-110">Queue</span></span> | <span data-ttu-id="03ae2-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="03ae2-111">Capacity</span></span> | <span data-ttu-id="03ae2-112">Capacité maximale</span><span class="sxs-lookup"><span data-stu-id="03ae2-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="03ae2-113">default</span><span class="sxs-lookup"><span data-stu-id="03ae2-113">default</span></span> | <span data-ttu-id="03ae2-114">25%</span><span class="sxs-lookup"><span data-stu-id="03ae2-114">25%</span></span> | <span data-ttu-id="03ae2-115">50%</span><span class="sxs-lookup"><span data-stu-id="03ae2-115">50%</span></span> |
| <span data-ttu-id="03ae2-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="03ae2-116">thrftsvr</span></span> | <span data-ttu-id="03ae2-117">25%</span><span class="sxs-lookup"><span data-stu-id="03ae2-117">25%</span></span> | <span data-ttu-id="03ae2-118">50%</span><span class="sxs-lookup"><span data-stu-id="03ae2-118">50%</span></span> |
| <span data-ttu-id="03ae2-119">spark</span><span class="sxs-lookup"><span data-stu-id="03ae2-119">spark</span></span> | <span data-ttu-id="03ae2-120">50%</span><span class="sxs-lookup"><span data-stu-id="03ae2-120">50%</span></span> | <span data-ttu-id="03ae2-121">50%</span><span class="sxs-lookup"><span data-stu-id="03ae2-121">50%</span></span> |

1. <span data-ttu-id="03ae2-122">Sélectionnez hello **Ambari vues** icône et modèle de grille puis sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="03ae2-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="03ae2-123">Sélectionnez ensuite **YARN Queue Manager** (Gestionnaire de files d’attente YARN).</span><span class="sxs-lookup"><span data-stu-id="03ae2-123">Next, select **YARN Queue Manager**.</span></span>

    ![Sélectionnez l’icône du mode de Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="03ae2-125">Sélectionnez hello **par défaut** file d’attente.</span><span class="sxs-lookup"><span data-stu-id="03ae2-125">Select hello **default** queue.</span></span>

    ![Sélectionnez la file d’attente par défaut de hello](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="03ae2-127">Pourquoi **par défaut** file d’attente, modifiez hello **capacité** de 50 % too25 %.</span><span class="sxs-lookup"><span data-stu-id="03ae2-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="03ae2-128">Pourquoi **thriftsvr** file d’attente, modifiez hello **capacité** too25 %.</span><span class="sxs-lookup"><span data-stu-id="03ae2-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Modification hello capacité too25 % des files d’attente par défaut et thriftsvr hello](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="03ae2-130">toocreate une nouvelle file d’attente, sélectionnez **ajouter une file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="03ae2-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Sélectionner Add Queue](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="03ae2-132">Nom hello nouvelle file d’attente.</span><span class="sxs-lookup"><span data-stu-id="03ae2-132">Name hello new queue.</span></span>

    ![Nom de la file d’attente de hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="03ae2-134">Laissez hello **capacité** des valeurs à 50 %, puis sélectionnez hello **Actions** bouton.</span><span class="sxs-lookup"><span data-stu-id="03ae2-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Sélectionnez le bouton d’Actions hello](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="03ae2-136">Sélectionnez **Save and Refresh Queues** (Enregistrer et actualiser les files d’attente).</span><span class="sxs-lookup"><span data-stu-id="03ae2-136">Select **Save and Refresh Queues**.</span></span>

    ![Sélectionner Save and Refresh Queues](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="03ae2-138">Ces modifications sont visibles immédiatement sur hello interface utilisateur du Planificateur de fils.</span><span class="sxs-lookup"><span data-stu-id="03ae2-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="03ae2-139">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="03ae2-139">Additional reading</span></span>

- [<span data-ttu-id="03ae2-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="03ae2-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="03ae2-141">Comment télécharger les journaux YARN à partir d’un cluster ?</span><span class="sxs-lookup"><span data-stu-id="03ae2-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="03ae2-142">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="03ae2-142">Resolution steps</span></span> 

1. <span data-ttu-id="03ae2-143">Se connecter toohello HDInsight cluster à l’aide d’un client Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="03ae2-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="03ae2-144">Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="03ae2-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="03ae2-145">toolist tous hello ID d’application des applications fils hello qui sont en cours d’exécution, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03ae2-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="03ae2-146">ID de Hello sont répertoriés dans hello **APPLICATIONID** colonne.</span><span class="sxs-lookup"><span data-stu-id="03ae2-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="03ae2-147">Vous pouvez télécharger les journaux à partir de hello **APPLICATIONID** colonne.</span><span class="sxs-lookup"><span data-stu-id="03ae2-147">You can download logs from hello **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="03ae2-148">journaux de conteneur toodownload fils pour tous les maîtres d’application, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03ae2-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="03ae2-149">Cette commande crée un fichier journal nommé amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="03ae2-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="03ae2-150">journaux conteneur toodownload fils seul maître application de la dernière hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03ae2-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="03ae2-151">Cette commande crée un fichier journal nommé latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="03ae2-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="03ae2-152">journaux de conteneur toodownload fils pour hello première application deux formes de base, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03ae2-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="03ae2-153">Cette commande crée un fichier journal nommé first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="03ae2-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="03ae2-154">utilisation de tous les journaux du conteneur des fils toodownload hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03ae2-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="03ae2-155">Cette commande crée un fichier journal nommé logs.txt.</span><span class="sxs-lookup"><span data-stu-id="03ae2-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="03ae2-156">toodownload hello fils conteneur journal pour un conteneur spécifique, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03ae2-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="03ae2-157">Cette commande crée un fichier journal nommé containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="03ae2-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="03ae2-158"><a name="additional-reading-2"></a>Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="03ae2-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="03ae2-159">Se connecter tooHDInsight (Hadoop) à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="03ae2-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="03ae2-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Concepts et applications Apache Hadoop Yarn, en anglais)</span><span class="sxs-lookup"><span data-stu-id="03ae2-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







