---
title: "Création d’un travail d’exportation pour Azure Import/Export | Microsoft Docs"
description: "Découvrez comment créer un travail d’exportation pour le service Microsoft Azure Import/Export."
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="a75ca-103">Création d’un travail d’exportation pour le service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="a75ca-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="a75ca-104">La création d’un travail d’exportation pour le service Microsoft Azure Import/Export à l’aide de l’API REST implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a75ca-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="a75ca-105">Sélection des blobs à exporter.</span><span class="sxs-lookup"><span data-stu-id="a75ca-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="a75ca-106">Obtention d’un emplacement d’expédition.</span><span class="sxs-lookup"><span data-stu-id="a75ca-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="a75ca-107">Création du travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="a75ca-107">Creating the export job.</span></span>

-   <span data-ttu-id="a75ca-108">Expédition de vos disques vides à Microsoft via un service de transport pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a75ca-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="a75ca-109">Mise à jour du travail d’exportation avec les informations du colis.</span><span class="sxs-lookup"><span data-stu-id="a75ca-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="a75ca-110">Réception des disques renvoyés par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a75ca-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="a75ca-111">Consultez [Transfert de données vers le stockage Blob à l’aide du service Microsoft Azure Import/Export](storage-import-export-service.md) pour une présentation du service Import/Export et un didacticiel expliquant comment utiliser le [portail Azure](https://portal.azure.com/) pour créer et gérer les travaux d’importation et d’exportation.</span><span class="sxs-lookup"><span data-stu-id="a75ca-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="a75ca-112">Sélection des blobs à exporter</span><span class="sxs-lookup"><span data-stu-id="a75ca-112">Selecting blobs to export</span></span>
 <span data-ttu-id="a75ca-113">Pour créer un travail d’exportation, vous devrez fournir une liste des blobs que vous souhaitez exporter à partir de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a75ca-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="a75ca-114">Plusieurs options s’offrent à vous pour sélectionner les blobs à exporter :</span><span class="sxs-lookup"><span data-stu-id="a75ca-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="a75ca-115">Vous pouvez utiliser un chemin d’accès de blob relatif pour sélectionner un seul objet blob et toutes ses captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="a75ca-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="a75ca-116">Vous pouvez utiliser un chemin d’accès de blob relatif pour sélectionner un seul objet blob, sans ses captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="a75ca-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="a75ca-117">Vous pouvez utiliser un chemin d’accès de blob relatif et une heure de capture instantanée pour sélectionner une seule capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="a75ca-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="a75ca-118">Vous pouvez utiliser un préfixe de blob pour sélectionner tous les blobs et les captures instantanées avec le préfixe spécifié.</span><span class="sxs-lookup"><span data-stu-id="a75ca-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="a75ca-119">Vous pouvez exporter tous les blobs et les captures instantanées dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a75ca-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="a75ca-120">Pour plus d’informations sur la spécification des blobs à exporter, consultez l’opération [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="a75ca-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="a75ca-121">Obtention de votre emplacement d’expédition</span><span class="sxs-lookup"><span data-stu-id="a75ca-121">Obtaining your shipping location</span></span>
