---
title: "aaaManaging actifs et les entités associées avec Media Services .NET SDK"
description: "Découvrez comment toomanage actifs et les entités connexes avec hello Media Services SDK pour .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Gestion des éléments multimédias et des entités connexes avec le Kit de développement logiciel (SDK) Media Services .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

Cette rubrique montre comment toomanage Azure Media Services pour les entités avec .NET. 

>[!NOTE]
> À partir du 1er avril 2017, n’importe quel enregistrement de la tâche dans votre compte plu de 90 jours est automatiquement supprimé, ainsi que ses enregistrements de tâche associés, même si le nombre total de hello d’enregistrements est au-dessous du quota maximal de hello. Par exemple, le 1er avril 2017, tout enregistrement de travail dans votre compte antérieur au 31 décembre 2016 sera automatiquement supprimé. Si vous avez besoin des informations de tâche/hello tooarchive, vous pouvez utiliser le code hello décrite dans cette rubrique.

## <a name="prerequisites"></a>Composants requis

Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Obtenir une référence pointant vers un élément multimédia
Une tâche fréquente est tooget une ressource existante tooan de référence dans Media Services. Hello, exemple de code suivant montre comment vous pouvez obtenir une référence d’élément multimédia à partir de la collection d’éléments multimédias hello sur le serveur de hello objet de contexte, selon un hello d’ID actif suivant l’exemple de code utilise une requête Linq tooget un objet de IAsset référence tooan existant.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Répertorier tous les éléments multimédias
Au fur et à mesure du nombre de hello d’éléments multimédias dans le stockage, il est utile toolist vos éléments multimédias. Hello, exemple de code suivant montre comment tooiterate via hello collection actifs sur l’objet de contexte de serveur hello. À chaque élément multimédia, exemple de code hello écrit également certaines de sa console de toohello de valeurs de propriété. Par exemple, chaque élément multimédia peut contenir plusieurs fichiers multimédias. exemple de code Hello écrit tous les fichiers associés à chaque élément multimédia.

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a>Obtenir une référence pointant vers un travail

Lorsque vous travaillez avec des tâches de traitement dans le code de Media Services, vous devez souvent tooget un travail existant de référence tooan, selon un hello ID. exemple de code suivant montre comment l’objet à partir de la collection de tâches hello tooget un tooan référence IJob.

Vous ont besoin de tooget référence à un travail lors du démarrage d’un travail d’encodage longue et devez état du travail toocheck hello sur un thread. Dans ce cas, lors de la méthode hello renvoie à partir d’un thread, vous devez tooretrieve un travail de tooa référence actualisée.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Répertorier les travaux et les éléments multimédias
Une tâche associée importante est actifs toolist avec leur travail associé dans Media Services. Hello exemple de code suivant vous montre comment toolist chaque objet IJob, puis pour chaque tâche, il affiche des propriétés sur les travaux de hello, toutes les tâches associées, entrées toutes les ressources et tous les éléments multimédias de sortie. code Hello dans cet exemple peut être utile pour nombreuses autres tâches. Par exemple, si vous souhaitez que les éléments multimédias de sortie hello toolist à partir d’un ou plusieurs travaux d’encodage que vous avez exécutés précédemment, ce code montre comment les éléments multimédias de sortie de tooaccess hello. Lorsque vous disposez d’une ressource en sortie tooan référence, vous pouvez diffuser hello tooother contenu utilisateurs ou applications en téléchargeant ou en fournissant des URL. 

Pour plus d’informations sur les options de fourniture de ressources, consultez [fournir des ressources avec hello Media Services SDK pour .NET](media-services-deliver-streaming-content.md).

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a>Répertorier toutes les stratégies d’accès
Dans Media Services, vous pouvez définir une stratégie d’accès sur un élément multimédia ou ses fichiers. Une stratégie d’accès définit les autorisations hello pour un fichier ou un élément multimédia (le type d’accès et la durée de hello). Dans votre code Media Services, vous définissez généralement une stratégie d’accès en créant un objet IAccessPolicy et en l’associant à un élément multimédia existant. Ensuite, vous créez un objet ILocator, ce qui vous permet de fournir des tooassets d’un accès direct dans Media Services. projet Visual Studio Hello qui accompagne cette documentation contient plusieurs exemples de code qui montrent comment toocreate et attribuez accéder aux stratégies et les localisateurs tooassets.

