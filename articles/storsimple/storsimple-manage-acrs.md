---
title: "enregistrements de contrôle d’accès aaaManage dans StorSimple | Documents Microsoft"
description: "Décrit comment le contrôle d’accès toouse enregistre toodetermine (ACR) les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="813cf-103">Utiliser des enregistrements de contrôle d’accès hello StorSimple Manager service toomanage</span><span class="sxs-lookup"><span data-stu-id="813cf-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="813cf-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="813cf-104">Overview</span></span>
<span data-ttu-id="813cf-105">Enregistrements de contrôle d’accès (ACR) permettent de toospecify les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="813cf-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="813cf-106">ACR sont définies les volume spécifique tooa et contenir hello iSCSI (IQN) de noms qualifiés d’hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="813cf-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="813cf-107">Quand un hôte tente de tooconnect tooa volume, les appareils hello vérifie hello QU'ACR associé à ce volume pour le nom IQN de hello et si une correspondance est trouvée, hello est établie.</span><span class="sxs-lookup"><span data-stu-id="813cf-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="813cf-108">la section sur hello des enregistrements de contrôle d’accès Hello **configurer** page affiche tous les enregistrements de contrôle d’accès hello avec hello correspondant iqn des hôtes de hello.</span><span class="sxs-lookup"><span data-stu-id="813cf-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="813cf-109">Ce didacticiel explique hello suivant ACR tâches :</span><span class="sxs-lookup"><span data-stu-id="813cf-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="813cf-110">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-110">Add an access control record</span></span> 
* <span data-ttu-id="813cf-111">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-111">Edit an access control record</span></span> 
* <span data-ttu-id="813cf-112">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="813cf-113">Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="813cf-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="813cf-114">Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="813cf-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="813cf-115">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-115">Add an access control record</span></span>
<span data-ttu-id="813cf-116">Vous utilisez le service StorSimple Manager hello **configurer** page tooadd ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="813cf-117">En général, vous associez un enregistrement de contrôle d’accès à un volume.</span><span class="sxs-lookup"><span data-stu-id="813cf-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="813cf-118">Effectuer hello suivant les étapes tooadd un ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="813cf-119">tooadd un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-119">tooadd an access control record</span></span>
1. <span data-ttu-id="813cf-120">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="813cf-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="813cf-121">Bonjour tabulaire sous **enregistrements de contrôle d’accès**, fournissez un **nom** pour votre ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="813cf-122">Fournissez le nom IQN de hello de votre hôte Windows sous **nom de l’initiateur iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="813cf-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="813cf-123">tooget hello IQN de votre hôte Windows Server, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="813cf-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="813cf-124">Démarrez l’initiateur iSCSI Microsoft hello sur votre hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="813cf-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="813cf-125">Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **Configuration** , sélectionnez et copiez les chaîne hello de hello **nom de l’initiateur** champ.</span><span class="sxs-lookup"><span data-stu-id="813cf-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="813cf-126">Collez cette chaîne Bonjour **nom de l’initiateur iSCSI** champ sur la table d’ACR hello Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="813cf-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="813cf-127">Cliquez sur **enregistrer** hello toosave nouvellement créé ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="813cf-128">Hello tabulaires liste va être mis à jour tooreflect cet ajout.</span><span class="sxs-lookup"><span data-stu-id="813cf-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="813cf-129">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-129">Edit an access control record</span></span>
<span data-ttu-id="813cf-130">Vous utilisez hello **configurer** page Bonjour tooedit de portail classique Azure ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="813cf-131">Vous pouvez modifier uniquement les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="813cf-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="813cf-132">tooedit qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="813cf-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="813cf-133">Effectuer hello suivant les étapes tooedit un ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="813cf-134">tooedit un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-134">tooedit an access control record</span></span>
1. <span data-ttu-id="813cf-135">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="813cf-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="813cf-136">Dans hello tabulaire la liste des enregistrements de contrôle d’accès hello, pointez sur hello ACR que vous souhaitez toomodify.</span><span class="sxs-lookup"><span data-stu-id="813cf-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="813cf-137">Fournir un nouveau nom et/ou le nom IQN hello ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="813cf-138">Cliquez sur **enregistrer** toosave hello modifié ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="813cf-139">Hello tabulaires liste va être mis à jour tooreflect cette modification.</span><span class="sxs-lookup"><span data-stu-id="813cf-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="813cf-140">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-140">Delete an access control record</span></span>
<span data-ttu-id="813cf-141">Vous utilisez hello **configurer** page Bonjour toodelete de portail classique Azure ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="813cf-142">Vous pouvez uniquement supprimer les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="813cf-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="813cf-143">toodelete qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="813cf-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="813cf-144">Effectuer hello suivant les étapes toodelete un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="813cf-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="813cf-145">toodelete un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="813cf-145">toodelete an access control record</span></span>
1. <span data-ttu-id="813cf-146">Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur le nom du service hello, puis cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="813cf-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="813cf-147">Dans hello tabulaire la liste des enregistrements de contrôle d’accès (ACR) hello, pointez sur hello ACR que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="813cf-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="813cf-148">Une icône de suppression (**x**) apparaît dans la colonne de droite extrêmes hello pour hello ACR que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="813cf-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="813cf-149">Cliquez sur hello **x** hello de toodelete icône ACR.</span><span class="sxs-lookup"><span data-stu-id="813cf-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="813cf-150">Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** toocontinue avec suppression des hello.</span><span class="sxs-lookup"><span data-stu-id="813cf-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="813cf-151">la liste tabulaire Hello sera mis à jour tooreflect hello suppression.</span><span class="sxs-lookup"><span data-stu-id="813cf-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="813cf-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="813cf-152">Next steps</span></span>
* <span data-ttu-id="813cf-153">En savoir plus sur la [gestion des volumes StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="813cf-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="813cf-154">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="813cf-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

