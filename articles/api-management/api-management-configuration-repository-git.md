---
title: "Configurer le service Gestion des API à l’aide de Git - Azure | Microsoft Docs"
description: "Découvrez comment enregistrer et configurer votre configuration du service Gestion des API à l’aide de Git"
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
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="89002-103">Comment enregistrer et configurer votre configuration du service Gestion des API à l’aide de Git</span><span class="sxs-lookup"><span data-stu-id="89002-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="89002-104">Chaque instance du service Gestion des API gère une base de données de configuration qui contient des informations sur la configuration et les métadonnées de cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="89002-105">Vous pouvez modifier l’instance de service en ajustant un paramètre dans le portail de publication, en utilisant une applet de commande PowerShell ou en effectuant un appel API REST.</span><span class="sxs-lookup"><span data-stu-id="89002-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="89002-106">Outre ces méthodes, vous pouvez gérer votre configuration d’instance de service à l’aide de Git, notamment dans le cadre des scénarios de gestion de service suivants :</span><span class="sxs-lookup"><span data-stu-id="89002-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="89002-107">Contrôle de version de la configuration : téléchargez et stockez différentes versions de votre configuration de service</span><span class="sxs-lookup"><span data-stu-id="89002-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="89002-108">Modifications en bloc de la configuration : apportez des modifications à plusieurs parties de votre configuration de service dans votre dépôt local et intégrez les modifications au serveur en une seule opération</span><span class="sxs-lookup"><span data-stu-id="89002-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="89002-109">Chaîne d’outils et flux de travail Git familiers : utilisez les flux de travail et les outils Git qui vous sont déjà familiers</span><span class="sxs-lookup"><span data-stu-id="89002-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="89002-110">Le diagramme suivant montre une vue d’ensemble des différentes façons de configurer votre instance du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="89002-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Configurer avec Git][api-management-git-configure]

<span data-ttu-id="89002-112">Quand vous apportez des modifications à votre service en utilisant le portail de publication, les applets de commande PowerShell ou l’API REST, vous gérez votre base de données de configuration de service à l’aide du point de terminaison `https://{name}.management.azure-api.net` , comme indiqué sur le côté droit du diagramme.</span><span class="sxs-lookup"><span data-stu-id="89002-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="89002-113">Le côté gauche du diagramme illustre comment vous pouvez gérer votre configuration de service à l’aide de Git et du dépôt Git pour votre service situé à l’adresse `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="89002-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="89002-114">Les étapes suivantes fournissent une vue d’ensemble de la gestion de votre instance du service Gestion des API à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="89002-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="89002-115">Accéder à la configuration de Git dans votre service</span><span class="sxs-lookup"><span data-stu-id="89002-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="89002-116">Enregistrer votre base de données de configuration de service dans votre dépôt Git</span><span class="sxs-lookup"><span data-stu-id="89002-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="89002-117">Cloner le dépôt Git sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="89002-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="89002-118">Récupérer le dernier dépôt sur votre ordinateur local, puis valider les modifications et les transférer vers votre dépôt</span><span class="sxs-lookup"><span data-stu-id="89002-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="89002-119">Déployer les modifications depuis votre dépôt dans votre base de données de configuration de service</span><span class="sxs-lookup"><span data-stu-id="89002-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="89002-120">Cet article décrit comment activer et utiliser Git pour gérer votre configuration de service et fournit une référence pour les fichiers et dossiers dans le dépôt Git.</span><span class="sxs-lookup"><span data-stu-id="89002-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="89002-121">Accéder à la configuration de Git dans votre service</span><span class="sxs-lookup"><span data-stu-id="89002-121">Access Git configuration in your service</span></span>
<span data-ttu-id="89002-122">Vous pouvez rapidement vérifier l’état de votre configuration Git en affichant l’icône Git dans le coin supérieur droit du portail de publication.</span><span class="sxs-lookup"><span data-stu-id="89002-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="89002-123">Dans cet exemple, le message d’état indique que des modifications apportées au dépôt n’ont pas été enregistrées.</span><span class="sxs-lookup"><span data-stu-id="89002-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="89002-124">Cela est dû au fait que la base de données de configuration du service Gestion des API n’a pas encore été enregistrée dans le dépôt.</span><span class="sxs-lookup"><span data-stu-id="89002-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![État de Git][api-management-git-icon-enable]

