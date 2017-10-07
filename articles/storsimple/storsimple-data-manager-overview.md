---
title: "vue d’ensemble du Gestionnaire de données Azure StorSimple aaaMicrosoft | Documents Microsoft"
description: "Fournit une vue d’ensemble de hello transmet au service StorSimple Data Manager (version préliminaire privée)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="5d976-103">Vue d’ensemble de StorSimple Data Manager (version préliminaire privée)</span><span class="sxs-lookup"><span data-stu-id="5d976-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="5d976-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5d976-104">Overview</span></span>

<span data-ttu-id="5d976-105">Microsoft Azure StorSimple est une solution de stockage cloud hybride adresses hello complexités de couramment associées à des partages de fichiers de données non structurées.</span><span class="sxs-lookup"><span data-stu-id="5d976-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="5d976-106">StorSimple utilise le stockage cloud comme une extension de hello solution locale et reconnaît automatiquement les données sur un stockage local hello et de stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="5d976-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="5d976-107">Protection des données, d’intégrer local et les instantanés cloud, hello inutile une immense infrastructure de stockage.</span><span class="sxs-lookup"><span data-stu-id="5d976-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="5d976-108">Archivage et récupération d’urgence est également transparente avec cloud hello agissant comme un emplacement hors site.</span><span class="sxs-lookup"><span data-stu-id="5d976-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="5d976-109">Hello data transformation services que nous vous présentons dans ce document, permet un accès tooseamlessly vous hello StorSimple des données dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="5d976-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="5d976-110">Ce service fournit des données de tooextract d’API à partir de StorSimple et présenter tooother Azure services dans des formats qui peuvent être facilement consommées.</span><span class="sxs-lookup"><span data-stu-id="5d976-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="5d976-111">formats de Hello pris en charge dans cette version d’évaluation sont des objets BLOB Windows Azure et des éléments multimédias Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5d976-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="5d976-112">Cette transformation permet de vous tooeasily câble des services tels que les données toooperate Azure Media Services, Azure HDInsight, Azure Machine Learning et Azure Search sur l’appareil local de série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="5d976-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="5d976-113">Le diagramme de blocs général ci-dessous illustre cela.</span><span class="sxs-lookup"><span data-stu-id="5d976-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagramme général](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="5d976-115">Ce document explique comment s’inscrire à la version préliminaire privée de ce service.</span><span class="sxs-lookup"><span data-stu-id="5d976-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="5d976-116">Elle explique également comment vous pouvez utiliser ce service toowrite les applications qui utilisent des données de StorSimple et d’autres services Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="5d976-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="5d976-117">Inscription à la version préliminaire de Data Manager</span><span class="sxs-lookup"><span data-stu-id="5d976-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="5d976-118">Avant de vous inscrivez pour le service de gestionnaire de données hello, passez en revue hello suivant des conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="5d976-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5d976-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5d976-119">Prerequisites</span></span>

<span data-ttu-id="5d976-120">Cet exercice suppose que vous disposiez :</span><span class="sxs-lookup"><span data-stu-id="5d976-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="5d976-121">d’un abonnement Azure actif ;</span><span class="sxs-lookup"><span data-stu-id="5d976-121">an active Azure subscription.</span></span>
* <span data-ttu-id="5d976-122">accès tooa inscrit l’appareil de série StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="5d976-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="5d976-123">tous les hello clés associées aux appareils de hello StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="5d976-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="5d976-124">Inscription</span><span class="sxs-lookup"><span data-stu-id="5d976-124">Sign up</span></span>

<span data-ttu-id="5d976-125">Hello Data StorSimple Manager est en aperçu privé.</span><span class="sxs-lookup"><span data-stu-id="5d976-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="5d976-126">Effectuez hello suivant toosign étapes pour une version préliminaire limitée de ce service :</span><span class="sxs-lookup"><span data-stu-id="5d976-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="5d976-127">Se connecter à hello portail Azure avec l’extension de données de StorSimple Manager hello à : [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="5d976-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="5d976-128">Utilisez toolog de vos informations d’identification Azure dans.</span><span class="sxs-lookup"><span data-stu-id="5d976-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="5d976-129">Cliquez sur hello  **+**  icône toocreate un service.</span><span class="sxs-lookup"><span data-stu-id="5d976-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="5d976-130">Cliquez sur **stockage** puis cliquez sur **voir tous les** dans le panneau hello qui s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5d976-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Rechercher l’icône de StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="5d976-132">Icône du Gestionnaire de données de StorSimple hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5d976-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Sélectionner l’icône de StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="5d976-134">Cliquez sur l’icône de StorSimple Data Manager, puis sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5d976-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="5d976-135">Choisir l’abonnement hello que vous souhaitez tooenable pour la version préliminaire limitée de hello, puis sur **Inscrivez-moi !**</span><span class="sxs-lookup"><span data-stu-id="5d976-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Inscription](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="5d976-137">Envoie une demande tooonboard vous.</span><span class="sxs-lookup"><span data-stu-id="5d976-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="5d976-138">Nous vous intégrerons dès que possible.</span><span class="sxs-lookup"><span data-stu-id="5d976-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="5d976-139">Une fois votre abonnement activé, vous pouvez créer un service StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="5d976-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="5d976-140">tooeasily accéder au service de données de StorSimple Manager hello, cliquez sur hello étoile toopin il tooyour favoris.</span><span class="sxs-lookup"><span data-stu-id="5d976-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Accéder à StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="5d976-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d976-142">Next steps</span></span>

<span data-ttu-id="5d976-143">[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="5d976-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
