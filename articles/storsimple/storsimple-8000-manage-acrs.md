---
title: "enregistrements de contrôle d’accès aaaManage dans StorSimple | Documents Microsoft"
description: "Décrit comment le contrôle d’accès toouse enregistre toodetermine (ACR) les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello."
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="25563-103">Utiliser des enregistrements de contrôle d’accès hello StorSimple Manager service toomanage</span><span class="sxs-lookup"><span data-stu-id="25563-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="25563-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="25563-104">Overview</span></span>
<span data-ttu-id="25563-105">Enregistrements de contrôle d’accès (ACR) permettent de toospecify les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="25563-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="25563-106">ACR sont définies les volume spécifique tooa et contenir hello iSCSI (IQN) de noms qualifiés d’hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="25563-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="25563-107">Quand un hôte tente de tooconnect tooa volume, les appareils hello vérifie hello QU'ACR associé à ce volume pour le nom IQN de hello et si une correspondance est trouvée, hello est établie.</span><span class="sxs-lookup"><span data-stu-id="25563-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="25563-108">Hello des enregistrements de contrôle d’accès dans hello **Configuration** section de votre Panneau de service du Gestionnaire de périphériques StorSimple afficher tous les enregistrements de contrôle d’accès hello avec hello correspondant iqn des hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="25563-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="25563-109">Ce didacticiel explique hello suivant ACR tâches :</span><span class="sxs-lookup"><span data-stu-id="25563-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="25563-110">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-110">Add an access control record</span></span>
* <span data-ttu-id="25563-111">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-111">Edit an access control record</span></span>
* <span data-ttu-id="25563-112">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="25563-113">Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="25563-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="25563-114">Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="25563-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="25563-115">Obtenir hello IQN</span><span class="sxs-lookup"><span data-stu-id="25563-115">Get hello IQN</span></span>

<span data-ttu-id="25563-116">Effectuer hello suivant les étapes tooget hello IQN d’un hôte Windows qui exécute Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="25563-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="25563-117">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-117">Add an access control record</span></span>
<span data-ttu-id="25563-118">Vous utilisez hello **Configuration** section hello le Gestionnaire de périphériques StorSimple service panneau tooadd ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="25563-119">En général, vous associez un enregistrement de contrôle d’accès à un volume.</span><span class="sxs-lookup"><span data-stu-id="25563-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="25563-120">Effectuer hello suivant les étapes tooadd un ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="25563-121">tooadd un ACR</span><span class="sxs-lookup"><span data-stu-id="25563-121">tooadd an ACR</span></span>

1. <span data-ttu-id="25563-122">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="25563-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="25563-123">Bonjour **enregistrements de contrôle d’accès** panneau, cliquez sur **+ ajouter un ACR**.</span><span class="sxs-lookup"><span data-stu-id="25563-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="25563-125">Bonjour **ajouter un ACR** panneau, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="25563-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="25563-126">Saisissez un nom pour votre ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="25563-127">Fournissez le nom IQN de hello de votre hôte Windows Server sous **iSCSI (IQN) de nom initiateur**.</span><span class="sxs-lookup"><span data-stu-id="25563-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="25563-128">Cliquez sur **ajouter** toocreate hello ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-128">Click **Add** toocreate hello ACR.</span></span>

        ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="25563-130">Hello récemment ajouté QU'ACR s’affichera dans la liste tabulaire hello d’ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="25563-132">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-132">Edit an access control record</span></span>
<span data-ttu-id="25563-133">Vous utilisez hello **Configuration** section hello le Gestionnaire de périphériques StorSimple service panneau tooedit ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="25563-134">Il vous est recommandé de modifier uniquement les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="25563-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="25563-135">tooedit qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="25563-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="25563-136">Effectuer hello suivant les étapes tooedit un ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="25563-137">tooedit un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="25563-138">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="25563-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="25563-140">Dans hello tabulaire la liste des enregistrements de contrôle d’accès hello, cliquez sur et sélectionnez hello ACR que vous souhaitez toomodify.</span><span class="sxs-lookup"><span data-stu-id="25563-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="25563-142">Bonjour **enregistrement de contrôle d’accès modifier** panneau, fournir un autre hôte tooanother correspondant IQN.</span><span class="sxs-lookup"><span data-stu-id="25563-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="25563-144">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="25563-144">Click **Save**.</span></span> <span data-ttu-id="25563-145">Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="25563-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="25563-147">Vous êtes averti lorsque hello ACR est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="25563-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="25563-148">la liste tabulaire Hello met également à jour les modifications de hello tooreflect.</span><span class="sxs-lookup"><span data-stu-id="25563-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="25563-149">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-149">Delete an access control record</span></span>
<span data-ttu-id="25563-150">Vous utilisez hello **Configuration** section hello le Gestionnaire de périphériques StorSimple service panneau toodelete ACR.</span><span class="sxs-lookup"><span data-stu-id="25563-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="25563-151">Vous pouvez uniquement supprimer les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="25563-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="25563-152">toodelete qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="25563-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="25563-153">Effectuer hello suivant les étapes toodelete un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="25563-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="25563-154">toodelete un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="25563-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="25563-155">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="25563-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="25563-157">Dans hello tabulaire la liste des enregistrements de contrôle d’accès hello, cliquez sur et sélectionnez hello ACR que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="25563-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="25563-159">Menu contextuel de hello tooinvoke et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="25563-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="25563-161">Lorsque vous êtes invité à confirmer l’opération, passez en revue les informations hello et puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="25563-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="25563-163">Vous êtes averti lorsque la suppression hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="25563-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="25563-164">la liste tabulaire Hello est mise à jour tooreflect hello suppression.</span><span class="sxs-lookup"><span data-stu-id="25563-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="25563-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="25563-166">Next steps</span></span>
* <span data-ttu-id="25563-167">En savoir plus sur la [gestion des volumes StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="25563-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="25563-168">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="25563-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

