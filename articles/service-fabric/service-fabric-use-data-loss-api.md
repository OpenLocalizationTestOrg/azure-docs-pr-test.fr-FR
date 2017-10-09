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
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="2d119-103">Comment tooInvoke une perte de données sur les Services</span><span class="sxs-lookup"><span data-stu-id="2d119-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="2d119-104">Ce document décrit comment toocause une perte de données dans vos services et doit être utilisée avec précaution.</span><span class="sxs-lookup"><span data-stu-id="2d119-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="2d119-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="2d119-105">Introduction</span></span>
<span data-ttu-id="2d119-106">Vous pouvez appeler une perte de données sur une partition de votre service Service Fabric en appelant StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="2d119-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="2d119-107">Cette api utilise hello injection d’erreurs et d’Analysis Service tooperform hello toocause données perte conditions de travail.</span><span class="sxs-lookup"><span data-stu-id="2d119-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="2d119-108">À l’aide de hello injection d’erreurs et d’Analysis Services</span><span class="sxs-lookup"><span data-stu-id="2d119-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="2d119-109">Hello injection d’erreurs et d’Analysis Services prend en charge actuellement hello suivant d’API dans le graphique de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2d119-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="2d119-110">à droite de Hello du graphique de hello montre l’applet de commande PowerShell correspondante hello.</span><span class="sxs-lookup"><span data-stu-id="2d119-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="2d119-111">Veuillez consultez la documentation du msdn toohello sur chaque API pour plus d’informations sur chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="2d119-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="2d119-112">C# API</span><span class="sxs-lookup"><span data-stu-id="2d119-112">C# API</span></span> | <span data-ttu-id="2d119-113">Applet de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d119-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="2d119-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="2d119-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="2d119-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="2d119-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="2d119-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="2d119-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="2d119-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="2d119-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="2d119-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="2d119-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="2d119-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="2d119-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="2d119-120">Vue d’ensemble conceptuelle de l’exécution d’une commande</span><span class="sxs-lookup"><span data-stu-id="2d119-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="2d119-121">Hello d’injection d’erreurs et d’Analysis Services utilise un modèle asynchrone, où vous démarrez hello de commande avec une API, appelle l’API de « Start » tooas hello dans ce document, puis vérifie hello progression de cette commande à l’aide d’une API « GetProgress » jusqu'à ce qu’il a atteint un terminal état, ou jusqu'à ce que vous l’annuler.</span><span class="sxs-lookup"><span data-stu-id="2d119-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="2d119-122">toostart une commande, appeler des API de « Start » de hello pour les API correspondantes hello.</span><span class="sxs-lookup"><span data-stu-id="2d119-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="2d119-123">Cette API retourne lorsque hello injection d’erreurs et d’Analysis Services a accepté la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="2d119-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="2d119-124">Toutefois, elle n’indique pas jusqu’où une commande est exécutée, ou si elle a déjà démarré.</span><span class="sxs-lookup"><span data-stu-id="2d119-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="2d119-125">En cours de toocheck de commande d’une commande, appelez hello « GetProgress « API correspondant toohello « Démarrer » des API appelée précédemment.</span><span class="sxs-lookup"><span data-stu-id="2d119-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="2d119-126">Hello « GetProgress « API retournera un objet indiquant l’état actuel de hello de commande hello à l’intérieur de sa propriété d’état.</span><span class="sxs-lookup"><span data-stu-id="2d119-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="2d119-127">La commande s’exécute indéfiniment jusqu'à ce que :</span><span class="sxs-lookup"><span data-stu-id="2d119-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="2d119-128">Elle se termine correctement.</span><span class="sxs-lookup"><span data-stu-id="2d119-128">It completes successfully.</span></span>  <span data-ttu-id="2d119-129">Si vous appelez « GetProgress » sur ce dernier dans ce cas, l’état de l’objet de progression hello sera terminée.</span><span class="sxs-lookup"><span data-stu-id="2d119-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="2d119-130">Elle rencontre une erreur irrécupérable.</span><span class="sxs-lookup"><span data-stu-id="2d119-130">It encounters a fatal error.</span></span>  <span data-ttu-id="2d119-131">Si vous appelez « GetProgress » sur ce dernier dans ce cas, état de l’objet de progression hello générera une erreur</span><span class="sxs-lookup"><span data-stu-id="2d119-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="2d119-132">Vous l’annulez via hello [CancelTestCommandAsync] [ cancel] API, ou [Stop-ServiceFabricTestCommand] [ cancelps] applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d119-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="2d119-133">Si vous appelez « GetProgress » sur ce dernier dans ce cas, hello état de progression de l’objet sera soit annulé ou ForceCancelled, selon une toothat argument API.</span><span class="sxs-lookup"><span data-stu-id="2d119-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="2d119-134">Consultez la documentation de hello pour [CancelTestCommandAsync] [ cancel] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2d119-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="2d119-135">Détails de l’exécution d’une commande</span><span class="sxs-lookup"><span data-stu-id="2d119-135">Details of Running a Command</span></span>
<span data-ttu-id="2d119-136">Dans l’ordre toostart une commande, appelez hello API de démarrer avec des arguments de hello attendu.</span><span class="sxs-lookup"><span data-stu-id="2d119-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="2d119-137">Toutes les API Start ont un argument Guid nommé operationId.</span><span class="sxs-lookup"><span data-stu-id="2d119-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="2d119-138">Vous devez effectuer le suivi des argument operationId de hello, car il est utilisé progression tootrack de cette commande.</span><span class="sxs-lookup"><span data-stu-id="2d119-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="2d119-139">Cela doit être passé dans hello « GetProgress « API en cours de tootrack d’ordre de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="2d119-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="2d119-140">Hello operationId doit être unique.</span><span class="sxs-lookup"><span data-stu-id="2d119-140">hello operationId must be unique.</span></span>

