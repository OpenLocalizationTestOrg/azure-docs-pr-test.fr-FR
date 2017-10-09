---
title: "livraison d’aaaContinuous avec Git et Visual Studio Team Services dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure votre Visual Studio Team Services projets d’équipe toouse Git tooautomatically générer et déployer des fonctionnalités de l’application Web toohello dans Azure App Service ou cloud services."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="bb0b4-103">TooAzure de livraison continue avec Visual Studio Team Services et Git</span><span class="sxs-lookup"><span data-stu-id="bb0b4-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="bb0b4-104">Vous pouvez utiliser toohost de projets d’équipe Visual Studio Team Services un référentiel Git de votre code source et automatiquement générer et déployer des applications web tooAzure ou services de cloud computing, chaque fois que vous effectuez un push un référentiel de toohello de validation.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="bb0b4-105">Vous aurez besoin de Visual Studio 2013 et hello Azure SDK est installé.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="bb0b4-106">Si vous ne disposez pas de Visual Studio 2013, téléchargez-le en choisissant hello **commencez gratuitement** lien [www.visualstudio.com](http://www.visualstudio.com). Installation Bonjour Azure SDK depuis [ici](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="bb0b4-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="bb0b4-107">Vous avez besoin une toocomplete de compte Visual Studio Team Services pour ce didacticiel : vous pouvez [ouvrir un compte Visual Studio Team Services gratuit](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="bb0b4-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="bb0b4-108">tooset d’un tooautomatically de service cloud générer et déployer tooAzure à l’aide de Visual Studio Team Services, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="bb0b4-109">1 : Création d'un référentiel Git</span><span class="sxs-lookup"><span data-stu-id="bb0b4-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="bb0b4-110">Si vous ne disposez pas de compte Visual Studio Team Services, vous pouvez en obtenir un [ici](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="bb0b4-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="bb0b4-111">Lorsque vous créez un projet d'équipe, choisissez Git comme système de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="bb0b4-112">Suivez le projet d’équipe tooyour hello instructions tooconnect Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="bb0b4-113">Dans **Team Explorer**, choisissez hello **cloner ce référentiel** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="bb0b4-114">Spécifier l’emplacement de hello de copie locale de hello, puis choisissez hello **Clone** bouton.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="bb0b4-115">2 : créer un projet et validez-la toohello référentiel</span><span class="sxs-lookup"><span data-stu-id="bb0b4-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="bb0b4-116">Dans **Team Explorer**, Bonjour **Solutions** , choisissez hello **nouveau** lien toocreate un nouveau projet dans le référentiel local de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="bb0b4-117">Vous pouvez déployer une application web ou un service cloud (Application Azure) par hello suivant les étapes dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="bb0b4-118">Créez un projet de service cloud Azure ou un projet MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="bb0b4-119">Assurez-vous que les cibles du projet hello hello .NET Framework 4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="bb0b4-120">Si vous créez un projet de service cloud, ajoutez un rôle web ASP.NET MVC et un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="bb0b4-121">Si vous souhaitez toocreate une application web, choisissez hello **Application Web ASP.NET** modèle de projet, puis choisissez **MVC**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="bb0b4-122">Pour plus d’informations, consultez la rubrique [Création d’une application web ASP.NET dans Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="bb0b4-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="bb0b4-123">Ouvrez le menu contextuel de hello pour la solution de hello, puis choisissez **valider**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="bb0b4-124">S’il s’agit hello première fois que vous utilisez Git dans Visual Studio Team Services, vous devez tooprovide tooidentify de certaines informations vous-même dans Git.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="bb0b4-125">Bonjour **modifications en attente** zone de **Team Explorer**, entrez votre nom d’utilisateur et votre adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="bb0b4-126">Entrez un commentaire pour la validation de hello, puis choisissez hello **validation** bouton.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="bb0b4-127">Notez hello options tooinclude ou exclure lorsque vous archivez des modifications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="bb0b4-128">Si hello modifications que vous souhaitez sont exclus, choisissez **tout inclure**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="bb0b4-129">Vous avez maintenant hello validée change dans votre copie locale du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="bb0b4-130">Ensuite, de synchroniser ces modifications avec le serveur de hello en choisissant hello **synchronisation** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="bb0b4-131">3 : connecter hello projet tooAzure</span><span class="sxs-lookup"><span data-stu-id="bb0b4-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="bb0b4-132">Maintenant que vous avez un référentiel Git dans Visual Studio Team Services avec du code source qu’il contient, vous êtes prêt tooconnect votre tooAzure de référentiel git.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="bb0b4-133">Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), sélectionnez votre cloud service ou une application web ou créez-en un en choisissant Bonjour + l’icône située en bas à gauche hello et en choisissant **Service Cloud** ou **Web App**, puis **création rapide**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="bb0b4-134">Pour les services de cloud, choisissez hello **configurer la publication avec Visual Studio Team Services** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="bb0b4-135">Pour les applications web, choisissez hello **configurer le déploiement à partir du contrôle de code source** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="bb0b4-136">Dans l’Assistant de hello, tapez le nom hello de votre compte Visual Studio Team Services dans la zone de texte hello et choisissez hello **autoriser maintenant** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="bb0b4-137">Vous pouvez être invité à toosign dans.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="bb0b4-138">Bonjour **demande de connexion** boîte de dialogue contextuelle, choisissez **accepter** tooauthorize tooconfigure Azure votre projet d’équipe dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="bb0b4-139">Si la procédure d’autorisation réussit, une zone déroulante affiche la liste de vos projets d’équipe Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="bb0b4-140">Sélectionnez Nom hello du projet d’équipe que vous avez créé dans les étapes précédentes hello et choisissez le bouton hello de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="bb0b4-141">Hello prochaine fois que vous effectuez un push un référentiel de tooyour de validation, Visual Studio Team Services générera et déploiera votre tooAzure du projet.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="bb0b4-142">4 : Déclenchement d'une régénération et redéploiement de votre projet</span><span class="sxs-lookup"><span data-stu-id="bb0b4-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="bb0b4-143">Dans Visual Studio, ouvrez un fichier et modifiez-le.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="bb0b4-144">Par exemple, modifiez le fichier de hello `_Layout.cshtml` sous hello affichages\\dossier partagé dans un rôle de web MVC.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="bb0b4-145">Modifier le texte de pied de page hello pour le site de hello et enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="bb0b4-146">Dans **l’Explorateur de solutions**, ouvrez le menu contextuel de hello hello nœud de la solution, le nœud de projet, hello fichier ou vous avez modifié, puis choisissez **valider**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="bb0b4-147">Tapez un commentaire et sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="bb0b4-148">Choisissez hello **synchronisation** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="bb0b4-149">Choisissez hello **Push** lien toopush votre référentiel toohello de validation dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="bb0b4-150">(Vous pouvez également utiliser hello **synchronisation** bouton toocopy votre référentiel toohello de validations.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="bb0b4-151">Hello différence est que **synchronisation** également extrait hello modifications les plus récentes à partir du référentiel de hello.)</span><span class="sxs-lookup"><span data-stu-id="bb0b4-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="bb0b4-152">Choisissez hello **domestique** bouton tooreturn toohello **Team Explorer** page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="bb0b4-153">Choisissez **génère** tooview hello les builds en cours.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="bb0b4-154">**Team Explorer** indique qu’une build est disponible pour archivage.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="bb0b4-155">tooview un journal détaillé que hello génération progresse, double-cliquez sur nom hello build hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="bb0b4-156">Lors de la génération de hello est en cours d’exécution, examiner une définition de build hello qui a été créée lorsque vous avez utilisé hello Assistant toolink tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="bb0b4-157">Ouvrez le menu contextuel de hello pour la définition de build hello et choisissez **modifier la définition de Build**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="bb0b4-158">Bonjour **déclencheur** onglet, vous verrez que définition de build hello a la valeur toobuild sur chaque archivage, par défaut.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="bb0b4-159">(Pour un service cloud, Visual Studio Team Services génère et déploie toohello de branche principale hello environnement intermédiaire automatiquement.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="bb0b4-160">Vous avez toujours toodo un site en direct toohello toodeploy étape manuelle.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="bb0b4-161">Pour une application web qui n’a pas environnement intermédiaire, il déploie branche principale de hello directement toohello live site.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="bb0b4-162">Bonjour **processus** onglet, vous pouvez voir d’un environnement de déploiement hello est défini nom toohello de votre application web ou de service de cloud.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="bb0b4-163">Spécifier des valeurs pour les propriétés de hello si vous souhaitez que les valeurs différentes de celles des valeurs par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="bb0b4-164">Hello propriétés pour la publication de Azure sont Bonjour **déploiement** section et vous devrez peut-être également tooset MSBuild paramètres.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="bb0b4-165">Par exemple, dans un projet de service cloud, toospecify une configuration de service autre que « Cloud », définissez hello MSbuild paramètres trop`/p:TargetProfile=[YourProfile]` où *[YourProfile]* correspond à un fichier de configuration de service avec un nom tel que ServiceConfiguration. *YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="bb0b4-166">Hello tableau suivant répertorie les propriétés disponibles hello dans hello **déploiement** section :</span><span class="sxs-lookup"><span data-stu-id="bb0b4-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="bb0b4-167">Propriété</span><span class="sxs-lookup"><span data-stu-id="bb0b4-167">Property</span></span> | <span data-ttu-id="bb0b4-168">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="bb0b4-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="bb0b4-169">Autoriser les certificats non approuvés</span><span class="sxs-lookup"><span data-stu-id="bb0b4-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="bb0b4-170">Si cette propriété a la valeur false, des certificats SSL doivent être signés par une autorité racine.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="bb0b4-171">Autoriser la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="bb0b4-171">Allow Upgrade</span></span> |<span data-ttu-id="bb0b4-172">Permet à un déploiement existant au lieu de créer un nouveau hello déploiement tooupdate.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="bb0b4-173">Conserve l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="bb0b4-174">Ne pas supprimer</span><span class="sxs-lookup"><span data-stu-id="bb0b4-174">Do Not Delete</span></span> |<span data-ttu-id="bb0b4-175">Si cette propriété a la valeur true, ne remplacez pas un déploiement sans rapport (la mise à niveau est autorisée).</span><span class="sxs-lookup"><span data-stu-id="bb0b4-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="bb0b4-176">Chemin d’accès tooDeployment paramètres</span><span class="sxs-lookup"><span data-stu-id="bb0b4-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="bb0b4-177">fichier de .pubxml tooyour Hello chemin d’accès pour une application web, dossier racine de toohello relatif de dépôt de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="bb0b4-178">Ignorée pour les services cloud.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="bb0b4-179">Environnement de déploiement SharePoint</span><span class="sxs-lookup"><span data-stu-id="bb0b4-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="bb0b4-180">Bonjour même en tant que nom de service hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="bb0b4-181">Environnement de déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="bb0b4-181">Azure Deployment Environment</span></span> |<span data-ttu-id="bb0b4-182">Hello cloud ou application nom du service web.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="bb0b4-183">À ce stade, la création de la build doit être terminée.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="bb0b4-184">Si vous double-cliquez sur le nom de la build hello, Visual Studio affiche un **résumé de la Build**, y compris les résultats des tests à partir d’associées des projets de test unitaire.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="bb0b4-185">Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez afficher le déploiement de hello associé sur hello **déploiements** onglet lorsque hello environnement intermédiaire est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="bb0b4-186">Parcourir les URL du site tooyour.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="bb0b4-187">Pour une application web, choisissez simplement hello **Parcourir** bouton dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="bb0b4-188">Pour un service cloud, choisissez hello URL Bonjour **aperçu rapide** section Hello **tableau de bord** page qui affiche l’environnement intermédiaire de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="bb0b4-189">Les déploiements à partir de l’intégration continue pour les services cloud sont environnement intermédiaire de toohello publié par défaut.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="bb0b4-190">Vous pouvez le modifier en définissant les hello **autre environnement de Service Cloud** propriété trop**Production**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="bb0b4-191">Voici où les URL du site hello est sur la page du tableau de bord du service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="bb0b4-192">Un nouvel onglet de navigateur s’ouvre tooreveal votre site en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="bb0b4-193">Si vous apportez des autres modifications tooyour projet vous déclencheur génère plus et vous vont s’accumuler plusieurs déploiements.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="bb0b4-194">Hello dernière une est marquée comme Active.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="bb0b4-195">5 : Redéploiement d'une build antérieure</span><span class="sxs-lookup"><span data-stu-id="bb0b4-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="bb0b4-196">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-196">This step is optional.</span></span> <span data-ttu-id="bb0b4-197">Hello portail Azure classic, choisissez un précédent déploiement et choisissez **redéployer** toorewind votre tooan site précédemment archivage.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="bb0b4-198">Notez que cela déclenche une nouvelle génération dans TFS et crée une entrée dans l’historique de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="bb0b4-199">6 : modifier le déploiement de Production hello</span><span class="sxs-lookup"><span data-stu-id="bb0b4-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="bb0b4-200">Lorsque vous êtes prêt, vous pouvez promouvoir hello intermédiaire toohello environnement de Production en choisissant **échanger** Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="bb0b4-201">environnement d’intermédiaire Hello nouvellement déployé est promue tooProduction et environnement de Production précédent hello, le cas échéant, devient un environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="bb0b4-202">Hello déploiement actif peut être différente pour hello Production et les environnements de préproduction, mais l’historique de déploiement hello des builds récentes est hello même indépendamment de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="bb0b4-203">7 : Déploiement à partir d’une branche en cours d’utilisation</span><span class="sxs-lookup"><span data-stu-id="bb0b4-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="bb0b4-204">Lorsque vous utilisez Git, vous généralement apportez des modifications dans une branche de travail et s’intégrer dans la branche principale de hello lorsque votre développement atteint un état terminé.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="bb0b4-205">Pendant la phase de développement hello d’un projet, vous souhaitez toobuild et déployer tooAzure de branche de travail hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="bb0b4-206">Dans **Team Explorer**, choisissez hello **accueil** bouton, puis choisissez hello **Branches** bouton.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="bb0b4-207">Choisissez hello **nouvelle branche** lien.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="bb0b4-208">Entrez le nom hello de branche hello, tels que « working », puis choisissez **créer une branche**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="bb0b4-209">pour créer une branche locale.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="bb0b4-210">Publier la branche de hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-210">Publish hello branch.</span></span> <span data-ttu-id="bb0b4-211">Choisissez le nom de la branche hello dans **Unpublished branches**, puis choisissez **publier**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="bb0b4-212">Par défaut, modifie uniquement le déclencheur de branche principale toohello une build en continu.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="bb0b4-213">tooset de build en continu pour une branche de travail, choisissez hello **génère** page **Team Explorer**, puis choisissez **modifier la définition de Build**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="bb0b4-214">Ouvrez hello **paramètres Source** onglet. Sous **analysé les branches pour l’intégration continue et build**, choisissez **cliquez ici tooadd une nouvelle ligne**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="bb0b4-215">Spécifiez la branche hello créé, tels que refs/têtes/travail.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="bb0b4-216">Apportez une modification dans le code hello, fichier hello modifié sur le menu contextuel hello ouvrir, puis choisissez **valider**.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="bb0b4-217">Choisissez hello **validations non synchronisées** la liaison et choisissez hello **synchronisation** bouton ou hello **Push** hello toocopy de lien change copie toohello de branche de travail hello dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="bb0b4-218">Accédez toohello **génère** afficher et rechercher build hello déclenchant simplement obtenu pour la branche de travail hello.</span><span class="sxs-lookup"><span data-stu-id="bb0b4-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb0b4-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb0b4-219">Next steps</span></span>
<span data-ttu-id="bb0b4-220">consultez d’autres conseils sur l’utilisation de Git avec Visual Studio Team Services, toolearn [développer et partager votre code dans Git, à l’aide de Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) et pour plus d’informations sur l’utilisation d’un référentiel Git qui n’est pas géré par toopublish de Visual Studio Team Services tooAzure, consultez [tooAzure de déploiement continu du Service d’applications](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="bb0b4-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="bb0b4-221">Pour en savoir plus sur Visual Studio Team Services, consultez [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="bb0b4-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
