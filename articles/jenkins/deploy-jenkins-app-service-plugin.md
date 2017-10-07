---
title: "aaaDeploy tooAzure du Service d’applications avec Jenkins Plugin | Documents Microsoft"
description: "Découvrez comment toodeploy de plug-in Azure App Service Jenkins toouse Java web tooAzure app dans Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="e4592-103">Déployer tooAzure du Service d’applications avec le plug-in de Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="e4592-104">toodeploy un tooAzure d’application web Java, vous pouvez utiliser CLI d’Azure dans [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) ou vous pouvez utiliser de hello [plug-in Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="e4592-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="e4592-105">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4592-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4592-106">Configurer Jenkins toodeploy tooAzure du Service d’applications via FTP</span><span class="sxs-lookup"><span data-stu-id="e4592-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="e4592-107">Configurer Jenkins toodeploy tooAzure du Service d’applications sur Linux avec Docker</span><span class="sxs-lookup"><span data-stu-id="e4592-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="e4592-108">Créer et configurer l’instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="e4592-109">Si vous n’avez pas déjà un maître de Jenkins, commencer par hello [modèle de Solution](install-jenkins-solution-template.md), ce qui inclut JDK8 et hello suivant plug-ins requis :</span><span class="sxs-lookup"><span data-stu-id="e4592-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="e4592-110">[Plug-in du client Git Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="e4592-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="e4592-111">[Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="e4592-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="e4592-112">[Informations d’identification Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="e4592-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="e4592-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="e4592-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="e4592-114">Vous pouvez utiliser hello toodeploy de plug-in du Service d’applications Web App dans toutes les langues (par exemple, c#, PHP, Java et node.js, etc.) sont pris en charge par le Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="e4592-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="e4592-115">Dans ce didacticiel, nous utilisons hello exemple d’application Java, [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="e4592-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="e4592-116">toofork hello référentiel tooyour propre compte GitHub, cliquez sur hello **branchement** bouton dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="e4592-117">Java JDK et Maven sont requis pour la création de projet de Java hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="e4592-118">Veillez à qu'installer les composants hello dans master de Jenkins hello ou agent de machine virtuelle hello si vous utilisez un seul pour l’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="e4592-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="e4592-119">tooinstall, connectez-vous en instance de Jenkins toohello à l’aide de SSH et exécutez hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="e4592-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="e4592-120">Pour le déploiement de tooApp Service sur Linux, vous devez également tooinstall Docker sur master de Jenkins hello ou un agent de machine virtuelle hello utilisé pour la build.</span><span class="sxs-lookup"><span data-stu-id="e4592-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="e4592-121">Consultez l’article de toothis tooinstall Docker : https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="e4592-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="e4592-122">Ajouter des informations d’identification de service Azure principal tooJenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="e4592-123">Un principal du service Azure est nécessaire toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e4592-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="e4592-124">Utilisez [CLI d’Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ou [portail Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="e4592-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="e4592-125">Dans le tableau de bord hello Jenkins, cliquez sur **informations d’identification -> système ->**.</span><span class="sxs-lookup"><span data-stu-id="e4592-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="e4592-126">Cliquez sur **Informations d’identification globales (sans restriction)**.</span><span class="sxs-lookup"><span data-stu-id="e4592-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="e4592-127">Cliquez sur **ajouter les informations d’identification** tooadd un principal de service Microsoft Azure en remplissant hello ID d’abonnement, ID de Client, question secrète du Client et OAuth 2.0 Token Endpoint.</span><span class="sxs-lookup"><span data-stu-id="e4592-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="e4592-128">Fournissez l’ID, **mySp**, à utiliser dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="e4592-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="e4592-129">Plug-in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e4592-129">Azure App Service plugin</span></span>

<span data-ttu-id="e4592-130">V1.0 de plug-in du Service d’applications Azure prend en charge le déploiement continu tooAzure application Web via :</span><span class="sxs-lookup"><span data-stu-id="e4592-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="e4592-131">Git et FTP</span><span class="sxs-lookup"><span data-stu-id="e4592-131">Git and FTP</span></span>
* <span data-ttu-id="e4592-132">Docker pour application web sur Linux</span><span class="sxs-lookup"><span data-stu-id="e4592-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="e4592-133">Configurer Jenkins toodeploy application Web via FTP à l’aide du tableau de bord hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="e4592-134">toodeploy votre tooAzure de project Web App, vous pouvez télécharger vos artefacts de build (par exemple, les fichier .war dans Java) à l’aide de Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="e4592-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="e4592-135">Avant de configurer la tâche hello dans Jenkins, vous devez un plan de Service d’applications Azure et une application Web pour l’application de Java hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e4592-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="e4592-136">Créer un plan de Service d’application Azure avec hello **libre** tarification à l’aide de hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande CLI.</span><span class="sxs-lookup"><span data-stu-id="e4592-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="e4592-137">un plan de Hello définit hello ressources physiques utilisées toohost vos applications.</span><span class="sxs-lookup"><span data-stu-id="e4592-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="e4592-138">Toutes les applications affectées tooan un plan de partagent ces ressources, ce qui vous toosave coût lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="e4592-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="e4592-139">Créez une application web.</span><span class="sxs-lookup"><span data-stu-id="e4592-139">Create a Web App.</span></span> <span data-ttu-id="e4592-140">Vous pouvez soit hello utilisation [portail Azure](/azure/app-service-web/web-sites-configure) ou utilisez hello suit commande Az CLI :</span><span class="sxs-lookup"><span data-stu-id="e4592-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="e4592-141">Assurez-vous que vous définissez configuration hello Java runtime dont votre application a besoin.</span><span class="sxs-lookup"><span data-stu-id="e4592-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="e4592-142">Hello suivant commande CLI d’Azure configure hello web application toorun sur une récente Java JDK de 8 et [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="e4592-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="e4592-143">Configurer la tâche de Jenkins hello</span><span class="sxs-lookup"><span data-stu-id="e4592-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="e4592-144">Créer un nouveau projet **freestyle** dans le tableau de bord Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="e4592-145">Configurer **gestion du Code Source** toouse votre branche local de [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) en fournissant hello **URL du référentiel**.</span><span class="sxs-lookup"><span data-stu-id="e4592-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="e4592-146">Par exemple : http://github.com/&lt;votreID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="e4592-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="e4592-147">Ajoutez un projet de hello Build étape toobuild à l’aide de Maven.</span><span class="sxs-lookup"><span data-stu-id="e4592-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="e4592-148">Pour ce faire, ajoutez une étape **Exécuter un interpréteur de commandes**.</span><span class="sxs-lookup"><span data-stu-id="e4592-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="e4592-149">Pour cet exemple, nous avons besoin d’un fichier étape supplémentaire toorename hello *.war dans tooROOT.war du dossier cible.</span><span class="sxs-lookup"><span data-stu-id="e4592-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="e4592-150">Ajoutez une action post-build en sélectionnant **Publier une application web Azure**.</span><span class="sxs-lookup"><span data-stu-id="e4592-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="e4592-151">Approvisionnement, « mySp » principal du service Azure hello stockées dans l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="e4592-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="e4592-152">Dans **Configuration de l’application** , choisissez hello ressource groupe et l’application web dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e4592-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="e4592-153">plug-in Hello détecte automatiquement si hello application Web est Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="e4592-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="e4592-154">Pour une application Web basée sur Windows, l’option hello « Publier les fichiers » est présentée.</span><span class="sxs-lookup"><span data-stu-id="e4592-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="e4592-155">Remplir dans les fichiers de hello souhaité toodeploy (par exemple, un war package si vous utilisez Java.) Les répertoires source et cible sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="e4592-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="e4592-156">paramètres de Hello permettent les dossiers source et cible toospecify lors du téléchargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="e4592-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="e4592-157">L’application web Java sur Azure est exécutée sur un serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e4592-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="e4592-158">Ainsi, vous chargez votre package war dans le dossier webapps.</span><span class="sxs-lookup"><span data-stu-id="e4592-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="e4592-159">Pour cet exemple, définissez **répertoire Source** trop « cible » et fournir des applications « Web » pour **répertoire cible**.</span><span class="sxs-lookup"><span data-stu-id="e4592-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="e4592-160">Si vous souhaitez que le connecteur de tooa toodeploy autre que de production, vous pouvez également définir **emplacement** nom.</span><span class="sxs-lookup"><span data-stu-id="e4592-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="e4592-161">Enregistrer le projet de hello et générez-le.</span><span class="sxs-lookup"><span data-stu-id="e4592-161">Save hello project and build it.</span></span> <span data-ttu-id="e4592-162">Votre application web est déployée tooAzure lors de la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="e4592-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="e4592-163">Déployer l’application Web via FTP à l’aide du pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="e4592-164">plug-in Hello est compatible avec le pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4592-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="e4592-165">Vous pouvez consulter l’exemple tooa dans le référentiel GitHub de hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="e4592-166">Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="e4592-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="e4592-167">Cliquez sur hello crayon icône tooedit ce groupe de ressources de fichier tooupdate hello et le nom de votre application web sur la ligne 11 et 12 respectivement.</span><span class="sxs-lookup"><span data-stu-id="e4592-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="e4592-168">Modifier la ligne 14 tooupdate d’identification de votre instance de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e4592-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="e4592-169">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="e4592-170">Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="e4592-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="e4592-171">Fournissez un nom pour le travail de hello et sélectionnez **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e4592-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="e4592-172">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4592-172">Click **OK**.</span></span>
3. <span data-ttu-id="e4592-173">Cliquez sur hello **Pipeline** onglet suivant.</span><span class="sxs-lookup"><span data-stu-id="e4592-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="e4592-174">Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.</span><span class="sxs-lookup"><span data-stu-id="e4592-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="e4592-175">Pour **SCM**, sélectionnez **Git**.</span><span class="sxs-lookup"><span data-stu-id="e4592-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="e4592-176">Entrez hello GitHub URL pour votre référentiel RAMIFIÉ : https :&lt;votre dépôt RAMIFIÉ > .git</span><span class="sxs-lookup"><span data-stu-id="e4592-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="e4592-177">Mise à jour **chemin d’accès du Script** trop « Jenkinsfile_ftp_plugin »</span><span class="sxs-lookup"><span data-stu-id="e4592-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="e4592-178">Cliquez sur **enregistrer** et la tâche d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="e4592-179">Configurer Jenkins toodeploy application Web sur Linux avec Docker</span><span class="sxs-lookup"><span data-stu-id="e4592-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="e4592-180">Outre Git/FTP, l’application web sur Linux prend en charge le déploiement à l’aide de Docker.</span><span class="sxs-lookup"><span data-stu-id="e4592-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="e4592-181">toodeploy à l’aide de Docker, vous devez tooprovide un fichier Dockerfile par les packages de votre application web avec le runtime du service dans une image docker.</span><span class="sxs-lookup"><span data-stu-id="e4592-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="e4592-182">Plug-in hello génère des images de hello, il transmet le Registre de docker tooa, puis déploie l’application web de hello image tooyour.</span><span class="sxs-lookup"><span data-stu-id="e4592-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="e4592-183">L’application web sur Linux prend également en charge les méthodes traditionnelles telles que Git et FTP, mais uniquement pour les langages intégrés (.NET Core, Node.js, PHP et Ruby).</span><span class="sxs-lookup"><span data-stu-id="e4592-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="e4592-184">Pour d’autres langues, vous devez toopackage votre exécution de code et le service de l’application ensemble dans une image docker et utilisez docker toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e4592-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="e4592-185">Avant de configurer la tâche hello dans Jenkins, vous devez un service d’application Azure sur Linux.</span><span class="sxs-lookup"><span data-stu-id="e4592-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="e4592-186">Un Registre de conteneur est également nécessaire toostore et gérer vos images de conteneur Docker privés.</span><span class="sxs-lookup"><span data-stu-id="e4592-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="e4592-187">Vous pouvez utiliser DockerHub ; nous utilisons Azure Container Registry pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="e4592-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="e4592-188">Vous pouvez suivre les étapes de hello [ici](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate une application Web sur Linux</span><span class="sxs-lookup"><span data-stu-id="e4592-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="e4592-189">Registre de conteneur Azure est géré [Docker Registre] service (https://docs.docker.com/registry/) en fonction de hello 2.0 de Registre Docker open source.</span><span class="sxs-lookup"><span data-stu-id="e4592-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="e4592-190">Suivez les étapes de hello [ici] (/ azure/container-registry/container-registry-get-started-azure-cli) pour plus d’informations sur la façon de toodo donc.</span><span class="sxs-lookup"><span data-stu-id="e4592-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="e4592-191">Vous pouvez également utiliser DockerHub.</span><span class="sxs-lookup"><span data-stu-id="e4592-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="e4592-192">toodeploy à l’aide de docker :</span><span class="sxs-lookup"><span data-stu-id="e4592-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="e4592-193">Créez un nouveau projet freestyle dans le tableau de bord Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e4592-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="e4592-194">Configurer **gestion du Code Source** toouse votre branche local de [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) en fournissant hello **URL du référentiel**.</span><span class="sxs-lookup"><span data-stu-id="e4592-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="e4592-195">Par exemple : http://github.com/&lt;votre_id>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="e4592-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="e4592-196">Ajoutez un projet de hello Build étape toobuild à l’aide de Maven.</span><span class="sxs-lookup"><span data-stu-id="e4592-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="e4592-197">Faire en ajoutant une **exécuter shell** et ajoutez hello ligne dans **commande**:</span><span class="sxs-lookup"><span data-stu-id="e4592-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="e4592-198">Ajoutez une action post-build en sélectionnant **Publier une application web Azure**.</span><span class="sxs-lookup"><span data-stu-id="e4592-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="e4592-199">Fournissez, **mySp**, principal du service Azure hello stockée dans l’étape précédente en tant qu’informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="e4592-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="e4592-200">Dans **Configuration de l’application** , choisissez le groupe de ressources hello et une application web de Linux dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e4592-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="e4592-201">Choisissez Publier via Docker.</span><span class="sxs-lookup"><span data-stu-id="e4592-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="e4592-202">Renseignez le chemin **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="e4592-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="e4592-203">Vous pouvez conserver la valeur par défaut hello « / Dockerfile » pour **URL de Registre Docker**, fournissez au format hello https://&lt;myRegistry >. azurecr.io si vous utilisez le Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="e4592-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="e4592-204">Laissez ce champ vide si vous utilisez DockerHub.</span><span class="sxs-lookup"><span data-stu-id="e4592-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="e4592-205">Pour **informations d’identification du Registre**, ajouter des informations d’identification de hello pour hello Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="e4592-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="e4592-206">Vous pouvez obtenir hello userid et password par hello suivant des commandes CLI d’Azure en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e4592-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="e4592-207">Hello première commande active compte d’administrateur hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="e4592-208">Hello du nom de l’image docker et de balise dans **avancé** onglet sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="e4592-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="e4592-209">Par défaut, le nom de l’image est obtenue à partir de l’image de hello nom que vous avez configuré dans la balise d’Azure hello portail (dans le paramètre de conteneur Docker.) est généré à partir de $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="e4592-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="e4592-210">Assurez-vous que vous spécifiez le nom de l’image hello dans des portails Azure ou fournissez une valeur pour **Image Docker** dans **avancé** onglet. Pour cet exemple, indiquez « &lt;votreRegistre>.azurecr.io/calculator » pour **Image Docker** et ne renseignez pas **Balise d’image Docker**.</span><span class="sxs-lookup"><span data-stu-id="e4592-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="e4592-211">Notez que le déploiement échoue si vous utilisez le paramètre Image Docker prédéfini.</span><span class="sxs-lookup"><span data-stu-id="e4592-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="e4592-212">Assurez-vous de que modifier docker config toouse personnalisée dans le paramètre de conteneur Docker dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e4592-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="e4592-213">Pour l’image intégrée, utilisez toodeploy de méthode de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="e4592-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="e4592-214">Méthode de téléchargement toofile similaire, vous pouvez choisir un autre emplacement autre que de production.</span><span class="sxs-lookup"><span data-stu-id="e4592-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="e4592-215">Enregistrez et générez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-215">Save and build hello project.</span></span> <span data-ttu-id="e4592-216">Vous voyez votre image de conteneur est transmise tooyour Registre et de l’application web est déployée.</span><span class="sxs-lookup"><span data-stu-id="e4592-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="e4592-217">Déployer tooWeb application sur Linux avec Docker à l’aide du pipeline de Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="e4592-218">Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="e4592-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="e4592-219">Cliquez sur hello crayon icône tooedit ce groupe de ressources de fichier tooupdate hello et le nom de votre application web sur la ligne 11 et 12 respectivement.</span><span class="sxs-lookup"><span data-stu-id="e4592-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="e4592-220">Modifier la ligne 13 tooyour conteneur Registre serveur</span><span class="sxs-lookup"><span data-stu-id="e4592-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="e4592-221">Modifier la ligne 16 tooupdate d’identification de votre instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="e4592-222">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4592-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="e4592-223">Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="e4592-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="e4592-224">Fournissez un nom pour le travail de hello et sélectionnez **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e4592-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="e4592-225">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4592-225">Click **OK**.</span></span>
3. <span data-ttu-id="e4592-226">Cliquez sur hello **Pipeline** onglet suivant.</span><span class="sxs-lookup"><span data-stu-id="e4592-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="e4592-227">Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.</span><span class="sxs-lookup"><span data-stu-id="e4592-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="e4592-228">Pour **SCM**, sélectionnez **Git**.</span><span class="sxs-lookup"><span data-stu-id="e4592-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="e4592-229">Entrez hello GitHub URL pour votre référentiel RAMIFIÉ : https :&lt;votre dépôt RAMIFIÉ > .git</span><span class="sxs-lookup"><span data-stu-id="e4592-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="e4592-230">Mise à jour 7, **chemin d’accès du Script** trop « Jenkinsfile_container_plugin »</span><span class="sxs-lookup"><span data-stu-id="e4592-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="e4592-231">Cliquez sur **enregistrer** et la tâche d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="e4592-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="e4592-232">Vérifier votre application web</span><span class="sxs-lookup"><span data-stu-id="e4592-232">Verify your web app</span></span>

1. <span data-ttu-id="e4592-233">le fichier WAR tooverify hello est déployé avec succès l’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="e4592-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="e4592-234">Ouvrez un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="e4592-234">Open a web browser.</span></span>
2. <span data-ttu-id="e4592-235">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping vous consultez :</span><span class="sxs-lookup"><span data-stu-id="e4592-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="e4592-236">Bienvenue dans l’application Web de tooJava !!!</span><span class="sxs-lookup"><span data-stu-id="e4592-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="e4592-237">La mise à jour est effectuée !</span><span class="sxs-lookup"><span data-stu-id="e4592-237">This is updated!</span></span>
   <span data-ttu-id="e4592-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="e4592-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="e4592-239">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y</span><span class="sxs-lookup"><span data-stu-id="e4592-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Calculatrice : ajouter](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="e4592-241">Pour App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="e4592-241">For App service on Linux</span></span>

* <span data-ttu-id="e4592-242">tooverify, dans Azure CLI, exécutez :</span><span class="sxs-lookup"><span data-stu-id="e4592-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="e4592-243">Vous obtenez hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="e4592-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="e4592-244">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="e4592-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="e4592-245">Vous voyez le message de type hello :</span><span class="sxs-lookup"><span data-stu-id="e4592-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="e4592-246">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y</span><span class="sxs-lookup"><span data-stu-id="e4592-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="e4592-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e4592-247">Next steps</span></span>

<span data-ttu-id="e4592-248">Dans ce didacticiel, vous utilisez hello Azure App Service plug-in toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e4592-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="e4592-249">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4592-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4592-250">Configurer Jenkins toodeploy Azure App Service via FTP</span><span class="sxs-lookup"><span data-stu-id="e4592-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="e4592-251">Configurer Jenkins toodeploy tooAzure du Service d’applications sur Linux avec Docker</span><span class="sxs-lookup"><span data-stu-id="e4592-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
