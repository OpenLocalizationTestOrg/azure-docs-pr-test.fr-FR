---
title: "Résolution des problèmes de l’outil Azure Import-Export | Microsoft Docs"
description: "Découvrez certains des problèmes courants que observés avec l’outil Azure Import-Export et comment les gérer."
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
ms.openlocfilehash: 7bfda602dbc0ea47828a7c9243b8b9b09ec78432
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="ba529-103">Résolution des problèmes associés à l’outil d’importation/d’exportation Azure</span><span class="sxs-lookup"><span data-stu-id="ba529-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="ba529-104">L’outil Microsoft Azure Import/Export renvoie des messages d’erreur s’il rencontre des problèmes.</span><span class="sxs-lookup"><span data-stu-id="ba529-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="ba529-105">Cette rubrique répertorie certains des problèmes courants que les utilisateurs peuvent rencontrer.</span><span class="sxs-lookup"><span data-stu-id="ba529-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="ba529-106">Une session de copie échoue, que faire ?</span><span class="sxs-lookup"><span data-stu-id="ba529-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="ba529-107">Lorsqu’une session de copie échoue, il existe deux possibilités :</span><span class="sxs-lookup"><span data-stu-id="ba529-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="ba529-108">Si une nouvelle tentative est possible, par exemple si le partage réseau était déconnecté pendant une courte période et qu’il est de nouveau en ligne, vous pouvez reprendre la session de copie.</span><span class="sxs-lookup"><span data-stu-id="ba529-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="ba529-109">Si l’erreur n’est pas récupérable, par exemple si vous avez spécifié un mauvais répertoire de fichier source dans les paramètres de ligne de commande, vous devez abandonner la session de copie.</span><span class="sxs-lookup"><span data-stu-id="ba529-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="ba529-110">Consultez la page [Préparer des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md) pour plus d’informations sur la reprise et l’abandon de sessions de copie.</span><span class="sxs-lookup"><span data-stu-id="ba529-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="ba529-111">Je n’arrive pas à reprendre ou à abandonner une session de copie.</span><span class="sxs-lookup"><span data-stu-id="ba529-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="ba529-112">S’il s’agit de la première session de copie d’un lecteur, le message d’erreur doit indiquer : « La première session de copie ne peut pas être reprise ou abandonnée ».</span><span class="sxs-lookup"><span data-stu-id="ba529-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="ba529-113">Dans ce cas, vous pouvez supprimer l’ancien fichier journal et réexécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="ba529-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="ba529-114">Si la session de copie n’est pas la première du lecteur, elle peut toujours être reprise ou abandonnée.</span><span class="sxs-lookup"><span data-stu-id="ba529-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="ba529-115">J’ai perdu le fichier journal, est-il quand même possible de créer le travail ?</span><span class="sxs-lookup"><span data-stu-id="ba529-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="ba529-116">Le fichier journal d’un lecteur contient les informations complètes de copie des données sur ce lecteur ; il est nécessaire pour ajouter d’autres fichiers au lecteur et sera utilisé pour créer un travail d’importation.</span><span class="sxs-lookup"><span data-stu-id="ba529-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="ba529-117">Si le fichier journal est perdu, vous devrez répéter toutes les sessions de copie du lecteur.</span><span class="sxs-lookup"><span data-stu-id="ba529-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ba529-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba529-118">Next steps</span></span>
 
* [<span data-ttu-id="ba529-119">Configuration de l’outil Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="ba529-119">Setting up the azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="ba529-120">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="ba529-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="ba529-121">Consultation de l’état du travail avec les fichiers journaux de copie</span><span class="sxs-lookup"><span data-stu-id="ba529-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="ba529-122">Réparation d’un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="ba529-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="ba529-123">Réparation d’un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="ba529-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
