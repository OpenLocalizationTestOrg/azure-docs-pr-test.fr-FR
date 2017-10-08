---
title: "aaaConfigure votre service de gestion des API à l’aide de Git - Azure | Documents Microsoft"
description: "Découvrez comment toosave et configurer votre configuration de service de gestion des API à l’aide de Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="5429f-103">Comment toosave et configurer votre configuration de service de gestion des API à l’aide de Git</span><span class="sxs-lookup"><span data-stu-id="5429f-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="5429f-104">Chaque instance de service de gestion des API gère une base de données de configuration qui contient des informations sur la configuration de hello et des métadonnées pour l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="5429f-105">Modifications peuvent être apportées à l’instance de service toohello en modifiant un paramètre dans le portail de publication hello, à l’aide d’une applet de commande PowerShell ou un appel d’API REST.</span><span class="sxs-lookup"><span data-stu-id="5429f-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="5429f-106">En outre les méthodes toothese, vous pouvez également gérer votre configuration d’instance de service à l’aide de Git, permettant ainsi de scénarios de gestion de service tels que :</span><span class="sxs-lookup"><span data-stu-id="5429f-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="5429f-107">Contrôle de version de la configuration : téléchargez et stockez différentes versions de votre configuration de service</span><span class="sxs-lookup"><span data-stu-id="5429f-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="5429f-108">En bloc les modifications de configuration - apporter des modifications toomultiple des parties de votre configuration du service dans votre référentiel local et intégrer le serveur de toohello arrière de modifications de hello en une seule opération</span><span class="sxs-lookup"><span data-stu-id="5429f-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="5429f-109">Chaîne d’outils Git et les flux de travail - familiers utiliser outils Git de hello et flux de travail que vous connaissez déjà</span><span class="sxs-lookup"><span data-stu-id="5429f-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="5429f-110">Hello suivant schéma montre une vue d’ensemble de tooconfigure de différentes façons hello votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="5429f-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Configurer avec Git][api-management-git-configure]

