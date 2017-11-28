---
title: "applications aaaPublish tooindividual les utilisateurs dans une collection Azure RemoteApp (version préliminaire) | Documents Microsoft"
description: "Découvrez comment vous pouvez publier des utilisateurs de tooindividual d’applications, au lieu d’en fonction des groupes dans Azure RemoteApp."
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
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="8b755-103">Publier des applications tooindividual les utilisateurs dans une collection Azure RemoteApp (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="8b755-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8b755-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="8b755-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8b755-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8b755-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8b755-106">Cet article explique comment toopublish applications tooindividual les utilisateurs dans une collection Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8b755-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="8b755-107">Il s’agit de nouvelles fonctionnalités dans Azure RemoteApp, actuellement en aperçu privé et premiers tooselect uniquement disponible à des fins d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="8b755-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="8b755-108">À l’origine Azure RemoteApp n'activé qu’une seule manière de publier des applications : administrateur de hello serait de publier des applications à partir de l’image de hello et ils seraient utilisateurs tooall visible dans la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="8b755-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="8b755-109">Un scénario courant consiste à tooinclude de nombreuses applications dans une seule image et déploiement une collection dans les coûts de gestion ordre tooreduce.</span><span class="sxs-lookup"><span data-stu-id="8b755-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="8b755-110">Souvent pas toutes les applications sont pertinentes tooall utilisateurs – les administrateurs préfèrent les utilisateurs de tooindividual toopublish applications afin qu’ils ne voyez pas les applications inutiles dans leur application de flux.</span><span class="sxs-lookup"><span data-stu-id="8b755-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="8b755-111">Azure RemoteApp offre désormais cette possibilité dans le cadre d’une fonctionnalité préliminaire limitée.</span><span class="sxs-lookup"><span data-stu-id="8b755-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="8b755-112">Voici un bref résumé des nouvelles fonctionnalités de hello :</span><span class="sxs-lookup"><span data-stu-id="8b755-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="8b755-113">Une collection peut être paramétrée dans deux modes différents :</span><span class="sxs-lookup"><span data-stu-id="8b755-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="8b755-114">mode collection d’origine Hello, où tous les utilisateurs dans une collection peuvent voir toutes les applications publiées.</span><span class="sxs-lookup"><span data-stu-id="8b755-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="8b755-115">Il s’agit de mode par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="8b755-115">This is hello default mode.</span></span>
   * <span data-ttu-id="8b755-116">nouveau mode d’application Hello, où les utilisateurs voient uniquement les applications qui ont été explicitement affecté toothem</span><span class="sxs-lookup"><span data-stu-id="8b755-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="8b755-117">Au moment de hello mode d’application hello ne peut être activé à l’aide des applets de commande PowerShell de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8b755-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="8b755-118">Quand définir le mode de tooapplication, affectation d’utilisateurs dans la collection de hello ne peut pas être géré via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8b755-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="8b755-119">L’affectation d’utilisateurs a toobe géré via les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b755-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="8b755-120">Les utilisateurs voient seulement hello les applications publiées directement toothem.</span><span class="sxs-lookup"><span data-stu-id="8b755-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="8b755-121">Toutefois, il peut être encore possible pour un utilisateur toolaunch hello autres applications disponibles sur l’image de hello en y accédant directement dans le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="8b755-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="8b755-122">Cette fonctionnalité ne fournit pas un verrouillage sécurisé d’applications. Il limite uniquement la visibilité dans l’application hello de flux.</span><span class="sxs-lookup"><span data-stu-id="8b755-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="8b755-123">Si vous devez tooisolate des utilisateurs à partir d’applications, vous devez toouse des regroupements séparés pour cela.</span><span class="sxs-lookup"><span data-stu-id="8b755-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="8b755-124">Comment tooget applets de commande PowerShell de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8b755-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="8b755-125">nouvelle fonctionnalité d’aperçu des hello de tootry, vous devez applets de commande Azure PowerShell toouse.</span><span class="sxs-lookup"><span data-stu-id="8b755-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8b755-126">Il n’est pas possible toouse hello Azure Management tooenable portail hello nouvelle application mode de publication.</span><span class="sxs-lookup"><span data-stu-id="8b755-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="8b755-127">Tout d’abord, assurez-vous que vous disposez hello [module Azure PowerShell](/powershell/azure/overview) installé.</span><span class="sxs-lookup"><span data-stu-id="8b755-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="8b755-128">Puis lancez console PowerShell de hello en mode administrateur et exécution hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="8b755-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="8b755-129">Vous êtes invité à saisir vos nom d’utilisateur et mot de passe Azure.</span><span class="sxs-lookup"><span data-stu-id="8b755-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="8b755-130">Une fois connecté, vous serez en mesure de toorun Azure RemoteApp applets de commande par rapport à vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="8b755-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="8b755-131">Comment toocheck quel mode d’une collection est en</span><span class="sxs-lookup"><span data-stu-id="8b755-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="8b755-132">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="8b755-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Vérifier le mode de collecte hello](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="8b755-134">Hello AclLevel propriété peut avoir hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b755-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="8b755-135">Collection : hello d’origine mode de publication.</span><span class="sxs-lookup"><span data-stu-id="8b755-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="8b755-136">Tous les utilisateurs peuvent visualiser l’ensemble des applications publiées.</span><span class="sxs-lookup"><span data-stu-id="8b755-136">All users see all published apps.</span></span>
* <span data-ttu-id="8b755-137">Application : hello nouveau mode de publication.</span><span class="sxs-lookup"><span data-stu-id="8b755-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="8b755-138">Les utilisateurs voient uniquement les applications hello publié directement toothem.</span><span class="sxs-lookup"><span data-stu-id="8b755-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="8b755-139">Comment le mode de publication tooapplication tooswitch</span><span class="sxs-lookup"><span data-stu-id="8b755-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="8b755-140">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="8b755-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="8b755-141">État de publication application est conservé : initialement tous les utilisateurs verront toutes les applications publiées de hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="8b755-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="8b755-142">Comment les utilisateurs toolist qui peuvent voir une application spécifique</span><span class="sxs-lookup"><span data-stu-id="8b755-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="8b755-143">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="8b755-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="8b755-144">Celle-ci répertorie tous les utilisateurs peuvent voir l’application hello.</span><span class="sxs-lookup"><span data-stu-id="8b755-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="8b755-145">Remarque : Vous pouvez voir des alias d’application hello (appelés « alias application » dans la syntaxe hello ci-dessus) en exécutant Get-AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="8b755-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="8b755-146">Comment tooassign un utilisateur d’application tooa</span><span class="sxs-lookup"><span data-stu-id="8b755-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="8b755-147">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="8b755-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="8b755-148">utilisateur de Hello bénéficient d’application hello dans le client d’Azure RemoteApp hello et sera en mesure de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="8b755-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="8b755-149">Comment tooremove une application à partir d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="8b755-149">How tooremove an application from a user</span></span>
<span data-ttu-id="8b755-150">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="8b755-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="8b755-151">Appel à commentaires</span><span class="sxs-lookup"><span data-stu-id="8b755-151">Providing feedback</span></span>
<span data-ttu-id="8b755-152">Nous vous remercions de nous faire part de vos commentaires et suggestions concernant cette fonctionnalité en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="8b755-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="8b755-153">Veuillez remplir hello [enquête](http://www.instant.ly/s/FDdrb) toolet dites-nous ce que vous pensez.</span><span class="sxs-lookup"><span data-stu-id="8b755-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="8b755-154">N’ont pas eu une fonctionnalité d’aperçu chance tootry hello ?</span><span class="sxs-lookup"><span data-stu-id="8b755-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="8b755-155">Si vous n’avez pas encore participé à la version préliminaire de hello, utilisez ce [enquête](http://www.instant.ly/s/AY83p) toorequest accès.</span><span class="sxs-lookup"><span data-stu-id="8b755-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

