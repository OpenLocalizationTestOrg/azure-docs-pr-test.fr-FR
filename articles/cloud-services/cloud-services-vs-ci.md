---
title: remise aaaContinuous pour cloud services avec Visual Studio Online | Documents Microsoft
description: "Découvrez comment tooset de livraison continue pour Azure cloud applications sans enregistrer les fichiers de configuration de service de clés toohello stockage de diagnostics"
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="92593-103">Securely enregistrer Services Diagnostics clé de stockage Cloud et tooAzure d’intégration continue du programme d’installation et de déploiement à l’aide de Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="92593-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="92593-104">Il est aujourd'hui un communes des projets sources pratique tooopen.</span><span class="sxs-lookup"><span data-stu-id="92593-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="92593-105">L’enregistrement des secrets de l’application dans les fichiers de configuration n’est plus sûr, dans la mesure où des failles de sécurité peuvent provoquer la révélation des secrets à partir des contrôles de code source publics.</span><span class="sxs-lookup"><span data-stu-id="92593-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="92593-106">Le stockage de clé secrète comme texte en clair dans un fichier dans un pipeline de l’intégration continue n’est pas sécurisé soit depuis les serveurs de build peut être ressources partagées sur un environnement de Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="92593-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="92593-107">Cet article explique comment Visual Studio et Visual Studio Online permet d’atténuer les problèmes de sécurité hello pendant le développement et le processus d’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="92593-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="92593-108">Supprimer le secret de clé de stockage de diagnostic dans le fichier de configuration de projet</span><span class="sxs-lookup"><span data-stu-id="92593-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="92593-109">L’extension des diagnostics des services cloud nécessite un stockage Azure pour l’enregistrement des résultats des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="92593-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="92593-110">Auparavant, chaîne de connexion de stockage hello est spécifié dans les fichiers de configuration (.cscfg) de Services de cloud computing hello et peut être activé dans le contrôle de toosource.</span><span class="sxs-lookup"><span data-stu-id="92593-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="92593-111">Dans la dernière version de Windows Azure SDK hello, nous avons modifié du store tooonly hello comportement un partielle chaîne de connexion avec la clé hello remplacé par un jeton.</span><span class="sxs-lookup"><span data-stu-id="92593-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="92593-112">Hello comme suit décrire le fonctionnement des outils de Services de cloud computing hello nouvelle :</span><span class="sxs-lookup"><span data-stu-id="92593-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="92593-113">1. Ouvrez le Concepteur de rôle hello</span><span class="sxs-lookup"><span data-stu-id="92593-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="92593-114">Double-cliquez sur ou cliquez avec le bouton droit sur un concepteur de rôle Services de cloud computing rôle tooopen</span><span class="sxs-lookup"><span data-stu-id="92593-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Ouvrez le Concepteur de rôle][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="92593-116">2. Dans la section Diagnostics, une nouvelle case à cocher « Ne pas supprimer le secret de clé de stockage du projet » a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="92593-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="92593-117">Si vous utilisez l’émulateur de stockage local hello, cette case à cocher est désactivée, car il n’existe aucun secret toomanage pour la chaîne de connexion locale hello, qui est UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="92593-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![La chaîne de connexion de l’émulateur de stockage local n’est pas secrète][1]

* <span data-ttu-id="92593-119">Si vous créez un nouveau projet, cette case est désactivée par défaut.</span><span class="sxs-lookup"><span data-stu-id="92593-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="92593-120">Ainsi, dans la section de clé de stockage hello de chaîne de connexion de stockage hello sélectionné qui est remplacé par un jeton.</span><span class="sxs-lookup"><span data-stu-id="92593-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="92593-121">Hello valeur du jeton de hello trouverez sous le dossier AppData itinérant de l’utilisateur actuel hello, par exemple : C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="92593-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="92593-122">Notez le dossier user\AppData hello est l’accès contrôlé par la connexion d’utilisateur et est considéré comme un emplacement sécurisé toostore les secrets de développement.</span><span class="sxs-lookup"><span data-stu-id="92593-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![La clé de stockage est enregistrée dans le dossier du profil utilisateur][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="92593-124">3. Sélectionnez un compte de stockage de diagnostics</span><span class="sxs-lookup"><span data-stu-id="92593-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="92593-125">Sélectionnez un compte de stockage à partir de la boîte de dialogue hello lancé en cliquant sur hello «... »</span><span class="sxs-lookup"><span data-stu-id="92593-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="92593-126">.</span><span class="sxs-lookup"><span data-stu-id="92593-126">button.</span></span> <span data-ttu-id="92593-127">Notez la chaîne de connexion de stockage hello généré ne disposera de clé de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="92593-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="92593-128">Par exemple : DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="92593-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="92593-129">4.    Débogage du projet de hello</span><span class="sxs-lookup"><span data-stu-id="92593-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="92593-130">F5 toostart de débogage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92593-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="92593-131">Tout doit fonctionner dans hello même façon qu’avant.</span><span class="sxs-lookup"><span data-stu-id="92593-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="92593-132">![Démarrer le débogage local][3]</span><span class="sxs-lookup"><span data-stu-id="92593-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="92593-133">5. Publier un projet à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92593-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="92593-134">Lancement hello boîte de dialogue Publier et poursuivre les instructions de connexion toopublish hello applicaion tooAzure.</span><span class="sxs-lookup"><span data-stu-id="92593-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="92593-135">6. Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="92593-135">6. Additional information</span></span>
> <span data-ttu-id="92593-136">Remarque : panneau des paramètres dans le Concepteur de rôle hello hello resteront car il n’est pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="92593-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="92593-137">Si vous souhaitez la fonctionnalité de gestion des secrets toouse hello pour les diagnostics, accédez à onglet Configurations de toohello.</span><span class="sxs-lookup"><span data-stu-id="92593-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Ajouter des paramètres][4]

> <span data-ttu-id="92593-139">Remarque : Si activé, clé d’Application Insights hello sera stocké en tant que texte brut.</span><span class="sxs-lookup"><span data-stu-id="92593-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="92593-140">Hello clé est uniquement utilisée pour télécharger contenu est donc aucune donnée sensible au risque de compromission.</span><span class="sxs-lookup"><span data-stu-id="92593-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="92593-141">Créer et publier un projet de service cloud à l’aide des modèles de tâches en ligne Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92593-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="92593-142">Hello qui suit illustre comment toosetup intégration continue pour les Services de cloud computing de projet à l’aide de tâches en ligne de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="92593-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="92593-143">1.    Obtenir un compte VSO</span><span class="sxs-lookup"><span data-stu-id="92593-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="92593-144">[Créer le compte Visual Studio Online] [ Create Visual Studio Online account] si vous n’avez pas déjà</span><span class="sxs-lookup"><span data-stu-id="92593-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="92593-145">[Créer le projet d’équipe] [ Create team project] dans votre compte en ligne de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92593-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="92593-146">2.    Configurer le contrôle de code source dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92593-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="92593-147">Connecter le projet d’équipe tooa</span><span class="sxs-lookup"><span data-stu-id="92593-147">Connect tooa team project</span></span>

![Connecter tooteam projet][5]

![Sélectionnez tooconnect de projet d’équipe à][6]

* <span data-ttu-id="92593-150">Ajouter votre contrôle toosource de projet</span><span class="sxs-lookup"><span data-stu-id="92593-150">Add your project toosource control</span></span>

![Ajouter le contrôle toosource du projet][7]

![Mapper le dossier de contrôle de projet tooa source][8]

* <span data-ttu-id="92593-153">Archivez votre projet à partir de Team Explorer</span><span class="sxs-lookup"><span data-stu-id="92593-153">Check in your project from Team Explorer</span></span>

![Vérifiez dans le projet de contrôle de toosource][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="92593-155">3.    Configurer le processus de génération</span><span class="sxs-lookup"><span data-stu-id="92593-155">3.    Configure Build process</span></span>
* <span data-ttu-id="92593-156">Parcourir le projet d’équipe tooyour et ajouter un processus de génération de nouveaux modèles</span><span class="sxs-lookup"><span data-stu-id="92593-156">Browse tooyour team project and add a new build process Templates</span></span>

![Ajoutez une nouvelle génération][10]

* <span data-ttu-id="92593-158">Sélectionnez une tâche de génération</span><span class="sxs-lookup"><span data-stu-id="92593-158">Select build task</span></span>

![Ajoutez une tâche de génération][11]

![Sélectionnez le modèle de tâche de génération Visual Studio][12]

* <span data-ttu-id="92593-161">Modifiez l’entrée de tâche de génération.</span><span class="sxs-lookup"><span data-stu-id="92593-161">Edit build task input.</span></span> <span data-ttu-id="92593-162">Veuillez personnaliser build hello paramètres selon tooyour doivent</span><span class="sxs-lookup"><span data-stu-id="92593-162">Please customize hello build parameters according tooyour need</span></span>

![Configurez la tâche de génération][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="92593-164">Configurez les variables de génération</span><span class="sxs-lookup"><span data-stu-id="92593-164">Configure build variables</span></span>

![Configurez les variables de génération][14]

* <span data-ttu-id="92593-166">Ajouter une cible de build tooupload tâche</span><span class="sxs-lookup"><span data-stu-id="92593-166">Add a task tooupload build drop</span></span>

![Choisissez de publier la tâche de cible de génération][15]

![Configurez la publication de la tâche de cible de génération][16]

* <span data-ttu-id="92593-169">Exécutez hello build</span><span class="sxs-lookup"><span data-stu-id="92593-169">Run hello build</span></span>

![Mettez la nouvelle génération en file d’attente][17]

![Affichez le résumé de génération][18]

* <span data-ttu-id="92593-172">Si la génération de hello est réussie, vous verrez un toobelow similaire de résultat</span><span class="sxs-lookup"><span data-stu-id="92593-172">if hello build is successful you will see a result similar toobelow</span></span>

![Résultat de la génération][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="92593-174">4.    Configurez un processus de publication</span><span class="sxs-lookup"><span data-stu-id="92593-174">4.    Configure Release process</span></span>
* <span data-ttu-id="92593-175">Créez une nouvelle version</span><span class="sxs-lookup"><span data-stu-id="92593-175">Create a new release</span></span>

![Créez une nouvelle version][20]

* <span data-ttu-id="92593-177">Sélectionnez la tâche de déploiement des Services Cloud Azure hello</span><span class="sxs-lookup"><span data-stu-id="92593-177">Select hello Azure Cloud Services Deployment task</span></span>

![Sélectionnez la tâche de déploiement des services cloud Azure][21]

* <span data-ttu-id="92593-179">Comme la clé de compte de stockage hello n’est pas activée dans le contrôle toosource, nous devons toospecify une clé secrète hello pour la définition d’extensions de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="92593-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="92593-180">Développez hello **des Options avancées pour la création d’un Service** section et modifier hello **clés de compte de stockage de Diagnostics** entrée de paramètre.</span><span class="sxs-lookup"><span data-stu-id="92593-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="92593-181">Cette entrée utilise plusieurs lignes de la paire clé / valeur au format hello de **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="92593-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="92593-182">Remarque : Si votre compte de stockage est sous de diagnostics hello même abonnement qu’où vous allez publier l’application de Services de cloud computing hello, vous ne disposez tooenter hello clé dans l’entrée de tâche de déploiement hello ; déploiement de Hello récupèrera par programmation les informations de stockage hello à partir de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="92593-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Configurez la tâche de déploiement des services cloud][22]

* <span data-ttu-id="92593-184">Secret de l’utilisation de variables toosave build clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="92593-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="92593-185">entrée de Variables toomask une variable en tant que secret sur l’icône de verrou hello sur le côté droit de hello Hello</span><span class="sxs-lookup"><span data-stu-id="92593-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Enregistrez les clés de stockage dans les variables de génération secrètes][23]

* <span data-ttu-id="92593-187">Créez une version et de déployer votre tooAzure de projet</span><span class="sxs-lookup"><span data-stu-id="92593-187">Create a release and deploy your project tooAzure</span></span>

![Créez une nouvelle version][24]

## <a name="next-steps"></a><span data-ttu-id="92593-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92593-189">Next steps</span></span>
<span data-ttu-id="92593-190">toolearn en savoir plus sur la définition d’extensions de diagnostic pour les Services de Cloud Azure, consultez [activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="92593-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
