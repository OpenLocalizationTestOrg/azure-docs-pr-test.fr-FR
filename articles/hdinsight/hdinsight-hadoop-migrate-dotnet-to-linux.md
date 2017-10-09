---
title: "aaaUse .NET avec Hadoop MapReduce dans HDInsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment les applications .NET toouse de diffusion en continu MapReduce sur HDInsight de basés sur Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Migrer des solutions .NET pour HDInsight de basés sur Windows basée sur les tooLinux de HDInsight

Utilisation des clusters basés sur Linux de HDInsight [Mono (https://mono-project.com)](https://mono-project.com) toorun les applications .NET. Mono vous permet de composants de .NET toouse telles que les applications MapReduce hdinsight de basés sur Linux. Dans ce document, découvrez comment les solutions de .NET toomigrate créé pour toowork des clusters basés sur Windows de HDInsight avec Mono sur HDInsight de basés sur Linux.

## <a name="mono-compatibility-with-net"></a>Compatibilité de Mono avec .NET

La version 4.2.1 de Mono est incluse dans la version 3.5 de HDInsight. Pour plus d’informations sur la version de hello de Mono inclus avec HDInsight, consultez [versions des composants HDInsight](hdinsight-component-versioning.md). tooinstall une version spécifique de Mono, consultez hello [installation ou mise à jour Mono](hdinsight-hadoop-install-mono.md) document.

Pour plus d’informations sur la compatibilité entre Mono et .NET, consultez hello [compatibilité Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.

> [!IMPORTANT]
> infrastructure SCP.NET Hello est compatible avec Mono. Pour plus d’informations sur l’utilisation de SCP.NET avec Mono, consultez [topologies de toodevelop C# utilisez Visual Studio d’Apache Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Analyse de portabilité automatisée

Hello [Analyseur de portabilité .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) peut être utilisé toogenerate un rapport des incompatibilités entre votre application et de Mono. Utilisez hello suivant les étapes tooconfigure hello analyseur toocheck votre application pour une portabilité Mono :

1. Installer hello [Analyseur de portabilité .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Pendant l’installation, sélectionnez la version hello de toouse de Visual Studio.

2. À partir de Visual Studio 2015, sélectionnez __analyser__ > __paramètres d’analyseur de portabilité__et vous assurer que __4.5__ est archivé hello __Mono__  section.

    ![4.5 archivé Mono section pour les paramètres d’analyseur hello](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Sélectionnez __OK__ configuration de hello toosave.

3. Sélectionnez __Analyser__ > __Analyser la portabilité d’Assembly__. Sélectionnez assembly hello qui contient votre solution, puis __ouvrir__ toobegin analyse.

4. Une fois l’analyse terminée, sélectionnez __Analyser__ > __Afficher les rapports d’analyse__. Dans __résultats de l’analyse portabilité__, sélectionnez __ouvrir rapport__ tooopen un rapport.

    ![Boîte de dialogue des résultats de l’analyseur de portabilité](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Analyseur de Hello ne peut pas intercepter tous les problèmes avec votre solution. Par exemple, un chemin de fichier de `c:\temp\file.txt` est considéré comme OK car Mono s’exécute sur Windows et le chemin d’accès de hello est valide dans ce contexte. Toutefois, le chemin d’accès hello n’est pas valide sur une plate-forme Linux.

## <a name="manual-portability-analysis"></a>Analyse de portabilité manuelle

Effectuer un audit manuel de votre code à l’aide des informations de hello Bonjour [la portabilité des applications (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.

## <a name="modify-and-build"></a>Modifier et générer

Vous pouvez continuer à toouse Visual Studio toobuild vos solutions .NET pour HDInsight. Toutefois, vous devez vérifier que ce projet hello est configuré toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Déploiement et test

Une fois que vous avez modifié votre solution à l’aide de recommandations hello à partir de hello Analyseur de portabilité .NET ou d’une analyse manuelle, vous devez la tester avec HDInsight. Test de solution hello sur un cluster HDInsight de basés sur Linux peut révéler des problèmes subtils toobe corrigé. Nous vous recommandons d’activer la fonction de journalisation supplémentaire dans votre application lors de son test.

Pour plus d’informations sur l’accès aux journaux, consultez hello suivant des documents :

* [Accéder aux journaux des applications YARN dans HDInsight sous Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Étapes suivantes

* [Utilisation de C# avec MapReduce dans HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Utilisation des fonctions définies par l’utilisateur C# avec Hive et Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Développement de topologies C# pour Storm sur HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)