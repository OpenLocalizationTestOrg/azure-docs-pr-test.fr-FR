---
title: "aaaTroubleshoot HBase à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses toocommon des questions sur l’utilisation de HBase et Azure HDInsight."
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
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="2f61e-103">Résolution de problèmes HBase à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f61e-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="2f61e-104">En savoir plus sur les questions hello et leurs résolutions lorsque vous travaillez avec des charges utiles Apache HBase dans Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="2f61e-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="2f61e-105">Comment exécuter des rapports de commande hbck avec plusieurs régions non attribuées</span><span class="sxs-lookup"><span data-stu-id="2f61e-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="2f61e-106">Un message d’erreur courants que vous pouvez voir lorsque vous exécutez hello `hbase hbck` commande est « plusieurs régions est non assignées ou trous dans la chaîne hello des régions. »</span><span class="sxs-lookup"><span data-stu-id="2f61e-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="2f61e-107">Bonjour HBase Master UI, vous pouvez voir le nombre hello des régions sont non équilibrées sur tous les serveurs de la région.</span><span class="sxs-lookup"><span data-stu-id="2f61e-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="2f61e-108">Vous pouvez ensuite exécuter `hbase hbck` commande toosee des trous dans la chaîne de région de hello.</span><span class="sxs-lookup"><span data-stu-id="2f61e-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="2f61e-109">Trous peuvent résulter des régions en mode hors connexion hello, affectations de hello dans ce correctif tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="2f61e-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="2f61e-110">toobring hello régions non attribués à l’état normal tooa arrière, terminer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f61e-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="2f61e-111">Se connecter toohello HDInsight HBase cluster à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="2f61e-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="2f61e-112">tooconnect shell de soigneur hello, exécutez hello `hbase zkcli` commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="2f61e-113">Exécutez hello `rmr /hbase/regions-in-transition` commande ou hello `rmr /hbase-unsecure/regions-in-transition` commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="2f61e-114">tooexit de hello `hbase zkcli` shell, utilisez hello `exit` commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="2f61e-115">Ouvrez hello Apache Ambari UI et redémarrez hello Active HBase Master service.</span><span class="sxs-lookup"><span data-stu-id="2f61e-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="2f61e-116">Exécutez hello `hbase hbck` commande (sans les options).</span><span class="sxs-lookup"><span data-stu-id="2f61e-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="2f61e-117">Vérifiez la sortie hello de cette tooensure de commande toutes les régions sont assignées.</span><span class="sxs-lookup"><span data-stu-id="2f61e-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="2f61e-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Comment corriger les problèmes de délai d’expiration lors de l’utilisation des commandes hbck pour l’affectation des régions ?</span><span class="sxs-lookup"><span data-stu-id="2f61e-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="2f61e-119">Problème</span><span class="sxs-lookup"><span data-stu-id="2f61e-119">Issue</span></span>

<span data-ttu-id="2f61e-120">Une cause potentielle de problèmes de délai d’attente lorsque vous utilisez hello `hbck` commande peut être que plusieurs régions sont Bonjour « en transition » l’état d’un certain temps.</span><span class="sxs-lookup"><span data-stu-id="2f61e-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="2f61e-121">Vous pouvez consulter ces régions hors connexion Bonjour HBase Master UI.</span><span class="sxs-lookup"><span data-stu-id="2f61e-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="2f61e-122">Un grand nombre de régions tentent tootransition, HBase Master peut le délai d’attente et être toobring Impossible de ces régions en ligne.</span><span class="sxs-lookup"><span data-stu-id="2f61e-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="2f61e-123">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-123">Resolution steps</span></span>

1. <span data-ttu-id="2f61e-124">Se connecter toohello HDInsight HBase cluster à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="2f61e-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="2f61e-125">tooconnect shell de soigneur hello, exécutez hello `hbase zkcli` commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="2f61e-126">Exécutez hello `rmr /hbase/regions-in-transition` ou hello `rmr /hbase-unsecure/regions-in-transition` commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="2f61e-127">tooexit hello `hbase zkcli` shell, utilisez hello `exit` commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="2f61e-128">Bonjour Ambari UI, redémarrer hello Active HBase Master.</span><span class="sxs-lookup"><span data-stu-id="2f61e-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="2f61e-129">Exécutez hello `hbase hbck -fixAssignments` réexécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="2f61e-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Comment forcer la désactivation du mode sans échec du stockage HDFS dans un cluster ?</span><span class="sxs-lookup"><span data-stu-id="2f61e-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="2f61e-131">Problème</span><span class="sxs-lookup"><span data-stu-id="2f61e-131">Issue</span></span>

