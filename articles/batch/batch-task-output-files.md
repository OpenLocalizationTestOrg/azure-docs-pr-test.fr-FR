---
title: "aaaPersist projet et la tâche de sortie tooAzure stockage avec hello API de service de traitement par lots Azure | Documents Microsoft"
description: "Découvrez comment des tooAzure stockage de sortie de projet et la tâche de traitement par lots toopersist toouse API de service de traitement par lots."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Conserver des tâches données tooAzure stockage avec hello API de service de traitement par lots

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Depuis la version 2017-05-01, hello API de service de traitement par lots prend en charge la persistance tooAzure de données de sortie stockage pour les tâches et le Gestionnaire des tâches qui s’exécutent sur les pools de configuration d’ordinateur virtuel hello. Lorsque vous ajoutez une tâche, vous pouvez spécifier un conteneur dans le stockage Azure en tant que destination hello pour la sortie de la tâche hello. service de traitement par lots Hello écrit ensuite n’importe quel conteneur de toothat de données de sortie lors de la tâche hello est terminée.

Un hello de toousing parti par lots de la sortie de la tâche service API toopersist est que vous n’avez pas besoin d’application hello toomodify hello tâche est en cours d’exécution. Au lieu de cela, avec une application cliente quelques modifications simples tooyour, vous pouvez conserver la sortie de la tâche hello de code hello qui crée la tâche hello.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Quand utiliser le résultat de la tâche toopersist hello API de lot ?

Traitement par lots Azure fournit plusieurs méthodes toopersist sortie de la tâche. À l’aide de hello API de service de traitement par lots est une approche pratique est meilleure toothese adapté aux scénarios :

- Vous souhaitez sortie de tâche toowrite code toopersist d’au sein de votre application cliente, sans modifier l’application hello votre tâche est en cours d’exécution.
- Vous souhaitez toopersist de la sortie des tâches de traitement par lots et le gestionnaire tâches dans des pools créés avec la configuration d’ordinateur virtuel hello.
- Vous souhaitez que le conteneur de stockage Azure tooan toopersist sortie avec un nom quelconque.
- Vous souhaitez que le conteneur de stockage Azure toopersist sortie tooan nommé toohello conformément [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Si votre scénario diffère de celles répertoriées ci-dessus, vous devrez peut-être tooconsider une approche différente. Par exemple, API de lot hello ne prend pas en charge tooAzure de sortie en continu stockage pendant l’exécution de la tâche hello. toostream de sortie, envisagez d’utiliser la bibliothèque Conventions pour les fichiers Batch pour .NET hello. Pour d’autres langues, vous devez tooimplement votre propre solution. Pour plus d’informations sur les autres options pour la sortie de tâche persistantes, consultez [tooAzure stockage de sortie de projet de la persistance et la tâche](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Créer un conteneur dans le stockage Azure

sortie de la tâche de toopersist tooAzure de stockage, vous devez toocreate un conteneur qui sert de destination hello pour vos fichiers de sortie. Créer le conteneur de hello avant d’exécuter la tâche, de préférence avant d’envoyer votre travail. conteneur de hello toocreate, utilisez hello approprié Azure Storage client library ou kit de développement logiciel. Pour plus d’informations sur les API de stockage Azure, consultez hello [documentation Azure Storage](https://docs.microsoft.com/azure/storage/).

Par exemple, si vous écrivez votre application en c#, utilisez hello [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Hello suivant montre l’exemple de comment toocreate un conteneur :

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Obtenir une signature d’accès partagé pour le conteneur de hello

Après avoir créé le conteneur de hello, obtenir une signature d’accès partagé (SAS) avec un accès en écriture toohello conteneur. Une SAP fournit un conteneur de toohello accès délégué. Hello SAP accorde un accès avec un jeu spécifié d’autorisations et sur un intervalle de temps spécifié. Hello service Batch doit une SAP de conteneur de toohello écriture autorisations toowrite tâche sortie. Pour plus d’informations sur les signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé \(SAP\) dans le stockage Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Lorsque vous obtenez une SAP à l’aide des API de stockage Azure de hello, hello API renvoie une chaîne de jeton SAS. Cette chaîne de jeton inclut tous les paramètres de hello SAP, y compris les autorisations de hello et intervalle de salutation pendant le hello SAS est valide. toouse hello SAS tooaccess un conteneur dans le stockage Azure, vous devez les URI de ressource de toohello de chaîne de jeton SAS de tooappend hello. Hello URI de ressource, ainsi que de hello ajouté de jeton SAS, fournit un accès authentifié tooAzure stockage.

Hello exemple suivant montre comment la chaîne pour le conteneur de hello du jeton tooget un SAS en écriture seule, puis ajoute l’URI du conteneur toohello hello SAS :

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Spécifier les fichiers de sortie pour le résultat de la tâche

toospecify des fichiers de sortie d’une tâche, créer une collection de [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) des objets et affecter toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) propriété lorsque vous créez la tâche hello. 

exemple de code .NET Hello crée une tâche qui écrit le fichier tooa de nombres aléatoires nommé `output.txt`. exemple de Hello crée un fichier de sortie pour `output.txt` toobe écrit toohello conteneur. exemple de Hello crée également des fichiers de sortie pour les fichiers journaux qui correspondent au modèle de fichier hello `std*.txt` (_par exemple,_, `stdout.txt` et `stderr.txt`). URL du conteneur Hello requiert hello SAS qui a été créé précédemment pour le conteneur de hello. Hello service Batch utilise le conteneur toohello accès hello SAS tooauthenticate : 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Spécifier un modèle de fichier pour la correspondance

Lorsque vous spécifiez un fichier de sortie, vous pouvez utiliser hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) propriété toospecify un modèle de fichier pour la correspondance. modèle de fichier Hello peut correspondent aux fichiers de zéro, un seul fichier ou un ensemble de fichiers qui sont créés par la tâche hello.

Hello **FilePattern** propriété prend en charge les caractères génériques de système de fichiers standard telles que `*` (pour non récursives correspond à) et `**` (pour récursive correspond à). Par exemple, exemple de code hello ci-dessus spécifie hello fichier modèle toomatch `std*.txt` de manière non récursive : 

`filePattern: @"..\std*.txt"`

tooupload un seul fichier, spécifiez un modèle de fichier sans caractères génériques. Par exemple, exemple de code hello ci-dessus spécifie hello fichier modèle toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Spécifier une condition de chargement

Hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) propriété autorise conditionnelle de téléchargement des fichiers de sortie. Un scénario courant consiste à tooupload un ensemble de fichiers si la tâche hello réussit et un autre ensemble de fichiers en cas d’échec. Par exemple, vous souhaiterez des fichiers journaux détaillés tooupload uniquement lorsque la tâche hello échoue et se termine avec un code de sortie différent de zéro. De même, vous pouvez choisir les fichiers de résultats tooupload uniquement si la tâche hello réussit, que ces fichiers peuvent être manquantes ou incomplètes si hello tâche échoue.

