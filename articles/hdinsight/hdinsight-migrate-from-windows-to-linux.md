---
title: "aaaMigrate de HDInsight de basés sur Windows basée sur les tooLinux HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toomigrate à partir d’un HDInsight basés sur Windows tooa HDInsight de basés sur Linux cluster du cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Migrer à partir d’un cluster basés sur Linux de tooa de cluster HDInsight de basés sur Windows

Ce document fournit des détails sur les différences de hello entre HDInsight sur Windows et Linux et des conseils sur la façon de cluster basés sur Linux de toomigrate de charges de travail tooa.

HDInsight de basés sur Windows fournit une toouse facilement Hadoop dans le cloud de hello, vous devrez peut-être toomigrate tooa basés sur Linux cluster. Par exemple, tootake parti d’outils basés sur Linux et les technologies qui sont requis pour votre solution. Beaucoup de choses dans l’écosystème de Hadoop hello est développées sur les systèmes Linux et ne pas être disponibles pour une utilisation avec HDInsight de basés sur Windows. En outre, un grand nombre de livres, de vidéos et d’autres documents de formation supposent que vous employez un système Linux quand vous utilisez Hadoop.

> [!NOTE]
> Clusters HDInsight utilisent Ubuntu à long terme (LTS) en tant que système d’exploitation de hello pour les nœuds hello dans un cluster de hello. Pour plus d’informations sur la version de hello d’Ubuntu disponible avec HDInsight, ainsi que d’autres informations de contrôle de version de composant, consultez [versions des composants HDInsight](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Tâches de migration

flux de travail général Hello pour la migration est la suivante.

![Diagramme du workflow de migration](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Lisez chaque section de ce document toounderstand les modifications qui peuvent être nécessaires lors de la migration de votre flux de travail existant, les tâches et les clusters etc. tooa Linux.

2. Créez un cluster Linux comme environnement de test ou d’assurance qualité. Pour plus d’informations sur la création d’un cluster Linux, consultez [Création de clusters Linux dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Copie des travaux, des sources de données et récepteurs toohello nouvel environnement.

4. Effectuer une validation test toomake assurer que vos tâches fonctionnent comme prévu sur le nouveau cluster de hello.

Une fois que vous avez vérifié que tout fonctionne comme prévu, planifier des temps d’arrêt pour la migration de hello. Pendant ce temps mort, effectuer hello suivant des actions :

1. Sauvegardez toutes les données temporaires stockées localement sur les nœuds de cluster hello. par exemple si vous avez des données stockées directement sur un nœud principal.

2. Supprimer le cluster de basé sur Windows hello.

3. Créez un cluster basé sur Linux à l’aide de hello même hello cluster basé sur Windows utilisé par une banque de données de valeur par défaut. cluster de Hello basés sur Linux peut continuer à travailler sur vos données de production existant.

4. Importez toutes les données temporaires que vous avez sauvegardées.

5. Début travaux/continuer le traitement à l’aide du nouveau cluster de hello.

### <a name="copy-data-toohello-test-environment"></a>Environnement de test de toohello de données de copie

Nombreuses données toocopy hello et les travaux, toutefois hello deux présentés dans cette section sont hello plus simple méthodes toodirectly déplacer les fichiers tooa cluster de test.

#### <a name="hdfs-copy"></a>Copie HDFS

Utilisez hello suivant des données de toocopy d’étapes à partir du cluster de test toohello hello production cluster. Ces étapes utilisent hello `hdfs dfs` utilitaire qui est inclus avec HDInsight.

1. Trouver hello stockage par défaut et le compte d’informations sur le conteneur de votre cluster existant. Bonjour à l’exemple suivant utilise PowerShell tooretrieve ces informations :

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate un environnement de test, suivez les étapes de hello dans hello basés sur Linux de créer des clusters HDInsight document. Arrêter avant de créer le cluster de hello et sélectionnez à la place **Configuration facultative**.

3. Dans le panneau de Configuration facultatives hello, sélectionnez **des comptes de stockage liés**.

4. Sélectionnez **ajouter une clé de stockage**et lorsque vous y êtes invité, sélectionnez le compte de stockage hello qui a été retournée par hello script PowerShell à l’étape 1. Cliquez sur **Sélectionner** dans chaque panneau. Enfin, créez le cluster de hello.

5. Une fois que le cluster de hello a été créé, se connecter à l’aide de tooit **SSH.** Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

6. À partir de la session SSH de hello, utilisez hello suivant des fichiers de commandes toocopy dans hello lié stockage compte toohello par défaut compte de stockage. Remplacez le conteneur avec les informations de conteneur hello retournées par PowerShell. Remplacez __compte__ par le nom de compte hello. Remplacez toodata de chemin d’accès hello par fichier de données tooa hello chemin d’accès.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Si la structure de répertoire hello qui contient les données de salutation n’existe pas sur l’environnement de test hello, vous pouvez créer à l’aide de hello de commande suivante :

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Hello `-p` commutateur permet la création de tous les répertoires dans le chemin d’accès hello hello.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Copie directe entre les objets blob dans Stockage Azure

Vous pouvez également toouse hello `Start-AzureStorageBlobCopy` Azure PowerShell applet de commande toocopy objets BLOB entre des comptes de stockage en dehors de HDInsight. Pour plus d’informations, consultez Comment hello toomanage section objets BLOB Azure à l’aide d’Azure PowerShell avec le stockage Azure.

## <a name="client-side-technologies"></a>Technologies côté client

Les technologies côté client telles que [applets de commande Azure PowerShell](/powershell/azureps-cmdlets-docs), [CLI d’Azure](../cli-install-nodejs.md), ou hello [.NET SDK pour Hadoop](https://hadoopsdk.codeplex.com/) continuer toowork les clusters basés sur Linux. Ces technologies reposent sur REST API qui sont identiques hello les deux types de cluster du système d’exploitation.

## <a name="server-side-technologies"></a>Technologies côté serveur

Hello tableau suivant fournit des conseils sur la migration des composants côté serveur qui sont spécifiques à Windows.

| Si vous utilisez cette technologie... | Procédez comme suit... |
| --- | --- |
| **PowerShell** (scripts côté serveur, notamment les actions de script utilisées lors de la création du cluster) |Réécrivez-les en tant que scripts Bash. En ce qui concerne les actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md) et [Développement d’actions de script avec HDInsight](hdinsight-hadoop-script-actions-linux.md). |
| **Interface de ligne de commande Azure** (scripts côté serveur) |Hello CLI d’Azure est disponible sous Linux, il n’est pas préinstallé sur les nœuds principaux d’un cluster HDInsight hello. Pour plus d’informations sur l’installation de hello CLI d’Azure, consultez [prise en main Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **Composants .NET** |.NET est pris en charge sur HDInsight sous Linux via [Mono](https://mono-project.com). Pour plus d’informations, consultez [solutions .NET de migration basée sur tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Composants Win32 ou autre technologie propre à Windows** |Conseils dépendent hello composant ou une technologie. Vous pouvez être en mesure de toofind une version compatible avec Linux, ou vous devez toofind une solution alternative ou réécrire ce composant. |

> [!IMPORTANT]
> gestion de HDInsight Hello SDK n’est pas entièrement compatible avec Mono. Il ne doit pas être utilisé comme partie des solutions déployées toohello HDInsight cluster pour l’instant.

## <a name="cluster-creation"></a>Création du cluster

Cette section fournit des informations sur les différences dans la création du cluster.

### <a name="ssh-user"></a>Utilisateur SSH

Les clusters HDInsight basés sur Linux utilisent hello **Secure Shell (SSH)** protocole des nœuds de cluster toohello tooprovide accès à distance. Contrairement au Bureau à distance pour les clusters sous Windows, la plupart des clients SSH ne fournissent pas d’expérience utilisateur graphique. Au lieu de cela, les clients SSH fournissent une ligne de commande qui vous permet de toorun commandes sur le cluster de hello. Certains clients (tels que [MobaXterm](http://mobaxterm.mobatek.net/)) fournissent un Explorateur de système de fichiers de graphique dans la ligne de commande à distance plus tooa.

Lors de la création du cluster, vous devez fournir un utilisateur SSH et un **mot de passe** ou un **certificat de clé publique** pour l’authentification.

Nous recommandons d’utiliser un certificat de clé publique, qui est plus sécurisé qu’un mot de passe. L’authentification par certificat fonctionne en générant une paire de clés publique/privée signée, puis en fournissant la clé publique de hello lors de la création du cluster de hello. Lors de la connexion serveur toohello à l’aide de SSH, clé privée de hello sur le client de hello fournit l’authentification de connexion de hello.

Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Personnalisation des clusters

Les **actions de script** utilisées avec les clusters Linux doivent être écrites dans un script Bash. Alors que les Actions de Script peuvent être utilisées au cours de création d’un cluster, pour les clusters basés sur Linux ils peuvent également être utilisés tooperform personnalisation après qu’un cluster est disponible et en cours d’exécution. Pour plus d’informations, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md) et [Développement d’actions de script avec HDInsight](hdinsight-hadoop-script-actions-linux.md).

**Bootstrap**est une autre fonctionnalité de personnalisation. Pour les clusters Windows, cette fonctionnalité vous permet d’emplacement de hello toospecify de bibliothèques supplémentaires pour une utilisation avec la ruche. Après la création du cluster, ces bibliothèques sont automatiquement disponibles pour une utilisation avec les requêtes Hive sans hello besoin toouse `ADD JAR`.

fonctionnalité d’amorçage Hello pour les clusters basés sur Linux ne fournit pas cette fonctionnalité. Utilisez à la place l’action de script décrite dans [Ajouter les bibliothèques Hive lors de la création de cluster HDInsight](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Virtual Network

Les clusters HDInsight Windows fonctionnent uniquement avec les réseaux virtuels classiques tandis que les clusters HDInsight Linux nécessitent des réseaux virtuels Resource Manager. Si vous disposez de ressources un réseau virtuel classique qui hello cluster HDInsight de Linux doit se connecter à, consultez [la connexion à un gestionnaire de ressources des réseaux virtuels de tooa réseau virtuel classique](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Pour plus d’informations sur la configuration requise pour utiliser des réseaux virtuels Azure avec HDInsight, consultez [Extension des capacités de HDInsight à l’aide d’Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Gestion et surveillance

La plupart du site web hello interfaces utilisateur que vous avez peut-être utilisé avec HDInsight basés sur Windows, telles que l’historique des travaux ou d’interface utilisateur de fils, sont disponibles via Ambari. En outre, hello vue de la ruche Ambari fournit un moyen toorun requêtes Hive à l’aide de votre navigateur web. Hello l’interface utilisateur de Ambari Web est disponible sur les clusters basés sur Linux à https://CLUSTERNAME.azurehdinsight.net.

Pour plus d’informations sur l’utilisation de Ambari, consultez hello suivant des documents :

* [Interface utilisateur web Ambari](hdinsight-hadoop-manage-ambari.md)
* [API Ambari REST](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Alertes Ambari

Ambari est un système d’alerte qui peut vous indiquer des problèmes potentiels avec le cluster de hello. Les alertes s’affichent sous forme d’entrées rouges ou jaunes Bonjour l’interface utilisateur de Ambari Web, toutefois, vous pouvez également récupérer via l’API REST de hello.

> [!IMPORTANT]
> Les alertes Ambari indiquent qu’un problème se pose *peut-être* et non pas qu’un problème se pose *vraiment*. Par exemple, vous pouvez recevoir une alerte indiquant que HiveServer2 n’est pas accessible, même si vous pouvez y accéder normalement.
>
> De nombreuses alertes sont implémentées comme des requêtes basées sur un intervalle pour un service et attendent une réponse dans un intervalle de temps spécifique. Afin de l’alerte de hello ne signifie pas nécessairement que hello service est arrêté, juste qu’il n’a pas retourné les résultats dans un laps de temps hello attendu.

Vous devez évaluer si une alerte se produit pendant une période prolongée, ou si elle reflète des problèmes d’utilisateur qui ont été signalés avant de prendre des mesures.

## <a name="file-system-locations"></a>Emplacements du système de fichiers

Hello système de fichiers de cluster Linux est disposé différemment des clusters HDInsight de basés sur Windows. Utilisez hello table toofind couramment utilisée fichiers suivants.

| Je dois toofind... | Il se trouve dans... |
| --- | --- |
| Configuration |`/etc`. Par exemple, `/etc/hadoop/conf/core-site.xml` |
| Fichiers journaux |`/var/logs` |
| Hortonworks Data Platform (HDP) |`/usr/hdp`. Il existe deux répertoires situés dans ce cas, une version HDP actuelle hello et `current`. Hello `current` répertoire contient des liens symboliques toofiles et les répertoires situés dans le répertoire de numéro de version hello. Hello `current` active est fournie comme un moyen pratique de l’accès aux fichiers HDP depuis hello numéro de version changements comme hello HDP est mise à jour. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

En règle générale, si vous connaissez le nom du fichier de hello de hello, vous pouvez utiliser hello de commande suivante à partir d’un chemin de fichier SSH session toofind hello :

    find / -name FILENAME 2>/dev/null

Vous pouvez également utiliser des caractères génériques avec le nom de fichier hello. Par exemple, `find / -name *streaming*.jar 2>/dev/null` renvoie hello chemin d’accès tooany fichiers jar qui contiennent le mot hello streaming en tant que partie du nom de fichier hello.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig et MapReduce

Les charges de travail Pig et MapReduce sont similaires sur les clusters Linux. Toutefois, les clusters HDInsight sous Linux peuvent être créés à l’aide de versions plus récentes de Hadoop, Hive et Pig. Ces différences de version peuvent introduire des modifications dans le fonctionnement de vos solutions existantes. Pour plus d’informations sur les versions des composants inclus avec HDInsight hello, consultez [le contrôle de version HDInsight composant](hdinsight-component-versioning.md).

HDInsight sous Linux ne fournit pas la fonctionnalité de bureau à distance. Au lieu de cela, vous pouvez utiliser le protocole SSH tooremotely connecter toohello nœuds principaux d’un cluster. Pour plus d’informations, consultez hello suivant des documents :

* [Utilisation de Hive avec SSH](hdinsight-hadoop-use-hive-ssh.md)
* [Utiliser Pig avec SSH](hdinsight-hadoop-use-pig-ssh.md)
* [Utiliser MapReduce avec SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Si vous utilisez un magasin de métadonnées externe de ruche, vous devez sauvegarder le magasin de métadonnées hello avant de l’utiliser avec HDInsight de basés sur Linux. HDInsight sous Linux est disponible avec les versions plus récentes de Hive, qui peut se révéler incompatible avec les metastores créés par les versions antérieures.

Hello suivant graphique fournit des conseils sur la migration de vos charges de travail Hive.

| Sur Windows, j’utilise... | Sur Linux, j’utilise... |
| --- | --- |
| **Éditeur Hive** |[Affichage Hive dans Ambari](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez est le moteur d’exécution par défaut hello pour les clusters basés sur Linux, afin de définie l’instruction hello n’est plus nécessaire. |
| Fonctions définies par l’utilisateur C# | Pour plus d’informations sur la validation des composants C# hdinsight de basés sur Linux, consultez [solutions .NET de migration basée sur tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Fichiers CMD ou des scripts sur serveur hello invoqué en tant que partie d’une tâche Hive |Scripts Bash |
| `hive` à partir du Bureau à distance |Utilisez [Beeline](hdinsight-hadoop-use-hive-beeline.md) ou [Hive à partir d’une session SSH](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| Sur Windows, j’utilise... | Sur Linux, j’utilise... |
| --- | --- |
| Fonctions définies par l’utilisateur C# | Pour plus d’informations sur la validation des composants C# hdinsight de basés sur Linux, consultez [solutions .NET de migration basée sur tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Fichiers CMD ou des scripts sur serveur hello invoqué en tant que partie d’une tâche Pig |Scripts Bash |

### <a name="mapreduce"></a>MapReduce

| Sur Windows, j’utilise... | Sur Linux, j’utilise... |
| --- | --- |
| Composants du mappeur et raccord de réduction C# | Pour plus d’informations sur la validation des composants C# hdinsight de basés sur Linux, consultez [solutions .NET de migration basée sur tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Fichiers CMD ou des scripts sur serveur hello invoqué en tant que partie d’une tâche Hive |Scripts Bash |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Si vous utilisez un magasin de métadonnées Oozie externe, vous devez sauvegarder le magasin de métadonnées hello avant de l’utiliser avec HDInsight de basés sur Linux. HDInsight sous Linux est disponible avec les versions plus récentes d’Oozie, qui peut se révéler incompatible avec les metastores créés par les versions antérieures.

Les flux de travail Oozie autorisent les actions de l’interpréteur de commandes. Les actions de shell utilisent le shell par défaut de hello pour les commandes de ligne de commande du toorun hello système d’exploitation. Si vous avez Oozie de flux de travail qui s’appuient sur hello interpréteur de commandes Windows, vous devez réécrire toorely de flux de travail hello dans l’environnement de shell Linux hello (interpréteur de commandes). Pour plus d’informations sur l’utilisation des actions de l’interpréteur de commandes avec Oozie, consultez [Extension d’action d’interpréteur de commandes Oozie](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).

Si vous avez des flux de travail Oozie qui s’appuient sur les applications C# appelées à l’aide des actions de l’interpréteur de commandes, vous devez valider ces applications dans un environnement Linux. Pour plus d’informations, consultez [solutions .NET de migration basée sur tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| Sur Windows, j’utilise... | Sur Linux, j’utilise... |
| --- | --- |
| Tableau de bord Storm |Hello Storm le tableau de bord n’est pas disponible. Consultez [topologies de déployer et gérer une tempête sur HDInsight de basés sur Linux](hdinsight-storm-deploy-monitor-topology-linux.md) pour les topologies toosubmit façons |
| Interface utilisateur de Storm |Hello Storm UI est disponible à l’adresse https://CLUSTERNAME.azurehdinsight.net/stormui |
| Visual Studio toocreate, déployer et gérer des topologies c# ou hybride |Visual Studio peut être utilisé toocreate, déployer et gérer c# (SCP.NET) ou les topologies hybride sur tempête de basés sur Linux sur les clusters HDInsight créés après le 28/10/2016. |

## <a name="hbase"></a>HBase

Sur les clusters basés sur Linux, est parent de znode hello pour HBase `/hbase-unsecure`. Définissez cette valeur dans la configuration de hello pour toutes les applications clientes Java qui utilisent les API de Java HBase native.

Pour obtenir un exemple de client qui définit cette valeur, consultez [Utilisation de Maven pour créer des applications Java utilisant HBase avec HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) .

## <a name="spark"></a>Spark

Les clusters Spark étaient disponibles sur les clusters Windows dans la version préliminaire. La version mise à la disponibilité générale (GA) de Spark est uniquement disponible avec les clusters Linux. Il n’existe aucun chemin de migration d’un cluster de Spark de basés sur Windows aperçu cluster tooa version Spark de basés sur Linux.

## <a name="known-issues"></a>Problèmes connus

### <a name="azure-data-factory-custom-net-activities"></a>Activités .NET personnalisées Azure Data Factory

Les activités .NET personnalisées Azure Data Factory ne sont actuellement pas prises en charge sur les clusters HDInsight Linux. Au lieu de cela, vous devez utiliser une des hello suivant des activités personnalisées de méthodes tooimplement dans le cadre de votre pipeline ADF.

* Exécutez les activités .NET sur le pool Azure Batch. Voir section de service lié d’utiliser Azure Batch hello de [utiliser des activités personnalisées dans un pipeline Azure Data Factory](../data-factory/data-factory-use-custom-activities.md)
* Implémentez l’activité hello comme une activité MapReduce. Pour plus d’informations, consultez [Appeler des programmes MapReduce à partir de Data Factory](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Fins de ligne

En règle générale, les fins de ligne sur les systèmes Windows utilisent CRLF, alors que les systèmes Linux utilisent LF. Si vous produisez ou que vous attendez, les données à des fins de ligne CRLF, vous devrez peut-être toomodify hello producteurs ou consommateurs toowork avec la fin de ligne hello LF.

Par exemple, HDInsight sur un cluster basé sur Windows à l’aide d’Azure PowerShell tooquery renvoie des données avec CRLF. Hello même requête avec un cluster basé sur Linux retourne LF. Vous devez tester toosee si la fin de ligne hello provoque un problème avec votre solutuion avant la migration de cluster de tooa basés sur Linux.

Si vous avez des scripts qui sont exécutées directement sur les nœuds de cluster Linux hello, vous devez toujours utiliser le saut de ligne en tant que la fin de ligne hello. Si vous utilisez CRLF, des erreurs peuvent apparaître lors de l’exécution des scripts de hello sur un cluster basé sur Linux.

Si vous savez que les scripts de hello ne contiennent pas de chaînes de caractères CR incorporés, vous pouvez en bloc les fins de ligne hello de modification à l’aide d’une des méthodes suivantes de hello :

* **Avant de télécharger toohello cluster**: hello utilisation suivant les fins de ligne hello PowerShell instructions toochange CRLF tooLF avant de télécharger le cluster de toohello script hello.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Après avoir téléchargé toohello cluster**: suivant de hello utilisation de commandes à partir d’un toohello de session SSH script de hello toomodify cluster basé sur Linux.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Étapes suivantes

* [Découvrez comment toocreate clusters HDInsight de basés sur Linux](hdinsight-hadoop-provision-linux-clusters.md)
* [Utiliser SSH tooconnect tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Gérer des clusters HDInsight à l’aide de l’interface utilisateur Web d’Ambari](hdinsight-hadoop-manage-ambari.md)
