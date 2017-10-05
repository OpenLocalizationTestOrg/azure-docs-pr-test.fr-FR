---
title: "Déployer sur Azure App Service avec le plug-in Jenkins | Microsoft Docs"
description: "Découvrez comment utiliser le plug-in Azure App Service Jenkins pour déployer une application web Java sur Azure dans Jenkins."
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="6c86f-103">Déployer sur Azure App Service avec le plug-in Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="6c86f-104">Pour déployer une application web Java sur Azure, vous pouvez utiliser Azure CLI dans [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) ou vous pouvez utiliser le [plug-in Azure App Service Jenkins](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="6c86f-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="6c86f-105">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c86f-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c86f-106">Configurer Jenkins pour déployer sur Azure App Service via FTP</span><span class="sxs-lookup"><span data-stu-id="6c86f-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="6c86f-107">Configurer Jenkins pour déployer sur Azure App Service sur Linux par le biais de Docker</span><span class="sxs-lookup"><span data-stu-id="6c86f-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="6c86f-108">Créer et configurer l’instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="6c86f-109">Si vous ne disposez pas encore d’un serveur maître Jenkins, commencez par utiliser le [modèle de solution](install-jenkins-solution-template.md), qui inclut JDK8 et les plug-ins requis suivants :</span><span class="sxs-lookup"><span data-stu-id="6c86f-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="6c86f-110">[Plug-in du client Git Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="6c86f-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="6c86f-111">[Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="6c86f-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="6c86f-112">[Informations d’identification Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="6c86f-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="6c86f-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="6c86f-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="6c86f-114">Vous pouvez utiliser le plug-in App Service pour déployer l’application web dans tous les langages (par exemple, C#, PHP, Java et node.js, etc.) pris en charge par Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6c86f-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="6c86f-115">Dans ce didacticiel, nous utilisons l’exemple d’application Java, [Application web Java simple pour Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="6c86f-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="6c86f-116">Pour répliquer le dépôt sur votre propre compte GitHub, cliquez sur le bouton **Bifurcation** en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="6c86f-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="6c86f-117">Java JDK et Maven sont obligatoires pour la génération du projet Java.</span><span class="sxs-lookup"><span data-stu-id="6c86f-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="6c86f-118">Veillez à installer les composants sur le serveur maître Jenkins ou l’agent de la machine virtuelle si vous en utilisez un à des fins d’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="6c86f-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="6c86f-119">Pour les installer, connectez-vous à l’instance Jenkins à l’aide du protocole SSH et exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c86f-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="6c86f-120">Pour le déploiement sur App Service sur Linux, vous devez également installer Docker sur le serveur maître Jenkins ou l’agent de la machine virtuelle que vous utilisez pour la build.</span><span class="sxs-lookup"><span data-stu-id="6c86f-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="6c86f-121">Reportez-vous à cet article pour installer Docker : https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="6c86f-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="6c86f-122">Ajout du principal de service Azure aux informations d’identification Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="6c86f-123">Un principal de service Azure est nécessaire pour les déploiements sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c86f-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="6c86f-124">Utiliser [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ou le [portail Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) pour créer un principal de service Azure</span><span class="sxs-lookup"><span data-stu-id="6c86f-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="6c86f-125">Dans le tableau de bord Jenkins, cliquez sur **Informations d’identification > Système**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="6c86f-126">Cliquez sur **Informations d’identification globales (sans restriction)**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="6c86f-127">Cliquez sur **Ajouter des informations d’identification** pour ajouter un principal de service Microsoft Azure en renseignant les valeurs suivantes : ID d’abonnement, ID de client, secret client et point de terminaison de jeton OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6c86f-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="6c86f-128">Fournissez l’ID, **mySp**, à utiliser dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="6c86f-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="6c86f-129">Plug-in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6c86f-129">Azure App Service plugin</span></span>

<span data-ttu-id="6c86f-130">Le plug-in Azure App Service v1.0 prend en charge le déploiement continu sur Azure Web App via :</span><span class="sxs-lookup"><span data-stu-id="6c86f-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="6c86f-131">Git et FTP</span><span class="sxs-lookup"><span data-stu-id="6c86f-131">Git and FTP</span></span>
* <span data-ttu-id="6c86f-132">Docker pour application web sur Linux</span><span class="sxs-lookup"><span data-stu-id="6c86f-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="6c86f-133">Configurer Jenkins pour déployer une application web via FTP à l’aide du tableau de bord Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="6c86f-134">Pour déployer votre projet sur Azure Web App, vous pouvez charger vos artefacts de build (par exemple, un fichier .war en Java) à l’aide de Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="6c86f-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="6c86f-135">Avant de configurer le travail dans Jenkins, vous avez besoin d’un plan Azure App Service et d’une application web pour l’exécution de l’application Java.</span><span class="sxs-lookup"><span data-stu-id="6c86f-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="6c86f-136">Créez un plan Azure App Service avec le niveau tarifaire **Gratuit** à l’aide de la commande d’interface de ligne de commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="6c86f-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="6c86f-137">Le plan App Service définit les ressources physiques utilisées pour héberger vos applications.</span><span class="sxs-lookup"><span data-stu-id="6c86f-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="6c86f-138">Toutes les applications affectées à un plan App Service partagent ces ressources, ce qui vous permet de réduire les coûts lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="6c86f-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="6c86f-139">Créez une application web.</span><span class="sxs-lookup"><span data-stu-id="6c86f-139">Create a Web App.</span></span> <span data-ttu-id="6c86f-140">Vous pouvez utiliser le [portail Azure](/azure/app-service-web/web-sites-configure) ou la commande CLI Az suivante :</span><span class="sxs-lookup"><span data-stu-id="6c86f-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="6c86f-141">Vérifiez que vous définissez la configuration du runtime Java dont votre application a besoin.</span><span class="sxs-lookup"><span data-stu-id="6c86f-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="6c86f-142">La commande Azure CLI suivante configure l’application web de manière à ce qu’elle s’exécute sur un JDK Java 8 récent et sur [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="6c86f-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="6c86f-143">Configurer la tâche Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="6c86f-144">Créer un nouveau projet **freestyle** dans le tableau de bord Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="6c86f-145">Configurez la **gestion du code source** de sorte à utiliser votre duplication locale de l’[Application web Java simple pour Azure](https://github.com/azure-devops/javawebappsample) en fournissant l’**URL du dépôt**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="6c86f-146">Par exemple : http://github.com/&lt;votreID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="6c86f-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="6c86f-147">Ajoutez une étape de génération pour générer le projet à l’aide de Maven.</span><span class="sxs-lookup"><span data-stu-id="6c86f-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="6c86f-148">Pour ce faire, ajoutez une étape **Exécuter un interpréteur de commandes**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="6c86f-149">Pour cet exemple, nous avons besoin d’une étape supplémentaire pour renommer le fichier *.war dans le dossier cible et lui attribuer le nom ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="6c86f-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="6c86f-150">Ajoutez une action post-build en sélectionnant **Publier une application web Azure**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="6c86f-151">Indiquez, « mySp », le principal de service Azure stocké à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="6c86f-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="6c86f-152">Dans **Configuration de l’application**, choisissez le groupe de ressources et l’application web compris dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6c86f-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="6c86f-153">Le plug-in détecte automatiquement si l’application web est une application Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="6c86f-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="6c86f-154">Pour une application web basée sur Windows, l’option « Publier les fichiers » est présentée.</span><span class="sxs-lookup"><span data-stu-id="6c86f-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="6c86f-155">Renseignez les fichiers à déployer (par exemple, un package war si vous utilisez Java). Les répertoires source et cible sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="6c86f-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="6c86f-156">Les paramètres vous permettent de spécifier les dossiers source et cible lors du chargement des fichiers.</span><span class="sxs-lookup"><span data-stu-id="6c86f-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="6c86f-157">L’application web Java sur Azure est exécutée sur un serveur Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6c86f-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="6c86f-158">Ainsi, vous chargez votre package war dans le dossier webapps.</span><span class="sxs-lookup"><span data-stu-id="6c86f-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="6c86f-159">Pour cet exemple, définissez le **répertoire source** sur « target » et indiquez « webapps » pour le **répertoire cible**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="6c86f-160">Pour déployer sur un emplacement autre qu’un emplacement de production, vous pouvez également définir le nom **Slot**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="6c86f-161">Enregistrez le projet et générez-le.</span><span class="sxs-lookup"><span data-stu-id="6c86f-161">Save the project and build it.</span></span> <span data-ttu-id="6c86f-162">Votre application web est déployée sur Azure quand la build est terminée.</span><span class="sxs-lookup"><span data-stu-id="6c86f-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="6c86f-163">Déployer l’application Web via FTP à l’aide du pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="6c86f-164">Le plug-in est compatible avec le pipeline.</span><span class="sxs-lookup"><span data-stu-id="6c86f-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="6c86f-165">Vous pouvez vous référer à un exemple dans le dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c86f-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="6c86f-166">Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="6c86f-167">Cliquez sur l’icône du crayon pour modifier ce fichier et mettre à jour le groupe de ressources, ainsi que le nom de votre application web sur les lignes 11 et 12, respectivement.</span><span class="sxs-lookup"><span data-stu-id="6c86f-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="6c86f-168">Modifiez la ligne 14 pour mettre à jour l’ID des informations d’identification dans votre instance Jenkins.</span><span class="sxs-lookup"><span data-stu-id="6c86f-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="6c86f-169">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="6c86f-170">Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="6c86f-171">Fournissez un nom pour le travail et sélectionnez **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="6c86f-172">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-172">Click **OK**.</span></span>
3. <span data-ttu-id="6c86f-173">Ensuite, cliquez sur l’onglet **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="6c86f-174">Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="6c86f-175">Pour **SCM**, sélectionnez **Git**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="6c86f-176">Entrez l’URL GitHub de votre dépôt dupliqué : https:&lt;votre dépôt dupliqué>.git</span><span class="sxs-lookup"><span data-stu-id="6c86f-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="6c86f-177">Remplacez le **chemin du script** par « Jenkinsfile_ftp_plugin ».</span><span class="sxs-lookup"><span data-stu-id="6c86f-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="6c86f-178">Cliquez sur **Enregistrer** et exécutez la tâche.</span><span class="sxs-lookup"><span data-stu-id="6c86f-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="6c86f-179">Configurer Jenkins pour déployer l’application web sur Linux via Docker</span><span class="sxs-lookup"><span data-stu-id="6c86f-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="6c86f-180">Outre Git/FTP, l’application web sur Linux prend en charge le déploiement à l’aide de Docker.</span><span class="sxs-lookup"><span data-stu-id="6c86f-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="6c86f-181">Pour déployer à l’aide de Docker, vous devez fournir un fichier Docker qui intègre votre application web et le runtime du service dans une image Docker.</span><span class="sxs-lookup"><span data-stu-id="6c86f-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="6c86f-182">Le plug-in crée ensuite l’image, l’insère dans un registre Docker et déploie l’image sur votre application web.</span><span class="sxs-lookup"><span data-stu-id="6c86f-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="6c86f-183">L’application web sur Linux prend également en charge les méthodes traditionnelles telles que Git et FTP, mais uniquement pour les langages intégrés (.NET Core, Node.js, PHP et Ruby).</span><span class="sxs-lookup"><span data-stu-id="6c86f-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="6c86f-184">Pour les autres langages, vous devez empaqueter le code de votre application et le runtime du service dans une image Docker et utiliser Docker pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="6c86f-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="6c86f-185">Avant de configurer la tâche dans Jenkins, vous avez besoin d’un service d’application Azure sur Linux.</span><span class="sxs-lookup"><span data-stu-id="6c86f-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="6c86f-186">Un registre de conteneurs est également nécessaire pour stocker et gérer vos images conteneurs Docker privées.</span><span class="sxs-lookup"><span data-stu-id="6c86f-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="6c86f-187">Vous pouvez utiliser DockerHub ; nous utilisons Azure Container Registry pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="6c86f-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="6c86f-188">Vous pouvez suivre les étapes indiquées [ici](/azure/app-service-web/app-service-linux-how-to-create-web-app) pour créer une application web sur Linux.</span><span class="sxs-lookup"><span data-stu-id="6c86f-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="6c86f-189">Azure Container Registry est un service [de registre Docker] géré (https://docs.docker.com/registry/) basé sur le registre open source Docker 2.0.</span><span class="sxs-lookup"><span data-stu-id="6c86f-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="6c86f-190">Suivez les étapes indiquées [ici] (/azure/container-registry/container-registry-get-started-azure-cli) pour plus d’informations sur la marche à suivre.</span><span class="sxs-lookup"><span data-stu-id="6c86f-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="6c86f-191">Vous pouvez également utiliser DockerHub.</span><span class="sxs-lookup"><span data-stu-id="6c86f-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="6c86f-192">Pour déployer à l’aide de Docker :</span><span class="sxs-lookup"><span data-stu-id="6c86f-192">To deploy using docker:</span></span>

1. <span data-ttu-id="6c86f-193">Créez un nouveau projet freestyle dans le tableau de bord Jenkins.</span><span class="sxs-lookup"><span data-stu-id="6c86f-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="6c86f-194">Configurez la **gestion du code source** de sorte à utiliser votre duplication locale de l’[Application web Java simple pour Azure](https://github.com/azure-devops/javawebappsample) en fournissant l’**URL du dépôt**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="6c86f-195">Par exemple : http://github.com/&lt;votre_id>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="6c86f-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="6c86f-196">Ajoutez une étape de génération pour générer le projet à l’aide de Maven.</span><span class="sxs-lookup"><span data-stu-id="6c86f-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="6c86f-197">Pour cela, ajoutez une étape **Exécuter un interpréteur de commandes** et ajoutez la ligne suivante dans **Commande** :</span><span class="sxs-lookup"><span data-stu-id="6c86f-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="6c86f-198">Ajoutez une action post-build en sélectionnant **Publier une application web Azure**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="6c86f-199">Indiquez, **mySp**, le principal de service Azure stocké à l’étape précédente, comme informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="6c86f-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="6c86f-200">Dans la section **Configuration de l’application**, choisissez le groupe de ressources et une application web Linux compris dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6c86f-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="6c86f-201">Choisissez Publier via Docker.</span><span class="sxs-lookup"><span data-stu-id="6c86f-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="6c86f-202">Renseignez le chemin **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="6c86f-203">Vous pouvez conserver la valeur par défaut « /Dockerfile » pour l’**URL du registre Docker** fournie au format https://&lt;monRegistre>.azurecr.io si vous utilisez Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6c86f-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="6c86f-204">Laissez ce champ vide si vous utilisez DockerHub.</span><span class="sxs-lookup"><span data-stu-id="6c86f-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="6c86f-205">Dans le champ **Informations d’identification du registre**, ajoutez celles d’Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6c86f-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="6c86f-206">Vous pouvez obtenir l’ID utilisateur et un mot de passe en exécutant les commandes suivantes dans Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c86f-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="6c86f-207">La première commande active le compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6c86f-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="6c86f-208">Le nom et la balise de l’image Docker sous l’onglet **Avancé** sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="6c86f-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="6c86f-209">Par défaut, le nom de l’image est obtenue à partir du nom de l’image que vous avez configuré dans le portail Azure (paramètre Conteneur Docker.) La balise est générée à partir de $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="6c86f-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="6c86f-210">Vérifiez que vous spécifiez le nom de l’image dans le portail Azure ou fournissez une valeur pour **Image Docker** sous l’onglet **Avancé**. Pour cet exemple, indiquez « &lt;votreRegistre>.azurecr.io/calculator » pour **Image Docker** et ne renseignez pas **Balise d’image Docker**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="6c86f-211">Notez que le déploiement échoue si vous utilisez le paramètre Image Docker prédéfini.</span><span class="sxs-lookup"><span data-stu-id="6c86f-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="6c86f-212">Veillez bien à modifier la configuration Docker pour utiliser l’image personnalisée dans le paramètre Conteneur Docker dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6c86f-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="6c86f-213">Pour l’image prédéfinie, utilisez une approche de déploiement par chargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="6c86f-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="6c86f-214">À l’instar de l’approche par chargement de fichier, vous pouvez choisir un emplacement autre qu’un emplacement de production.</span><span class="sxs-lookup"><span data-stu-id="6c86f-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="6c86f-215">Enregistrez et générez le projet.</span><span class="sxs-lookup"><span data-stu-id="6c86f-215">Save and build the project.</span></span> <span data-ttu-id="6c86f-216">Vous constatez que votre image conteneur est placée dans votre registre et que l’application web est déployée.</span><span class="sxs-lookup"><span data-stu-id="6c86f-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="6c86f-217">Déployer sur une application web sur Linux via Docker en utilisant le pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="6c86f-218">Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="6c86f-219">Cliquez sur l’icône du crayon pour modifier ce fichier et mettre à jour le groupe de ressources, ainsi que le nom de votre application web sur les lignes 11 et 12, respectivement.</span><span class="sxs-lookup"><span data-stu-id="6c86f-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="6c86f-220">Remplacer la ligne 13 par votre serveur de registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="6c86f-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="6c86f-221">Remplacer la ligne 16 pour mettre à jour l’ID des informations d’identification dans votre instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="6c86f-222">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="6c86f-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="6c86f-223">Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="6c86f-224">Fournissez un nom pour le travail et sélectionnez **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="6c86f-225">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-225">Click **OK**.</span></span>
3. <span data-ttu-id="6c86f-226">Ensuite, cliquez sur l’onglet **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="6c86f-227">Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="6c86f-228">Pour **SCM**, sélectionnez **Git**.</span><span class="sxs-lookup"><span data-stu-id="6c86f-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="6c86f-229">Entrez l’URL GitHub de votre dépôt dupliqué : https:&lt;votre dépôt dupliqué>.git</span><span class="sxs-lookup"><span data-stu-id="6c86f-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="6c86f-230">7, Mettez à jour le **chemin du script** en indiquant « Jenkinsfile_container_plugin ».</span><span class="sxs-lookup"><span data-stu-id="6c86f-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="6c86f-231">Cliquez sur **Enregistrer** et exécutez la tâche.</span><span class="sxs-lookup"><span data-stu-id="6c86f-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="6c86f-232">Vérifier votre application web</span><span class="sxs-lookup"><span data-stu-id="6c86f-232">Verify your web app</span></span>

1. <span data-ttu-id="6c86f-233">Pour vérifier le déploiement du fichier WAR dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="6c86f-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="6c86f-234">Ouvrez un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="6c86f-234">Open a web browser.</span></span>
2. <span data-ttu-id="6c86f-235">Accédez à http://&lt;nom_application>.azurewebsites.net/api/calculator/ping. Vous voyez :</span><span class="sxs-lookup"><span data-stu-id="6c86f-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="6c86f-236">Bienvenue dans l’application web Java !</span><span class="sxs-lookup"><span data-stu-id="6c86f-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="6c86f-237">La mise à jour est effectuée !</span><span class="sxs-lookup"><span data-stu-id="6c86f-237">This is updated!</span></span>
   <span data-ttu-id="6c86f-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="6c86f-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="6c86f-239">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (remplacez &lt;x> et &lt;y> par n’importe quels chiffres) pour obtenir la somme de x et de y</span><span class="sxs-lookup"><span data-stu-id="6c86f-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Calculatrice : ajouter](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="6c86f-241">Pour App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="6c86f-241">For App service on Linux</span></span>

* <span data-ttu-id="6c86f-242">Pour vérifier, dans l’interface CLI Azure, exécutez :</span><span class="sxs-lookup"><span data-stu-id="6c86f-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="6c86f-243">Vous obtenez le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="6c86f-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="6c86f-244">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="6c86f-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="6c86f-245">Le message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="6c86f-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="6c86f-246">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (remplacez &lt;x> et &lt;y> par n’importe quels chiffres) pour obtenir la somme de x et de y</span><span class="sxs-lookup"><span data-stu-id="6c86f-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="6c86f-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c86f-247">Next steps</span></span>

<span data-ttu-id="6c86f-248">Dans ce didacticiel, vous utilisez le plug-in Azure App Service pour effectuer le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c86f-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="6c86f-249">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c86f-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c86f-250">Configurer Jenkins pour déployer Azure App Service via FTP</span><span class="sxs-lookup"><span data-stu-id="6c86f-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="6c86f-251">Configurer Jenkins pour déployer sur Azure App Service sur Linux par le biais de Docker</span><span class="sxs-lookup"><span data-stu-id="6c86f-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 