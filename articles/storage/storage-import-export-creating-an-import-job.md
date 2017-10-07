---
title: "aaaCreate un travail d’importation pour Azure Import/Export | Documents Microsoft"
description: "Découvrez comment toocreate une importation de hello service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="a59bf-103">Création d’un travail d’importation pour hello service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="a59bf-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="a59bf-104">Création d’un travail d’importation pour le service de Microsoft Azure Import/Export hello à l’aide des API REST de hello implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a59bf-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="a59bf-105">Préparation des lecteurs à hello outil d’importation/exportation Azure.</span><span class="sxs-lookup"><span data-stu-id="a59bf-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="a59bf-106">Obtenir le lecteur hello tooship hello emplacement toowhich.</span><span class="sxs-lookup"><span data-stu-id="a59bf-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="a59bf-107">Création de tâche d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-107">Creating hello import job.</span></span>

-   <span data-ttu-id="a59bf-108">Hello d’expédition des lecteurs tooMicrosoft via un service de transport pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a59bf-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="a59bf-109">Mise à jour le travail d’importation hello avec hello détails de l’expédition.</span><span class="sxs-lookup"><span data-stu-id="a59bf-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="a59bf-110">Consultez [à l’aide du service d’importation/exportation de Microsoft Azure hello données tooTransfer tooBlob stockage](storage-import-export-service.md) pour une vue d’ensemble du service d’importation/exportation hello et un didacticiel qui montre comment toouse hello [portail Azure](https://portal.azure.com/) toocreate et gérer l’importation et exportation des travaux.</span><span class="sxs-lookup"><span data-stu-id="a59bf-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="a59bf-111">Préparation des lecteurs à hello outil d’importation/exportation Azure</span><span class="sxs-lookup"><span data-stu-id="a59bf-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="a59bf-112">Hello étapes tooprepare lecteurs pour un travail d’importation sont hello même si vous créez hello portal de hello jobvia ou via hello API REST.</span><span class="sxs-lookup"><span data-stu-id="a59bf-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="a59bf-113">Voici une brève présentation de la préparation du disque.</span><span class="sxs-lookup"><span data-stu-id="a59bf-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="a59bf-114">Consultez toohello [Azure Import-ExportTool référence](storage-import-export-tool-how-to-v1.md) pour des instructions complètes.</span><span class="sxs-lookup"><span data-stu-id="a59bf-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="a59bf-115">Vous pouvez télécharger hello outil d’importation/exportation Azure [ici](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="a59bf-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="a59bf-116">La préparation de votre disque implique :</span><span class="sxs-lookup"><span data-stu-id="a59bf-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="a59bf-117">Identification hello toobe de données importée.</span><span class="sxs-lookup"><span data-stu-id="a59bf-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="a59bf-118">Identification des objets BLOB de destination hello dans le stockage Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="a59bf-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="a59bf-119">À l’aide de toocopy d’outil d’importation/exportation Azure hello tooone de vos données ou de plusieurs disques durs.</span><span class="sxs-lookup"><span data-stu-id="a59bf-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="a59bf-120">Hello, outil d’importation/exportation Azure génèrera également un fichier manifeste pour chacun des lecteurs de hello lors de sa préparation.</span><span class="sxs-lookup"><span data-stu-id="a59bf-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="a59bf-121">Un fichier de manifeste contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a59bf-121">A manifest file contains:</span></span>

-   <span data-ttu-id="a59bf-122">Énumération de tous les fichiers de hello prévus pour le téléchargement et mappages hello à partir de ces tooblobs de fichiers.</span><span class="sxs-lookup"><span data-stu-id="a59bf-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="a59bf-123">Sommes de contrôle des segments hello de chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="a59bf-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="a59bf-124">Informations sur les tooassociate de métadonnées et propriétés hello avec chaque objet blob.</span><span class="sxs-lookup"><span data-stu-id="a59bf-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="a59bf-125">Une liste des hello action tootake si un objet blob qui est en cours de téléchargement a hello même nom qu’un objet blob existant dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="a59bf-126">Les options possibles sont : a) remplacer l’objet blob de hello avec fichier de hello, (b) conserver l’objet blob existant de hello et ignorer le téléchargement du fichier de hello, c) ajouter un nom de toohello suffixe afin qu’il n’est pas en conflit avec d’autres fichiers.</span><span class="sxs-lookup"><span data-stu-id="a59bf-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="a59bf-127">Obtention de votre emplacement d’expédition</span><span class="sxs-lookup"><span data-stu-id="a59bf-127">Obtaining your shipping location</span></span>

<span data-ttu-id="a59bf-128">Avant de créer un travail d’importation, vous avez besoin tooobtain un nom d’emplacement d’expédition et l’adresse en appelant hello [liste des emplacements](/rest/api/storageimportexport/listlocations) opération.</span><span class="sxs-lookup"><span data-stu-id="a59bf-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="a59bf-129">`List Locations` renvoie une liste d’emplacements et leurs adresses postales.</span><span class="sxs-lookup"><span data-stu-id="a59bf-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="a59bf-130">Vous pouvez sélectionner un emplacement à partir de hello retourné liste et votre adresse de toothat de disques durs de livraison.</span><span class="sxs-lookup"><span data-stu-id="a59bf-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="a59bf-131">Vous pouvez également utiliser hello `Get Location` hello de tooobtain opération copie les adresses pour un emplacement spécifique directement.</span><span class="sxs-lookup"><span data-stu-id="a59bf-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="a59bf-132">Suivez les étapes de hello sous l’emplacement d’expédition tooobtain hello :</span><span class="sxs-lookup"><span data-stu-id="a59bf-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="a59bf-133">Identifier le nom hello d’emplacement hello de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a59bf-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="a59bf-134">Cette valeur peut être trouvée sous hello **emplacement** champ du compte de stockage hello **tableau de bord** Bonjour portail Azure ou interrogé à l’aide d’opération de l’API de gestion des services hello [obtenir le stockage Propriétés de compte](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="a59bf-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="a59bf-135">Récupérer emplacement hello tooprocess disponibles à ce compte de stockage en appelant hello `Get Location` opération.</span><span class="sxs-lookup"><span data-stu-id="a59bf-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="a59bf-136">Si hello `AlternateLocations` propriété d’emplacement de hello contient l’emplacement hello lui-même, puis il est OK toouse cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="a59bf-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="a59bf-137">Sinon, appelez hello `Get Location` opération en utilisant un des emplacements de remplacement hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="a59bf-138">emplacement d’origine de Hello peut être fermé temporairement pour maintenance.</span><span class="sxs-lookup"><span data-stu-id="a59bf-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="a59bf-139">Création du travail d’importation hello</span><span class="sxs-lookup"><span data-stu-id="a59bf-139">Creating hello import job</span></span>
<span data-ttu-id="a59bf-140">travail d’importation toocreate hello, appel hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération.</span><span class="sxs-lookup"><span data-stu-id="a59bf-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="a59bf-141">Vous devez hello tooprovide informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a59bf-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="a59bf-142">Un nom pour la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-142">A name for hello job.</span></span>

-   <span data-ttu-id="a59bf-143">nom de compte de stockage Hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-143">hello storage account name.</span></span>

-   <span data-ttu-id="a59bf-144">Hello obtenu à l’étape précédente de hello nom de l’emplacement d’expédition.</span><span class="sxs-lookup"><span data-stu-id="a59bf-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="a59bf-145">Type de travail (importation).</span><span class="sxs-lookup"><span data-stu-id="a59bf-145">A job type (Import).</span></span>

-   <span data-ttu-id="a59bf-146">adresse de retour Hello laquelle hello lecteurs doivent être envoyés une fois le travail d’importation hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="a59bf-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="a59bf-147">liste Hello de lecteurs dans la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-147">hello list of drives in hello job.</span></span> <span data-ttu-id="a59bf-148">Pour chaque lecteur, vous devez inclure hello informations a été obtenues pendant l’étape de préparation du lecteur hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a59bf-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="a59bf-149">Id de lecteur Hello</span><span class="sxs-lookup"><span data-stu-id="a59bf-149">hello drive Id</span></span>

    -   <span data-ttu-id="a59bf-150">clé de BitLocker Hello</span><span class="sxs-lookup"><span data-stu-id="a59bf-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="a59bf-151">chemin d’accès relatif Hello fichier manifeste sur le disque dur hello</span><span class="sxs-lookup"><span data-stu-id="a59bf-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="a59bf-152">Hello Base16 encodé hachage MD5 de fichier manifeste</span><span class="sxs-lookup"><span data-stu-id="a59bf-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="a59bf-153">Expédition de vos disques</span><span class="sxs-lookup"><span data-stu-id="a59bf-153">Shipping your drives</span></span>
<span data-ttu-id="a59bf-154">Vous devez expédier votre adresse de toohello de disques que vous avez obtenue à partir de l’étape précédente de hello, et vous devez fournir hello service Import/Export avec hello suivi du numéro de package de hello.</span><span class="sxs-lookup"><span data-stu-id="a59bf-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="a59bf-155">Vous devez expédier vos disques via un service de transport pris en charge, qui vous fournira un numéro de suivi pour votre colis.</span><span class="sxs-lookup"><span data-stu-id="a59bf-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="a59bf-156">Mise à jour de la tâche d’importation hello avec vos informations d’expédition</span><span class="sxs-lookup"><span data-stu-id="a59bf-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="a59bf-157">Après avoir configuré votre numéro de suivi, appelez hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) hello de tooupdate opération copie le nom de l’opérateur, le numéro de suivi hello du travail de hello et hello compte du transporteur pour les retours.</span><span class="sxs-lookup"><span data-stu-id="a59bf-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="a59bf-158">Vous pouvez éventuellement spécifier le nombre de hello des lecteurs et hello date d’expédition.</span><span class="sxs-lookup"><span data-stu-id="a59bf-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a59bf-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a59bf-159">Next steps</span></span>

* [<span data-ttu-id="a59bf-160">À l’aide des API REST du service importation/exportation hello</span><span class="sxs-lookup"><span data-stu-id="a59bf-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
