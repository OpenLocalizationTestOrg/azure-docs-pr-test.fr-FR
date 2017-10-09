---
title: "aaaInstall ou mettre à jour Mono sur HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse une version spécifique de Mono avec le cluster HDInsight. Mono est utilisé toorun .NET applications sur les clusters HDInsight de basés sur Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Installation ou mise à jour de Mono sur HDInsight

Découvrez comment tooinstall une version spécifique de [Mono](https://www.mono-project.com) dans HDInsight 3.4 ou version ultérieure.

Mono est installé sur HDInsight 3.4 et versions ultérieures et est utilisé toorun applications .NET. Pour plus d’informations sur la version de hello de Mono inclus avec chaque version de HDInsight, consultez [le contrôle de version HDInsight composant](hdinsight-component-versioning.md). tooinstall une version différente sur votre cluster, utilisez hello script action dans ce document. 

## <a name="how-it-works"></a>Fonctionnement

Ce script accepte hello suivant paramètre :

* __Numéro de version mono__: version hello de tooinstall Mono. version de Hello doit être disponible à partir de [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

script de Hello installe hello suivant Mono packages :

* __mono-complete__

* __ca-certificates-mono__

## <a name="hello-script"></a>script de Hello

__Emplacement du script__ : [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Conditions requises__ :

* script de Hello doit être appliquée sur hello __head nœuds__ et __nœuds worker__.

## <a name="toouse-hello-script"></a>script de hello toouse

Pour plus d’informations sur comment toouse ce script avec HDInsight, consultez hello [HDInsight de basés sur Linux de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document. Vous pouvez utiliser le script hello via hello portail Azure, Azure PowerShell, ou hello CLI d’Azure.

Alors que suit hello document d’action de script, utilisez hello suivant l’URI :

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Lors de la configuration HDInsight avec ce script, sélectionnez script hello en tant que __Persisted__. Ce paramètre permet de nœuds de tooworker script hello ajoutées via les opérations de mise à l’échelle HDInsight tooapply.


## <a name="next-steps"></a>Étapes suivantes

Vous avez appris comment tooupgrade ou installez une version spécifique de Mono sur HDInsight. Pour plus d’informations sur l’utilisation des applications .NET avec Mono sur HDInsight, consultez hello suivant des documents :

* [Utilisation de .NET pour la diffusion MapReduce sur HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Utilisation de .NET avec Hive et Pig sur HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Développement de solutions C# avec Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Migrer des solutions .NET basée sur tooLinux de HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Pour plus d’informations sur l’utilisation des actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md)