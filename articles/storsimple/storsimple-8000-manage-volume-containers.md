---
title: "aaaManage vos conteneurs de volumes StorSimple sur l’appareil de série StorSimple 8000 de hello | Documents Microsoft"
description: "Explique comment vous pouvez utiliser hello le Gestionnaire de périphériques StorSimple conteneurs de volumes service page tooadd, modifier ou supprimer un conteneur de volume."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="54772-103">Utiliser des conteneurs de volumes StorSimple hello le Gestionnaire de périphériques StorSimple service toomanage</span><span class="sxs-lookup"><span data-stu-id="54772-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="54772-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="54772-104">Overview</span></span>
<span data-ttu-id="54772-105">Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gérer des conteneurs de volumes StorSimple.</span><span class="sxs-lookup"><span data-stu-id="54772-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="54772-106">Un conteneur de volumes créé dans un appareil Microsoft Azure StorSimple contient un ou plusieurs volumes hébergeant les paramètres de consommation du compte de stockage, du chiffrement et de la bande passante.</span><span class="sxs-lookup"><span data-stu-id="54772-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="54772-107">Un appareil peut comporter plusieurs conteneurs de volumes pour l’ensemble de ses volumes.</span><span class="sxs-lookup"><span data-stu-id="54772-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="54772-108">Un conteneur de volumes a hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="54772-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="54772-109">**Volumes** – hello à plusieurs niveaux ou attaché localement des volumes StorSimple qui sont contenus dans le conteneur de volume hello.</span><span class="sxs-lookup"><span data-stu-id="54772-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="54772-110">**Chiffrement** : clé de chiffrement pouvant être définie pour chaque conteneur de volumes.</span><span class="sxs-lookup"><span data-stu-id="54772-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="54772-111">Cette clé est utilisée pour chiffrer les données de hello sont envoyées à partir de votre cloud toohello du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="54772-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="54772-112">Une clé de niveau militaire AES-256 bits est utilisée avec la clé de hello entré par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="54772-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="54772-113">toosecure vos données, nous vous recommandons de toujours activer le chiffrement de stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="54772-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="54772-114">**Compte de stockage** : hello compte de stockage Azure qui sont des données hello toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="54772-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="54772-115">Tous les volumes de hello résidant dans un conteneur de volume partagent ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54772-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="54772-116">Vous pouvez choisir un compte de stockage à partir d’une liste existante ou créer un nouveau compte lorsque vous créez le conteneur de volume hello puis spécifiez les informations d’identification hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="54772-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="54772-117">**Bande passante cloud** – hello la bande passante consommée par les appareils hello lorsque hello de données à partir de l’appareil de hello envoyée toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="54772-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="54772-118">Vous pouvez appliquer un contrôle de bande passante en définissant une valeur comprise entre 1 et 1 000 Mbits/s lorsque vous créez ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="54772-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="54772-119">Si vous souhaitez hello appareil tooconsume la bande passante disponible, définissez ce champ trop**illimité**.</span><span class="sxs-lookup"><span data-stu-id="54772-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="54772-120">Vous pouvez également créer et appliquer une bande passante tooallocate du modèle de bande passante selon une planification.</span><span class="sxs-lookup"><span data-stu-id="54772-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="54772-121">Hello procédures suivantes expliquent comment toouse hello StorSimple **conteneurs de volumes** hello toocomplete de panneau opérations communes suivantes :</span><span class="sxs-lookup"><span data-stu-id="54772-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="54772-122">Ajouter un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="54772-122">Add a volume container</span></span>
* <span data-ttu-id="54772-123">Modifier un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="54772-123">Modify a volume container</span></span>
* <span data-ttu-id="54772-124">Supprimer un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="54772-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="54772-125">Ajouter un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="54772-125">Add a volume container</span></span>
<span data-ttu-id="54772-126">Effectuer hello suivant les étapes tooadd un conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="54772-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="54772-127">Modifier un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="54772-127">Modify a volume container</span></span>
<span data-ttu-id="54772-128">Effectuer hello suivant les étapes toomodify un conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="54772-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="54772-129">Supprimer un conteneur de volumes</span><span class="sxs-lookup"><span data-stu-id="54772-129">Delete a volume container</span></span>
<span data-ttu-id="54772-130">Un conteneur de volumes comporte plusieurs volumes.</span><span class="sxs-lookup"><span data-stu-id="54772-130">A volume container has volumes within it.</span></span> <span data-ttu-id="54772-131">Il peut être supprimé que si tous les volumes hello qu’il contient sont supprimés en premier.</span><span class="sxs-lookup"><span data-stu-id="54772-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="54772-132">Effectuer hello suivant les étapes toodelete un conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="54772-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="54772-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54772-133">Next steps</span></span>
* <span data-ttu-id="54772-134">En savoir plus sur la [gestion des volumes StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="54772-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="54772-135">En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="54772-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