<span data-ttu-id="2d119-141">Après avoir correctement appelé hello API Démarrer, hello GetProgress API doit être appelée dans une boucle jusqu'à ce que hello retourné progression propriété State de l’objet est terminée.</span><span class="sxs-lookup"><span data-stu-id="2d119-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="2d119-142">Toutes les commandes [FabricTransientException][fte] et OperationCanceledException doivent être relancées.</span><span class="sxs-lookup"><span data-stu-id="2d119-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="2d119-143">Lors de la commande hello a atteint un état terminal (terminé, Faulted ou annulée), hello retourné la propriété Result de l’objet de progression aura plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2d119-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="2d119-144">Si l’état de hello est terminée, Result.SelectedPartition.PartitionId contient les id de partition hello qui a été sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2d119-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="2d119-145">La valeur Result.Exception sera nulle.</span><span class="sxs-lookup"><span data-stu-id="2d119-145">Result.Exception will be null.</span></span>  <span data-ttu-id="2d119-146">Si l’état de hello est défectueux, Result.Exception aura hello de raison hello injection d’erreurs et de la commande hello de Service a généré une erreur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="2d119-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="2d119-147">Result.SelectedPartition.PartitionId aura un id de partition hello qui a été sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2d119-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="2d119-148">Dans certaines situations, commande hello ne peut-être pas été suffisamment loin toochoose une partition.</span><span class="sxs-lookup"><span data-stu-id="2d119-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="2d119-149">Dans ce cas, hello PartitionId est égal à 0.</span><span class="sxs-lookup"><span data-stu-id="2d119-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="2d119-150">Si l’état de hello est annulée, Result.Exception sera null.</span><span class="sxs-lookup"><span data-stu-id="2d119-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="2d119-151">Comme hello Faulted cas, Result.SelectedPartition.PartitionId aura un id de partition hello qui a été choisi, mais si la commande hello n'a pas traité suffisamment loin toodo par conséquent, il est égal à 0.</span><span class="sxs-lookup"><span data-stu-id="2d119-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="2d119-152">Reportez-vous également exemple toohello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2d119-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="2d119-153">Hello exemple de code ci-dessous montre comment toostart vérifier puis cours sur une perte de données toocause commande sur une partition spécifique.</span><span class="sxs-lookup"><span data-stu-id="2d119-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

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

<span data-ttu-id="2d119-154">exemple Hello ci-dessous montre comment toouse hello PartitionSelector toochoose une partition aléatoire d’un service spécifié :</span><span class="sxs-lookup"><span data-stu-id="2d119-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

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

## <a name="history-and-truncation"></a><span data-ttu-id="2d119-155">Historique et troncation</span><span class="sxs-lookup"><span data-stu-id="2d119-155">History and Truncation</span></span>
<span data-ttu-id="2d119-156">Après qu’une commande a atteint un état terminal, ses métadonnées restent Bonjour injection d’erreurs et Analysis Services pour un certain temps, avant d’être supprimé toosave espace.</span><span class="sxs-lookup"><span data-stu-id="2d119-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="2d119-157">Si « GetProgress » est appelée à l’aide d’operationId hello d’une commande une fois qu’il a été supprimée, elle retournera une FabricException avec un code d’erreur de KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="2d119-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