<span data-ttu-id="a75ca-122">Avant de créer un travail d’exportation, vous devez obtenir un nom et une adresse d’emplacement d’expédition en appelant l’opération [Get Location](https://portal.azure.com) ou [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="a75ca-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="a75ca-123">`List Locations` renvoie une liste d’emplacements et leurs adresses postales.</span><span class="sxs-lookup"><span data-stu-id="a75ca-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="a75ca-124">Vous pouvez sélectionner un emplacement dans la liste renvoyée et expédier vos disques durs à cette adresse.</span><span class="sxs-lookup"><span data-stu-id="a75ca-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="a75ca-125">Vous pouvez également utiliser l’opération `Get Location` pour obtenir directement l’adresse d’expédition relative à un emplacement spécifique.</span><span class="sxs-lookup"><span data-stu-id="a75ca-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="a75ca-126">Suivez les étapes ci-dessous pour obtenir l’emplacement d’expédition :</span><span class="sxs-lookup"><span data-stu-id="a75ca-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="a75ca-127">Identifiez le nom de l’emplacement de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a75ca-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="a75ca-128">Cette valeur se trouve sous le champ **Emplacement** sur le **Tableau de bord** du compte de stockage dans le portail classique. Elle peut également être obtenue en utilisant l’opération de l’API Gestion des services [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="a75ca-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="a75ca-129">Récupérez l’emplacement disponible pour traiter ce compte de stockage en appelant l’opération `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="a75ca-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="a75ca-130">Si la propriété `AlternateLocations` de l’emplacement contient l’emplacement lui-même, alors il est possible d’utiliser cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="a75ca-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="a75ca-131">Sinon, appelez une nouvelle fois l’opération `Get Location` en utilisant l’un des autres emplacements.</span><span class="sxs-lookup"><span data-stu-id="a75ca-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="a75ca-132">L’emplacement d’origine peut être fermé temporairement pour maintenance.</span><span class="sxs-lookup"><span data-stu-id="a75ca-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="a75ca-133">Création du travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="a75ca-133">Creating the export job</span></span>
 <span data-ttu-id="a75ca-134">Pour créer le travail d’exportation, appelez l’opération [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="a75ca-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="a75ca-135">Vous devez fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a75ca-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="a75ca-136">Nom du travail.</span><span class="sxs-lookup"><span data-stu-id="a75ca-136">A name for the job.</span></span>

-   <span data-ttu-id="a75ca-137">nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a75ca-137">The storage account name.</span></span>

-   <span data-ttu-id="a75ca-138">Nom de l’emplacement d’expédition, obtenu à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="a75ca-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="a75ca-139">Type de travail (exportation).</span><span class="sxs-lookup"><span data-stu-id="a75ca-139">A job type (Export).</span></span>

-   <span data-ttu-id="a75ca-140">L’adresse de retour à laquelle les disques doivent être envoyés une fois le travail d’exportation terminé.</span><span class="sxs-lookup"><span data-stu-id="a75ca-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="a75ca-141">La liste des blobs (ou des préfixes de blob) à exporter.</span><span class="sxs-lookup"><span data-stu-id="a75ca-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="a75ca-142">Expédition de vos disques</span><span class="sxs-lookup"><span data-stu-id="a75ca-142">Shipping your drives</span></span>
 <span data-ttu-id="a75ca-143">Ensuite, utilisez l’outil Azure Import/Export pour déterminer le nombre de disques à envoyer, en fonction des blobs que vous avez sélectionnés pour l’exportation et de la taille du disque.</span><span class="sxs-lookup"><span data-stu-id="a75ca-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="a75ca-144">Consultez la [référence sur l’outil Azure Import/Export](storage-import-export-tool-how-to-v1.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a75ca-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="a75ca-145">Placez les disques dans un seul colis et expédiez-les à l’adresse obtenue à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="a75ca-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="a75ca-146">Notez le numéro de suivi de votre colis pour l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="a75ca-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="a75ca-147">Vous devez expédier vos disques via un service de transport pris en charge, qui vous fournira un numéro de suivi pour votre colis.</span><span class="sxs-lookup"><span data-stu-id="a75ca-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="a75ca-148">Mise à jour du travail d’exportation avec vos informations de colis</span><span class="sxs-lookup"><span data-stu-id="a75ca-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="a75ca-149">Dès que vous avez votre numéro de suivi, appelez l’opération [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) pour mettre à jour le numéro de suivi et le nom du transporteur correspondant au travail.</span><span class="sxs-lookup"><span data-stu-id="a75ca-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="a75ca-150">Vous pouvez éventuellement spécifier le nombre de disques, l’adresse de retour et la date d’expédition.</span><span class="sxs-lookup"><span data-stu-id="a75ca-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="a75ca-151">Réception du package</span><span class="sxs-lookup"><span data-stu-id="a75ca-151">Receiving the package</span></span>
 <span data-ttu-id="a75ca-152">Une fois votre travail d’exportation traité, vos disques vous sont renvoyés avec vos données chiffrées.</span><span class="sxs-lookup"><span data-stu-id="a75ca-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="a75ca-153">Vous pouvez récupérer la clé BitLocker pour chacun des disques en appelant l’opération [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="a75ca-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a75ca-154">Cette clé vous permettra de déverrouiller le disque.</span><span class="sxs-lookup"><span data-stu-id="a75ca-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="a75ca-155">Le fichier manifeste de disque sur chaque disque contient la liste des fichiers sur le disque, ainsi que l’adresse du blob d’origine pour chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="a75ca-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a75ca-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a75ca-156">Next steps</span></span>

* [<span data-ttu-id="a75ca-157">Utilisation de l’API REST du service Import/Export</span><span class="sxs-lookup"><span data-stu-id="a75ca-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
