---
title: aaaUse un PC Windows avec Hadoop dans HDInsight - Azure | Documents Microsoft
description: "Travailler à partir d’un PC Windows dans Hadoop sur HDInsight. Gérer et interroger des clusters avec les outils PowerShell, Visual Studio et Linux. Développer des solutions Big Data avec .NET."
services: hdinsight
keywords: hadoop sur windows,hadoop pour windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Travail Bonjour écosystème Hadoop dans HDInsight à partir d’un PC Windows

En savoir plus sur le développement et les options de gestion sur hello PC Windows pour travailler dans l’écosystème hello Hadoop HDInsight. 

HDInsight est basé sur Apache Hadoop, et sur des composants et des technologies Hadoop open source développées sur Linux. HDInsight version 3.4 et versions ultérieures utilise hello distribution Ubuntu Linux comme hello sous-jacente du système d’exploitation pour le cluster de hello. Vous pouvez cependant travailler avec HDInsight à partir d’un client Windows ou de l’environnement de développement Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Utiliser PowerShell pour les tâches de gestion et de déploiement
Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser les tâches de déploiement et de gestion dans HDInsight à partir de Windows.

Voici des exemples de tâches que vous pouvez effectuer avec PowerShell :

* [Créer des clusters en utilisant PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Exécuter des requêtes Hive avec PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Gérer des clusters avec PowerShell](hdinsight-administer-use-powershell.md)

Suivez les étapes trop[installer et configurer Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) version la plus récente tooget hello. Si vous avez des scripts qui doivent toobe modifié toouse hello nouvelles applets de commande pour le Gestionnaire de ressources Azure, consultez [migrer tooAzure des outils de développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Utilitaires que vous pouvez exécuter dans un navigateur
Hello utilitaires suivants ont une interface utilisateur qui s’exécute dans un navigateur web :
* **[Interface de cloud computing Azure (aperçu)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  est un interpréteur de commandes interactive, la ligne de commande qui s’exécute dans votre navigateur et depuis hello portail Azure.
* **[L’interface utilisateur Web de Ambari](hdinsight-hadoop-manage-ambari.md)**  est une gestion et surveillance utilitaire disponible dans hello portail Azure qui peut être utilisés toomanage différents types de tâches, telles que :
    * [Utilisez Ambari avec hello API REST](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Affichage Hive dans Ambari](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Vue Tez dans Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Data Lake Tools (Hadoop) pour Visual Studio
Utilisez Data Lake Tools pour Visual Studio toodeploy et gérer des topologies de Storm. Outils de LAC de données installe également hello SCP.NET SDK, qui vous permet de topologies de C# Storm toodevelop avec Visual Studio.

Avant d’aborder toohello suivez exemples [installation et essayez de Data Lake Tools pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Voici des exemples de tâches que vous pouvez effectuer avec Visual Studio et Data Lake Tools pour Visual Studio :
* [Déployer et gérer des topologies Storm depuis Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Développer des topologies C# pour Storm à l’aide de Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md). les bits Hello incluent des exemples de modèles pour les topologies Storm, vous pouvez vous connecter à toodatabases, telles que la base de données Azure Cosmos et de la base de données SQL.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio et hello .NET SDK 

Vous pouvez utiliser Visual Studio avec des clusters de toomanage .NET SDK hello et développer des applications de données volumineuses. Vous pouvez utiliser les autres environnements IDE pour hello tâches suivantes, mais les exemples sont présentés dans Visual Studio.

Exemples de tâches que vous pouvez faire avec hello SDK .NET dans Visual Studio :
* [Créer des clusters et travailler dans HDInsight à partir d’une application .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Exécuter des requêtes Hive à l’aide de hello .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [Utiliser des fonctions C# définies par l’utilisateur avec le streaming Hive et Pig sur Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> Conseil Si vous utilisez des solutions .NET avec des clusters HDInsight de basés sur Windows, il est un tooplan de temps une migration basée sur tooLinux de clusters. Pour plus d’informations, consultez [solution de migration de .NET pour HDInsight de basés sur Windows basée sur les tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>Intellij IDEA et IDE Eclipse pour les clusters Spark
Les deux [Intellij idée](https://www.jetbrains.com/idea/download) et hello [IDE Eclipse](https://www.eclipse.org/downloads/) peut être utilisé pour :
* Développer et soumettre une application Scala Spark sur un cluster HDInsight Spark.
* Accéder à des ressources de cluster Spark.
* Développer et exécuter une application Scala Spark localement.

Ces articles expliquent comment : 
* Intellij idée : [applications Spark de créer à l’aide de hello Azure Toolkit pour Intellij plug-in et hello Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE ou Scala IDE pour Eclipse : [des applications de création de Spark et hello boîte à outils Azure pour Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Notebooks sur Spark pour les scientifiques des données 
Les clusters Apache Spark dans HDInsight incluent les notebooks et les noyaux Zeppelin qui peuvent être utilisés avec les notebooks Jupyter. 

* [Découvrez comment noyaux toouse sur Spark clusters avec des applications de Spark Notebook blocs-notes tootest](hdinsight-apache-spark-zeppelin-notebook.md)
* [Découvrez comment les blocs-notes de Zeppelin toouse sur Spark clusters travaux de Spark toorun](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Exécuter sur Windows des outils et des technologies basés sur Linux

Si vous rencontrez une situation où vous devez utiliser un outil ou une technologie qui est uniquement disponible sur Linux, tenez compte des hello options suivantes :

* **Bash (bêta) sur Windows 10** fournit un sous-système Linux sur Windows. Interpréteur de commandes vous permet de toodirectly exécuter des utilitaires de Linux sans avoir toomaintain une installation Linux dédiée. [Installer et exécuter la version bêta de hello Bash sur Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker pour Windows** fournit des outils basés sur Linux de réduire l’accès et peut être exécuté directement à partir de Windows. Par exemple, vous pouvez utiliser le client Beeline de Docker toorun hello pour la ruche directement à partir de Windows. Vous pouvez également utiliser Docker toorun un bloc-notes jupyter local et vous connecter à distance de tooSpark sur HDInsight. [Bien démarrer avec Docker pour Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  vous permet de système de fichiers toographically Parcourir hello cluster sur une connexion SSH.

## <a name="next-steps"></a>Étapes suivantes
Si vous êtes de nouveau tooworking dans des clusters basés sur Linux, consultez hello suivre les articles :
* [Configurer Hadoop, Kafka, Spark ou d’autres clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [Conseils pour les clusters HDInsight sur Linux](hdinsight-hadoop-linux-information.md)