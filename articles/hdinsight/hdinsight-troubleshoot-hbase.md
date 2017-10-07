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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Résolution de problèmes HBase à l’aide d’Azure HDInsight

En savoir plus sur les questions hello et leurs résolutions lorsque vous travaillez avec des charges utiles Apache HBase dans Apache Ambari.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Comment exécuter des rapports de commande hbck avec plusieurs régions non attribuées

Un message d’erreur courants que vous pouvez voir lorsque vous exécutez hello `hbase hbck` commande est « plusieurs régions est non assignées ou trous dans la chaîne hello des régions. »

Bonjour HBase Master UI, vous pouvez voir le nombre hello des régions sont non équilibrées sur tous les serveurs de la région. Vous pouvez ensuite exécuter `hbase hbck` commande toosee des trous dans la chaîne de région de hello.

Trous peuvent résulter des régions en mode hors connexion hello, affectations de hello dans ce correctif tout d’abord. 

toobring hello régions non attribués à l’état normal tooa arrière, terminer hello comme suit :

1. Se connecter toohello HDInsight HBase cluster à l’aide de SSH.
2. tooconnect shell de soigneur hello, exécutez hello `hbase zkcli` commande.
3. Exécutez hello `rmr /hbase/regions-in-transition` commande ou hello `rmr /hbase-unsecure/regions-in-transition` commande.
4. tooexit de hello `hbase zkcli` shell, utilisez hello `exit` commande.
5. Ouvrez hello Apache Ambari UI et redémarrez hello Active HBase Master service.
6. Exécutez hello `hbase hbck` commande (sans les options). Vérifiez la sortie hello de cette tooensure de commande toutes les régions sont assignées.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Comment corriger les problèmes de délai d’expiration lors de l’utilisation des commandes hbck pour l’affectation des régions ?

### <a name="issue"></a>Problème

Une cause potentielle de problèmes de délai d’attente lorsque vous utilisez hello `hbck` commande peut être que plusieurs régions sont Bonjour « en transition » l’état d’un certain temps. Vous pouvez consulter ces régions hors connexion Bonjour HBase Master UI. Un grand nombre de régions tentent tootransition, HBase Master peut le délai d’attente et être toobring Impossible de ces régions en ligne.

### <a name="resolution-steps"></a>Étapes de résolution

1. Se connecter toohello HDInsight HBase cluster à l’aide de SSH.
2. tooconnect shell de soigneur hello, exécutez hello `hbase zkcli` commande.
3. Exécutez hello `rmr /hbase/regions-in-transition` ou hello `rmr /hbase-unsecure/regions-in-transition` commande.
4. tooexit hello `hbase zkcli` shell, utilisez hello `exit` commande.
5. Bonjour Ambari UI, redémarrer hello Active HBase Master.
6. Exécutez hello `hbase hbck -fixAssignments` réexécutez la commande.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Comment forcer la désactivation du mode sans échec du stockage HDFS dans un cluster ?

### <a name="issue"></a>Problème

Hello local Hadoop Distributed fichier système (HDFS) est bloqué en mode sans échec sur le cluster HDInsight de hello.

### <a name="detailed-description"></a>Description détaillée

Cette erreur peut résulter d’un échec lorsque vous exécutez hello HDFS commande suivante :

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

erreur Hello que vous pouvez voir lorsque vous essayez de commande de hello toorun ressemble à ceci :

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

### <a name="probable-cause"></a>Cause probable

Hello cluster HDInsight a été mis à l’échelle vers le bas tooa très peu de nœuds. nombre de Hello de nœuds est inférieur ou fermez le facteur de réplication toohello HDFS.

### <a name="resolution-steps"></a>Étapes de résolution 

1. Obtenez l’état hello Hello que HDFS sur hello HDInsight de cluster en exécutant hello suivant de commandes :

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
2. Vous pouvez également vérifier l’intégrité de hello Hello que HDFS sur hello HDInsight cluster à l’aide de hello suivant de commandes :

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

3. Si vous déterminez qu’il n’y a aucun bloc manquant, endommagé ou under-répliquées, ou que ces blocs peuvent être ignorées, exécutez hello suivant commande tootake hello nom du nœud du mode sans échec :

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Comment résoudre les problèmes de connectivité JDBC ou SQLLine avec Apache Phoenix ?

### <a name="resolution-steps"></a>Étapes de résolution

tooconnect avec Phoenix, vous devez fournir l’adresse IP de hello d’un nœud soigneur actif. Vérifiez que hello soigneur tente de service toowhich sqlline.py tooconnect est en cours d’exécution.
1. Se connecter toohello cluster HDInsight à l’aide de SSH.
2. Entrez hello de commande suivante :
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Vous pouvez obtenir l’adresse IP de hello du nœud de soigneur actif hello de hello Ambari UI. Accédez trop**HBase** > **liens rapides** > **ZK\* (actif)** > **soigneur informations**. 

