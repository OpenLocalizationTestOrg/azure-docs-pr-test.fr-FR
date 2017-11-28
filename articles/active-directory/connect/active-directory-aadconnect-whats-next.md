---
title: "Azure AD Connect : Étapes suivantes et gestion Azure AD Connect | Microsoft Docs"
description: "Apprenez à étendre la configuration par défaut et les tâches opérationnelles pour Azure AD Connect."
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
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="05d64-103">Étapes suivantes et gestion d’Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="05d64-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="05d64-104">Utilisez les procédures opérationnelles dans cet article pour personnaliser Azure Active Directory (Azure AD) Connect pour l’adapter aux besoins et aux spécifications de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="05d64-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="05d64-105">Ajout d’administrateurs de synchronisation supplémentaires</span><span class="sxs-lookup"><span data-stu-id="05d64-105">Add additional sync admins</span></span>
<span data-ttu-id="05d64-106">Par défaut, seul l’utilisateur qui a effectué l’installation et les administrateurs locaux est en mesure de gérer le moteur de synchronisation installé.</span><span class="sxs-lookup"><span data-stu-id="05d64-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="05d64-107">Pour que d’autres personnes puissent accéder au moteur de synchronisation et en assurer la gestion, localisez le groupe nommé ADSyncAdmins sur le serveur local et ajoutez ces personnes à ce groupe.</span><span class="sxs-lookup"><span data-stu-id="05d64-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="05d64-108">Attribution des licences aux utilisateurs Azure AD Premium et Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="05d64-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="05d64-109">Maintenant que vos utilisateurs ont été synchronisés dans le cloud, vous devez leur attribuer une licence afin qu’ils puissent commencer à utiliser les applications cloud telles qu’Office 365.</span><span class="sxs-lookup"><span data-stu-id="05d64-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="05d64-110">Pour l’attribution d’une licence Azure AD Premium ou Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="05d64-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="05d64-111">Connectez-vous au portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="05d64-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="05d64-112">Sélectionnez **Active Directory**à gauche.</span><span class="sxs-lookup"><span data-stu-id="05d64-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="05d64-113">Sur la page **Active Directory**, double-cliquez sur le répertoire qui contient les utilisateurs que vous souhaitez configurer.</span><span class="sxs-lookup"><span data-stu-id="05d64-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="05d64-114">En haut de la page du répertoire, sélectionnez **Licences**.</span><span class="sxs-lookup"><span data-stu-id="05d64-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="05d64-115">Sur la page **Licences**, sélectionnez **Active Directory Premium** ou **Enterprise Mobility Suite**, puis cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="05d64-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="05d64-116">Dans la boîte de dialogue, sélectionnez les utilisateurs auxquels vous souhaitez attribuer des licences, puis cliquez sur l'icône de coche pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="05d64-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="05d64-117">Vérification de la tâche de synchronisation planifiée</span><span class="sxs-lookup"><span data-stu-id="05d64-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="05d64-118">Utilisez le portail Azure pour vérifier l’état d’une synchronisation.</span><span class="sxs-lookup"><span data-stu-id="05d64-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="05d64-119">Pour la vérification de la tâche de synchronisation planifiée</span><span class="sxs-lookup"><span data-stu-id="05d64-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="05d64-120">Connectez-vous au portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="05d64-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="05d64-121">Sélectionnez **Active Directory**à gauche.</span><span class="sxs-lookup"><span data-stu-id="05d64-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="05d64-122">Sur la page **Active Directory**, double-cliquez sur le répertoire qui contient les utilisateurs que vous souhaitez configurer.</span><span class="sxs-lookup"><span data-stu-id="05d64-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="05d64-123">En haut de la page du répertoire, sélectionnez **Intégration du répertoire**.</span><span class="sxs-lookup"><span data-stu-id="05d64-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="05d64-124">Sous **l’intégration à un Active Directory local**, notez l’heure de la dernière synchronisation.</span><span class="sxs-lookup"><span data-stu-id="05d64-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="05d64-125"><center>![Heure de synchronisation d’annuaires](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="05d64-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="05d64-126">Lancement d’une tâche de synchronisation planifiée</span><span class="sxs-lookup"><span data-stu-id="05d64-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="05d64-127">Si vous devez exécuter une tâche de synchronisation, vous pouvez le faire en l’exécutant une nouvelle fois depuis l’Assistant Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="05d64-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="05d64-128">Vous devez fournir vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d64-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="05d64-129">Dans l’Assistant, sélectionnez la tâche **Personnalisation des options de synchronisation** et cliquez sur **Suivant** pour terminer l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="05d64-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="05d64-130">À la fin, vérifiez que la case **Démarrez le processus de synchronisation dès que la configuration initiale est terminée** est cochée.</span><span class="sxs-lookup"><span data-stu-id="05d64-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="05d64-131"><center>![Démarrage de la synchronisation](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="05d64-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="05d64-132">Pour plus d’informations sur le planificateur de synchronisation Azure AD Connect, consultez [Planificateur Azure AD Connect](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="05d64-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="05d64-133">Tâches supplémentaires disponibles dans Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="05d64-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="05d64-134">Après l’installation initiale d’Azure AD Connect, vous pouvez toujours redémarrer l’Assistant depuis la page de démarrage ou le raccourci du bureau Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="05d64-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="05d64-135">Vous remarquerez qu’en passant à nouveau par l’Assistant de nouvelles options apparaissent sous forme de tâches supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="05d64-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="05d64-136">Le tableau suivant fournit un résumé de ces tâches et une brève description de chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="05d64-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![Liste des tâches supplémentaires](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="05d64-138">Tâche supplémentaire</span><span class="sxs-lookup"><span data-stu-id="05d64-138">Additional task</span></span> | <span data-ttu-id="05d64-139">Description</span><span class="sxs-lookup"><span data-stu-id="05d64-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05d64-140">**Afficher le scénario sélectionné**</span><span class="sxs-lookup"><span data-stu-id="05d64-140">**View the selected scenario**</span></span> |<span data-ttu-id="05d64-141">Afficher votre solution Azure AD Connect actuelle.</span><span class="sxs-lookup"><span data-stu-id="05d64-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="05d64-142">Cela inclut les paramètres généraux, les répertoires synchronisés et les paramètres de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="05d64-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="05d64-143">**Personnalisation des options de synchronisation**</span><span class="sxs-lookup"><span data-stu-id="05d64-143">**Customize synchronization options**</span></span> |<span data-ttu-id="05d64-144">Modifier la configuration actuelle, notamment par l’ajout de forêts Active Directory supplémentaires à la configuration ou l’activation d’options de synchronisation telles que l’utilisateur, le groupe, l’appareil ou le mot de passe en écriture différée.</span><span class="sxs-lookup"><span data-stu-id="05d64-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="05d64-145">**Activation du mode intermédiaire**</span><span class="sxs-lookup"><span data-stu-id="05d64-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="05d64-146">Réalisez un déploiement intermédiaire des informations qui ne sont pas immédiatement synchronisées et ne sont pas exportées vers Azure AD ou l’Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="05d64-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="05d64-147">Cette fonctionnalité vous permet d’afficher un aperçu des synchronisations avant qu’elles ne s’effectuent.</span><span class="sxs-lookup"><span data-stu-id="05d64-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="05d64-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05d64-148">Next steps</span></span>
<span data-ttu-id="05d64-149">En savoir plus sur [l’intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="05d64-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