<span data-ttu-id="2f61e-132">Hello local Hadoop Distributed fichier système (HDFS) est bloqué en mode sans échec sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="2f61e-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="2f61e-133">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="2f61e-133">Detailed description</span></span>

<span data-ttu-id="2f61e-134">Cette erreur peut résulter d’un échec lorsque vous exécutez hello HDFS commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2f61e-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="2f61e-135">erreur Hello que vous pouvez voir lorsque vous essayez de commande de hello toorun ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="2f61e-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
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

### <a name="probable-cause"></a><span data-ttu-id="2f61e-136">Cause probable</span><span class="sxs-lookup"><span data-stu-id="2f61e-136">Probable cause</span></span>

<span data-ttu-id="2f61e-137">Hello cluster HDInsight a été mis à l’échelle vers le bas tooa très peu de nœuds.</span><span class="sxs-lookup"><span data-stu-id="2f61e-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="2f61e-138">nombre de Hello de nœuds est inférieur ou fermez le facteur de réplication toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="2f61e-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="2f61e-139">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-139">Resolution steps</span></span> 

1. <span data-ttu-id="2f61e-140">Obtenez l’état hello Hello que HDFS sur hello HDInsight de cluster en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="2f61e-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

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
2. <span data-ttu-id="2f61e-141">Vous pouvez également vérifier l’intégrité de hello Hello que HDFS sur hello HDInsight cluster à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="2f61e-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
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

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="2f61e-142">Si vous déterminez qu’il n’y a aucun bloc manquant, endommagé ou under-répliquées, ou que ces blocs peuvent être ignorées, exécutez hello suivant commande tootake hello nom du nœud du mode sans échec :</span><span class="sxs-lookup"><span data-stu-id="2f61e-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="2f61e-143">Comment résoudre les problèmes de connectivité JDBC ou SQLLine avec Apache Phoenix ?</span><span class="sxs-lookup"><span data-stu-id="2f61e-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="2f61e-144">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-144">Resolution steps</span></span>

<span data-ttu-id="2f61e-145">tooconnect avec Phoenix, vous devez fournir l’adresse IP de hello d’un nœud soigneur actif.</span><span class="sxs-lookup"><span data-stu-id="2f61e-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="2f61e-146">Vérifiez que hello soigneur tente de service toowhich sqlline.py tooconnect est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2f61e-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="2f61e-147">Se connecter toohello cluster HDInsight à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="2f61e-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="2f61e-148">Entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2f61e-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="2f61e-149">Vous pouvez obtenir l’adresse IP de hello du nœud de soigneur actif hello de hello Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="2f61e-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="2f61e-150">Accédez trop**HBase** > **liens rapides** > **ZK\* (actif)** > **soigneur informations**.</span><span class="sxs-lookup"><span data-stu-id="2f61e-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="2f61e-151">Si hello sqlline.py se connecte tooPhoenix et n’expire pas, hello exécution commande suivante disponibilité de hello toovalidate et de l’intégrité de Phoenix :</span><span class="sxs-lookup"><span data-stu-id="2f61e-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="2f61e-152">Si la commande fonctionne, il n’existe aucun problème.</span><span class="sxs-lookup"><span data-stu-id="2f61e-152">If this command works, there is no issue.</span></span> <span data-ttu-id="2f61e-153">l’adresse IP Hello fournie par l’utilisateur de hello est peut-être incorrecte.</span><span class="sxs-lookup"><span data-stu-id="2f61e-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="2f61e-154">Toutefois, si la commande hello s’interrompt pendant une durée prolongée, puis affiche hello l’erreur suivante, continuer toostep 5.</span><span class="sxs-lookup"><span data-stu-id="2f61e-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="2f61e-155">Exécutez hello suivant les commandes à partir de condition de hello hello du nœud principal (hn0) toodiagnose Hello Phoenix système. Table du catalogue :</span><span class="sxs-lookup"><span data-stu-id="2f61e-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="2f61e-156">commande Hello doit retourner un suivant de toohello erreur similaire :</span><span class="sxs-lookup"><span data-stu-id="2f61e-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="2f61e-157">Bonjour Ambari UI, effectuez hello suivant du service de HMaster étapes toorestart hello sur tous les nœuds de soigneur :</span><span class="sxs-lookup"><span data-stu-id="2f61e-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="2f61e-158">Bonjour **Résumé** section accédez trop de HBase,**HBase** > **Active HBase Master**.</span><span class="sxs-lookup"><span data-stu-id="2f61e-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="2f61e-159">Bonjour **composants** section, redémarrez hello HBase Master service.</span><span class="sxs-lookup"><span data-stu-id="2f61e-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="2f61e-160">Répétez ces étapes pour les services **Standby HBase Master** (Master HBase de secours) restants.</span><span class="sxs-lookup"><span data-stu-id="2f61e-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="2f61e-161">Il peut prendre jusqu'à minutes toofive hello HBase Master service toostabilize et terminer le processus de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="2f61e-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="2f61e-162">Après quelques minutes, répétez hello sqlline.py commandes tooconfirm ce système hello. Table du catalogue est activé et qu’il peut être interrogé.</span><span class="sxs-lookup"><span data-stu-id="2f61e-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="2f61e-163">Lorsque hello système. Table du catalogue est différé toonormal, tooPhoenix de problème de connectivité hello doit être résolu automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2f61e-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="2f61e-164">Pourquoi un serveur maître toofail toostart</span><span class="sxs-lookup"><span data-stu-id="2f61e-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="2f61e-165">Error</span><span class="sxs-lookup"><span data-stu-id="2f61e-165">Error</span></span> 

