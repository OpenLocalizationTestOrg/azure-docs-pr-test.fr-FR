---
title: "aaaDiagnostics et la récupération pour les travaux d’importation/exportation Azure | Documents Microsoft"
description: "Découvrez comment les tâches de service de la journalisation documentée tooenable pour Microsoft Azure Import/Export."
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
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="f6635-103">Diagnostic et récupération d’erreur pour les travaux Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="f6635-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="f6635-104">Pour chaque lecteur traité, hello service Azure Import/Export crée un journal des erreurs dans le compte de stockage hello associé.</span><span class="sxs-lookup"><span data-stu-id="f6635-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="f6635-105">Vous pouvez également activer la journalisation détaillée en définissant un hello `LogLevel` propriété trop`Verbose` lors de l’appel hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span><span class="sxs-lookup"><span data-stu-id="f6635-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="f6635-106">Par défaut, les journaux sont écrits conteneur tooa nommé `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="f6635-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="f6635-107">Vous pouvez spécifier un nom différent en définissant la hello `DiagnosticsPath` propriété lors de l’appel hello `Put Job` ou `Update Job Properties` operations.</span><span class="sxs-lookup"><span data-stu-id="f6635-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="f6635-108">Hello journaux sont stockés en tant qu’objets BLOB de blocs avec hello respectent les conventions d’affectation de noms : `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="f6635-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="f6635-109">Vous pouvez récupérer hello URI des journaux hello pour un travail en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération.</span><span class="sxs-lookup"><span data-stu-id="f6635-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="f6635-110">Hello URI pour la journalisation documentée hello est retourné dans hello `VerboseLogUri` propriété pour chaque lecteur, alors que hello URI hello journal des erreurs est retourné dans hello `ErrorLogUri` propriété.</span><span class="sxs-lookup"><span data-stu-id="f6635-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="f6635-111">Vous pouvez utiliser hello journalisation hello tooidentify de données suivants.</span><span class="sxs-lookup"><span data-stu-id="f6635-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="f6635-112">Erreurs de disque</span><span class="sxs-lookup"><span data-stu-id="f6635-112">Drive errors</span></span>

<span data-ttu-id="f6635-113">Hello éléments suivants est classé en tant qu’erreurs de lecteur :</span><span class="sxs-lookup"><span data-stu-id="f6635-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="f6635-114">Erreurs dans l’accès ou hello lors de la lecture du fichier manifeste</span><span class="sxs-lookup"><span data-stu-id="f6635-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="f6635-115">Clés BitLocker incorrectes</span><span class="sxs-lookup"><span data-stu-id="f6635-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="f6635-116">Erreurs de lecture/écriture sur le disque</span><span class="sxs-lookup"><span data-stu-id="f6635-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="f6635-117">Erreurs d’objet blob</span><span class="sxs-lookup"><span data-stu-id="f6635-117">Blob errors</span></span>

<span data-ttu-id="f6635-118">Hello éléments suivants est classée comme des erreurs de l’objet blob :</span><span class="sxs-lookup"><span data-stu-id="f6635-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="f6635-119">Objet blob ou nom incorrect ou conflictuel</span><span class="sxs-lookup"><span data-stu-id="f6635-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="f6635-120">Fichiers manquants</span><span class="sxs-lookup"><span data-stu-id="f6635-120">Missing files</span></span>

-   <span data-ttu-id="f6635-121">Objet blob introuvable</span><span class="sxs-lookup"><span data-stu-id="f6635-121">Blob not found</span></span>

-   <span data-ttu-id="f6635-122">Fichiers tronqués (fichiers hello sur le disque de hello sont plus petits que ceux spécifiés dans le manifeste de hello)</span><span class="sxs-lookup"><span data-stu-id="f6635-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="f6635-123">Contenu de fichier endommagé (pour les travaux d’importation, détecté par une incompatibilité de la somme de contrôle MD5)</span><span class="sxs-lookup"><span data-stu-id="f6635-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="f6635-124">Fichiers de propriétés et de métadonnées blob endommagés (détectés par une incompatibilité de la somme de contrôle MD5)</span><span class="sxs-lookup"><span data-stu-id="f6635-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="f6635-125">Schéma incorrect pour les propriétés d’objet blob hello et/ou les fichiers de métadonnées</span><span class="sxs-lookup"><span data-stu-id="f6635-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="f6635-126">Il peut arriver dans laquelle certaines parties d’un travail d’importation ou d’exportation n’aboutissent pas, alors que hello globale travail est terminé.</span><span class="sxs-lookup"><span data-stu-id="f6635-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="f6635-127">Dans ce cas, vous pouvez soit charger ou télécharger hello manquant hello données sur le réseau, ou vous pouvez créer les données de salutation un nouveau travail tootransfer.</span><span class="sxs-lookup"><span data-stu-id="f6635-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="f6635-128">Consultez hello [référence de l’outil Azure Import/Export](storage-import-export-tool-how-to-v1.md) toolearn comment toorepair hello des données sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="f6635-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6635-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6635-129">Next steps</span></span>

* [<span data-ttu-id="f6635-130">À l’aide des API REST du service importation/exportation hello</span><span class="sxs-lookup"><span data-stu-id="f6635-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
