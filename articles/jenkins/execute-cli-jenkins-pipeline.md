---
title: "Exécuter l’interface de ligne de commande Azure avec Jenkins | Microsoft Docs"
description: "Découvrez comment utiliser l’interface CLI Azure pour déployer une application web Java vers Azure dans un pipeline Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="0aae2-103">Déploiement dans Azure App Service avec Jenkins et l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="0aae2-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="0aae2-104">Pour déployer une application web Java dans Azure, vous pouvez utiliser l’interface CLI Azure dans le [pipeline Jenkins](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="0aae2-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="0aae2-105">Dans ce didacticiel, vous créez un pipeline CI/CD sur une machine virtuelle Azure et apprenez notamment comment :</span><span class="sxs-lookup"><span data-stu-id="0aae2-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0aae2-106">Créer une machine virtuelle Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="0aae2-107">Configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-107">Configure Jenkins</span></span>
> * <span data-ttu-id="0aae2-108">Créer une application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="0aae2-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="0aae2-109">Préparer un dépôt GitHub</span><span class="sxs-lookup"><span data-stu-id="0aae2-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="0aae2-110">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="0aae2-111">Exécuter le pipeline et vérifier l’application web</span><span class="sxs-lookup"><span data-stu-id="0aae2-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="0aae2-112">Ce didacticiel requiert Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0aae2-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0aae2-113">Pour connaître la version de l’interface, exécutez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="0aae2-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="0aae2-114">Si vous devez mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0aae2-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="0aae2-115">Créer et configurer l’instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="0aae2-116">Si vous ne disposez pas encore d’un serveur maître Jenkins, commencez par utiliser le [modèle de solution](install-jenkins-solution-template.md), qui inclut le plug-in requis [Informations d’identification Azure](https://plugins.jenkins.io/azure-credentials) par défaut.</span><span class="sxs-lookup"><span data-stu-id="0aae2-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="0aae2-117">Le plug-in Informations d’identification Azure vous permet de stocker les informations d’identification du principal de service Microsoft Azure dans Jenkins.</span><span class="sxs-lookup"><span data-stu-id="0aae2-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="0aae2-118">Dans la version 1.2, nous avons ajouté la prise en charge afin que le pipeline Jenkins puisse obtenir les informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="0aae2-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="0aae2-119">Vérifiez que vous disposez de la version 1.2 ou d’une version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="0aae2-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="0aae2-120">Dans le tableau de bord Jenkins, cliquez sur **Gérer Jenkins -> Gestionnaire de plug-in ->** et recherchez **Informations d’identification Azure**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="0aae2-121">Mettez à jour le plug-in si la version est antérieure à la version 1.2.</span><span class="sxs-lookup"><span data-stu-id="0aae2-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="0aae2-122">Java JDK et Maven sont également requis dans le serveur maître Jenkins.</span><span class="sxs-lookup"><span data-stu-id="0aae2-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="0aae2-123">Pour les installer, connectez-vous au serveur maître Jenkins à l’aide de SSH et exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0aae2-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="0aae2-124">Ajout du principal de service Azure aux informations d’identification Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="0aae2-125">Les informations d’identification Azure sont nécessaires pour exécuter l’interface CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="0aae2-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="0aae2-126">Dans le tableau de bord Jenkins, cliquez sur **Informations d’identification > Système**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="0aae2-127">Cliquez sur **Informations d’identification globales (sans restriction)**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="0aae2-128">Cliquez sur **Ajouter des informations d’identification** pour ajouter un [principal de service Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en renseignant les valeurs suivantes : ID d’abonnement, ID de client, secret client et point de terminaison de jeton OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0aae2-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="0aae2-129">Fournissez un ID qui sera utilisé dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0aae2-129">Provide an ID for use in subsequent step.</span></span>

![Ajout d’informations d'identification](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="0aae2-131">Créer un plan Azure App Service pour déployer l’application web Java</span><span class="sxs-lookup"><span data-stu-id="0aae2-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="0aae2-132">Créez un plan Azure App Service avec le niveau tarifaire **Gratuit** à l’aide de la commande d’interface de ligne de commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="0aae2-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="0aae2-133">Le plan App Service définit les ressources physiques utilisées pour héberger vos applications.</span><span class="sxs-lookup"><span data-stu-id="0aae2-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="0aae2-134">Toutes les applications affectées à un plan App Service partagent ces ressources, ce qui vous permet de réduire les coûts lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="0aae2-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="0aae2-135">Lorsque le plan est prêt, l’interface de ligne de commande Azure affiche une sortie similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0aae2-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="0aae2-136">Création d’une application web Azure</span><span class="sxs-lookup"><span data-stu-id="0aae2-136">Create an Azure Web app</span></span>

 <span data-ttu-id="0aae2-137">Utilisez la commande d’interface de ligne de commande [az webapp create](/cli/azure/appservice/web#create) pour créer une définition d’application web dans le plan App Service `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="0aae2-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="0aae2-138">La définition d’application web fournit une URL pour accéder à votre application et permet de configurer plusieurs options pour déployer votre code dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0aae2-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="0aae2-139">Remplacez l’espace réservé `<app_name>` avec votre propre nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="0aae2-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="0aae2-140">Ce nom unique est utilisé dans le nom de domaine par défaut de l’application web. Pour cette raison, ce nom doit être unique sur l’ensemble des applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0aae2-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="0aae2-141">Vous pouvez mapper une entrée de nom de domaine personnalisée vers l’application web avant de l’exposer à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0aae2-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="0aae2-142">Une fois que la définition de l’application web est prête, l’interface de ligne de commande Azure affiche des informations similaires à celles de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0aae2-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="0aae2-143">Configurer Java</span><span class="sxs-lookup"><span data-stu-id="0aae2-143">Configure Java</span></span> 

<span data-ttu-id="0aae2-144">Définissez la configuration d’exécution Java dont votre application a besoin avec la commande [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="0aae2-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="0aae2-145">La commande suivante configure l’application web de manière à ce qu’elle s’exécute sur un JDK Java 8 récent et sur [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="0aae2-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="0aae2-146">Préparer un dépôt GitHub</span><span class="sxs-lookup"><span data-stu-id="0aae2-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="0aae2-147">Ouvrez le dépôt [Application web Java simple pour Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="0aae2-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="0aae2-148">Pour répliquer le dépôt sur votre propre compte GitHub, cliquez sur le bouton **Bifurcation** en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="0aae2-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="0aae2-149">Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="0aae2-150">Cliquez sur l’icône du crayon pour modifier ce fichier et mettre à jour le groupe de ressources, ainsi que le nom de votre application web sur les lignes 20 et 21, respectivement.</span><span class="sxs-lookup"><span data-stu-id="0aae2-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="0aae2-151">Modifiez la ligne 23 pour mettre à jour l’ID des informations d’identification dans votre instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="0aae2-152">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="0aae2-153">Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="0aae2-154">Fournissez un nom pour le travail et sélectionnez **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="0aae2-155">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-155">Click **OK**.</span></span>
* <span data-ttu-id="0aae2-156">Ensuite, cliquez sur l’onglet **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="0aae2-157">Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="0aae2-158">Pour **SCM**, sélectionnez **Git**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="0aae2-159">Entrez l’URL GitHub de votre dépôt dupliqué : https:\<votre dépôt dupliqué\>.git</span><span class="sxs-lookup"><span data-stu-id="0aae2-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="0aae2-160">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0aae2-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="0aae2-161">Tester votre pipeline</span><span class="sxs-lookup"><span data-stu-id="0aae2-161">Test your pipeline</span></span>
* <span data-ttu-id="0aae2-162">Accédez au pipeline que vous avez créé, cliquez sur **Générer maintenant**</span><span class="sxs-lookup"><span data-stu-id="0aae2-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="0aae2-163">En quelques secondes, une build doit être générée. Vous pouvez y accéder et cliquer sur **Sortie de la console** pour afficher les détails</span><span class="sxs-lookup"><span data-stu-id="0aae2-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="0aae2-164">Vérifier votre application web</span><span class="sxs-lookup"><span data-stu-id="0aae2-164">Verify your web app</span></span>
<span data-ttu-id="0aae2-165">Pour vérifier le déploiement du fichier WAR dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="0aae2-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="0aae2-166">Ouvrez un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="0aae2-166">Open a web browser:</span></span>

* <span data-ttu-id="0aae2-167">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="0aae2-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="0aae2-168">Vous voyez :</span><span class="sxs-lookup"><span data-stu-id="0aae2-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="0aae2-169">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (remplacez &lt;x> et &lt;y> par n’importe quels chiffres) pour obtenir la somme de x et de y</span><span class="sxs-lookup"><span data-stu-id="0aae2-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![Calculatrice : ajouter](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="0aae2-171">Déployer dans une application web Azure sous Linux</span><span class="sxs-lookup"><span data-stu-id="0aae2-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="0aae2-172">Maintenant que vous savez comment utiliser l’interface CLI Azure dans votre pipeline Jenkins, vous pouvez modifier le script pour déployer dans une application web Azure sous Linux.</span><span class="sxs-lookup"><span data-stu-id="0aae2-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="0aae2-173">L’application web sous Linux prend en charge une méthode différente pour le déploiement, à savoir l’utilisation de Docker.</span><span class="sxs-lookup"><span data-stu-id="0aae2-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="0aae2-174">Pour déployer, vous devez fournir un fichier Docker qui intègre votre application web et le runtime du service dans une image Docker.</span><span class="sxs-lookup"><span data-stu-id="0aae2-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="0aae2-175">Le plug-in crée ensuite l’image, l’insère dans un registre Docker et déploie l’image dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="0aae2-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="0aae2-176">Suivez les étapes décrites [ici](/azure/app-service-web/app-service-linux-how-to-create-web-app) pour créer une application web Azure qui s’exécute sous Linux.</span><span class="sxs-lookup"><span data-stu-id="0aae2-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="0aae2-177">Installez Docker sur votre instance Jenkins en suivant les instructions dans cet [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="0aae2-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="0aae2-178">Créez un registre de conteneur dans le portail Azure à l’aide des étapes décrites [ici](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0aae2-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="0aae2-179">Dans le même dépôt dupliqué [Application web Java simple pour Azure](https://github.com/azure-devops/javawebappsample), modifiez le fichier **Jenkinsfile2** :</span><span class="sxs-lookup"><span data-stu-id="0aae2-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="0aae2-180">Mettez à jour les lignes 18 à 21 à l’aide du nom de votre groupe de ressources, de votre application web et de l’enregistrement de contrôle d’accès, respectivement.</span><span class="sxs-lookup"><span data-stu-id="0aae2-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="0aae2-181">Mettez à jour \<azsrvprincipal\> sur la ligne 24 à l’aide de vos informations d’identification</span><span class="sxs-lookup"><span data-stu-id="0aae2-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="0aae2-182">Créez un pipeline Jenkins comme lors du déploiement dans l’application web Azure sous Windows, en utilisant **Jenkinsfile2** à la place.</span><span class="sxs-lookup"><span data-stu-id="0aae2-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="0aae2-183">Exécutez votre nouveau travail.</span><span class="sxs-lookup"><span data-stu-id="0aae2-183">Run your new job.</span></span>
* <span data-ttu-id="0aae2-184">Pour vérifier, dans l’interface CLI Azure, exécutez :</span><span class="sxs-lookup"><span data-stu-id="0aae2-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="0aae2-185">Vous obtenez le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="0aae2-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="0aae2-186">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="0aae2-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="0aae2-187">Le message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="0aae2-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="0aae2-188">Accédez à http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (remplacez &lt;x> et &lt;y> par n’importe quels chiffres) pour obtenir la somme de x et de y</span><span class="sxs-lookup"><span data-stu-id="0aae2-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="0aae2-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0aae2-189">Next steps</span></span>
<span data-ttu-id="0aae2-190">Dans ce didacticiel, vous avez configuré un pipeline Jenkins qui extrait le code source dans le dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="0aae2-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="0aae2-191">Il exécute Maven pour générer un fichier war et utilise ensuite l’interface CLI Azure pour le déploiement vers Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0aae2-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="0aae2-192">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="0aae2-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0aae2-193">Créer une machine virtuelle Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="0aae2-194">Configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-194">Configure Jenkins</span></span>
> * <span data-ttu-id="0aae2-195">Créer une application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="0aae2-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="0aae2-196">Préparer un dépôt GitHub</span><span class="sxs-lookup"><span data-stu-id="0aae2-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="0aae2-197">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="0aae2-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="0aae2-198">Exécuter le pipeline et vérifier l’application web</span><span class="sxs-lookup"><span data-stu-id="0aae2-198">Run the pipeline and verify the web app</span></span>
