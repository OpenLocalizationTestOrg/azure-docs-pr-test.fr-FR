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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="57c33-103">Annulation et suppression de travaux du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="57c33-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="57c33-104">toorequest qu’un travail annulé avant qu’il est Bonjour `Packaging` état, l’appel hello [propriétés de tâche de mise à jour](/rest/api/storageimportexport/jobs#Jobs_Update) opération et ensemble hello `CancelRequested` élément trop`true`.</span><span class="sxs-lookup"><span data-stu-id="57c33-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="57c33-105">travail de Hello est annulé sur une base du meilleur effort.</span><span class="sxs-lookup"><span data-stu-id="57c33-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="57c33-106">Si les lecteurs sont en cours de hello de transfert de données, les données peuvent continuer toobe transférée même après que l’annulation a été demandée.</span><span class="sxs-lookup"><span data-stu-id="57c33-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="57c33-107">Un travail annulé est déplacé toohello `Completed` d’état et doivent être conservées pendant 90 jours, à quel point il est supprimé.</span><span class="sxs-lookup"><span data-stu-id="57c33-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="57c33-108">toodelete un travail, appel hello [supprimer le travail](/rest/api/storageimportexport/jobs#Jobs_Delete) opération avant que le travail de hello a été expédiée (autrement dit, pendant le travail de hello hello `Creating` état).</span><span class="sxs-lookup"><span data-stu-id="57c33-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="57c33-109">Vous pouvez également supprimer un travail lorsqu’il est Bonjour `Completed` état.</span><span class="sxs-lookup"><span data-stu-id="57c33-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="57c33-110">Après la suppression d’un travail, ses informations et l’état ne sont plus accessibles via l’API REST de hello ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="57c33-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57c33-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57c33-111">Next steps</span></span>

* [<span data-ttu-id="57c33-112">À l’aide des API REST du service importation/exportation hello</span><span class="sxs-lookup"><span data-stu-id="57c33-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
