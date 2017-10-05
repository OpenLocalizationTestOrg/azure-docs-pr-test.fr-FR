---
title: "Résolution de problèmes HBase à l’aide d’Azure HDInsight | Microsoft Docs"
description: "Obtenez les réponses aux questions courantes sur l’utilisation de HBase et d’Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 15412c3853a2b8436c5e96034c9a92a2a1094662
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="ce460-103">Résolution de problèmes HBase à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce460-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="ce460-104">Découvrez les principaux problèmes rencontrés lors de l’utilisation de charges utiles Apache HBase dans Apache Ambari, et leur résolution.</span><span class="sxs-lookup"><span data-stu-id="ce460-104">Learn about the top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="ce460-105">Comment exécuter des rapports de commande hbck avec plusieurs régions non attribuées</span><span class="sxs-lookup"><span data-stu-id="ce460-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="ce460-106">Un message d’erreur courant indiquant que plusieurs régions ne sont pas attribuées ou qu’il y a des trous dans la chaîne de régions peut s’afficher lorsque vous exécutez la commande `hbase hbck`.</span><span class="sxs-lookup"><span data-stu-id="ce460-106">A common error message that you might see when you run the `hbase hbck` command is "multiple regions being unassigned or holes in the chain of regions."</span></span>

<span data-ttu-id="ce460-107">Dans l’interface utilisateur HBase Master, vous pouvez voir le nombre de régions en état de déséquilibre sur tous les serveurs régionaux.</span><span class="sxs-lookup"><span data-stu-id="ce460-107">In the HBase Master UI, you can see the number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="ce460-108">Vous pouvez ensuite exécuter la commande `hbase hbck` pour afficher les trous dans la chaîne de régions.</span><span class="sxs-lookup"><span data-stu-id="ce460-108">Then, you can run `hbase hbck` command to see holes in the region chain.</span></span>

<span data-ttu-id="ce460-109">Les trous peuvent être dus à des régions hors connexion, donc commencez par corriger les attributions.</span><span class="sxs-lookup"><span data-stu-id="ce460-109">Holes might be caused by the offline regions, so fix the assignments first.</span></span> 

<span data-ttu-id="ce460-110">Pour rétablir les régions non attribuées à leur état normal, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ce460-110">To bring the unassigned regions back to a normal state, complete the following steps:</span></span>

