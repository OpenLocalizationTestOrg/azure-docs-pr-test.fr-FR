---
title: "enregistrements de contrôle d’accès aaaManage pour StorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment le contrôle d’accès toomanage enregistre toodetermine (ACR) les hôtes qui peuvent se connecter tooa volume hello StorSimple Virtual Array."
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
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="37f55-103">Utilisez le Gestionnaire de périphérique StorSimple toomanage des enregistrements de contrôle d’accès pour StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="37f55-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="37f55-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="37f55-104">Overview</span></span>

<span data-ttu-id="37f55-105">Enregistrements de contrôle d’accès (ACR) permettent de toospecify les hôtes qui peuvent se connecter tooa volume hello StorSimple Virtual Array (également appelé hello local périphérique virtuel StorSimple).</span><span class="sxs-lookup"><span data-stu-id="37f55-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="37f55-106">ACR sont définies les volume spécifique tooa et contenir hello iSCSI (IQN) de noms qualifiés d’hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="37f55-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="37f55-107">Quand un hôte tente de tooconnect tooa volume, les appareils hello vérifie hello ACR associé à ce volume pour le nom IQN de hello, et s’il existe une correspondance, puis hello est établie.</span><span class="sxs-lookup"><span data-stu-id="37f55-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="37f55-108">Hello **enregistrements de contrôle d’accès** panneau dans hello **Configuration** section de votre service de gestionnaire de périphériques affiche tous les enregistrements de contrôle d’accès hello avec hello correspondant iqn des hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="37f55-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Gestion d’enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="37f55-110">Ce didacticiel explique hello suivant ACR tâches :</span><span class="sxs-lookup"><span data-stu-id="37f55-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="37f55-111">Obtenir hello IQN</span><span class="sxs-lookup"><span data-stu-id="37f55-111">Get hello IQN</span></span>
* <span data-ttu-id="37f55-112">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-112">Add an access control record</span></span>
* <span data-ttu-id="37f55-113">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-113">Edit an access control record</span></span>
* <span data-ttu-id="37f55-114">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="37f55-115">Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="37f55-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="37f55-116">Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="37f55-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="37f55-117">Obtenir hello IQN</span><span class="sxs-lookup"><span data-stu-id="37f55-117">Get hello IQN</span></span>

<span data-ttu-id="37f55-118">Effectuer hello suivant les étapes tooget hello IQN d’un hôte Windows qui exécute Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="37f55-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="37f55-119">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-119">Add an ACR</span></span>

<span data-ttu-id="37f55-120">Vous utilisez **enregistrements de contrôle d’accès** panneau dans hello **Configuration** section de votre tooadd de service du Gestionnaire de périphériques StorSimple ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="37f55-121">En général, vous associez un enregistrement de contrôle d’accès à un volume.</span><span class="sxs-lookup"><span data-stu-id="37f55-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="37f55-122">Pour plus d’informations sur l’association d’un ACR à un volume, accédez trop[ajouter un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="37f55-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37f55-123">Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="37f55-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="37f55-124">Effectuer hello suivant les étapes tooadd un ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="37f55-125">tooadd un ACR</span><span class="sxs-lookup"><span data-stu-id="37f55-125">tooadd an ACR</span></span>

