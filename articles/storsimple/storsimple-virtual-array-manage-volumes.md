---
title: "Gérer des volumes sur StorSimple Virtual Array | Microsoft Docs"
description: "Décrit le service StorSimple Device Manager et vous explique comment l’utiliser pour gérer des volumes sur votre instance StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="fb464-103">Utiliser le service StorSimple Device Manager pour gérer les volumes sur l’instance StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="fb464-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="fb464-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fb464-104">Overview</span></span>

<span data-ttu-id="fb464-105">Ce didacticiel explique comment utiliser le service StorSimple Device Manager pour créer et gérer des volumes sur votre instance StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="fb464-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="fb464-106">Le service StorSimple Device Manager est une extension dans le portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web.</span><span class="sxs-lookup"><span data-stu-id="fb464-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="fb464-107">Outre la gestion des partages et des volumes, le service StorSimple Device Manager prend en charge l’affichage et la gestion des appareils, l’affichage des alertes,l’affichage et la gestion des stratégies de sauvegardes et du catalogue de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="fb464-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="fb464-108">Types de volume</span><span class="sxs-lookup"><span data-stu-id="fb464-108">Volume Types</span></span>

<span data-ttu-id="fb464-109">Les volumes StorSimple peuvent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="fb464-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="fb464-110">**Attaché localement** : les données de ces volumes demeurent à tout moment sur le tableau ; elles ne se dispersent pas dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="fb464-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="fb464-111">**Hiérarchisé**: les données de ces volumes peuvent se disperser dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="fb464-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="fb464-112">Lorsque vous créez un volume à plusieurs niveaux, environ 10 % de l’espace est configuré au niveau local et 90 % dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="fb464-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="fb464-113">Par exemple, si vous avez configuré un volume de 1 To, 100 Go résident dans l'espace local et 900 Go sont utilisés dans le cloud lorsque les données sont stockées en niveaux.</span><span class="sxs-lookup"><span data-stu-id="fb464-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="fb464-114">Cela implique que si vous n’avez plus d’espace local sur l’appareil, vous ne pouvez pas configurer un volume à plusieurs niveaux (car les 10 % requis sur l’espace local ne seront pas disponibles).</span><span class="sxs-lookup"><span data-stu-id="fb464-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="fb464-115">Capacité allouée</span><span class="sxs-lookup"><span data-stu-id="fb464-115">Provisioned capacity</span></span>
<span data-ttu-id="fb464-116">Reportez-vous au tableau suivant pour connaître la capacité maximale allouée pour chaque type de volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="fb464-117">**Identificateur de la limite**</span><span class="sxs-lookup"><span data-stu-id="fb464-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="fb464-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="fb464-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="fb464-119">Taille minimale d’un volume hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="fb464-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="fb464-120">500 Go</span><span class="sxs-lookup"><span data-stu-id="fb464-120">500 GB</span></span>        |
| <span data-ttu-id="fb464-121">Taille maximale d’un volume hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="fb464-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="fb464-122">5 To</span><span class="sxs-lookup"><span data-stu-id="fb464-122">5 TB</span></span>          |
| <span data-ttu-id="fb464-123">Taille minimale d'un volume épinglé localement</span><span class="sxs-lookup"><span data-stu-id="fb464-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="fb464-124">50 Go</span><span class="sxs-lookup"><span data-stu-id="fb464-124">50 GB</span></span>         |
| <span data-ttu-id="fb464-125">Taille maximale d'un volume épinglé localement</span><span class="sxs-lookup"><span data-stu-id="fb464-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="fb464-126">500 Go</span><span class="sxs-lookup"><span data-stu-id="fb464-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="fb464-127">Le panneau Volumes</span><span class="sxs-lookup"><span data-stu-id="fb464-127">The Volumes blade</span></span>
<span data-ttu-id="fb464-128">Sur le panneau de synthèse du service StorSimple, le menu **Volumes** affiche la liste des volumes de stockage sur un tableau StorSimple considéré et vous donne les moyens de les gérer.</span><span class="sxs-lookup"><span data-stu-id="fb464-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Panneau Volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="fb464-130">Un volume est constitué d’une série d’attributs :</span><span class="sxs-lookup"><span data-stu-id="fb464-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="fb464-131">**Nom du volume** : nom descriptif qui doit être unique et vous aide à identifier le volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="fb464-132">**État** : peut être en ligne ou hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fb464-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="fb464-133">Si un volume est hors connexion, il n’est pas visible pour les initiateurs (serveurs) qui sont autorisés à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="fb464-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="fb464-134">**Type** : indique si le volume est **Hiérarchisé** (par défaut) ou **Épinglé localement**.</span><span class="sxs-lookup"><span data-stu-id="fb464-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="fb464-135">**Capacité** : spécifie la quantité de données utilisées par rapport au volume total des données pouvant être stockées par l’initiateur (serveur).</span><span class="sxs-lookup"><span data-stu-id="fb464-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="fb464-136">**Sauvegarde** : dans le cas d’une instance StorSimple Virtual Array, l’ensemble des volumes sont automatiquement activés pour la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="fb464-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="fb464-137">**Hôtes connectés** : indique les initiateurs (serveurs) autorisés à accéder à ce volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Détails de volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="fb464-139">Suivez les instructions de ce didacticiel pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="fb464-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="fb464-140">Ajout d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-140">Add a volume</span></span>
* <span data-ttu-id="fb464-141">Modification d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-141">Modify a volume</span></span>
* <span data-ttu-id="fb464-142">Mise hors connexion d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-142">Take a volume offline</span></span>
* <span data-ttu-id="fb464-143">Suppression d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="fb464-144">Ajout d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-144">Add a volume</span></span>

