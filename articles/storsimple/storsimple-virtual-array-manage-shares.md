---
title: "Gérer des partages StorSimple Virtual Array | Microsoft Docs"
description: "Décrit le service StorSimple Device Manager et vous explique comment l’utiliser pour gérer des partages sur votre instance StorSimple Virtual Array."
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
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="86c51-103">Utiliser le service StorSimple Device Manager pour gérer des partages sur l’instance StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="86c51-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="86c51-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="86c51-104">Overview</span></span>

<span data-ttu-id="86c51-105">Ce didacticiel explique comment utiliser le service StorSimple Device Manager pour créer et gérer des partages sur votre instance StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="86c51-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="86c51-106">Le service StorSimple Device Manager est une extension dans le portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web.</span><span class="sxs-lookup"><span data-stu-id="86c51-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="86c51-107">Outre la gestion des partages et des volumes, le service StorSimple Device Manager prend en charge l’affichage et la gestion des appareils, l’affichage des alertes, la gestion des stratégies de sauvegardes et la gestion du catalogue de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="86c51-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="86c51-108">Types de partages</span><span class="sxs-lookup"><span data-stu-id="86c51-108">Share Types</span></span>

<span data-ttu-id="86c51-109">Les partages StorSimple peuvent être les suivants :</span><span class="sxs-lookup"><span data-stu-id="86c51-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="86c51-110">**Attaché localement** : les données de ces partages demeurent à tout moment sur le tableau ; elles ne débordent pas sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="86c51-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="86c51-111">**Hiérarchisé** : les données de ces partages peuvent déborder sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="86c51-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="86c51-112">Lorsque vous créez un partage à plusieurs niveaux, environ 10 % de l’espace est configuré au niveau local et 90 % dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="86c51-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="86c51-113">Par exemple, si vous avez configuré un partage de 1 To, 100 Go résident dans l’espace local et 900 Go sont utilisés dans le cloud lorsque les données sont stockées en niveaux.</span><span class="sxs-lookup"><span data-stu-id="86c51-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="86c51-114">Cela implique que si vous n’avez plus d’espace local sur l’appareil, vous ne pouvez pas configurer un partage à plusieurs niveaux (car les 10 % requis sur l’espace local ne seront pas disponibles).</span><span class="sxs-lookup"><span data-stu-id="86c51-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="86c51-115">Capacité allouée</span><span class="sxs-lookup"><span data-stu-id="86c51-115">Provisioned capacity</span></span>

<span data-ttu-id="86c51-116">Reportez-vous au tableau suivant pour connaître la capacité maximale allouée pour chaque type de partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="86c51-117">**Identificateur de la limite**</span><span class="sxs-lookup"><span data-stu-id="86c51-117">**Limit identifier**</span></span> | <span data-ttu-id="86c51-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="86c51-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="86c51-119">Taille minimale d’un partage hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="86c51-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="86c51-120">500 Go</span><span class="sxs-lookup"><span data-stu-id="86c51-120">500 GB</span></span> |
| <span data-ttu-id="86c51-121">Taille maximale d’un partage hiérarchisé</span><span class="sxs-lookup"><span data-stu-id="86c51-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="86c51-122">20 To</span><span class="sxs-lookup"><span data-stu-id="86c51-122">20 TB</span></span> |
| <span data-ttu-id="86c51-123">Taille minimale d'un partage épinglé localement</span><span class="sxs-lookup"><span data-stu-id="86c51-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="86c51-124">50 Go</span><span class="sxs-lookup"><span data-stu-id="86c51-124">50 GB</span></span> |
| <span data-ttu-id="86c51-125">Taille maximale d'un partage épinglé localement</span><span class="sxs-lookup"><span data-stu-id="86c51-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="86c51-126">2 To</span><span class="sxs-lookup"><span data-stu-id="86c51-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="86c51-127">Le panneau Partages</span><span class="sxs-lookup"><span data-stu-id="86c51-127">The Shares blade</span></span>