1. <span data-ttu-id="ce460-111">Connectez-vous au cluster HDInsight HBase à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="ce460-111">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="ce460-112">Pour vous connecter avec l’interpréteur de commandes ZooKeeper, exécutez la commande `hbase zkcli`.</span><span class="sxs-lookup"><span data-stu-id="ce460-112">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="ce460-113">Exécutez la commande `rmr /hbase/regions-in-transition` ou la commande `rmr /hbase-unsecure/regions-in-transition`.</span><span class="sxs-lookup"><span data-stu-id="ce460-113">Run the `rmr /hbase/regions-in-transition` command or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="ce460-114">Pour quitter l’interpréteur de commandes `hbase zkcli`, utilisez la commande `exit`.</span><span class="sxs-lookup"><span data-stu-id="ce460-114">To exit from the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="ce460-115">Ouvrez l’interface utilisateur d’Apache Ambari et redémarrez le service HBase Master actif.</span><span class="sxs-lookup"><span data-stu-id="ce460-115">Open the Apache Ambari UI, and then restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="ce460-116">Exécutez de nouveau la commande `hbase hbck` (sans aucune option).</span><span class="sxs-lookup"><span data-stu-id="ce460-116">Run the `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="ce460-117">Vérifiez la sortie de cette commande et assurez-vous que toutes les régions sont assignées.</span><span class="sxs-lookup"><span data-stu-id="ce460-117">Check the output of this command to ensure that all regions are being assigned.</span></span>


## <span data-ttu-id="ce460-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Comment corriger les problèmes de délai d’expiration lors de l’utilisation des commandes hbck pour l’affectation des régions ?</span><span class="sxs-lookup"><span data-stu-id="ce460-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="ce460-119">Problème</span><span class="sxs-lookup"><span data-stu-id="ce460-119">Issue</span></span>

<span data-ttu-id="ce460-120">Les problèmes de délai d’expiration rencontrés lors de l’utilisation de la commande `hbck` peuvent être dus à la présence de plusieurs régions en état de transition pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="ce460-120">A potential cause for timeout issues when you use the `hbck` command might be that several regions are in the "in transition" state for a long time.</span></span> <span data-ttu-id="ce460-121">Ces régions apparaissent comme étant hors connexion dans l’interface utilisateur HBase Master.</span><span class="sxs-lookup"><span data-stu-id="ce460-121">You can see those regions as offline in the HBase Master UI.</span></span> <span data-ttu-id="ce460-122">En raison du grand nombre de régions en tentative de transition, HBase Master pourrait connaître un problème de délai d’expiration et ne pas parvenir remettre ces régions en ligne.</span><span class="sxs-lookup"><span data-stu-id="ce460-122">Because a high number of regions are attempting to transition, HBase Master might timeout and be unable to bring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ce460-123">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-123">Resolution steps</span></span>

1. <span data-ttu-id="ce460-124">Connectez-vous au cluster HDInsight HBase à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="ce460-124">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="ce460-125">Pour vous connecter avec l’interpréteur de commandes ZooKeeper, exécutez la commande `hbase zkcli`.</span><span class="sxs-lookup"><span data-stu-id="ce460-125">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="ce460-126">Exécutez la commande `rmr /hbase/regions-in-transition` ou `rmr /hbase-unsecure/regions-in-transition`.</span><span class="sxs-lookup"><span data-stu-id="ce460-126">Run the `rmr /hbase/regions-in-transition` or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="ce460-127">Pour quitter l’interpréteur de commandes `hbase zkcli`, utilisez la commande `exit`.</span><span class="sxs-lookup"><span data-stu-id="ce460-127">To exit the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="ce460-128">Ouvrez l’interface utilisateur d’Ambari et redémarrez le service HBase Master actif.</span><span class="sxs-lookup"><span data-stu-id="ce460-128">In the Ambari UI, restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="ce460-129">Exécutez de nouveau la commande `hbase hbck -fixAssignments`.</span><span class="sxs-lookup"><span data-stu-id="ce460-129">Run the `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="ce460-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Comment forcer la désactivation du mode sans échec du stockage HDFS dans un cluster ?</span><span class="sxs-lookup"><span data-stu-id="ce460-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="ce460-131">Problème</span><span class="sxs-lookup"><span data-stu-id="ce460-131">Issue</span></span>

<span data-ttu-id="ce460-132">Le stockage HDFS (Hadoop Distributed File System) est bloqué en mode sans échec sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ce460-132">The local Hadoop Distributed File System (HDFS) is stuck in safe mode on the HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="ce460-133">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="ce460-133">Detailed description</span></span>

<span data-ttu-id="ce460-134">Cette erreur peut résulter d’un échec de l’exécution de la commande HDFS suivante :</span><span class="sxs-lookup"><span data-stu-id="ce460-134">This error might be caused by a failure when you run the following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="ce460-135">L’erreur qui peut s’afficher lorsque vous tentez d’exécuter la commande ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ce460-135">The error you might see when you try to run the command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="ce460-136">Cause probable</span><span class="sxs-lookup"><span data-stu-id="ce460-136">Probable cause</span></span>

<span data-ttu-id="ce460-137">Le cluster HDInsight a été redimensionné et ne compte plus que quelques nœuds.</span><span class="sxs-lookup"><span data-stu-id="ce460-137">The HDInsight cluster has been scaled down to a very few nodes.</span></span> <span data-ttu-id="ce460-138">Le nombre de nœuds est inférieur au facteur de réplication HDFS ou proche de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="ce460-138">The number of nodes is below or close to the HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ce460-139">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-139">Resolution steps</span></span> 