<span data-ttu-id="89002-126">Pour afficher et configurer vos paramètres de configuration Git, cliquez sur l’icône Git, ou cliquez dans le menu **Sécurité** et accédez à l’onglet **Dépôt de configuration**.</span><span class="sxs-lookup"><span data-stu-id="89002-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Activer GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="89002-128">Tous les secrets qui ne sont pas définis en tant que propriétés sont stockés dans le dépôt et demeurent dans son historique jusqu’à ce que vous désactiviez et réactiviez l’accès à Git.</span><span class="sxs-lookup"><span data-stu-id="89002-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="89002-129">Les propriétés fournissent un emplacement sécurisé pour gérer les valeurs de chaîne constante, notamment les secrets, dans toutes les stratégies et configurations de l’API ; vous n’êtes donc pas obligé de les stocker directement dans les instructions de votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="89002-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="89002-130">Pour plus d’informations, consultez [Utilisation des propriétés dans les stratégies Gestion des API Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="89002-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="89002-131">Pour plus d’informations sur l’activation ou la désactivation de l’accès à Git en utilisant l’API REST, consultez [Activer ou désactiver l’accès à Git à l’aide de l’API REST](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="89002-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="89002-132">Pour enregistrer la configuration du service dans le dépôt Git</span><span class="sxs-lookup"><span data-stu-id="89002-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="89002-133">La première étape avant le clonage du dépôt consiste à enregistrer l’état actuel de la configuration du service dans le dépôt.</span><span class="sxs-lookup"><span data-stu-id="89002-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="89002-134">Cliquez sur **Enregistrer la configuration dans le dépôt**.</span><span class="sxs-lookup"><span data-stu-id="89002-134">Click **Save configuration to repository**.</span></span>

![Enregistrer la configuration][api-management-save-configuration]

<span data-ttu-id="89002-136">Apportez les modifications souhaitées dans l’écran de confirmation, puis cliquez sur **OK** pour les enregistrer.</span><span class="sxs-lookup"><span data-stu-id="89002-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Enregistrer la configuration][api-management-save-configuration-confirm]

<span data-ttu-id="89002-138">Après quelques instants, la configuration est enregistrée, et l’état de configuration du dépôt est affiché, y compris la date et l’heure de la dernière modification de la configuration et de la dernière synchronisation entre la configuration du service et le dépôt.</span><span class="sxs-lookup"><span data-stu-id="89002-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![État de la configuration][api-management-configuration-status]

<span data-ttu-id="89002-140">Une fois la configuration enregistrée dans le dépôt, elle peut être clonée.</span><span class="sxs-lookup"><span data-stu-id="89002-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="89002-141">Pour plus d’informations sur l’exécution de cette opération avec l’API REST, consultez [Valider l’instantané de configuration à l’aide de l’API REST](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="89002-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="89002-142">Pour cloner le dépôt sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="89002-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="89002-143">Pour cloner un dépôt, vous avez besoin de l’URL de votre dépôt, d’un nom d’utilisateur et d’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="89002-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="89002-144">Le nom d’utilisateur et l’URL sont affichés en haut de l’onglet **Dépôt de configuration** .</span><span class="sxs-lookup"><span data-stu-id="89002-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Clonage Git][api-management-configuration-git-clone]

<span data-ttu-id="89002-146">Le mot de passe est généré en bas de l’onglet **Dépôt de configuration** .</span><span class="sxs-lookup"><span data-stu-id="89002-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Générer un mot de passe][api-management-generate-password]

<span data-ttu-id="89002-148">Pour générer un mot de passe, vérifiez d’abord que le champ **Expiration** est défini sur la date et l’heure d’expiration souhaitées, puis cliquez sur **Générer un jeton**.</span><span class="sxs-lookup"><span data-stu-id="89002-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Mot de passe][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="89002-150">Notez ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="89002-150">Make a note of this password.</span></span> <span data-ttu-id="89002-151">Une fois que vous quittez cette page, le mot de passe ne s’affiche plus.</span><span class="sxs-lookup"><span data-stu-id="89002-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="89002-152">Les exemples suivants utilisent l’outil Git Bash de [Git pour Windows](http://www.git-scm.com/downloads) , mais vous pouvez utiliser n’importe quel outil Git auquel vous êtes habitué.</span><span class="sxs-lookup"><span data-stu-id="89002-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="89002-153">Ouvrez votre outil Git dans le dossier de votre choix et exécutez la commande suivante pour cloner le dépôt git sur votre ordinateur local, à l’aide de la commande fournie par le portail de publication.</span><span class="sxs-lookup"><span data-stu-id="89002-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="89002-154">Quand vous y êtes invité, fournissez le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="89002-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="89002-155">En cas d’erreur, essayez de modifier votre commande `git clone` pour y inclure le nom d’utilisateur et le mot de passe, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="89002-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="89002-156">En cas d’erreur, essayez d’appliquer un encodage URL à la partie mot de passe de la commande.</span><span class="sxs-lookup"><span data-stu-id="89002-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="89002-157">Pour effectuer cette opération rapidement, vous pouvez ouvrir Visual Studio et exécuter la commande ci-dessous dans la **Fenêtre Exécution**.</span><span class="sxs-lookup"><span data-stu-id="89002-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="89002-158">Pour ouvrir la **Fenêtre Exécution**, ouvrez une solution ou un projet dans Visual Studio (ou créez une application console vide), puis choisissez **Fenêtres**, **Exécution** dans le menu **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="89002-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="89002-159">Pour construire la commande git, utilisez le mot de passe codé, avec votre nom d’utilisateur et l’emplacement du dépôt.</span><span class="sxs-lookup"><span data-stu-id="89002-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="89002-160">Une fois le dépôt cloné, vous pouvez l’afficher et l’utiliser dans votre système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="89002-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="89002-161">Pour plus d’informations, consultez [Référence de la structure des fichiers et des dossiers du dépôt Git local](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="89002-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="89002-162">Pour mettre à jour votre dépôt local avec la dernière configuration de l’instance du service</span><span class="sxs-lookup"><span data-stu-id="89002-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="89002-163">Si vous apportez des modifications à votre instance du service Gestion des API dans le portail de publication ou à l’aide de l’API REST, vous devez enregistrer ces modifications dans le dépôt pour pouvoir mettre à jour votre dépôt local avec les dernières modifications.</span><span class="sxs-lookup"><span data-stu-id="89002-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="89002-164">Pour ce faire, cliquez sur **Enregistrer la configuration dans le dépôt** sous l’onglet **Dépôt de configuration** dans le portail de publication, puis exécutez la commande suivante dans votre dépôt local.</span><span class="sxs-lookup"><span data-stu-id="89002-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="89002-165">Avant d’exécuter `git pull` , vérifiez que vous vous trouvez dans le dossier de votre dépôt local.</span><span class="sxs-lookup"><span data-stu-id="89002-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="89002-166">Si vous venez d’exécuter la commande `git clone` , vous devez accéder au répertoire de votre dépôt en exécutant une commande semblable à la suivante.</span><span class="sxs-lookup"><span data-stu-id="89002-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="89002-167">Pour transférer les modifications depuis votre dépôt local vers le dépôt du serveur</span><span class="sxs-lookup"><span data-stu-id="89002-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="89002-168">Pour transférer les modifications depuis votre dépôt local vers le dépôt du serveur, vous devez valider vos modifications, puis les transférer vers le dépôt du serveur.</span><span class="sxs-lookup"><span data-stu-id="89002-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="89002-169">Pour valider vos modifications, ouvrez votre outil de commande Git, accédez au répertoire de votre dépôt local et exécutez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="89002-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="89002-170">Pour transférer toutes les validations vers le serveur, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="89002-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="89002-171">Pour déployer les modifications de configuration de service sur l’instance du service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="89002-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="89002-172">Une fois vos modifications locales validées et transférées vers le dépôt du serveur, vous pouvez les déployer sur votre instance du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="89002-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Déployer][api-management-configuration-deploy]

<span data-ttu-id="89002-174">Pour plus d’informations sur l’exécution de cette opération en utilisant l’API REST, consultez [Déployer les modifications Git dans votre base de données de configuration à l’aide de l’API REST](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="89002-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="89002-175">Référence de la structure des fichiers et des dossiers du dépôt Git local</span><span class="sxs-lookup"><span data-stu-id="89002-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="89002-176">Les fichiers et dossiers dans le dépôt git local contiennent les informations de configuration sur l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="89002-177">Item</span><span class="sxs-lookup"><span data-stu-id="89002-177">Item</span></span> | <span data-ttu-id="89002-178">Description</span><span class="sxs-lookup"><span data-stu-id="89002-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89002-179">Dossier api-management racine</span><span class="sxs-lookup"><span data-stu-id="89002-179">root api-management folder</span></span> |<span data-ttu-id="89002-180">Contient la configuration de niveau supérieur pour l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="89002-181">Dossier apis</span><span class="sxs-lookup"><span data-stu-id="89002-181">apis folder</span></span> |<span data-ttu-id="89002-182">Contient la configuration des API dans l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="89002-183">Dossier groups</span><span class="sxs-lookup"><span data-stu-id="89002-183">groups folder</span></span> |<span data-ttu-id="89002-184">Contient la configuration des groupes dans l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="89002-185">Dossier policies</span><span class="sxs-lookup"><span data-stu-id="89002-185">policies folder</span></span> |<span data-ttu-id="89002-186">Contient les stratégies dans l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="89002-187">Dossier portalStyles</span><span class="sxs-lookup"><span data-stu-id="89002-187">portalStyles folder</span></span> |<span data-ttu-id="89002-188">Contient la configuration des personnalisations du portail des développeurs dans l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="89002-189">Dossier products</span><span class="sxs-lookup"><span data-stu-id="89002-189">products folder</span></span> |<span data-ttu-id="89002-190">Contient la configuration des produits dans l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="89002-191">Dossier templates</span><span class="sxs-lookup"><span data-stu-id="89002-191">templates folder</span></span> |<span data-ttu-id="89002-192">Contient la configuration des modèles d’e-mail dans l’instance de service</span><span class="sxs-lookup"><span data-stu-id="89002-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="89002-193">Chaque dossier peut contenir un ou plusieurs fichiers et, dans certains cas, un ou plusieurs dossiers, par exemple un dossier par API, produit ou groupe.</span><span class="sxs-lookup"><span data-stu-id="89002-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="89002-194">Les fichiers dans chaque dossier sont spécifiques du type d’entité décrit par le nom du dossier.</span><span class="sxs-lookup"><span data-stu-id="89002-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="89002-195">Type de fichier</span><span class="sxs-lookup"><span data-stu-id="89002-195">File type</span></span> | <span data-ttu-id="89002-196">Objectif</span><span class="sxs-lookup"><span data-stu-id="89002-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="89002-197">json</span><span class="sxs-lookup"><span data-stu-id="89002-197">json</span></span> |<span data-ttu-id="89002-198">Informations de configuration sur l’entité concernée</span><span class="sxs-lookup"><span data-stu-id="89002-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="89002-199">html</span><span class="sxs-lookup"><span data-stu-id="89002-199">html</span></span> |<span data-ttu-id="89002-200">Descriptions de l’entité, souvent affichées dans le portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="89002-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="89002-201">xml</span><span class="sxs-lookup"><span data-stu-id="89002-201">xml</span></span> |<span data-ttu-id="89002-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="89002-202">Policy statements</span></span> |
| <span data-ttu-id="89002-203">css</span><span class="sxs-lookup"><span data-stu-id="89002-203">css</span></span> |<span data-ttu-id="89002-204">Feuilles de style pour la personnalisation du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="89002-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="89002-205">Ces fichiers peuvent être créés, supprimés, modifiés et gérés dans votre système de fichiers local, et les modifications peuvent être déployées sur votre instance du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="89002-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="89002-206">Les entités suivantes ne se trouvent pas dans le dépôt Git et ne peuvent pas être configurées à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="89002-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="89002-207">Utilisateurs</span><span class="sxs-lookup"><span data-stu-id="89002-207">Users</span></span>
> * <span data-ttu-id="89002-208">Abonnements</span><span class="sxs-lookup"><span data-stu-id="89002-208">Subscriptions</span></span>
> * <span data-ttu-id="89002-209">Propriétés</span><span class="sxs-lookup"><span data-stu-id="89002-209">Properties</span></span>
> * <span data-ttu-id="89002-210">Entités du portail des développeur autres que les styles</span><span class="sxs-lookup"><span data-stu-id="89002-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="89002-211">Dossier api-management racine</span><span class="sxs-lookup"><span data-stu-id="89002-211">Root api-management folder</span></span>
<span data-ttu-id="89002-212">Le dossier `api-management` racine contient un fichier `configuration.json` qui renferme des informations de premier niveau sur l’instance de service dans le format suivant.</span><span class="sxs-lookup"><span data-stu-id="89002-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

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

<span data-ttu-id="89002-213">Les quatre premiers paramètres (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` et `UserRegistrationTermsConsentRequired`) correspondent aux paramètres suivants, disponibles dans l’onglet **Identités** de la section **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="89002-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="89002-214">Paramètre d’identité</span><span class="sxs-lookup"><span data-stu-id="89002-214">Identity setting</span></span> | <span data-ttu-id="89002-215">Correspond à</span><span class="sxs-lookup"><span data-stu-id="89002-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="89002-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="89002-216">RegistrationEnabled</span></span> |<span data-ttu-id="89002-217">**Rediriger les utilisateurs anonymes vers la page de connexion** </span><span class="sxs-lookup"><span data-stu-id="89002-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="89002-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="89002-218">UserRegistrationTerms</span></span> |<span data-ttu-id="89002-219">**Conditions d’utilisation liées à l’inscription de l’utilisateur** </span><span class="sxs-lookup"><span data-stu-id="89002-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="89002-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="89002-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="89002-221">**Afficher les conditions d’utilisation dans la page d’abonnement** </span><span class="sxs-lookup"><span data-stu-id="89002-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="89002-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="89002-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="89002-223">**Exiger le consentement** </span><span class="sxs-lookup"><span data-stu-id="89002-223">**Require consent** checkbox</span></span> |

![Paramètres d’identité][api-management-identity-settings]

<span data-ttu-id="89002-225">Les quatre paramètres qui suivent (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` et `DelegationValidationKey`) correspondent aux paramètres suivants, disponibles dans l’onglet **Délégation** de la section **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="89002-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="89002-226">Paramètre de délégation</span><span class="sxs-lookup"><span data-stu-id="89002-226">Delegation setting</span></span> | <span data-ttu-id="89002-227">Correspond à</span><span class="sxs-lookup"><span data-stu-id="89002-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="89002-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="89002-228">DelegationEnabled</span></span> |<span data-ttu-id="89002-229">Case à cocher **Déléguer la connexion et l’inscription**</span><span class="sxs-lookup"><span data-stu-id="89002-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="89002-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="89002-230">DelegationUrl</span></span> |<span data-ttu-id="89002-231">**URL de point de terminaison de la délégation** </span><span class="sxs-lookup"><span data-stu-id="89002-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="89002-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="89002-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="89002-233">**Déléguer l’abonnement au produit** </span><span class="sxs-lookup"><span data-stu-id="89002-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="89002-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="89002-234">DelegationValidationKey</span></span> |<span data-ttu-id="89002-235">**Déléguer la clé de validation** </span><span class="sxs-lookup"><span data-stu-id="89002-235">**Delegate Validation Key** textbox</span></span> |

![Paramètres de délégation][api-management-delegation-settings]

<span data-ttu-id="89002-237">Le dernier paramètre, `$ref-policy`, correspond au fichier d’instructions de stratégie globale pour l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="89002-238">Dossier apis</span><span class="sxs-lookup"><span data-stu-id="89002-238">apis folder</span></span>
<span data-ttu-id="89002-239">Le dossier `apis` contient un dossier pour chaque API dans l’instance de service qui renferme les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="89002-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="89002-240">`apis\<api name>\configuration.json` : cet élément représente la configuration de l’API et contient des informations sur l’URL du service principal et sur les opérations.</span><span class="sxs-lookup"><span data-stu-id="89002-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="89002-241">Vous pouvez obtenir les mêmes informations en appelant l’opération [Obtenir une API spécifique](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) avec `export=true` au format `application/json`.</span><span class="sxs-lookup"><span data-stu-id="89002-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="89002-242">`apis\<api name>\api.description.html` : cet élément décrit l’API et correspond à la propriété `description` de [l’entité API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="89002-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="89002-243">`apis\<api name>\operations\` : ce dossier contient des fichiers `<operation name>.description.html` correspondant aux opérations dans l’API.</span><span class="sxs-lookup"><span data-stu-id="89002-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="89002-244">Chaque fichier contient la description d’une opération unique dans l’API, qui correspond à la propriété `description` de l’ [entité opération](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) dans l’API REST.</span><span class="sxs-lookup"><span data-stu-id="89002-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="89002-245">Dossier groups</span><span class="sxs-lookup"><span data-stu-id="89002-245">groups folder</span></span>
<span data-ttu-id="89002-246">Le dossier `groups` contient un dossier pour chaque groupe défini dans l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="89002-247">`groups\<group name>\configuration.json` : cet élément correspond à la configuration du groupe.</span><span class="sxs-lookup"><span data-stu-id="89002-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="89002-248">Vous pouvez obtenir les mêmes informations en appelant l’opération [Obtenir un groupe spécifique](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) .</span><span class="sxs-lookup"><span data-stu-id="89002-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="89002-249">`groups\<group name>\description.html` : cet élément décrit le groupe et correspond à la propriété `description` de [l’entité groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="89002-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="89002-250">Dossier policies</span><span class="sxs-lookup"><span data-stu-id="89002-250">policies folder</span></span>
<span data-ttu-id="89002-251">Le dossier `policies` contient les instructions de stratégie pour votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="89002-252">`policies\global.xml` : contient les stratégies définies dans l’étendue globale de votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="89002-253">`policies\apis\<api name>\` : si des stratégies sont définies à l’échelle de l’API, elles se trouvent dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="89002-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="89002-254">`policies\apis\<api name>\<operation name>\` : si des stratégies sont définies à l’échelle des opérations, elles se trouvent dans ce dossier, qui contient des fichiers `<operation name>.xml` correspondant aux instructions de stratégie pour chaque opération.</span><span class="sxs-lookup"><span data-stu-id="89002-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="89002-255">`policies\products\` : si des stratégies sont définies à l’échelle des produits, elles se trouvent dans ce dossier, qui contient des fichiers `<product name>.xml` correspondant aux instructions de stratégie pour chaque produit.</span><span class="sxs-lookup"><span data-stu-id="89002-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="89002-256">Dossier portalStyles</span><span class="sxs-lookup"><span data-stu-id="89002-256">portalStyles folder</span></span>
<span data-ttu-id="89002-257">Le dossier `portalStyles` contient la configuration et les feuilles de style pour les personnalisations du portail des développeurs pour l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="89002-258">`portalStyles\configuration.json` : contient les noms des feuilles de style utilisées par le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="89002-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="89002-259">`portalStyles\<style name>.css` : chaque fichier `<style name>.css` contient des styles pour le portail des développeurs (`Preview.css` et `Production.css` par défaut).</span><span class="sxs-lookup"><span data-stu-id="89002-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="89002-260">Dossier products</span><span class="sxs-lookup"><span data-stu-id="89002-260">products folder</span></span>
<span data-ttu-id="89002-261">Le dossier `products` contient un dossier pour chaque produit défini dans l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="89002-262">`products\<product name>\configuration.json` : cet élément correspond à la configuration du produit.</span><span class="sxs-lookup"><span data-stu-id="89002-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="89002-263">Vous pouvez obtenir les mêmes informations en appelant l’opération [Obtenir un produit spécifique](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) .</span><span class="sxs-lookup"><span data-stu-id="89002-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="89002-264">`products\<product name>\product.description.html` : cet élément décrit le produit et correspond à la propriété `description` de [l’entité produit](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) dans l’API REST.</span><span class="sxs-lookup"><span data-stu-id="89002-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="89002-265">modèles</span><span class="sxs-lookup"><span data-stu-id="89002-265">templates</span></span>
<span data-ttu-id="89002-266">Le dossier `templates` contient la configuration des [modèles d’e-mail](api-management-howto-configure-notifications.md) dans l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="89002-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="89002-267">`<template name>\configuration.json` : cet élément correspond à la configuration du modèle d’e-mail.</span><span class="sxs-lookup"><span data-stu-id="89002-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="89002-268">`<template name>\body.html` : il s’agit du corps du modèle d’e-mail.</span><span class="sxs-lookup"><span data-stu-id="89002-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89002-269">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89002-269">Next steps</span></span>
<span data-ttu-id="89002-270">Pour plus d’informations sur d’autres méthodes pour gérer votre instance de service, consultez les sources suivantes :</span><span class="sxs-lookup"><span data-stu-id="89002-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="89002-271">Gérer votre instance de service à l’aide des applets de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="89002-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="89002-272">Référence sur les applets de commande PowerShell de déploiement des services</span><span class="sxs-lookup"><span data-stu-id="89002-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="89002-273">Référence sur les applets de commande PowerShell de gestion des services</span><span class="sxs-lookup"><span data-stu-id="89002-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="89002-274">Gérer votre instance de service dans le portail de publication</span><span class="sxs-lookup"><span data-stu-id="89002-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="89002-275">Gérer votre première API</span><span class="sxs-lookup"><span data-stu-id="89002-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="89002-276">Gérer votre instance de service à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="89002-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="89002-277">Référence de l’API REST Gestion des API</span><span class="sxs-lookup"><span data-stu-id="89002-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="89002-278">Regarder une vidéo de présentation</span><span class="sxs-lookup"><span data-stu-id="89002-278">Watch a video overview</span></span>
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




