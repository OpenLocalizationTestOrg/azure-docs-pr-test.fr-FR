---
title: "Comment appeler une perte des données sur des services Service Fabric | Microsoft Docs"
description: "Explique comment utiliser l’API de perte des données"
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
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="f7239-103">Comment appeler la perte des données sur des services</span><span class="sxs-lookup"><span data-stu-id="f7239-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="f7239-104">Ce document décrivent comment entraîner une perte de données dans vos services et doit être utilisé avec précaution.</span><span class="sxs-lookup"><span data-stu-id="f7239-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="f7239-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="f7239-105">Introduction</span></span>
<span data-ttu-id="f7239-106">Vous pouvez appeler une perte de données sur une partition de votre service Service Fabric en appelant StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="f7239-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="f7239-107">Cette API utilise le service d’injection et d’analyse des erreurs pour provoquer des conditions de perte de données.</span><span class="sxs-lookup"><span data-stu-id="f7239-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="f7239-108">Utilisation du service d’injection et d’analyse des erreurs</span><span class="sxs-lookup"><span data-stu-id="f7239-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="f7239-109">Le service d’injection et d’analyse des erreurs prend actuellement en charge les API suivantes, comme indiqué dans le graphique ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f7239-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="f7239-110">Le côté droit du graphique montre l’applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7239-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="f7239-111">Reportez-vous à la documentation msdn de chaque API pour plus d’informations sur chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="f7239-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="f7239-112">C# API</span><span class="sxs-lookup"><span data-stu-id="f7239-112">C# API</span></span> | <span data-ttu-id="f7239-113">Applet de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7239-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="f7239-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="f7239-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="f7239-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="f7239-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="f7239-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="f7239-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="f7239-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="f7239-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="f7239-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="f7239-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="f7239-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="f7239-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="f7239-120">Vue d’ensemble conceptuelle de l’exécution d’une commande</span><span class="sxs-lookup"><span data-stu-id="f7239-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="f7239-121">Le service d’injection et d’analyse des erreurs utilise un modèle asynchrone dans lequel vous démarrez la commande avec une API, appelée API « Start » dans ce document, puis vérifie la progression de cette commande à l’aide d’une API « GetProgress » jusqu'à ce qu’elle atteigne un état terminal, ou jusqu'à ce que vous l’annuliez.</span><span class="sxs-lookup"><span data-stu-id="f7239-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="f7239-122">Pour démarrer une commande, appelez l’API « Start » pour l’API correspondante.</span><span class="sxs-lookup"><span data-stu-id="f7239-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="f7239-123">Cette API est renvoyée lorsque le service d’injection et d’analyse des erreurs a accepté la demande.</span><span class="sxs-lookup"><span data-stu-id="f7239-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="f7239-124">Toutefois, elle n’indique pas jusqu’où une commande est exécutée, ou si elle a déjà démarré.</span><span class="sxs-lookup"><span data-stu-id="f7239-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="f7239-125">Pour vérifier la progression d’une commande, appelez l’API qui correspond à l’API « Start » précédemment appelée « GetProgress ».</span><span class="sxs-lookup"><span data-stu-id="f7239-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="f7239-126">L’API « GetProgress » renvoie un objet qui indique l’état actuel de la commande à l’intérieur de sa propriété d’état (State).</span><span class="sxs-lookup"><span data-stu-id="f7239-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="f7239-127">La commande s’exécute indéfiniment jusqu'à ce que :</span><span class="sxs-lookup"><span data-stu-id="f7239-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="f7239-128">Elle se termine correctement.</span><span class="sxs-lookup"><span data-stu-id="f7239-128">It completes successfully.</span></span>  <span data-ttu-id="f7239-129">Si vous appelez « GetProgress » sur cette API dans ce cas, l’état de progression de l’objet affiche Completed (terminé).</span><span class="sxs-lookup"><span data-stu-id="f7239-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="f7239-130">Elle rencontre une erreur irrécupérable.</span><span class="sxs-lookup"><span data-stu-id="f7239-130">It encounters a fatal error.</span></span>  <span data-ttu-id="f7239-131">Si vous appelez « GetProgress » sur cette API dans ce cas, l’état de progression de l’objet affiche Faulted (défaillance)</span><span class="sxs-lookup"><span data-stu-id="f7239-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="f7239-132">Pour l’annuler, utilisez l’API [CancelTestCommandAsync][cancel] ou l’applet de commande PowerShell [Stop-ServiceFabricTestCommand][cancelps].</span><span class="sxs-lookup"><span data-stu-id="f7239-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="f7239-133">Si vous appelez « GetProgress » sur cette API dans ce cas, l’état de progression de l’objet affiche Cancelled (annulé) ou ForceCancelled (annulation forcée), selon un argument de cette API.</span><span class="sxs-lookup"><span data-stu-id="f7239-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="f7239-134">Consultez la documentation de [CancelTestCommandAsync][cancel] pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="f7239-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="f7239-135">Détails de l’exécution d’une commande</span><span class="sxs-lookup"><span data-stu-id="f7239-135">Details of Running a Command</span></span>
<span data-ttu-id="f7239-136">Pour démarrer une commande, appelez l’API Start avec les arguments attendus.</span><span class="sxs-lookup"><span data-stu-id="f7239-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="f7239-137">Toutes les API Start ont un argument Guid nommé operationId.</span><span class="sxs-lookup"><span data-stu-id="f7239-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="f7239-138">Vous devriez effectuer le suivi de l’argument operationId car il est utilisé pour suivre la progression de cette commande.</span><span class="sxs-lookup"><span data-stu-id="f7239-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="f7239-139">Cet argument doit être passée à l’API « GetProgress » afin de suivre la progression de la commande.</span><span class="sxs-lookup"><span data-stu-id="f7239-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="f7239-140">La valeur operationId doit être unique.</span><span class="sxs-lookup"><span data-stu-id="f7239-140">The operationId must be unique.</span></span>

