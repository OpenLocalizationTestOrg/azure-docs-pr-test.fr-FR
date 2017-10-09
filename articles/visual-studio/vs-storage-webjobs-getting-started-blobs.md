---
title: "aaaGet a démarré avec le stockage d’objets blob et de Visual Studio (projets de la tâche Web) de services connectés | Documents Microsoft"
description: "Comment tooget démarrer à l’aide du stockage d’objets Blob dans un projet de la tâche Web après la connexion tooan stockage Azure à l’aide de Visual Studio de services connectés."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Prise en main du stockage d’objets blob Azure et des services connectés Visual Studio (projets WebJob)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article fournit c# des exemples de code qui montrent comment tootrigger un processus lorsqu’un objet blob Azure est créé ou mis à jour. exemples de code Hello utilisent hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x. Lorsque vous ajoutez un projet de tâche Web tooa compte stockage à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue, package NuGet de stockage Azure approprié de hello est installé, les références .NET appropriées hello sont toohello ajouté projet et les chaînes de connexion pour le compte de stockage hello sont mis à jour dans le fichier App.config hello.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Comment tootrigger une fonction lorsqu’un objet blob est créé ou mis à jour
Cette section montre comment toouse hello **BlobTrigger** attribut.

 **Remarque :** hello toowatch de fichiers WebJobs SDK analyses de journal pour les objets BLOB nouveau ou modifié. Ce processus est lent ; une fonction ne peut-être pas déclenchée jusqu'à ce que quelques minutes ou plus après que l’objet blob de hello est créé.  Si votre application doit immédiatement les objets BLOB de tooprocess, hello recommandé consiste toocreate un message de la file d’attente lorsque vous créez les blob hello et que vous utilisez hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribut au lieu de hello **BlobTrigger** attribut sur la fonction hello qui traite l’objet blob de hello.

### <a name="single-placeholder-for-blob-name-with-extension"></a>Espace réservé unique pour le nom d’objet blob avec extension
Hello exemple de code suivant copie les objets BLOB de texte qui s’affichent dans hello *d’entrée* conteneur toohello *sortie* conteneur :

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

constructeur d’attribut Hello prend un paramètre de chaîne qui spécifie le nom du conteneur hello et un espace réservé pour le nom d’objet blob hello. Dans cet exemple, si un objet blob nommé *Blob1.txt* est créé dans hello *d’entrée* conteneur, la fonction hello crée un objet blob nommé *Blob1.txt* Bonjour *sortie*  conteneur.

Vous pouvez spécifier un modèle de nom avec un espace réservé au nom hello blob, comme indiqué dans hello suivant l’exemple de code :

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Ce code copie uniquement les objets blob dont le nom commence par "original-". Par exemple, *d’origine-Blob1.txt* Bonjour *d’entrée* conteneur est copié trop*copie-Blob1.txt* Bonjour *sortie* conteneur.

Si vous avez besoin de toospecify un modèle de nom pour les noms d’objet blob qui ont des accolades dans le nom de hello, deux accolades hello. Par exemple, si vous souhaitez que les objets BLOB toofind hello *images* conteneur qui ont des noms comme suit :

        {20140101}-soundfile.mp3

utilisez ce qui suit pour votre modèle :

        images/{{20140101}}-{name}

Dans l’exemple de hello, hello *nom* valeur d’espace réservé serait *soundfile.mp3*.

### <a name="separate-blob-name-and-extension-placeholders"></a>Séparation des espaces réservés d’extension et des noms d’objet blob
Hello modifications suivantes au code exemple hello extension de fichier pendant la copie des objets BLOB qui s’affichent dans hello *d’entrée* conteneur toohello *sortie* conteneur. code de Hello consigne extension hello Hello *d’entrée* d’objets blob et définit l’extension hello Hello *sortie* trop d’objets blob*.txt*.

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

## <a name="types-that-you-can-bind-tooblobs"></a>Types que vous pouvez lier tooblobs
Vous pouvez utiliser hello **BlobTrigger** attribut sur hello les types suivants :