3. Si hello sqlline.py se connecte tooPhoenix et n’expire pas, hello exécution commande suivante disponibilité de hello toovalidate et de l’intégrité de Phoenix :

   ```apache
           !tables
           !quit
   ```      
4. Si la commande fonctionne, il n’existe aucun problème. l’adresse IP Hello fournie par l’utilisateur de hello est peut-être incorrecte. Toutefois, si la commande hello s’interrompt pendant une durée prolongée, puis affiche hello l’erreur suivante, continuer toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Exécutez hello suivant les commandes à partir de condition de hello hello du nœud principal (hn0) toodiagnose Hello Phoenix système. Table du catalogue :

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   commande Hello doit retourner un suivant de toohello erreur similaire : 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. Bonjour Ambari UI, effectuez hello suivant du service de HMaster étapes toorestart hello sur tous les nœuds de soigneur :

    1. Bonjour **Résumé** section accédez trop de HBase,**HBase** > **Active HBase Master**. 
    2. Bonjour **composants** section, redémarrez hello HBase Master service.
    3. Répétez ces étapes pour les services **Standby HBase Master** (Master HBase de secours) restants. 

Il peut prendre jusqu'à minutes toofive hello HBase Master service toostabilize et terminer le processus de récupération hello. Après quelques minutes, répétez hello sqlline.py commandes tooconfirm ce système hello. Table du catalogue est activé et qu’il peut être interrogé. 

Lorsque hello système. Table du catalogue est différé toonormal, tooPhoenix de problème de connectivité hello doit être résolu automatiquement.


## <a name="what-causes-a-master-server-toofail-toostart"></a>Pourquoi un serveur maître toofail toostart

### <a name="error"></a>Error 

Le renommage atomique échoue.

### <a name="detailed-description"></a>Description détaillée

Au cours du processus de démarrage hello, HMaster termine le nombre d’étapes d’initialisation. Ceux-ci incluent le déplacement des données à partir de rien de hello (.tmp) dossier de données toohello. HMaster examine également toosee de dossier hello journaux WAL (WALs) s’il existe des serveurs de la région ne répond pas, et ainsi de suite. 

Lors du démarrage, HMaster exécute une commande `list` de base sur ces dossiers. S’il rencontre un fichier inattendu dans l’un de ces dossiers, il envoie une exception et ne démarre pas.  

### <a name="probable-cause"></a>Cause probable

Dans les journaux du serveur de la région de hello, essayez de chronologie de hello tooidentify de création du fichier hello et alors voir s’il y a qu'un arrêt de processus autour hello heure hello fichier a été créé. (Contactez HBase prise en charge tooassist vous dans cette opération.) Cela nous permet de vous fournir des mécanismes plus robustes afin de vous éviter ce bogue et de garantir un arrêt approprié des processus.

### <a name="resolution-steps"></a>Étapes de résolution

Vérifiez la pile des appels hello et essayez de toodetermine le dossier qui pose problème de hello (par exemple, il peut être hello WALs dossier ou un dossier de .tmp hello). Ensuite, dans l’Explorateur de Cloud ou à l’aide des commandes HDFS, essayez toolocate hello problème du fichier. En règle générale, il s’agit d’un fichier \*-renamePending.json. (hello \*-renamePending.json fichier est un fichier journal qui a utilisé les opération de changement de nom atomique hello tooimplement dans le pilote WASB hello. Échéance toobugs dans cette implémentation, ces fichiers peuvent être restant après les défaillances de processus et ainsi de suite.) Forcez la suppression de ce fichier soit dans Cloud Explorer, soit à l’aide de commandes HDFS. 

