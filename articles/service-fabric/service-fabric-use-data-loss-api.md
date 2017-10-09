---
title: "aaaHow tooInvoke perte de données sur les Services de Fabric Service | Documents Microsoft"
description: "Décrit comment toouse hello une perte de données api"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a>Comment tooInvoke une perte de données sur les Services
> [!WARNING]
> Ce document décrit comment toocause une perte de données dans vos services et doit être utilisée avec précaution.
> 
> 

## <a name="introduction"></a>Introduction
Vous pouvez appeler une perte de données sur une partition de votre service Service Fabric en appelant StartPartitionDataLossAsync().  Cette api utilise hello injection d’erreurs et d’Analysis Service tooperform hello toocause données perte conditions de travail.

## <a name="using-hello-fault-injection-and-analysis-service"></a>À l’aide de hello injection d’erreurs et d’Analysis Services
Hello injection d’erreurs et d’Analysis Services prend en charge actuellement hello suivant d’API dans le graphique de hello ci-dessous.  à droite de Hello du graphique de hello montre l’applet de commande PowerShell correspondante hello.  Veuillez consultez la documentation du msdn toohello sur chaque API pour plus d’informations sur chacun d’eux.

| C# API | Applet de commande PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Vue d’ensemble conceptuelle de l’exécution d’une commande
Hello d’injection d’erreurs et d’Analysis Services utilise un modèle asynchrone, où vous démarrez hello de commande avec une API, appelle l’API de « Start » tooas hello dans ce document, puis vérifie hello progression de cette commande à l’aide d’une API « GetProgress » jusqu'à ce qu’il a atteint un terminal état, ou jusqu'à ce que vous l’annuler.
toostart une commande, appeler des API de « Start » de hello pour les API correspondantes hello.  Cette API retourne lorsque hello injection d’erreurs et d’Analysis Services a accepté la demande de hello.  Toutefois, elle n’indique pas jusqu’où une commande est exécutée, ou si elle a déjà démarré.  En cours de toocheck de commande d’une commande, appelez hello « GetProgress « API correspondant toohello « Démarrer » des API appelée précédemment.  Hello « GetProgress « API retournera un objet indiquant l’état actuel de hello de commande hello à l’intérieur de sa propriété d’état.  La commande s’exécute indéfiniment jusqu'à ce que :

1. Elle se termine correctement.  Si vous appelez « GetProgress » sur ce dernier dans ce cas, l’état de l’objet de progression hello sera terminée.
2. Elle rencontre une erreur irrécupérable.  Si vous appelez « GetProgress » sur ce dernier dans ce cas, état de l’objet de progression hello générera une erreur
3. Vous l’annulez via hello [CancelTestCommandAsync] [ cancel] API, ou [Stop-ServiceFabricTestCommand] [ cancelps] applet de commande PowerShell.  Si vous appelez « GetProgress » sur ce dernier dans ce cas, hello état de progression de l’objet sera soit annulé ou ForceCancelled, selon une toothat argument API.  Consultez la documentation de hello pour [CancelTestCommandAsync] [ cancel] pour plus d’informations.

## <a name="details-of-running-a-command"></a>Détails de l’exécution d’une commande
Dans l’ordre toostart une commande, appelez hello API de démarrer avec des arguments de hello attendu.  Toutes les API Start ont un argument Guid nommé operationId.  Vous devez effectuer le suivi des argument operationId de hello, car il est utilisé progression tootrack de cette commande.  Cela doit être passé dans hello « GetProgress « API en cours de tootrack d’ordre de la commande hello.  Hello operationId doit être unique.

Après avoir correctement appelé hello API Démarrer, hello GetProgress API doit être appelée dans une boucle jusqu'à ce que hello retourné progression propriété State de l’objet est terminée.  Toutes les commandes [FabricTransientException][fte] et OperationCanceledException doivent être relancées.
Lors de la commande hello a atteint un état terminal (terminé, Faulted ou annulée), hello retourné la propriété Result de l’objet de progression aura plus d’informations.  Si l’état de hello est terminée, Result.SelectedPartition.PartitionId contient les id de partition hello qui a été sélectionné.  La valeur Result.Exception sera nulle.  Si l’état de hello est défectueux, Result.Exception aura hello de raison hello injection d’erreurs et de la commande hello de Service a généré une erreur d’analyse.  Result.SelectedPartition.PartitionId aura un id de partition hello qui a été sélectionné.  Dans certaines situations, commande hello ne peut-être pas été suffisamment loin toochoose une partition.  Dans ce cas, hello PartitionId est égal à 0.  Si l’état de hello est annulée, Result.Exception sera null.  Comme hello Faulted cas, Result.SelectedPartition.PartitionId aura un id de partition hello qui a été choisi, mais si la commande hello n'a pas traité suffisamment loin toodo par conséquent, il est égal à 0.  Reportez-vous également exemple toohello ci-dessous.

Hello exemple de code ci-dessous montre comment toostart vérifier puis cours sur une perte de données toocause commande sur une partition spécifique.

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

exemple Hello ci-dessous montre comment toouse hello PartitionSelector toochoose une partition aléatoire d’un service spécifié :

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a>Historique et troncation
Après qu’une commande a atteint un état terminal, ses métadonnées restent Bonjour injection d’erreurs et Analysis Services pour un certain temps, avant d’être supprimé toosave espace.  Si « GetProgress » est appelée à l’aide d’operationId hello d’une commande une fois qu’il a été supprimée, elle retournera une FabricException avec un code d’erreur de KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
