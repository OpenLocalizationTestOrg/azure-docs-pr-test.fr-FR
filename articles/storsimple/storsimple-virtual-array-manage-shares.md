---
title: partage de StorSimple Virtual Array aaaManage | Documents Microsoft
description: "Décrit les hello StorSimple le Gestionnaire de périphériques et explique comment toouse il partages toomanage sur votre tableau virtuel StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="fa1fa-103">Utiliser des partages toomanage du service de gestionnaire de périphériques StorSimple hello sur hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="fa1fa-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="fa1fa-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fa1fa-104">Overview</span></span>

<span data-ttu-id="fa1fa-105">Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gérer les partages sur votre tableau virtuel StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="fa1fa-106">Hello service du Gestionnaire de périphériques StorSimple est une extension Bonjour portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="fa1fa-107">Dans Ajout toomanaging partages et les volumes, vous pouvez utiliser hello le Gestionnaire de périphériques StorSimple service tooview gérer les appareils, afficher les alertes, gérer les stratégies de sauvegarde et gérer le catalogue de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="fa1fa-108">Types de partages</span><span class="sxs-lookup"><span data-stu-id="fa1fa-108">Share Types</span></span>

<span data-ttu-id="fa1fa-109">Les partages StorSimple peuvent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="fa1fa-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="fa1fa-110">**Attaché localement**: les données dans ces partages reste sur le tableau de hello en permanence et ne pas déborder toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="fa1fa-111">**Niveaux**: les données dans ces partages peuvent déborder toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="fa1fa-112">Lorsque vous créez un partage hiérarchisé, environ 10 % d’espace de hello est approvisionné sur le niveau de local hello et 90 % d’espace de hello est configuré dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="fa1fa-113">Par exemple, si vous avez configuré un partage de 1 To, 100 Go peut résider dans un espace local hello et 900 Go sera utilisée dans le cloud de hello hello lorsque des niveaux de données.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="fa1fa-114">À son tour, cela implique que si vous manquez tout l’espace local hello sur l’appareil de hello, vous ne pouvez pas configurer un partage hiérarchisé (car hello 10 % requis sur hello local niveau ne sera pas disponible).</span><span class="sxs-lookup"><span data-stu-id="fa1fa-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="fa1fa-115">Capacité allouée</span><span class="sxs-lookup"><span data-stu-id="fa1fa-115">Provisioned capacity</span></span>

<span data-ttu-id="fa1fa-116">Consultez toohello tableau pour une capacité déployée maximale pour chaque type de partage suivant.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="fa1fa-117">**Identificateur de la limite**</span><span class="sxs-lookup"><span data-stu-id="fa1fa-117">**Limit identifier**</span></span> | <span data-ttu-id="fa1fa-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="fa1fa-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="fa1fa-119">Taille minimale d’un partage hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="fa1fa-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="fa1fa-120">500 Go</span><span class="sxs-lookup"><span data-stu-id="fa1fa-120">500 GB</span></span> |
| <span data-ttu-id="fa1fa-121">Taille maximale d’un partage hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="fa1fa-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="fa1fa-122">20 To</span><span class="sxs-lookup"><span data-stu-id="fa1fa-122">20 TB</span></span> |
| <span data-ttu-id="fa1fa-123">Taille minimale d'un partage épinglé localement</span><span class="sxs-lookup"><span data-stu-id="fa1fa-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="fa1fa-124">50 Go</span><span class="sxs-lookup"><span data-stu-id="fa1fa-124">50 GB</span></span> |
| <span data-ttu-id="fa1fa-125">Taille maximale d'un partage épinglé localement</span><span class="sxs-lookup"><span data-stu-id="fa1fa-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="fa1fa-126">2 To</span><span class="sxs-lookup"><span data-stu-id="fa1fa-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="fa1fa-127">Panneau de partages Hello</span><span class="sxs-lookup"><span data-stu-id="fa1fa-127">hello Shares blade</span></span>

