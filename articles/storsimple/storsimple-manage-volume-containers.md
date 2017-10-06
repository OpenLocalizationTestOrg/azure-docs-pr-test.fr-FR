---
title: aaaManage vos conteneurs de volumes StorSimple | Documents Microsoft
description: Explique comment vous pouvez utiliser hello StorSimple Manager conteneurs de volumes service page tooadd, modifier ou supprimer un conteneur de volume.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="dc9e7-103">Utiliser des conteneurs de volumes StorSimple hello StorSimple Manager service toomanage</span><span class="sxs-lookup"><span data-stu-id="dc9e7-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="dc9e7-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dc9e7-104">Overview</span></span>
<span data-ttu-id="dc9e7-105">Ce didacticiel explique comment toouse hello toocreate du service StorSimple Manager et de gérer des conteneurs de volumes StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="dc9e7-106">Un conteneur de volumes créé dans un appareil Microsoft Azure StorSimple contient un ou plusieurs volumes hébergeant les paramètres de consommation du compte de stockage, du chiffrement et de la bande passante.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="dc9e7-107">Un appareil peut comporter plusieurs conteneurs de volumes pour l’ensemble de ses volumes.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="dc9e7-108">Un conteneur de volumes a hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="dc9e7-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="dc9e7-109">**Volumes** – hello à plusieurs niveaux ou attaché localement des volumes StorSimple qui sont contenus dans le conteneur de volume hello.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="dc9e7-110">Un conteneur de volume peut contenir des volumes de StorSimple too256.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="dc9e7-111">**Chiffrement** : clé de chiffrement pouvant être définie pour chaque conteneur de volumes.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="dc9e7-112">Cette clé est utilisée pour chiffrer les données de hello sont envoyées à partir de votre cloud toohello du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="dc9e7-113">Une clé de niveau militaire AES-256 bits est utilisée avec la clé de hello entré par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="dc9e7-114">toosecure vos données, nous vous recommandons de toujours activer le chiffrement de stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="dc9e7-115">**Compte de stockage** : hello compte de stockage qui est le fournisseur de services de stockage cloud tooyour lié.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="dc9e7-116">Tous les volumes de hello résidant dans un conteneur de volume partagent ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="dc9e7-117">Vous pouvez choisir un compte de stockage à partir d’une liste existante ou créer un nouveau compte lorsque vous créez le conteneur de volume hello puis spécifiez les informations d’identification hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="dc9e7-118">**Bande passante cloud** – hello la bande passante consommée par les appareils hello lorsque hello de données à partir de l’appareil de hello envoyée toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="dc9e7-119">Vous pouvez appliquer un contrôle de bande passante en définissant une valeur comprise entre 1 et 1 000 Mbits/s lorsque vous définissez ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="dc9e7-120">Si vous souhaitez hello appareil tooconsume de la bande passante disponible de tous les, définissez tooUnlimited de ce champ.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="dc9e7-121">Vous pouvez également créer et appliquer une bande passante tooallocate du modèle de bande passante selon une planification.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Page des conteneurs de volumes](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="dc9e7-123">Procédures suivantes expliquent comment toouse hello StorSimple **conteneurs de volumes** hello toocomplete de page après les opérations courantes :</span><span class="sxs-lookup"><span data-stu-id="dc9e7-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="dc9e7-124">Ajouter un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-124">Add a volume container</span></span> 
* <span data-ttu-id="dc9e7-125">Modifier un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-125">Modify a volume container</span></span> 
* <span data-ttu-id="dc9e7-126">Supprimer un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="dc9e7-127">Ajouter un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-127">Add a volume container</span></span>
<span data-ttu-id="dc9e7-128">Effectuer hello suivant les étapes tooadd un conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="dc9e7-129">Modifier un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-129">Modify a volume container</span></span>
<span data-ttu-id="dc9e7-130">Effectuer hello suivant les étapes toomodify un conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="dc9e7-131">Supprimer un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-131">Delete a volume container</span></span>
<span data-ttu-id="dc9e7-132">Un conteneur de volumes comporte plusieurs volumes.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-132">A volume container has volumes within it.</span></span> <span data-ttu-id="dc9e7-133">Il peut être supprimé que si tous les volumes hello qu’il contient sont supprimés en premier.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="dc9e7-134">Effectuer hello suivant les étapes toodelete un conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="dc9e7-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="dc9e7-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc9e7-135">Next steps</span></span>
* <span data-ttu-id="dc9e7-136">En savoir plus sur la [gestion des volumes StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="dc9e7-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="dc9e7-137">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="dc9e7-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