<span data-ttu-id="86c51-128">Sur le panneau de synthèse du service StorSimple, le menu **Partages** affiche la liste des partages de stockage sur un tableau StorSimple considéré et vous donne les moyens de les gérer.</span><span class="sxs-lookup"><span data-stu-id="86c51-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![Panneau Partages](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="86c51-130">Un partage est constitué d’une série d’attributs :</span><span class="sxs-lookup"><span data-stu-id="86c51-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="86c51-131">**Nom du partage** : nom descriptif qui doit être unique et vous aide à identifier le partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="86c51-132">**État** : peut être en ligne ou hors connexion.</span><span class="sxs-lookup"><span data-stu-id="86c51-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="86c51-133">Si un partage est hors connexion, ses utilisateurs ne seront pas en mesure d’y accéder.</span><span class="sxs-lookup"><span data-stu-id="86c51-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="86c51-134">**Type** : indique si le partage est **Hiérarchisé** (valeur par défaut) ou **Attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="86c51-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="86c51-135">**Capacité** : spécifie la quantité de données utilisées par rapport au volume total des données pouvant être stockées sur le partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="86c51-136">**Description** : un paramètre facultatif décrivant le partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="86c51-137">**Autorisations** : les autorisations NTFS d’accès au partage pouvant être gérées via l’Explorateur Windows.</span><span class="sxs-lookup"><span data-stu-id="86c51-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="86c51-138">**Sauvegarde** : dans le cas d’une instance StorSimple Virtual Array, l’ensemble des partages sont automatiquement activés pour la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="86c51-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Détails des partages](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="86c51-140">Suivez les instructions de ce didacticiel pour effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="86c51-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="86c51-141">Ajouter un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-141">Add a share</span></span>
* <span data-ttu-id="86c51-142">Modifier un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-142">Modify a share</span></span>
* <span data-ttu-id="86c51-143">Mettre un partage hors connexion</span><span class="sxs-lookup"><span data-stu-id="86c51-143">Take a share offline</span></span>
* <span data-ttu-id="86c51-144">Supprimer un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="86c51-145">Ajouter un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-145">Add a share</span></span>

