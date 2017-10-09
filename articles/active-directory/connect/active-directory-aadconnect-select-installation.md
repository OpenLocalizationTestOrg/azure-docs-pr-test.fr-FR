---
title: "Azure AD Connect : Sélectionner le type d’installation | Microsoft Docs"
description: "Cette rubrique vous explique comment comment tooselect hello type d’installation toouse pour Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="b0bb8-103">Sélectionnez le toouse de type d’installation pour Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="b0bb8-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="b0bb8-104">Azure AD Connect a deux types d’installation pour une nouvelle installation : Express et personnalisée.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="b0bb8-105">Cette rubrique vous aide à toodecide qui option toouse pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="b0bb8-106">Express</span><span class="sxs-lookup"><span data-stu-id="b0bb8-106">Express</span></span>
<span data-ttu-id="b0bb8-107">Express est l’option la plus courante hello et est utilisé par environ 90 % de toutes les nouvelles installations.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="b0bb8-108">Il a été conçu tooprovide une configuration qui fonctionne pour les scénarios de client les plus courants hello.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="b0bb8-109">Elle suppose que :</span><span class="sxs-lookup"><span data-stu-id="b0bb8-109">It assumes:</span></span>

- <span data-ttu-id="b0bb8-110">Vous avez une seule forêt Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="b0bb8-111">Vous avez un compte administrateur d’entreprise que vous pouvez utiliser pour l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="b0bb8-112">Vous avez moins de 100 000 objets dans votre annuaire Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="b0bb8-113">Vous obtenez :</span><span class="sxs-lookup"><span data-stu-id="b0bb8-113">You get:</span></span>

- <span data-ttu-id="b0bb8-114">[Synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) de tooAzure local AD pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="b0bb8-115">Une configuration qui synchronise [les utilisateurs, les groupes, les contacts et les ordinateurs Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="b0bb8-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="b0bb8-116">La synchronisation de tous les objets éligibles dans tous les domaines et toutes les unités d’organisation.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="b0bb8-117">[Mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) est activé toomake que vous utilisez toujours hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="b0bb8-118">Cas où vous pouvez toujours utiliser Express :</span><span class="sxs-lookup"><span data-stu-id="b0bb8-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="b0bb8-119">Si vous ne souhaitez pas toosynchronize tous d’unités d’organisation, vous pouvez toujours utiliser Express et sur la dernière page de hello, désélectionnez **démarrer le processus de synchronisation hello...** *.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="b0bb8-120">Ensuite, réexécutez l’Assistant installation de hello et modifier les unités d’organisation hello dans [les options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) et activer la synchronisation planifiée.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="b0bb8-121">Vous souhaitez tooenable l’une des fonctionnalités hello dans Azure AD Premium, telles que l’écriture différée de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="b0bb8-122">Effectuez tout d’abord tooget express hello initiale l’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="b0bb8-123">Ensuite, réexécutez l’Assistant installation de hello et modifier hello [les options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="b0bb8-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="b0bb8-124">Personnalisée</span><span class="sxs-lookup"><span data-stu-id="b0bb8-124">Custom</span></span>
<span data-ttu-id="b0bb8-125">chemin d’accès personnalisé de Hello permet de nombreuses autres options que la version express.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="b0bb8-126">Elle doit être utilisée dans tous les cas où la configuration de hello décrite dans la section précédente pour express n’est pas représentative de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="b0bb8-127">Utilisez-la quand :</span><span class="sxs-lookup"><span data-stu-id="b0bb8-127">Use when:</span></span>

- <span data-ttu-id="b0bb8-128">Vous n’avez pas de compte d’administrateur accès tooan entreprise dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="b0bb8-129">Vous avez plusieurs forêts ou que vous envisagez de toosynchronize plusieurs forêts dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="b0bb8-130">Vous avez des domaines dans votre forêt n’est pas accessible à partir du serveur de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="b0bb8-131">Vous envisagez de fédération de toouse ou de l’authentification directe pour la connexion d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="b0bb8-132">Vous disposez de plus de 100 000 objets et que vous devez toouse une complète de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="b0bb8-133">Vous envisagez de toouse basée sur le groupe de filtrage et non seulement le domaine ou le filtrage basé sur une unité d’organisation.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="b0bb8-134">Mise à niveau à partir de DirSync</span><span class="sxs-lookup"><span data-stu-id="b0bb8-134">Upgrade from DirSync</span></span>
<span data-ttu-id="b0bb8-135">Si vous utilisez actuellement la synchronisation d’annuaire, puis suivez les étapes de hello dans [mise à niveau à partir de la synchronisation d’annuaire](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade votre configuration existante.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="b0bb8-136">Il existe deux scénarios différents de mise à niveau :</span><span class="sxs-lookup"><span data-stu-id="b0bb8-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="b0bb8-137">Connecter tooinstall de mise à niveau sur place sur hello même serveur.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="b0bb8-138">Parallèle déploiement tooinstall se connecter sur un nouveau serveur alors que le serveur de synchronisation d’annuaire hello existant est toujours opérationnel.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="b0bb8-139">Mise à niveau à partir d’Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="b0bb8-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="b0bb8-140">Si vous utilisez Azure AD Sync, vous pouvez suivre hello [mêmes étapes](active-directory-aadconnect-upgrade-previous-version.md) comme lorsque vous mettez à niveau à partir d’une connexion version tooa plus récente.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="b0bb8-141">Il existe deux scénarios différents de mise à niveau :</span><span class="sxs-lookup"><span data-stu-id="b0bb8-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="b0bb8-142">Connecter tooinstall de mise à niveau sur place sur hello même serveur.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="b0bb8-143">Migration de basculement tooinstall se connecter sur un nouveau serveur lors de serveur de synchronisation Azure AD existant hello est toujours opérationnel.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="b0bb8-144">Migrer depuis FIM2010 ou MIM2016</span><span class="sxs-lookup"><span data-stu-id="b0bb8-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="b0bb8-145">Si vous utilisez actuellement Microsoft Forefront Identity Manager 2010 ou Microsoft Identity Manager 2016 avec hello connecteur Azure AD, votre seule option est une migration.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="b0bb8-146">Suivez les étapes de hello décrites dans [basculement-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="b0bb8-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="b0bb8-147">Dans les étapes de hello, remplacez toute mention d’Azure AD Sync avec FIM 2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0bb8-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0bb8-148">Next steps</span></span>
<span data-ttu-id="b0bb8-149">En fonction de l’option de hello sélectionnée toouse, utilisez le tableau de hello de toofind gauche du contenu toohello votre article avec hello les étapes détaillées.</span><span class="sxs-lookup"><span data-stu-id="b0bb8-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
