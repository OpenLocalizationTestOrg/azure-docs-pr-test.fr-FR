---
title: "Azure AD Connect : Étapes suivantes et comment toomanage Azure AD Connect | Documents Microsoft"
description: "Découvrez comment tooextend hello configuration par défaut et les tâches opérationnelles pour Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="6cb55-103">Étapes suivantes et comment toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6cb55-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="6cb55-104">Procédez hello opérationnels dans cette toomeet de Connect de Azure Active Directory (Azure AD) de l’article toocustomize besoins et exigences de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="6cb55-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="6cb55-105">Ajout d’administrateurs de synchronisation supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6cb55-105">Add additional sync admins</span></span>
<span data-ttu-id="6cb55-106">Par défaut, le seul utilisateur hello hello installation et les administrateurs locaux sont moteur de synchronisation en mesure de toomanage hello installé.</span><span class="sxs-lookup"><span data-stu-id="6cb55-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="6cb55-107">Pour tooaccess de personnes supplémentaires toobe en mesure de gérer le moteur de synchronisation hello, recherchez le groupe hello nommé ADSyncAdmins sur le serveur local de hello et ajoutez-les toothis groupe.</span><span class="sxs-lookup"><span data-stu-id="6cb55-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="6cb55-108">Affecter des utilisateurs Active Directory Premium et Enterprise Mobility Suite tooAzure de licences</span><span class="sxs-lookup"><span data-stu-id="6cb55-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="6cb55-109">Maintenant que vos utilisateurs ont été synchronisés toohello cloud, vous devez tooassign les une licence afin qu’ils peuvent commencer avec les applications de cloud telles qu’Office 365.</span><span class="sxs-lookup"><span data-stu-id="6cb55-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="6cb55-110">tooassign une Azure AD Premium ou la licence de la Suite Enterprise Mobility</span><span class="sxs-lookup"><span data-stu-id="6cb55-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="6cb55-111">Se connecter toohello portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6cb55-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="6cb55-112">Sur hello gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6cb55-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="6cb55-113">Sur hello **Active Directory** page, double-cliquez sur le répertoire hello ayant hello utilisateurs tooset des.</span><span class="sxs-lookup"><span data-stu-id="6cb55-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="6cb55-114">En hello haut hello active, sélectionnez **licences**.</span><span class="sxs-lookup"><span data-stu-id="6cb55-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="6cb55-115">Sur hello **licences** page, sélectionnez **Active Directory Premium** ou **Enterprise Mobility Suite**, puis cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="6cb55-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="6cb55-116">Dans la boîte de dialogue hello, sélectionnez les utilisateurs de hello vous souhaitez tooassign licences, puis cliquez sur hello coche icône toosave hello change.</span><span class="sxs-lookup"><span data-stu-id="6cb55-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="6cb55-117">Vérifier la tâche de synchronisation planifiée hello</span><span class="sxs-lookup"><span data-stu-id="6cb55-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="6cb55-118">Utilisez hello toocheck portail Azure hello statut d’une synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6cb55-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="6cb55-119">tâche de synchronisation planifiée hello tooverify</span><span class="sxs-lookup"><span data-stu-id="6cb55-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="6cb55-120">Se connecter toohello portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6cb55-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="6cb55-121">Sur hello gauche, sélectionnez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6cb55-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="6cb55-122">Sur hello **Active Directory** page, double-cliquez sur le répertoire hello ayant hello utilisateurs tooset des.</span><span class="sxs-lookup"><span data-stu-id="6cb55-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="6cb55-123">En hello haut hello active, sélectionnez **intégration d’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="6cb55-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="6cb55-124">Sous **intégration avec Active Directory local**, hello de Remarque dernière heure de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6cb55-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="6cb55-125"><center>![Heure de synchronisation d’annuaires](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="6cb55-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="6cb55-126">Lancement d’une tâche de synchronisation planifiée</span><span class="sxs-lookup"><span data-stu-id="6cb55-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="6cb55-127">Si vous avez besoin d’une tâche de synchronisation de toorun, faire cela en réexécutant via l’Assistant d’Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="6cb55-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="6cb55-128">Vous devez tooprovide vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cb55-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="6cb55-129">Dans l’Assistant de hello, sélectionnez hello **personnaliser les options de synchronisation** de tâches, puis cliquez sur **suivant** toomove via l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="6cb55-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="6cb55-130">À la fin de hello, assurez-vous que hello **démarrer le processus de synchronisation hello dès la fin de la configuration initiale de hello** est activée.</span><span class="sxs-lookup"><span data-stu-id="6cb55-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="6cb55-131"><center>![Démarrage de la synchronisation](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="6cb55-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="6cb55-132">Pour plus d’informations sur la synchronisation de Connect hello Azure AD du planificateur, consultez [Azure Scheduler de connexion AD](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="6cb55-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="6cb55-133">Tâches supplémentaires disponibles dans Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6cb55-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="6cb55-134">Après l’installation initiale d’Azure AD Connect, vous pouvez toujours démarrer hello Assistant à nouveau à partir de hello Azure AD Connect start page ou bureau d’un raccourci.</span><span class="sxs-lookup"><span data-stu-id="6cb55-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="6cb55-135">Vous remarquerez que via l’Assistant de hello redevenir fournit de nouvelles options sous forme de hello des tâches supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6cb55-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="6cb55-136">Hello tableau suivant fournit un résumé de ces tâches et une brève description de chaque tâche.</span><span class="sxs-lookup"><span data-stu-id="6cb55-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Liste des tâches supplémentaires](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="6cb55-138">Tâche supplémentaire</span><span class="sxs-lookup"><span data-stu-id="6cb55-138">Additional task</span></span> | <span data-ttu-id="6cb55-139">Description</span><span class="sxs-lookup"><span data-stu-id="6cb55-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cb55-140">**Scénario de vue hello sélectionné**</span><span class="sxs-lookup"><span data-stu-id="6cb55-140">**View hello selected scenario**</span></span> |<span data-ttu-id="6cb55-141">Afficher votre solution Azure AD Connect actuelle.</span><span class="sxs-lookup"><span data-stu-id="6cb55-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="6cb55-142">Cela inclut les paramètres généraux, les répertoires synchronisés et les paramètres de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6cb55-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="6cb55-143">**Personnalisation des options de synchronisation**</span><span class="sxs-lookup"><span data-stu-id="6cb55-143">**Customize synchronization options**</span></span> |<span data-ttu-id="6cb55-144">Modifier la configuration actuelle du hello comme l’ajout de la configuration de toohello de forêts Active Directory supplémentaire ou l’activation des options de synchronisation tels que l’utilisateur, groupe, appareil ou écriture différée de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6cb55-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="6cb55-145">**Activation du mode intermédiaire**</span><span class="sxs-lookup"><span data-stu-id="6cb55-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="6cb55-146">Informations sur la phase qui ne sont pas synchronisées immédiatement et ne sont pas exporté tooAzure AD ou sur site Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6cb55-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="6cb55-147">Avec cette fonctionnalité, vous pouvez afficher un aperçu des synchronisations hello avant qu’ils surviennent.</span><span class="sxs-lookup"><span data-stu-id="6cb55-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6cb55-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6cb55-148">Next steps</span></span>
<span data-ttu-id="6cb55-149">En savoir plus sur [l’intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6cb55-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
