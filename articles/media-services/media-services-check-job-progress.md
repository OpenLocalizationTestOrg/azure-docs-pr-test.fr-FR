---
title: "aaaMonitor progression du travail à l’aide de .NET"
description: "Découvrez comment toouse événement Gestionnaire code tootrack progression du travail et envoyer des mises à jour de l’état. exemple de code Hello est écrite en c# et utilise hello Media Services SDK pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee720ed6-8ce5-4434-b6d6-4df71fca224e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 530aa1d78437cd7c41b4d9a895f9a0e9de0ad49d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="b9ef4-104">Surveiller la progression des travaux à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="b9ef4-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9ef4-105">Portail</span><span class="sxs-lookup"><span data-stu-id="b9ef4-105">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="b9ef4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="b9ef4-106">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="b9ef4-107">REST</span><span class="sxs-lookup"><span data-stu-id="b9ef4-107">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="b9ef4-108">Lorsque vous exécutez des tâches, vous nécessitent souvent une progression du travail tootrack moyen.</span><span class="sxs-lookup"><span data-stu-id="b9ef4-108">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="b9ef4-109">Vous pouvez vérifier la progression de hello en définissant un gestionnaire d’événements StateChanged (comme décrit dans cette rubrique) ou à l’aide de toomonitor de stockage de file d’attente Azure Media Services travail notifications (comme décrit dans [cela](media-services-dotnet-check-job-progress-with-queues.md) rubrique).</span><span class="sxs-lookup"><span data-stu-id="b9ef4-109">You can check hello progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage toomonitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-toomonitor-job-progress"></a><span data-ttu-id="b9ef4-110">Définir la progression du travail StateChanged événement Gestionnaire toomonitor</span><span class="sxs-lookup"><span data-stu-id="b9ef4-110">Define StateChanged event handler toomonitor job progress</span></span>
<span data-ttu-id="b9ef4-111">Hello, exemple de code suivant définit un gestionnaire d’événements StateChanged hello.</span><span class="sxs-lookup"><span data-stu-id="b9ef4-111">hello following code example defines hello StateChanged event handler.</span></span> <span data-ttu-id="b9ef4-112">Ce gestionnaire d’événements effectue le suivi de la progression de la tâche et fournit l’état de mise à jour, en fonction de l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="b9ef4-112">This event handler tracks job progress and provides updated status, depending on hello state.</span></span> <span data-ttu-id="b9ef4-113">code de Hello définit également la méthode de LogJobStop hello.</span><span class="sxs-lookup"><span data-stu-id="b9ef4-113">hello code also defines hello LogJobStop method.</span></span> <span data-ttu-id="b9ef4-114">Cette méthode d'assistance journalise les détails de l'erreur.</span><span class="sxs-lookup"><span data-stu-id="b9ef4-114">This helper method logs error details.</span></span>

    private static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);

        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("********************");
                Console.WriteLine("Job is finished.");
                Console.WriteLine("Please wait while local tasks or downloads complete...");
                Console.WriteLine("********************");
                Console.WriteLine();
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                LogJobStop(job.Id);
                break;
            default:
                break;
        }
    }

    private static void LogJobStop(string jobId)
    {
        StringBuilder builder = new StringBuilder();
        IJob job = GetJob(jobId);

        builder.AppendLine("\nThe job stopped due toocancellation or an error.");
        builder.AppendLine("***************************");
        builder.AppendLine("Job ID: " + job.Id);
        builder.AppendLine("Job Name: " + job.Name);
        builder.AppendLine("Job State: " + job.State.ToString());
        builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
        builder.AppendLine("Media Services account name: " + _accountName);
        builder.AppendLine("Media Services account location: " + _accountLocation);
        // Log job errors if they exist.  
        if (job.State == JobState.Error)
        {
            builder.Append("Error Details: \n");
            foreach (ITask task in job.Tasks)
            {
                foreach (ErrorDetail detail in task.ErrorDetails)
                {
                    builder.AppendLine("  Task Id: " + task.Id);
                    builder.AppendLine("    Error Code: " + detail.Code);
                    builder.AppendLine("    Error Message: " + detail.Message + "\n");
                }
            }
        }
        builder.AppendLine("***************************\n");
        // Write hello output tooa local file and toohello console. hello template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="b9ef4-115">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b9ef4-115">Next step</span></span>
<span data-ttu-id="b9ef4-116">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b9ef4-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b9ef4-117">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b9ef4-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

