---
title: Remise continue pour les services cloud avec Visual Studio Online | Microsoft Docs
description: "Apprenez à configurer la remise continue pour les applications cloud Azure sans enregistrer la clé de stockage de diagnostic sur les fichiers de configuration de service"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="45ae4-103">Enregistrer en toute sécurité la clé de stockage de diagnostic des services cloud et configurer l’intégration et le déploiement continus dans Azure à l’aide de Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="45ae4-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="45ae4-104">Il est aujourd’hui courant d’ouvrir les projets source.</span><span class="sxs-lookup"><span data-stu-id="45ae4-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="45ae4-105">L’enregistrement des secrets de l’application dans les fichiers de configuration n’est plus sûr, dans la mesure où des failles de sécurité peuvent provoquer la révélation des secrets à partir des contrôles de code source publics.</span><span class="sxs-lookup"><span data-stu-id="45ae4-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="45ae4-106">Le stockage des secrets sous forme de texte brut dans un fichier situé dans un pipeline d’intégration continue n’est pas sûr non plus, car les serveurs de génération peuvent constituer des ressources partagées dans l’environnement cloud.</span><span class="sxs-lookup"><span data-stu-id="45ae4-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="45ae4-107">Cet article explique comment Visual Studio et Visual Studio Online limitent les risques liés à la sécurité lors du développement et du processus d’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="45ae4-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="45ae4-108">Supprimer le secret de clé de stockage de diagnostic dans le fichier de configuration de projet</span><span class="sxs-lookup"><span data-stu-id="45ae4-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="45ae4-109">L’extension des diagnostics des services cloud nécessite un stockage Azure pour l’enregistrement des résultats des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="45ae4-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="45ae4-110">La chaîne de connexion au stockage était par le passé spécifiée dans les fichiers de configuration des services cloud (.cscfg) et pouvait être vérifiée via le contrôle du code source.</span><span class="sxs-lookup"><span data-stu-id="45ae4-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="45ae4-111">Dans la dernière version du Kit de développement logiciel (SDK) Azure, le comportement a été modifié pour stocker uniquement une chaîne de connexion partielle, la clé étant remplacée par un jeton.</span><span class="sxs-lookup"><span data-stu-id="45ae4-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="45ae4-112">Les étapes suivantes décrivent le fonctionnement des nouveaux outils de services cloud :</span><span class="sxs-lookup"><span data-stu-id="45ae4-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="45ae4-113">1. Ouvrez le Concepteur de rôle</span><span class="sxs-lookup"><span data-stu-id="45ae4-113">1. Open the Role designer</span></span>
* <span data-ttu-id="45ae4-114">Double-cliquez ou cliquez avec le bouton droit de la souris sur un rôle de service cloud pour ouvrir le Concepteur de rôle</span><span class="sxs-lookup"><span data-stu-id="45ae4-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Ouvrez le Concepteur de rôle][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="45ae4-116">2. Dans la section Diagnostics, une nouvelle case à cocher « Ne pas supprimer le secret de clé de stockage du projet » a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="45ae4-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="45ae4-117">Si vous utilisez l’émulateur de stockage local, cette case est désactivée, car il n’existe aucun secret à gérer pour la chaîne de connexion locale, qui est UseDevelopmentStorage=true.</span><span class="sxs-lookup"><span data-stu-id="45ae4-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![La chaîne de connexion de l’émulateur de stockage local n’est pas secrète][1]

