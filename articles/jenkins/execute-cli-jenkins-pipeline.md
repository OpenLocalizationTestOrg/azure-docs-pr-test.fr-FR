---
title: "aaaExecute hello CLI d’Azure avec Jenkins | Documents Microsoft"
description: "Découvrez comment toouse CLI d’Azure toodeploy Java web tooAzure d’application dans le Pipeline de Jenkins"
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
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="8d9a4-103">Déployer tooAzure du Service d’applications avec Jenkins et hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="8d9a4-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="8d9a4-104">toodeploy un tooAzure d’application web Java, vous pouvez utiliser CLI d’Azure dans [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="8d9a4-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="8d9a4-105">Dans ce didacticiel, vous créez un pipeline CI/CD sur une machine virtuelle Azure et apprenez notamment comment :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d9a4-106">Créer une machine virtuelle Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="8d9a4-107">Configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-107">Configure Jenkins</span></span>
> * <span data-ttu-id="8d9a4-108">Créer une application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="8d9a4-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="8d9a4-109">Préparer un dépôt GitHub</span><span class="sxs-lookup"><span data-stu-id="8d9a4-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="8d9a4-110">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="8d9a4-111">Exécuter le pipeline de hello et vérifiez que l’application web hello</span><span class="sxs-lookup"><span data-stu-id="8d9a4-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="8d9a4-112">Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8d9a4-113">version de hello toofind, exécutez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="8d9a4-114">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8d9a4-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="8d9a4-115">Créer et configurer l’instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="8d9a4-116">Si vous n’avez pas déjà un maître de Jenkins, commencer par hello [modèle de Solution](install-jenkins-solution-template.md), qui inclut la hello requis [informations d’identification Azure](https://plugins.jenkins.io/azure-credentials) plug-in par défaut.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="8d9a4-117">plug-in des informations d’identification Azure Hello vous permet d’informations d’identification toostore Microsoft Azure service principales de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="8d9a4-118">Dans la version 1.2, nous avons ajouté la prise en charge de hello ce Jenkins Pipeline peut obtenir des informations d’identification Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="8d9a4-119">Vérifiez que vous disposez de la version 1.2 ou d’une version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="8d9a4-120">Dans le tableau de bord hello Jenkins, cliquez sur **Jenkins de gérer -> Gestionnaire de plug-in ->** et recherchez **informations d’identification Azure**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="8d9a4-121">Mettre à jour des plug-in hello si la version de hello est antérieure à la version 1.2.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="8d9a4-122">Java JDK et Maven sont également requis dans master de Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="8d9a4-123">tooinstall, connectez-vous dans master tooJenkins à l’aide de SSH, puis réexécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="8d9a4-124">Ajouter des informations d’identification de service Azure principal tooJenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="8d9a4-125">Informations d’identification Azure sont nécessaire tooexecute CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="8d9a4-126">Dans le tableau de bord hello Jenkins, cliquez sur **informations d’identification -> système ->**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="8d9a4-127">Cliquez sur **Informations d’identification globales (sans restriction)**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="8d9a4-128">Cliquez sur **ajouter les informations d’identification** tooadd un [principal du service Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en remplissant hello ID d’abonnement, ID de Client, question secrète du Client et OAuth 2.0 Token Endpoint.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="8d9a4-129">Fournissez un ID qui sera utilisé dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-129">Provide an ID for use in subsequent step.</span></span>

![Ajout d’informations d'identification](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="8d9a4-131">Créer un Service d’application Azure pour le déploiement d’application web Java hello</span><span class="sxs-lookup"><span data-stu-id="8d9a4-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="8d9a4-132">Créer un plan de Service d’application Azure avec hello **libre** tarification à l’aide de hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande CLI.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="8d9a4-133">un plan de Hello définit hello ressources physiques utilisées toohost vos applications.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="8d9a4-134">Toutes les applications affectées tooan un plan de partagent ces ressources, ce qui vous toosave coût lors de l’hébergement de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="8d9a4-135">Lorsque le plan de hello est prêt, hello Qu'azure CLI montre similaire de sortie toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="8d9a4-136">Création d’une application web Azure</span><span class="sxs-lookup"><span data-stu-id="8d9a4-136">Create an Azure Web app</span></span>

 <span data-ttu-id="8d9a4-137">Hello d’utilisation [az webapp créer](/cli/azure/appservice/web#create) toocreate de commande CLI une définition d’application web Bonjour `myAppServicePlan` plan App Service.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="8d9a4-138">définition d’application web Hello fournit à votre application un tooaccess URL et configure plusieurs options toodeploy tooAzure de votre code.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="8d9a4-139">Hello de substitution `<app_name>` espace réservé avec votre propre nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="8d9a4-140">Ce nom unique fait partie du nom de domaine par défaut hello pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="8d9a4-141">Vous pouvez mapper une application web de domaine personnalisé nom entrée toohello avant de vous exposez tooyour utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="8d9a4-142">Lors de la définition d’application web hello est prête, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="8d9a4-143">Configurer Java</span><span class="sxs-lookup"><span data-stu-id="8d9a4-143">Configure Java</span></span> 

<span data-ttu-id="8d9a4-144">Configuration de hello Java runtime dont votre application a besoin par hello [mise à jour du fichier config web app service az](/cli/azure/appservice/web/config#update) commande.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="8d9a4-145">Hello commande suivante configure hello web application toorun sur une récente Java JDK de 8 et [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="8d9a4-146">Préparer un dépôt GitHub</span><span class="sxs-lookup"><span data-stu-id="8d9a4-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="8d9a4-147">Ouvrez hello [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) référentiel.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="8d9a4-148">toofork hello référentiel tooyour propre compte GitHub, cliquez sur hello **branchement** bouton dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="8d9a4-149">Dans l’interface utilisateur web de GitHub, ouvrez le fichier **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="8d9a4-150">Cliquez sur hello crayon icône tooedit ce groupe de ressources de fichier tooupdate hello et le nom de votre application web sur la ligne 20 et 21 respectivement.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="8d9a4-151">Modifier les informations d’identification ligne 23 tooupdate dans votre instance Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="8d9a4-152">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="8d9a4-153">Ouvrez Jenkins dans un navigateur web, cliquez sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="8d9a4-154">Fournissez un nom pour le travail de hello et sélectionnez **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="8d9a4-155">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-155">Click **OK**.</span></span>
* <span data-ttu-id="8d9a4-156">Cliquez sur hello **Pipeline** onglet suivant.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="8d9a4-157">Pour **Définition**, sélectionnez **Script de pipeline à partir de SCM**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="8d9a4-158">Pour **SCM**, sélectionnez **Git**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="8d9a4-159">Entrez hello GitHub URL pour votre référentiel RAMIFIÉ : https :\<votre dépôt RAMIFIÉ\>.git</span><span class="sxs-lookup"><span data-stu-id="8d9a4-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="8d9a4-160">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="8d9a4-161">Tester votre pipeline</span><span class="sxs-lookup"><span data-stu-id="8d9a4-161">Test your pipeline</span></span>
* <span data-ttu-id="8d9a4-162">Accédez pipeline toohello vous avez créé, cliquez sur **générer maintenant**</span><span class="sxs-lookup"><span data-stu-id="8d9a4-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="8d9a4-163">Une build doit réussir en quelques secondes, et vous pouvez toohello build et cliquez sur **la sortie de Console** détails de hello toosee</span><span class="sxs-lookup"><span data-stu-id="8d9a4-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="8d9a4-164">Vérifier votre application web</span><span class="sxs-lookup"><span data-stu-id="8d9a4-164">Verify your web app</span></span>
<span data-ttu-id="8d9a4-165">le fichier WAR tooverify hello est déployé avec succès l’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="8d9a4-166">Ouvrez un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-166">Open a web browser:</span></span>

* <span data-ttu-id="8d9a4-167">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="8d9a4-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="8d9a4-168">Vous voyez :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="8d9a4-169">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y</span><span class="sxs-lookup"><span data-stu-id="8d9a4-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Calculatrice : ajouter](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="8d9a4-171">Déployer tooAzure application Web sur Linux</span><span class="sxs-lookup"><span data-stu-id="8d9a4-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="8d9a4-172">Maintenant que vous savez comment toouse CLI d’Azure dans votre Jenkins de pipeline, vous pouvez modifier hello script toodeploy tooan Azure Web App sur Linux.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="8d9a4-173">Web application sur Linux prend en charge un déploiement différemment toodo hello, qui est toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="8d9a4-174">toodeploy, vous devez tooprovide un fichier Dockerfile par les packages de votre application web avec le runtime du service dans une image Docker.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="8d9a4-175">plug-in Hello ensuite générer l’image de hello, poussez-le du Registre de tooa Docker et déployer l’application web de hello image tooyour.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="8d9a4-176">Suivez les étapes de hello [ici](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate une application Web de Azure en cours d’exécution sur Linux.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="8d9a4-177">Installer Docker sur votre instance de Jenkins en suivant les instructions de hello dans ce [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="8d9a4-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="8d9a4-178">Créer un conteneur de Registre Bonjour portail Azure à l’aide des étapes de hello [ici](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8d9a4-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="8d9a4-179">Dans hello même [Simple d’application Web Java pour Azure](https://github.com/azure-devops/javawebappsample) référentiel vous dupliquée, modifier hello **Jenkinsfile2** fichier :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="8d9a4-180">Ligne de 18-21, mettre à jour les noms de toohello de votre groupe de ressources, une application web et un ACR respectivement.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="8d9a4-181">Ligne 24, mise à jour \<azsrvprincipal\> tooyour d’identification</span><span class="sxs-lookup"><span data-stu-id="8d9a4-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="8d9a4-182">Créer un pipeline Jenkins comme vous l’avez fait lors du déploiement d’application web de tooAzure dans Windows, cette fois, utilisez **Jenkinsfile2** à la place.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="8d9a4-183">Exécutez votre nouveau travail.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-183">Run your new job.</span></span>
* <span data-ttu-id="8d9a4-184">tooverify, dans Azure CLI, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="8d9a4-185">Vous obtenez hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="8d9a4-186">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="8d9a4-187">Vous voyez le message de type hello :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="8d9a4-188">Accédez toohttp : / /&lt;nom_application >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (remplacez &lt;x > et &lt;y > avec tous les nombres) somme hello tooget x et y</span><span class="sxs-lookup"><span data-stu-id="8d9a4-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="8d9a4-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d9a4-189">Next steps</span></span>
<span data-ttu-id="8d9a4-190">Dans ce didacticiel, vous avez configuré un pipeline de Jenkins extrait de code source de hello dans le référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="8d9a4-191">Exécute Maven toobuild un fichier war, puis utilise Azure CLI toodeploy tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="8d9a4-192">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d9a4-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d9a4-193">Créer une machine virtuelle Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="8d9a4-194">Configurer Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-194">Configure Jenkins</span></span>
> * <span data-ttu-id="8d9a4-195">Créer une application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="8d9a4-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="8d9a4-196">Préparer un dépôt GitHub</span><span class="sxs-lookup"><span data-stu-id="8d9a4-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="8d9a4-197">Créer un pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="8d9a4-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="8d9a4-198">Exécuter le pipeline de hello et vérifiez que l’application web hello</span><span class="sxs-lookup"><span data-stu-id="8d9a4-198">Run hello pipeline and verify hello web app</span></span>