Hello suivant exemple de code montre comment toolist toutes les stratégies d’accès serveur de hello et type de hello affiche des autorisations associées à chaque. Les stratégies d’accès tooview une autre façon utile est toolist tous les objets ILocator sur le serveur de hello, et ensuite pour chaque localisateur, vous pouvez répertorier sa stratégie d’accès associé à l’aide de sa propriété de la stratégie d’accès.

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a>Limiter les stratégies d’accès 

>[!NOTE]
> Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies). 

Par exemple, vous pouvez créer un ensemble générique de stratégies avec hello suivant du code qui ne s’exécute une seule fois dans votre application. Vous pouvez enregistrer le fichier de journal ID tooa pour une utilisation ultérieure :

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Ensuite, vous pouvez utiliser hello existant ID dans votre code comme suit :

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Répertorier tous les localisateurs
Un localisateur est une URL qui fournit un chemin d’accès direct de tooaccess un élément multimédia, ainsi que les actifs de toohello autorisations tel que défini par la stratégie d’accès associée du localisateur hello. Chaque élément multimédia peut avoir une collection d’objets ILocator associée à sa propriété Locators. contexte de serveur Hello possède également un ensemble de localisateurs qui contient tous les localisateurs.

Hello exemple de code suivant répertorie tous les localisateurs sur le serveur de hello. Pour chaque localisateur, il affiche hello Id pour les ressources connexes hello et stratégie d’accès. Elle affiche également le type hello des autorisations, date d’expiration de hello et actifs de toohello hello chemin d’accès complet.

Notez qu’une ressource de tooan de chemin d’accès de recherche est uniquement un base URL toohello élément multimédia. toocreate qu'un tooindividual directe des fichiers qu’un utilisateur ou une application peut accéder, votre code doit ajouter chemin d’accès du localisateur de toohello chemin hello fichier spécifique. Pour plus d’informations sur la façon de toodo, consultez les rubrique hello [fournir des ressources avec hello Media Services SDK pour .NET](media-services-deliver-streaming-content.md).

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Énumérer les grandes collections d'entités
Lors de l’interrogation des entités, il existe une limite de 1000 entités retournées à la fois, car il est public reste v2 limite les résultats de too1000 de résultats de requête. Vous devez toouse Skip et Take lors de l’énumération dans les grandes collections d’entités. 

Hello fonction suivant parcourt tous les travaux hello Bonjour fourni compte Media Services. Media Services renvoie 1 000 tâches dans Collection de tâches. fonction Hello rend l’utilisation de Skip et prendre toomake Assurez-vous que tous les travaux sont énumérés (au cas où vous avez plus de 1 000 travaux dans votre compte).

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a>Supprimer un élément multimédia
Bonjour à l’exemple suivant supprime une ressource.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Supprimer un travail
toodelete un travail, vous devez vérifier l’état hello du travail hello comme indiqué dans la propriété d’état hello. Les travaux terminés ou annulés peuvent être supprimés, tandis que pour les travaux dans d’autres états, par exemple en file d’attente, planifiés ou en cours de traitement, il faut d’abord procéder à une annulation, puis supprimer le travail.

Hello exemple de code suivant montre une méthode de suppression d’une tâche en la vérification des États de travail et en supprimant lorsque l’état de hello est terminé ou annulé. Ce code dépend de la section précédente de hello dans cette rubrique pour obtenir une tâche tooa de référence : obtenir une référence de projet.

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a>Supprimer une stratégie d’accès
Hello exemple de code suivant montre comment tooget une stratégie d’accès de référence tooan basée sur un identificateur de stratégie et stratégie de hello toodelete.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