1. <span data-ttu-id="ce460-140">Déterminez l’état du stockage HDFS du cluster HDInsight à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce460-140">Get the status of the HDFS on the HDInsight cluster by running the following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="ce460-141">Vous pouvez également vérifier l’intégrité du stockage HDFS du cluster HDInsight à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce460-141">You also can check the integrity of the HDFS on the HDInsight cluster by using the following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting to namenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   The filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="ce460-142">Si aucun bloc n’est manquant, endommagé ou sous-répliqué ou si ces blocs peuvent être ignorés, exécutez la commande suivante pour désactiver le mode sans échec sur le nœud de nom :</span><span class="sxs-lookup"><span data-stu-id="ce460-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run the following command to take the name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="ce460-143">Comment résoudre les problèmes de connectivité JDBC ou SQLLine avec Apache Phoenix ?</span><span class="sxs-lookup"><span data-stu-id="ce460-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ce460-144">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-144">Resolution steps</span></span>

<span data-ttu-id="ce460-145">Pour vous connecter avec Phoenix, vous devez fournir l’adresse IP d’un nœud Zookeeper actif.</span><span class="sxs-lookup"><span data-stu-id="ce460-145">To connect with Phoenix, you must provide the IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="ce460-146">Assurez-vous que le service Zookeeper auquel l’utilitaire sqlline.py essaie de se connecter est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ce460-146">Ensure that the ZooKeeper service to which sqlline.py is trying to connect is up and running.</span></span>
1. <span data-ttu-id="ce460-147">Connectez-vous au cluster HDInsight à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="ce460-147">Sign in to the HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="ce460-148">Entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ce460-148">Enter the following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="ce460-149">Vous pouvez obtenir l’adresse IP du nœud ZooKeeper actif à partir de l’interface utilisateur d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="ce460-149">You can get the IP address of the active ZooKeeper node from the Ambari UI.</span></span> <span data-ttu-id="ce460-150">Accédez à **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info** (HBase > Liens rapides > ZK (acitf) > Infos ZooKeeper).</span><span class="sxs-lookup"><span data-stu-id="ce460-150">Go to **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="ce460-151">Si l’utilitaire sqlline.py se connecte à Phoenix et n’expire pas, exécutez la commande suivante pour valider la disponibilité et l’intégrité de Phoenix :</span><span class="sxs-lookup"><span data-stu-id="ce460-151">If the sqlline.py connects to Phoenix and does not timeout, run the following command to validate the availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="ce460-152">Si la commande fonctionne, il n’existe aucun problème.</span><span class="sxs-lookup"><span data-stu-id="ce460-152">If this command works, there is no issue.</span></span> <span data-ttu-id="ce460-153">L’adresse IP fournie par l’utilisateur peut être incorrecte.</span><span class="sxs-lookup"><span data-stu-id="ce460-153">The IP address provided by the user might be incorrect.</span></span> <span data-ttu-id="ce460-154">Toutefois, si la commande s’interrompt pendant une durée prolongée, puis affiche l’erreur suivante, passez à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="ce460-154">However, if the command pauses for an extended time and then displays the following error, continue to step 5.</span></span>

   ```apache
           Error while connecting to sqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting to jdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="ce460-155">Exécutez les commandes suivantes à partir du nœud principal (hn0) pour diagnostiquer l’état de la table Phoenix SYSTEM.CATALOG :</span><span class="sxs-lookup"><span data-stu-id="ce460-155">Run the following commands from the head node (hn0) to diagnose the condition of the Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="ce460-156">La commande doit renvoyer une erreur similaire à la suivante :</span><span class="sxs-lookup"><span data-stu-id="ce460-156">The command should return an error similar to the following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="ce460-157">À partir de l’interface utilisateur Ambari, suivez les étapes ci-dessous pour redémarrer le service HMaster sur tous les nœuds ZooKeeper :</span><span class="sxs-lookup"><span data-stu-id="ce460-157">In the Ambari UI, complete the following steps to restart the HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="ce460-158">Dans la section **Summary** (Résumé) de HBase, accédez à **HBase** > **Active HBase Master** (HBase > HBase Master actif).</span><span class="sxs-lookup"><span data-stu-id="ce460-158">In the **Summary** section of HBase, go to **HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="ce460-159">Dans la section **Components** (Composants), redémarrez le service HBase Master.</span><span class="sxs-lookup"><span data-stu-id="ce460-159">In the **Components** section, restart the HBase Master service.</span></span>
    3. <span data-ttu-id="ce460-160">Répétez ces étapes pour les services **Standby HBase Master** (Master HBase de secours) restants.</span><span class="sxs-lookup"><span data-stu-id="ce460-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="ce460-161">La stabilisation et la récupération complète du service HBase Master peuvent prendre jusqu’à cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="ce460-161">It can take up to five minutes for the HBase Master service to stabilize and finish the recovery process.</span></span> <span data-ttu-id="ce460-162">Après quelques minutes, répétez les commandes sqlline.py pour confirmer que la table SYSTEM.CATALOG est activée et qu’elle peut être interrogée.</span><span class="sxs-lookup"><span data-stu-id="ce460-162">After a few minutes, repeat the sqlline.py commands to confirm that the SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="ce460-163">Une fois la table SYSTEM.CATALOG revenue à son fonctionnement normal, le problème de connectivité à Phoenix devrait se résoudre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ce460-163">When the SYSTEM.CATALOG table is back to normal, the connectivity issue to Phoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-to-fail-to-start"></a><span data-ttu-id="ce460-164">Pourquoi le démarrage d’un serveur maître échoue-t-il ?</span><span class="sxs-lookup"><span data-stu-id="ce460-164">What causes a master server to fail to start</span></span>

### <a name="error"></a><span data-ttu-id="ce460-165">Error</span><span class="sxs-lookup"><span data-stu-id="ce460-165">Error</span></span> 

<span data-ttu-id="ce460-166">Le renommage atomique échoue.</span><span class="sxs-lookup"><span data-stu-id="ce460-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="ce460-167">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="ce460-167">Detailed description</span></span>

<span data-ttu-id="ce460-168">Pendant le processus de démarrage, HMaster exécute de nombreuses étapes d’initialisation.</span><span class="sxs-lookup"><span data-stu-id="ce460-168">During the startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="ce460-169">Cela inclut le déplacement des données à partir du dossier de travail (.tmp) vers le dossier de données.</span><span class="sxs-lookup"><span data-stu-id="ce460-169">These include moving data from the scratch (.tmp) folder to the data folder.</span></span> <span data-ttu-id="ce460-170">HMaster examine également le dossier de journaux WAL (write-ahead log) pour voir s’il existe des serveurs régionaux ne répondant pas, etc.</span><span class="sxs-lookup"><span data-stu-id="ce460-170">HMaster also looks at the write-ahead logs (WALs) folder to see if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="ce460-171">Lors du démarrage, HMaster exécute une commande `list` de base sur ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="ce460-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="ce460-172">S’il rencontre un fichier inattendu dans l’un de ces dossiers, il envoie une exception et ne démarre pas.</span><span class="sxs-lookup"><span data-stu-id="ce460-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="ce460-173">Cause probable</span><span class="sxs-lookup"><span data-stu-id="ce460-173">Probable cause</span></span>

<span data-ttu-id="ce460-174">Dans les journaux des serveurs régionaux, essayez d’identifier la chronologie de création des fichiers et de déterminer si un blocage de processus s’est produit autour de l’heure de création du fichier.</span><span class="sxs-lookup"><span data-stu-id="ce460-174">In the region server logs, try to identify the timeline of the file creation, and then see if there was a process crash around the time the file was created.</span></span> <span data-ttu-id="ce460-175">(Contactez le support HBase si vous avez besoin d’aide.) Cela nous permet de vous fournir des mécanismes plus robustes afin de vous éviter ce bogue et de garantir un arrêt approprié des processus.</span><span class="sxs-lookup"><span data-stu-id="ce460-175">(Contact HBase support to assist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ce460-176">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-176">Resolution steps</span></span>

<span data-ttu-id="ce460-177">Vérifiez la pile des appels et essayez de déterminer quel dossier pourrait être responsable du problème (par exemple le dossier de journaux WAL ou le dossier .tmp).</span><span class="sxs-lookup"><span data-stu-id="ce460-177">Check the call stack and try to determine which folder might be causing the problem (for instance, it might be the WALs folder or the .tmp folder).</span></span> <span data-ttu-id="ce460-178">Ensuite, dans Cloud Explorer ou à l’aide de commandes HDFS, tentez de localiser le fichier posant problème.</span><span class="sxs-lookup"><span data-stu-id="ce460-178">Then, in Cloud Explorer or by using HDFS commands, try to locate the problem file.</span></span> <span data-ttu-id="ce460-179">En règle générale, il s’agit d’un fichier \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="ce460-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="ce460-180">(Le fichier \*-renamePending.json est un fichier journal utilisé pour implémenter l’opération de renommage atomique au niveau du pilote WASB.</span><span class="sxs-lookup"><span data-stu-id="ce460-180">(The \*-renamePending.json file is a journal file that's used to implement the atomic rename operation in the WASB driver.</span></span> <span data-ttu-id="ce460-181">En raison des bogues de cette implémentation, ces fichiers peuvent rester après le blocage du processus, etc.) Forcez la suppression de ce fichier soit dans Cloud Explorer, soit à l’aide de commandes HDFS.</span><span class="sxs-lookup"><span data-stu-id="ce460-181">Due to bugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="ce460-182">Dans certains cas, cet emplacement contient également un fichier temporaire nommé *$$$. $$$*.</span><span class="sxs-lookup"><span data-stu-id="ce460-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="ce460-183">Vous devez utiliser la commande HDFS `ls` pour voir ce fichier ; vous ne pouvez pas le voir dans Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="ce460-183">You have to use HDFS `ls` command to see this file; you cannot see the file in Cloud Explorer.</span></span> <span data-ttu-id="ce460-184">Pour supprimer ce fichier, utilisez la commande HDFS `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="ce460-184">To delete this file, use the HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="ce460-185">Après avoir exécuté ces commandes, HMaster devrait démarrer immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ce460-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="ce460-186">Error</span><span class="sxs-lookup"><span data-stu-id="ce460-186">Error</span></span>

