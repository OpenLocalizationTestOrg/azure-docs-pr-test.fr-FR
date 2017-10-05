---
title: "Déploiement Git local vers Azure App Service"
description: "Découvrez comment activer le déploiement Git local vers Azure App Service"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="a9a38-103">Déploiement Git local vers Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a9a38-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="a9a38-104">Ce didacticiel vous montre comment déployer votre application vers [Azure App Service] depuis un référentiel Git sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a9a38-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="a9a38-105">App Service prend en charge cette approche avec l'option de déploiement **Git local** dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="a9a38-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="a9a38-106">La plupart des commandes Git décrites dans cet article sont exécutées automatiquement pendant la création d’une application App Service avec l’[interface de ligne de commande Azure] comme décrit [ici](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a9a38-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9a38-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a9a38-107">Prerequisites</span></span>
<span data-ttu-id="a9a38-108">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a9a38-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="a9a38-109">Git.</span><span class="sxs-lookup"><span data-stu-id="a9a38-109">Git.</span></span> <span data-ttu-id="a9a38-110">Vous pouvez télécharger le fichier binaire d’installation [ici](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="a9a38-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="a9a38-111">Connaissances élémentaires de Git.</span><span class="sxs-lookup"><span data-stu-id="a9a38-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="a9a38-112">Un compte Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a9a38-112">A Microsoft Azure account.</span></span> <span data-ttu-id="a9a38-113">Si vous n’avez pas de compte, vous pouvez [demander un essai gratuit](https://azure.microsoft.com/pricing/free-trial) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="a9a38-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="a9a38-114">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="a9a38-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="a9a38-115">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="a9a38-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="a9a38-116"><a name="Step1"></a>Étape 1 : création d’un référentiel local</span><span class="sxs-lookup"><span data-stu-id="a9a38-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="a9a38-117">Effectuez les tâches suivantes pour créer un nouveau référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="a9a38-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="a9a38-118">Lancez un outil de ligne de commande, comme **GitBash** (Windows) ou **Bash** (Unix Shell).</span><span class="sxs-lookup"><span data-stu-id="a9a38-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="a9a38-119">Sur les systèmes OS X, la ligne de commande est accessible depuis l'application **Terminal** .</span><span class="sxs-lookup"><span data-stu-id="a9a38-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="a9a38-120">Accédez au répertoire où figure le contenu à déployer.</span><span class="sxs-lookup"><span data-stu-id="a9a38-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="a9a38-121">Utilisez la commande suivante pour initialiser un nouveau référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="a9a38-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="a9a38-122"><a name="Step2"></a>Étape 2 : validation de votre contenu</span><span class="sxs-lookup"><span data-stu-id="a9a38-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="a9a38-123">App Service prend en charge des applications créées dans différents langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="a9a38-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="a9a38-124">Si votre référentiel inclut déjà du contenu, ignorez ce point et passez au point 2 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a9a38-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="a9a38-125">Si votre référentiel n'inclut pas encore de contenu, remplissez-le simplement avec un fichier .html statique comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9a38-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="a9a38-126">À l'aide d'un éditeur de texte, créez un fichier nommé **index.html** à la racine du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="a9a38-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="a9a38-127">Ajoutez le texte suivant dans le fichier index.html et enregistrez ce dernier : *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="a9a38-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="a9a38-128">Dans la ligne de commande, vérifiez que vous êtes bien à la racine de votre référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="a9a38-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="a9a38-129">Puis utilisez la commande suivante pour ajouter des fichiers à votre référentiel :</span><span class="sxs-lookup"><span data-stu-id="a9a38-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="a9a38-130">Ensuite, validez les modifications apportées au référentiel au moyen de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a9a38-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="a9a38-131"><a name="Step3"></a>Étape 3 : activation du référentiel de l’application App Service</span><span class="sxs-lookup"><span data-stu-id="a9a38-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="a9a38-132">Pour activer un référentiel Git pour votre application App Service, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="a9a38-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="a9a38-133">Connectez-vous au [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="a9a38-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="a9a38-134">Dans le panneau de votre application App Service, cliquez sur **Paramètres > Source du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="a9a38-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="a9a38-135">Cliquez successivement sur **Choisir une source**, **Référentiel Git local** et **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9a38-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Référentiel Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="a9a38-137">Si vous configurez un référentiel pour la première fois dans Azure, vous devez créer des informations d’identification de connexion pour ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="a9a38-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="a9a38-138">Vous les utiliserez pour vous connecter au référentiel Azure et pour envoyer les modifications depuis votre référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="a9a38-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="a9a38-139">Dans le panneau de votre application, cliquez sur **Paramètres > Informations d’identification du déploiement**, puis configurez le nom d’utilisateur et le mot de passe de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="a9a38-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="a9a38-140">Quand vous avez terminé, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a9a38-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="a9a38-141"><a name="Step4"></a>Étape 4 : déploiement de votre projet</span><span class="sxs-lookup"><span data-stu-id="a9a38-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="a9a38-142">Pour publier votre application vers App Service à l’aide de Git local, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9a38-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="a9a38-143">Dans le portail Azure, dans le panneau de votre application, cliquez sur **Paramètres > Propriétés** pour l’**URL Git**.</span><span class="sxs-lookup"><span data-stu-id="a9a38-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="a9a38-144">**URL Git** est la référence hors programme vers laquelle vous effectuez le déploiement à partir de votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="a9a38-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="a9a38-145">Vous utiliserez cette URL dans la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="a9a38-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="a9a38-146">À l'aide de la ligne de commande, vérifiez que vous êtes bien à la racine de votre référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="a9a38-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="a9a38-147">Utilisez `git remote` pour ajouter la référence hors programme répertoriée dans **URL Git** à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="a9a38-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="a9a38-148">Votre commande ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a9a38-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="a9a38-149">La commande **remote** ajoute une référence nommée dans un référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="a9a38-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="a9a38-150">Dans cet exemple, une référence nommée « azure » est créée pour le référentiel de votre application web.</span><span class="sxs-lookup"><span data-stu-id="a9a38-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="a9a38-151">Diffusez votre contenu vers App Service à l'aide de la nouvelle référence **azure** distante que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="a9a38-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="a9a38-152">Revenez à votre application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a38-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="a9a38-153">Une entrée de journal de votre dernière diffusion push doit apparaître dans le panneau **Déploiements** .</span><span class="sxs-lookup"><span data-stu-id="a9a38-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="a9a38-154">Cliquez sur le bouton **Parcourir** en haut du panneau de l'application pour vérifier que le contenu a été déployé.</span><span class="sxs-lookup"><span data-stu-id="a9a38-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="a9a38-155"><a name="Step5"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="a9a38-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="a9a38-156">Voici les erreurs ou les problèmes rencontrés couramment lors de l’utilisation de Git pour publier vers une application App Service dans Azure :</span><span class="sxs-lookup"><span data-stu-id="a9a38-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="a9a38-157">**Symptôme**: Impossible d'accéder à '[URL_du_site]' : Impossible de se connecter à [Adresse_scm]</span><span class="sxs-lookup"><span data-stu-id="a9a38-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="a9a38-158">**Cause**: Cette erreur peut se produire si l'application n'est pas opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="a9a38-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="a9a38-159">**Résolution**: démarrez l’application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a38-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="a9a38-160">Le déploiement Git ne fonctionne pas tant que l’application n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a9a38-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="a9a38-161">**Symptôme**: Impossible de résoudre l'hôte « nom_hôte »</span><span class="sxs-lookup"><span data-stu-id="a9a38-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="a9a38-162">**Cause**: Cette erreur peut se produire si les informations d'adresse entrées au moment de la création du référentiel distant « azure » sont incorrectes.</span><span class="sxs-lookup"><span data-stu-id="a9a38-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="a9a38-163">**Résolution** : utilisez la commande `git remote -v` pour répertorier tous les référentiels distants avec l’URL associée.</span><span class="sxs-lookup"><span data-stu-id="a9a38-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="a9a38-164">Vérifiez que l'URL du référentiel distant « azure » est correcte.</span><span class="sxs-lookup"><span data-stu-id="a9a38-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="a9a38-165">Si nécessaire, supprimez et recréez ce référentiel distant au moyen de l’URL correcte.</span><span class="sxs-lookup"><span data-stu-id="a9a38-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="a9a38-166">**Symptôme**: aucune référence en commun, ni spécifiée ; aucune action effectuée.</span><span class="sxs-lookup"><span data-stu-id="a9a38-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="a9a38-167">Perhaps you should specify a branch such as 'master'.</span><span class="sxs-lookup"><span data-stu-id="a9a38-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="a9a38-168">**Cause**: Cette erreur peut se produire si vous ne spécifiez pas de branche au moment de l'exécution d'une opération git push et que vous n'avez pas défini la valeur push.default utilisée par Git.</span><span class="sxs-lookup"><span data-stu-id="a9a38-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="a9a38-169">**Résolution**: Exécutez de nouveau l'opération Push, en spécifiant la branche principale.</span><span class="sxs-lookup"><span data-stu-id="a9a38-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="a9a38-170">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9a38-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="a9a38-171">**Symptôme**: src refspec [nom_branche] ne correspond à aucun élément.</span><span class="sxs-lookup"><span data-stu-id="a9a38-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="a9a38-172">**Cause**: Cette erreur peut se produire si vous tentez d'effectuer une opération Push sur une autre branche que la branche principale sur le référentiel distant « azure ».</span><span class="sxs-lookup"><span data-stu-id="a9a38-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="a9a38-173">**Résolution**: Exécutez de nouveau l'opération Push, en spécifiant la branche principale.</span><span class="sxs-lookup"><span data-stu-id="a9a38-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="a9a38-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9a38-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="a9a38-175">**Symptôme** : échec RPC ; résultat=22, Code HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="a9a38-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="a9a38-176">**Cause** : cette erreur peut se produire si vous essayez de transmettre un dépôt Git volumineux via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a9a38-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="a9a38-177">**Résolution** : modifiez la configuration git sur l’ordinateur local pour agrandir le postBuffer.</span><span class="sxs-lookup"><span data-stu-id="a9a38-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="a9a38-178">**Symptôme**: erreur : des modifications ont été validées dans le référentiel distant, mais votre application web n’a pas été mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a9a38-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="a9a38-179">**Cause**: Cette erreur peut se produire si vous déployez une application Node.js contenant un fichier package.json spécifiant des modules obligatoires supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a9a38-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="a9a38-180">**Résolution**: Des messages supplémentaires contenant « npm ERR!</span><span class="sxs-lookup"><span data-stu-id="a9a38-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="a9a38-181">» doivent être consignés avant cette erreur et peuvent fournir davantage de contexte sur la défaillance.</span><span class="sxs-lookup"><span data-stu-id="a9a38-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="a9a38-182">Voici les causes connues de cette erreur et le message « npm ERR!</span><span class="sxs-lookup"><span data-stu-id="a9a38-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="a9a38-183">» correspondant :</span><span class="sxs-lookup"><span data-stu-id="a9a38-183">message:</span></span>

* <span data-ttu-id="a9a38-184">**Fichier package.json incorrect**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="a9a38-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="a9a38-185">Couldn’t read dependencies.</span><span class="sxs-lookup"><span data-stu-id="a9a38-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="a9a38-186">**Un module natif qui n’a pas de distribution binaire pour Windows**:</span><span class="sxs-lookup"><span data-stu-id="a9a38-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="a9a38-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="a9a38-187">npm ERR!</span></span> <span data-ttu-id="a9a38-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="a9a38-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="a9a38-189">OU</span><span class="sxs-lookup"><span data-stu-id="a9a38-189">OR</span></span>
  * <span data-ttu-id="a9a38-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="a9a38-190">npm ERR!</span></span> <span data-ttu-id="a9a38-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="a9a38-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9a38-192">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a9a38-192">Additional Resources</span></span>
* [<span data-ttu-id="a9a38-193">Documentation Git</span><span class="sxs-lookup"><span data-stu-id="a9a38-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="a9a38-194">Documentation du projet Kudu</span><span class="sxs-lookup"><span data-stu-id="a9a38-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="a9a38-195">Déploiement continu vers Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a9a38-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="a9a38-196">Comment utiliser PowerShell pour Azure</span><span class="sxs-lookup"><span data-stu-id="a9a38-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="a9a38-197">Utilisation des outils en ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a9a38-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="a9a38-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="a9a38-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="a9a38-199">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a9a38-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="a9a38-200">[interface de ligne de commande Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="a9a38-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
