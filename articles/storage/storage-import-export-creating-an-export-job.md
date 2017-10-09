---
title: "aaaCreate une exportation de la tâche d’importation/exportation Azure | Documents Microsoft"
description: "Découvrez comment toocreate une exportation de la tâche pour hello service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="76765-103">Création d’un travail d’exportation pour hello service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="76765-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="76765-104">Création d’un travail d’exportation pour le service de Microsoft Azure Import/Export hello à l’aide des API REST de hello implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76765-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="76765-105">En sélectionnant hello tooexport des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="76765-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="76765-106">Obtention d’un emplacement d’expédition.</span><span class="sxs-lookup"><span data-stu-id="76765-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="76765-107">Création de travail d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="76765-107">Creating hello export job.</span></span>

-   <span data-ttu-id="76765-108">Expédition tooMicrosoft de vos lecteurs vides via un service de transport pris en charge.</span><span class="sxs-lookup"><span data-stu-id="76765-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="76765-109">Mise à jour le travail d’exportation hello avec les informations de package hello.</span><span class="sxs-lookup"><span data-stu-id="76765-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="76765-110">Lecteurs hello réception expédiés par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76765-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="76765-111">Consultez [à l’aide du service d’importation/exportation de Windows Azure hello données tooTransfer tooBlob stockage](storage-import-export-service.md) pour une vue d’ensemble du service d’importation/exportation hello et un didacticiel qui montre comment toouse hello [portail Azure](https://portal.azure.com/) toocreate et gérer l’importation et exportation des travaux.</span><span class="sxs-lookup"><span data-stu-id="76765-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="76765-112">Sélection d’objets BLOB tooexport</span><span class="sxs-lookup"><span data-stu-id="76765-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="76765-113">toocreate un travail d’exportation, vous devez tooprovide une liste d’objets BLOB que vous souhaitez tooexport à partir de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="76765-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="76765-114">Il existe plusieurs façons tooselect BLOB toobe exporté :</span><span class="sxs-lookup"><span data-stu-id="76765-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="76765-115">Vous pouvez utiliser un tooselect de chemin d’accès relatif blob un seul objet blob et tous ses instantanés.</span><span class="sxs-lookup"><span data-stu-id="76765-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="76765-116">Vous pouvez utiliser un tooselect de chemin d’accès relatif blob un seul objet blob à l’exclusion de ses instantanés.</span><span class="sxs-lookup"><span data-stu-id="76765-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="76765-117">Vous pouvez utiliser un chemin d’accès de l’objet blob relatif et un tooselect de temps un seul instantané de capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="76765-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="76765-118">Vous pouvez utiliser un tooselect de préfixe d’objet blob tous les objets BLOB et instantanés avec hello préfixe.</span><span class="sxs-lookup"><span data-stu-id="76765-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="76765-119">Vous pouvez exporter tous les objets BLOB et captures instantanées dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="76765-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="76765-120">Pour plus d’informations sur la spécification d’objets BLOB tooexport, consultez hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération.</span><span class="sxs-lookup"><span data-stu-id="76765-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="76765-121">Obtention de votre emplacement d’expédition</span><span class="sxs-lookup"><span data-stu-id="76765-121">Obtaining your shipping location</span></span>
<span data-ttu-id="76765-122">Avant de créer un travail d’exportation, vous avez besoin tooobtain un nom d’emplacement d’expédition et l’adresse en appelant hello [obtenir l’emplacement](https://portal.azure.com) ou [liste des emplacements](/rest/api/storageimportexport/listlocations) opération.</span><span class="sxs-lookup"><span data-stu-id="76765-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="76765-123">`List Locations` renvoie une liste d’emplacements et leurs adresses postales.</span><span class="sxs-lookup"><span data-stu-id="76765-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="76765-124">Vous pouvez sélectionner un emplacement à partir de hello retourné liste et votre adresse de toothat de disques durs de livraison.</span><span class="sxs-lookup"><span data-stu-id="76765-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="76765-125">Vous pouvez également utiliser hello `Get Location` hello de tooobtain opération copie les adresses pour un emplacement spécifique directement.</span><span class="sxs-lookup"><span data-stu-id="76765-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="76765-126">Suivez les étapes de hello sous l’emplacement d’expédition tooobtain hello :</span><span class="sxs-lookup"><span data-stu-id="76765-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="76765-127">Identifier le nom hello d’emplacement hello de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="76765-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="76765-128">Cette valeur peut être trouvée sous hello **emplacement** champ du compte de stockage hello **tableau de bord** dans classic hello portail ou interrogé à l’aide d’opération de l’API de gestion des services hello [obtenir Propriétés de compte de stockage](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="76765-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="76765-129">Récupérer emplacement hello qui sont disponibles tooprocess ce compte de stockage en appelant hello `Get Location` opération.</span><span class="sxs-lookup"><span data-stu-id="76765-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="76765-130">Si hello `AlternateLocations` propriété d’emplacement de hello contient l’emplacement hello lui-même, puis il est OK toouse cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="76765-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="76765-131">Sinon, appelez hello `Get Location` opération en utilisant un des emplacements de remplacement hello.</span><span class="sxs-lookup"><span data-stu-id="76765-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="76765-132">emplacement d’origine de Hello peut être fermé temporairement pour maintenance.</span><span class="sxs-lookup"><span data-stu-id="76765-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="76765-133">Création du travail d’exportation hello</span><span class="sxs-lookup"><span data-stu-id="76765-133">Creating hello export job</span></span>
 <span data-ttu-id="76765-134">travail d’exportation toocreate hello, appel hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération.</span><span class="sxs-lookup"><span data-stu-id="76765-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="76765-135">Vous devez hello tooprovide informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="76765-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="76765-136">Un nom pour la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="76765-136">A name for hello job.</span></span>

-   <span data-ttu-id="76765-137">nom de compte de stockage Hello.</span><span class="sxs-lookup"><span data-stu-id="76765-137">hello storage account name.</span></span>

-   <span data-ttu-id="76765-138">Hello copie le nom de l’emplacement, obtenu à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="76765-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="76765-139">Type de travail (exportation).</span><span class="sxs-lookup"><span data-stu-id="76765-139">A job type (Export).</span></span>

-   <span data-ttu-id="76765-140">adresse de retour Hello laquelle hello lecteurs doivent être envoyés une fois le travail d’exportation hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="76765-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="76765-141">Bonjour toobe liste d’objets BLOB (ou préfixes d’objet blob) exporté.</span><span class="sxs-lookup"><span data-stu-id="76765-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="76765-142">Expédition de vos disques</span><span class="sxs-lookup"><span data-stu-id="76765-142">Shipping your drives</span></span>
 <span data-ttu-id="76765-143">Ensuite, utilisez hello outil d’importation/exportation Azure toodetermine hello nombre de lecteurs que vous devez toosend, en fonction de BLOB hello que vous avez sélectionné toobe exporté et hello taille du lecteur.</span><span class="sxs-lookup"><span data-stu-id="76765-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="76765-144">Consultez hello [référence de l’outil Azure Import/Export](storage-import-export-tool-how-to-v1.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="76765-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="76765-145">Lecteurs hello de package dans un même package et expédiez-les toohello adresse obtenue Bonjour étape antérieure.</span><span class="sxs-lookup"><span data-stu-id="76765-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="76765-146">Notez hello suivi du numéro de votre package pour l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="76765-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="76765-147">Vous devez expédier vos disques via un service de transport pris en charge, qui vous fournira un numéro de suivi pour votre colis.</span><span class="sxs-lookup"><span data-stu-id="76765-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="76765-148">Mise à jour de la tâche d’exportation hello avec les informations de package</span><span class="sxs-lookup"><span data-stu-id="76765-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="76765-149">Après avoir configuré votre numéro de suivi, appelez hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) nom d’opération tooupdated hello transporteur et numéro hello travail de suivi.</span><span class="sxs-lookup"><span data-stu-id="76765-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="76765-150">Vous pouvez éventuellement spécifier le nombre de hello de lecteurs, l’adresse de retour hello et hello date d’expédition.</span><span class="sxs-lookup"><span data-stu-id="76765-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="76765-151">Réception hello package</span><span class="sxs-lookup"><span data-stu-id="76765-151">Receiving hello package</span></span>
 <span data-ttu-id="76765-152">Une fois votre travail d’exportation a été traité, vos lecteurs seront affichera tooyou avec vos données chiffrées.</span><span class="sxs-lookup"><span data-stu-id="76765-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="76765-153">Vous pouvez récupérer la clé de BitLocker hello pour chacun des lecteurs hello en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération.</span><span class="sxs-lookup"><span data-stu-id="76765-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="76765-154">Vous pouvez déverrouiller lecteur hello à l’aide de la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="76765-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="76765-155">fichier manifeste de lecteur Hello sur chaque lecteur contient hello liste des fichiers sur le lecteur de hello, ainsi que d’adresse d’objet blob d’origine hello pour chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="76765-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76765-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76765-156">Next steps</span></span>

* [<span data-ttu-id="76765-157">À l’aide des API REST du service importation/exportation hello</span><span class="sxs-lookup"><span data-stu-id="76765-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
