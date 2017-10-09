---
title: "aaaScale des rôles de travail dans les Services d’applications - Azure pile | Documents Microsoft"
description: "Instructions détaillées pour la mise à l’échelle d’App Services Azure Stack"
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a><span data-ttu-id="33ece-103">App Service sur Azure Stack : ajouter davantage de rôles de travail</span><span class="sxs-lookup"><span data-stu-id="33ece-103">App Service on Azure Stack: Adding more worker roles</span></span> 

<span data-ttu-id="33ece-104">Ce document fournit des instructions sur la façon tooscale du Service d’applications sur les rôles de travail Azure pile.</span><span class="sxs-lookup"><span data-stu-id="33ece-104">This document provides instructions about how tooscale App Service on Azure Stack worker roles.</span></span> <span data-ttu-id="33ece-105">Il contient les étapes de création d’applications de toosupport de rôles de travail supplémentaires de n’importe quelle taille.</span><span class="sxs-lookup"><span data-stu-id="33ece-105">It contains steps for creating additional worker roles toosupport applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="33ece-106">Si votre environnement POC Azure Stack n’a pas plus de 96 Go de RAM, l’ajout de capacité supplémentaire pourrait se révéler difficile.</span><span class="sxs-lookup"><span data-stu-id="33ece-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="33ece-107">App Service sur Azure Stack, par défaut, prend en charge les niveaux Worker gratuits et partagés.</span><span class="sxs-lookup"><span data-stu-id="33ece-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="33ece-108">tooadd autres niveaux de travail, vous devez tooadd plusieurs rôles de travail.</span><span class="sxs-lookup"><span data-stu-id="33ece-108">tooadd other worker tiers, you need tooadd more worker roles.</span></span>

