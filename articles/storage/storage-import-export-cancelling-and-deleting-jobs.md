---
title: "Annulation et suppression d’un travail d’importation Azure Import/Export | Microsoft Docs"
description: "Découvrez comment annuler et supprimer des travaux pour le service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="69917-103">Annulation et suppression de travaux du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="69917-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="69917-104">Vous pouvez demander qu’un travail soit annulé avant qu’il ne soit dans l’état `Packaging` en appelant l’opération [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) et en définissant l’élément `CancelRequested` sur `true`.</span><span class="sxs-lookup"><span data-stu-id="69917-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="69917-105">Le travail sera annulé de manière optimale.</span><span class="sxs-lookup"><span data-stu-id="69917-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="69917-106">Si des données sont en cours de transfert sur les disques, cette opération peut se poursuivre même après que l’annulation ait été demandée.</span><span class="sxs-lookup"><span data-stu-id="69917-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="69917-107">Un travail annulé passe à l’état `Completed` et sera conservé pendant 90 jours, après quoi il sera supprimé.</span><span class="sxs-lookup"><span data-stu-id="69917-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="69917-108">Pour supprimer un travail, appelez l’opération [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) avant que le travail ne soit expédié (*c’est-à-dire*, pendant que le travail est dans l’état `Creating`).</span><span class="sxs-lookup"><span data-stu-id="69917-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="69917-109">Vous pouvez également supprimer un travail lorsqu’il se trouve dans l’état `Completed`.</span><span class="sxs-lookup"><span data-stu-id="69917-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="69917-110">Après la suppression d’un travail, ses informations et son état ne sont plus accessibles via l’API REST ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="69917-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69917-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69917-111">Next steps</span></span>

* [<span data-ttu-id="69917-112">Utilisation de l’API REST du service Import/Export</span><span class="sxs-lookup"><span data-stu-id="69917-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
