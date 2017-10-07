---
title: ordinateur de tooyour aaaDownload Media Services actifs - Azure | Documents Microsoft
description: "En savoir plus sur l’ordinateur de tooyour toodownload actifs. Exemples de code sont écrits en c# et utilisent hello Media Services SDK pour .NET."
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
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="2b4a3-104">Fourniture d’un élément multimédia par téléchargement</span><span class="sxs-lookup"><span data-stu-id="2b4a3-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="2b4a3-105">Cette rubrique présente les options de remise des fichiers multimédias téléchargé tooMedia Services.</span><span class="sxs-lookup"><span data-stu-id="2b4a3-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="2b4a3-106">De nombreux scénarios d'application permettent de fournir du contenu Media Services.</span><span class="sxs-lookup"><span data-stu-id="2b4a3-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="2b4a3-107">Il est possible de télécharger des éléments multimédias ou d'y accéder en utilisant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="2b4a3-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="2b4a3-108">Vous pouvez envoyer application tooanother contenu de support ou le fournisseur de contenu tooanother.</span><span class="sxs-lookup"><span data-stu-id="2b4a3-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="2b4a3-109">Pour améliorer les performances et l’évolutivité, vous pouvez également fournir du contenu en utilisant un réseau de distribution de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="2b4a3-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="2b4a3-110">Cet exemple montre comment toodownload fichiers multimédias à partir de l’ordinateur local tooyour de Media Services.</span><span class="sxs-lookup"><span data-stu-id="2b4a3-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="2b4a3-111">requêtes de code Hello hello travaux associés de compte de service de média hello par ID de tâche et accède à ses **OutputMediaAssets** (ce qui est un ensemble hello d’un ou plusieurs éléments multimédias de sortie qui résulte de l’exécution d’un travail).</span><span class="sxs-lookup"><span data-stu-id="2b4a3-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="2b4a3-112">Cet exemple montre comment multimédia de sortie toodownload actifs à partir d’un travail, mais vous peuvent appliquer hello même toodownload d’approche autres actifs.</span><span class="sxs-lookup"><span data-stu-id="2b4a3-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="2b4a3-113">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="2b4a3-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="2b4a3-114">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="2b4a3-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="2b4a3-115">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="2b4a3-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
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
            // Use hello following event handler toocheck download progress.
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="2b4a3-116">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="2b4a3-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b4a3-117">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2b4a3-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2b4a3-118">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2b4a3-118">See Also</span></span>
[<span data-ttu-id="2b4a3-119">de diffusion de contenu en continu</span><span class="sxs-lookup"><span data-stu-id="2b4a3-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

