---
title: "Réexécution de l’Assistant Installation d’Azure AD Connect | Microsoft Docs"
description: "Explique le fonctionnement de l’Assistant Installation la deuxième fois que vous l’exécutez."
keywords: "L’Assistant Installation d’Azure AD Connect vous permet de configurer les paramètres de maintenance la deuxième fois que vous l’exécutez"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="6aabe-104">Azure AD Connect Sync : exécuter l’Assistant Installation une deuxième fois</span><span class="sxs-lookup"><span data-stu-id="6aabe-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="6aabe-105">La première fois que vous exécutez l’Assistant Installation d’Azure AD Connect, il vous guide dans la procédure de configuration de votre installation.</span><span class="sxs-lookup"><span data-stu-id="6aabe-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="6aabe-106">Si vous réexécutez l’Assistant Installation, il vous propose des options de maintenance.</span><span class="sxs-lookup"><span data-stu-id="6aabe-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="6aabe-107">Vous trouverez l’Assistant Installation dans le menu Démarrer sous le nom **Azure Connect AD**.</span><span class="sxs-lookup"><span data-stu-id="6aabe-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Menu Démarrer](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="6aabe-109">Lorsque vous démarrez l’Assistant Installation, une page s’affiche avec ces options :</span><span class="sxs-lookup"><span data-stu-id="6aabe-109">When you start the installation wizard, you see a page with these options:</span></span>

![Page avec une liste de tâches supplémentaires](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="6aabe-111">Si vous avez installé AD FS avec Azure AD Connect, vous avez davantage d’options.</span><span class="sxs-lookup"><span data-stu-id="6aabe-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="6aabe-112">Les options supplémentaires que vous avez pour AD FS sont documentées dans [Gestion AD FS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="6aabe-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="6aabe-113">Sélectionnez l’une des tâches et cliquez sur **Suivant** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="6aabe-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6aabe-114">Tant que l’Assistant Installation est ouvert, toutes les opérations du moteur de synchronisation sont suspendues.</span><span class="sxs-lookup"><span data-stu-id="6aabe-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="6aabe-115">Prenez soin de fermer l’Assistant Installation dès que vous avez terminé vos modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="6aabe-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="6aabe-116">Afficher la configuration actuelle</span><span class="sxs-lookup"><span data-stu-id="6aabe-116">View current configuration</span></span>
<span data-ttu-id="6aabe-117">Cette option vous donne un aperçu rapide de vos options actuellement configurées.</span><span class="sxs-lookup"><span data-stu-id="6aabe-117">This option gives you a quick view of your currently configured options.</span></span>

![Page avec la liste de toutes les options et leur état](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="6aabe-119">Cliquez sur **Précédent** pour revenir en arrière.</span><span class="sxs-lookup"><span data-stu-id="6aabe-119">Click **Previous** to go back.</span></span> <span data-ttu-id="6aabe-120">Si vous sélectionnez **Quitter**, vous fermez l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="6aabe-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="6aabe-121">Personnaliser les options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="6aabe-121">Customize synchronization options</span></span>
<span data-ttu-id="6aabe-122">Cette option est utilisée pour apporter des modifications à la configuration de la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6aabe-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="6aabe-123">Vous voyez un sous-ensemble d’options provenant du chemin d’installation de la configuration personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6aabe-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="6aabe-124">Et ce, même si vous avez initialement utilisé l’installation rapide.</span><span class="sxs-lookup"><span data-stu-id="6aabe-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="6aabe-125">[Ajouter d’autres annuaires](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="6aabe-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="6aabe-126">Pour supprimer un annuaire, consultez [Supprimer un connecteur](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="6aabe-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="6aabe-127">[Modifier le filtrage par domaine ou unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="6aabe-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="6aabe-128">Supprimer le filtrage de groupe.</span><span class="sxs-lookup"><span data-stu-id="6aabe-128">Remove Group filtering.</span></span>
* <span data-ttu-id="6aabe-129">[Modifier les fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="6aabe-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="6aabe-130">Les autres options provenant de l’installation initiale ne peuvent pas être modifiées et ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="6aabe-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="6aabe-131">Ces options sont :</span><span class="sxs-lookup"><span data-stu-id="6aabe-131">These options are:</span></span>

* <span data-ttu-id="6aabe-132">Modifier l’attribut à utiliser pour userPrincipalName et sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="6aabe-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="6aabe-133">Modifier la méthode de jointure d’objets provenant de différentes forêts.</span><span class="sxs-lookup"><span data-stu-id="6aabe-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="6aabe-134">Activer le filtrage de groupe.</span><span class="sxs-lookup"><span data-stu-id="6aabe-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="6aabe-135">Actualiser le schéma d’annuaire</span><span class="sxs-lookup"><span data-stu-id="6aabe-135">Refresh directory schema</span></span>
<span data-ttu-id="6aabe-136">Cette option est utilisée si vous avez modifié le schéma dans l’une de vos forêts AD DS locales.</span><span class="sxs-lookup"><span data-stu-id="6aabe-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="6aabe-137">Par exemple, vous pouvez avoir installé Exchange ou effectué une mise à niveau vers un schéma Windows Server 2012 avec des objets de périphérique.</span><span class="sxs-lookup"><span data-stu-id="6aabe-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="6aabe-138">Dans ce cas, vous devez demander à Azure AD Connect de relire le schéma AD DS et de mettre à jour son cache.</span><span class="sxs-lookup"><span data-stu-id="6aabe-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="6aabe-139">Cette action régénère également les règles de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="6aabe-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="6aabe-140">Si vous ajoutez le schéma Exchange, par exemple, les règles de synchronisation d’Exchange sont ajoutées à la configuration.</span><span class="sxs-lookup"><span data-stu-id="6aabe-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="6aabe-141">Lorsque vous sélectionnez cette option, tous les annuaires de votre configuration sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="6aabe-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="6aabe-142">Vous pouvez conserver le paramètre par défaut et actualiser toutes les forêts ou désélectionner certaines d’entre elles.</span><span class="sxs-lookup"><span data-stu-id="6aabe-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Page avec la liste de tous les annuaires de l’environnement](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="6aabe-144">Configurer le mode de préproduction</span><span class="sxs-lookup"><span data-stu-id="6aabe-144">Configure staging mode</span></span>
<span data-ttu-id="6aabe-145">Cette option permet d’activer et de désactiver le mode de préproduction sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="6aabe-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="6aabe-146">Vous trouverez plus d’informations sur le mode de préproduction et son utilisation dans [Opérations](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="6aabe-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="6aabe-147">L’option s’affiche si la préproduction est actuellement activée ou désactivée : </span><span class="sxs-lookup"><span data-stu-id="6aabe-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Option qui affiche également l’état actuel du mode de préproduction](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="6aabe-149">Pour modifier l’état, sélectionnez cette option et cochez ou décochez la case.</span><span class="sxs-lookup"><span data-stu-id="6aabe-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Option qui affiche également l’état actuel du mode de préproduction](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="6aabe-151">Modifier la connexion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6aabe-151">Change user sign-in</span></span>
<span data-ttu-id="6aabe-152">Cette option vous permet de passer de la synchronisation de mot de passe à la fédération ou l’inverse.</span><span class="sxs-lookup"><span data-stu-id="6aabe-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="6aabe-153">Vous ne pouvez pas passer à **ne pas configurer**.</span><span class="sxs-lookup"><span data-stu-id="6aabe-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="6aabe-154">Pour plus d’informations sur cette option, consultez [connexion de l’utilisateur](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="6aabe-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aabe-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6aabe-155">Next steps</span></span>
* <span data-ttu-id="6aabe-156">En savoir plus sur le modèle de configuration utilisé par la synchronisation d’Azure AD Connect dans [Comprendre l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="6aabe-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="6aabe-157">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="6aabe-157">**Overview topics**</span></span>

* [<span data-ttu-id="6aabe-158">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="6aabe-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="6aabe-159">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6aabe-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
