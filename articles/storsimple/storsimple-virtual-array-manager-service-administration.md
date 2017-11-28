---
title: "aaaMicrosoft administration de l’unité de stockage Azure StorSimple Manager virtuelle | Documents Microsoft"
description: "Découvrez comment toomanage vos locaux StorSimple Virtual Array à l’aide du service de gestionnaire de périphériques StorSimple hello dans hello portail Azure."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 958244a5-f9f5-455e-b7ef-71a65558872e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 1fabf9ca524b461266346a6cabf49aef772032ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="9467e-103">Utilisez hello le Gestionnaire de périphériques StorSimple service tooadminister votre tableau virtuel StorSimple</span><span class="sxs-lookup"><span data-stu-id="9467e-103">Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array</span></span>
![flux du processus d'installation](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a><span data-ttu-id="9467e-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9467e-105">Overview</span></span>
<span data-ttu-id="9467e-106">Cet article décrit l’interface de service de gestionnaire de périphériques StorSimple hello, y compris la manière dont les tooconnect tooit et hello différentes options disponibles et fournit des liens toohello spécifique des flux de travail qui peuvent être effectuées via cette interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9467e-106">This article describes hello StorSimple Device Manager service interface, including how tooconnect tooit and hello various options available, and provides links toohello specific workflows that can be performed via this UI.</span></span>

<span data-ttu-id="9467e-107">À la fin de cet article, vous serez en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9467e-107">After reading this article, you will know how to:</span></span>

* <span data-ttu-id="9467e-108">Connecter le service de gestionnaire de périphériques StorSimple toohello</span><span class="sxs-lookup"><span data-stu-id="9467e-108">Connect toohello StorSimple Device Manager service</span></span>
* <span data-ttu-id="9467e-109">Accédez hello le Gestionnaire de périphériques StorSimple UI</span><span class="sxs-lookup"><span data-stu-id="9467e-109">Navigate hello StorSimple Device Manager UI</span></span>
* <span data-ttu-id="9467e-110">Administrer votre tableau virtuel StorSimple via hello service du Gestionnaire de périphériques StorSimple</span><span class="sxs-lookup"><span data-stu-id="9467e-110">Administer your StorSimple Virtual Array via hello StorSimple Device Manager service</span></span>

> [!NOTE]
> <span data-ttu-id="9467e-111">options de gestion tooview hello disponibles pour appareil de série hello StorSimple 8000, accédez trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9467e-111">tooview hello management options available for hello StorSimple 8000 series device, go too[Use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>
> 
> 

## <a name="connect-toohello-storsimple-device-manager-service"></a><span data-ttu-id="9467e-112">Connecter le service de gestionnaire de périphériques StorSimple toohello</span><span class="sxs-lookup"><span data-stu-id="9467e-112">Connect toohello StorSimple Device Manager service</span></span>
<span data-ttu-id="9467e-113">Hello service du Gestionnaire de périphériques StorSimple s’exécute dans Microsoft Azure et connecte les réseaux virtuels de toomultiple StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9467e-113">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="9467e-114">Vous utilisez un portail central de Microsoft Azure en cours d’exécution dans un navigateur toomanage ces appareils.</span><span class="sxs-lookup"><span data-stu-id="9467e-114">You use a central Microsoft Azure portal running in a browser toomanage these devices.</span></span> <span data-ttu-id="9467e-115">tooconnect toohello service du Gestionnaire de périphériques StorSimple, procédez comme hello suivant.</span><span class="sxs-lookup"><span data-stu-id="9467e-115">tooconnect toohello StorSimple Device Manager service, do hello following.</span></span>

#### <a name="tooconnect-toohello-service"></a><span data-ttu-id="9467e-116">tooconnect toohello service</span><span class="sxs-lookup"><span data-stu-id="9467e-116">tooconnect toohello service</span></span>
1. <span data-ttu-id="9467e-117">Accédez trop[https://ms.portal.azure.com](https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9467e-117">Go too[https://ms.portal.azure.com](https://ms.portal.azure.com).</span></span>
2. <span data-ttu-id="9467e-118">Vos informations d’identification de compte Microsoft, ouvrez une session sur le portail Microsoft Azure toohello (situé en haut à droite de hello du volet de hello).</span><span class="sxs-lookup"><span data-stu-id="9467e-118">Using your Microsoft account credentials, log on toohello Microsoft Azure portal (located at hello top-right of hello pane).</span></span>
3. <span data-ttu-id="9467e-119">Accédez tooBrowse--> « Filtre » sur les gestionnaires d’appareil StorSimple tooview tous les gestionnaires de votre appareil dans un abonnement donné.</span><span class="sxs-lookup"><span data-stu-id="9467e-119">Navigate tooBrowse --> 'Filter' on StorSimple Device Managers tooview all your device managers in a given subscription.</span></span>

## <a name="use-hello-storsimple-device-manager-service-tooperform-management-tasks"></a><span data-ttu-id="9467e-120">Utiliser des tâches de gestion hello le Gestionnaire de périphériques StorSimple service tooperform</span><span class="sxs-lookup"><span data-stu-id="9467e-120">Use hello StorSimple Device Manager service tooperform management tasks</span></span>
<span data-ttu-id="9467e-121">Hello tableau suivant présente un résumé de toutes les tâches de gestion courantes hello et flux de travail complexes qui peut être effectuées dans le panneau Résumé du service Gestionnaire de périphériques StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="9467e-121">hello following table shows a summary of all hello common management tasks and complex workflows that can be performed within hello StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="9467e-122">Ces tâches sont organisées en fonction de lames hello sur lequel elles sont démarrées.</span><span class="sxs-lookup"><span data-stu-id="9467e-122">These tasks are organized based on hello blades on which they are initiated.</span></span>

<span data-ttu-id="9467e-123">Pour plus d’informations sur chaque flux de travail, cliquez sur hello procédure adéquate décrite dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="9467e-123">For more information about each workflow, click hello appropriate procedure in hello table.</span></span>

#### <a name="storsimple-device-manager-workflows"></a><span data-ttu-id="9467e-124">Flux de travail de StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="9467e-124">StorSimple Device Manager workflows</span></span>
| <span data-ttu-id="9467e-125">Si vous le souhaitez toodo...</span><span class="sxs-lookup"><span data-stu-id="9467e-125">If you want toodo this ...</span></span> | <span data-ttu-id="9467e-126">Suivez cette procédure</span><span class="sxs-lookup"><span data-stu-id="9467e-126">Use this procedure</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9467e-127">Création d’un service</span><span class="sxs-lookup"><span data-stu-id="9467e-127">Create a service</span></span></br><span data-ttu-id="9467e-128">Supprimer un service</span><span class="sxs-lookup"><span data-stu-id="9467e-128">Delete a service</span></span></br><span data-ttu-id="9467e-129">Obtenir la clé d’inscription hello</span><span class="sxs-lookup"><span data-stu-id="9467e-129">Get hello service registration key</span></span></br><span data-ttu-id="9467e-130">Régénérer la clé d’inscription hello</span><span class="sxs-lookup"><span data-stu-id="9467e-130">Regenerate hello service registration key</span></span> |[<span data-ttu-id="9467e-131">Déployer le service du Gestionnaire de périphériques StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="9467e-131">Deploy hello StorSimple Device Manager service</span></span>](storsimple-virtual-array-manage-service.md) |
| <span data-ttu-id="9467e-132">Afficher les journaux activité hello</span><span class="sxs-lookup"><span data-stu-id="9467e-132">View hello activity logs</span></span> |[<span data-ttu-id="9467e-133">Utilisez le résumé du service StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="9467e-133">Use hello StorSimple service summary</span></span>](storsimple-virtual-array-service-summary.md) |
| <span data-ttu-id="9467e-134">Désactiver un Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-134">Deactivate a Virtual Array</span></span></br><span data-ttu-id="9467e-135">Supprimer un Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-135">Delete a Virtual Array</span></span> |[<span data-ttu-id="9467e-136">Désactiver ou supprimer un Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-136">Deactivate or delete a virtual array</span></span>](storsimple-virtual-array-deactivate-and-delete-device.md) |
| <span data-ttu-id="9467e-137">Récupération d’urgence et basculement d’appareil</span><span class="sxs-lookup"><span data-stu-id="9467e-137">Disaster recovery and device failover</span></span></br><span data-ttu-id="9467e-138">Conditions préalables de basculement</span><span class="sxs-lookup"><span data-stu-id="9467e-138">Failover prerequisites</span></span></br><span data-ttu-id="9467e-139">Continuité d’activité et récupération d’urgence (Business Continuity Disaster Recovery - BCDR)</span><span class="sxs-lookup"><span data-stu-id="9467e-139">Business continuity disaster recovery (BCDR)</span></span></br><span data-ttu-id="9467e-140">Erreurs pendant une récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="9467e-140">Errors during disaster recovery</span></span> |[<span data-ttu-id="9467e-141">Basculement d'appareil et  récupération d'urgence pour votre StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-141">Disaster recovery and device failover for your StorSimple Virtual Array</span></span>](storsimple-virtual-array-failover-dr.md) |
| <span data-ttu-id="9467e-142">Sauvegarder des partages et des volumes</span><span class="sxs-lookup"><span data-stu-id="9467e-142">Back up shares and volumes</span></span></br><span data-ttu-id="9467e-143">Exécuter une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="9467e-143">Take a manual backup</span></span></br><span data-ttu-id="9467e-144">Modifier la planification sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="9467e-144">Change hello backup schedule</span></span></br><span data-ttu-id="9467e-145">Afficher les sauvegardes existantes</span><span class="sxs-lookup"><span data-stu-id="9467e-145">View existing backups</span></span> |[<span data-ttu-id="9467e-146">Sauvegarder votre StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-146">Back up your StorSimple Virtual Array</span></span>](storsimple-virtual-array-backup.md) |
| <span data-ttu-id="9467e-147">Cloner des partages à partir d’un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9467e-147">Clone shares from a backup set</span></span></br><span data-ttu-id="9467e-148">Cloner des volumes à partir d’un jeu de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9467e-148">Clone volumes from a backup set</span></span></br><span data-ttu-id="9467e-149">Récupération au niveau élément (serveur de fichiers uniquement)</span><span class="sxs-lookup"><span data-stu-id="9467e-149">Item-level recovery (file server only)</span></span> |[<span data-ttu-id="9467e-150">Cloner à partir d’une sauvegarde de votre instance StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-150">Clone from a backup of your StorSimple Virtual Array</span></span>](storsimple-virtual-array-clone.md) |
| <span data-ttu-id="9467e-151">À propos des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="9467e-151">About  storage accounts</span></span></br><span data-ttu-id="9467e-152">Ajout d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="9467e-152">Add a storage account</span></span></br><span data-ttu-id="9467e-153">Modification d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="9467e-153">Edit a storage account</span></span></br><span data-ttu-id="9467e-154">Suppression d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="9467e-154">Delete a storage account</span></span> |[<span data-ttu-id="9467e-155">Gérer les comptes de stockage pour hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-155">Manage storage accounts for hello StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-storage-accounts.md) |
| <span data-ttu-id="9467e-156">À propos des enregistrements de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="9467e-156">About access control records</span></span></br><span data-ttu-id="9467e-157">Ajouter ou modifier un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="9467e-157">Add or modify an access control record</span></span> </br><span data-ttu-id="9467e-158">Supprimer un enregistrement de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="9467e-158">Delete an access control record</span></span> |[<span data-ttu-id="9467e-159">Gérer les enregistrements de contrôle d’accès pour hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-159">Manage access control records for hello StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-acrs.md) |
| <span data-ttu-id="9467e-160">Affichage des détails d’une tâche</span><span class="sxs-lookup"><span data-stu-id="9467e-160">View job details</span></span> |[<span data-ttu-id="9467e-161">Gérer les tâches StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-161">Manage StorSimple Virtual Array jobs</span></span>](storsimple-virtual-array-manage-jobs.md) |
| <span data-ttu-id="9467e-162">Configurer des paramètres d’alerte</span><span class="sxs-lookup"><span data-stu-id="9467e-162">Configure alert settings</span></span></br><span data-ttu-id="9467e-163">Réception de notifications d’alerte</span><span class="sxs-lookup"><span data-stu-id="9467e-163">Receive alert notifications</span></span></br><span data-ttu-id="9467e-164">Gérer les alertes</span><span class="sxs-lookup"><span data-stu-id="9467e-164">Manage alerts</span></span></br><span data-ttu-id="9467e-165">Consulter les alertes</span><span class="sxs-lookup"><span data-stu-id="9467e-165">Review alerts</span></span> |[<span data-ttu-id="9467e-166">Afficher et gérer les alertes d’hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-166">View and manage alerts for hello StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-alerts.md) |
| <span data-ttu-id="9467e-167">Modifier le mot de passe administrateur hello appareil</span><span class="sxs-lookup"><span data-stu-id="9467e-167">Modify hello device administrator password</span></span> |[<span data-ttu-id="9467e-168">Modifier le mot de passe de l’administrateur d’appareil hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-168">Change hello StorSimple Virtual Array device administrator password</span></span>](storsimple-virtual-array-change-device-admin-password.md) |
| <span data-ttu-id="9467e-169">Installer les mises à jour logicielles</span><span class="sxs-lookup"><span data-stu-id="9467e-169">Install software updates</span></span> |[<span data-ttu-id="9467e-170">Mettre à jour votre Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-170">Update your Virtual Array</span></span>](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> <span data-ttu-id="9467e-171">Vous devez utiliser hello [interface utilisateur web locale](storsimple-ova-web-ui-admin.md) pour hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="9467e-171">You must use hello [local web UI](storsimple-ova-web-ui-admin.md) for hello following tasks:</span></span>
> 
> * [<span data-ttu-id="9467e-172">Récupérer la clé de chiffrement de données de service hello</span><span class="sxs-lookup"><span data-stu-id="9467e-172">Retrieve hello service data encryption key</span></span>](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [<span data-ttu-id="9467e-173">Création d’un package de prise en charge</span><span class="sxs-lookup"><span data-stu-id="9467e-173">Create a support package</span></span>](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [<span data-ttu-id="9467e-174">Arrêt et redémarrage d’un Virtual Array</span><span class="sxs-lookup"><span data-stu-id="9467e-174">Stop and restart a Virtual Array</span></span>](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9467e-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9467e-175">Next steps</span></span>
<span data-ttu-id="9467e-176">Pour plus d’informations sur hello l’interface utilisateur web et comment toouse, accédez trop[utilisez hello tooadminister de l’interface utilisateur web StorSimple votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="9467e-176">For information about hello web UI and how toouse it, go too[Use hello StorSimple web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>