<span data-ttu-id="ce460-187">Aucune adresse de serveur n’est répertoriée dans la table *hbase: meta* au niveau de la région xxx.</span><span class="sxs-lookup"><span data-stu-id="ce460-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="ce460-188">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="ce460-188">Detailed description</span></span>

<span data-ttu-id="ce460-189">Un message indiquant que la table *hbase: meta* n’est pas en ligne peut s’afficher sur votre cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="ce460-189">You might see a message on your Linux cluster that indicates that the *hbase: meta* table is not online.</span></span> <span data-ttu-id="ce460-190">L’exécution de la commande `hbck` peut renvoyer l’erreur suivante : « hbase: meta table replicaId 0 is not found on any region » (replicaId 0 introuvable dans toutes les régions de la table hbase: meta).</span><span class="sxs-lookup"><span data-stu-id="ce460-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="ce460-191">Le problème peut provenir de l’échec de l’initialisation de HMaster après le redémarrage de HBase.</span><span class="sxs-lookup"><span data-stu-id="ce460-191">The problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="ce460-192">Dans les journaux HMaster, le message « No server address listed in hbase: meta for region hbase: backup \<region name\> » (Aucune adresse de serveur n’est répertoriée dans la table hbase: meta au niveau de la région hbase: backup xxx) s’affiche parfois.</span><span class="sxs-lookup"><span data-stu-id="ce460-192">In the HMaster logs, you might see the message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="ce460-193">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-193">Resolution steps</span></span>