1. <span data-ttu-id="86c51-146">À partir du panneau de synthèse du service StorSimple, cliquez sur **+ Ajouter un partage** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="86c51-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="86c51-147">Le panneau **Ajouter un partage** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="86c51-147">This opens up the **Add share** blade.</span></span>

    ![Ajouter un partage](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="86c51-149">Dans le panneau **Ajouter un partage**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86c51-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="86c51-150">Dans le champ **Nom du partage**, entrez un nom unique pour votre partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="86c51-151">Le nom doit être une chaîne contenant entre 3 et 127 caractères.</span><span class="sxs-lookup"><span data-stu-id="86c51-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="86c51-152">Une **Description** facultative pour le partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-152">An optional **Description** for the share.</span></span> <span data-ttu-id="86c51-153">La description permet d'identifier les propriétaires du partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="86c51-154">Dans la liste déroulante **Type**, spécifiez si vous souhaitez créer un partage **Hiérarchisé** ou **Attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="86c51-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="86c51-155">Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un **Partage attaché localement**.</span><span class="sxs-lookup"><span data-stu-id="86c51-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="86c51-156">Pour toutes les autres données, sélectionnez un partage **Hiérarchisé**.</span><span class="sxs-lookup"><span data-stu-id="86c51-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="86c51-157">Dans le champ **Capacité**, spécifiez la taille du partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="86c51-158">Un partage hiérarchisé doit être compris entre 500 Go et 20 To, tandis qu’un partage attaché doit être compris entre 50 Go et 2 To.</span><span class="sxs-lookup"><span data-stu-id="86c51-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="86c51-159">Dans le champ **Affecter une autorisation d’accès total par défaut**, attribuez les autorisations à l’utilisateur ou au groupe qui doivent accéder à ce partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="86c51-160">Spécifiez le nom de l’utilisateur ou du groupe d’utilisateurs au format _john@contoso.com_.</span><span class="sxs-lookup"><span data-stu-id="86c51-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="86c51-161">Nous vous recommandons d'utiliser un groupe d'utilisateurs (plutôt qu'un seul utilisateur) lorsque vous accordez des privilèges d'administrateur pour accéder à ces partages.</span><span class="sxs-lookup"><span data-stu-id="86c51-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="86c51-162">Après avoir attribué les autorisations à cet emplacement, vous pouvez utiliser l’Explorateur de fichiers par la suite pour modifier ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="86c51-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="86c51-163">Lorsque vous avez terminé de configurer votre partage, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="86c51-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="86c51-164">Un partage est créé avec les paramètres spécifiés ; une notification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="86c51-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="86c51-165">Par défaut, la sauvegarde est activée pour le partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="86c51-166">Pour vérifier que le partage a été créé, accédez au panneau **Partages**.</span><span class="sxs-lookup"><span data-stu-id="86c51-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="86c51-167">Le partage devrait y apparaître.</span><span class="sxs-lookup"><span data-stu-id="86c51-167">You should see the share listed.</span></span>
   
    ![Le partage stimule la réussite.](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="86c51-169">Modifier un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-169">Modify a share</span></span>

<span data-ttu-id="86c51-170">Modifiez un partage lorsque vous devez modifier sa description.</span><span class="sxs-lookup"><span data-stu-id="86c51-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="86c51-171">Une fois le partage créé, aucune autre propriété de partage ne peut être modifiée.</span><span class="sxs-lookup"><span data-stu-id="86c51-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="86c51-172">Pour modifier un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-172">To modify a share</span></span>

1. <span data-ttu-id="86c51-173">À partir du paramètre **Partages** du panneau de synthèse du service StorSimple, sélectionnez le tableau virtuel sur lequel est hébergé le partage à modifier.</span><span class="sxs-lookup"><span data-stu-id="86c51-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="86c51-174">**Sélectionnez** le partage pour afficher la description actuelle et le modifier.</span><span class="sxs-lookup"><span data-stu-id="86c51-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="86c51-175">Pour enregistrer les modifications, cliquez sur la barre de commandes **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="86c51-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="86c51-176">Vos paramètres spécifiés sont appliqués ; une notification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="86c51-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="86c51-177">Modifier un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="86c51-178">Mettre un partage hors connexion</span><span class="sxs-lookup"><span data-stu-id="86c51-178">Take a share offline</span></span>

<span data-ttu-id="86c51-179">Si vous envisagez de modifier ou de supprimer un partage, il vous faudra éventuellement le déplacer hors connexion.</span><span class="sxs-lookup"><span data-stu-id="86c51-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="86c51-180">Lorsqu’un partage est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="86c51-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="86c51-181">Ce déplacement hors connexion s’effectue sur l’hôte et sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="86c51-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="86c51-182">Pour déplacer un partage hors connexion</span><span class="sxs-lookup"><span data-stu-id="86c51-182">To take a share offline</span></span>

1. <span data-ttu-id="86c51-183">Assurez-vous que le partage en question n’est pas utilisé avant de le mettre hors connexion.</span><span class="sxs-lookup"><span data-stu-id="86c51-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="86c51-184">Pour déplacer le partage sur le tableau hors connexion, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86c51-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="86c51-185">À partir du paramètre **Partages** du panneau de synthèse du service StorSimple, sélectionnez le panneau virtuel sur lequel est hébergé le partage que vous souhaitez déplacer hors connexion.</span><span class="sxs-lookup"><span data-stu-id="86c51-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="86c51-186">**Sélectionnez** le partage, puis cliquez sur **...** (sinon cliquez avec le bouton droit sur cette ligne), puis dans le menu contextuel, sélectionnez **Mettre hors connexion**.</span><span class="sxs-lookup"><span data-stu-id="86c51-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Partage hors connexion](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="86c51-188">Passez en revue les informations du panneau **Mettre hors connexion**, puis confirmez votre acceptation de l’opération.</span><span class="sxs-lookup"><span data-stu-id="86c51-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="86c51-189">Cliquez sur **Mettre hors connexion** pour déplacer le partage.</span><span class="sxs-lookup"><span data-stu-id="86c51-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="86c51-190">Une notification de l’opération en cours s’affiche.</span><span class="sxs-lookup"><span data-stu-id="86c51-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="86c51-191">Pour vérifier que le partage a été mis hors connexion, accédez au panneau **Partages**.</span><span class="sxs-lookup"><span data-stu-id="86c51-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="86c51-192">Le partage doit apparaître comme élément hors connexion.</span><span class="sxs-lookup"><span data-stu-id="86c51-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="86c51-193">Supprimer un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86c51-194">Un partage peut être supprimé uniquement s’il est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="86c51-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="86c51-195">Pour supprimer un partage, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="86c51-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="86c51-196">Pour supprimer un partage</span><span class="sxs-lookup"><span data-stu-id="86c51-196">To delete a share</span></span>

1. <span data-ttu-id="86c51-197">À partir du paramètre **Partages** du panneau de synthèse du service StorSimple, sélectionnez le tableau virtuel sur lequel est hébergé le partage à supprimer.</span><span class="sxs-lookup"><span data-stu-id="86c51-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="86c51-198">**Sélectionnez** le partage, puis cliquez sur **...** (sinon cliquez avec le bouton droit sur cette ligne), puis dans le menu contextuel, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="86c51-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Supprimer un partage](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="86c51-200">Vérifiez l’état du partage à supprimer.</span><span class="sxs-lookup"><span data-stu-id="86c51-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="86c51-201">Si le partage que vous souhaitez supprimer n’est pas hors connexion, déplacez-le dans un premier temps.</span><span class="sxs-lookup"><span data-stu-id="86c51-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="86c51-202">Suivez les étapes de [Mettre un partage hors connexion](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="86c51-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="86c51-203">Lorsque vous êtes invité à confirmer l’opération dans le panneau **Supprimer**, validez la confirmation, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="86c51-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="86c51-204">Le partage est mis à jour, et le panneau **Partages** représente la liste mise à jour des partages dans le tableau virtuel.</span><span class="sxs-lookup"><span data-stu-id="86c51-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c51-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86c51-205">Next steps</span></span>
<span data-ttu-id="86c51-206">Découvrez comment [cloner un partage StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="86c51-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