* <span data-ttu-id="45ae4-119">Si vous créez un nouveau projet, cette case est désactivée par défaut.</span><span class="sxs-lookup"><span data-stu-id="45ae4-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="45ae4-120">De ce fait, la section Clé de stockage de la chaîne de connexion de stockage sélectionnée est remplacée par un jeton.</span><span class="sxs-lookup"><span data-stu-id="45ae4-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="45ae4-121">La valeur du jeton se trouve sous le dossier AppData Roaming de l’utilisateur actuel, par exemple : C:\Utilisateurs\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="45ae4-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="45ae4-122">Notez que l’accès au dossier user\AppData est contrôlé par les droits de l’utilisateur connecté et est considéré comme un emplacement sécurisé pour stocker les secrets de développement.</span><span class="sxs-lookup"><span data-stu-id="45ae4-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![La clé de stockage est enregistrée dans le dossier du profil utilisateur][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="45ae4-124">3. Sélectionnez un compte de stockage de diagnostics</span><span class="sxs-lookup"><span data-stu-id="45ae4-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="45ae4-125">Sélectionnez un compte de stockage à partir de la boîte de dialogue ouverte en cliquant sur « ... »</span><span class="sxs-lookup"><span data-stu-id="45ae4-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="45ae4-126">.</span><span class="sxs-lookup"><span data-stu-id="45ae4-126">button.</span></span> <span data-ttu-id="45ae4-127">Notez que la chaîne de connexion de stockage générée n’a pas la clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="45ae4-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="45ae4-128">Par exemple : DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="45ae4-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="45ae4-129">4.    Débogage du projet</span><span class="sxs-lookup"><span data-stu-id="45ae4-129">4.    Debugging the project</span></span>
* <span data-ttu-id="45ae4-130">F5 pour lancer le débogage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45ae4-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="45ae4-131">Tout doit fonctionner comme avant.</span><span class="sxs-lookup"><span data-stu-id="45ae4-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="45ae4-132">![Démarrer le débogage local][3]</span><span class="sxs-lookup"><span data-stu-id="45ae4-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="45ae4-133">5. Publier un projet à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45ae4-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="45ae4-134">Ouvrez la boîte de dialogue Publier et suivez les instructions de connexion pour publier l’application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="45ae4-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="45ae4-135">6. Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="45ae4-135">6. Additional information</span></span>
> <span data-ttu-id="45ae4-136">Remarque : le panneau Paramètres du Concepteur de rôle reste inchangé pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="45ae4-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="45ae4-137">Si vous souhaitez utiliser la fonctionnalité de gestion des secrets pour les diagnostics, accédez à l’onglet Configurations.</span><span class="sxs-lookup"><span data-stu-id="45ae4-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Ajouter des paramètres][4]

> <span data-ttu-id="45ae4-139">Remarque : si cette option est activée, la clé Application Insights sera stockée en tant que texte brut.</span><span class="sxs-lookup"><span data-stu-id="45ae4-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="45ae4-140">La clé est uniquement utilisée pour télécharger le contenu. Il n’existe donc aucun risque de compromission des données sensibles.</span><span class="sxs-lookup"><span data-stu-id="45ae4-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="45ae4-141">Créer et publier un projet de service cloud à l’aide des modèles de tâches en ligne Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45ae4-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="45ae4-142">Les étapes suivantes expliquent comment configurer l’intégration continue pour un projet de service cloud à l’aide des tâches en ligne Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="45ae4-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="45ae4-143">1.    Obtenir un compte VSO</span><span class="sxs-lookup"><span data-stu-id="45ae4-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="45ae4-144">[Créer le compte Visual Studio Online] [ Create Visual Studio Online account] si vous n’avez pas déjà</span><span class="sxs-lookup"><span data-stu-id="45ae4-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="45ae4-145">[Créer le projet d’équipe] [ Create team project] dans votre compte en ligne de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45ae4-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="45ae4-146">2.    Configurer le contrôle de code source dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45ae4-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="45ae4-147">Connectez-vous à un projet d’équipe</span><span class="sxs-lookup"><span data-stu-id="45ae4-147">Connect to a team project</span></span>

![Connectez-vous à un projet d’équipe][5]

![Sélectionnez le projet d’équipe auquel vous connecter][6]

* <span data-ttu-id="45ae4-150">Ajoutez votre projet au contrôle de code source</span><span class="sxs-lookup"><span data-stu-id="45ae4-150">Add your project to source control</span></span>

![Ajoutez le projet au contrôle de code source][7]

![Mappez le projet vers un dossier de contrôle de code source][8]

* <span data-ttu-id="45ae4-153">Archivez votre projet à partir de Team Explorer</span><span class="sxs-lookup"><span data-stu-id="45ae4-153">Check in your project from Team Explorer</span></span>