1. <span data-ttu-id="ce460-194">Entrez la commande suivante dans l’interpréteur de commandes HBase (modifiez les valeurs le cas échéant) :</span><span class="sxs-lookup"><span data-stu-id="ce460-194">In the HBase shell, enter the following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="ce460-195">Supprimez l’entrée *hbase: namespace*.</span><span class="sxs-lookup"><span data-stu-id="ce460-195">Delete the *hbase: namespace* entry.</span></span> <span data-ttu-id="ce460-196">Cette entrée peut être à l’origine de l’erreur signalée lorsque la table *hbase: namespace* est analysée.</span><span class="sxs-lookup"><span data-stu-id="ce460-196">This entry might be the same error that's being reported when the *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="ce460-197">Pour rétablir le fonctionnement de HBase, redémarrez le service HMaster actif à partir de l’interface utilisateur Ambari.</span><span class="sxs-lookup"><span data-stu-id="ce460-197">To bring up HBase in a running state, in the Ambari UI, restart the Active HMaster service.</span></span>  

4. <span data-ttu-id="ce460-198">Dans l’interpréteur de commandes HBase, exécutez la commande suivante pour afficher toutes les tables hors connexion :</span><span class="sxs-lookup"><span data-stu-id="ce460-198">In the HBase shell, to bring up all offline tables, run the following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="ce460-199">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="ce460-199">Additional reading</span></span>

