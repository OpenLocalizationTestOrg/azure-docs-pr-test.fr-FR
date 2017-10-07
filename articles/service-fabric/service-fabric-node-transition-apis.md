---
title: "aaaStart et stop tootest de nœuds de cluster Azure microservices | Documents Microsoft"
description: "Découvrez comment toouse erreur injection tootest une application de Service Fabric par le démarrage et arrêt des nœuds de cluster."
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
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>En remplaçant hello nœud de démarrage et arrêt nœud API avec hello API de Transition de nœud

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>Que hello nœud d’arrêter et démarrer les API de nœud ?

Hello arrêter les API de nœud (géré : [StopNodeAsync()][stopnode], PowerShell : [Stop-ServiceFabricNode][stopnodeps]) s’arrête à un nœud de Service Fabric.  Un nœud de Service Fabric est le processus, pas un ordinateur virtuel ou un ordinateur : hello machine virtuelle ou ordinateur sera toujours être en cours d’exécution.  Pour rest hello du document de hello « nœud » signifie le nœud Service Fabric.  L’arrêt d’un nœud les place dans un *arrêté* état où il n’est pas membre du cluster de hello et ne peut pas héberger les services, instaurant ainsi une *vers le bas* nœud.  Cela est utile pour l’injection d’erreurs dans hello système tootest votre application.  Hello démarrer les API de nœud (géré : [StartNodeAsync()][startnode], PowerShell : [Start-ServiceFabricNode][startnodeps]]) inverse hello arrêter les API de nœud,  ce qui amène hello nœud tooa retour un état normal.

## <a name="why-are-we-replacing-these"></a>Pourquoi remplaçons-nous ces API ?

Comme décrit précédemment, un *arrêté* nœud de Service Fabric est un nœud a été volontairement à l’aide de hello arrêter les API de nœud.  A *vers le bas* nœud est un nœud est arrêté pour une raison quelconque (par exemple hello ordinateur ou la machine virtuelle est désactivée).  Avec hello arrêter les API de nœud, système de hello n’expose pas toodifferentiate d’informations entre *arrêté* nœuds et *vers le bas* nœuds.

De plus, certaines erreurs renvoyées par ces API ne sont pas aussi descriptives qu’elles pourraient l’être.  Par exemple, appeler hello d’arrêter les API de nœud sur un déjà *arrêté* nœud retournera une erreur de hello *InvalidAddress*.  Cette expérience pourrait être améliorée.

En outre, durée hello pour qu'un nœud est arrêté est « infinite » jusqu'à hello que démarrer les API de nœud est appelé.  Nous avons découvert que cela pouvait provoquer des problèmes et des erreurs.  Par exemple, nous avons vu où un utilisateur appelé hello arrêter les API de nœud sur un nœud, puis souvenez plus de problèmes.  Une version ultérieure, il était difficile de savoir si le nœud de hello était *vers le bas* ou *arrêté*.


## <a name="introducing-hello-node-transition-apis"></a>Présentation de hello API de Transition de nœud

Nous avons résolu les problèmes ci-dessus dans un nouvel ensemble d’API.  Hello nouvelle Transition de nœud API (géré : [StartNodeTransitionAsync()][snt]) peut être utilisée tootransition un tooa de nœud de Service Fabric *arrêté* état ou tootransition il à partir d’un *arrêté* tooa état normal d’état.  Veuillez noter que hello « Start » dans le nom hello Hello API ne fait pas référence à un nœud de toostarting.  Il fait référence à une opération asynchrone, que le système de hello exécutera tootransition hello nœud tooeither de toobeginning *arrêté* ou en état démarré.

**Utilisation**

Si hello API de Transition de nœud ne lève pas une exception lorsqu’elle est appelée, puis hello système a accepté l’opération asynchrone de hello et il exécutera.  Un appel réussi n’implique pas l’opération de hello est fini de s’exécuter.  tooget plus d’informations sur l’état actuel de hello d’opération hello, appel hello nœud Transition progression API (géré : [GetNodeTransitionProgressAsync()][gntp]) avec le guid hello utilisé lors de l’appel de nœud API de transition pour cette opération.  Hello nœud Transition progression de l’API retourne un objet NodeTransitionProgress.  Propriété d’état de cet objet spécifie l’état actuel de hello d’opération de hello.  Si l’état hello est « Running » puis hello exécution d’une opération.  Si elle est terminée, l’opération de hello est terminé sans erreur.  Si elle est défaillante, un problème survenu l’exécution d’opération de hello.  Exception de la propriété du résultat de Hello propriété indique quel hello émettre était.  Consultez https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate pour plus d’informations sur la propriété d’état hello et hello « Utilisation de l’exemple » ci-dessous pour des exemples de code.


