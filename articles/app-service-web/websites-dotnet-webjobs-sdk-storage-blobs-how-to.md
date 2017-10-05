---
title: "Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs"
description: "Découvrez comment utiliser le stockage d’objets blob Microsoft Azure avec le Kit de développement logiciel (SDK) WebJobs. Déclenchez un processus lorsqu’un nouvel objet blob apparaît dans un conteneur et gérez les « objets blob incohérents »."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a>Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs
## <a name="overview"></a>Vue d’ensemble
Ce guide fournit des exemples de code c# qui montrent comment déclencher un processus pendant la création ou la mise à jour d’un objet blob Azure. Les exemples de code utilisent le [Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk.md) version 1.x.

Pour obtenir des exemples de code vous indiquant comment créer des objets blob, consultez la rubrique [Utilisation du stockage de file d’attente Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Ce guide suppose que vous savez [comment créer un projet WebJob dans Visual Studio avec des chaînes de connexion qui pointent vers votre compte de stockage](websites-dotnet-webjobs-sdk-get-started.md) ou [plusieurs comptes de stockage](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a> Déclenchement d’une fonction lors de la création ou de la mise à jour d’un objet blob
Cette section vous indique comment utiliser l’attribut `BlobTrigger` . 

> [!NOTE]
> Le kit de développement logiciel (SDK) WebJobs analyse les fichiers journaux pour surveiller les objets blob qui ont été créés ou modifiés. Ce processus ne se déroule pas en temps réel ; il se peut qu’une fonction ne se déclenche que quelques minutes ou plus après la création de l’objet blob. En outre, des [journaux de stockage sont créés sur la base du « meilleur effort »](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; il n’est pas garanti que tous les événements soient capturés. Dans certaines conditions, des journaux peuvent être omis. Si les limitations relatives à la vitesse et à la fiabilité des déclenchements d’objets blob ne sont pas acceptables pour votre application, il est conseillé d’utiliser la méthode de création d’un message de file d’attente lorsque vous créez l’objet blob et l’attribut [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) à la place de l’attribut `BlobTrigger` sur la fonction qui traite l’objet blob.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Espace réservé unique pour le nom d’objet blob avec extension
L’exemple de code suivant copie les objets blob de texte qui apparaissent dans le conteneur *input* vers le conteneur *output* :

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Le constructeur d’attribut prend un paramètre de chaîne qui spécifie le nom du conteneur ainsi qu’un espace réservé pour le nom de l’objet blob. Dans cet exemple, si un objet blob nommé *Blob1.txt* est créé dans le conteneur *input*, la fonction crée un objet blob appelé *Blob1.txt* dans le conteneur *output*. 

Vous pouvez spécifier un modèle de nom avec l’espace réservé de nom d’objet blob, comme indiqué dans l’exemple de code suivant :

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Ce code copie uniquement les objets blob dont le nom commence par "original-". Par exemple, *original-Blob1.txt* dans le conteneur *input* est copié vers *copy-Blob1.txt* dans le conteneur *output*.

Si vous devez spécifier un modèle de nom pour les noms d’objet blob qui présentent des accolades, doublez ces dernières. Par exemple, si vous souhaitez rechercher des objets blob, dans le conteneur *images* , qui présentent des noms comme suit :

        {20140101}-soundfile.mp3

utilisez ce qui suit pour votre modèle :

        images/{{20140101}}-{name}

Dans cet exemple, la valeur de l’espace réservé *name* correspond à *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Séparation des espaces réservés d’extension et des noms d’objet blob
L’exemple de code suivant remplace l’extension de fichier pendant la copie des objets blob qui s’affichent dans le conteneur *input*, vers le conteneur *output*. Le code enregistre l’extension de l’objet blob *input* et définit l’extension de l’objet blob *output* sur *.txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a id="types"></a> Types que vous pouvez lier aux objets blob
Vous pouvez utiliser l’attribut `BlobTrigger` sur les types de paramètre suivants :

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* Autres types de désérialisation par [ICloudBlobStreamBinder](#icbsb) 

Si vous souhaitez utiliser directement le compte Microsoft Azure Storage, vous pouvez ajouter un paramètre `CloudStorageAccount` à la signature de méthode.

Pour obtenir des exemples, consultez le [code de liaison d’objets blob dans le référentiel azure-webjobs-sdk sur GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a> Obtention du contenu de l’objet blob de texte via la liaison à une chaîne
Si vous attendez des objets de texte blob, vous pouvez appliquer l’élément `BlobTrigger` à un paramètre `string`. L’exemple de code suivant lie un objet blob de texte à un paramètre `string` nommé `logMessage`. La fonction utilise ce paramètre pour écrire le contenu de l’objet blob dans le tableau de bord du Kit de développement logiciel (SDK) WebJobs. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a> Obtention de contenu d’objet blob sérialisé via ICloudBlobStreamBinder
L’exemple de code suivant utilise une classe qui implémente l’élément `ICloudBlobStreamBinder` pour activer l’attribut `BlobTrigger`, afin de lier un objet blob au type `WebImage`.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

Le code de liaison du type `WebImage` est fourni dans une classe `WebImageBinder` dérivée de la classe `ICloudBlobStreamBinder`.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-the-blob-path-for-the-triggering-blob"></a>Obtenir le chemin d'accès aux objets blob pour l'objet blob de déclenchement
Pour obtenir le nom du conteneur et le nom blob de l'objet blob qui a déclenché la fonction, incluez un paramètre de chaîne `blobTrigger` dans la signature de la fonction.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a> Gestion des objets blob incohérents
Lorsqu’une fonction `BlobTrigger` échoue, le Kit de développement logiciel (SDK) l’appelle à nouveau, au cas où l’échec aurait été provoqué par une erreur temporaire. Si le problème est occasionné par le contenu de l’objet blob, la fonction échoue chaque fois qu’elle tente de traiter cet objet. Par défaut, le Kit de développement logiciel (SDK) appelle une fonction jusqu’à 5 fois pour un objet blob donné. En cas d’échec après la cinquième tentative, le Kit de développement logiciel (SDK) ajoute un message à la file d’attente nommée *webjobs-blobtrigger-poison*.

Vous pouvez configurer le nombre maximal de tentatives. Le paramètre [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) est utilisé à la fois pour la gestion des objets blob incohérents et pour l’administration des messages de la file d’attente de messages incohérents. 

Le message en file d’attente associé aux objets blob incohérents correspond à un objet JSON, qui contient les propriétés suivantes :

* FunctionId (au format *{nom_tâche_web}*.Functions.*{nom_fonction}*, par exemple : WebJob1.Functions.CopyBlob)
* BlobType (« BlockBlob » ou « PageBlob »)
* ContainerName
* BlobName
* ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)

Dans l’exemple de code suivant, la fonction `CopyBlob` comporte du code qui provoque l’échec de cette fonction chaque fois qu’elle est appelée. Une fois que le Kit de développement logiciel (SDK) a atteint le nombre de tentatives d’appel défini, un message est créé dans la file d’attente des objets blob incohérents. Ce message est traité par la fonction `LogPoisonBlob`. 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Le Kit de développement logiciel (SDK) désérialise automatiquement le message JSON. Voici la classe `PoisonBlobMessage` : 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a> Algorithme d’interrogation des objets blob
Le Kit de développement logiciel (SDK) WebJobs analyse tous les conteneurs spécifiés par les attributs `BlobTrigger` au démarrage de l’application. Dans un compte de stockage volumineux, cette analyse peut prendre du temps. Il se peut que les nouveaux objets blob ne soient pas tout de suite détectés et que les fonctions `BlobTrigger` ne soient pas exécutées avant un certain temps.

Pour détecter des objets blob nouveaux ou modifiés après le démarrage de l’application, le Kit de développement logiciel (SDK) lit régulièrement les journaux de stockage d’objets blob. Les journaux des objets blob sont mis en mémoire tampon ; ils ne sont écrits physiquement que toutes les 10 minutes environ. Il peut donc y avoir un délai important après la création ou la mise à jour d’un objet blob avant l’exécution de la fonction `BlobTrigger` correspondante. 

Il existe une exception pour les objets blob que vous créez à l’aide de l’attribut `Blob` . Lorsque le Kit de développement logiciel (SDK) WebJobs crée un objet blob, il le transmet immédiatement à toutes les fonctions `BlobTrigger` correspondantes. Par conséquent, si vous avez une chaîne d’entrées et de sorties d’objets blob, le Kit de développement logiciel (SDK) peut les traiter efficacement. Mais si vous voulez bénéficier d’une faible latence lors de l’exécution des fonctions de traitement des objets blob créés ou mis à jour par d’autres moyens, nous vous recommandons d’utiliser l’élément `QueueTrigger` plutôt que l’élément `BlobTrigger`.

### <a id="receipts"></a> Reçus d’objets blob
Le Kit de développement logiciel (SDK) Webjobs s’assure qu’aucune fonction `BlobTrigger` n’est appelée plusieurs fois pour un seul et même objet blob, nouveau ou mis à jour. Pour ce faire, il tient à jour les *reçus d’objets blob* afin de déterminer si la version d’un objet blob donné a été traitée.

Les reçus d’objets blob sont stockés dans un conteneur appelé *azure-webjobs-hosts* associé au compte de stockage Microsoft Azure indiqué par la chaîne de connexion AzureWebJobsStorage. Un reçu d’objet blob contient les informations suivantes :

* Fonction appelée pour l’objet blob ("*{nom_tâche_web}*.Functions.*{nom_fonction}*", par exemple : « WebJob1.Functions.CopyBlob »)
* Nom du conteneur
* Type d’objet blob (« BlockBlob » ou « PageBlob »)
* Nom de l’objet blob
* ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)

Si vous souhaitez forcer le retraitement d’un objet blob, vous pouvez supprimer manuellement le reçu de l’objet blob à partir du conteneur *azure-webjobs-hosts* .

## <a id="queues"></a>Sujets connexes traités dans l’article relatif aux files d’attente
Pour en savoir plus sur la gestion du traitement d’objets blob déclenché par un message en file d’attente, ou pour consulter des scénarios relatifs au Kit de développement logiciel (SDK) WebJobs non spécifiques du traitement d’objets blob, consultez la rubrique [Utilisation du stockage de la file d’attente Azure avec le Kit de développement logiciel (SDK) WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Les sujets associés abordés dans cet article sont les suivants :

* Fonctions asynchrones
* Instances multiples
* Arrêt approprié
* Utilisation des attributs du Kit de développement logiciel (SDK) WebJobs dans le corps d’une fonction
* Définition des chaînes de connexion du Kit de développement logiciel (SDK) dans le code.
* Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code
* Configuration de l’élément `MaxDequeueCount` pour la gestion des objets blob incohérents.
* Déclenchement manuel d’une fonction
* Écriture de journaux

## <a id="nextsteps"></a> Étapes suivantes
Ce guide fournit des exemples de code qui indiquent comment gérer des scénarios courants pour l’utilisation des objets blob Microsoft Azure. Pour plus d’informations sur l’utilisation d’Azure Webjobs et du Kit de développement logiciel (SDK) WebJobs Azure, consultez la rubrique [Azure Webjobs - Ressources recommandées](http://go.microsoft.com/fwlink/?linkid=390226).

