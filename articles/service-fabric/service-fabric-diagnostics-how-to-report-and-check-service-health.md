---
title: "contrôle d’intégrité aaaReport et vérification avec Azure Service Fabric | Documents Microsoft"
description: "Découvrez comment l’intégrité de toosend les rapports à partir de votre code de service et comment le contrôle d’intégrité de hello toocheck de votre service à l’aide des outils de surveillance de la santé hello que Azure Service Fabric fournit."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Signaler et contrôler l’intégrité du service
Lorsque vos services rencontrent des problèmes, votre capacité toorespond tooand correctif incidents et les pannes dépend de vos problèmes de hello toodetect capacité rapidement. Si vous signalez des problèmes et des défaillances du Gestionnaire de contrôle d’intégrité toohello Azure Service Fabric à partir de votre code de service, vous pouvez utiliser que le Service Fabric fournit l’état d’intégrité toocheck hello des outils d’analyse d’état standard.

Il existe trois méthodes que vous pouvez signaler l’intégrité du service de hello :

* Utilisez les objets [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).  
  Vous pouvez utiliser hello `Partition` et `CodePackageActivationContext` objets de contrôle d’intégrité de hello tooreport d’éléments qui font partie du contexte actuel de hello. Par exemple, le code qui s’exécute en tant que partie d’un réplica peut signaler d’intégrité uniquement sur ce réplica, partition hello auquel il appartient et application hello dont il fait partie de.
* Utilisez `FabricClient`.   
  Vous pouvez utiliser `FabricClient` intégrité tooreport à partir du code de service hello si hello cluster n’est pas [sécurisé](service-fabric-cluster-security.md) ou si le service de hello est en cours d’exécution avec des privilèges d’administrateur. La plupart des scénarios réels n’utilisent pas de clusters non sécurisés et ne fournissent pas de privilèges Administrateur. Avec `FabricClient`, vous pouvez signaler l’intégrité de toute entité qui fait partie du cluster de hello. Dans l’idéal, toutefois, code de service doit uniquement envoyer des rapports qui sont la santé propres tooits connexes.
* Utilisez hello API REST au cluster de hello, application, application déployée, service, package de service, partition, réplicas ou les niveaux de nœud. Cela peut être l’intégrité tooreport utilisé dans un conteneur.

Cet article vous guide dans un exemple où les rapports d’intégrité à partir de code de service hello. Hello montre également comment outils hello fournies par l’infrastructure de Service peuvent être l’état d’intégrité utilisées toocheck hello. Cet article est prévue toobe un brève introduction toohello d’analyse du fonctionnement fonctionnalités du Service Fabric. Pour plus d’informations, vous pouvez lire série hello des articles détaillés sur le contrôle d’intégrité qui commencent par un lien de hello en fin de hello de cet article.

## <a name="prerequisites"></a>Composants requis
Vous devez disposer de hello installé :

* Visual Studio 2015 ou Visual Studio 2017
* SDK Service Fabric

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate un cluster local développement sécurisé
* Ouvrez PowerShell avec des privilèges d’administrateur et exécutez hello suivant de commandes :