![Archivez le projet dans le contrôle de code source][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="45ae4-155">3.    Configurer le processus de génération</span><span class="sxs-lookup"><span data-stu-id="45ae4-155">3.    Configure Build process</span></span>
* <span data-ttu-id="45ae4-156">Accédez à votre projet d’équipe et ajoutez un nouveau modèle de processus de génération</span><span class="sxs-lookup"><span data-stu-id="45ae4-156">Browse to your team project and add a new build process Templates</span></span>

![Ajoutez une nouvelle génération][10]

* <span data-ttu-id="45ae4-158">Sélectionnez une tâche de génération</span><span class="sxs-lookup"><span data-stu-id="45ae4-158">Select build task</span></span>

![Ajoutez une tâche de génération][11]

![Sélectionnez le modèle de tâche de génération Visual Studio][12]

* <span data-ttu-id="45ae4-161">Modifiez l’entrée de tâche de génération.</span><span class="sxs-lookup"><span data-stu-id="45ae4-161">Edit build task input.</span></span> <span data-ttu-id="45ae4-162">Veuillez personnaliser les paramètres de génération en fonction de vos besoins</span><span class="sxs-lookup"><span data-stu-id="45ae4-162">Please customize the build parameters according to your need</span></span>

![Configurez la tâche de génération][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="45ae4-164">Configurez les variables de génération</span><span class="sxs-lookup"><span data-stu-id="45ae4-164">Configure build variables</span></span>

![Configurez les variables de génération][14]

* <span data-ttu-id="45ae4-166">Ajoutez une tâche pour charger la cible de génération</span><span class="sxs-lookup"><span data-stu-id="45ae4-166">Add a task to upload build drop</span></span>

![Choisissez de publier la tâche de cible de génération][15]

![Configurez la publication de la tâche de cible de génération][16]

* <span data-ttu-id="45ae4-169">Exécutez la génération</span><span class="sxs-lookup"><span data-stu-id="45ae4-169">Run the build</span></span>

![Mettez la nouvelle génération en file d’attente][17]

![Affichez le résumé de génération][18]

* <span data-ttu-id="45ae4-172">Si la génération est réussie, vous verrez un résultat semblable à celui-ci</span><span class="sxs-lookup"><span data-stu-id="45ae4-172">if the build is successful you will see a result similar to below</span></span>

![Résultat de la génération][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="45ae4-174">4.    Configurez un processus de publication</span><span class="sxs-lookup"><span data-stu-id="45ae4-174">4.    Configure Release process</span></span>
* <span data-ttu-id="45ae4-175">Créez une nouvelle version</span><span class="sxs-lookup"><span data-stu-id="45ae4-175">Create a new release</span></span>

![Créez une nouvelle version][20]

* <span data-ttu-id="45ae4-177">Sélectionnez la tâche de déploiement des services cloud Azure</span><span class="sxs-lookup"><span data-stu-id="45ae4-177">Select the Azure Cloud Services Deployment task</span></span>

![Sélectionnez la tâche de déploiement des services cloud Azure][21]

* <span data-ttu-id="45ae4-179">La clé de compte de stockage n’étant pas archivé dans le contrôle de code source, nous devons spécifier la clé secrète pour la configuration des extensions des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="45ae4-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="45ae4-180">Développez la section **Options avancées pour la création d’un service** et modifiez l’entrée de paramètre **Clés de compte de stockage de diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="45ae4-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="45ae4-181">Cette entrée inclut plusieurs lignes de la paire clé / valeur au format **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="45ae4-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="45ae4-182">Remarque : si votre compte de stockage de diagnostics est dans le même abonnement que celui où vous allez publier l’application de services cloud, il est inutile d’entrer la clé dans l’entrée de tâche de déploiement ; le déploiement obtiendra automatiquement les informations de stockage à partir de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="45ae4-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Configurez la tâche de déploiement des services cloud][22]

* <span data-ttu-id="45ae4-184">Utilisez les variables de génération secrètes pour enregistrer les clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="45ae4-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="45ae4-185">Pour masquer une variable secrète, cliquez sur l’icône de verrou sur le côté droit de l’entrée Variables</span><span class="sxs-lookup"><span data-stu-id="45ae4-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Enregistrez les clés de stockage dans les variables de génération secrètes][23]

* <span data-ttu-id="45ae4-187">Créez une version et déployez votre projet dans Azure</span><span class="sxs-lookup"><span data-stu-id="45ae4-187">Create a release and deploy your project to Azure</span></span>

![Créez une nouvelle version][24]

## <a name="next-steps"></a><span data-ttu-id="45ae4-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45ae4-189">Next steps</span></span>
<span data-ttu-id="45ae4-190">Pour en savoir plus sur la configuration des extensions de diagnostic pour les Services de Cloud Azure, consultez [activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="45ae4-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