<span data-ttu-id="fa1fa-128">Hello **partages** menu sur votre Panneau de résumé du service StorSimple affiche la liste hello des partages de stockage sur un tableau de StorSimple donné et vous permet de toomanage les.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Panneau Partages](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="fa1fa-130">Un partage est constitué d’une série d’attributs :</span><span class="sxs-lookup"><span data-stu-id="fa1fa-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="fa1fa-131">**Nom de partage** : un nom descriptif qui doit être uniques et permet d’identifier le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="fa1fa-132">**État** : peut être en ligne ou hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="fa1fa-133">Si un partage est hors connexion, utilisateurs du partage de hello ne seront pas en mesure de tooaccess il.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="fa1fa-134">**Type** – indique si le partage de hello est **à plusieurs niveaux** (hello par défaut) ou **attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="fa1fa-135">**Capacité** – spécifie la quantité hello de données utilisées comme comparés toohello la quantité totale de données qui peuvent être stockées sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="fa1fa-136">**Description** – un paramètre facultatif qui permet de décrire le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="fa1fa-137">**Autorisations** -hello autorisations toohello partage NTFS qui peut être géré via l’Explorateur Windows.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="fa1fa-138">**Sauvegarde** : en cas de hello StorSimple Virtual Array, tous les partages sont automatiquement activés pour sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Détails des partages](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="fa1fa-140">Suivez les instructions de hello dans cette hello didacticiel tooperform tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="fa1fa-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="fa1fa-141">Ajouter un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-141">Add a share</span></span>
* <span data-ttu-id="fa1fa-142">Modifier un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-142">Modify a share</span></span>
* <span data-ttu-id="fa1fa-143">Mettre un partage hors connexion</span><span class="sxs-lookup"><span data-stu-id="fa1fa-143">Take a share offline</span></span>
* <span data-ttu-id="fa1fa-144">Supprimer un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="fa1fa-145">Ajouter un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-145">Add a share</span></span>

1. <span data-ttu-id="fa1fa-146">Dans le volet Résumé du service de StorSimple hello, cliquez sur **+ ajouter partage** à partir de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="fa1fa-147">Cela ouvre hello **ajouter partage** panneau.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-147">This opens up hello **Add share** blade.</span></span>

    ![Ajouter un partage](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="fa1fa-149">Bonjour **ajouter partage** panneau, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fa1fa-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="fa1fa-150">Bonjour **nom de partage** , entrez un nom unique pour le partage.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="fa1fa-151">nom de Hello doit être une chaîne qui contient des caractères too127 3.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="fa1fa-152">Facultatif **Description** pour partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="fa1fa-153">description de Hello aidera à identifier les propriétaires de partage hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="fa1fa-154">Bonjour **Type** déroulante liste, spécifiez si toocreate un **à plusieurs niveaux** ou **attaché localement** partager.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="fa1fa-155">Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un **Partage attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="fa1fa-156">Pour toutes les autres données, sélectionnez un partage **Hiérarchisé**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="fa1fa-157">Bonjour **capacité** Indiquez la taille de hello du partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="fa1fa-158">Un partage hiérarchisé doit être compris entre 500 Go et 20 To, tandis qu’un partage attaché doit être compris entre 50 Go et 2 To.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="fa1fa-159">Bonjour **valeur par défaut toutes les autorisations** champ, affecter hello autorisations toohello utilisateur ou groupe hello qui accède à ce partage.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="fa1fa-160">Spécifier le nom hello de hello utilisateur ou un groupe d’utilisateurs hello  _john@contoso.com_  format.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="fa1fa-161">Nous vous recommandons d’utiliser un tooaccess des privilèges d’administrateur utilisateur groupe (au lieu d’un seul utilisateur) tooallow ces partages.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="fa1fa-162">Une fois que vous avez affecté des autorisations hello ici, vous pouvez ensuite utiliser l’Explorateur de fichiers toomodify ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="fa1fa-163">Lorsque vous avez terminé de configurer votre partage, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="fa1fa-164">Un partage sera créé avec hello spécifié les paramètres et que vous voyez une notification.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="fa1fa-165">Par défaut, la sauvegarde sera être activée pour le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="fa1fa-166">tooconfirm qui hello partage a été a été créé correctement, accédez toohello **partages** panneau.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="fa1fa-167">Vous devez voir hello partager répertoriées.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-167">You should see hello share listed.</span></span>
   
    ![Le partage stimule la réussite.](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="fa1fa-169">Modifier un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-169">Modify a share</span></span>

<span data-ttu-id="fa1fa-170">Modifier un partage lorsque vous avez besoin de description de hello toochange du partage de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="fa1fa-171">Aucun autres propriétés de partage ne peuvent être modifiées une fois que le partage de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="fa1fa-172">toomodify un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-172">toomodify a share</span></span>

1. <span data-ttu-id="fa1fa-173">À partir de hello **partages** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello partage que vous souhaitez vous toomodify réside.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="fa1fa-174">**Sélectionnez** hello description actuelle de partage tooview hello et le modifier.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="fa1fa-175">Enregistrez vos modifications en cliquant sur hello **enregistrer** barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="fa1fa-176">Vos paramètres spécifiés sont appliqués ; une notification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="fa1fa-177">Modifier un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="fa1fa-178">Mettre un partage hors connexion</span><span class="sxs-lookup"><span data-stu-id="fa1fa-178">Take a share offline</span></span>

<span data-ttu-id="fa1fa-179">Vous devrez peut-être tootake un partage hors connexion lors de la planification toomodify ou supprimer il.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="fa1fa-180">Lorsqu’un partage est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="fa1fa-181">Vous devez tootake hello partage hors connexion sur l’ordinateur hôte de hello, ainsi que sur les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="fa1fa-182">tootake un partage hors connexion</span><span class="sxs-lookup"><span data-stu-id="fa1fa-182">tootake a share offline</span></span>

1. <span data-ttu-id="fa1fa-183">Assurez-vous que ce partage hello en question n’est pas en cours d’utilisation avant sa mise hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="fa1fa-184">Prendre hello partage tableau hello hors connexion en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fa1fa-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="fa1fa-185">À partir de hello **partages** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello partage que vous souhaitez vous tootake hors connexion réside.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="fa1fa-186">**Sélectionnez** du partage de hello et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **mettre hors connexion**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Partage hors connexion](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="fa1fa-188">Passez en revue les informations de hello Bonjour **mettre hors connexion** panneau et confirmez que vous acceptez d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="fa1fa-189">Cliquez sur **mettre hors connexion** partage de hello tootake hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="fa1fa-190">Vous voyez une notification d’opération hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="fa1fa-191">tooconfirm qui hello partage a été effectuée correctement hors connexion, accédez toohello **partages** panneau.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="fa1fa-192">Vous devez voir l’état hello du partage hello comme étant hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="fa1fa-193">Supprimer un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa1fa-194">Un partage peut être supprimé uniquement s’il est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="fa1fa-195">Hello complet suivant les étapes toodelete un partage.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="fa1fa-196">toodelete un partage</span><span class="sxs-lookup"><span data-stu-id="fa1fa-196">toodelete a share</span></span>

1. <span data-ttu-id="fa1fa-197">À partir de hello **partages** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le partage hello vous souhaitez toodelete réside.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="fa1fa-198">**Sélectionnez** du partage de hello et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Supprimer un partage](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="fa1fa-200">Vérifier l’état de hello du partage de hello souhaité toodelete.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="fa1fa-201">Si le partage hello toodelete n’est pas hors connexion, mettre hors connexion tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="fa1fa-202">Suivez les étapes de hello dans [hors connexion un partage](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="fa1fa-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="fa1fa-203">Lorsque vous êtes invité à confirmer l’opération Bonjour **supprimer** panneau, acceptez la confirmation de hello et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="fa1fa-204">partage de Hello va être supprimée et hello **partages** panneau affiche la liste de hello mis à jour d’actions au sein de l’unité de stockage virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="fa1fa-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa1fa-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fa1fa-205">Next steps</span></span>
<span data-ttu-id="fa1fa-206">Découvrez comment trop[cloner un partage de StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="fa1fa-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

