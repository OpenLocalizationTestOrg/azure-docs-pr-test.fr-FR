---
title: "Gérer les enregistrements de contrôle d’accès dans StorSimple | Microsoft Docs"
description: "Décrit comment utiliser les enregistrements de contrôle d’accès pour déterminer les hôtes qui peuvent se connecter à un volume sur l’appareil StorSimple."
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
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="99351-103">Utiliser le service StorSimple Manager pour gérer les enregistrements de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="99351-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="99351-104">Overview</span></span>
<span data-ttu-id="99351-105">Les enregistrements de contrôle d’accès vous permettent de spécifier les hôtes qui peuvent se connecter à un volume sur l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="99351-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="99351-106">Les enregistrements de contrôle d’accès sont définis pour un volume spécifique et contiennent les noms complets iSCSI (IQN) des ordinateurs hôtes.</span><span class="sxs-lookup"><span data-stu-id="99351-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="99351-107">Lorsqu’un hôte essaie de se connecter à un volume, l’appareil vérifie l’enregistrement de contrôle d’accès associé à ce volume pour le nom complet iSCSI (IQN) et s’il existe une correspondance, la connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="99351-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="99351-108">La section des enregistrements de contrôle d’accès de la page **Configurer** affiche tous les enregistrements de contrôle d’accès avec les noms complets iSCSI (IQN) des hôtes correspondants.</span><span class="sxs-lookup"><span data-stu-id="99351-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="99351-109">Le didacticiel décrit les tâches courantes liées aux enregistrements de contrôle d’accès :</span><span class="sxs-lookup"><span data-stu-id="99351-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="99351-110">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-110">Add an access control record</span></span> 
* <span data-ttu-id="99351-111">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-111">Edit an access control record</span></span> 
* <span data-ttu-id="99351-112">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="99351-113">Lorsque vous attribuez un enregistrement de contrôle d’accès à un volume, veillez à ce que plusieurs hôtes non cluster n’accèdent pas simultanément au volume, sans quoi celui-ci pourrait être endommagé.</span><span class="sxs-lookup"><span data-stu-id="99351-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="99351-114">Lorsque vous supprimez un enregistrement de contrôle d’accès d’un volume, assurez-vous que l’hôte correspondant n’accède pas au volume, car la suppression pourrait entraîner une perturbation des opérations de lecture-écriture.</span><span class="sxs-lookup"><span data-stu-id="99351-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="99351-115">Ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-115">Add an access control record</span></span>
<span data-ttu-id="99351-116">Utilisez la page **Configuration** du service StorSimple Manager pour ajouter des enregistrements de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="99351-117">En général, vous associez un enregistrement de contrôle d’accès à un volume.</span><span class="sxs-lookup"><span data-stu-id="99351-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="99351-118">Effectuez les opérations suivantes pour ajouter un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="99351-119">Pour ajouter un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-119">To add an access control record</span></span>
1. <span data-ttu-id="99351-120">Dans la page d’accueil du service, sélectionnez votre service, double-cliquez sur son nom, puis cliquez sur l’onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="99351-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="99351-121">Dans le tableau sous **Enregistrements de contrôle d’accès**, attribuez un **Nom** à votre enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="99351-122">Sous **Nom d’initiateur iSCSI**, indiquez le nom IQN de votre hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="99351-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="99351-123">Pour obtenir le nom IQN de l’hôte Windows Server, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="99351-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="99351-124">Démarrez l’initiateur Microsoft iSCSI sur l’hôte Windows.</span><span class="sxs-lookup"><span data-stu-id="99351-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="99351-125">Dans la fenêtre **Propriétés de l’initiateur iSCSI**, sous l’onglet **Configuration**, sélectionnez et copiez la chaîne affichée dans le champ **Nom de l’initiateur**.</span><span class="sxs-lookup"><span data-stu-id="99351-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="99351-126">Collez la chaîne du champ **Nom d’initiateur iSCSI** dans la table des enregistrements de contrôle d’accès du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="99351-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="99351-127">Cliquez sur **Enregistrer** pour sauvegarder l’enregistrement de contrôle d’accès nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="99351-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="99351-128">La liste de la table est mise à jour pour refléter les modifications.</span><span class="sxs-lookup"><span data-stu-id="99351-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="99351-129">Modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-129">Edit an access control record</span></span>
<span data-ttu-id="99351-130">Utilisez la page **Configurer** du portail Azure Classic pour modifier les enregistrements de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="99351-131">Vous pouvez modifier uniquement les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="99351-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="99351-132">Pour modifier un enregistrement de contrôle d’accès associé à un volume en cours d’utilisation, vous devez d’abord placer le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="99351-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="99351-133">Effectuez les opérations suivantes pour modifier un enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="99351-134">Pour modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-134">To edit an access control record</span></span>
1. <span data-ttu-id="99351-135">Dans la page d’accueil du service, sélectionnez votre service, double-cliquez sur son nom, puis cliquez sur l’onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="99351-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="99351-136">Dans la liste de la table des enregistrements de contrôle d’accès, pointez sur l’enregistrement que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="99351-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="99351-137">Attribuez un nouveau nom et/ou nom IQN à l’enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="99351-138">Cliquez sur **Enregistrer** pour sauvegarder l’enregistrement de contrôle d’accès modifié.</span><span class="sxs-lookup"><span data-stu-id="99351-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="99351-139">La liste de la table est mise à jour pour refléter la modification.</span><span class="sxs-lookup"><span data-stu-id="99351-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="99351-140">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-140">Delete an access control record</span></span>
<span data-ttu-id="99351-141">Utilisez la page **Configurer** du portail Azure Classic pour supprimer les enregistrements de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="99351-142">Vous pouvez uniquement supprimer les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="99351-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="99351-143">Pour supprimer un enregistrement de contrôle d’accès associé à un volume en cours d’utilisation, vous devez d’abord placer le volume hors connexion.</span><span class="sxs-lookup"><span data-stu-id="99351-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="99351-144">Pour supprimer un enregistrement de contrôle d’accès, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="99351-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="99351-145">Pour supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="99351-145">To delete an access control record</span></span>
1. <span data-ttu-id="99351-146">Dans la page d’accueil du service, sélectionnez votre service, double-cliquez sur son nom, puis cliquez sur l’onglet **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="99351-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="99351-147">Dans la liste de la table des enregistrements de contrôle d’accès, pointez sur l’enregistrement que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="99351-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="99351-148">Une icône de suppression (**x**) apparaît dans la colonne la plus à droite, en regard de l’enregistrement de contrôle d’accès que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="99351-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="99351-149">Cliquez sur l’icône **x** pour supprimer l’enregistrement de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="99351-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="99351-150">Lorsque vous êtes invité à confirmer la suppression, cliquez sur **Oui** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="99351-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="99351-151">La liste de la table est mise à jour pour refléter la suppression.</span><span class="sxs-lookup"><span data-stu-id="99351-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99351-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="99351-152">Next steps</span></span>
* <span data-ttu-id="99351-153">En savoir plus sur la [gestion des volumes StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="99351-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="99351-154">En savoir plus sur [l’utilisation du service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="99351-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