<span data-ttu-id="ce460-200">[Unable to process the HBase table](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table) (Traitement de la table HBase impossible, en anglais)</span><span class="sxs-lookup"><span data-stu-id="ce460-200">[Unable to process the HBase table](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)</span></span>


### <a name="error"></a><span data-ttu-id="ce460-201">Error</span><span class="sxs-lookup"><span data-stu-id="ce460-201">Error</span></span>

<span data-ttu-id="ce460-202">HMaster arrive à expiration avec une exception irrécupérable du type « java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned » (Expiration du délai de 300000ms en attente de l’affectation de la table namespace).</span><span class="sxs-lookup"><span data-stu-id="ce460-202">HMaster times out with a fatal exception similar to "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="ce460-203">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="ce460-203">Detailed description</span></span>

<span data-ttu-id="ce460-204">Vous pourriez rencontrer ce problème si plusieurs tables et régions n’ont pas été vidées lors du redémarrage de vos services HMaster.</span><span class="sxs-lookup"><span data-stu-id="ce460-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="ce460-205">Le redémarrage risque d’échouer, et vous le message d’erreur précédent s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ce460-205">Restart might fail, and you'll see the preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="ce460-206">Cause probable</span><span class="sxs-lookup"><span data-stu-id="ce460-206">Probable cause</span></span>

<span data-ttu-id="ce460-207">Il s’agit d’un problème connu avec le service HMaster.</span><span class="sxs-lookup"><span data-stu-id="ce460-207">This is a known issue with the HMaster service.</span></span> <span data-ttu-id="ce460-208">Les tâches générales de démarrage du cluster peuvent prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="ce460-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="ce460-209">HMaster s’arrête, car la table namespace n’a pas encore été affectée.</span><span class="sxs-lookup"><span data-stu-id="ce460-209">HMaster shuts down because the namespace table isn’t yet assigned.</span></span> <span data-ttu-id="ce460-210">Cela se produit uniquement lorsqu’une grande quantité de données n’a pas été vidée, et qu’un délai d’expiration de cinq minutes est insuffisant.</span><span class="sxs-lookup"><span data-stu-id="ce460-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="ce460-211">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-211">Resolution steps</span></span>

1. <span data-ttu-id="ce460-212">Dans l’interface utilisateur d’Ambari, accédez à **HBase** > **Configs**.</span><span class="sxs-lookup"><span data-stu-id="ce460-212">In the Ambari UI, go to **HBase** > **Configs**.</span></span> <span data-ttu-id="ce460-213">Dans le fichier personnalisé hbase-site.XML, ajoutez le paramètre suivant :</span><span class="sxs-lookup"><span data-stu-id="ce460-213">In the custom hbase-site.xml file, add the following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="ce460-214">Redémarrez les services requis (HMaster et éventuellement d’autres services HBase).</span><span class="sxs-lookup"><span data-stu-id="ce460-214">Restart the required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="ce460-215">Pourquoi le redémarrage échoue-t-il sur un serveur régional ?</span><span class="sxs-lookup"><span data-stu-id="ce460-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="ce460-216">Problème</span><span class="sxs-lookup"><span data-stu-id="ce460-216">Issue</span></span>

