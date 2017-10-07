---
title: remise aaaContinuous pour cloud services avec TFS dans Azure | Documents Microsoft
description: "Découvrez comment les applications cloud tooset de livraison continue pour Azure. Exemples de code pour les instructions en ligne de commande MSBuild et les scripts PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="115a9-104">Remise continue pour Cloud Services dans Azure</span><span class="sxs-lookup"><span data-stu-id="115a9-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="115a9-105">Hello est décrite dans cet article vous montre comment tooset de livraison continue pour les applications de cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="115a9-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="115a9-106">Ce processus vous permet de créer automatiquement des packages et de déployer hello package tooAzure après chaque archivage de code.</span><span class="sxs-lookup"><span data-stu-id="115a9-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="115a9-107">processus de génération de package décrit dans cet article Hello est équivalent toohello **Package** commande dans Visual Studio et la procédure de publication est équivalent toohello **publier** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="115a9-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="115a9-108">Hello article couvre hello méthodes que vous utiliseriez toocreate un serveur de builds avec les instructions de ligne de commande MSBuild et scripts Windows PowerShell et également montre comment toooptionally configurer Visual Studio Team Foundation Server - définitions de Build d’équipe commandes de MSBuild toouse hello et scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="115a9-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="115a9-109">processus de Hello est personnalisable pour votre environnement de génération et les environnements cibles Azure.</span><span class="sxs-lookup"><span data-stu-id="115a9-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="115a9-110">Vous pouvez également utiliser Visual Studio Team Services, une version de TFS qui est hébergé dans Azure, toodo cela plus facilement.</span><span class="sxs-lookup"><span data-stu-id="115a9-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="115a9-111">Avant de commencer, vous devez publier votre application à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="115a9-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="115a9-112">Cela permet de garantir que toutes les ressources de hello sont disponibles et initialisé lors du processus de publication tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="115a9-113">1 : configurer hello serveur Build</span><span class="sxs-lookup"><span data-stu-id="115a9-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="115a9-114">Avant de pouvoir créer un package Azure à l’aide de MSBuild, vous devez installer les logiciels requis de hello et les outils sur le serveur de builds hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="115a9-115">Visual Studio n’est pas requis toobe installé sur le serveur de builds hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="115a9-116">Si vous souhaitez toouse Service Team Foundation Build toomanage de votre serveur de builds, suivez les instructions de hello Bonjour [Service Team Foundation Build] [ Team Foundation Build Service] documentation.</span><span class="sxs-lookup"><span data-stu-id="115a9-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="115a9-117">Sur le serveur de builds hello, installez hello [.NET Framework 4.5.2][.NET Framework 4.5.2], qui inclut MSBuild.</span><span class="sxs-lookup"><span data-stu-id="115a9-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="115a9-118">Installer hello dernières [outils de création de Azure pour .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="115a9-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="115a9-119">Installer hello [bibliothèques Azure pour .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="115a9-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="115a9-120">Serveur de builds de copier le fichier Microsoft.WebApplication.targets hello à partir d’un toohello d’installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="115a9-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="115a9-121">Sur un ordinateur avec Visual Studio est installé, ce fichier se trouve dans le répertoire hello C:\\Files(x86)%\\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="115a9-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="115a9-122">Vous devez le copier toohello même répertoire sur le serveur de builds hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="115a9-123">Installer hello [Azure Tools pour Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="115a9-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="115a9-124">2 : Génération d'un package à l'aide des commandes MSBuild</span><span class="sxs-lookup"><span data-stu-id="115a9-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="115a9-125">Cette section décrit comment tooconstruct un MSBuild commande qui crée un package Azure.</span><span class="sxs-lookup"><span data-stu-id="115a9-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="115a9-126">Exécutez cette étape sur hello build server tooverify que tout est configuré correctement et qui exécute la commande de MSBuild hello ce que vous souhaitez toodo.</span><span class="sxs-lookup"><span data-stu-id="115a9-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="115a9-127">Vous pouvez ajouter cette ligne de commande de tooexisting générer des scripts sur le serveur de builds hello, ou vous pouvez utiliser la ligne de commande hello dans une définition de Build TFS, comme décrit dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="115a9-128">Pour plus d’informations sur les paramètres de ligne de commande et MSBuild, consultez la page [Référence de la ligne de commande MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="115a9-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="115a9-129">Si Visual Studio est installé sur le serveur de builds hello, recherchez et sélectionnez **invite de commandes Visual Studio** Bonjour **Visual Studio Tools** dossier dans Windows.</span><span class="sxs-lookup"><span data-stu-id="115a9-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="115a9-130">Si Visual Studio n’est pas installé sur le serveur de builds hello, ouvrez une invite de commandes et assurez-vous que le MSBuild.exe est accessible sur le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="115a9-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="115a9-131">MSBuild est installé avec hello .NET Framework dans hello chemin d’accès % Windir%\\Microsoft.NET\\Framework\\*Version*.</span><span class="sxs-lookup"><span data-stu-id="115a9-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="115a9-132">Par exemple, pour ajouter la variable d’environnement PATH MSBuild.exe toohello lorsque vous avez installé .NET Framework 4, tapez Bonjour commande à l’invite de commandes hello suivante :</span><span class="sxs-lookup"><span data-stu-id="115a9-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="115a9-133">À l’invite de commandes hello accédez dossier toohello contenant le fichier de projet Windows Azure que vous souhaitez toobuild.</span><span class="sxs-lookup"><span data-stu-id="115a9-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="115a9-134">Exécuter MSBuild avec hello /target : publier l’option comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="115a9-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="115a9-135">Cette option peut être abrégée en /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="115a9-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="115a9-136">option de /t:Publish Hello dans MSBuild ne doit pas être confondue avec les commandes de publication hello disponibles dans Visual Studio lorsque vous avez hello Qu'azure SDK installé.</span><span class="sxs-lookup"><span data-stu-id="115a9-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="115a9-137">Hello /t : option de publication uniquement les builds hello packages Azure.</span><span class="sxs-lookup"><span data-stu-id="115a9-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="115a9-138">Il ne déploie pas les packages hello comme les commandes de publication hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="115a9-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="115a9-139">Si vous le souhaitez, vous pouvez spécifier le nom du projet hello comme paramètre de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="115a9-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="115a9-140">Si non spécifié, le répertoire actuel de hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="115a9-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="115a9-141">Pour plus d’informations sur les options de ligne de commande MSBuild, consultez la page [Référence de la ligne de commande MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="115a9-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="115a9-142">Recherchez la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-142">Locate hello output.</span></span> <span data-ttu-id="115a9-143">Par défaut, cette commande crée un répertoire dans la relation toohello racine dossier hello projet, tel que *Répertoireprojet*\\bin\\*Configuration* \\ App.Publish\\.</span><span class="sxs-lookup"><span data-stu-id="115a9-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="115a9-144">Lorsque vous générez un projet Windows Azure, vous générez deux fichiers, fichier de package hello lui-même et hello qui accompagne le fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="115a9-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="115a9-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="115a9-145">Project.cspkg</span></span>
   * <span data-ttu-id="115a9-146">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="115a9-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="115a9-147">Par défaut, tous les projets Azure comprennent un fichier de configuration de service (.cscfg file) pour les versions locales (débogage) et un autre pour les versions cloud (intermédiaire ou de production), mais vous pouvez ajouter ou supprimer les fichiers de configuration de service selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="115a9-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="115a9-148">Lorsque vous créez un package dans Visual Studio, vous devez le tooinclude de fichier de configuration de service en même temps que le package de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="115a9-149">Spécifiez le fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-149">Specify hello service configuration file.</span></span> <span data-ttu-id="115a9-150">Lorsque vous générez un package à l’aide de MSBuild, le fichier de configuration de service local hello est inclus par défaut.</span><span class="sxs-lookup"><span data-stu-id="115a9-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="115a9-151">tooinclude un fichier de configuration de service différent, définissez la propriété de Profilcible de la commande MSBuild hello, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="115a9-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="115a9-152">Spécifiez l’emplacement hello pour la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-152">Specify hello location for hello output.</span></span> <span data-ttu-id="115a9-153">Chemin d’accès de hello jeu à l’aide de la/p : PublishDir =*active* \\ option, y compris hello à droite du séparateur barre oblique inverse, hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="115a9-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="115a9-154">Une fois que vous avez construit et testé un MSBuild appropriée toobuild de ligne de commande de vos projets et les associer dans un package d’Azure, vous pouvez ajouter cette ligne de commande tooyour des scripts de build.</span><span class="sxs-lookup"><span data-stu-id="115a9-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="115a9-155">Si votre serveur de builds utilise des scripts personnalisés, ce processus dépend des particularités de votre processus de génération personnalisé.</span><span class="sxs-lookup"><span data-stu-id="115a9-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="115a9-156">Si vous utilisez TFS comme un environnement de génération, vous pouvez suivre les instructions hello hello prochaine étape tooadd hello package Azure build tooyour processus de génération.</span><span class="sxs-lookup"><span data-stu-id="115a9-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="115a9-157">3 : Génération d’un package avec TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="115a9-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="115a9-158">Si vous avez configuré comme serveur de création d’un contrôleur de build et le hello Team Foundation Server (TFS) configuré comme un ordinateur de build TFS, puis vous pouvez éventuellement configurer une génération automatique de votre package d’Azure.</span><span class="sxs-lookup"><span data-stu-id="115a9-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="115a9-159">Pour plus d’informations sur comment tooset haut et utiliser Team Foundation server comme un système de génération, consultez [montée en charge votre système de génération][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="115a9-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="115a9-160">En particulier, la procédure suivante suppose que vous avez configuré votre serveur de builds comme décrit dans [déployer et configurer un serveur de builds][Deploy and configure a build server], et que vous avez créé un projet d’équipe créé un cloud projet de service dans le projet d’équipe hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="115a9-161">tooconfigure TFS toobuild Azure packages, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="115a9-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="115a9-162">Dans Visual Studio sur votre ordinateur de développement sur le menu Affichage de hello, choisissez **Team Explorer**, ou choisissez Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="115a9-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="115a9-163">Dans la fenêtre Team Explorer, développez hello **génère** nœud ou choisissez hello **génère** page, puis choisissez **nouvelle définition de Build**.</span><span class="sxs-lookup"><span data-stu-id="115a9-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Option Nouvelle définition de build][0]
2. <span data-ttu-id="115a9-165">Choisissez hello **déclencheur** onglet et spécifier hello souhaitées conditions lorsque vous souhaitez hello toobe package généré.</span><span class="sxs-lookup"><span data-stu-id="115a9-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="115a9-166">Par exemple, spécifier **intégration continue** package de hello toobuild chaque fois qu’un contrôle de source de vérification se produit.</span><span class="sxs-lookup"><span data-stu-id="115a9-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="115a9-167">Choisissez hello **paramètres Source** onglet et vérifiez que votre dossier de projet est répertorié dans hello **dossier de contrôle de code Source** colonne, et l’état hello est **Active**.</span><span class="sxs-lookup"><span data-stu-id="115a9-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="115a9-168">Choisissez hello **générer les valeurs par défaut** onglet et sous contrôleur de Build, vérifiez le nom de hello du serveur de builds hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="115a9-169">Choisissez également hello option **dossier de dépôt suivant de toohello de sortie de build copie** et spécifiez l’emplacement de dépôt hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="115a9-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="115a9-170">Choisissez hello **processus** onglet. Sous l’onglet processus de hello, choisissez un modèle par défaut de hello, sous **générer**, choisissez le projet de hello si elle n’est pas déjà sélectionnée et développez hello **avancé** section Bonjour **générer**section de la grille de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="115a9-171">Choisissez **Arguments MSBuild**et définissez les arguments de ligne de commande MSBuild hello appropriés comme décrit à l’étape 2 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="115a9-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="115a9-172">Par exemple, entrez **/t : publier/p : PublishDir =\\\\myserver\\supprime\\**  toobuild un package hello du package et copie les fichiers toohello emplacement \\ \\myserver\\supprime\\:</span><span class="sxs-lookup"><span data-stu-id="115a9-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![Arguments MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="115a9-174">Copie hello fichiers tooa partage public rend plus facile toomanually déployer des packages de hello à partir de votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="115a9-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="115a9-175">Réussite hello de votre étape de génération de test en vérifiant dans un projet de tooyour de modification ou d’une nouvelle build en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="115a9-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="115a9-176">tooqueue d’une nouvelle build, dans Team Explorer, cliquez sur **toutes les définitions de Build,** , puis **file d’attente une nouvelle Build**.</span><span class="sxs-lookup"><span data-stu-id="115a9-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="115a9-177">4 : Publication d'un package à l'aide d'un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="115a9-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="115a9-178">Cette section décrit comment tooconstruct un script Windows PowerShell qui publiera le package d’application Cloud hello sortie tooAzure à l’aide des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="115a9-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="115a9-179">Ce script peut être appelé une fois l’étape de génération de hello dans votre automatisation de génération personnalisée.</span><span class="sxs-lookup"><span data-stu-id="115a9-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="115a9-180">Il peut également être appelé depuis les activités de workflow du modèle de processus dans Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="115a9-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="115a9-181">Installer hello [applets de commande Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="115a9-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="115a9-182">Pendant la phase d’installation hello applet de commande, choisissez tooinstall comme un composant logiciel enfichable.</span><span class="sxs-lookup"><span data-stu-id="115a9-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="115a9-183">Notez que cette version officiellement pris en charge remplace la version antérieure de hello proposée via CodePlex, bien que les versions précédentes de hello numéro 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="115a9-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="115a9-184">Démarrez PowerShell Azure à l’aide du menu Démarrer de hello ou page de démarrage.</span><span class="sxs-lookup"><span data-stu-id="115a9-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="115a9-185">Si vous démarrez de cette façon, hello applets de commande PowerShell de Azure est chargé.</span><span class="sxs-lookup"><span data-stu-id="115a9-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="115a9-186">À l’invite de PowerShell hello, vérifiez que les applets de commande PowerShell hello sont chargées en entrant la commande partielle hello `Get-Azure` et en appuyant sur hello touche Tab pour la saisie semi-automatique des instructions.</span><span class="sxs-lookup"><span data-stu-id="115a9-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="115a9-187">Si vous appuyez sur TAB. hello à plusieurs reprises, vous devez voir les différentes commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="115a9-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="115a9-188">Vérifiez que vous pouvez vous connecter tooyour abonnement Azure en important les informations de votre abonnement à partir du fichier .publishsettings de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="115a9-189">Puis entrez la commande hello</span><span class="sxs-lookup"><span data-stu-id="115a9-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="115a9-190">Ceci affiche les informations sur votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="115a9-190">This shows information about your subscription.</span></span> <span data-ttu-id="115a9-191">Vérifiez que tout est correct.</span><span class="sxs-lookup"><span data-stu-id="115a9-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="115a9-192">Enregistrer le modèle de script hello fourni à fin hello de cet article dans votre dossier de scripts en tant que c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="115a9-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="115a9-193">Passez en revue la section des paramètres de script de hello hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="115a9-194">Ajoutez des valeurs ou modifiez les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="115a9-194">Add or modify any default values.</span></span> <span data-ttu-id="115a9-195">Ces valeurs peuvent de toute manière être ignorées en indiquant des paramètres explicites.</span><span class="sxs-lookup"><span data-stu-id="115a9-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="115a9-196">Vérifiez contient le service cloud valide des comptes de stockage créés dans votre abonnement qui peut être ciblé par hello du script de publication.</span><span class="sxs-lookup"><span data-stu-id="115a9-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="115a9-197">Le compte de stockage (stockage d’objets blob) sera être utilisé tooupload et stocker temporairement les fichier de package et de configuration de déploiement hello pendant le déploiement est en cours de création.</span><span class="sxs-lookup"><span data-stu-id="115a9-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="115a9-198">toocreate un nouveau service cloud, vous pouvez appeler cette hello script ou utilisez [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="115a9-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="115a9-199">nom de service de cloud Hello sera utilisé en tant que préfixe dans un nom de domaine complet, et par conséquent, il doit être unique.</span><span class="sxs-lookup"><span data-stu-id="115a9-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="115a9-200">toocreate un compte de stockage, vous pouvez appeler cette hello script ou utilisez [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="115a9-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="115a9-201">nom de compte de stockage Hello sera utilisé en tant que préfixe dans un nom de domaine complet, et par conséquent, il doit être unique.</span><span class="sxs-lookup"><span data-stu-id="115a9-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="115a9-202">Vous pouvez essayer à l’aide de hello même nom que le service cloud.</span><span class="sxs-lookup"><span data-stu-id="115a9-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="115a9-203">Appeler le script de hello directement à partir d’Azure PowerShell ou associer cette toooccur automation de script tooyour hôte build après génération du package hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="115a9-204">script de Hello sera toujours supprimer ou remplacer vos déploiements existants par défaut si elles sont détectées.</span><span class="sxs-lookup"><span data-stu-id="115a9-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="115a9-205">Ceci est nécessaire pour permettre la remise continue automatique là où il n'est pas possible de demander à l'utilisateur d'intervenir.</span><span class="sxs-lookup"><span data-stu-id="115a9-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="115a9-206">**Exemple de scénario 1 :** toohello déploiement continu environnement d’un service intermédiaire :</span><span class="sxs-lookup"><span data-stu-id="115a9-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="115a9-207">Cette opération est normalement suivie d'un test de vérification et d'un échange d'adresses IP virtuelles.</span><span class="sxs-lookup"><span data-stu-id="115a9-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="115a9-208">permutation de Hello adresse IP virtuelle peut être effectuée via hello [portail Azure](https://portal.azure.com) ou en utilisant l’applet de commande Move-déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="115a9-209">**Exemple de scénario 2 :** environnement de production toohello déploiement continu d’un service de test dédié</span><span class="sxs-lookup"><span data-stu-id="115a9-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="115a9-210">**Bureau à distance :**</span><span class="sxs-lookup"><span data-stu-id="115a9-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="115a9-211">Si le Bureau à distance est activé dans votre projet Windows Azure, vous devez étapes supplémentaires à usage unique tooperform hello tooensure que bon certificat de Service Cloud est téléchargés les services de cloud computing tooall ciblées par ce script.</span><span class="sxs-lookup"><span data-stu-id="115a9-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="115a9-212">Recherchez les valeurs d’empreinte numérique du certificat hello attendus par vos rôles.</span><span class="sxs-lookup"><span data-stu-id="115a9-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="115a9-213">Les valeurs de l’empreinte numérique sont visibles dans la section certificats de hello du fichier de configuration de cloud (c'est-à-dire ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="115a9-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="115a9-214">Il est également visible dans la boîte de dialogue hello Configuration Bureau à distance dans Visual Studio vous afficher les Options et afficher hello sélectionné de certificat.</span><span class="sxs-lookup"><span data-stu-id="115a9-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="115a9-215">Télécharger des certificats de bureau à distance en tant qu’une étape d’installation unique à l’aide de hello script de l’applet de commande suivant :</span><span class="sxs-lookup"><span data-stu-id="115a9-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="115a9-216">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="115a9-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="115a9-217">Vous pouvez également exporter le fichier de certificat PFX hello avec la clé privée et le téléchargement des certificats tooeach cible cloud service à l’aide de la [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="115a9-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="115a9-218">**Mise à niveau du déploiement et suppression du déploiement -\> Nouveau déploiement**</span><span class="sxs-lookup"><span data-stu-id="115a9-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="115a9-219">Hello script par défaut effectue un déploiement de mise à niveau ($enableDeploymentUpgrade = 1) lorsque aucun paramètre n’est passé ou la valeur 1 est passée de manière explicite.</span><span class="sxs-lookup"><span data-stu-id="115a9-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="115a9-220">Pour les instances uniques, ceci présente l'avantage de prendre moins de temps qu'un déploiement complet.</span><span class="sxs-lookup"><span data-stu-id="115a9-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="115a9-221">Pour les instances qui nécessitent une haute disponibilité, qu'il présente également l’avantage de hello de laisser des instances en cours d’exécution tandis que d’autres sont mis à niveau (parcours de votre domaine de mise à jour), ainsi que votre adresse IP virtuelle n’est pas supprimé.</span><span class="sxs-lookup"><span data-stu-id="115a9-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="115a9-222">Déploiement de mise à niveau peut être désactivé dans le script de hello ($enableDeploymentUpgrade = 0) ou en passant *enableDeploymentUpgrade - 0* en tant que paramètre, ce qui modifie la suppression de toofirst de comportement de script tout déploiement existant, puis créer un nouveau déploiement.</span><span class="sxs-lookup"><span data-stu-id="115a9-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="115a9-223">script de Hello sera toujours supprimer ou remplacer vos déploiements existants par défaut si elles sont détectées.</span><span class="sxs-lookup"><span data-stu-id="115a9-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="115a9-224">Ceci est nécessaire pour permettre la remise continue automatique là où il n'est pas possible de demander à l'utilisateur ou à l'opérateur d'intervenir.</span><span class="sxs-lookup"><span data-stu-id="115a9-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="115a9-225">5 : Publication d’un package avec TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="115a9-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="115a9-226">Cette étape facultative connecte à TFS Team Build toohello script créé à l’étape 4, qui gère la publication de tooAzure de génération de package hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="115a9-227">Cela implique la modification hello de modèle de processus utilisé par votre définition de build pour qu’il exécute une activité de publier à fin hello du flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="115a9-228">Hello publication s’exécute la commande PowerShell en passant les paramètres de génération de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="115a9-229">Sortie de hello MSBuild cible et un script de publication sera redirigé dans la sortie de génération standard de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="115a9-230">Modifier hello responsable de la définition de Build en continu déployer.</span><span class="sxs-lookup"><span data-stu-id="115a9-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="115a9-231">Sélectionnez hello **processus** onglet.</span><span class="sxs-lookup"><span data-stu-id="115a9-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="115a9-232">Suivez [ces instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd un projet d’activité pour hello générer le modèle de processus, téléchargez le modèle par défaut de hello, ajoutez-le au projet de hello et archivez-le.</span><span class="sxs-lookup"><span data-stu-id="115a9-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="115a9-233">Renommer le modèle de processus de génération hello, telles que AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="115a9-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="115a9-234">Retourner toohello **processus** onglet et utiliser **afficher les détails** tooshow une liste des modèles de processus de génération disponibles.</span><span class="sxs-lookup"><span data-stu-id="115a9-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="115a9-235">Choisissez hello **nouveau...**  bouton, puis accédez de projet toohello vous venez d’ajouter et archivé.</span><span class="sxs-lookup"><span data-stu-id="115a9-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="115a9-236">Recherchez le modèle hello vous venez de créer et choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="115a9-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="115a9-237">Ouvrez hello sélectionné de modèle de processus à modifier.</span><span class="sxs-lookup"><span data-stu-id="115a9-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="115a9-238">Vous pouvez ouvrir directement dans le Concepteur de flux de travail hello ou dans toowork de l’éditeur XML hello avec hello XAML.</span><span class="sxs-lookup"><span data-stu-id="115a9-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="115a9-239">Ajoutez hello suivant de la liste des nouveaux arguments en tant que lignes séparées dans l’onglet des arguments hello du Concepteur de flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="115a9-240">Tous ces arguments doivent avoir direction=In et type=String.</span><span class="sxs-lookup"><span data-stu-id="115a9-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="115a9-241">Il s’agit des paramètres tooflow utilisé à partir de la définition de build hello dans le flux de travail hello, quels hello de toocall utilisé get puis publier le script.</span><span class="sxs-lookup"><span data-stu-id="115a9-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Liste des arguments][3]

   <span data-ttu-id="115a9-243">Hello que XAML correspondant se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="115a9-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="115a9-244">Ajoutez une nouvelle séquence à fin hello de s’exécuter sur l’Agent :</span><span class="sxs-lookup"><span data-stu-id="115a9-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="115a9-245">Commencez par ajouter un toocheck d’activité instruction If pour un fichier de script valide.</span><span class="sxs-lookup"><span data-stu-id="115a9-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="115a9-246">Valeur des toothis de condition hello :</span><span class="sxs-lookup"><span data-stu-id="115a9-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="115a9-247">Bonjour puis les cas de hello instruction If, ajouter une nouvelle activité de séquence.</span><span class="sxs-lookup"><span data-stu-id="115a9-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="115a9-248">Ensemble hello affichage nom too'Start publier '</span><span class="sxs-lookup"><span data-stu-id="115a9-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="115a9-249">Hello début publier la séquence étant toujours sélectionnée, ajouter la liste suivante de nouvelles variables en tant que lignes séparées dans l’onglet variables de Concepteur de workflow hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="115a9-250">Toutes les variables doivent comporter type =String et Scope=Start publish.</span><span class="sxs-lookup"><span data-stu-id="115a9-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="115a9-251">Il s’agit des paramètres tooflow utilisé à partir de la définition de build hello dans le flux de travail, le hello de toocall utilisé get puis publier le script.</span><span class="sxs-lookup"><span data-stu-id="115a9-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="115a9-252">SubscriptionDataFilePath, de type String</span><span class="sxs-lookup"><span data-stu-id="115a9-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="115a9-253">PublishScriptFilePath, de type String</span><span class="sxs-lookup"><span data-stu-id="115a9-253">PublishScriptFilePath, of type String</span></span>

        ![Nouvelles variables][4]
   4. <span data-ttu-id="115a9-255">Si vous utilisez TFS 2012 ou version antérieure, ajoutez une activité ConvertWorkspaceItem début de hello de hello nouvelle séquence.</span><span class="sxs-lookup"><span data-stu-id="115a9-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="115a9-256">Si vous utilisez TFS 2013 ou version ultérieure, ajoutez une activité GetLocalPath début de hello de nouvelle séquence de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="115a9-257">Pour un ConvertWorkspaceItem, définissez les propriétés de hello comme suit : Direction = ServerToLocal, DisplayName = 'Convert publish nom de fichier de script', entrée = 'PublishScriptLocation', résultat = 'PublishScriptFilePath', espace de travail = 'Espace de travail'.</span><span class="sxs-lookup"><span data-stu-id="115a9-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="115a9-258">Pour une activité GetLocalPath, définissez hello propriété IncomingPath too'PublishScriptLocation », et hello too'PublishScriptFilePath de résultat '.</span><span class="sxs-lookup"><span data-stu-id="115a9-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="115a9-259">Cette toohello de chemin d’accès hello activité convertit un script à partir d’emplacements de serveur TFS de publication (le cas échéant) le chemin d’accès de tooa standard disque local.</span><span class="sxs-lookup"><span data-stu-id="115a9-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="115a9-260">Si vous utilisez TFS 2012 ou version antérieure, ajoutez une autre activité ConvertWorkspaceItem à fin hello de hello nouvelle séquence.</span><span class="sxs-lookup"><span data-stu-id="115a9-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="115a9-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="115a9-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="115a9-262">Si vous utilisez TFS 2013 ou version ultérieure, ajoutez un autre GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="115a9-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="115a9-263">IncomingPath='SubscriptionDataFileLocation' et Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="115a9-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="115a9-264">Ajouter une activité InvokeProcess à fin hello Hello nouvelle séquence.</span><span class="sxs-lookup"><span data-stu-id="115a9-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="115a9-265">Cette activité d’appels PowerShell.exe avec des arguments de hello transmis par hello la définition de Build.</span><span class="sxs-lookup"><span data-stu-id="115a9-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="115a9-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="115a9-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="115a9-267">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="115a9-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="115a9-268">Nom de fichier = « PowerShell » (en incluant les guillemets hello)</span><span class="sxs-lookup"><span data-stu-id="115a9-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="115a9-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="115a9-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="115a9-270">Bonjour **Handle Standard Output** section zone de texte de la InvokeProcess, définissez too'data de valeur de zone de texte hello ».</span><span class="sxs-lookup"><span data-stu-id="115a9-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="115a9-271">Il s’agit d’une variable toostore les données de sortie standard salutation.</span><span class="sxs-lookup"><span data-stu-id="115a9-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="115a9-272">Ajouter une activité WriteBuildMessage juste en dessous de hello **Handle Standard Output** section.</span><span class="sxs-lookup"><span data-stu-id="115a9-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="115a9-273">Définir l’Importance de hello = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' et hello Message = « données ».</span><span class="sxs-lookup"><span data-stu-id="115a9-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="115a9-274">Cela garantit la sortie standard de hello du script sera écrite toohello sortie de la génération.</span><span class="sxs-lookup"><span data-stu-id="115a9-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="115a9-275">Bonjour **Handle Error Output** section zone de texte de la InvokeProcess, définissez too'data de valeur de zone de texte hello ».</span><span class="sxs-lookup"><span data-stu-id="115a9-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="115a9-276">Il s’agit d’une les données de variable toostore salutation erreur standard.</span><span class="sxs-lookup"><span data-stu-id="115a9-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="115a9-277">Ajouter une activité WriteBuildError juste en dessous de hello **Handle Error Output** section.</span><span class="sxs-lookup"><span data-stu-id="115a9-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="115a9-278">Définir hello Message = « données ».</span><span class="sxs-lookup"><span data-stu-id="115a9-278">Set hello Message='data'.</span></span> <span data-ttu-id="115a9-279">Ainsi, les erreurs de types hello du script de hello sera écrite toohello sortie d’erreur de build.</span><span class="sxs-lookup"><span data-stu-id="115a9-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="115a9-280">Corrigez toutes les erreurs, indiquées par des points d'exclamation bleus.</span><span class="sxs-lookup"><span data-stu-id="115a9-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="115a9-281">Placez le curseur sur le points d’exclamation tooget une indication de l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="115a9-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="115a9-282">Enregistrer le workflow hello pour effacer des erreurs.</span><span class="sxs-lookup"><span data-stu-id="115a9-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="115a9-283">résultat final de Hello Hello publier des activités doit ressembler à ceci dans le Concepteur de hello un flux de travail :</span><span class="sxs-lookup"><span data-stu-id="115a9-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Activités de workflow][5]

   <span data-ttu-id="115a9-285">résultat final de Hello Hello publier des flux de travail activités doit ressembler à ceci en XAML :</span><span class="sxs-lookup"><span data-stu-id="115a9-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="115a9-286">Enregistrer le workflow de modèle de processus de génération hello et archiver ce fichier.</span><span class="sxs-lookup"><span data-stu-id="115a9-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="115a9-287">Modifier la définition de build hello (fermer si elle est déjà ouverte) et sélectionnez hello **nouveau** bouton si vous ne voyez pas encore hello nouveau modèle dans hello liste des modèles de processus.</span><span class="sxs-lookup"><span data-stu-id="115a9-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="115a9-288">Définissez les valeurs de propriété de paramètre hello Bonjour section divers comme suit :</span><span class="sxs-lookup"><span data-stu-id="115a9-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="115a9-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Cette valeur est dérivée de : ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="115a9-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="115a9-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Cette valeur est dérivée de : ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="115a9-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="115a9-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="115a9-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="115a9-292">ServiceName = 'mycloudservicename' *utilisation hello approprié nom du service cloud ici*</span><span class="sxs-lookup"><span data-stu-id="115a9-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="115a9-293">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="115a9-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="115a9-294">StorageAccountName = 'mystorageaccountname' *utilisation hello approprié nom compte de stockage ici*</span><span class="sxs-lookup"><span data-stu-id="115a9-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="115a9-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="115a9-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="115a9-296">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="115a9-296">SubscriptionName = 'default'</span></span>

    ![Valeurs de propriétés des paramètres][6]
11. <span data-ttu-id="115a9-298">Enregistrer les modifications de hello toohello la définition de Build.</span><span class="sxs-lookup"><span data-stu-id="115a9-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="115a9-299">File d’attente d’un tooexecute de Build à la fois hello build du package et de publication.</span><span class="sxs-lookup"><span data-stu-id="115a9-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="115a9-300">Si vous avez un déclencheur défini tooContinuous intégration, vous allez exécuter ce comportement sur chaque archivage.</span><span class="sxs-lookup"><span data-stu-id="115a9-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="115a9-301">Modèle de script PublishCloudService.ps1</span><span class="sxs-lookup"><span data-stu-id="115a9-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="115a9-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="115a9-302">Next steps</span></span>
<span data-ttu-id="115a9-303">débogage distant tooenable lors de l’utilisation de la livraison continue, consultez [activer le débogage distant lors de l’utilisation de livraison continue toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="115a9-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