![Commandes qui montrent comment toocreate un cluster de développement sécurisé](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy une application et vérifier son état d’intégrité
1. Ouvrez Visual Studio en tant qu’administrateur.
2. Créer un projet à l’aide de hello **avec état Service** modèle.
   
    ![Créer une application Service Fabric avec des services avec état](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Appuyez sur **F5** application hello de toorun en mode débogage. Hello application est déployée toohello local.
4. Après l’application hello est en cours d’exécution, cliquez sur icône du Gestionnaire du Cluster Local hello dans la zone de notification hello et sélectionnez **gérer un Cluster Local** de tooopen de menu contextuel hello Service Fabric Explorer.
   
    ![Ouvrez Service Fabric Explorer à partir de la zone de notification](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. intégrité des applications Hello doit être affichée comme dans cette image. À ce stade, l’application hello doit être saine sans erreurs.
   
    ![Application saine dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Vous pouvez également vérifier l’intégrité de hello à l’aide de PowerShell. Vous pouvez utiliser ```Get-ServiceFabricApplicationHealth``` toocheck contrôle d’intégrité d’une application et vous pouvez utiliser ```Get-ServiceFabricServiceHealth``` toocheck contrôle d’intégrité d’un service. Hello rapport d’intégrité pour hello même application dans PowerShell est dans cette image.
   
    ![Application saine dans PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>code de service tooadd l’intégrité personnalisée événements tooyour
modèles de projet de Service Fabric Hello dans Visual Studio contiennent un exemple de code. Hello étapes suivantes montrent comment vous pouvez signaler des événements d’état personnalisé à partir de votre code de service. Ces rapports s’affichent automatiquement dans les outils standard hello pour que l’infrastructure de Service fournit, telles que le Service Fabric Explorer, vue de contrôle d’intégrité du portail Azure et PowerShell d’analyse du fonctionnement.

1. Rouvrez l’application hello que vous avez créé précédemment dans Visual Studio, ou créez une application à l’aide de hello **avec état Service** modèle Visual Studio.
2. Ouvrez le fichier de Stateful1.cs hello et recherche hello `myDictionary.TryGetValueAsync` appeler Bonjour `RunAsync` (méthode). Vous pouvez voir que cette méthode retourne un `result` que contient hello la valeur actuelle du compteur de hello, car il est logique de clé hello dans cette application est tookeep en cours d’exécution un nombre. S’il s’agissait d’une application réelle, et si un manque de hello du résultat représenté une défaillance, vous souhaiteriez tooflag cet événement.
3. tooreport un événement de contrôle d’intégrité en cas de manque de hello de résultat représente une erreur, ajoutez hello comme suit.
   
    a. Ajouter hello `System.Fabric.Health` espace de noms toohello Stateful1.cs fichier.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Ajouter hello après le code après hello `myDictionary.TryGetValueAsync` appeler
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Nous signalons l’intégrité du réplica, car il provient d’un service avec état. Hello `HealthInformation` paramètre stocke des informations sur le problème d’intégrité hello signalée.
   
    Si vous aviez créé un service sans état, utiliser hello suivant de code
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Si votre service s’exécute avec des privilèges d’administrateur ou si hello cluster n’est pas [sécurisé](service-fabric-cluster-security.md), vous pouvez également utiliser `FabricClient` intégrité tooreport comme indiqué dans hello comme suit.  
   
    a. Créer hello `FabricClient` instance après hello `var myDictionary` déclaration.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Ajouter hello après le code après hello `myDictionary.TryGetValueAsync` appeler.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Nous allons simuler cette panne et la faire apparaître dans les outils de contrôle d’intégrité hello. Échec de hello toosimulate, commentez hello de première ligne dans le contrôle d’intégrité hello signale le code que vous avez ajouté précédemment. Une fois que vous mettez en commentez hello première ligne, code de hello ressemblera à hello l’exemple suivant.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Ce code déclenche rapport d’intégrité de hello chaque fois `RunAsync` s’exécute. Dès que vous modifiez hello, appuyez sur **F5** application hello de toorun.
6. Après que l’application hello est en cours d’exécution, ouvrez le contrôle d’intégrité de Service Fabric Explorer toocheck hello de l’application hello. Cette fois-ci, Service Fabric Explorer montre que l’application hello est défectueux. Il s’agit en raison de l’erreur hello qui a été signalée à partir du code hello que nous avons ajouté précédemment.
   
    ![Application non saine dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Si vous sélectionnez le réplica principal de hello dans arborescence hello de Service Fabric Explorer, vous verrez que **l’état d’intégrité** indique une erreur de trop. Service Fabric Explorer affiche également le rapport d’intégrité de hello détails qui ont été ajoutés toohello `HealthInformation` paramètre dans le code hello. Vous pouvez voir hello même rapports d’intégrité dans PowerShell et hello portail Azure.
   
    ![Intégrité du réplica dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Ce rapport reste dans le Gestionnaire de contrôle d’intégrité hello jusqu'à ce qu’il est remplacé par un autre rapport, ou jusqu'à ce que ce réplica est supprimé. Étant donné que nous n’avez pas défini `TimeToLive` pour ce rapport d’intégrité Bonjour `HealthInformation` de l’objet, les rapports hello n’expire jamais.

Il est recommandé que le contrôle d’intégrité doit être signalé sur un niveau plus granulaire de hello, qui dans ce cas est le réplica de hello. Vous pouvez également signaler l’intégrité sur `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

contrôle d’intégrité tooreport sur `Application`, `DeployedApplication`, et `DeployedServicePackage`, utilisez `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Étapes suivantes
* [Présentation approfondie de l’intégrité de Service Fabric](service-fabric-health-introduction.md)
* [API REST pour les rapports d’intégrité du service](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [API REST pour les rapports d’intégrité de l’application](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