* **string**
* **TextReader**
* **Stream**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Autres types de désérialisation par [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Si vous souhaitez toowork directement avec hello compte de stockage Azure, vous pouvez également ajouter un **CloudStorageAccount** signature de méthode toohello de paramètre.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Mise en route du contenu d’objet blob de texte par liaison toostring
Si les objets BLOB de texte est attendus, **BlobTrigger** peuvent être appliqué tooa **chaîne** paramètre. exemple de code suivant Hello lie un tooa d’objets blob de texte **chaîne** paramètre nommé **logMessage**. fonction Hello utilise ce contenu de hello paramètre toowrite de hello blob toohello du tableau de bord WebJobs SDK.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Obtention de contenu d’objet blob sérialisé via ICloudBlobStreamBinder
Hello exemple de code suivant utilise une classe qui implémente **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind un toohello de l’objet blob d’attribut **webimage pour** type.

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

Hello **webimage pour** code de liaison est fournie dans un **WebImageBinder** classe qui dérive de **ICloudBlobStreamBinder**.

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

## <a name="how-toohandle-poison-blobs"></a>Comment les objets BLOB toohandle incohérents
Lorsqu’un **BlobTrigger** fonction échoue, hello SDK appelle à nouveau, en cas d’échec de hello a été provoquée par une erreur temporaire. Si l’erreur de hello est provoquée par le contenu de l’objet blob de hello hello, fonction hello échoue à chaque fois qu’il essaie d’objet blob de tooprocess hello. Par défaut, hello SDK appelle une fonction des heures de too5 pour un objet blob donné. Si vous essayez de cinquième hello échoue, hello Kit de développement logiciel ajoute une file d’attente de tooa message nommé *webjobs-blobtrigger-incohérents*.

Hello le nombre maximal de tentatives est configurable. Hello même [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) paramètre est utilisé pour la gestion des objets blob incohérent et la gestion des messages de file d’attente de messages incohérents.

message de file d’attente Hello pour les objets BLOB incohérent est un objet JSON qui contient les propriétés suivantes de hello :

* ID de fonction (au format de hello *{nom de la tâche Web}*. Fonctions. *{Nom de la fonction}*, par exemple : WebJob1.Functions.CopyBlob)
* BlobType (« BlockBlob » ou « PageBlob »)
* ContainerName
* BlobName
* ETag (identificateur de version de l’objet blob, par exemple : « 0x8D1DC6E70A277EF »)

Dans hello code suivant exemple hello **CopyBlob** fonction comporte du code qui provoque son toofail chaque fois qu’elle est appelée. Une fois hello SDK appelle pour le nombre maximal de hello de nouvelles tentatives, un message est créé sur la file d’attente de messages incohérents blob hello et ce message est traité par hello **LogPoisonBlob** (fonction).

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

Hello SDK désérialise automatiquement un message JSON hello. Voici hello **PoisonBlobMessage** classe :

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Algorithme d’interrogation des objets blob
Hello WebJobs SDK analyse tous les conteneurs spécifiés par **BlobTrigger** attributs au démarrage de l’application. Dans un compte de stockage volumineux, cette analyse peut prendre du temps. Il se peut que les nouveaux objets blob ne soient pas tout de suite détectés et que les fonctions **BlobTrigger** ne soient pas exécutées avant un certain temps.

toodetect BLOB nouvelles ou modifiées après le démarrage de l’application, hello que SDK lit périodiquement à partir du stockage d’objets blob hello se connecte. Hello blob journaux sont en mémoire tampon et sont écrites uniquement physiquement de toutes les 10 minutes ou, par conséquent, il peut y avoir un délai important après un objet blob est créé ou mis à jour avant hello correspondant **BlobTrigger** fonction s’exécute.

Il existe une exception pour les objets BLOB que vous créez à l’aide de hello **Blob** attribut. Lorsque hello WebJobs SDK crée un nouvel objet blob, il passe immédiatement hello un nouvel objet blob correspondant à tooany **BlobTrigger** fonctions. Par conséquent, si vous avez une chaîne d’objets blob entrées et sorties, hello SDK peut les traiter efficacement. Mais si vous voulez bénéficier d’une faible latence lors de l’exécution des fonctions de traitement des objets blob créés ou mis à jour par d’autres moyens, nous vous recommandons d’utiliser l’élément **QueueTrigger** plutôt que l’élément **BlobTrigger**.

### <a name="blob-receipts"></a>Reçus d’objets blob
Hello WebJobs SDK vous assurer qu’aucune **BlobTrigger** fonction est appelée plusieurs fois pour hello même nouveaux ou mis à jour des objets blob. Pour ce faire, il en conservant *accusés de réception d’objets blob* dans l’ordre toodetermine si une version de l’objet blob donné a été traitée.

Accusés de réception BLOB sont stockées dans un conteneur nommé *hôtes de tâches Web azure* dans le compte de stockage Azure hello spécifié par la chaîne de connexion AzureWebJobsStorage de hello. Un accusé de réception d’objet blob a hello informations suivantes :

* fonction qui a été appelée pour l’objet blob de hello de Hello («*{nom de la tâche Web}*. Fonctions. *{Nom de la fonction}*», par exemple : « WebJob1.Functions.CopyBlob »)
* nom du conteneur Hello
* type d’objet blob Hello (« BlockBlob » ou « Un PageBlob »)
* nom d’objet blob Hello
* Hello ETag (un identificateur de version des objets blob, par exemple : « 0x8D1DC6E70A277EF »)

Si vous souhaitez tooforce retraitement d’un objet blob, vous pouvez supprimer manuellement le reçu de blob hello pour cet objet blob à partir de hello *hôtes de tâches Web azure* conteneur.

## <a name="related-topics-covered-by-hello-queues-article"></a>Rubriques connexes couvertes par l’article de files d’attente hello
Pour plus d’informations sur la façon dont le traitement des objets blob toohandle déclenché par un message de la file d’attente, ou pour les tâches Web scénarios du Kit de développement logiciel pas tooblob spécifique du traitement, consultez [comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Rubriques connexes dans cet article hello suivants :

* Fonctions asynchrones
* Instances multiples
* Arrêt approprié
* Utiliser les attributs de WebJobs SDK dans le corps d’une fonction de hello
* Définir des chaînes de connexion du Kit de développement logiciel hello dans le code.
* Définition des valeurs des paramètres de constructeur du Kit de développement logiciel (SDK) WebJobs dans le code
* Configuration de **MaxDequeueCount** pour la gestion des objets blob incohérents.
* Déclenchement manuel d’une fonction
* Écriture de journaux

## <a name="next-steps"></a>Étapes suivantes
Cet article a fourni des exemples de code qui montrent comment les objets BLOB toohandle des scénarios courants d’utilisation de Azure. Pour plus d’informations sur la façon dont toouse tâches Web Azure et hello WebJobs SDK, consultez [les ressources de documentation Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).
