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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="3d4f5-103">Gestion des éléments multimédias et des entités connexes avec le Kit de développement logiciel (SDK) Media Services .NET</span><span class="sxs-lookup"><span data-stu-id="3d4f5-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d4f5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3d4f5-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="3d4f5-105">REST</span><span class="sxs-lookup"><span data-stu-id="3d4f5-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="3d4f5-106">Cette rubrique montre comment toomanage Azure Media Services pour les entités avec .NET.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="3d4f5-107">À partir du 1er avril 2017, n’importe quel enregistrement de la tâche dans votre compte plu de 90 jours est automatiquement supprimé, ainsi que ses enregistrements de tâche associés, même si le nombre total de hello d’enregistrements est au-dessous du quota maximal de hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="3d4f5-108">Par exemple, le 1er avril 2017, tout enregistrement de travail dans votre compte antérieur au 31 décembre 2016 sera automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="3d4f5-109">Si vous avez besoin des informations de tâche/hello tooarchive, vous pouvez utiliser le code hello décrite dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d4f5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3d4f5-110">Prerequisites</span></span>

<span data-ttu-id="3d4f5-111">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="3d4f5-112">Obtenir une référence pointant vers un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="3d4f5-112">Get an Asset Reference</span></span>
<span data-ttu-id="3d4f5-113">Une tâche fréquente est tooget une ressource existante tooan de référence dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="3d4f5-114">Hello, exemple de code suivant montre comment vous pouvez obtenir une référence d’élément multimédia à partir de la collection d’éléments multimédias hello sur le serveur de hello objet de contexte, selon un hello d’ID actif suivant l’exemple de code utilise une requête Linq tooget un objet de IAsset référence tooan existant.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

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

## <a name="list-all-assets"></a><span data-ttu-id="3d4f5-115">Répertorier tous les éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="3d4f5-115">List All Assets</span></span>
<span data-ttu-id="3d4f5-116">Au fur et à mesure du nombre de hello d’éléments multimédias dans le stockage, il est utile toolist vos éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="3d4f5-117">Hello, exemple de code suivant montre comment tooiterate via hello collection actifs sur l’objet de contexte de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="3d4f5-118">À chaque élément multimédia, exemple de code hello écrit également certaines de sa console de toohello de valeurs de propriété.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="3d4f5-119">Par exemple, chaque élément multimédia peut contenir plusieurs fichiers multimédias.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="3d4f5-120">exemple de code Hello écrit tous les fichiers associés à chaque élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-120">hello code example writes out all files associated with each asset.</span></span>

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

## <a name="get-a-job-reference"></a><span data-ttu-id="3d4f5-121">Obtenir une référence pointant vers un travail</span><span class="sxs-lookup"><span data-stu-id="3d4f5-121">Get a Job Reference</span></span>

<span data-ttu-id="3d4f5-122">Lorsque vous travaillez avec des tâches de traitement dans le code de Media Services, vous devez souvent tooget un travail existant de référence tooan, selon un hello ID. exemple de code suivant montre comment l’objet à partir de la collection de tâches hello tooget un tooan référence IJob.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="3d4f5-123">Vous ont besoin de tooget référence à un travail lors du démarrage d’un travail d’encodage longue et devez état du travail toocheck hello sur un thread.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="3d4f5-124">Dans ce cas, lors de la méthode hello renvoie à partir d’un thread, vous devez tooretrieve un travail de tooa référence actualisée.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

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