<span data-ttu-id="2f61e-166">Le renommage atomique échoue.</span><span class="sxs-lookup"><span data-stu-id="2f61e-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="2f61e-167">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="2f61e-167">Detailed description</span></span>

<span data-ttu-id="2f61e-168">Au cours du processus de démarrage hello, HMaster termine le nombre d’étapes d’initialisation.</span><span class="sxs-lookup"><span data-stu-id="2f61e-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="2f61e-169">Ceux-ci incluent le déplacement des données à partir de rien de hello (.tmp) dossier de données toohello.</span><span class="sxs-lookup"><span data-stu-id="2f61e-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="2f61e-170">HMaster examine également toosee de dossier hello journaux WAL (WALs) s’il existe des serveurs de la région ne répond pas, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="2f61e-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="2f61e-171">Lors du démarrage, HMaster exécute une commande `list` de base sur ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="2f61e-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="2f61e-172">S’il rencontre un fichier inattendu dans l’un de ces dossiers, il envoie une exception et ne démarre pas.</span><span class="sxs-lookup"><span data-stu-id="2f61e-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="2f61e-173">Cause probable</span><span class="sxs-lookup"><span data-stu-id="2f61e-173">Probable cause</span></span>

<span data-ttu-id="2f61e-174">Dans les journaux du serveur de la région de hello, essayez de chronologie de hello tooidentify de création du fichier hello et alors voir s’il y a qu'un arrêt de processus autour hello heure hello fichier a été créé.</span><span class="sxs-lookup"><span data-stu-id="2f61e-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="2f61e-175">(Contactez HBase prise en charge tooassist vous dans cette opération.) Cela nous permet de vous fournir des mécanismes plus robustes afin de vous éviter ce bogue et de garantir un arrêt approprié des processus.</span><span class="sxs-lookup"><span data-stu-id="2f61e-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="2f61e-176">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-176">Resolution steps</span></span>

<span data-ttu-id="2f61e-177">Vérifiez la pile des appels hello et essayez de toodetermine le dossier qui pose problème de hello (par exemple, il peut être hello WALs dossier ou un dossier de .tmp hello).</span><span class="sxs-lookup"><span data-stu-id="2f61e-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="2f61e-178">Ensuite, dans l’Explorateur de Cloud ou à l’aide des commandes HDFS, essayez toolocate hello problème du fichier.</span><span class="sxs-lookup"><span data-stu-id="2f61e-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="2f61e-179">En règle générale, il s’agit d’un fichier \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="2f61e-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="2f61e-180">(hello \*-renamePending.json fichier est un fichier journal qui a utilisé les opération de changement de nom atomique hello tooimplement dans le pilote WASB hello.</span><span class="sxs-lookup"><span data-stu-id="2f61e-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="2f61e-181">Échéance toobugs dans cette implémentation, ces fichiers peuvent être restant après les défaillances de processus et ainsi de suite.) Forcez la suppression de ce fichier soit dans Cloud Explorer, soit à l’aide de commandes HDFS.</span><span class="sxs-lookup"><span data-stu-id="2f61e-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="2f61e-182">Dans certains cas, cet emplacement contient également un fichier temporaire nommé *$$$. $$$*.</span><span class="sxs-lookup"><span data-stu-id="2f61e-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="2f61e-183">Vous avez toouse HDFS `ls` de la commande toosee ce fichier ; vous ne pouvez pas voir fichier hello dans Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="2f61e-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="2f61e-184">toodelete ce fichier, la commande HDFS hello use `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="2f61e-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="2f61e-185">Après avoir exécuté ces commandes, HMaster devrait démarrer immédiatement.</span><span class="sxs-lookup"><span data-stu-id="2f61e-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="2f61e-186">Error</span><span class="sxs-lookup"><span data-stu-id="2f61e-186">Error</span></span>

