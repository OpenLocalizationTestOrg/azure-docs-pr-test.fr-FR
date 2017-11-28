---
title: "livraison d’aaaContinuous avec Visual Studio Team Services dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure votre Visual Studio Team Services projets d’équipe tooautomatically générer et déployer des fonctionnalités de l’application Web toohello dans Azure App Service ou cloud services."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="3b015-103">TooAzure de livraison continue à l’aide de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="3b015-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="3b015-104">Vous pouvez configurer votre build tooautomatically Visual Studio Team Services les projets d’équipe et déployer des applications web tooAzure ou services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="3b015-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="3b015-105">(Pour plus d’informations sur comment tooset une build en continu et la déployer à l’aide du système une *local* Team Foundation Server, consultez [livraison continue pour les Services de Cloud dans Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="3b015-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="3b015-106">Ce didacticiel suppose que vous avez Visual Studio 2013 et hello Azure SDK est installé.</span><span class="sxs-lookup"><span data-stu-id="3b015-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="3b015-107">Si vous ne disposez pas de Visual Studio 2013, téléchargez-le en choisissant hello **commencez gratuitement** lien [www.visualstudio.com](http://www.visualstudio.com). Installation Bonjour Azure SDK depuis [ici](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="3b015-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="3b015-108">Vous avez besoin une toocomplete de compte Visual Studio Team Services pour ce didacticiel : vous pouvez [ouvrir un compte Visual Studio Team Services gratuit](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="3b015-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="3b015-109">tooset d’un tooautomatically de service cloud générer et déployer tooAzure à l’aide de Visual Studio Team Services, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="3b015-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="3b015-110">1 : Création d'un projet d'équipe</span><span class="sxs-lookup"><span data-stu-id="3b015-110">1: Create a team project</span></span>
<span data-ttu-id="3b015-111">Suivez les instructions de hello [ici](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate votre équipe de projet et le lier tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b015-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="3b015-112">Cette procédure pas à pas part du principe que vous utilisez TFVC (Team Foundation Version Control) en tant que solution de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="3b015-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="3b015-113">Si vous souhaitez toouse Git pour le contrôle de version, consultez [version de Git hello de cette procédure pas à pas](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="3b015-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="3b015-114">2 : vérifier dans un contrôle toosource de projet</span><span class="sxs-lookup"><span data-stu-id="3b015-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="3b015-115">Dans Visual Studio, ouvrez solution hello vous souhaitez toodeploy ou créez un.</span><span class="sxs-lookup"><span data-stu-id="3b015-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="3b015-116">Vous pouvez déployer une application web ou un service cloud (Application Azure) par hello suivant les étapes dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="3b015-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="3b015-117">Si vous souhaitez toocreate une nouvelle solution, créez un nouveau projet de Service Cloud Azure, ou un nouveau projet ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="3b015-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="3b015-118">Assurez-vous que hello projet cible .NET Framework 4 ou 4.5 et si vous créez un projet de service cloud, ajoutez un rôle web d’ASP.NET MVC et un rôle de travail et choisissez l’application Internet pour un rôle web de hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="3b015-119">Lorsque vous y êtes invité, choisissez **Application Internet**.</span><span class="sxs-lookup"><span data-stu-id="3b015-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="3b015-120">Si vous souhaitez toocreate une application web, choisissez le modèle de projet d’Application Web ASP.NET hello, puis MVC.</span><span class="sxs-lookup"><span data-stu-id="3b015-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="3b015-121">Consultez la rubrique [Création d’une application Web ASP.NET dans Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3b015-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3b015-122">Actuellement, Visual Studio Team Services ne prend en charge que les déploiements CI des applications web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b015-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="3b015-123">Les projets de site web n’entrent pas dans ce cadre.</span><span class="sxs-lookup"><span data-stu-id="3b015-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="3b015-124">Ouvrez le menu contextuel de hello pour la solution de hello, puis choisissez **tooSource d’ajouter la Solution contrôle**.</span><span class="sxs-lookup"><span data-stu-id="3b015-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="3b015-125">Accepter ou modifier les valeurs par défaut hello et choisissez hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="3b015-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="3b015-126">Une fois que la fin du processus de hello, les icônes de contrôle de code source s’affichent dans **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="3b015-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="3b015-127">Ouvrez le menu contextuel de hello pour la solution de hello, puis choisissez **archiver**.</span><span class="sxs-lookup"><span data-stu-id="3b015-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="3b015-128">Bonjour **modifications en attente** zone de **Team Explorer**, tapez un commentaire d’archivage hello et choisissez hello **archiver** bouton.</span><span class="sxs-lookup"><span data-stu-id="3b015-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="3b015-129">Notez hello options tooinclude ou exclure lorsque vous archivez des modifications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3b015-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="3b015-130">Si vous le souhaitez modifications sont exclues, choisissez hello **tout inclure** lien.</span><span class="sxs-lookup"><span data-stu-id="3b015-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="3b015-131">3 : connecter hello projet tooAzure</span><span class="sxs-lookup"><span data-stu-id="3b015-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="3b015-132">Maintenant que vous avez un projet d’équipe Visual Studio Team Services avec du code source qu’il contient, vous êtes prêt tooconnect votre projet d’équipe tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3b015-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="3b015-133">Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), sélectionnez votre cloud service ou une application web ou créez-en un en choisissant hello  **+**  icône située en bas à gauche hello et en choisissant **leServiceCloud** ou **application Web** , puis **création rapide**.</span><span class="sxs-lookup"><span data-stu-id="3b015-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="3b015-134">Choisissez hello **configurer la publication avec Visual Studio Team Services** lien.</span><span class="sxs-lookup"><span data-stu-id="3b015-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="3b015-135">Dans l’Assistant de hello, tapez le nom hello de votre compte Visual Studio Team Services dans la zone de texte hello et cliquez sur hello **autoriser maintenant** lien.</span><span class="sxs-lookup"><span data-stu-id="3b015-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="3b015-136">Vous pouvez être invité à toosign dans.</span><span class="sxs-lookup"><span data-stu-id="3b015-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="3b015-137">Bonjour **demande de connexion** boîte de dialogue contextuelle, choisissez hello **accepter** bouton tooauthorize tooconfigure Azure votre projet d’équipe dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3b015-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="3b015-138">Si le processus d'autorisation aboutit, une zone déroulante affiche une liste de vos projets Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3b015-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="3b015-139">Choisissez le nom de hello du projet d’équipe que vous avez créé dans les étapes précédentes hello, puis coche hello de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="3b015-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="3b015-140">Une fois que votre projet est lié, vous verrez des instructions relatives à la vérification dans le projet d’équipe de modifications tooyour Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3b015-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="3b015-141">Sur votre prochain archivage, Visual Studio Team Services générera et déploiera votre tooAzure du projet.</span><span class="sxs-lookup"><span data-stu-id="3b015-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="3b015-142">Essayez cette maintenant en cliquant sur hello **archiver à partir de Visual Studio** lier, puis hello **lancer Visual Studio** lien (ou équivalent de hello **Visual Studio** bouton bas hello écran portail Hello).</span><span class="sxs-lookup"><span data-stu-id="3b015-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="3b015-143">4 : Déclenchement d'une régénération et redéploiement de votre projet</span><span class="sxs-lookup"><span data-stu-id="3b015-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="3b015-144">Dans Visual Studio **Team Explorer**, choisissez hello **Explorateur du contrôle de code Source** lien.</span><span class="sxs-lookup"><span data-stu-id="3b015-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="3b015-145">Parcourir le fichier de solution tooyour et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="3b015-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="3b015-146">Dans l' **Explorateur de solutions**, ouvrez un fichier et modifiez-le.</span><span class="sxs-lookup"><span data-stu-id="3b015-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="3b015-147">Par exemple, modifiez le fichier de hello `_Layout.cshtml` sous hello affichages\\dossier partagé dans un rôle de web MVC.</span><span class="sxs-lookup"><span data-stu-id="3b015-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="3b015-148">Modifier le logo hello pour le site de hello, puis choisissez **Ctrl + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="3b015-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="3b015-149">Dans **Team Explorer**, choisissez hello **modifications en attente** lien.</span><span class="sxs-lookup"><span data-stu-id="3b015-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="3b015-150">Entrez un commentaire, puis choisissez hello **archiver** bouton.</span><span class="sxs-lookup"><span data-stu-id="3b015-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="3b015-151">Choisissez hello **domestique** bouton tooreturn toohello **Team Explorer** page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="3b015-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="3b015-152">Choisissez hello **génère** hello tooview de lien les builds en cours.</span><span class="sxs-lookup"><span data-stu-id="3b015-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="3b015-153">**Team Explorer** indique qu’une build est disponible pour archivage.</span><span class="sxs-lookup"><span data-stu-id="3b015-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="3b015-154">Double-cliquez sur nom hello de build hello dans progression tooview un journal détaillé fur hello et build.</span><span class="sxs-lookup"><span data-stu-id="3b015-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="3b015-155">Lors de la génération de hello est en cours d’exécution, examiner une définition de build hello qui a été créée lorsque vous avez lié tooAzure TFS à l’aide d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="3b015-156">Ouvrez le menu contextuel de hello pour la définition de build hello et choisissez **modifier la définition de Build**.</span><span class="sxs-lookup"><span data-stu-id="3b015-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="3b015-157">Bonjour **déclencheur** onglet, vous verrez que définition de build hello a la valeur toobuild sur chaque archivage par défaut.</span><span class="sxs-lookup"><span data-stu-id="3b015-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="3b015-158">Bonjour **processus** onglet, vous pouvez voir d’un environnement de déploiement hello est défini nom toohello de votre application web ou de service de cloud.</span><span class="sxs-lookup"><span data-stu-id="3b015-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="3b015-159">Si vous travaillez avec des applications web, propriétés hello que vous voyez sera différentes de celles présentées ici.</span><span class="sxs-lookup"><span data-stu-id="3b015-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="3b015-160">Spécifier des valeurs pour les propriétés de hello si vous souhaitez que les valeurs différentes de celles des valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="3b015-161">Hello propriétés pour la publication de Azure sont Bonjour **déploiement** section.</span><span class="sxs-lookup"><span data-stu-id="3b015-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="3b015-162">Hello tableau suivant répertorie les propriétés disponibles hello dans hello **déploiement** section :</span><span class="sxs-lookup"><span data-stu-id="3b015-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="3b015-163">Propriété</span><span class="sxs-lookup"><span data-stu-id="3b015-163">Property</span></span> | <span data-ttu-id="3b015-164">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="3b015-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3b015-165">Autoriser les certificats non approuvés</span><span class="sxs-lookup"><span data-stu-id="3b015-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="3b015-166">Si cette propriété a la valeur false, des certificats SSL doivent être signés par une autorité racine.</span><span class="sxs-lookup"><span data-stu-id="3b015-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="3b015-167">Autoriser la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="3b015-167">Allow Upgrade</span></span> |<span data-ttu-id="3b015-168">Permet à un déploiement existant au lieu de créer un nouveau hello déploiement tooupdate.</span><span class="sxs-lookup"><span data-stu-id="3b015-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="3b015-169">Conserve l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="3b015-170">Ne pas supprimer</span><span class="sxs-lookup"><span data-stu-id="3b015-170">Do Not Delete</span></span> |<span data-ttu-id="3b015-171">Si cette propriété a la valeur true, ne remplacez pas un déploiement sans rapport (la mise à niveau est autorisée).</span><span class="sxs-lookup"><span data-stu-id="3b015-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="3b015-172">Chemin d’accès tooDeployment paramètres</span><span class="sxs-lookup"><span data-stu-id="3b015-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="3b015-173">fichier de .pubxml tooyour Hello chemin d’accès pour une application web, dossier racine de toohello relatif de dépôt de hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="3b015-174">Ignorée pour les services cloud.</span><span class="sxs-lookup"><span data-stu-id="3b015-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="3b015-175">Environnement de déploiement SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b015-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="3b015-176">Bonjour même en tant que nom de service hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="3b015-177">Environnement de déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="3b015-177">Azure Deployment Environment</span></span> |<span data-ttu-id="3b015-178">Hello cloud ou application nom du service web.</span><span class="sxs-lookup"><span data-stu-id="3b015-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="3b015-179">Si vous utilisez plusieurs configurations de service (fichiers .cscfg), vous pouvez spécifier la configuration de service désiré hello Bonjour **arguments de Build, Avancé, MSBuild** paramètre.</span><span class="sxs-lookup"><span data-stu-id="3b015-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="3b015-180">Par exemple, toouse ServiceConfiguration.Test.cscfg, définissez les arguments MSBuild option de ligne de `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="3b015-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="3b015-181">À ce stade, la création de la build doit être terminée.</span><span class="sxs-lookup"><span data-stu-id="3b015-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="3b015-182">Si vous double-cliquez sur le nom de la build hello, Visual Studio affiche un **résumé de la Build**, y compris les résultats des tests à partir d’associées des projets de test unitaire.</span><span class="sxs-lookup"><span data-stu-id="3b015-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="3b015-183">Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez afficher le déploiement de hello associé sur hello **déploiements** onglet lorsque hello environnement intermédiaire est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="3b015-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="3b015-184">Parcourir les URL du site tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b015-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="3b015-185">Pour une application web, cliquez sur hello **Parcourir** bouton de barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="3b015-186">Pour un service cloud, choisissez hello URL Bonjour **aperçu rapide** section Hello **tableau de bord** page qui affiche l’environnement intermédiaire de hello pour un service cloud.</span><span class="sxs-lookup"><span data-stu-id="3b015-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="3b015-187">Les déploiements à partir de l’intégration continue pour les services cloud sont environnement intermédiaire de toohello publié par défaut.</span><span class="sxs-lookup"><span data-stu-id="3b015-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="3b015-188">Vous pouvez le modifier en définissant les hello **autre environnement de Service Cloud** propriété trop**Production**.</span><span class="sxs-lookup"><span data-stu-id="3b015-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="3b015-189">Cette capture d’écran montre où hello QU'URL du site se trouve sur la page du tableau de bord du service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="3b015-190">Un nouvel onglet de navigateur s’ouvre tooreveal votre site en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3b015-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="3b015-191">Services de cloud computing, si vous apportez d’autres projets tooyour de modifications, vous déclencheur génère plus et vous vont s’accumuler plusieurs déploiements.</span><span class="sxs-lookup"><span data-stu-id="3b015-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="3b015-192">Hello version la plus récente marquée comme Active.</span><span class="sxs-lookup"><span data-stu-id="3b015-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="3b015-193">5 : Redéploiement d'une build antérieure</span><span class="sxs-lookup"><span data-stu-id="3b015-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="3b015-194">Cette étape s’applique toocloud services et est facultative.</span><span class="sxs-lookup"><span data-stu-id="3b015-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="3b015-195">Dans hello portail Azure classic, choisissez un précédent déploiement, puis hello **redéployer** bouton toorewind votre tooan site précédemment archivage.</span><span class="sxs-lookup"><span data-stu-id="3b015-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="3b015-196">Notez que cela déclenche une nouvelle génération dans TFS et crée une entrée dans l’historique de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="3b015-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="3b015-197">6 : modifier le déploiement de Production hello</span><span class="sxs-lookup"><span data-stu-id="3b015-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="3b015-198">Cette étape s’applique uniquement les services toocloud, pas les applications web.</span><span class="sxs-lookup"><span data-stu-id="3b015-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="3b015-199">Lorsque vous êtes prêt, vous pouvez promouvoir hello intermédiaire toohello environnement de production en choisissant hello **échanger** bouton Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="3b015-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="3b015-200">environnement d’intermédiaire Hello nouvellement déployé est promue tooProduction et environnement de Production précédent hello, le cas échéant, devient un environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="3b015-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="3b015-201">Hello déploiement actif peut être différente pour hello Production et les environnements de préproduction, mais l’historique de déploiement hello des builds récentes est hello même indépendamment de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="3b015-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="3b015-202">7 : Exécution de tests unitaires</span><span class="sxs-lookup"><span data-stu-id="3b015-202">7: Run unit tests</span></span>
<span data-ttu-id="3b015-203">Cette étape s’applique uniquement les applications tooweb, pas les services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="3b015-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="3b015-204">tooput une porte de la qualité de votre déploiement, vous pouvez exécuter des tests unitaires et si elles échouent, vous pouvez arrêter le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="3b015-205">Dans Visual Studio, ajoutez un projet de test unitaire.</span><span class="sxs-lookup"><span data-stu-id="3b015-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="3b015-206">Ajoutez le projet références toohello projet tootest.</span><span class="sxs-lookup"><span data-stu-id="3b015-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="3b015-207">Ajoutez quelques tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="3b015-207">Add some unit tests.</span></span> <span data-ttu-id="3b015-208">tooget démarré, essayez un test factice qui passera toujours.</span><span class="sxs-lookup"><span data-stu-id="3b015-208">tooget started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="3b015-209">Modifier la définition de build hello, choisissez hello **processus** onglet et développez hello **Test** nœud.</span><span class="sxs-lookup"><span data-stu-id="3b015-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="3b015-210">Ensemble hello **faire échouer la build en cas d’échec du test** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="3b015-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="3b015-211">Cela signifie que le déploiement de hello n’aura pas lieu, sauf si les tests hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="3b015-212">Placez une nouvelle build dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="3b015-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="3b015-213">Lors de la génération de hello se poursuit, vérifier sa progression.</span><span class="sxs-lookup"><span data-stu-id="3b015-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="3b015-214">Lors de la génération de hello est terminée, vérifiez les résultats des tests hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="3b015-215">Essayez de créer un nouveau test qui échouera.</span><span class="sxs-lookup"><span data-stu-id="3b015-215">Try creating a test that will fail.</span></span> <span data-ttu-id="3b015-216">Ajouter un nouveau test en copiant hello premier, renommez-la et commentez la ligne hello de code qui déclare que NotImplementedException est une exception attendue.</span><span class="sxs-lookup"><span data-stu-id="3b015-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="3b015-217">Hello modification tooqueue archivez une nouvelle build.</span><span class="sxs-lookup"><span data-stu-id="3b015-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="3b015-218">Vue hello toosee détails des résultats sur les échecs de hello.</span><span class="sxs-lookup"><span data-stu-id="3b015-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="3b015-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b015-219">Next steps</span></span>
<span data-ttu-id="3b015-220">Pour en savoir plus sur le test unitaire dans Visual Studio Team Services, consultez [Exécuter des tests unitaires dans votre build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="3b015-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="3b015-221">Si vous utilisez Git, consultez [partager votre code dans Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) et [tooAzure de déploiement continu du Service d’applications](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3b015-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="3b015-222">Pour en savoir plus sur Visual Studio Team Services, consultez [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="3b015-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