## <a name="list-jobs-and-assets"></a><span data-ttu-id="3d4f5-125">Répertorier les travaux et les éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="3d4f5-125">List Jobs and Assets</span></span>
<span data-ttu-id="3d4f5-126">Une tâche associée importante est actifs toolist avec leur travail associé dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="3d4f5-127">Hello exemple de code suivant vous montre comment toolist chaque objet IJob, puis pour chaque tâche, il affiche des propriétés sur les travaux de hello, toutes les tâches associées, entrées toutes les ressources et tous les éléments multimédias de sortie.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="3d4f5-128">code Hello dans cet exemple peut être utile pour nombreuses autres tâches.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="3d4f5-129">Par exemple, si vous souhaitez que les éléments multimédias de sortie hello toolist à partir d’un ou plusieurs travaux d’encodage que vous avez exécutés précédemment, ce code montre comment les éléments multimédias de sortie de tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="3d4f5-130">Lorsque vous disposez d’une ressource en sortie tooan référence, vous pouvez diffuser hello tooother contenu utilisateurs ou applications en téléchargeant ou en fournissant des URL.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="3d4f5-131">Pour plus d’informations sur les options de fourniture de ressources, consultez [fournir des ressources avec hello Media Services SDK pour .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="list-all-access-policies"></a><span data-ttu-id="3d4f5-132">Répertorier toutes les stratégies d’accès</span><span class="sxs-lookup"><span data-stu-id="3d4f5-132">List all Access Policies</span></span>
<span data-ttu-id="3d4f5-133">Dans Media Services, vous pouvez définir une stratégie d’accès sur un élément multimédia ou ses fichiers.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="3d4f5-134">Une stratégie d’accès définit les autorisations hello pour un fichier ou un élément multimédia (le type d’accès et la durée de hello).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="3d4f5-135">Dans votre code Media Services, vous définissez généralement une stratégie d’accès en créant un objet IAccessPolicy et en l’associant à un élément multimédia existant.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="3d4f5-136">Ensuite, vous créez un objet ILocator, ce qui vous permet de fournir des tooassets d’un accès direct dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="3d4f5-137">projet Visual Studio Hello qui accompagne cette documentation contient plusieurs exemples de code qui montrent comment toocreate et attribuez accéder aux stratégies et les localisateurs tooassets.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="3d4f5-138">Hello suivant exemple de code montre comment toolist toutes les stratégies d’accès serveur de hello et type de hello affiche des autorisations associées à chaque.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="3d4f5-139">Les stratégies d’accès tooview une autre façon utile est toolist tous les objets ILocator sur le serveur de hello, et ensuite pour chaque localisateur, vous pouvez répertorier sa stratégie d’accès associé à l’aide de sa propriété de la stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="3d4f5-140">Limiter les stratégies d’accès</span><span class="sxs-lookup"><span data-stu-id="3d4f5-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="3d4f5-141">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="3d4f5-142">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="3d4f5-143">Par exemple, vous pouvez créer un ensemble générique de stratégies avec hello suivant du code qui ne s’exécute une seule fois dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="3d4f5-144">Vous pouvez enregistrer le fichier de journal ID tooa pour une utilisation ultérieure :</span><span class="sxs-lookup"><span data-stu-id="3d4f5-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="3d4f5-145">Ensuite, vous pouvez utiliser hello existant ID dans votre code comme suit :</span><span class="sxs-lookup"><span data-stu-id="3d4f5-145">Then, you can use hello existing IDs in your code like this:</span></span>

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

## <a name="list-all-locators"></a><span data-ttu-id="3d4f5-146">Répertorier tous les localisateurs</span><span class="sxs-lookup"><span data-stu-id="3d4f5-146">List All Locators</span></span>
<span data-ttu-id="3d4f5-147">Un localisateur est une URL qui fournit un chemin d’accès direct de tooaccess un élément multimédia, ainsi que les actifs de toohello autorisations tel que défini par la stratégie d’accès associée du localisateur hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="3d4f5-148">Chaque élément multimédia peut avoir une collection d’objets ILocator associée à sa propriété Locators.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="3d4f5-149">contexte de serveur Hello possède également un ensemble de localisateurs qui contient tous les localisateurs.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="3d4f5-150">Hello exemple de code suivant répertorie tous les localisateurs sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="3d4f5-151">Pour chaque localisateur, il affiche hello Id pour les ressources connexes hello et stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="3d4f5-152">Elle affiche également le type hello des autorisations, date d’expiration de hello et actifs de toohello hello chemin d’accès complet.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="3d4f5-153">Notez qu’une ressource de tooan de chemin d’accès de recherche est uniquement un base URL toohello élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="3d4f5-154">toocreate qu'un tooindividual directe des fichiers qu’un utilisateur ou une application peut accéder, votre code doit ajouter chemin d’accès du localisateur de toohello chemin hello fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="3d4f5-155">Pour plus d’informations sur la façon de toodo, consultez les rubrique hello [fournir des ressources avec hello Media Services SDK pour .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="3d4f5-156">Énumérer les grandes collections d'entités</span><span class="sxs-lookup"><span data-stu-id="3d4f5-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="3d4f5-157">Lors de l’interrogation des entités, il existe une limite de 1000 entités retournées à la fois, car il est public reste v2 limite les résultats de too1000 de résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="3d4f5-158">Vous devez toouse Skip et Take lors de l’énumération dans les grandes collections d’entités.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="3d4f5-159">Hello fonction suivant parcourt tous les travaux hello Bonjour fourni compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="3d4f5-160">Media Services renvoie 1 000 tâches dans Collection de tâches.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="3d4f5-161">fonction Hello rend l’utilisation de Skip et prendre toomake Assurez-vous que tous les travaux sont énumérés (au cas où vous avez plus de 1 000 travaux dans votre compte).</span><span class="sxs-lookup"><span data-stu-id="3d4f5-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

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

## <a name="delete-an-asset"></a><span data-ttu-id="3d4f5-162">Supprimer un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="3d4f5-162">Delete an Asset</span></span>
<span data-ttu-id="3d4f5-163">Bonjour à l’exemple suivant supprime une ressource.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="3d4f5-164">Supprimer un travail</span><span class="sxs-lookup"><span data-stu-id="3d4f5-164">Delete a Job</span></span>
<span data-ttu-id="3d4f5-165">toodelete un travail, vous devez vérifier l’état hello du travail hello comme indiqué dans la propriété d’état hello.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="3d4f5-166">Les travaux terminés ou annulés peuvent être supprimés, tandis que pour les travaux dans d’autres états, par exemple en file d’attente, planifiés ou en cours de traitement, il faut d’abord procéder à une annulation, puis supprimer le travail.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="3d4f5-167">Hello exemple de code suivant montre une méthode de suppression d’une tâche en la vérification des États de travail et en supprimant lorsque l’état de hello est terminé ou annulé.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="3d4f5-168">Ce code dépend de la section précédente de hello dans cette rubrique pour obtenir une tâche tooa de référence : obtenir une référence de projet.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

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


## <a name="delete-an-access-policy"></a><span data-ttu-id="3d4f5-169">Supprimer une stratégie d’accès</span><span class="sxs-lookup"><span data-stu-id="3d4f5-169">Delete an Access Policy</span></span>
<span data-ttu-id="3d4f5-170">Hello exemple de code suivant montre comment tooget une stratégie d’accès de référence tooan basée sur un identificateur de stratégie et stratégie de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="3d4f5-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="3d4f5-171">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="3d4f5-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3d4f5-172">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="3d4f5-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

