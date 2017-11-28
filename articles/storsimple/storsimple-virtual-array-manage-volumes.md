---
title: volumes StorSimple Virtual Array aaaManage | Documents Microsoft
description: "Décrit les hello StorSimple le Gestionnaire de périphériques et explique comment toouse il toomanage des volumes sur votre tableau virtuel StorSimple."
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
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="77116-103">Utilisez le Gestionnaire de périphériques StorSimple volumes de toomanage service sur hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="77116-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="77116-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="77116-104">Overview</span></span>

<span data-ttu-id="77116-105">Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gestion des volumes sur votre tableau virtuel StorSimple.</span><span class="sxs-lookup"><span data-stu-id="77116-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="77116-106">Hello service du Gestionnaire de périphériques StorSimple est une extension Bonjour portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web.</span><span class="sxs-lookup"><span data-stu-id="77116-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="77116-107">Dans Ajout toomanaging partages et les volumes, vous pouvez utiliser tooview de service de gestionnaire de périphériques StorSimple hello et gérer les appareils, afficher les alertes et afficher et gérer les stratégies de sauvegarde et de catalogue de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="77116-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="77116-108">Types de volume</span><span class="sxs-lookup"><span data-stu-id="77116-108">Volume Types</span></span>

<span data-ttu-id="77116-109">Les volumes StorSimple peuvent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="77116-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="77116-110">**Attaché localement**: données de ces volumes reste sur le tableau de hello en permanence et ne pas déborder toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="77116-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="77116-111">**Niveaux**: données de ces volumes peuvent déborder toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="77116-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="77116-112">Lorsque vous créez un volume hiérarchisé, environ 10 % d’espace de hello est approvisionné sur le niveau de local hello et 90 % d’espace de hello est configuré dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="77116-113">Par exemple, si vous avez configuré un volume de 1 To, 100 Go peut résider dans un espace local hello et 900 Go sera utilisée dans le cloud de hello hello lorsque des niveaux de données.</span><span class="sxs-lookup"><span data-stu-id="77116-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="77116-114">À son tour, cela implique que si vous manquez tout l’espace local hello sur l’appareil de hello, vous ne pouvez pas configurer un volume hiérarchisé (car hello 10 % requis sur hello local niveau ne sera pas disponible).</span><span class="sxs-lookup"><span data-stu-id="77116-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="77116-115">Capacité allouée</span><span class="sxs-lookup"><span data-stu-id="77116-115">Provisioned capacity</span></span>
<span data-ttu-id="77116-116">Consultez toohello tableau pour une capacité déployée maximale pour chaque type de volume.</span><span class="sxs-lookup"><span data-stu-id="77116-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="77116-117">**Identificateur de la limite**</span><span class="sxs-lookup"><span data-stu-id="77116-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="77116-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="77116-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="77116-119">Taille minimale d’un volume hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="77116-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="77116-120">500 Go</span><span class="sxs-lookup"><span data-stu-id="77116-120">500 GB</span></span>        |
| <span data-ttu-id="77116-121">Taille maximale d’un volume hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="77116-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="77116-122">5 To</span><span class="sxs-lookup"><span data-stu-id="77116-122">5 TB</span></span>          |
| <span data-ttu-id="77116-123">Taille minimale d'un volume épinglé localement</span><span class="sxs-lookup"><span data-stu-id="77116-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="77116-124">50 Go</span><span class="sxs-lookup"><span data-stu-id="77116-124">50 GB</span></span>         |
| <span data-ttu-id="77116-125">Taille maximale d'un volume épinglé localement</span><span class="sxs-lookup"><span data-stu-id="77116-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="77116-126">500 Go</span><span class="sxs-lookup"><span data-stu-id="77116-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="77116-127">Panneau de Volumes Hello</span><span class="sxs-lookup"><span data-stu-id="77116-127">hello Volumes blade</span></span>
<span data-ttu-id="77116-128">Hello **Volumes** menu sur votre Panneau de résumé du service StorSimple affiche la liste hello des volumes de stockage sur un tableau de StorSimple donné et vous permet de toomanage les.</span><span class="sxs-lookup"><span data-stu-id="77116-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Panneau Volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="77116-130">Un volume est constitué d’une série d’attributs :</span><span class="sxs-lookup"><span data-stu-id="77116-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="77116-131">**Nom de volume** – un nom descriptif qui doit être uniques et permet d’identifier le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="77116-132">**État** : peut être en ligne ou hors connexion.</span><span class="sxs-lookup"><span data-stu-id="77116-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="77116-133">Si un volume est hors connexion, il n’est pas visible tooinitiators (serveurs) autorisés accès toouse hello volume.</span><span class="sxs-lookup"><span data-stu-id="77116-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="77116-134">**Type** – indique si le volume de hello est **à plusieurs niveaux** (hello par défaut) ou **attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="77116-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="77116-135">**Capacité** – spécifie la quantité hello de données utilisées comme comparés toohello la quantité totale de données qui peuvent être stockées à l’initiateur hello (serveur).</span><span class="sxs-lookup"><span data-stu-id="77116-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="77116-136">**Sauvegarde** : en cas de hello StorSimple Virtual Array, tous les volumes sont automatiquement activés pour sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="77116-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="77116-137">**Connecté des ordinateurs hôtes** – spécifie les initiateurs hello (serveurs) autorisés accès toothis volume.</span><span class="sxs-lookup"><span data-stu-id="77116-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Détails de volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="77116-139">Suivez les instructions de hello dans cette hello didacticiel tooperform tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="77116-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="77116-140">Ajout d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-140">Add a volume</span></span>
* <span data-ttu-id="77116-141">Modification d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-141">Modify a volume</span></span>
* <span data-ttu-id="77116-142">Mise hors connexion d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-142">Take a volume offline</span></span>
* <span data-ttu-id="77116-143">Suppression d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="77116-144">Ajout d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-144">Add a volume</span></span>

