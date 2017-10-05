---
title: "Publier des applications pour des utilisateurs individuels dans une collection Azure RemoteApp (version préliminaire) | Microsoft Docs"
description: "Apprenez à publier des applications dans Azure RemoteApp à l’attention d’utilisateurs spécifiques plutôt qu’à des groupes."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="1cf2c-103">Publier des applications pour des utilisateurs individuels dans une collection Azure RemoteApp (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="1cf2c-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1cf2c-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1cf2c-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="1cf2c-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1cf2c-106">Cet article explique comment publier des applications pour des utilisateurs individuels dans une collection Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="1cf2c-107">Cette nouvelle fonctionnalité d’Azure RemoteApp, actuellement disponible en « version préliminaire privée », est réservée uniquement aux utilisateurs précoces à des fins d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="1cf2c-108">À l’origine, Azure RemoteApp n’offrait qu’un seul moyen de « publier » des applications : l’administrateur devait publier les applications à partir de l’image pour les rendre visibles à tous les utilisateurs de la collection.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="1cf2c-109">Dans un souci de réduction des coûts de gestion, il n’est pas rare que les administrateurs intègrent de nombreuses applications dans une même image et déploient une seule collection.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="1cf2c-110">Mais toutes les applications ne sont pas toujours utiles à l’ensemble des utilisateurs ; aussi, les administrateurs préféreront publier des applications à l’attention de certains utilisateurs spécifiques afin de ne pas les encombrer d’applications inutiles.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="1cf2c-111">Azure RemoteApp offre désormais cette possibilité dans le cadre d’une fonctionnalité préliminaire limitée.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="1cf2c-112">Voici un bref résumé de cette nouvelle fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="1cf2c-113">Une collection peut être paramétrée dans deux modes différents :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="1cf2c-114">le « mode collection » d’origine, grâce auquel tous les utilisateurs d’une collection peuvent visualiser l’ensemble des applications publiées.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="1cf2c-115">Il s’agit du mode par défaut ;</span><span class="sxs-lookup"><span data-stu-id="1cf2c-115">This is the default mode.</span></span>
   * <span data-ttu-id="1cf2c-116">le nouveau « mode application », dans lequel les utilisateurs voient uniquement les applications qui leur ont été explicitement affectées</span><span class="sxs-lookup"><span data-stu-id="1cf2c-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="1cf2c-117">Pour le moment, le mode application ne peut être activé qu’à l’aide des applets de commande PowerShell pour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="1cf2c-118">En mode application, l’affectation des utilisateurs dans la collection ne peut pas être gérée via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="1cf2c-119">Elle ne peut être gérée qu’au moyen des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="1cf2c-120">Les utilisateurs ne voient que les applications qui ont été directement publiées à leur attention.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="1cf2c-121">Un utilisateur a toutefois la possibilité de lancer les autres applications disponibles sur l’image en y accédant directement depuis le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="1cf2c-122">Cette fonctionnalité ne garantit pas un verrouillage sécurisé des applications ; elle ne fait que restreindre la visibilité dans le flux d’applications.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="1cf2c-123">Si vous souhaitez isoler les utilisateurs de certaines applications, vous devez utiliser des collections distinctes.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="1cf2c-124">Comment obtenir les applets de commande PowerShell pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1cf2c-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="1cf2c-125">Pour tester la nouvelle fonctionnalité en version préliminaire, vous devez utiliser les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="1cf2c-126">Vous ne pouvez pas pour le moment utiliser le portail de gestion Azure pour activer le nouveau mode de publication d’applications.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="1cf2c-127">Assurez-vous tout d’abord que vous disposez bien du [module Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="1cf2c-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="1cf2c-128">Lancez ensuite la console PowerShell en mode administrateur, puis exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="1cf2c-129">Vous êtes invité à saisir vos nom d’utilisateur et mot de passe Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="1cf2c-130">Une fois connecté, vous pouvez exécuter des applets de commande Azure RemoteApp sur vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="1cf2c-131">Comment vérifier le mode d’une collection</span><span class="sxs-lookup"><span data-stu-id="1cf2c-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="1cf2c-132">Exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Vérifier le mode de collecte](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="1cf2c-134">La propriété AclLevel peut avoir les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="1cf2c-135">Collection : mode de publication d’origine.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="1cf2c-136">Tous les utilisateurs peuvent visualiser l’ensemble des applications publiées.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-136">All users see all published apps.</span></span>
* <span data-ttu-id="1cf2c-137">Application : nouveau mode de publication.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-137">Application: the new publishing mode.</span></span> <span data-ttu-id="1cf2c-138">Les utilisateurs voient uniquement les applications qui ont été directement publiées à leur attention.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="1cf2c-139">Comment passer en mode de publication d’applications</span><span class="sxs-lookup"><span data-stu-id="1cf2c-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="1cf2c-140">Exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="1cf2c-141">L’état de publication des applications est conservé : tous les utilisateurs voient l’ensemble des applications initialement publiées.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="1cf2c-142">Comment répertorier les utilisateurs autorisés à visualiser une application spécifique</span><span class="sxs-lookup"><span data-stu-id="1cf2c-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="1cf2c-143">Exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="1cf2c-144">Cette commande permet de répertorier tous les utilisateurs pouvant visualiser l’application.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="1cf2c-145">Remarque : vous pouvez voir les alias de l’application (appelés « app alias » dans la syntaxe ci-dessus) en exécutant l’applet de commande Get-AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="1cf2c-146">Comment affecter une application à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1cf2c-146">How to assign an application to a user</span></span>
<span data-ttu-id="1cf2c-147">Exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="1cf2c-148">L’utilisateur voit à présent l’application dans le client Azure RemoteApp et sera en mesure de s’y connecter.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="1cf2c-149">Comment supprimer une application d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1cf2c-149">How to remove an application from a user</span></span>
<span data-ttu-id="1cf2c-150">Exécutez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1cf2c-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="1cf2c-151">Appel à commentaires</span><span class="sxs-lookup"><span data-stu-id="1cf2c-151">Providing feedback</span></span>
<span data-ttu-id="1cf2c-152">Nous vous remercions de nous faire part de vos commentaires et suggestions concernant cette fonctionnalité en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="1cf2c-153">Veuillez répondre à cette [enquête](http://www.instant.ly/s/FDdrb) pour nous dire ce que vous en pensez.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="1cf2c-154">Vous n’avez pas eu l’occasion de tester la fonctionnalité en version préliminaire ?</span><span class="sxs-lookup"><span data-stu-id="1cf2c-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="1cf2c-155">Si vous n’avez pas encore participé à l’évaluation, utilisez cette [enquête](http://www.instant.ly/s/AY83p) pour demander l’accès à la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1cf2c-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