**Faisant la distinction entre un nœud arrêté et un nœud en panne** si un nœud est *arrêté* à l’aide de hello nœud Transition API, sortie hello d’une requête de nœud (géré : [GetNodeListAsync()] [ nodequery], PowerShell : [Get-ServiceFabricNode][nodequeryps]) indiquera que ce nœud possède un *IsStopped* valeur de propriété de la valeur true.  Notez cette valeur diffère de la valeur hello hello *NodeStatus* propriété, qui indiquera *vers le bas*.  Si hello *NodeStatus* propriété a la valeur *vers le bas*, mais *IsStopped* est false, le nœud de hello a été pas arrêté à l’aide d’API de Transition de nœud de hello et est  *Vers le bas* en raison d’une autre raison.  Si hello *IsStopped* propriété est true et hello *NodeStatus* propriété *vers le bas*, puis il a été arrêté à l’aide de hello API de Transition de nœud.

Démarrer un *arrêté* nœud à l’aide des API de Transition de nœud de hello retournera il toofunction en tant que membre du cluster de hello normal à nouveau.  Hello sortie de requête de nœud hello API affichera *IsStopped* comme false, et *NodeStatus* en tant que quelque chose qui n’est pas interrompue (par exemple, vers le haut).


**Durée** lors de l’utilisation des API de Transition de nœud de hello toostop un nœud, un des hello paramètres obligatoires *stopNodeDurationInSeconds*, représente hello temps dans le nœud de hello secondes tookeep  *arrêté*.  Cette valeur doit être Bonjour plage ayant un minimum de 600 et un maximum de 14400 autorisée.  Une fois ce délai expiré, nœud de hello va redémarrer elle-même en état automatiquement.  Consultez tooSample 1 ci-dessous pour obtenir un exemple d’utilisation.

> [!WARNING]
> Évitez de combiner des API de Transition de nœud et hello nœud d’arrêter et démarrer les API de nœud.  recommandation de Hello est trop utiliser hello API de Transition de nœud.  > Si un nœud a déjà été arrêtée par le biais de hello arrêter les API de nœud, il doit être démarré à l’aide de hello démarrer les API de nœud tout d’abord avant d’utiliser hello > API de Transition de nœud.

> [!WARNING]
> API de Transition nœud plusieurs appels ne peut pas être effectués sur hello même nœud en parallèle.  Dans ce cas, hello nœud Transition API sera > lever une FabricException avec une valeur de la propriété ErrorCode de NodeTransitionInProgress.  Une fois qu’une transition de nœud sur un nœud spécifique a > été démarré, vous devez patienter jusqu'à ce que l’opération de hello atteigne un état terminal (terminé, Faulted ou ForceCancelled) avant de démarrer un > nouvelle transition sur hello que même nœud.  Les appels de transition de nœud parallèles sur des nœuds différents sont autorisés.


#### <a name="sample-usage"></a>Exemple d’utilisation


**Exemple 1** -hello suivant l’exemple hello nœud Transition API toostop un nœud.

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**Exemple 2** - hello suivant l’exemple démarre un *arrêté* nœud.  Il utilise des méthodes d’assistance à partir de l’exemple de première hello.

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**Exemple 3** - hello exemple suivant illustre une utilisation incorrecte.  Cette utilisation est incorrecte, car hello *stopDurationInSeconds* qu’elle fournit est supérieure à la plage autorisée de hello.  Depuis StartNodeTransitionAsync() échoue avec une erreur irrécupérable, opération de hello n’a pas été acceptée et API de progression hello ne doit pas être appelée.  Cet exemple utilise des méthodes d’assistance à partir de l’exemple de première hello.

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

**Exemple 4** - hello exemple suivant montre les informations d’erreur hello qui seront retournées par hello nœud Transition progression API lors de l’opération hello initiée par hello API de Transition de nœud est acceptée, mais échoue ultérieurement lors de l’exécution.  Dans les cas de hello, elle échoue car hello nœud Transition API tente toostart un nœud qui n’existe pas.  Cet exemple utilise des méthodes d’assistance à partir de l’exemple de première hello.

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