1. <span data-ttu-id="37f55-126">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="37f55-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="37f55-127">Bonjour **enregistrements de contrôle d’accès** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="37f55-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="37f55-128">Bonjour **ajouter un ACR** panneau, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="37f55-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="37f55-129">Saisissez un **Nom** pour votre ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="37f55-130">Sous **nom de l’initiateur iSCSI**, fournissez le nom IQN de hello de votre hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="37f55-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="37f55-131">tooget hello IQN de votre hôte Windows Server, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="37f55-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="37f55-132">Démarrez l’initiateur iSCSI Microsoft hello sur votre hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="37f55-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="37f55-133">Dans la fenêtre Propriétés de l’initiateur iSCSI hello, sur hello **Configuration** , sélectionnez et copiez les chaîne hello de hello **nom de l’initiateur** champ.</span><span class="sxs-lookup"><span data-stu-id="37f55-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="37f55-134">Collez cette chaîne Bonjour **IQN** champ hello **ajouter un ACR** panneau.</span><span class="sxs-lookup"><span data-stu-id="37f55-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="37f55-135">Cliquez sur **ajouter** tooadd hello ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Ajouter des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="37f55-137">Hello Liste tabulaire est mis à jour tooreflect cet ajout.</span><span class="sxs-lookup"><span data-stu-id="37f55-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="37f55-138">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-138">Edit an ACR</span></span>

<span data-ttu-id="37f55-139">Vous utilisez hello **enregistrements de contrôle d’accès** panneau dans hello **Configuration** section de votre service de gestionnaire de périphériques Bonjour Azure tooedit portail ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="37f55-140">Vous ne devez pas modifier un enregistrement de contrôle d’accès en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="37f55-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="37f55-141">tooedit qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="37f55-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="37f55-142">Effectuer hello suivant les étapes tooedit un ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="37f55-143">tooedit un ACR</span><span class="sxs-lookup"><span data-stu-id="37f55-143">tooedit an ACR</span></span>

1. <span data-ttu-id="37f55-144">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **Configuration** section, **enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="37f55-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="37f55-145">Bonjour **enregistrements de contrôle d’accès** panneau, à partir de la liste tabulaire hello des enregistrements de contrôle d’accès hello, double-cliquez sur hello ACR que vous souhaitez toomodify.</span><span class="sxs-lookup"><span data-stu-id="37f55-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="37f55-146">Bonjour **enregistrements de contrôle d’accès modifier** panneau, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="37f55-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="37f55-147">Approvisionnement hello IQN pour hello ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="37f55-148">Cliquez sur **enregistrer** haut hello hello panneau toosave hello modifié ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="37f55-149">Vous consultez hello message de confirmation suivant :</span><span class="sxs-lookup"><span data-stu-id="37f55-149">You see hello following confirmation message:</span></span>
   
        ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="37f55-151">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-151">Delete an access control record</span></span>

<span data-ttu-id="37f55-152">Vous utilisez hello **Configuration** page Bonjour Azure toodelete portail ACR.</span><span class="sxs-lookup"><span data-stu-id="37f55-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="37f55-153">Vous ne devez pas supprimer un enregistrement de contrôle d’accès en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="37f55-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="37f55-154">toodelete qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="37f55-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="37f55-155">Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="37f55-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="37f55-156">Effectuer hello suivant les étapes toodelete un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="37f55-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="37f55-157">toodelete un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="37f55-157">toodelete an access control record</span></span>

1. <span data-ttu-id="37f55-158">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **Configuration** section, **enregistrements de contrôle d’accès**.</span><span class="sxs-lookup"><span data-stu-id="37f55-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="37f55-159">Bonjour **enregistrements de contrôle d’accès** panneau, à partir de la liste tabulaire hello des enregistrements de contrôle d’accès hello, double-cliquez sur hello ACR que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="37f55-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="37f55-160">Dans Panneau d’enregistrements hello modifier accès contrôle, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="37f55-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![Supprimer des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="37f55-162">Lorsque vous êtes invité à confirmer l’opération, cliquez sur **supprimer** toocontinue avec suppression des hello.</span><span class="sxs-lookup"><span data-stu-id="37f55-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="37f55-163">la liste tabulaire Hello est mise à jour tooreflect hello suppression.</span><span class="sxs-lookup"><span data-stu-id="37f55-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Message d'avertissement](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="37f55-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37f55-165">Next steps</span></span>

* <span data-ttu-id="37f55-166">Découvrez comment [ajouter des volumes et configurer les enregistrements de contrôle d’accès](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="37f55-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

