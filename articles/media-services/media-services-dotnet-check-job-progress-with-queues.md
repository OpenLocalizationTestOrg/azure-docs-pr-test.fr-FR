---
title: "aaaUse file d’attente Azure storage toomonitor Media Services notifications du travail avec .NET | Documents Microsoft"
description: "Découvrez comment toomonitor de stockage toouse file d’attente Azure Media Services de notifications de la tâche. exemple de code Hello est écrite en c# et utilise hello Media Services SDK pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a>Utiliser des notifications de travaux de file d’attente Azure storage toomonitor Media Services avec .NET
Lorsque vous exécutez des tâches d’encodage, vous nécessitent souvent une progression du travail tootrack moyen. Vous pouvez configurer des notifications de Media Services toodeliver trop[stockage de file d’attente Azure](../storage/storage-dotnet-how-to-use-queues.md). Vous pouvez surveiller la progression du travail par les notifications de mise en route de hello stockage de file d’attente. 

Messages remis tooQueue stockage est accessible à partir de n’importe où dans Bonjour. Hello architecture de messagerie de stockage de file d’attente est fiable et évolutive. L’interrogation du Stockage File d’attente pour les messages est préférable aux autres méthodes.

Un scénario courant pour les notifications de Services tooMedia écoute est si vous développez un système de gestion de contenu qui doit tooperform certaines tâches supplémentaires après un travail d’encodage se termine (par exemple, l’étape suivante de tootrigger hello dans un flux de travail, ou toopublish contenu).

Cette rubrique montre comment les messages de notification de tooget à partir du stockage de file d’attente.  

## <a name="considerations"></a>Considérations
Considérez les éléments suivants de hello lors du développement d’applications de Media Services qui utilisent le stockage de file d’attente :

* Le Stockage File d’attente ne garantit pas une remise dans l’ordre d’arrivée (FIFO). Pour plus d'informations, consultez [Files d'attente Azure et files d'attente Azure Service Bus - comparaison et différences](https://msdn.microsoft.com/library/azure/hh767287.aspx).
* Le Stockage File d’attente n’est pas un service push. Vous avez la file d’attente de toopoll hello.
* Le nombre de files d’attente est illimité. Pour plus d'informations, consultez [API REST du service de file d'attente](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).
* Stockage de file d’attente a certaines limites et certaines toobe spécificités prenant en charge de. Celles-ci sont décrites dans [Files d’attente Azure et files d’attente Azure Service Bus - comparaison et différences](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).

## <a name="net-code-example"></a>Exemple de code .NET

exemple de code Hello dans cette section hello suivant :

1. Définit hello **EncodingJobMessage** classe qui mappe le format de message de notification toohello. code de Hello désérialise les messages reçus à partir de la file d’attente hello dans les objets de hello **EncodingJobMessage** type.
2. Charges hello Media Services et les informations de compte de stockage du fichier app.config de hello. exemple de code Hello utilise cette hello de toocreate informations **CloudMediaContext** et **CloudQueue** objets.
3. Crée une file d’attente hello qui reçoit les messages de notification sur hello travail d’encodage.
4. Crée la notification hello point de terminaison qui est mappé à la file d’attente de toohello.
5. Attache le travail de toohello de point de terminaison de notification hello et soumet le travail d’encodage hello. Vous pouvez avoir plusieurs notification des points de terminaison attachés tooa travail.
6. Passe **NotificationJobState.FinalStatesOnly** toohello **AddNew** (méthode). (Dans cet exemple, nous intéresse uniquement les États finaux de traitement hello.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. Si vous passez **NotificationJobState.All**, vous obtenez tous hello suivant des notifications de changement d’état : en file d’attente, planifié, le traitement et terminé. Toutefois, comme indiqué précédemment, le Stockage File d’attente ne garantit pas une remise dans l’ordre d’arrivée. les messages tooorder, utilisez hello **Timestamp** propriété (définie sur hello **EncodingJobMessage** type dans l’exemple hello ci-dessous). Les messages en double sont possibles. toocheck les doublons, utilisez hello **propriété ETag** (défini sur hello **EncodingJobMessage** type). Il se peut également que certaines notifications de modification d’état soient ignorées.
8. Attend que hello travail tooget toohello terminé état par la vérification de la file d’attente hello toutes les 10 secondes. Supprimer les messages une fois qu’ils ont été traités.
9. Supprime la file d’attente hello et le point de terminaison de notification hello.

> [!NOTE]
> Bonjour toomonitor recommandé pour que l’état d’un travail est en écoute les messages toonotification, comme indiqué dans hello l’exemple suivant.
>
> Vous pourriez également vérifier sur l’état d’un travail à l’aide de hello **IJob.State** propriété.  Un message de notification sur l’achèvement d’une tâche peut arrivent avant d’état de hello sur **IJob** est défini trop**terminé**. Hello **IJob.State** propriété reflète état précis de hello avec un léger retard.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio

1. Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 
2. Créer un nouveau dossier (dossier peut être n’importe où sur votre disque local) et copiez le fichier .mp4 que vous voulez tooencode et flux de données ou téléchargez progressivement. Dans cet exemple, le chemin d’accès de hello « C:\Media » est utilisé.

### <a name="code"></a>Code

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want tooget messages from hello queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display hello message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete hello message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
Bonjour précédent exemple produit hello suivant de sortie. Vos valeurs varieront.

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