<span data-ttu-id="5429f-112">Lorsque vous apportez des modifications service tooyour à l’aide du portail de publication hello, applets de commande PowerShell ou hello API REST, vous gérez votre base de données de configuration de service à l’aide de hello `https://{name}.management.azure-api.net` point de terminaison, comme indiqué dans le côté droit de hello du diagramme de hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="5429f-113">à gauche de Hello du diagramme de hello illustre comment vous pouvez gérer votre configuration de service à l’aide de Git et référentiel Git de votre service situé à `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="5429f-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="5429f-114">Hello suit fournit une vue d’ensemble de la gestion de votre instance de service de gestion des API à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="5429f-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="5429f-115">Accéder à la configuration de Git dans votre service</span><span class="sxs-lookup"><span data-stu-id="5429f-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="5429f-116">Enregistrer votre référentiel Git tooyour de base de données de configuration service</span><span class="sxs-lookup"><span data-stu-id="5429f-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="5429f-117">Cloner l’ordinateur local du tooyour dépôt Git hello</span><span class="sxs-lookup"><span data-stu-id="5429f-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="5429f-118">Extraire le référentiel de dernière hello la machine locale de tooyour et validation et push référentiel tooyour arrière de modifications</span><span class="sxs-lookup"><span data-stu-id="5429f-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="5429f-119">Déployer les modifications de hello à partir de votre référentiel dans votre base de données de configuration de service</span><span class="sxs-lookup"><span data-stu-id="5429f-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="5429f-120">Cet article décrit comment tooenable et utiliser Git toomanage votre configuration de service et fournit une référence pour les fichiers de hello et des dossiers dans le référentiel Git de hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="5429f-121">Accéder à la configuration de Git dans votre service</span><span class="sxs-lookup"><span data-stu-id="5429f-121">Access Git configuration in your service</span></span>
<span data-ttu-id="5429f-122">Vous pouvez rapidement afficher l’état hello de votre configuration Git en affichant l’icône de Git hello dans le coin supérieur droit de hello du portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="5429f-123">Dans cet exemple, le message d’état hello indique qu’il n’y a référentiel toohello de modifications non enregistrées.</span><span class="sxs-lookup"><span data-stu-id="5429f-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="5429f-124">Il s’agit, car la base de données de la configuration de service de hello gestion des API n’a pas encore été enregistré toohello référentiel.</span><span class="sxs-lookup"><span data-stu-id="5429f-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![État de Git][api-management-git-icon-enable]

<span data-ttu-id="5429f-126">tooview et configurer vos paramètres de configuration Git, vous pouvez cliquez sur icône Git de hello, ou cliquez sur hello **sécurité** menu et accédez toohello **dépôt de Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="5429f-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![Activer GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="5429f-128">Les secrets ne sont pas définies comme propriétés seront stockées dans le référentiel de hello et restent dans son historique jusqu'à ce que vous désactivent et réactiver l’accès de Git.</span><span class="sxs-lookup"><span data-stu-id="5429f-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="5429f-129">Propriétés fournissent un emplacement sécurisé de toomanage des valeurs de chaîne constante, y compris les clés secrètes, sur toutes les stratégies et de configuration de l’API, vous n’avez pas toostore directement dans vos instructions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="5429f-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="5429f-130">Pour plus d’informations, consultez [comment toouse des propriétés dans les stratégies de gestion des API Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="5429f-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="5429f-131">Pour plus d’informations sur l’activation ou désactivation Git l’accès à l’aide de hello API REST, consultez [activer ou désactiver l’accès Git à l’aide des API REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="5429f-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="5429f-132">référentiel Git de toosave hello service configuration toohello</span><span class="sxs-lookup"><span data-stu-id="5429f-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="5429f-133">première étape de Hello avant le clonage du référentiel de hello est toosave hello capables de référentiel de toohello de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="5429f-134">Cliquez sur **enregistrer la configuration toorepository**.</span><span class="sxs-lookup"><span data-stu-id="5429f-134">Click **Save configuration toorepository**.</span></span>

![Enregistrer la configuration][api-management-save-configuration]

<span data-ttu-id="5429f-136">Apportez les modifications souhaitées sur l’écran de confirmation hello et cliquez sur **Ok** toosave.</span><span class="sxs-lookup"><span data-stu-id="5429f-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Enregistrer la configuration][api-management-save-configuration-confirm]

<span data-ttu-id="5429f-138">Après quelques instants configuration de hello est enregistrée et état de la configuration du référentiel de hello hello s’affiche, y compris la date de hello et l’heure de dernière modification de configuration hello et hello dernière synchronisation entre la configuration du service hello et hello espace de stockage.</span><span class="sxs-lookup"><span data-stu-id="5429f-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![État de la configuration][api-management-configuration-status]

<span data-ttu-id="5429f-140">Une fois la configuration de hello est enregistrée toohello référentiel, il peut être cloné.</span><span class="sxs-lookup"><span data-stu-id="5429f-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="5429f-141">Pour plus d’informations sur la réalisation de cette opération à l’aide de hello API REST, consultez [configuration de la validation d’instantané à l’aide des API REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="5429f-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="5429f-142">ordinateur local de tooclone hello référentiel tooyour</span><span class="sxs-lookup"><span data-stu-id="5429f-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="5429f-143">tooclone un référentiel, vous devez référentiel de tooyour hello URL, un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5429f-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="5429f-144">Hello nom d’utilisateur et les URL sont affichés haut hello Hello **dépôt de Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="5429f-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Clonage Git][api-management-configuration-git-clone]

<span data-ttu-id="5429f-146">mot de passe Hello est généré au bas de hello de hello **dépôt de Configuration** onglet.</span><span class="sxs-lookup"><span data-stu-id="5429f-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Générer un mot de passe][api-management-generate-password]

<span data-ttu-id="5429f-148">toogenerate un mot de passe, commencez par vous assurer que hello **expiration** est défini toohello souhaité date d’expiration et l’heure, puis cliquez sur **générer le jeton**.</span><span class="sxs-lookup"><span data-stu-id="5429f-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Mot de passe][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="5429f-150">Notez ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5429f-150">Make a note of this password.</span></span> <span data-ttu-id="5429f-151">Une fois que vous conservez ce mot de passe de hello de page ne s’affiche plus.</span><span class="sxs-lookup"><span data-stu-id="5429f-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="5429f-152">Hello suivant des exemples d’utilisation hello interpréteur de commandes Git outil à partir de [Git pour Windows](http://www.git-scm.com/downloads) mais vous pouvez utiliser n’importe quel outil Git qui vous sont familières.</span><span class="sxs-lookup"><span data-stu-id="5429f-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="5429f-153">Ouvrir votre outil de Git dans le dossier de votre choix hello et exécutez hello suivant commande tooclone hello git référentiel tooyour ordinateur local, à l’aide de la commande hello fournie par le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="5429f-154">Fournir le nom d’utilisateur hello et le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="5429f-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="5429f-155">Si vous recevez des erreurs, essayez de modifier votre `git clone` commande tooinclude hello nom d’utilisateur, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="5429f-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="5429f-156">Si cela fournit une erreur, essayez de mot de passe hello de commande hello de codage d’URL.</span><span class="sxs-lookup"><span data-stu-id="5429f-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="5429f-157">Un moyen rapide toodo il s’agit de tooopen Visual Studio et de commande suivant de hello problème Bonjour **fenêtre exécution**.</span><span class="sxs-lookup"><span data-stu-id="5429f-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="5429f-158">tooopen hello **fenêtre exécution**, ouvrez la solution ou le projet dans Visual Studio (ou créer une application console vide), puis choisissez **Windows**, **exécution** à partir de Hello **déboguer** menu.</span><span class="sxs-lookup"><span data-stu-id="5429f-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="5429f-159">Utilisez le mot de passe de hello encodé en même temps que votre nom et le référentiel emplacement tooconstruct hello git commande utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5429f-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="5429f-160">Une fois le référentiel de hello est cloné, vous pouvez afficher et utiliser dans votre système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="5429f-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="5429f-161">Pour plus d’informations, consultez [Référence de la structure des fichiers et des dossiers du dépôt Git local](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="5429f-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="5429f-162">tooupdate votre référentiel local avec la configuration de l’instance hello plus récente service</span><span class="sxs-lookup"><span data-stu-id="5429f-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="5429f-163">Si vous effectuez l’instance de service de gestion des API tooyour modifications dans le portail de publication hello ou à l’aide des API REST de hello, vous devez enregistrer ces référentiel toohello de modifications avant que vous pouvez mettre à jour votre référentiel local avec les modifications les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="5429f-164">toodo, cliquez sur **enregistrer la configuration toorepository** sur hello **dépôt de Configuration** onglet dans le portail de publication hello et puis exécutez hello suivant de commande dans votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="5429f-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="5429f-165">Avant d’exécuter `git pull` vous assurer que vous êtes dans le dossier de hello pour votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="5429f-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="5429f-166">Si vous venez d’effectuer hello `git clone` commande, vous devez modifier le référentiel de tooyour hello active en exécutant une commande hello suivante.</span><span class="sxs-lookup"><span data-stu-id="5429f-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="5429f-167">modifications toopush à partir de votre référentiel de serveur toohello dépôt local</span><span class="sxs-lookup"><span data-stu-id="5429f-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="5429f-168">toopush passe de votre référentiel de serveur toohello référentiel local, vous devez valider vos modifications et les transmettre toohello référentiel du serveur.</span><span class="sxs-lookup"><span data-stu-id="5429f-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="5429f-169">toocommit vos modifications, ouvrez votre outil de commande Git, directory toohello du commutateur de votre référentiel local et hello du problème suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="5429f-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="5429f-170">toopush tous hello valide toohello serveur, exécutez hello la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="5429f-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="5429f-171">toodeploy n’importe quelle instance du service de gestion des API service configuration modifications toohello</span><span class="sxs-lookup"><span data-stu-id="5429f-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="5429f-172">Une fois vos modifications locales sont validées et envoyées toohello référentiel du serveur, vous pouvez les déployer instance de service de gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="5429f-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Déployer][api-management-configuration-deploy]

<span data-ttu-id="5429f-174">Pour plus d’informations sur la réalisation de cette opération à l’aide de hello API REST, consultez [Git de déploiement change tooconfiguration de base de données à l’aide des API REST de hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="5429f-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="5429f-175">Référence de la structure des fichiers et des dossiers du dépôt Git local</span><span class="sxs-lookup"><span data-stu-id="5429f-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="5429f-176">Hello fichiers et dossiers dans le référentiel git local de hello contiennent des informations de configuration de hello sur l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="5429f-177">Item</span><span class="sxs-lookup"><span data-stu-id="5429f-177">Item</span></span> | <span data-ttu-id="5429f-178">Description</span><span class="sxs-lookup"><span data-stu-id="5429f-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5429f-179">Dossier api-management racine</span><span class="sxs-lookup"><span data-stu-id="5429f-179">root api-management folder</span></span> |<span data-ttu-id="5429f-180">Contient la configuration de niveau supérieur pour l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="5429f-181">Dossier apis</span><span class="sxs-lookup"><span data-stu-id="5429f-181">apis folder</span></span> |<span data-ttu-id="5429f-182">Contient la configuration hello pour les API de hello dans l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="5429f-183">Dossier groups</span><span class="sxs-lookup"><span data-stu-id="5429f-183">groups folder</span></span> |<span data-ttu-id="5429f-184">Contient la configuration de hello pour les groupes de hello dans l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="5429f-185">Dossier policies</span><span class="sxs-lookup"><span data-stu-id="5429f-185">policies folder</span></span> |<span data-ttu-id="5429f-186">Contient des stratégies de hello dans l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="5429f-187">Dossier portalStyles</span><span class="sxs-lookup"><span data-stu-id="5429f-187">portalStyles folder</span></span> |<span data-ttu-id="5429f-188">Contient la configuration hello pour les personnalisations de portail de développement hello dans l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="5429f-189">Dossier products</span><span class="sxs-lookup"><span data-stu-id="5429f-189">products folder</span></span> |<span data-ttu-id="5429f-190">Contient la configuration hello pour les produits hello dans l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="5429f-191">Dossier templates</span><span class="sxs-lookup"><span data-stu-id="5429f-191">templates folder</span></span> |<span data-ttu-id="5429f-192">Contient la configuration hello pour les modèles de messagerie hello dans l’instance de service hello</span><span class="sxs-lookup"><span data-stu-id="5429f-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="5429f-193">Chaque dossier peut contenir un ou plusieurs fichiers et, dans certains cas, un ou plusieurs dossiers, par exemple un dossier par API, produit ou groupe.</span><span class="sxs-lookup"><span data-stu-id="5429f-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="5429f-194">fichiers Hello dans chaque dossier sont spécifiques pour le type d’entité hello décrite par le nom du dossier hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="5429f-195">Type de fichier</span><span class="sxs-lookup"><span data-stu-id="5429f-195">File type</span></span> | <span data-ttu-id="5429f-196">Objectif</span><span class="sxs-lookup"><span data-stu-id="5429f-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="5429f-197">json</span><span class="sxs-lookup"><span data-stu-id="5429f-197">json</span></span> |<span data-ttu-id="5429f-198">Informations de configuration sur l’entité correspondante de hello</span><span class="sxs-lookup"><span data-stu-id="5429f-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="5429f-199">html</span><span class="sxs-lookup"><span data-stu-id="5429f-199">html</span></span> |<span data-ttu-id="5429f-200">Description de l’entité hello, souvent affiché dans le portail des développeurs hello</span><span class="sxs-lookup"><span data-stu-id="5429f-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="5429f-201">xml</span><span class="sxs-lookup"><span data-stu-id="5429f-201">xml</span></span> |<span data-ttu-id="5429f-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="5429f-202">Policy statements</span></span> |
| <span data-ttu-id="5429f-203">css</span><span class="sxs-lookup"><span data-stu-id="5429f-203">css</span></span> |<span data-ttu-id="5429f-204">Feuilles de style pour la personnalisation du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="5429f-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="5429f-205">Ces fichiers peuvent être créés, supprimés, modifiés et gérés sur votre système de fichiers local, et les modifications de hello déployées toohello arrière de votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="5429f-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="5429f-206">Bonjour entités suivantes ne figurent pas dans le référentiel Git de hello et ne peut pas être configurées à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="5429f-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="5429f-207">Utilisateurs</span><span class="sxs-lookup"><span data-stu-id="5429f-207">Users</span></span>
> * <span data-ttu-id="5429f-208">Abonnements</span><span class="sxs-lookup"><span data-stu-id="5429f-208">Subscriptions</span></span>
> * <span data-ttu-id="5429f-209">Propriétés</span><span class="sxs-lookup"><span data-stu-id="5429f-209">Properties</span></span>
> * <span data-ttu-id="5429f-210">Entités du portail des développeur autres que les styles</span><span class="sxs-lookup"><span data-stu-id="5429f-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="5429f-211">Dossier api-management racine</span><span class="sxs-lookup"><span data-stu-id="5429f-211">Root api-management folder</span></span>
<span data-ttu-id="5429f-212">racine de Hello `api-management` dossier contient un `configuration.json` fichier qui contient le niveau supérieur d’informations sur l’instance de service hello Bonjour suivant le format.</span><span class="sxs-lookup"><span data-stu-id="5429f-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="5429f-213">Hello les quatre premiers paramètres (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, et `UserRegistrationTermsConsentRequired`) mapper toohello suivant les paramètres de hello **identités** onglet Bonjour **sécurité** section.</span><span class="sxs-lookup"><span data-stu-id="5429f-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="5429f-214">Paramètre d’identité</span><span class="sxs-lookup"><span data-stu-id="5429f-214">Identity setting</span></span> | <span data-ttu-id="5429f-215">Mappe trop</span><span class="sxs-lookup"><span data-stu-id="5429f-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="5429f-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="5429f-216">RegistrationEnabled</span></span> |<span data-ttu-id="5429f-217">**Les utilisateurs anonymes toosign dans la page de redirection** case à cocher</span><span class="sxs-lookup"><span data-stu-id="5429f-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="5429f-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="5429f-218">UserRegistrationTerms</span></span> |<span data-ttu-id="5429f-219">**Conditions d’utilisation liées à l’inscription de l’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="5429f-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="5429f-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="5429f-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="5429f-221">**Afficher les conditions d’utilisation dans la page d’abonnement**</span><span class="sxs-lookup"><span data-stu-id="5429f-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="5429f-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="5429f-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="5429f-223">**Exiger le consentement**</span><span class="sxs-lookup"><span data-stu-id="5429f-223">**Require consent** checkbox</span></span> |

![Paramètres d’identité][api-management-identity-settings]

<span data-ttu-id="5429f-225">Hello quatre paramètres (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, et `DelegationValidationKey`) mapper toohello suivant les paramètres de hello **délégation** onglet Bonjour **sécurité** section.</span><span class="sxs-lookup"><span data-stu-id="5429f-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="5429f-226">Paramètre de délégation</span><span class="sxs-lookup"><span data-stu-id="5429f-226">Delegation setting</span></span> | <span data-ttu-id="5429f-227">Mappe trop</span><span class="sxs-lookup"><span data-stu-id="5429f-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="5429f-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="5429f-228">DelegationEnabled</span></span> |<span data-ttu-id="5429f-229">Case à cocher **Déléguer la connexion et l’inscription**</span><span class="sxs-lookup"><span data-stu-id="5429f-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="5429f-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="5429f-230">DelegationUrl</span></span> |<span data-ttu-id="5429f-231">**URL de point de terminaison de la délégation**</span><span class="sxs-lookup"><span data-stu-id="5429f-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="5429f-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="5429f-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="5429f-233">**Déléguer l’abonnement au produit**</span><span class="sxs-lookup"><span data-stu-id="5429f-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="5429f-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="5429f-234">DelegationValidationKey</span></span> |<span data-ttu-id="5429f-235">**Déléguer la clé de validation**</span><span class="sxs-lookup"><span data-stu-id="5429f-235">**Delegate Validation Key** textbox</span></span> |

![Paramètres de délégation][api-management-delegation-settings]

<span data-ttu-id="5429f-237">Hello paramètre final, `$ref-policy`, mappe le fichier d’instructions de la stratégie globale toohello pour l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="5429f-238">Dossier apis</span><span class="sxs-lookup"><span data-stu-id="5429f-238">apis folder</span></span>
<span data-ttu-id="5429f-239">Hello `apis` dossier contient un dossier pour chaque API dans l’instance de service hello qui contient les éléments suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="5429f-240">`apis\<api name>\configuration.json`-Cette configuration hello pour hello API et contient des informations sur l’URL du service principal hello et les opérations de hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="5429f-241">Il s’agit de hello mêmes informations qui doit être retournées si vous étiez toocall [obtenir une API spécifique](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) avec `export=true` dans `application/json` format.</span><span class="sxs-lookup"><span data-stu-id="5429f-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="5429f-242">`apis\<api name>\api.description.html`-Il s’agit de description hello Hello API et correspond toohello `description` propriété Hello [entité API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="5429f-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="5429f-243">`apis\<api name>\operations\`-ce dossier contient `<operation name>.description.html` fichiers que les opérations de mappage toohello dans hello API.</span><span class="sxs-lookup"><span data-stu-id="5429f-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="5429f-244">Chaque fichier contient la description hello d’une seule opération Bonjour API qui mappe toohello `description` propriété Hello [entité opération](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) Bonjour API REST.</span><span class="sxs-lookup"><span data-stu-id="5429f-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="5429f-245">Dossier groups</span><span class="sxs-lookup"><span data-stu-id="5429f-245">groups folder</span></span>
<span data-ttu-id="5429f-246">Hello `groups` dossier contient un dossier pour chaque groupe défini dans l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="5429f-247">`groups\<group name>\configuration.json`-configuration hello pour le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="5429f-248">Il s’agit de hello mêmes informations qui doit être retournées si vous étiez toocall hello [obtenir un groupe spécifique](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) opération.</span><span class="sxs-lookup"><span data-stu-id="5429f-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="5429f-249">`groups\<group name>\description.html`-Il s’agit de description hello du groupe de hello et correspond toohello `description` propriété Hello [groupe entité](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="5429f-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="5429f-250">Dossier policies</span><span class="sxs-lookup"><span data-stu-id="5429f-250">policies folder</span></span>
<span data-ttu-id="5429f-251">Hello `policies` dossier contient des instructions de stratégie hello pour votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="5429f-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="5429f-252">`policies\global.xml` : contient les stratégies définies dans l’étendue globale de votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="5429f-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="5429f-253">`policies\apis\<api name>\` : si des stratégies sont définies à l’échelle de l’API, elles se trouvent dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="5429f-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="5429f-254">`policies\apis\<api name>\<operation name>\`dossier - si vous disposez de toutes les stratégies définies dans le cadre de l’opération, elles sont contenues dans ce dossier dans `<operation name>.xml` fichiers qui mappent des instructions de stratégie toohello pour chaque opération.</span><span class="sxs-lookup"><span data-stu-id="5429f-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="5429f-255">`policies\products\`-Si vous disposez de toutes les stratégies définies au niveau de portée du produit, elles sont contenues dans ce dossier, qui contient `<product name>.xml` fichiers qui mappent toohello les instructions de stratégie pour chaque produit.</span><span class="sxs-lookup"><span data-stu-id="5429f-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="5429f-256">Dossier portalStyles</span><span class="sxs-lookup"><span data-stu-id="5429f-256">portalStyles folder</span></span>
<span data-ttu-id="5429f-257">Hello `portalStyles` dossier contient les feuilles de style et de configuration pour les personnalisations de portail de développement pour l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="5429f-258">`portalStyles\configuration.json`-contient les noms de hello hello de feuilles de style utilisées par le portail des développeurs hello</span><span class="sxs-lookup"><span data-stu-id="5429f-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="5429f-259">`portalStyles\<style name>.css`-chaque `<style name>.css` fichier contient des styles pour le portail des développeurs hello (`Preview.css` et `Production.css` par défaut).</span><span class="sxs-lookup"><span data-stu-id="5429f-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="5429f-260">Dossier products</span><span class="sxs-lookup"><span data-stu-id="5429f-260">products folder</span></span>
<span data-ttu-id="5429f-261">Hello `products` dossier contient un dossier pour chaque produit défini dans l’instance de service hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="5429f-262">`products\<product name>\configuration.json`-configuration hello pour le produit de hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="5429f-263">Il s’agit de hello mêmes informations qui doit être retournées si vous étiez toocall hello [obtenir un produit spécifique](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) opération.</span><span class="sxs-lookup"><span data-stu-id="5429f-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="5429f-264">`products\<product name>\product.description.html`-Il s’agit de description hello du produit de hello et correspond toohello `description` propriété Hello [entité product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) Bonjour API REST.</span><span class="sxs-lookup"><span data-stu-id="5429f-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="5429f-265">modèles</span><span class="sxs-lookup"><span data-stu-id="5429f-265">templates</span></span>
<span data-ttu-id="5429f-266">Hello `templates` dossier contient la configuration de hello [modèles de messagerie](api-management-howto-configure-notifications.md) hello des instances de service.</span><span class="sxs-lookup"><span data-stu-id="5429f-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="5429f-267">`<template name>\configuration.json`-configuration hello hello modèle de courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="5429f-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="5429f-268">`<template name>\body.html`-corps hello du modèle d’e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="5429f-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5429f-269">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5429f-269">Next steps</span></span>
<span data-ttu-id="5429f-270">Pour plus d’informations sur les autres façons de toomanage votre instance de service, consultez :</span><span class="sxs-lookup"><span data-stu-id="5429f-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="5429f-271">Gérer votre instance de service à l’aide de hello suivant d’applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="5429f-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="5429f-272">Référence sur les applets de commande PowerShell de déploiement des services</span><span class="sxs-lookup"><span data-stu-id="5429f-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="5429f-273">Référence sur les applets de commande PowerShell de gestion des services</span><span class="sxs-lookup"><span data-stu-id="5429f-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="5429f-274">Gérer votre instance de service dans le portail de publication hello</span><span class="sxs-lookup"><span data-stu-id="5429f-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="5429f-275">Gérer votre première API</span><span class="sxs-lookup"><span data-stu-id="5429f-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="5429f-276">Gérer votre instance de service à l’aide des API REST de hello</span><span class="sxs-lookup"><span data-stu-id="5429f-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="5429f-277">Référence de l’API REST Gestion des API</span><span class="sxs-lookup"><span data-stu-id="5429f-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="5429f-278">Regarder une vidéo de présentation</span><span class="sxs-lookup"><span data-stu-id="5429f-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




