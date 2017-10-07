---
title: "aaaLocal déploiement Git tooAzure du Service d’applications"
description: "Découvrez comment tooAzure tooenable local Git déploiement du Service d’applications."
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
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="2f8f4-103">TooAzure déploiement Git local du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="2f8f4-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="2f8f4-104">Ce didacticiel vous montre comment toodeploy votre application trop[Azure App Service] à partir d’un référentiel Git sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="2f8f4-105">Service d’applications prend en charge cette approche avec hello **Git Local** option de déploiement dans hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="2f8f4-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="2f8f4-106">Nombre de commandes Git de hello décrits dans cet article sont exécutées automatiquement lors de la création d’une application de Service d’applications à l’aide de hello [Interface de ligne de commande Azure] comme décrit [ici](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f8f4-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2f8f4-107">Prerequisites</span></span>
<span data-ttu-id="2f8f4-108">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2f8f4-109">Git.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-109">Git.</span></span> <span data-ttu-id="2f8f4-110">Vous pouvez télécharger le fichier binaire d’installation hello [ici](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="2f8f4-111">Connaissances élémentaires de Git.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="2f8f4-112">Un compte Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f4-112">A Microsoft Azure account.</span></span> <span data-ttu-id="2f8f4-113">Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="2f8f4-114">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="2f8f4-115">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="2f8f4-116"><a name="Step1"></a>Étape 1 : création d’un référentiel local</span><span class="sxs-lookup"><span data-stu-id="2f8f4-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="2f8f4-117">Effectuer hello suivant de tâches toocreate un référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="2f8f4-118">Lancez un outil de ligne de commande, comme **GitBash** (Windows) ou **Bash** (Unix Shell).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="2f8f4-119">Sur les systèmes OS X, vous pouvez accéder hello de ligne de commande via hello **Terminal** application.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="2f8f4-120">Accédez répertoire toohello où toodeploy de contenu hello serait localisé.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="2f8f4-121">Hello suivant commande tooinitialize un référentiel Git, utilisez :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="2f8f4-122"><a name="Step2"></a>Étape 2 : validation de votre contenu</span><span class="sxs-lookup"><span data-stu-id="2f8f4-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="2f8f4-123">App Service prend en charge des applications créées dans différents langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="2f8f4-124">Si votre référentiel contient déjà le contenu ignorer ce point et déplacer toopoint 2 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="2f8f4-125">Si votre référentiel n'inclut pas encore de contenu, remplissez-le simplement avec un fichier .html statique comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="2f8f4-126">À l’aide d’un éditeur de texte, créez un nouveau fichier nommé **index.html** à racine hello du référentiel Git de hello</span><span class="sxs-lookup"><span data-stu-id="2f8f4-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="2f8f4-127">Ajouter hello après le texte comme contenu hello pour hello index.html fichier et enregistrez-le : *Hello Git !*</span><span class="sxs-lookup"><span data-stu-id="2f8f4-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="2f8f4-128">À partir de hello de ligne de commande, vérifiez que vous êtes sous racine hello de votre référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="2f8f4-129">Utilisez ensuite hello suivant du référentiel de commande tooadd fichiers tooyour :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="2f8f4-130">Ensuite, la validation hello modifications toohello référentiel à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="2f8f4-131"><a name="Step3"></a>Étape 3 : Activer hello référentiel d’application de Service d’applications</span><span class="sxs-lookup"><span data-stu-id="2f8f4-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="2f8f4-132">Effectuer hello suivant les étapes tooenable un référentiel Git pour votre application de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="2f8f4-133">Connectez-vous à toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="2f8f4-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="2f8f4-134">Dans le panneau de votre application App Service, cliquez sur **Paramètres > Source du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="2f8f4-135">Cliquez successivement sur **Choisir une source**, **Référentiel Git local** et **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Référentiel Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="2f8f4-137">S’il s’agit de votre premier paramètre de temps un référentiel dans Azure, vous devez toocreate informations d’identification pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="2f8f4-138">Vous allez utiliser les toolog dans hello référentiel Azure et publier des modifications à partir de votre référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="2f8f4-139">Dans le panneau de votre application, cliquez sur **Paramètres > Informations d’identification du déploiement**, puis configurez le nom d’utilisateur et le mot de passe de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="2f8f4-140">Quand vous avez terminé, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="2f8f4-141"><a name="Step4"></a>Étape 4 : déploiement de votre projet</span><span class="sxs-lookup"><span data-stu-id="2f8f4-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="2f8f4-142">Utilisez hello suivant les étapes toopublish votre tooApp app Service à l’aide de Git Local.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="2f8f4-143">Dans le panneau de votre application Bonjour portail Azure, cliquez sur **Paramètres > Propriétés** pour hello **URL Git**.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="2f8f4-144">**URL GIT** est hello référence distante toodeploy toofrom votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="2f8f4-145">Vous utiliserez cette URL de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="2f8f4-146">Hello de ligne de commande, vérifiez que vous êtes dans la racine de hello de votre référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="2f8f4-147">Utilisez `git remote` tooadd hello informations référence à distance répertorié dans **URL Git** à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="2f8f4-148">Votre commande doit ressembler similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="2f8f4-149">Hello **distant** commande ajoute un référentiel distant tooa de référence nommée.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="2f8f4-150">Dans cet exemple, une référence nommée « azure » est créée pour le référentiel de votre application web.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="2f8f4-151">Push de votre contenu tooApp Service à l’aide de nouveau hello **azure** distant vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="2f8f4-152">Revenir en arrière application tooyour Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="2f8f4-153">Une entrée de journal de votre publication la plus récente doit être affichée dans hello **déploiements** panneau.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="2f8f4-154">Cliquez sur hello **Parcourir** bouton haut hello hello tooverify à panneau de l’application hello contenu a été déployé.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="2f8f4-155"><a name="Step5"></a>Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="2f8f4-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="2f8f4-156">Hello Voici les erreurs ou des problèmes couramment rencontrés lors de l’utilisation de Git toopublish tooan application de Service de l’application dans Azure :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="2f8f4-157">**Symptôme**: Impossible de tooaccess '[siteURL]' : Échec de tooconnect trop [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="2f8f4-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="2f8f4-158">**Cause**: cette erreur peut se produire si l’application hello n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="2f8f4-159">**Résolution**: application hello de démarrage Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="2f8f4-160">Déploiement GIT ne fonctionne pas, sauf si l’application hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="2f8f4-161">**Symptôme**: Impossible de résoudre l'hôte « nom_hôte »</span><span class="sxs-lookup"><span data-stu-id="2f8f4-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="2f8f4-162">**Cause**: cette erreur peut se produire si les informations d’adresse hello entré lors de la création hello 'azure' distant était incorrect.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="2f8f4-163">**Résolution**: hello d’utilisation `git remote -v` commande toolist toutes les bases de données distantes, ainsi que les URL hello associé.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="2f8f4-164">Vérifiez que les URL hello hello 'azure' distant est correct.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="2f8f4-165">Si nécessaire, supprimez et recréez ce distant à l’aide de l’URL appropriée hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="2f8f4-166">**Symptôme**: aucune référence en commun, ni spécifiée ; aucune action effectuée.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="2f8f4-167">Perhaps you should specify a branch such as 'master'.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="2f8f4-168">**Cause**: cette erreur peut se produire si vous ne pas spécifier une branche lors de l’exécution d’une opération de diffusion de git et ont la valeur not set hello push.default utilisé par Git.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="2f8f4-169">**Résolution**: effectuer l’opération hello push configuration de la branche maître hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="2f8f4-170">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="2f8f4-171">**Symptôme**: src refspec [nom_branche] ne correspond à aucun élément.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="2f8f4-172">**Cause**: cette erreur peut se produire si vous essayez de branche de tooa toopush autres que master sur hello 'azure' à distance.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="2f8f4-173">**Résolution**: effectuer l’opération hello push configuration de la branche maître hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="2f8f4-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="2f8f4-175">**Symptôme** : échec RPC ; résultat=22, Code HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="2f8f4-176">**Cause**: cette erreur peut se produire si vous essayez de toopush un référentiel git volumineux sur HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="2f8f4-177">**Résolution**: modifier la configuration git hello sur hello ordinateur local toomake hello post-mémoire tampon plus grande</span><span class="sxs-lookup"><span data-stu-id="2f8f4-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="2f8f4-178">**Symptôme**: erreur - référentiel tooremote validée de modifications, mais votre application web ne pas mis à jour.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="2f8f4-179">**Cause**: Cette erreur peut se produire si vous déployez une application Node.js contenant un fichier package.json spécifiant des modules obligatoires supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="2f8f4-180">**Résolution**: Des messages supplémentaires contenant « npm ERR!</span><span class="sxs-lookup"><span data-stu-id="2f8f4-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="2f8f4-181">doit être connecté toothis préalable erreur et peut fournir un contexte supplémentaire en cas d’échec hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="2f8f4-182">suivant de Hello est connues des causes de cette erreur et hello correspondant 'npm ERR !'</span><span class="sxs-lookup"><span data-stu-id="2f8f4-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="2f8f4-183">» correspondant :</span><span class="sxs-lookup"><span data-stu-id="2f8f4-183">message:</span></span>

* <span data-ttu-id="2f8f4-184">**Fichier package.json incorrect**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="2f8f4-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="2f8f4-185">Couldn’t read dependencies.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="2f8f4-186">**Native module that does not have a binary distribution for Windows**:</span><span class="sxs-lookup"><span data-stu-id="2f8f4-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="2f8f4-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="2f8f4-187">npm ERR!</span></span> <span data-ttu-id="2f8f4-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="2f8f4-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="2f8f4-189">OU</span><span class="sxs-lookup"><span data-stu-id="2f8f4-189">OR</span></span>
  * <span data-ttu-id="2f8f4-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="2f8f4-190">npm ERR!</span></span> <span data-ttu-id="2f8f4-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="2f8f4-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f8f4-192">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2f8f4-192">Additional Resources</span></span>
* [<span data-ttu-id="2f8f4-193">Documentation Git</span><span class="sxs-lookup"><span data-stu-id="2f8f4-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="2f8f4-194">Documentation du projet Kudu</span><span class="sxs-lookup"><span data-stu-id="2f8f4-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="2f8f4-195">TooAzure de déploiement d’un Service d’applications</span><span class="sxs-lookup"><span data-stu-id="2f8f4-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="2f8f4-196">Comment toouse PowerShell pour Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f4-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="2f8f4-197">Comment toouse hello Interface de ligne de commande de Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f4-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Interface de ligne de commande Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