exemple de code ci-dessus Hello définit hello **UploadCondition** propriété trop**TaskCompletion**. Ce paramètre spécifie que si le fichier hello est toobe téléchargé une fois les tâches hello terminée, quelle que soit la valeur hello du code de sortie hello. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Pour les autres paramètres, consultez hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Lever l’ambiguïté de fichiers avec hello même nom

tâches Hello dans un travail peuvent produire des fichiers qui ont hello même nom. Par exemple, `stdout.txt` et `stderr.txt` sont créés pour chaque tâche qui s’exécute dans un travail. Étant donné que chaque tâche s’exécute dans son propre contexte, ces fichiers ne sont en conflit sur le système de fichiers du nœud hello. Toutefois, lorsque vous téléchargez des fichiers à partir de plusieurs conteneurs partagé tooa de tâches, vous devez les fichiers toodisambiguate avec hello même nom.

Hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) propriété spécifie l’objet blob de destination hello ou un répertoire virtuel pour les fichiers de sortie. Vous pouvez utiliser hello **chemin d’accès** objet blob de propriété tooname hello ou un répertoire virtuel de telle sorte que les fichiers de sortie avec hello même nom sont nommées de manière unique dans le stockage Azure. À l’aide des ID de tâche : hello dans le chemin d’accès hello est un bon moyen tooensure les noms uniques et identifier facilement les fichiers.

Si hello **FilePattern** propriété a la valeur tooa génériques expression, puis tous les fichiers qui correspondent au modèle de hello sont téléchargées toohello répertoire virtuel spécifié par hello **chemin d’accès** propriété. Par exemple, si hello conteneur est `mycontainer`, tâche hello ID est `mytask`, et le modèle de fichier hello est `..\std*.txt`, puis hello absolue URI toohello les fichiers de sortie dans le stockage Azure doit être similaires à :

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Si hello **FilePattern** propriété ensemble toomatch un seul nom de fichier, ce qui signifie qu’il ne contienne pas de caractères génériques, hello ensuite la valeur de hello **chemin d’accès** propriété spécifie le nom d’objet blob complet hello . Si vous prévoyez d’affectation de noms est en conflit avec un seul fichier à partir de plusieurs tâches, puis intégrer hello nom du répertoire virtuel de hello de toodisambiguate de nom de fichier hello ces fichiers. Par exemple, set hello **chemin d’accès** ID de tâche : hello propriété tooinclude, caractère de délimiteur hello (en général, une barre oblique) et nom de fichier hello :

`path: taskId + @"/output.txt"`

Hello absolus fichiers de sortie URI toohello pour un ensemble de tâches sera semblables à :

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Pour plus d’informations sur les répertoires virtuels dans le stockage Azure, consultez [répertorier les objets BLOB de hello dans un conteneur](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Diagnostiquer les erreurs de chargement de fichier

Si la sortie de téléchargement de fichiers tooAzure stockage échoue, puis tâche hello déplace toohello **terminé** état et hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) est définie. Examinez hello **FailureInformation** toodetermine de propriété d’indiquer l’erreur s’est produite. Voici, par exemple, une erreur se produit lors du téléchargement du fichier si le conteneur de hello est introuvable : 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

