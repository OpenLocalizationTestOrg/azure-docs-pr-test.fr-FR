---
title: "Gérer les enregistrements de contrôle d’accès pour StorSimple Virtual Array | Microsoft Docs"
description: "Décrit comment gérer les enregistrements de contrôle d’accès pour déterminer les hôtes qui peuvent se connecter à un volume sur le StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="67130-103">Utiliser StorSimple Device Manager pour gérer les enregistrements de contrôle d’accès pour StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="67130-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="67130-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="67130-104">Overview</span></span>

<span data-ttu-id="67130-105">Les enregistrements de contrôle d’accès vous permettent de spécifier les hôtes qui peuvent se connecter à un volume sur le StorSimple Virtual Array (également appelé appareil virtuel local StorSimple).</span><span class="sxs-lookup"><span data-stu-id="67130-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="67130-106">Les enregistrements de contrôle d’accès sont définis pour un volume spécifique et contiennent les noms complets iSCSI (IQN) des ordinateurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="67130-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="67130-107">Quand un hôte essaie de se connecter à un volume, l’appareil vérifie l’enregistrement de contrôle d’accès associé à ce volume pour le nom IQN et, s’il existe une correspondance, la connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="67130-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="67130-108">Le panneau **Enregistrements de contrôle d’accès** de la section **Configuration** de votre service Device Manager affiche tous les enregistrements de contrôle d’accès avec les noms complets iSCSI (IQN) des hôtes correspondants.</span><span class="sxs-lookup"><span data-stu-id="67130-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![Gestion d’enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="67130-110">Le didacticiel décrit les tâches courantes liées aux enregistrements de contrôle d’accès :</span><span class="sxs-lookup"><span data-stu-id="67130-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="67130-111">Obtenir le nom IQN</span><span class="sxs-lookup"><span data-stu-id="67130-111">Get the IQN</span></span>
* <span data-ttu-id="67130-112">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-112">Add an access control record</span></span>
* <span data-ttu-id="67130-113">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-113">Edit an access control record</span></span>
* <span data-ttu-id="67130-114">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="67130-115">Lorsque vous attribuez un enregistrement de contrôle d’accès à un volume, veillez à ce que plusieurs hôtes non cluster n’accèdent pas simultanément au volume, sans quoi celui-ci pourrait être endommagé.</span><span class="sxs-lookup"><span data-stu-id="67130-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="67130-116">Lorsque vous supprimez un enregistrement de contrôle d’accès d’un volume, assurez-vous que l’hôte correspondant n’accède pas au volume, car la suppression pourrait entraîner une perturbation des opérations de lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="67130-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="67130-117">Obtenir le nom IQN</span><span class="sxs-lookup"><span data-stu-id="67130-117">Get the IQN</span></span>

<span data-ttu-id="67130-118">Procédez comme suit pour obtenir le nom IQN d’un hôte Windows exécutant Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="67130-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="67130-119">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-119">Add an ACR</span></span>

<span data-ttu-id="67130-120">Pour ajouter des enregistrements de contrôle d’accès, utilisez le panneau **Enregistrements de contrôle d’accès** de la section **Configuration** de votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="67130-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="67130-121">En général, vous associez un enregistrement de contrôle d’accès à un volume.</span><span class="sxs-lookup"><span data-stu-id="67130-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="67130-122">Pour plus d’informations sur l’association d’un enregistrement de contrôle d’accès à un volume, consultez la page [Ajouter un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="67130-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67130-123">Lorsque vous attribuez un enregistrement de contrôle d’accès à un volume, veillez à ce que plusieurs hôtes non cluster n’accèdent pas simultanément au volume, sans quoi celui-ci pourrait être endommagé.</span><span class="sxs-lookup"><span data-stu-id="67130-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="67130-124">Effectuez les opérations suivantes pour ajouter un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="67130-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="67130-125">Pour ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-125">To add an ACR</span></span>

1. <span data-ttu-id="67130-126">Sur la page d’accueil du service, sélectionnez votre service, double-cliquez sur le nom du service, puis dans la section **Configuration**, cliquez sur **Enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="67130-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="67130-127">Dans le panneau **Enregistrements de contrôle d’accès**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="67130-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="67130-128">Dans le panneau **Ajouter un ACR**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="67130-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="67130-129">Saisissez un **Nom** pour votre ACR.</span><span class="sxs-lookup"><span data-stu-id="67130-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="67130-130">Sous **Nom d’initiateur iSCSI**, indiquez le nom IQN de votre hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="67130-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="67130-131">Pour obtenir le nom IQN de l’hôte Windows Server, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="67130-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="67130-132">Démarrez l’initiateur Microsoft iSCSI sur l’hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="67130-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="67130-133">Dans la fenêtre Propriétés de l’initiateur iSCSI, sous l’onglet **Configuration**, sélectionnez et copiez la chaîne affichée dans le champ **Nom de l’initiateur**.</span><span class="sxs-lookup"><span data-stu-id="67130-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="67130-134">Collez cette chaîne dans le champ **IQN** du panneau **Ajouter un ACR**.</span><span class="sxs-lookup"><span data-stu-id="67130-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="67130-135">Cliquez sur **Ajouter** pour ajouter l’enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="67130-135">Click **Add** to add the ACR.</span></span>  
   
        ![Ajouter des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="67130-137">La liste tabulaire est mise à jour pour refléter les modifications.</span><span class="sxs-lookup"><span data-stu-id="67130-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="67130-138">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-138">Edit an ACR</span></span>

<span data-ttu-id="67130-139">Pour modifier des enregistrements de contrôle d’accès, utilisez le panneau **Enregistrements de contrôle d’accès** de la section **Configuration** de votre service StorSimple Device Manager dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="67130-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="67130-140">Vous ne devez pas modifier un enregistrement de contrôle d’accès en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="67130-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="67130-141">Pour modifier un enregistrement de contrôle d’accès associé à un volume en cours d’utilisation, vous devez d’abord placer le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="67130-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="67130-142">Effectuez les opérations suivantes pour modifier un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="67130-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="67130-143">Pour modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-143">To edit an ACR</span></span>

1. <span data-ttu-id="67130-144">Sur la page d’accueil du service, sélectionnez votre service, double-cliquez sur le nom du service, puis dans la section **Configuration**, cliquez sur **Enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="67130-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="67130-145">Dans la liste tabulaire des enregistrements de contrôle d’accès du panneau **Enregistrements de contrôle d’accès**, double-cliquez sur l’enregistrement que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="67130-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="67130-146">Dans le panneau **Enregistrements de contrôle d’accès**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="67130-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="67130-147">Indiquez le nom qualifié (IQN) de l’enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="67130-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="67130-148">Cliquez sur **Enregistrer** en haut du panneau pour enregistrer l’enregistrement de contrôle d’accès modifié.</span><span class="sxs-lookup"><span data-stu-id="67130-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="67130-149">Le message de confirmation suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="67130-149">You see the following confirmation message:</span></span>
   
        ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="67130-151">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-151">Delete an access control record</span></span>

<span data-ttu-id="67130-152">Pour supprimer des enregistrements de contrôle d’accès, utilisez la page **Configuration** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="67130-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="67130-153">Vous ne devez pas supprimer un enregistrement de contrôle d’accès en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="67130-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="67130-154">Pour supprimer un enregistrement de contrôle d’accès associé à un volume en cours d’utilisation, vous devez d’abord placer le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="67130-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="67130-155">Lorsque vous supprimez un enregistrement de contrôle d’accès d’un volume, assurez-vous que l’hôte correspondant n’accède pas au volume, car la suppression pourrait entraîner une perturbation des opérations de lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="67130-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="67130-156">Pour supprimer un enregistrement de contrôle d’accès, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="67130-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="67130-157">Pour supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="67130-157">To delete an access control record</span></span>

1. <span data-ttu-id="67130-158">Sur la page d’accueil du service, sélectionnez votre service, double-cliquez sur le nom du service, puis dans la section **Configuration**, cliquez sur **Enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="67130-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="67130-159">Dans la liste tabulaire des enregistrements de contrôle d’accès du panneau **Enregistrements de contrôle d’accès**, double-cliquez sur l’enregistrement que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="67130-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="67130-160">Dans le panneau Enregistrements de contrôle d’accès, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="67130-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![Supprimer des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="67130-162">Lorsque vous êtes invité à confirmer la suppression, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="67130-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="67130-163">La liste tabulaire est mise à jour pour refléter la suppression.</span><span class="sxs-lookup"><span data-stu-id="67130-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![Message d'avertissement](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="67130-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67130-165">Next steps</span></span>

* <span data-ttu-id="67130-166">Découvrez comment [ajouter des volumes et configurer les enregistrements de contrôle d’accès](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="67130-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

