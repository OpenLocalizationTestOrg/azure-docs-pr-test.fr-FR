---
title: "Télécharger des éléments multimédias Media Services sur votre ordinateur - Azure | Microsoft Docs"
description: "Découvrez comment télécharger des éléments multimédias sur votre ordinateur. Les exemples de code sont écrits en C# et utilisent le Kit de développement logiciel (SDK) Media Services pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d8e740e969f68c85842f42c109328423da1b4414
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="64c63-104">Fourniture d’un élément multimédia par téléchargement</span><span class="sxs-lookup"><span data-stu-id="64c63-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="64c63-105">Cette rubrique présente les options disponibles pour fournir des éléments multimédias chargés sur Media Services.</span><span class="sxs-lookup"><span data-stu-id="64c63-105">This topic discusses options for delivering media assets uploaded to Media Services.</span></span> <span data-ttu-id="64c63-106">De nombreux scénarios d'application permettent de fournir du contenu Media Services.</span><span class="sxs-lookup"><span data-stu-id="64c63-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="64c63-107">Il est possible de télécharger des éléments multimédias ou d'y accéder en utilisant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="64c63-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="64c63-108">Vous pouvez envoyer du contenu multimédia vers une autre application ou un autre fournisseur de contenu.</span><span class="sxs-lookup"><span data-stu-id="64c63-108">You can send media content to another application or to another content provider.</span></span> <span data-ttu-id="64c63-109">Pour améliorer les performances et l’évolutivité, vous pouvez également fournir du contenu en utilisant un réseau de distribution de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="64c63-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="64c63-110">Cet exemple montre comment télécharger des éléments multimédias depuis Media Services sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="64c63-110">This example shows how to download media assets from Media Services to your local computer.</span></span> <span data-ttu-id="64c63-111">Le code lance une requête sur les tâches associées au compte Media Services par ID de tâche et accède à l'ensemble **OutputMediaAssets** du compte (qui regroupe un ou plusieurs éléments multimédias en sortie, suite à l'exécution d'une tâche).</span><span class="sxs-lookup"><span data-stu-id="64c63-111">The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="64c63-112">Cet exemple indique comment télécharger des éléments multimédias en sortie depuis une tâche, mais il est possible d’appliquer la même approche pour télécharger d’autres éléments.</span><span class="sxs-lookup"><span data-stu-id="64c63-112">This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.</span></span>

>[!NOTE]
><span data-ttu-id="64c63-113">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="64c63-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="64c63-114">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="64c63-114">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="64c63-115">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="64c63-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="64c63-116">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="64c63-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="64c63-117">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="64c63-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="64c63-118">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="64c63-118">See Also</span></span>
[<span data-ttu-id="64c63-119">de diffusion de contenu en continu</span><span class="sxs-lookup"><span data-stu-id="64c63-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