<span data-ttu-id="ce460-217">L’échec du redémarrage d’un serveur régional peut être évité en respectant ces meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="ce460-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="ce460-218">Il est recommandé d’interrompre les activités impliquant de lourdes charges de travail lorsque vous prévoyez de redémarrer les serveurs régionaux HBase.</span><span class="sxs-lookup"><span data-stu-id="ce460-218">We recommend that you pause heavy workload activity when you are planning to restart HBase region servers.</span></span> <span data-ttu-id="ce460-219">Si une application continue de se connecter aux serveurs régionaux pendant l’arrêt, cela ralentit le redémarrage de ces derniers de plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="ce460-219">If an application continues to connect with region servers when shutdown is in progress, the region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="ce460-220">En outre, il est judicieux de commencer par vider toutes les tables.</span><span class="sxs-lookup"><span data-stu-id="ce460-220">Also, it's a good idea to first flush all the tables.</span></span> <span data-ttu-id="ce460-221">Pour en savoir plus sur le vidage des tables, consultez ce billet de blog (en anglais) : [HDInsight HBase: How to Improve HBase cluster restart time by Flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/) (HDInsight HBase : comment améliorer le temps de redémarrage des clusters HBase en vidant les tables).</span><span class="sxs-lookup"><span data-stu-id="ce460-221">For a reference on how to flush tables, see [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="ce460-222">Si vous lancez l’opération de redémarrage sur des serveurs régionaux HBase à partir de l’interface utilisateur d’Ambari, vous voyez immédiatement que les serveurs régionaux s’arrêtent, mais qu’ils ne redémarrent pas immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ce460-222">If you initiate the restart operation on HBase region servers from the Ambari UI, you immediately see that the region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="ce460-223">Voici ce qui se passe en arrière-plan :</span><span class="sxs-lookup"><span data-stu-id="ce460-223">Here's what's happening behind the scenes:</span></span> 

1. <span data-ttu-id="ce460-224">Ambari Agent envoie une demande d’arrêt au serveur régional.</span><span class="sxs-lookup"><span data-stu-id="ce460-224">The Ambari agent sends a stop request to the region server.</span></span>
2. <span data-ttu-id="ce460-225">L’agent attend 30 secondes que le serveur s’arrête de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="ce460-225">The Ambari agent waits for 30 seconds for the region server to shut down gracefully.</span></span> 
3. <span data-ttu-id="ce460-226">Si votre application continue à se connecter au serveur régional, ce dernier ne sera pas arrêté immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ce460-226">If your application continues to connect with the region server, the server won't shut down immediately.</span></span> <span data-ttu-id="ce460-227">Le délai de 30 secondes expire avant l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="ce460-227">The 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="ce460-228">Après 30 secondes, Ambari Agent force l’arrêt du serveur régional en lui envoyant une commande force-kill (`kill -9`).</span><span class="sxs-lookup"><span data-stu-id="ce460-228">After 30 seconds, the Ambari agent sends a force-kill (`kill -9`) command to the region server.</span></span> <span data-ttu-id="ce460-229">Vous pouvez voir cet événement dans le journal ambari-agent (dans le répertoire /var/log/ du nœud de travail correspondant) :</span><span class="sxs-lookup"><span data-stu-id="ce460-229">You can see this in the ambari-agent log (in the /var/log/ directory of the respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="ce460-230">En raison de cet arrêt brutal, le port associé au processus ne peut pas être libéré même si le processus du serveur régional est arrêté.</span><span class="sxs-lookup"><span data-stu-id="ce460-230">Because of the abrupt shutdown, the port associated with the process might not be released, even though the region server process is stopped.</span></span> <span data-ttu-id="ce460-231">Cela peut entraîner l’exception AddressBindException au démarrage du serveur régional, comme indiqué dans les journaux suivants.</span><span class="sxs-lookup"><span data-stu-id="ce460-231">This situation can lead to an AddressBindException when the region server is starting, as shown in the following logs.</span></span> <span data-ttu-id="ce460-232">Cet élément apparaît dans le journal region-server.log du répertoire /var/log/hbase des nœuds de travail où le démarrage des serveurs régionaux échoue.</span><span class="sxs-lookup"><span data-stu-id="ce460-232">You can verify this in the region-server.log in the /var/log/hbase directory on the worker nodes where the region server fails to start.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding to /10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="ce460-233">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="ce460-233">Resolution steps</span></span>

1. <span data-ttu-id="ce460-234">Essayez de réduire la charge sur les serveurs régionaux HBase avant de lancer un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="ce460-234">Try to reduce the load on the HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="ce460-235">Si l’étape 1 n’a aucun effet, vous pouvez également essayer de redémarrer manuellement les serveurs régionaux sur les nœuds de travail à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce460-235">Alternatively (if step 1 doesn't help), try to manually restart region servers on the worker nodes by using the following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

