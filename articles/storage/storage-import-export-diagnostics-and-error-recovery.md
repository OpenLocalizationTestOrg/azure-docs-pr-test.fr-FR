---
title: "Diagnostic et récupération d’erreur pour les travaux Azure Import/Export | Microsoft Docs"
description: "Découvrez comment activer la journalisation documentée pour les travaux du service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="2fcb7-103">Diagnostic et récupération d’erreur pour les travaux Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="2fcb7-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="2fcb7-104">Pour chaque disque traité, le service Azure Import/Export crée un journal d’erreurs dans le compte de stockage associé.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="2fcb7-105">Vous pouvez également activer la journalisation documentée en définissant la propriété `LogLevel` sur `Verbose` lors de l’appel des opérations [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="2fcb7-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="2fcb7-106">Par défaut, les journaux sont écrits dans un conteneur nommé `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="2fcb7-107">Vous pouvez spécifier un autre nom en définissant la propriété `DiagnosticsPath` lors de l’appel des opérations `Put Job` ou `Update Job Properties`.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="2fcb7-108">Les journaux sont stockés sous la forme d’objets blob de blocs avec la convention d’affectation de noms suivante : `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="2fcb7-109">Vous pouvez récupérer l’URI des journaux pour un travail en appelant l’opération [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="2fcb7-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="2fcb7-110">L’URI pour le journal documenté est retourné dans la propriété `VerboseLogUri` pour chaque disque, alors que l’URI pour le journal d’erreurs est retourné dans la propriété `ErrorLogUri`.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="2fcb7-111">Vous pouvez utiliser les données de journalisation pour identifier les problèmes suivants.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="2fcb7-112">Erreurs de disque</span><span class="sxs-lookup"><span data-stu-id="2fcb7-112">Drive errors</span></span>

<span data-ttu-id="2fcb7-113">Les éléments suivants sont classés comme des erreurs de lecteur :</span><span class="sxs-lookup"><span data-stu-id="2fcb7-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="2fcb7-114">Erreurs d’accès ou de lecture du fichier de manifeste</span><span class="sxs-lookup"><span data-stu-id="2fcb7-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="2fcb7-115">Clés BitLocker incorrectes</span><span class="sxs-lookup"><span data-stu-id="2fcb7-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="2fcb7-116">Erreurs de lecture/écriture sur le disque</span><span class="sxs-lookup"><span data-stu-id="2fcb7-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="2fcb7-117">Erreurs d’objet blob</span><span class="sxs-lookup"><span data-stu-id="2fcb7-117">Blob errors</span></span>

<span data-ttu-id="2fcb7-118">Les éléments suivants sont classés comme des erreurs d’objet blob :</span><span class="sxs-lookup"><span data-stu-id="2fcb7-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="2fcb7-119">Objet blob ou nom incorrect ou conflictuel</span><span class="sxs-lookup"><span data-stu-id="2fcb7-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="2fcb7-120">Fichiers manquants</span><span class="sxs-lookup"><span data-stu-id="2fcb7-120">Missing files</span></span>

-   <span data-ttu-id="2fcb7-121">Objet blob introuvable</span><span class="sxs-lookup"><span data-stu-id="2fcb7-121">Blob not found</span></span>

-   <span data-ttu-id="2fcb7-122">Fichiers tronqués (les fichiers sur le disque sont plus petits que ceux spécifiés dans le manifeste)</span><span class="sxs-lookup"><span data-stu-id="2fcb7-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="2fcb7-123">Contenu de fichier endommagé (pour les travaux d’importation, détecté par une incompatibilité de la somme de contrôle MD5)</span><span class="sxs-lookup"><span data-stu-id="2fcb7-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="2fcb7-124">Fichiers de propriétés et de métadonnées blob endommagés (détectés par une incompatibilité de la somme de contrôle MD5)</span><span class="sxs-lookup"><span data-stu-id="2fcb7-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="2fcb7-125">Schéma incorrect des fichiers de propriétés et/ou de métadonnées blob</span><span class="sxs-lookup"><span data-stu-id="2fcb7-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="2fcb7-126">Il peut arriver que certaines parties d’un travail d’importation ou d’exportation n’aboutisse pas, alors que l’ensemble du travail est terminé.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="2fcb7-127">Dans ce cas, vous pouvez charger ou télécharger les parties manquantes des données sur le réseau, ou vous pouvez créer un nouveau travail pour transférer les données.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="2fcb7-128">Consultez la [référence sur l’outil Azure Import/Export](storage-import-export-tool-how-to-v1.md) pour découvrir comment corriger les données sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="2fcb7-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fcb7-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2fcb7-129">Next steps</span></span>

* [<span data-ttu-id="2fcb7-130">Utilisation de l’API REST du service Import/Export</span><span class="sxs-lookup"><span data-stu-id="2fcb7-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