<span data-ttu-id="2f61e-187">Aucune adresse de serveur n’est répertoriée dans la table *hbase: meta* au niveau de la région xxx.</span><span class="sxs-lookup"><span data-stu-id="2f61e-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="2f61e-188">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="2f61e-188">Detailed description</span></span>

<span data-ttu-id="2f61e-189">Vous pouvez voir un message sur votre cluster Linux qui indique que hello *hbase : métadonnées* table n’est pas en ligne.</span><span class="sxs-lookup"><span data-stu-id="2f61e-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="2f61e-190">L’exécution de la commande `hbck` peut renvoyer l’erreur suivante : « hbase: meta table replicaId 0 is not found on any region » (replicaId 0 introuvable dans toutes les régions de la table hbase: meta).</span><span class="sxs-lookup"><span data-stu-id="2f61e-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="2f61e-191">Hello problème est peut-être que HMaster pas pu initialiser une fois que vous avez redémarré HBase.</span><span class="sxs-lookup"><span data-stu-id="2f61e-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="2f61e-192">Dans les journaux HMaster hello, vous pouvez voir le message de type hello : « aucune adresse de serveur ne répertoriées dans hbase : les métadonnées pour la région hbase : sauvegarde \<nom de la région\>».</span><span class="sxs-lookup"><span data-stu-id="2f61e-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="2f61e-193">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-193">Resolution steps</span></span>

1. <span data-ttu-id="2f61e-194">Bonjour shell HBase, entrez hello suivant les commandes (modification de valeurs réelles, le cas échéant) :</span><span class="sxs-lookup"><span data-stu-id="2f61e-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="2f61e-195">Supprimer hello *hbase : espace de noms* entrée.</span><span class="sxs-lookup"><span data-stu-id="2f61e-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="2f61e-196">Cette entrée peut être hello même message d’erreur est signalée lorsque hello *hbase : espace de noms* table est analysée.</span><span class="sxs-lookup"><span data-stu-id="2f61e-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="2f61e-197">toobring des HBase en cours d’exécution, Bonjour Ambari UI, redémarrer hello HMaster Active.</span><span class="sxs-lookup"><span data-stu-id="2f61e-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="2f61e-198">Bonjour shell HBase, toobring toutes les tables en mode hors connexion, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2f61e-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="2f61e-199">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="2f61e-199">Additional reading</span></span>

