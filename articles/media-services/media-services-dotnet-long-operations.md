---
title: "aaaPolling opérations longues | Documents Microsoft"
description: "Cette rubrique montre comment les opérations de longue toopoll."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a>Diffusion vidéo en flux continu avec Azure Media Services

## <a name="overview"></a>Vue d'ensemble

Microsoft Azure Media Services propose des API qui envoient des demandes d’opérations de toostart tooMedia Services (par exemple : créer, Démarrer, arrêter ou supprimer un canal). Ces opérations sont des opérations de longue durée.

Hello Media Services .NET SDK fournit des API qui envoie la demande de hello et attendre hello opération toocomplete (en interne, hello API demandent progression de l’opération après certains intervalles). Par exemple, lorsque vous appelez le canal. Start(), méthode hello retourne après le démarrage du canal de hello. Vous pouvez également utiliser la version asynchrone de hello : await de canal. StartAsync() (pour plus d’informations sur le modèle asynchrone basé sur des tâches, consultez [appuyez sur](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). API d’envoyer une demande d’opération et interroge ensuite pour l’état de hello jusqu'à ce que l’opération hello est terminée sont appelées « méthodes d’interrogation ». Ces méthodes (notamment les version Async hello) sont recommandés pour les applications clientes complètes et/ou les services avec état.

Il existe des scénarios dans lesquels une application ne peut pas attendre d’une demande http longue et souhaite que toopoll de progression de l’opération hello manuellement. Un exemple classique serait un navigateur qui interagit avec un service web sans état : lors de la demande de navigateur de hello toocreate un canal, service web de hello initie une opération longue et renvoie hello navigateur de toohello ID opération. Hello navigateur peut alors demander hello web service tooget hello état de l’opération en fonction de hello ID. Hello Media Services .NET SDK fournit des API qui est utiles pour ce scénario. Ces API sont appelées « méthodes sans interrogation ».
« méthodes sans interrogation » Hello ont hello suivant le modèle d’affectation de noms : envoyer*NomOpération*opération (par exemple, SendCreateOperation). Envoyer*NomOpération*hello de retour des méthodes d’opération **IOperation** objet ; hello objet retourné contient des informations qui peuvent être utilisés tootrack hello opération. Envoi de Hello*NomOpération*OperationAsync méthodes retournent **tâche<IOperation>**.

Actuellement, hello suivant les méthodes sans interrogation de prise en charge des classes : **canal**, **StreamingEndpoint**, et **programme**.

toopoll pour l’état de l’opération hello, utilisez hello **GetOperation** méthode sur hello **OperationBaseCollection** classe. Utilisez hello suivant l’état de l’opération hello intervalles toocheck : pour **canal** et **StreamingEndpoint** opérations, utilisez 30 secondes ; pour **programme** opérations, utilisez 10 secondes.

## <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Exemple

Hello exemple suivant définit une classe appelée **ChannelOperations**. Cette définition de classe peut constituer un point de départ pour la définition de classe de votre service Web. Par souci de simplicité, hello exemples suivants utilisent les versions non asynchrones hello de méthodes.

Hello montre également comment les clients hello peuvent utiliser cette classe.

### <a name="channeloperations-class-definition"></a>Définition de la classe ChannelOperations

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a>code client Hello
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

