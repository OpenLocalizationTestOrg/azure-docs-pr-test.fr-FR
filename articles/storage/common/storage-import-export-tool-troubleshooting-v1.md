---
title: "aaaTroubleshooting hello outil d’importation/exportation Azure | Documents Microsoft"
description: "En savoir plus sur les problèmes courants de hello visibles lorsque vous utilisez hello outil d’importation/exportation Azure et comment toohandle les."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="1ddff-103">Résolution des problèmes de hello outil d’importation/exportation Azure</span><span class="sxs-lookup"><span data-stu-id="1ddff-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="1ddff-104">Hello, outil de Microsoft Azure Import/Export renvoie des messages d’erreur s’il rencontre des problèmes.</span><span class="sxs-lookup"><span data-stu-id="1ddff-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="1ddff-105">Cette rubrique répertorie certains des problèmes courants que les utilisateurs peuvent rencontrer.</span><span class="sxs-lookup"><span data-stu-id="1ddff-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="1ddff-106">Une session de copie échoue, que faire ?</span><span class="sxs-lookup"><span data-stu-id="1ddff-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="1ddff-107">Lorsqu’une session de copie échoue, il existe deux possibilités :</span><span class="sxs-lookup"><span data-stu-id="1ddff-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="1ddff-108">Si l’erreur de hello est renouvelable, par exemple, si le partage de réseau hello était hors connexion pour une courte période et maintenant est en ligne, vous pouvez reprendre la session de copie hello.</span><span class="sxs-lookup"><span data-stu-id="1ddff-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="1ddff-109">Si l’erreur de hello n’est pas renouvelable, par exemple, si vous avez spécifié un répertoire du fichier source incorrect hello dans les paramètres de ligne de commande hello, vous devez la session de copie tooabort hello.</span><span class="sxs-lookup"><span data-stu-id="1ddff-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="1ddff-110">Consultez la page [Préparer des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md) pour plus d’informations sur la reprise et l’abandon de sessions de copie.</span><span class="sxs-lookup"><span data-stu-id="1ddff-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="1ddff-111">Je n’arrive pas à reprendre ou à abandonner une session de copie.</span><span class="sxs-lookup"><span data-stu-id="1ddff-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="1ddff-112">Si la session de copie hello est hello première session de copie pour un lecteur, message d’erreur hello doit indiquer : « hello première session de copie ne peut pas être repris ou abandonnée. »</span><span class="sxs-lookup"><span data-stu-id="1ddff-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="1ddff-113">Dans ce cas, vous pouvez supprimer l’ancien fichier journal de hello et réexécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="1ddff-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="1ddff-114">Si une session de copie n’est pas hello un premier pour un lecteur, il peut toujours être repris ou abandonnée.</span><span class="sxs-lookup"><span data-stu-id="1ddff-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="1ddff-115">J’ai perdu le fichier journal de hello, est-il possible de créer le travail de hello ?</span><span class="sxs-lookup"><span data-stu-id="1ddff-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="1ddff-116">fichier de journal Hello pour un lecteur contient des informations complètes de hello de la copie du lecteur de données toothis, et il est nécessaire tooadd plus lecteur toohello de fichiers et sera toocreate utilisé un travail d’importation.</span><span class="sxs-lookup"><span data-stu-id="1ddff-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="1ddff-117">Si le fichier journal de hello est perdu, vous devez tooredo toutes les sessions de copie hello pour le lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="1ddff-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1ddff-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ddff-118">Next steps</span></span>
 
* [<span data-ttu-id="1ddff-119">Configuration de l’outil d’importation/exportation azure hello</span><span class="sxs-lookup"><span data-stu-id="1ddff-119">Setting up hello azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="1ddff-120">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="1ddff-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="1ddff-121">Consultation de l’état du travail avec les fichiers journaux de copie</span><span class="sxs-lookup"><span data-stu-id="1ddff-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="1ddff-122">Réparation d’un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="1ddff-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="1ddff-123">Réparation d’un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="1ddff-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
