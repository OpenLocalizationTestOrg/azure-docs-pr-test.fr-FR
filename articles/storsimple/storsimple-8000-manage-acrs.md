---
title: "Gérer les enregistrements de contrôle d’accès dans StorSimple | Microsoft Docs"
description: "Décrit comment utiliser les enregistrements de contrôle d’accès pour déterminer les hôtes qui peuvent se connecter à un volume sur l’appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="38856-103">Utiliser le service StorSimple Manager pour gérer les enregistrements de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="38856-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="38856-104">Overview</span></span>
<span data-ttu-id="38856-105">Les enregistrements de contrôle d’accès vous permettent de spécifier les hôtes qui peuvent se connecter à un volume sur l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="38856-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="38856-106">Les enregistrements de contrôle d’accès sont définis pour un volume spécifique et contiennent les noms complets iSCSI (IQN) des ordinateurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="38856-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="38856-107">Lorsqu’un hôte essaie de se connecter à un volume, l’appareil vérifie l’enregistrement de contrôle d’accès associé à ce volume pour le nom complet iSCSI (IQN) et s’il existe une correspondance, la connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="38856-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="38856-108">Les enregistrements de contrôle d’accès dans la section **Configuration** du panneau de votre service StorSimple Device Manager affichent tous les enregistrements de contrôle d’accès avec les noms complets iSCSI (IQN) des hôtes correspondants.</span><span class="sxs-lookup"><span data-stu-id="38856-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="38856-109">Le didacticiel décrit les tâches courantes liées aux enregistrements de contrôle d’accès :</span><span class="sxs-lookup"><span data-stu-id="38856-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="38856-110">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-110">Add an access control record</span></span>
* <span data-ttu-id="38856-111">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-111">Edit an access control record</span></span>
* <span data-ttu-id="38856-112">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="38856-113">Lorsque vous attribuez un enregistrement de contrôle d’accès à un volume, veillez à ce que plusieurs hôtes non cluster n’accèdent pas simultanément au volume, sans quoi celui-ci pourrait être endommagé.</span><span class="sxs-lookup"><span data-stu-id="38856-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="38856-114">Lorsque vous supprimez un enregistrement de contrôle d’accès d’un volume, assurez-vous que l’hôte correspondant n’accède pas au volume, car la suppression pourrait entraîner une perturbation des opérations de lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="38856-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="38856-115">Obtenir le nom IQN</span><span class="sxs-lookup"><span data-stu-id="38856-115">Get the IQN</span></span>

<span data-ttu-id="38856-116">Procédez comme suit pour obtenir le nom IQN d’un hôte Windows exécutant Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="38856-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="38856-117">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-117">Add an access control record</span></span>
<span data-ttu-id="38856-118">Vous utilisez la section **Configuration** dans le panneau du service StorSimple Device Manager pour ajouter des enregistrements de contrôle d’accès (ACR).</span><span class="sxs-lookup"><span data-stu-id="38856-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="38856-119">En général, vous associez un enregistrement de contrôle d’accès à un volume.</span><span class="sxs-lookup"><span data-stu-id="38856-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="38856-120">Effectuez les opérations suivantes pour ajouter un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="38856-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="38856-121">Pour ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-121">To add an ACR</span></span>

1. <span data-ttu-id="38856-122">Accédez à votre service StorSimple Device Manager, double-cliquez sur le nom du service puis, dans la section **Configuration**, cliquez sur **Enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="38856-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="38856-123">Dans le panneau **Enregistrements de contrôle d’accès**, cliquez sur **+ Ajouter un ACR**.</span><span class="sxs-lookup"><span data-stu-id="38856-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="38856-125">Dans le panneau **Ajouter un ACR**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="38856-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="38856-126">Saisissez un nom pour votre ACR.</span><span class="sxs-lookup"><span data-stu-id="38856-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="38856-127">Sous **Nom d’initiateur iSCSI (IQN)**, indiquez le nom IQN de votre hôte Windows Server.</span><span class="sxs-lookup"><span data-stu-id="38856-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="38856-128">Cliquez sur **Ajouter** pour créer l’ACR.</span><span class="sxs-lookup"><span data-stu-id="38856-128">Click **Add** to create the ACR.</span></span>

        ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="38856-130">L’ACR nouvellement ajouté s’affiche dans la liste tabulaire d’ACR.</span><span class="sxs-lookup"><span data-stu-id="38856-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="38856-132">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-132">Edit an access control record</span></span>