Sur chaque téléchargement du fichier, lot écrit deux connecter à nœud de calcul fichiers toohello, `fileuploadout.txt` et `fileuploaderr.txt`. Vous pouvez examiner ces toolearn de fichiers journaux plus d’informations sur un échec spécifique. Dans les cas où hello fichier jamais tentative de chargement, par exemple, car il est impossible d’exécuter la tâche hello lui-même, puis ces fichiers journaux n’existent pas.

## <a name="diagnose-file-upload-performance"></a>Diagnostiquer les performances de chargement de fichier

Hello `fileuploadout.txt` fichier enregistre la progression du téléchargement. Vous pouvez examiner cette toolearn fichier prennent plus d’informations sur la durée pendant laquelle les téléchargements de votre fichier. N’oubliez pas qu’il existe plusieurs facteurs des performances tooupload, y compris la taille de hello du nœud hello, autre activité sur le nœud de hello au moment de hello de téléchargement de hello, si le conteneur cible de hello est Bonjour est de même région que le pool de traitement par lots hello, le nombre de nœuds téléchargement de compte de stockage toohello hello en même temps et ainsi de suite.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Utiliser les API de service de traitement par lots hello avec hello Conventions pour les fichiers Batch standard

Lorsque vous rendez persistante de sortie de la tâche avec hello API de service de traitement par lots, vous pouvez nommer votre conteneur de destination et les objets BLOB comme vous le souhaitez. Vous pouvez également choisir tooname leur selon toohello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). standard de Conventions pour les fichiers Hello détermine les noms de hello du conteneur de destination hello et d’objet blob dans le stockage Azure pour un fichier de sortie donnée en fonction du nom hello de hello projet et la tâche. Si vous utilisez hello Conventions standard pour les fichiers de nommer les fichiers de sortie, vos fichiers de sortie sont disponibles pour l’affichage dans hello [portail Azure](https://portal.azure.com).

Si vous développez en c#, vous pouvez utiliser les méthodes de hello intégrées hello [bibliothèque Conventions pour les fichiers Batch pour .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Cette bibliothèque crée hello nommé correctement les conteneurs et les chemins d’accès de l’objet blob pour vous. Par exemple, vous pouvez appeler hello API tooget hello correct nom hello conteneur, selon le nom de la tâche hello :

```csharp
string containerName = job.OutputStorageContainerName();
```

Vous pouvez utiliser hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) méthode tooreturn une URL de signature (SAP) d’accès partagé qui est utilisé toowrite toohello conteneur. Vous pouvez ensuite passer cette toohello SAS [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) constructeur.

Si vous développez dans une langue autre que c#, vous devez standard de Conventions pour les fichiers tooimplement hello vous-même.

## <a name="code-sample"></a>Exemple de code

Hello [PersistOutputs] [ github_persistoutputs] exemple de projet est un des hello [exemples de code Azure Batch] [ github_samples] sur GitHub. Cette solution Visual Studio montre comment toouse bibliothèque cliente de lot hello pour les tâches de toopersist .NET sortie toodurable stockage. toorun hello exemple, procédez comme suit :

1. Projet ouvert hello dans **Visual Studio 2015 ou plus récente**.
2. Ajouter votre lot et un stockage **informations d’identification de compte** trop**AccountSettings.settings** dans le projet de Microsoft.Azure.Batch.Samples.Common hello.
3. **Build** (mais ne s’exécutent pas) hello solution. Restaurez les packages NuGet si vous y êtes invité.
4. Hello d’utilisation tooupload portail Azure un [package d’application](batch-application-packages.md) pour **PersistOutputsTask**. Inclure hello `PersistOutputsTask.exe` et ses assemblys dépendants dans le package .zip de hello, ID de l’application hello ensemble trop « PersistOutputsTask » et application hello version du package trop « 1.0 ».
5. **Démarrer** hello (exécution) **PersistOutputs** projet.
6. Lorsque toochoose demandées hello persistance technologie toouse pour l’exemple hello, entrez **2** toorun hello exemple à l’aide de la sortie de la tâche toopersist hello API de service de traitement par lots.
7. Si vous le souhaitez, réexécutez exemple hello entrant **3** sortie toopersist hello API de lot, mais aussi tooname hello conteneur et l’objet blob de chemin de destination en fonction de toohello Conventions standard pour les fichiers.

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur la sortie de la tâche persistantes avec la bibliothèque de Conventions pour les fichiers hello pour .NET, consultez [conserver les travaux et des tâches données tooAzure stockage avec bibliothèque de Conventions pour les fichiers Batch hello pour .NET toopersist ](batch-task-output-file-conventions.md).
- Pour plus d’informations sur les autres approches pour la persistance des données de sortie dans le traitement par lots Azure, consultez [tooAzure stockage de sortie de projet de la persistance et la tâche](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
