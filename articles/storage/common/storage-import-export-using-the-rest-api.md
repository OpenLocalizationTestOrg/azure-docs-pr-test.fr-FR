---
title: aaaUsing hello API REST du service Azure Import/Export | Documents Microsoft
description: "Découvrez où toofind des ressources pour l’utilisation de hello Azure Import/Export service API REST, y compris les deux documents de référence tooand de procédure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="c2cee-103">À l’aide des API REST du service Azure Import/Export hello</span><span class="sxs-lookup"><span data-stu-id="c2cee-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="c2cee-104">Hello service Microsoft Azure Import/Export expose un contrôle par programmation de tooenable d’API REST de travaux d’importation/exportation.</span><span class="sxs-lookup"><span data-stu-id="c2cee-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="c2cee-105">Vous pouvez utiliser les API REST de hello tooperform hello toutes les opérations que vous pouvez effectuer avec hello importation/exportation [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c2cee-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c2cee-106">En outre, vous pouvez utiliser hello API REST tooperform certaines opérations granulaires, comme l’interrogation de hello Pourcentage achèvement d’une tâche, ce qui n’est pas disponible actuellement dans hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c2cee-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which is not currently available in hello Azure classic portal.</span></span>

<span data-ttu-id="c2cee-107">Consultez [à l’aide du service d’importation/exportation de Microsoft Azure hello données tooTransfer tooBlob stockage](../storage-import-export-service.md) pour une vue d’ensemble du service d’importation/exportation hello et un didacticiel qui montre comment toouse hello toocreate portail classique et gérer l’importation travaux et d’exportation.</span><span class="sxs-lookup"><span data-stu-id="c2cee-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](../storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="c2cee-108">Points de terminaison de service</span><span class="sxs-lookup"><span data-stu-id="c2cee-108">Service endpoints</span></span>

<span data-ttu-id="c2cee-109">Hello service Azure Import/Export est un fournisseur de ressources pour le Gestionnaire de ressources Azure et fournit un ensemble d’API REST à hello après le point de terminaison HTTPS pour la gestion des travaux d’importation/exportation :</span><span class="sxs-lookup"><span data-stu-id="c2cee-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="c2cee-110">Contrôle de version</span><span class="sxs-lookup"><span data-stu-id="c2cee-110">Versioning</span></span>

<span data-ttu-id="c2cee-111">Demandes de toohello service d’importation/exportation doit spécifier hello `api-version` paramètre et définissez sa valeur trop`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="c2cee-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="c2cee-112">Opérations du service Import/Export</span><span class="sxs-lookup"><span data-stu-id="c2cee-112">Import/Export service operations</span></span>

[<span data-ttu-id="c2cee-113">Création d’un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="c2cee-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="c2cee-114">Création d’un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="c2cee-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="c2cee-115">Récupération des informations d’état d’un travail</span><span class="sxs-lookup"><span data-stu-id="c2cee-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="c2cee-116">Énumération des travaux</span><span class="sxs-lookup"><span data-stu-id="c2cee-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="c2cee-117">Annulation et suppression de travaux</span><span class="sxs-lookup"><span data-stu-id="c2cee-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="c2cee-118">Sauvegarde de manifestes de lecteur</span><span class="sxs-lookup"><span data-stu-id="c2cee-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="c2cee-119">Diagnostic et récupération d’erreur pour les travaux d’importation / exportation</span><span class="sxs-lookup"><span data-stu-id="c2cee-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="c2cee-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c2cee-120">Next steps</span></span>

* [<span data-ttu-id="c2cee-121">API REST d’importation/exportation de stockage</span><span class="sxs-lookup"><span data-stu-id="c2cee-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