1. <span data-ttu-id="77116-145">Dans le volet Résumé du service de StorSimple hello, cliquez sur **+ ajouter un volume** à partir de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="77116-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="77116-146">Cela ouvre hello **Ajout du volume** panneau.</span><span class="sxs-lookup"><span data-stu-id="77116-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Ajouter un volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="77116-148">Bonjour **Ajout du volume** panneau, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="77116-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="77116-149">Bonjour **nom de Volume** , entrez un nom unique pour votre volume.</span><span class="sxs-lookup"><span data-stu-id="77116-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="77116-150">nom de Hello doit être une chaîne qui contient des caractères too127 3.</span><span class="sxs-lookup"><span data-stu-id="77116-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="77116-151">Bonjour **Type** déroulante liste, spécifiez si toocreate un **à plusieurs niveaux** ou **attaché localement** volume.</span><span class="sxs-lookup"><span data-stu-id="77116-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="77116-152">Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez **Volume attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="77116-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="77116-153">Pour toutes les autres données, sélectionnez le volume **hiérarchisé**.</span><span class="sxs-lookup"><span data-stu-id="77116-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="77116-154">Bonjour **capacité** Indiquez la taille de hello du volume de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="77116-155">Un volume hiérarchisé doit être compris entre 500 Go et 5 To, tandis qu’un volume attaché doit être compris entre 50 Go et 500 Go.</span><span class="sxs-lookup"><span data-stu-id="77116-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="77116-156">Cliquez sur **connecté des ordinateurs hôtes**, sélectionnez un accès contrôle enregistrement (ACR) correspondante toohello initiateur iSCSI que vous souhaitez tooconnect toothis volume, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="77116-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="77116-157">tooadd un nouvel hôte connecté, cliquez sur **ajouter un nouveau**, entrez un nom pour l’hôte de hello et son iSCSI nom qualifié (IQN), puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="77116-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Ajouter un volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="77116-159">Lorsque vous avez terminé de configurer votre volume, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="77116-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="77116-160">Un volume est créé par hello spécifié settings et une notification s’affiche sur la création réussie du hello hello identiques.</span><span class="sxs-lookup"><span data-stu-id="77116-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="77116-161">Par défaut, la sauvegarde sera être activée pour le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="77116-162">tooconfirm qui hello volume a été a été créé correctement, accédez toohello **Volumes** panneau.</span><span class="sxs-lookup"><span data-stu-id="77116-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="77116-163">Vous devez voir volume hello répertorié.</span><span class="sxs-lookup"><span data-stu-id="77116-163">You should see hello volume listed.</span></span>
   
    ![Le volume stimule la réussite](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="77116-165">Modification d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-165">Modify a volume</span></span>

<span data-ttu-id="77116-166">Modifier un volume lorsque vous avez besoin d’hôtes hello toochange qui accèdent aux volumes de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="77116-167">Hello autres attributs d’un volume ne peut pas être modifiées une fois que le volume de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="77116-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="77116-168">toomodify un volume</span><span class="sxs-lookup"><span data-stu-id="77116-168">toomodify a volume</span></span>

1. <span data-ttu-id="77116-169">À partir de hello **Volumes** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello volume que vous souhaitez vous toomodify réside.</span><span class="sxs-lookup"><span data-stu-id="77116-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="77116-170">**Sélectionnez** hello volume et cliquez sur **connecté des ordinateurs hôtes** tooview hello hôte actuellement connecté et modifiez-le tooa un autre serveur.</span><span class="sxs-lookup"><span data-stu-id="77116-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Modifier le volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="77116-172">Enregistrez vos modifications en cliquant sur hello **enregistrer** barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="77116-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="77116-173">Vos paramètres spécifiés sont appliqués ; une notification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="77116-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="77116-174">Mise hors connexion d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-174">Take a volume offline</span></span>

<span data-ttu-id="77116-175">Vous devrez peut-être tootake un volume hors connexion lors de la planification toomodify ou supprimer il.</span><span class="sxs-lookup"><span data-stu-id="77116-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="77116-176">Lorsqu’un volume est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="77116-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="77116-177">Vous devez tootake hello volume hors connexion sur l’ordinateur hôte de hello, ainsi que sur les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="77116-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="77116-178">tootake un volume hors connexion</span><span class="sxs-lookup"><span data-stu-id="77116-178">tootake a volume offline</span></span>

1. <span data-ttu-id="77116-179">Assurez-vous que le volume hello en question n’est pas utilisé avant de mettre hors connexion.</span><span class="sxs-lookup"><span data-stu-id="77116-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="77116-180">Mettez d’abord volume hello hors connexion sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="77116-181">Cela élimine tout risque potentiel de corruption des données sur le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="77116-182">Pour connaître la procédure, consultez instructions toohello de votre système d’exploitation hôte.</span><span class="sxs-lookup"><span data-stu-id="77116-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="77116-183">Une fois le volume hello sur l’ordinateur hôte de hello est hors connexion, prendre les volume hello tableau hello hors connexion en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="77116-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="77116-184">À partir de hello **Volumes** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello volume que vous souhaitez vous tootake hors connexion réside.</span><span class="sxs-lookup"><span data-stu-id="77116-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="77116-185">**Sélectionnez** hello volume et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **mettre hors connexion**.</span><span class="sxs-lookup"><span data-stu-id="77116-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Volume hors connexion](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="77116-187">Passez en revue les informations de hello Bonjour **mettre hors connexion** panneau et confirmez que vous acceptez d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="77116-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="77116-188">Cliquez sur **mettre hors connexion** tootake le volume hello hors connexion.</span><span class="sxs-lookup"><span data-stu-id="77116-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="77116-189">Vous voyez une notification d’opération hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="77116-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="77116-190">tooconfirm hello volume a été correctement mis hors connexion, accédez à toohello **Volumes** panneau.</span><span class="sxs-lookup"><span data-stu-id="77116-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="77116-191">Vous devez normalement voir État hello du volume de hello hors connexion.</span><span class="sxs-lookup"><span data-stu-id="77116-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Confirmation du volume hors connexion](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="77116-193">Suppression d’un volume</span><span class="sxs-lookup"><span data-stu-id="77116-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77116-194">Vous pouvez supprimer un volume uniquement s’il est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="77116-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="77116-195">Terminer hello suivant les étapes toodelete un volume.</span><span class="sxs-lookup"><span data-stu-id="77116-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="77116-196">toodelete un volume</span><span class="sxs-lookup"><span data-stu-id="77116-196">toodelete a volume</span></span>

1. <span data-ttu-id="77116-197">À partir de hello **Volumes** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello volume que vous souhaitez vous toodelete réside.</span><span class="sxs-lookup"><span data-stu-id="77116-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="77116-198">**Sélectionnez** hello volume et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="77116-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Supprimer un volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="77116-200">Vérifier l’état de hello du volume de hello souhaité toodelete.</span><span class="sxs-lookup"><span data-stu-id="77116-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="77116-201">Si hello volume de toodelete n’est pas hors connexion, des étapes il hello hors connexion de tout d’abord, suivant [mettre un volume hors connexion](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="77116-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="77116-202">Lorsque vous êtes invité à confirmer l’opération Bonjour **supprimer** panneau, acceptez la confirmation de hello et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="77116-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="77116-203">volume de Hello va être supprimée et hello **Volumes** panneau affichera la liste hello mis à jour de volumes au sein de l’unité de stockage virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="77116-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77116-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77116-204">Next steps</span></span>

<span data-ttu-id="77116-205">Découvrez comment trop[cloner un volume StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="77116-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