<span data-ttu-id="33ece-109">Si vous n’êtes pas sûr de ce qui a été déployé avec la valeur par défaut de hello du Service d’applications sur l’installation de la pile d’Azure, vous pouvez consulter des informations supplémentaires dans hello [du Service d’applications sur une vue d’ensemble de la pile de Azure](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33ece-109">If you are not sure what was deployed with hello default App Service on Azure Stack installation, you can review additional information in hello [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="33ece-110">Il existe deux façons tooadd une capacité supplémentaire tooApp Service sur la pile de Azure :</span><span class="sxs-lookup"><span data-stu-id="33ece-110">There are two ways tooadd additional capacity tooApp Service on Azure Stack:</span></span>
1.  <span data-ttu-id="33ece-111">[Ajouter des traitements supplémentaires directement à partir d’avec dans hello App Service ressource fournisseur Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span><span class="sxs-lookup"><span data-stu-id="33ece-111">[Add additional workers directly from with within hello App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span></span>
2.  <span data-ttu-id="33ece-112">[Créer des machines virtuelles supplémentaires manuellement et les ajouter toohello fournisseur de ressources du Service application](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span><span class="sxs-lookup"><span data-stu-id="33ece-112">[Create additional VMs manually and add them toohello App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span></span>

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a><span data-ttu-id="33ece-113">Ajouter des traitements supplémentaires directement dans hello application administrateur fournisseur des ressources de Service.</span><span class="sxs-lookup"><span data-stu-id="33ece-113">Add additional workers directly within hello App Service Resource Provider Admin.</span></span>

1.  <span data-ttu-id="33ece-114">Se connecter toohello portail de la pile de Azure en tant qu’administrateur de service hello ;</span><span class="sxs-lookup"><span data-stu-id="33ece-114">Log in toohello Azure Stack portal as hello service administrator;</span></span>
2.  <span data-ttu-id="33ece-115">Parcourir trop**fournisseurs de ressources** et sélectionnez hello **App Service ressource fournisseur Admin**. ![Fournisseurs de ressources Azure Stack][1]</span><span class="sxs-lookup"><span data-stu-id="33ece-115">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**. ![Azure Stack Resource Providers][1]</span></span>
3.  <span data-ttu-id="33ece-116">Cliquez sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="33ece-116">Click **Roles**.</span></span>  <span data-ttu-id="33ece-117">Vous trouverez répartition hello de tous les rôles du Service d’applications déployées.</span><span class="sxs-lookup"><span data-stu-id="33ece-117">Here you see hello breakdown of all App Service roles deployed.</span></span>
4.  <span data-ttu-id="33ece-118">Cliquez sur hello option **nouvelle Instance de rôle** ![ajouter une nouvelle instance de rôle][2]</span><span class="sxs-lookup"><span data-stu-id="33ece-118">Click hello option **New Role Instance** ![Add new role instance][2]</span></span>
5.  <span data-ttu-id="33ece-119">Bonjour **nouvelle Instance de rôle** panneau :</span><span class="sxs-lookup"><span data-stu-id="33ece-119">In hello **New Role Instance** blade:</span></span>
    1. <span data-ttu-id="33ece-120">Choisissez le nombre supplémentaire **instances de rôle** tooadd voulue.</span><span class="sxs-lookup"><span data-stu-id="33ece-120">Choose how many additional **role instances** you would like tooadd.</span></span>  <span data-ttu-id="33ece-121">Dans l’aperçu de hello, il existe un maximum de 10.</span><span class="sxs-lookup"><span data-stu-id="33ece-121">In hello preview, there is a maximum of 10.</span></span>
    2. <span data-ttu-id="33ece-122">Sélectionnez hello **type de rôle**.</span><span class="sxs-lookup"><span data-stu-id="33ece-122">Select hello **role type**.</span></span>  <span data-ttu-id="33ece-123">Dans cette version préliminaire, cette option est limitée tooWeb de travail.</span><span class="sxs-lookup"><span data-stu-id="33ece-123">In this preview, this option is limited tooWeb Worker.</span></span>
    3. <span data-ttu-id="33ece-124">Sélectionnez hello **niveau de worker** vous aimeriez toodeploy ce processus de travail, le choix par défaut sont faible, moyenne, grande ou partagé.</span><span class="sxs-lookup"><span data-stu-id="33ece-124">Select hello **worker tier** you would like toodeploy this worker into, default choices are Small, Medium, Large, or Shared.</span></span>  <span data-ttu-id="33ece-125">Si vous avez créé vos propres niveaux Worker, ceux-ci sont également disponibles pour la sélection.</span><span class="sxs-lookup"><span data-stu-id="33ece-125">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span></span>
    4. <span data-ttu-id="33ece-126">Cliquez sur **OK** toodeploy hello traitements supplémentaires</span><span class="sxs-lookup"><span data-stu-id="33ece-126">Click **OK** toodeploy hello additional workers</span></span>
6.  <span data-ttu-id="33ece-127">Service d’applications va de la pile de Azure ajouter maintenant hello des machines virtuelles supplémentaires, configurez-les, installer tous les logiciels requis de hello et les marquer comme prêt lorsque ce processus est terminé.</span><span class="sxs-lookup"><span data-stu-id="33ece-127">App Service on Azure Stack will now add hello additional VMs, configure them, install all hello required software and mark them as ready when this process is complete.</span></span>  <span data-ttu-id="33ece-128">Ce processus peut prendre environ 80 minutes.</span><span class="sxs-lookup"><span data-stu-id="33ece-128">This process can take approximately 80 minutes.</span></span>
7.  <span data-ttu-id="33ece-129">Vous pouvez surveiller la progression hello de préparation hello de nouveaux threads de travail hello en affichant les workers hello Bonjour **rôles** panneau.</span><span class="sxs-lookup"><span data-stu-id="33ece-129">You can monitor hello progress of hello readiness of hello new workers by viewing hello workers in hello **roles** blade.</span></span>

>[!NOTE]
>  <span data-ttu-id="33ece-130">Dans cette version préliminaire, hello flux intégré de nouvelle Instance de rôle est limitée tooWorker rôles et déployer des machines virtuelles de taille A1.</span><span class="sxs-lookup"><span data-stu-id="33ece-130">In this preview, hello integrated New Role Instance flow is limited tooWorker Roles and deploy VMs of size A1 only.</span></span>  <span data-ttu-id="33ece-131">Nous développerons cette fonctionnalité dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="33ece-131">We will be expanding this capability in a future release.</span></span>

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a><span data-ttu-id="33ece-132">Ajout d’une capacité supplémentaire tooApp Service manuellement sur la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="33ece-132">Manually adding additional capacity tooApp Service on Azure Stack.</span></span>

<span data-ttu-id="33ece-133">Hello étapes suivantes sont requises tooadd des rôles supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="33ece-133">hello following steps are required tooadd additional roles:</span></span>

1. [<span data-ttu-id="33ece-134">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="33ece-134">Create a new virtual machine</span></span>](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [<span data-ttu-id="33ece-135">Configuration de la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="33ece-135">Configure hello virtual machine</span></span>](#step-2-configure-the-virtual-machine)
3. [<span data-ttu-id="33ece-136">Configurer le rôle de travail hello web dans le portail d’Azure pile hello</span><span class="sxs-lookup"><span data-stu-id="33ece-136">Configure hello web worker role in hello Azure Stack portal</span></span>](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [<span data-ttu-id="33ece-137">Configurer des plans App Service</span><span class="sxs-lookup"><span data-stu-id="33ece-137">Configure app service plans</span></span>](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a><span data-ttu-id="33ece-138">Étape 1 : Créer une nouvelle machine virtuelle toosupport hello nouvelle taille d’instance</span><span class="sxs-lookup"><span data-stu-id="33ece-138">Step 1: Create a new VM toosupport hello new instance size</span></span>
<span data-ttu-id="33ece-139">Créez un ordinateur virtuel, comme décrit dans [cet article](azure-stack-provision-vm.md), vous être assuré que le respect de hello sont effectuées les sélections :</span><span class="sxs-lookup"><span data-stu-id="33ece-139">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that hello following selections are made:</span></span>

* <span data-ttu-id="33ece-140">Nom d’utilisateur et mot de passe : fournir hello du même nom d’utilisateur et mot de passe fourni lors de l’installation du Service d’applications sur la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="33ece-140">User name and password: Provide hello same user name and password you provided when you installed App Service on Azure Stack.</span></span>
* <span data-ttu-id="33ece-141">Abonnement : Utiliser un abonnement de fournisseur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="33ece-141">Subscription: Use hello default provider subscription.</span></span>
* <span data-ttu-id="33ece-142">Groupe de ressources : choisissez **AppService-LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="33ece-142">Resource group: Choose **AppService-LOCAL**.</span></span>

> [!NOTE]
> <span data-ttu-id="33ece-143">Stocker des rôles de travail des machines virtuelles hello Bonjour même groupe de ressources en tant que Service d’applications sur la pile de Azure est déployé sur.</span><span class="sxs-lookup"><span data-stu-id="33ece-143">Store hello virtual machines for worker roles in hello same resource group as App Service on Azure Stack is deployed to.</span></span> <span data-ttu-id="33ece-144">(Cela est recommandé pour cette version.)</span><span class="sxs-lookup"><span data-stu-id="33ece-144">(This is recommended for this release.)</span></span>
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a><span data-ttu-id="33ece-145">Étape 2 : Configurer hello Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="33ece-145">Step 2: Configure hello Virtual Machine</span></span>
<span data-ttu-id="33ece-146">Une fois terminé, déploiement de hello hello configuration suivante est rôle de traitement web requis toosupport hello :</span><span class="sxs-lookup"><span data-stu-id="33ece-146">Once hello deployment has completed, hello following configuration is required toosupport hello web worker role:</span></span>

1. <span data-ttu-id="33ece-147">Parcourir toohello **AppService LOCAL** groupe de ressources dans le portail de hello et sélectionnez hello nouvel ordinateur vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="33ece-147">Browse toohello **AppService-LOCAL** resource group in hello portal and select hello new machine you created in Step 1.</span></span>
2. <span data-ttu-id="33ece-148">Cliquez sur connecter Bonjour panneau toodownload hello distant bureau profil d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="33ece-148">Click connect in hello VM blade toodownload hello remote desktop profile.</span></span>  <span data-ttu-id="33ece-149">Ouvrez hello profil tooopen un tooyour de session Bureau à distance machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="33ece-149">Open hello profile tooopen a remote desktop session tooyour VM.</span></span>
3. <span data-ttu-id="33ece-150">Connectez-vous à toohello machine virtuelle à l’aide du nom d’utilisateur hello et le mot de passe spécifié à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="33ece-150">Log in toohello VM using hello username and password you specified in Step 1.</span></span>
4. <span data-ttu-id="33ece-151">Ouvrez PowerShell en cliquant sur hello **Démarrer** bouton et tapez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33ece-151">Open PowerShell by clicking hello **Start** button and typing PowerShell.</span></span> <span data-ttu-id="33ece-152">Avec le bouton droit **PowerShell.exe**, puis sélectionnez **exécuter en tant qu’administrateur** tooopen PowerShell en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="33ece-152">Right-click **PowerShell.exe**, and select **Run as administrator** tooopen PowerShell in administrator mode.</span></span>
5. <span data-ttu-id="33ece-153">Copie et collage de hello suivant les commandes (un à la fois) dans la fenêtre de PowerShell hello et appuyez sur entrez :</span><span class="sxs-lookup"><span data-stu-id="33ece-153">Copy and paste each of hello following commands (one at a time) into hello PowerShell window, and press enter:</span></span>
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. <span data-ttu-id="33ece-154">Fermez votre session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="33ece-154">Close your remote desktop session.</span></span>
7. <span data-ttu-id="33ece-155">Redémarrez hello machine virtuelle à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="33ece-155">Restart hello VM from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="33ece-156">Il s’agit de la configuration minimale requise pour App Service sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="33ece-156">These are minimum requirements for App Service on Azure Stack.</span></span> <span data-ttu-id="33ece-157">Ils sont des paramètres par défaut de hello d’image de Windows 2012 R2 hello inclus avec la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="33ece-157">They are hello default settings of hello Windows 2012 R2 image included with Azure Stack.</span></span> <span data-ttu-id="33ece-158">les instructions de Hello ont été fournies pour référence ultérieure et pour ceux qui utilisent une autre image.</span><span class="sxs-lookup"><span data-stu-id="33ece-158">hello instructions have been provided for future reference, and for those using a different image.</span></span>
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a><span data-ttu-id="33ece-159">Étape 3 : Configurer le rôle de travail hello dans le portail d’Azure pile hello</span><span class="sxs-lookup"><span data-stu-id="33ece-159">Step 3: Configure hello worker role in hello Azure Stack portal</span></span>
1. <span data-ttu-id="33ece-160">Portail hello ouvrir en tant qu’administrateur de service hello sur **ClientVM**.</span><span class="sxs-lookup"><span data-stu-id="33ece-160">Open hello portal as hello service administrator on **ClientVM**.</span></span>
2. <span data-ttu-id="33ece-161">Accédez trop**fournisseurs de ressources** &gt; **App Service ressource fournisseur Admin**.![ Administrateur de fournisseur de ressources du Service d’applications][3]</span><span class="sxs-lookup"><span data-stu-id="33ece-161">Navigate too**Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span></span>
3. <span data-ttu-id="33ece-162">Dans le panneau des paramètres de hello, cliquez sur **rôles**.![ Rôles de fournisseur de ressources du Service d’applications][4]</span><span class="sxs-lookup"><span data-stu-id="33ece-162">In hello settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span></span>
4. <span data-ttu-id="33ece-163">Cliquez sur **Ajouter une instance de rôle**.</span><span class="sxs-lookup"><span data-stu-id="33ece-163">Click **Add Role Instance**.</span></span>
5. <span data-ttu-id="33ece-164">Dans la zone de texte hello **nom du serveur** entrez hello **adresse IP** du serveur hello créé précédemment (dans la Section 1).</span><span class="sxs-lookup"><span data-stu-id="33ece-164">In hello textbox for **Server Name** enter hello **IP Address** of hello server you created earlier (in Section 1).</span></span>
6. <span data-ttu-id="33ece-165">Sélectionnez hello **Type de rôle** vous aimeriez tooadd - contrôleur, serveur d’administration, frontal, traitement Web, serveur de publication ou serveur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="33ece-165">Select hello **Role Type** you would like tooadd - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span></span>  <span data-ttu-id="33ece-166">Dans cette instance, sélectionnez Web Worker.</span><span class="sxs-lookup"><span data-stu-id="33ece-166">In this instance, select Web Worker.</span></span>
7. <span data-ttu-id="33ece-167">Cliquez sur hello **niveau** vous serez comme hello toodeploy nouvelle instance trop (petite, moyenne, grande ou partagé).</span><span class="sxs-lookup"><span data-stu-id="33ece-167">Click hello **Tier** you would like toodeploy hello new instance too(small, medium, large, or shared).</span></span>  <span data-ttu-id="33ece-168">Si vous avez créé vos propres niveaux Worker, ceux-ci sont également disponibles pour la sélection.</span><span class="sxs-lookup"><span data-stu-id="33ece-168">If you have created your own worker tiers these will also be available for selection.</span></span>
8. <span data-ttu-id="33ece-169">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="33ece-169">Click **OK.**</span></span>
9. <span data-ttu-id="33ece-170">Revenir en arrière toohello **rôles** vue</span><span class="sxs-lookup"><span data-stu-id="33ece-170">Go back toohello **Roles** view</span></span>
10. <span data-ttu-id="33ece-171">Cliquez sur hello ligne toohello correspondante combinaison Type de rôle et le niveau de traitement attribué de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="33ece-171">Click hello row corresponding toohello Role Type and Worker Tier combination you assigned your VM to.</span></span>
11. <span data-ttu-id="33ece-172">Recherchez pourquoi le nom de serveur que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="33ece-172">Look for hello Server Name you just added.</span></span> <span data-ttu-id="33ece-173">Passez en revue la colonne d’état hello et attendre la prochaine étape de toomove toohello état de hello « Prêt ».</span><span class="sxs-lookup"><span data-stu-id="33ece-173">Review hello status column, and wait toomove toohello next step until hello status is "Ready."</span></span> <span data-ttu-id="33ece-174">Ceci peut prendre environ 80 minutes.</span><span class="sxs-lookup"><span data-stu-id="33ece-174">This can take approximately 80 minutes.</span></span> <span data-ttu-id="33ece-175">![Rôle Fournisseur de ressources App Service prêt][5]</span><span class="sxs-lookup"><span data-stu-id="33ece-175">![App Service Resource Provider Role Ready][5]</span></span>

## <a name="step-4-configure-app-service-plans"></a><span data-ttu-id="33ece-176">Étape 4 : Configurer des plans App Service</span><span class="sxs-lookup"><span data-stu-id="33ece-176">Step 4: Configure app service plans</span></span>

1. <span data-ttu-id="33ece-177">Portail toohello sur hello ClientVM vous connecter.</span><span class="sxs-lookup"><span data-stu-id="33ece-177">Sign in toohello portal on hello ClientVM.</span></span>
2. <span data-ttu-id="33ece-178">Accédez trop**nouveau** &gt; **Web et Mobile**.</span><span class="sxs-lookup"><span data-stu-id="33ece-178">Navigate too**New** &gt; **Web and Mobile**.</span></span>
3. <span data-ttu-id="33ece-179">Sélectionnez le type de hello d’application, vous aimeriez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33ece-179">Select hello type of application you would like toodeploy.</span></span>
4. <span data-ttu-id="33ece-180">Fournir des informations de hello pour application hello et sélectionnez **un Plan / emplacement**.</span><span class="sxs-lookup"><span data-stu-id="33ece-180">Provide hello information for hello application, and then select **AppService Plan / Location**.</span></span>
    1. <span data-ttu-id="33ece-181">Cliquez sur **Create New**.</span><span class="sxs-lookup"><span data-stu-id="33ece-181">Click **Create New**.</span></span>
    2. <span data-ttu-id="33ece-182">Créer votre plan, en sélectionnant hello correspondant niveau tarifaire pour hello plan.</span><span class="sxs-lookup"><span data-stu-id="33ece-182">Create your plan, selecting hello corresponding pricing tier for hello plan.</span></span>

> [!NOTE]
> <span data-ttu-id="33ece-183">Dans ce panneau, vous pouvez créer plusieurs plans.</span><span class="sxs-lookup"><span data-stu-id="33ece-183">You can create multiple plans while on this blade.</span></span> <span data-ttu-id="33ece-184">Avant de déployer, toutefois, assurez-vous que vous avez sélectionné le plan approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="33ece-184">Before you deploy, however, ensure you have selected hello appropriate plan.</span></span>
> 
> 

<span data-ttu-id="33ece-185">Hello Voici un exemple de hello plusieurs niveaux de tarification disponibles par défaut.</span><span class="sxs-lookup"><span data-stu-id="33ece-185">hello following shows an example of hello multiple pricing tiers available by default.</span></span>  <span data-ttu-id="33ece-186">Vous remarquerez que s’il n’y a aucune disposition des employés pour un niveau de travail spécifique, hello de toochoose option hello correspondant du niveau tarifaire est indisponible.</span><span class="sxs-lookup"><span data-stu-id="33ece-186">You notice that if there are no available workers for a particular worker tier, hello option toochoose hello corresponding pricing tier is unavailable.</span></span>![Niveaux tarifaires par défaut App Service sur Azure Stack][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