<span data-ttu-id="38856-133">Vous utilisez la section **Configuration** dans le panneau du service StorSimple Device Manager pour modifier des enregistrements de contrôle d’accès (ACR).</span><span class="sxs-lookup"><span data-stu-id="38856-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="38856-134">Il vous est recommandé de modifier uniquement les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="38856-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="38856-135">Pour modifier un enregistrement de contrôle d’accès associé à un volume en cours d’utilisation, vous devez d’abord placer le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="38856-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="38856-136">Effectuez les opérations suivantes pour modifier un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="38856-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="38856-137">Pour modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-137">To edit an access control record</span></span>
1.  <span data-ttu-id="38856-138">Accédez à votre service StorSimple Device Manager, double-cliquez sur le nom du service puis, dans la section **Configuration**, cliquez sur **Enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="38856-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Accéder aux enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="38856-140">Dans la liste tabulaire des enregistrements de contrôle d’accès, cliquez et sélectionnez l’enregistrement que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="38856-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="38856-142">Dans le panneau **Modifier l’enregistrement de contrôle d’accès**, indiquez un autre IQN correspondant à un autre hôte.</span><span class="sxs-lookup"><span data-stu-id="38856-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="38856-144">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="38856-144">Click **Save**.</span></span> <span data-ttu-id="38856-145">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="38856-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="38856-147">Vous êtes informé lorsque l’ACR est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="38856-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="38856-148">La liste tabulaire est également mise à jour pour refléter la modification.</span><span class="sxs-lookup"><span data-stu-id="38856-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="38856-149">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-149">Delete an access control record</span></span>
<span data-ttu-id="38856-150">Vous utilisez la section **Configuration** dans le panneau du service StorSimple Device Manager pour supprimer des enregistrements de contrôle d’accès (ACR).</span><span class="sxs-lookup"><span data-stu-id="38856-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="38856-151">Vous pouvez uniquement supprimer les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="38856-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="38856-152">Pour supprimer un enregistrement de contrôle d’accès associé à un volume en cours d’utilisation, vous devez d’abord placer le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="38856-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="38856-153">Pour supprimer un enregistrement de contrôle d’accès, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="38856-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="38856-154">Pour supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="38856-154">To delete an access control record</span></span>
1.  <span data-ttu-id="38856-155">Accédez à votre service StorSimple Device Manager, double-cliquez sur le nom du service puis, dans la section **Configuration**, cliquez sur **Enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="38856-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Accéder aux enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="38856-157">Dans la liste tabulaire des enregistrements de contrôle d’accès, cliquez et sélectionnez l’enregistrement que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="38856-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Accéder aux enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="38856-159">Cliquez avec le bouton droit pour appeler le menu contextuel, puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="38856-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Accéder aux enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="38856-161">Lorsque vous êtes invité à confirmer l’opération, passez en revue les informations, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="38856-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Accéder aux enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="38856-163">Vous êtes informé lorsque la suppression est terminée.</span><span class="sxs-lookup"><span data-stu-id="38856-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="38856-164">La liste tabulaire est mise à jour pour refléter la suppression.</span><span class="sxs-lookup"><span data-stu-id="38856-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Accéder aux enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="38856-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38856-166">Next steps</span></span>
* <span data-ttu-id="38856-167">En savoir plus sur la [gestion des volumes StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="38856-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="38856-168">En savoir plus sur [l’utilisation du service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="38856-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

