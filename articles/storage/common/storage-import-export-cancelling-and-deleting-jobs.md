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
ms.openlocfilehash: 1e989c72fc03697bf6d2e515ff53003703665d1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="8df3c-103">Annulation et suppression de travaux du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="8df3c-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="8df3c-104">Pour demander qu’un travail soit annulé avant d’être à l’état `Packaging`, appelez l’opération [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) et définissez l’élément `CancelRequested` sur `true`.</span><span class="sxs-lookup"><span data-stu-id="8df3c-104">To request that a job be canceled before it is in the `Packaging` state, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="8df3c-105">Le travail est annulé de manière optimale.</span><span class="sxs-lookup"><span data-stu-id="8df3c-105">The job is canceled on a best-effort basis.</span></span> <span data-ttu-id="8df3c-106">Si des données sont en cours de transfert sur les disques, cette opération peut se poursuivre même après que l’annulation ait été demandée.</span><span class="sxs-lookup"><span data-stu-id="8df3c-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="8df3c-107">Un travail annulé passe à l’état `Completed` et est conservé pendant 90 jours. Après quoi, il est supprimé.</span><span class="sxs-lookup"><span data-stu-id="8df3c-107">A canceled job is moved to the `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="8df3c-108">Pour supprimer un travail, appelez l’opération [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) avant que le travail soit expédié (c’est-à-dire, pendant que le travail est à l’état `Creating`).</span><span class="sxs-lookup"><span data-stu-id="8df3c-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (that is, while the job is in the `Creating` state).</span></span> <span data-ttu-id="8df3c-109">Vous pouvez également supprimer un travail lorsqu’il se trouve dans l’état `Completed`.</span><span class="sxs-lookup"><span data-stu-id="8df3c-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="8df3c-110">Une fois le travail supprimé, ses informations et son état ne sont plus accessibles via l’API REST ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8df3c-110">After a job is deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df3c-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8df3c-111">Next steps</span></span>

* [<span data-ttu-id="8df3c-112">Utilisation de l’API REST du service Import/Export</span><span class="sxs-lookup"><span data-stu-id="8df3c-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
