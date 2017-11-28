---
title: "Assistant Installation de nouveau en cours d’exécution hello Azure AD Connect | Documents Microsoft"
description: "Explique comment l’Assistant installation hello fonctionne hello deuxième fois que vous exécutez."
keywords: "Assistant d’installation Bonjour Azure AD Connect vous permet de configurer des deuxième fois que vous exécutez hello de paramètres de maintenance"
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
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="613c1-104">Synchronisation Azure AD Connect : l’Assistant installation hello en cours d’exécution une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="613c1-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="613c1-105">Hello première fois vous exécutez l’Assistant d’installation Bonjour Azure AD Connect, il vous guide tooconfigure votre installation.</span><span class="sxs-lookup"><span data-stu-id="613c1-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="613c1-106">Si vous exécutez à nouveau l’Assistant installation Bonjour, il offre des options pour la maintenance.</span><span class="sxs-lookup"><span data-stu-id="613c1-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="613c1-107">Vous pouvez trouver l’Assistant installation hello dans le menu Démarrer de hello nommé **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="613c1-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Menu Démarrer](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="613c1-109">Lorsque vous démarrez l’Assistant installation hello, vous voyez une page avec ces options :</span><span class="sxs-lookup"><span data-stu-id="613c1-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Page avec une liste de tâches supplémentaires](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="613c1-111">Si vous avez installé AD FS avec Azure AD Connect, vous avez davantage d’options.</span><span class="sxs-lookup"><span data-stu-id="613c1-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="613c1-112">Hello options supplémentaires que vous avez pour ADFS sont documentées dans [gestion ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="613c1-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="613c1-113">Sélectionnez une des tâches de hello et cliquez sur **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="613c1-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="613c1-114">Alors que l’Assistant installation hello est ouvert, toutes les opérations de moteur de synchronisation hello sont suspendues.</span><span class="sxs-lookup"><span data-stu-id="613c1-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="613c1-115">Assurez-vous que vous fermez l’Assistant installation hello dès que vous avez terminé vos modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="613c1-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="613c1-116">Afficher la configuration actuelle</span><span class="sxs-lookup"><span data-stu-id="613c1-116">View current configuration</span></span>
<span data-ttu-id="613c1-117">Cette option vous donne un aperçu rapide de vos options actuellement configurées.</span><span class="sxs-lookup"><span data-stu-id="613c1-117">This option gives you a quick view of your currently configured options.</span></span>

![Page avec la liste de toutes les options et leur état](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="613c1-119">Cliquez sur **précédent** toogo précédent.</span><span class="sxs-lookup"><span data-stu-id="613c1-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="613c1-120">Si vous sélectionnez **Exit**, vous fermez l’Assistant installation hello.</span><span class="sxs-lookup"><span data-stu-id="613c1-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="613c1-121">Personnaliser les options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="613c1-121">Customize synchronization options</span></span>
<span data-ttu-id="613c1-122">Cette option est la configuration de la synchronisation modifications toohello toomake utilisé.</span><span class="sxs-lookup"><span data-stu-id="613c1-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="613c1-123">Vous consultez un sous-ensemble des options à partir du chemin d’installation de configuration personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="613c1-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="613c1-124">Et ce, même si vous avez initialement utilisé l’installation rapide.</span><span class="sxs-lookup"><span data-stu-id="613c1-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="613c1-125">[Ajouter d’autres annuaires](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="613c1-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="613c1-126">Pour supprimer un annuaire, consultez [Supprimer un connecteur](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="613c1-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="613c1-127">[Modifier le filtrage par domaine ou unité d’organisation](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="613c1-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="613c1-128">Supprimer le filtrage de groupe.</span><span class="sxs-lookup"><span data-stu-id="613c1-128">Remove Group filtering.</span></span>
* <span data-ttu-id="613c1-129">[Modifier les fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="613c1-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="613c1-130">Bonjour autres options de l’installation initiale de hello ne peut pas être modifiées et ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="613c1-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="613c1-131">Ces options sont :</span><span class="sxs-lookup"><span data-stu-id="613c1-131">These options are:</span></span>

* <span data-ttu-id="613c1-132">Modifiez toouse d’attribut hello pour userPrincipalName et sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="613c1-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="613c1-133">Modifier hello jointure de méthode pour les objets à partir de l’autre forêt.</span><span class="sxs-lookup"><span data-stu-id="613c1-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="613c1-134">Activer le filtrage de groupe.</span><span class="sxs-lookup"><span data-stu-id="613c1-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="613c1-135">Actualiser le schéma d’annuaire</span><span class="sxs-lookup"><span data-stu-id="613c1-135">Refresh directory schema</span></span>
<span data-ttu-id="613c1-136">Cette option est utilisée si vous avez modifié le schéma de hello dans un de vos locaux sur les forêts AD DS.</span><span class="sxs-lookup"><span data-stu-id="613c1-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="613c1-137">Par exemple, vous avez peut-être installé Exchange ou mis à niveau le schéma tooa Windows Server 2012 avec les objets périphériques.</span><span class="sxs-lookup"><span data-stu-id="613c1-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="613c1-138">Dans ce cas, vous avez besoin tooinstruct Azure AD Connect tooread hello schéma à partir des services AD DS et mettre à jour son cache.</span><span class="sxs-lookup"><span data-stu-id="613c1-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="613c1-139">Cette opération régénère également les règles de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="613c1-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="613c1-140">Si vous ajoutez un schéma d’Exchange hello, par exemple, les règles de synchronisation hello pour Exchange sont ajoutés toohello configuration.</span><span class="sxs-lookup"><span data-stu-id="613c1-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="613c1-141">Lorsque vous sélectionnez cette option, tous les répertoires hello dans votre configuration sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="613c1-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="613c1-142">Vous pouvez conserver le paramètre par défaut de hello et actualiser toutes les forêts ou désélectionnez certaines d'entre elles.</span><span class="sxs-lookup"><span data-stu-id="613c1-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Page avec une liste de tous les répertoires dans un environnement de hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="613c1-144">Configurer le mode de préproduction</span><span class="sxs-lookup"><span data-stu-id="613c1-144">Configure staging mode</span></span>
<span data-ttu-id="613c1-145">Cette option vous permet de tooenable et désactiver le mode de mise en lots sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="613c1-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="613c1-146">Vous trouverez plus d’informations sur le mode de préproduction et son utilisation dans [Opérations](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="613c1-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="613c1-147">option de Hello indique si la mise en lots est actuellement activé ou désactivé :</span><span class="sxs-lookup"><span data-stu-id="613c1-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Option qui s’affiche également état actuel de hello du mode de mise en lots](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="613c1-149">toochange hello état, sélectionnez cette option et la case à cocher Sélectionner ou désélectionner hello.</span><span class="sxs-lookup"><span data-stu-id="613c1-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Option qui s’affiche également état actuel de hello du mode de mise en lots](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="613c1-151">Modifier la connexion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="613c1-151">Change user sign-in</span></span>
<span data-ttu-id="613c1-152">Cette option vous permet de toochange de toofederation de synchronisation de mot de passe ou hello inverse.</span><span class="sxs-lookup"><span data-stu-id="613c1-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="613c1-153">Vous ne pouvez pas modifier trop**ne configurez pas**.</span><span class="sxs-lookup"><span data-stu-id="613c1-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="613c1-154">Pour plus d’informations sur cette option, consultez [connexion de l’utilisateur](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="613c1-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="613c1-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="613c1-155">Next steps</span></span>
* <span data-ttu-id="613c1-156">En savoir plus sur le modèle de configuration hello utilisé par la synchronisation Azure AD Connect dans [approvisionnement déclaratif compréhension](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="613c1-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="613c1-157">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="613c1-157">**Overview topics**</span></span>

* [<span data-ttu-id="613c1-158">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="613c1-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="613c1-159">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="613c1-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