<span data-ttu-id="f7239-141">Après l’appel réussi de l’API Start, l’API GetProgress devrait être appelée dans une boucle jusqu'à ce que la propriété d’état de progression de l’objet retourné affiche Completed (Terminé).</span><span class="sxs-lookup"><span data-stu-id="f7239-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="f7239-142">Toutes les commandes [FabricTransientException][fte] et OperationCanceledException doivent être relancées.</span><span class="sxs-lookup"><span data-stu-id="f7239-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="f7239-143">Lorsque la commande a atteint un état terminal (Completed, Faulted ou Cancelled), la propriété Result de progression de l’objet retourné aura plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f7239-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="f7239-144">Si l’état affiche Completed (terminé), Result.SelectedPartition.PartitionId contient l’ID de partition qui a été sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f7239-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="f7239-145">La valeur Result.Exception sera nulle.</span><span class="sxs-lookup"><span data-stu-id="f7239-145">Result.Exception will be null.</span></span>  <span data-ttu-id="f7239-146">Si l’état indique Faulted, Result.Exception indiquera la raison pour laquelle le service d’injection et d’analyse des erreurs a généré une erreur de la commande.</span><span class="sxs-lookup"><span data-stu-id="f7239-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="f7239-147">Result.SelectedPartition.PartitionId affichera l’ID de partition qui a été sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f7239-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="f7239-148">Dans certains cas, la commande n’a peut-être pas été suffisamment loin pour choisir une partition.</span><span class="sxs-lookup"><span data-stu-id="f7239-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="f7239-149">Dans ce cas, la valeur PartitionId sera 0.</span><span class="sxs-lookup"><span data-stu-id="f7239-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="f7239-150">Si l’état affiche Cancelled (annulé), la valeur Result.Exception est nulle.</span><span class="sxs-lookup"><span data-stu-id="f7239-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="f7239-151">Comme pour l’état Faulted (défaillance), Result.SelectedPartition.PartitionId affichera l’ID de partition qui a été choisi, mais si la commande n’a pas été suffisamment loin pour cela, la valeur sera 0.</span><span class="sxs-lookup"><span data-stu-id="f7239-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="f7239-152">Reportez-vous aussi à l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f7239-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="f7239-153">L’exemple de code ci-dessous montre comment démarrer puis vérifier la progression d’une commande pour provoquer une perte de données sur une partition spécifique.</span><span class="sxs-lookup"><span data-stu-id="f7239-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

<span data-ttu-id="f7239-154">L’exemple ci-dessous montre comment utiliser PartitionSelector pour choisir une partition aléatoire d’un service spécifié :</span><span class="sxs-lookup"><span data-stu-id="f7239-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

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
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

## <a name="history-and-truncation"></a><span data-ttu-id="f7239-155">Historique et troncation</span><span class="sxs-lookup"><span data-stu-id="f7239-155">History and Truncation</span></span>
<span data-ttu-id="f7239-156">Dès qu’une commande a atteint un état terminal, ses métadonnées resteront dans le service d’injection et d’analyse des erreurs pour un certain temps, avant d’être supprimées pour économiser de l’espace.</span><span class="sxs-lookup"><span data-stu-id="f7239-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="f7239-157">Si « GetProgress » est appelée à l’aide de la valeur operationId d’une commande après avoir été supprimée, elle retournera une valeur FabricException avec un code d’erreur KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="f7239-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
