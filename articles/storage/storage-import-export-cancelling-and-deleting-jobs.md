---
title: aaaCancel et supprimer un travail Azure Import/Export | Documents Microsoft
description: "Découvrez comment toocancel et supprimer des travaux pour hello service Microsoft Azure Import/Export."
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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="4acef-103">Annulation et suppression de travaux du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="4acef-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="4acef-104">Vous pouvez demander qu’une tâche annulée avant qu’il soit Bonjour `Packaging` état en appelant hello [propriétés de tâche de mise à jour](/rest/api/storageimportexport/jobs#Jobs_Update) opération et le paramètre hello `CancelRequested` élément trop`true`.</span><span class="sxs-lookup"><span data-stu-id="4acef-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="4acef-105">tâche de Hello sera annulée de manière optimale.</span><span class="sxs-lookup"><span data-stu-id="4acef-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="4acef-106">Si les lecteurs sont en cours de hello de transfert de données, les données peuvent continuer toobe transférée même après que l’annulation a été demandée.</span><span class="sxs-lookup"><span data-stu-id="4acef-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="4acef-107">Un travail annulé déplacera toohello `Completed` d’état et conservé pendant 90 jours, à quel point il sera supprimé.</span><span class="sxs-lookup"><span data-stu-id="4acef-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="4acef-108">toodelete un travail, appel hello [supprimer le travail](/rest/api/storageimportexport/jobs#Jobs_Delete) opération avant que le travail de hello a été expédiée (*c'est-à-dire*, tandis que le travail de hello est Bonjour `Creating` état).</span><span class="sxs-lookup"><span data-stu-id="4acef-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="4acef-109">Vous pouvez également supprimer un travail lorsqu’il est Bonjour `Completed` état.</span><span class="sxs-lookup"><span data-stu-id="4acef-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="4acef-110">Après la suppression d’un travail, ses informations et l’état ne sont plus accessibles via l’API REST de hello ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4acef-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4acef-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4acef-111">Next steps</span></span>

* [<span data-ttu-id="4acef-112">À l’aide des API REST du service importation/exportation hello</span><span class="sxs-lookup"><span data-stu-id="4acef-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