Dans certains cas, cet emplacement contient également un fichier temporaire nommé *$$$. $$$*. Vous avez toouse HDFS `ls` de la commande toosee ce fichier ; vous ne pouvez pas voir fichier hello dans Cloud Explorer. toodelete ce fichier, la commande HDFS hello use `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Après avoir exécuté ces commandes, HMaster devrait démarrer immédiatement. 

### <a name="error"></a>Error

Aucune adresse de serveur n’est répertoriée dans la table *hbase: meta* au niveau de la région xxx.

### <a name="detailed-description"></a>Description détaillée

Vous pouvez voir un message sur votre cluster Linux qui indique que hello *hbase : métadonnées* table n’est pas en ligne. L’exécution de la commande `hbck` peut renvoyer l’erreur suivante : « hbase: meta table replicaId 0 is not found on any region » (replicaId 0 introuvable dans toutes les régions de la table hbase: meta). Hello problème est peut-être que HMaster pas pu initialiser une fois que vous avez redémarré HBase. Dans les journaux HMaster hello, vous pouvez voir le message de type hello : « aucune adresse de serveur ne répertoriées dans hbase : les métadonnées pour la région hbase : sauvegarde \<nom de la région\>».  

### <a name="resolution-steps"></a>Étapes de résolution

1. Bonjour shell HBase, entrez hello suivant les commandes (modification de valeurs réelles, le cas échéant) :  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Supprimer hello *hbase : espace de noms* entrée. Cette entrée peut être hello même message d’erreur est signalée lorsque hello *hbase : espace de noms* table est analysée.

3. toobring des HBase en cours d’exécution, Bonjour Ambari UI, redémarrer hello HMaster Active.  

4. Bonjour shell HBase, toobring toutes les tables en mode hors connexion, exécutez hello de commande suivante :

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Documentation supplémentaire

[Table HBase à hello tooprocess Impossible](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Error

HMaster expire et un too"java.io.IOException similaires exception irrécupérable : 300000ms avec délai dépassé en attente de l’espace de noms table toobe est affecté. »

### <a name="detailed-description"></a>Description détaillée

Vous pourriez rencontrer ce problème si plusieurs tables et régions n’ont pas été vidées lors du redémarrage de vos services HMaster. Redémarrage risque d’échouer, et vous verrez hello précédant le message d’erreur.  

### <a name="probable-cause"></a>Cause probable

Il s’agit d’un problème connu avec hello HMaster service. Les tâches générales de démarrage du cluster peuvent prendre beaucoup de temps. HMaster s’arrête, car la table d’espace de noms hello n’est pas encore été affectée. Cela se produit uniquement lorsqu’une grande quantité de données n’a pas été vidée, et qu’un délai d’expiration de cinq minutes est insuffisant.
  
### <a name="resolution-steps"></a>Étapes de résolution

1. Bonjour Ambari UI, accédez trop**HBase** > **configurations**. Dans fichier de personnalisée hbase-site.XML de hello, ajoutez hello suivant paramètre : 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Redémarrez les services hello requis (HMaster et éventuellement d’autres services HBase).  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Pourquoi le redémarrage échoue-t-il sur un serveur régional ?

### <a name="issue"></a>Problème

L’échec du redémarrage d’un serveur régional peut être évité en respectant ces meilleures pratiques. Nous vous recommandons d’interrompre les activités de lourdes charges de travail lorsque vous planifiez des serveurs de la région toorestart HBase. Si une application poursuit tooconnect avec les serveurs de la région lors de l’arrêt est en cours, opération de redémarrage du serveur hello région sera plus lente en quelques minutes. Il est également un toofirst conseillé vidage que tous hello tables. Pour obtenir une référence sur la façon de tooflush tables, consultez [HDInsight HBase : comment cluster HBase de hello tooimprove redémarrage en vidant tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Si vous lancez le redémarrage hello sur HBase serveurs de la région de hello Ambari UI, vous voyez immédiatement que les serveurs de la région hello s’est arrêté, mais ils ne pas redémarrer immédiatement. 

Voici ce qui se passe en coulisses hello : 

1. agent de Ambari Hello envoie un arrêt demande toohello région serveur.
2. agent de Ambari Hello attend 30 secondes pour hello région server tooshut vers le bas en douceur. 
3. Si votre application continue tooconnect avec le serveur de la région de hello, serveur de hello ne sera pas arrêté immédiatement. délai d’attente de 30 secondes Hello arrive à expiration avant l’arrêt se produit. 
4. Après 30 secondes, l’agent de Ambari hello envoie un kill-force (`kill -9`) serveur de région toohello de commande. Vous pouvez le voir dans le journal d’ambari-agent hello (dans hello répertoire/var/log/du nœud de travail respectifs hello) :

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
En raison de l’arrêt brutal de hello, port hello associé hello processus ne peut pas libéré, même si le processus de serveur de la région de hello est arrêté. Cette situation peut entraîner tooan AddressBindException au démarrage de server de région de hello, comme indiqué dans hello suivant des journaux. Vous pouvez le vérifier dans la région de hello-server.log dans le répertoire de /var/log/hbase hello sur les nœuds de travail hello où le serveur de la région de hello échoue toostart. 

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

### <a name="resolution-steps"></a>Étapes de résolution

1. Essayez de charge de hello tooreduce sur les serveurs de la région hello HBase avant de lancer un redémarrage. 
2. Vous pouvez également try toomanually redémarrage région serveurs à l’aide de nœuds de travail hello hello suivant (si l’étape 1 ne permet pas), commandes :

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