1. <span data-ttu-id="fb464-145">À partir du panneau de synthèse du service StorSimple, cliquez sur **+ Ajouter un volume** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="fb464-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="fb464-146">Le panneau **Ajouter un volume** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="fb464-146">This opens up the **Add volume** blade.</span></span>
   
    ![Ajouter un volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="fb464-148">Dans le panneau **Ajouter un volume**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fb464-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="fb464-149">Dans le champ **Nom du volume**, saisissez un nom unique pour votre volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="fb464-150">Le nom doit être une chaîne contenant entre 3 et 127 caractères.</span><span class="sxs-lookup"><span data-stu-id="fb464-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="fb464-151">Dans la liste déroulante **Type**, spécifiez si vous souhaitez créer un volume **Hiérarchisé** ou **Attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="fb464-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="fb464-152">Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez **Volume attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="fb464-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="fb464-153">Pour toutes les autres données, sélectionnez le volume **hiérarchisé**.</span><span class="sxs-lookup"><span data-stu-id="fb464-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="fb464-154">Dans le champ **Capacité**, spécifiez la taille du volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="fb464-155">Un volume hiérarchisé doit être compris entre 500 Go et 5 To, tandis qu’un volume attaché doit être compris entre 50 Go et 500 Go.</span><span class="sxs-lookup"><span data-stu-id="fb464-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="fb464-156">Cliquez sur **Hôtes connectés**, sélectionnez un enregistrement de contrôle d’accès correspondant à l’initiateur iSCSI que vous souhaitez connecter à ce volume, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="fb464-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="fb464-157">Pour ajouter un hôte connecté, cliquez sur **Ajouter nouveau**, saisissez un nom pour l’hôte et son nom complet iSCSI, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fb464-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Ajouter un volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="fb464-159">Lorsque vous avez terminé de configurer votre volume, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="fb464-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="fb464-160">Un volume est créé avec les paramètres spécifiés ; une notification s’affiche en cas de création similaire.</span><span class="sxs-lookup"><span data-stu-id="fb464-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="fb464-161">Par défaut, la sauvegarde est activée pour le volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="fb464-162">Pour vérifier que le volume a été créé, accédez au panneau **Volumes**.</span><span class="sxs-lookup"><span data-stu-id="fb464-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="fb464-163">Le volume devrait y apparaître.</span><span class="sxs-lookup"><span data-stu-id="fb464-163">You should see the volume listed.</span></span>
   
    ![Le volume stimule la réussite](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="fb464-165">Modification d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-165">Modify a volume</span></span>

<span data-ttu-id="fb464-166">Modifiez un volume lorsque vous avez besoin de modifier les hôtes qui y accèdent.</span><span class="sxs-lookup"><span data-stu-id="fb464-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="fb464-167">Une fois le volume créé, il est impossible de modifier les autres attributs d’un volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="fb464-168">Pour modifier un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-168">To modify a volume</span></span>

1. <span data-ttu-id="fb464-169">À partir du paramètre **Volumes** du panneau de synthèse du service StorSimple, sélectionnez le tableau virtuel sur lequel est hébergé le volume à modifier.</span><span class="sxs-lookup"><span data-stu-id="fb464-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="fb464-170">**Sélectionnez** le volume, puis cliquez sur **Hôtes connectés** afin d’afficher l’hôte actuellement connecté et de l’affecter à un serveur différent.</span><span class="sxs-lookup"><span data-stu-id="fb464-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Modifier le volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="fb464-172">Pour enregistrer les modifications, cliquez sur la barre de commandes **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fb464-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="fb464-173">Vos paramètres spécifiés sont appliqués ; une notification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fb464-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="fb464-174">Mise hors connexion d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-174">Take a volume offline</span></span>

<span data-ttu-id="fb464-175">Vous devrez peut-être mettre un volume hors connexion si vous envisagez de le modifier ou de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="fb464-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="fb464-176">Lorsqu’un volume est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="fb464-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="fb464-177">Vous devrez mettre le volume hors connexion à la fois sur l’ordinateur hôte et sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="fb464-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="fb464-178">Pour mettre un volume hors connexion</span><span class="sxs-lookup"><span data-stu-id="fb464-178">To take a volume offline</span></span>

1. <span data-ttu-id="fb464-179">Assurez-vous que le volume en question n’est pas utilisé avant de le mettre hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fb464-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="fb464-180">Mettez d’abord le volume hors connexion sur l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="fb464-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="fb464-181">Cela élimine tout risque d’endommagement des données sur le volume.</span><span class="sxs-lookup"><span data-stu-id="fb464-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="fb464-182">Pour les instructions spécifiques, reportez-vous aux instructions du système d’exploitation de l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="fb464-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="fb464-183">Une fois le volume de l’hôte est hors connexion, mettez le volume du tableau hors connexion en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="fb464-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="fb464-184">À partir du paramètre **Volumes** du panneau de synthèse du service StorSimple, sélectionnez le tableau virtuel sur lequel est hébergé le volume que vous souhaitez déplacer hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fb464-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="fb464-185">**Sélectionnez** le volume, puis cliquez sur **...** (sinon cliquez avec le bouton droit sur cette ligne), puis dans le menu contextuel, sélectionnez **Mettre hors connexion**.</span><span class="sxs-lookup"><span data-stu-id="fb464-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Volume hors connexion](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="fb464-187">Passez en revue les informations du panneau **Mettre hors connexion**, puis confirmez votre acceptation de l’opération.</span><span class="sxs-lookup"><span data-stu-id="fb464-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="fb464-188">Cliquez sur **Mettre hors connexion** afin de mettre le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fb464-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="fb464-189">Une notification de l’opération en cours s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fb464-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="fb464-190">Pour vérifier que le volume a été mis hors connexion, accédez au panneau **Volumes**.</span><span class="sxs-lookup"><span data-stu-id="fb464-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="fb464-191">Le volume doit apparaître comme élément hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fb464-191">You should see the status of the volume as offline.</span></span>
     
       ![Confirmation du volume hors connexion](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="fb464-193">Suppression d’un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb464-194">Vous pouvez supprimer un volume uniquement s’il est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fb464-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="fb464-195">Pour supprimer un volume, procédez comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb464-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="fb464-196">Pour supprimer un volume</span><span class="sxs-lookup"><span data-stu-id="fb464-196">To delete a volume</span></span>

1. <span data-ttu-id="fb464-197">À partir du paramètre **Volumes** du panneau de synthèse du service StorSimple, sélectionnez le tableau virtuel sur lequel est hébergé le volume à supprimer.</span><span class="sxs-lookup"><span data-stu-id="fb464-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="fb464-198">**Sélectionnez** le volume, puis cliquez sur **...** (sinon cliquez avec le bouton droit sur cette ligne), puis dans le menu contextuel, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fb464-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Supprimer un volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="fb464-200">Vérifiez l’état du volume à supprimer.</span><span class="sxs-lookup"><span data-stu-id="fb464-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="fb464-201">Si le volume que vous souhaitez supprimer n’est pas hors connexion, mettez-le d’abord hors connexion, en suivant la procédure [Mise hors connexion d’un volume](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="fb464-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="fb464-202">Lorsque vous êtes invité à confirmer l’opération dans le panneau **Supprimer**, validez la confirmation, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fb464-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="fb464-203">Le volume est supprimé, et le panneau **Volumes** représente la liste mise à jour des volumes au sein du tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fb464-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb464-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb464-204">Next steps</span></span>

<span data-ttu-id="fb464-205">Découvrez comment [cloner un volume StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="fb464-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