[<span data-ttu-id="2f61e-200">Table HBase à hello tooprocess Impossible</span><span class="sxs-lookup"><span data-stu-id="2f61e-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="2f61e-201">Error</span><span class="sxs-lookup"><span data-stu-id="2f61e-201">Error</span></span>

<span data-ttu-id="2f61e-202">HMaster expire et un too"java.io.IOException similaires exception irrécupérable : 300000ms avec délai dépassé en attente de l’espace de noms table toobe est affecté. »</span><span class="sxs-lookup"><span data-stu-id="2f61e-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="2f61e-203">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="2f61e-203">Detailed description</span></span>

<span data-ttu-id="2f61e-204">Vous pourriez rencontrer ce problème si plusieurs tables et régions n’ont pas été vidées lors du redémarrage de vos services HMaster.</span><span class="sxs-lookup"><span data-stu-id="2f61e-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="2f61e-205">Redémarrage risque d’échouer, et vous verrez hello précédant le message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="2f61e-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="2f61e-206">Cause probable</span><span class="sxs-lookup"><span data-stu-id="2f61e-206">Probable cause</span></span>

<span data-ttu-id="2f61e-207">Il s’agit d’un problème connu avec hello HMaster service.</span><span class="sxs-lookup"><span data-stu-id="2f61e-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="2f61e-208">Les tâches générales de démarrage du cluster peuvent prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="2f61e-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="2f61e-209">HMaster s’arrête, car la table d’espace de noms hello n’est pas encore été affectée.</span><span class="sxs-lookup"><span data-stu-id="2f61e-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="2f61e-210">Cela se produit uniquement lorsqu’une grande quantité de données n’a pas été vidée, et qu’un délai d’expiration de cinq minutes est insuffisant.</span><span class="sxs-lookup"><span data-stu-id="2f61e-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="2f61e-211">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-211">Resolution steps</span></span>

1. <span data-ttu-id="2f61e-212">Bonjour Ambari UI, accédez trop**HBase** > **configurations**.</span><span class="sxs-lookup"><span data-stu-id="2f61e-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="2f61e-213">Dans fichier de personnalisée hbase-site.XML de hello, ajoutez hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="2f61e-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="2f61e-214">Redémarrez les services hello requis (HMaster et éventuellement d’autres services HBase).</span><span class="sxs-lookup"><span data-stu-id="2f61e-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="2f61e-215">Pourquoi le redémarrage échoue-t-il sur un serveur régional ?</span><span class="sxs-lookup"><span data-stu-id="2f61e-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="2f61e-216">Problème</span><span class="sxs-lookup"><span data-stu-id="2f61e-216">Issue</span></span>

<span data-ttu-id="2f61e-217">L’échec du redémarrage d’un serveur régional peut être évité en respectant ces meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="2f61e-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="2f61e-218">Nous vous recommandons d’interrompre les activités de lourdes charges de travail lorsque vous planifiez des serveurs de la région toorestart HBase.</span><span class="sxs-lookup"><span data-stu-id="2f61e-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="2f61e-219">Si une application poursuit tooconnect avec les serveurs de la région lors de l’arrêt est en cours, opération de redémarrage du serveur hello région sera plus lente en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2f61e-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="2f61e-220">Il est également un toofirst conseillé vidage que tous hello tables.</span><span class="sxs-lookup"><span data-stu-id="2f61e-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="2f61e-221">Pour obtenir une référence sur la façon de tooflush tables, consultez [HDInsight HBase : comment cluster HBase de hello tooimprove redémarrage en vidant tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="2f61e-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="2f61e-222">Si vous lancez le redémarrage hello sur HBase serveurs de la région de hello Ambari UI, vous voyez immédiatement que les serveurs de la région hello s’est arrêté, mais ils ne pas redémarrer immédiatement.</span><span class="sxs-lookup"><span data-stu-id="2f61e-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="2f61e-223">Voici ce qui se passe en coulisses hello :</span><span class="sxs-lookup"><span data-stu-id="2f61e-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="2f61e-224">agent de Ambari Hello envoie un arrêt demande toohello région serveur.</span><span class="sxs-lookup"><span data-stu-id="2f61e-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="2f61e-225">agent de Ambari Hello attend 30 secondes pour hello région server tooshut vers le bas en douceur.</span><span class="sxs-lookup"><span data-stu-id="2f61e-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="2f61e-226">Si votre application continue tooconnect avec le serveur de la région de hello, serveur de hello ne sera pas arrêté immédiatement.</span><span class="sxs-lookup"><span data-stu-id="2f61e-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="2f61e-227">délai d’attente de 30 secondes Hello arrive à expiration avant l’arrêt se produit.</span><span class="sxs-lookup"><span data-stu-id="2f61e-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="2f61e-228">Après 30 secondes, l’agent de Ambari hello envoie un kill-force (`kill -9`) serveur de région toohello de commande.</span><span class="sxs-lookup"><span data-stu-id="2f61e-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="2f61e-229">Vous pouvez le voir dans le journal d’ambari-agent hello (dans hello répertoire/var/log/du nœud de travail respectifs hello) :</span><span class="sxs-lookup"><span data-stu-id="2f61e-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

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
<span data-ttu-id="2f61e-230">En raison de l’arrêt brutal de hello, port hello associé hello processus ne peut pas libéré, même si le processus de serveur de la région de hello est arrêté.</span><span class="sxs-lookup"><span data-stu-id="2f61e-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="2f61e-231">Cette situation peut entraîner tooan AddressBindException au démarrage de server de région de hello, comme indiqué dans hello suivant des journaux.</span><span class="sxs-lookup"><span data-stu-id="2f61e-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="2f61e-232">Vous pouvez le vérifier dans la région de hello-server.log dans le répertoire de /var/log/hbase hello sur les nœuds de travail hello où le serveur de la région de hello échoue toostart.</span><span class="sxs-lookup"><span data-stu-id="2f61e-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

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
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
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

### <a name="resolution-steps"></a><span data-ttu-id="2f61e-233">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="2f61e-233">Resolution steps</span></span>

1. <span data-ttu-id="2f61e-234">Essayez de charge de hello tooreduce sur les serveurs de la région hello HBase avant de lancer un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="2f61e-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="2f61e-235">Vous pouvez également try toomanually redémarrage région serveurs à l’aide de nœuds de travail hello hello suivant (si l’étape 1 ne permet pas), commandes :</span><span class="sxs-lookup"><span data-stu-id="2f61e-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

