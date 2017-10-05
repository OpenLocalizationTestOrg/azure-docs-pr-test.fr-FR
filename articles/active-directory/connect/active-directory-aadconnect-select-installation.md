---
title: "Azure AD Connect : Sélectionner le type d’installation | Microsoft Docs"
description: "Cette rubrique vous montre comment sélectionner le type d’installation à utiliser pour Azure AD Connect"
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
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="d6228-103">Sélectionner le type d’installation à utiliser pour Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d6228-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="d6228-104">Azure AD Connect a deux types d’installation pour une nouvelle installation : Express et personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d6228-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="d6228-105">Cette rubrique vous aide à choisir l’option à utiliser lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="d6228-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="d6228-106">Express</span><span class="sxs-lookup"><span data-stu-id="d6228-106">Express</span></span>
<span data-ttu-id="d6228-107">Express est l’option la plus courante et est utilisée dans environ 90 % des nouvelles installations.</span><span class="sxs-lookup"><span data-stu-id="d6228-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="d6228-108">Elle a été conçue pour fournir une configuration qui fonctionne dans la plupart des scénarios des clients.</span><span class="sxs-lookup"><span data-stu-id="d6228-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="d6228-109">Elle suppose que :</span><span class="sxs-lookup"><span data-stu-id="d6228-109">It assumes:</span></span>

- <span data-ttu-id="d6228-110">Vous avez une seule forêt Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="d6228-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="d6228-111">Vous avez un compte administrateur d’entreprise que vous pouvez utiliser pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="d6228-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="d6228-112">Vous avez moins de 100 000 objets dans votre annuaire Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="d6228-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="d6228-113">Vous obtenez :</span><span class="sxs-lookup"><span data-stu-id="d6228-113">You get:</span></span>

- <span data-ttu-id="d6228-114">La [synchronisation du mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) du système local vers Azure AD pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d6228-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="d6228-115">Une configuration qui synchronise [les utilisateurs, les groupes, les contacts et les ordinateurs Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d6228-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="d6228-116">La synchronisation de tous les objets éligibles dans tous les domaines et toutes les unités d’organisation.</span><span class="sxs-lookup"><span data-stu-id="d6228-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="d6228-117">La [mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) est activée pour garantir que vous utilisez toujours la dernière version disponible.</span><span class="sxs-lookup"><span data-stu-id="d6228-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="d6228-118">Cas où vous pouvez toujours utiliser Express :</span><span class="sxs-lookup"><span data-stu-id="d6228-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="d6228-119">Si vous ne voulez pas synchroniser toutes les unités d’organisation, vous pouvez néanmoins utiliser Express et, dans la dernière page, désélectionner **Démarrer le processus de synchronisation...***.</span><span class="sxs-lookup"><span data-stu-id="d6228-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="d6228-120">Réexécutez ensuite l’Assistant Installation, changez les unités d’organisation dans les [options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) et activez la synchronisation planifiée.</span><span class="sxs-lookup"><span data-stu-id="d6228-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="d6228-121">Vous voulez activer une des fonctionnalités dans Azure AD Premium, comme la réécriture du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d6228-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="d6228-122">Choisissez d’abord Express pour effectuer l’installation initiale.</span><span class="sxs-lookup"><span data-stu-id="d6228-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="d6228-123">Réexécutez ensuite l’Assistant Installation et changez les [options de configuration](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="d6228-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="d6228-124">Personnalisée</span><span class="sxs-lookup"><span data-stu-id="d6228-124">Custom</span></span>
<span data-ttu-id="d6228-125">L’installation personnalisée offre beaucoup plus d’options que l’installation Express.</span><span class="sxs-lookup"><span data-stu-id="d6228-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="d6228-126">Elle doit être utilisée dans tous les cas où la configuration décrite dans la section précédente pour Express n’est pas représentative de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d6228-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="d6228-127">Utilisez-la quand :</span><span class="sxs-lookup"><span data-stu-id="d6228-127">Use when:</span></span>

- <span data-ttu-id="d6228-128">Vous n’avez pas accès à un compte administrateur d’entreprise dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6228-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="d6228-129">Vous avez plusieurs forêts ou vous prévoyez de synchroniser plusieurs forêts à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="d6228-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="d6228-130">Vous avez des domaines dans votre forêt qui ne sont pas accessibles à partir du serveur Connect.</span><span class="sxs-lookup"><span data-stu-id="d6228-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="d6228-131">Vous prévoyez d’utiliser la fédération ou l’authentification directe pour la connexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d6228-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="d6228-132">Vous avez plus de 100 000 objets et vous devez utiliser un serveur SQL Server complet.</span><span class="sxs-lookup"><span data-stu-id="d6228-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="d6228-133">Vous prévoyez d’utiliser le filtrage par groupe, et pas seulement le filtrage par domaine ou par unité d’organisation.</span><span class="sxs-lookup"><span data-stu-id="d6228-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="d6228-134">Effectuer une mise à niveau à partir de DirSync</span><span class="sxs-lookup"><span data-stu-id="d6228-134">Upgrade from DirSync</span></span>
<span data-ttu-id="d6228-135">Si vous utilisez actuellement DirSync, suivez les étapes de [Mise à niveau à partir de DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) pour mettre à niveau votre configuration existante.</span><span class="sxs-lookup"><span data-stu-id="d6228-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="d6228-136">Il existe deux scénarios différents de mise à niveau :</span><span class="sxs-lookup"><span data-stu-id="d6228-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="d6228-137">Mise à niveau sur place pour installer Connect sur le même serveur.</span><span class="sxs-lookup"><span data-stu-id="d6228-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="d6228-138">Déploiement en parallèle pour installer Connect sur un nouveau serveur, alors que le serveur DirSync existant est toujours opérationnel.</span><span class="sxs-lookup"><span data-stu-id="d6228-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="d6228-139">Mise à niveau à partir d’Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="d6228-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="d6228-140">Si vous utilisez actuellement Azure AD Sync, vous pouvez suivre les [mêmes étapes](active-directory-aadconnect-upgrade-previous-version.md) que celle de la mise à niveau d’une version de Connect vers une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="d6228-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="d6228-141">Il existe deux scénarios différents de mise à niveau :</span><span class="sxs-lookup"><span data-stu-id="d6228-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="d6228-142">Mise à niveau sur place pour installer Connect sur le même serveur.</span><span class="sxs-lookup"><span data-stu-id="d6228-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="d6228-143">Migration via une instance distincte pour installer Connect sur un nouveau serveur, alors que le serveur Azure AD Sync existant est toujours opérationnel.</span><span class="sxs-lookup"><span data-stu-id="d6228-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="d6228-144">Migrer depuis FIM2010 ou MIM2016</span><span class="sxs-lookup"><span data-stu-id="d6228-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="d6228-145">Si vous utilisez actuellement Forefront Identity Manager 2010 ou Microsoft Identity Manager 2016 avec le connecteur Azure AD, votre seule option est une migration.</span><span class="sxs-lookup"><span data-stu-id="d6228-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="d6228-146">Suivez les étapes décrites dans [Migration via une instance distincte](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="d6228-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="d6228-147">Dans les étapes, remplacez les mentions d’Azure AD Sync par FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="d6228-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6228-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6228-148">Next steps</span></span>
<span data-ttu-id="d6228-149">Selon l’option que vous avez choisie, utilisez la table des matières à gauche pour trouver votre article avec les étapes détaillées.</span><span class="sxs-lookup"><span data-stu-id="d6228-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
