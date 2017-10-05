---
title: "Utilisation de scripts Windows PowerShell pour publier dans des environnements de développement et de test | Microsoft Docs"
description: "Découvrez comment utiliser les scripts Windows PowerShell à partir de Visual Studio pour la publication dans des environnements de développement et de test."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="6e568-103">Utilisation de scripts Windows PowerShell pour publier des environnements de développement et de test</span><span class="sxs-lookup"><span data-stu-id="6e568-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="6e568-104">Lorsque vous créez une application web dans Visual Studio, vous pouvez générer un script Windows PowerShell que vous pouvez utiliser ultérieurement pour automatiser la publication de votre site web sur Azure en tant qu’application web dans Azure App Service ou dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="6e568-105">Vous pouvez modifier et étendre le script Windows PowerShell dans l’éditeur Visual Studio, conformément à vos besoins, ou intégrer le script à la build, aux tests et aux scripts de publication existants.</span><span class="sxs-lookup"><span data-stu-id="6e568-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="6e568-106">À l’aide de ces scripts, vous pouvez configurer des versions personnalisées (également connues comme environnements de développement et de test) de votre site pour une utilisation temporaire.</span><span class="sxs-lookup"><span data-stu-id="6e568-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="6e568-107">Par exemple, vous pouvez configurer une version particulière de votre site web sur une machine virtuelle Azure ou sur l’emplacement intermédiaire d’un site web pour exécuter une suite de tests, reproduire un bogue, tester un correctif, évaluer une proposition de modification ou configurer un environnement personnalisé pour une démonstration ou une présentation.</span><span class="sxs-lookup"><span data-stu-id="6e568-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="6e568-108">Une fois que vous avez créé un script qui publie votre projet, vous pouvez recréer des environnements identiques en réexécutant le script en fonction des besoins, ou en exécutant le script avec votre propre build de votre application web pour créer un environnement personnalisé de test.</span><span class="sxs-lookup"><span data-stu-id="6e568-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6e568-109">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="6e568-109">What you need</span></span>
* <span data-ttu-id="6e568-110">Kit de développement logiciel (SDK) Azure 2.3 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="6e568-111">Pour plus d’informations, consultez [Téléchargements Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) .</span><span class="sxs-lookup"><span data-stu-id="6e568-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="6e568-112">Vous n’avez pas besoin du kit de développement logiciel (SDK) Azure pour générer les scripts pour les projets web.</span><span class="sxs-lookup"><span data-stu-id="6e568-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="6e568-113">Cette fonctionnalité s’adresse aux projets web, et non aux rôles web dans les services cloud.</span><span class="sxs-lookup"><span data-stu-id="6e568-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="6e568-114">Azure PowerShell 0.7.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="6e568-115">Pour plus d’informations, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="6e568-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="6e568-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="6e568-117">Outils supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6e568-117">Additional tools</span></span>
<span data-ttu-id="6e568-118">Des outils et ressources supplémentaires sont disponibles pour l’utilisation de PowerShell dans Visual Studio pour le développement Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="6e568-119">Consultez [Outils PowerShell pour Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="6e568-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="6e568-120">Génération de scripts de publication</span><span class="sxs-lookup"><span data-stu-id="6e568-120">Generating the publish scripts</span></span>
<span data-ttu-id="6e568-121">Vous pouvez générer des scripts de publication pour une machine virtuelle qui héberge votre site web lorsque vous créez un projet en suivant [ces instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e568-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="6e568-122">Vous pouvez également [Générer des scripts de publication pour les applications web dans Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6e568-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="6e568-123">Scripts générés par Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e568-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="6e568-124">Visual Studio génère un dossier au niveau solution appelé **PublishScripts** qui contient deux fichiers Windows PowerShell, un script de publication pour votre machine virtuelle ou votre site web et un module qui contient des fonctions que vous pouvez utiliser dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="6e568-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="6e568-125">Visual Studio génère également un fichier au format JSON qui spécifie les détails du projet que vous déployez.</span><span class="sxs-lookup"><span data-stu-id="6e568-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="6e568-126">Script de publication Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e568-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="6e568-127">Le script de publication contient des étapes de publication spécifiques pour le déploiement sur un site web ou une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="6e568-128">Visual Studio propose la coloration de syntaxe pour le développement de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e568-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="6e568-129">Vous pouvez bénéficier d’une aide sur les fonctions et modifier librement les fonctions dans le script en fonction de l’évolution de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="6e568-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="6e568-130">Module Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e568-130">Windows PowerShell module</span></span>
<span data-ttu-id="6e568-131">Le module Windows PowerShell généré par Visual Studio contient des fonctions que le script de publication utilise.</span><span class="sxs-lookup"><span data-stu-id="6e568-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="6e568-132">Ce sont des fonctions Azure PowerShell et elles ne sont pas destinées à être modifiées.</span><span class="sxs-lookup"><span data-stu-id="6e568-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="6e568-133">Pour plus d’informations, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="6e568-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="6e568-134">Fichier de configuration JSON</span><span class="sxs-lookup"><span data-stu-id="6e568-134">JSON configuration file</span></span>
<span data-ttu-id="6e568-135">Le fichier JSON est créé dans le dossier **Configurations** et contient des données de configuration qui spécifient exactement les ressources à déployer sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="6e568-136">Le nom du fichier généré par Visual Studio est projet-nom-WAWS-dev.json, si vous avez créé un site web, ou projet-nom-VM-dev.json, si vous avez créé une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="6e568-137">Voici un exemple de fichier de configuration JSON généré lorsque vous créez un site web.</span><span class="sxs-lookup"><span data-stu-id="6e568-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="6e568-138">La plupart des valeurs sont explicites.</span><span class="sxs-lookup"><span data-stu-id="6e568-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="6e568-139">Le nom du site web est généré par Azure ; il peut donc ne pas correspondre au nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="6e568-139">The website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="6e568-140">Lorsque vous créez une machine virtuelle, le fichier de configuration JSON ressemble à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="6e568-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="6e568-141">Notez qu’un service cloud est créé comme un conteneur pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="6e568-142">La machine virtuelle contient les points de terminaison habituels pour l’accès web via HTTP et HTTPS, ainsi que les points de terminaison pour Web Deploy, ce qui vous permet de publier sur le site web à partir de votre ordinateur local, de la connexion Bureau à distance et de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e568-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="6e568-143">Vous pouvez modifier la configuration JSON pour changer ce qui se passe lorsque vous exécutez les scripts de publication.</span><span class="sxs-lookup"><span data-stu-id="6e568-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="6e568-144">Les sections `cloudService` et `virtualMachine` sont obligatoires, mais vous pouvez supprimer la section `databases` si vous n’en avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="6e568-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="6e568-145">Les propriétés qui sont vides dans le fichier de configuration par défaut généré par Visual Studio sont facultatives ; celles qui ont des valeurs dans le fichier de configuration par défaut sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="6e568-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="6e568-146">Si vous possédez un site web qui compte plusieurs environnements de déploiement (appelés emplacements) au lieu d’un site de production unique dans Azure, vous pouvez inclure le nom de l’emplacement dans le nom du site web dans le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="6e568-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="6e568-147">Par exemple, si votre site web est nommé **monsite** et que son emplacement est nommé **test**, l’URI est monsite-test.cloudapp.net, mais le nom correct à utiliser dans le fichier de configuration est monsite(test).</span><span class="sxs-lookup"><span data-stu-id="6e568-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="6e568-148">Vous pouvez uniquement effectuer cette opération si le site web et les emplacements existent déjà dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e568-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="6e568-149">S’ils n’existent pas, créez le site web en exécutant le script sans spécifier l’emplacement, puis créez l’emplacement dans le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885). Ensuite, exécutez le script avec le nom de site web modifié.</span><span class="sxs-lookup"><span data-stu-id="6e568-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="6e568-150">Pour plus d’informations sur les emplacements de déploiement pour les applications web, consultez [Configurer des environnements intermédiaires pour les applications web dans Azure App Service](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="6e568-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="6e568-151">Exécution de scripts de publication</span><span class="sxs-lookup"><span data-stu-id="6e568-151">How to run the publish scripts</span></span>
<span data-ttu-id="6e568-152">Si vous n’avez jamais exécuté de script Windows PowerShell auparavant, vous devez d’abord définir la stratégie d’exécution pour permettre l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="6e568-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="6e568-153">Il s’agit d’une fonctionnalité de sécurité visant à empêcher les utilisateurs d’exécuter des scripts Windows PowerShell s’ils sont vulnérables aux programmes malveillants ou aux virus impliquant l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="6e568-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="6e568-154">Exécutez le script</span><span class="sxs-lookup"><span data-stu-id="6e568-154">Run the script</span></span>
1. <span data-ttu-id="6e568-155">Créez le package Web Deploy pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="6e568-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="6e568-156">Un package Web Deploy est une archive compressée (fichier .zip) contenant les fichiers que vous souhaitez copier sur votre site web ou sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="6e568-157">Vous pouvez créer des packages Web Deploy dans Visual Studio pour toute application web.</span><span class="sxs-lookup"><span data-stu-id="6e568-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Créer un package Web Deploy](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="6e568-159">Pour plus d’informations, consultez [Comment : créer un package de déploiement web dans Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e568-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="6e568-160">Vous pouvez également automatiser la création de votre package Web Deploy, comme décrit dans la section **Personnalisation et extension des scripts de publication** plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="6e568-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="6e568-161">Dans l’**Explorateur de solutions**, ouvrez le menu contextuel du script, puis choisissez **Ouvrir avec PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="6e568-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="6e568-162">S’il s’agit de la première fois que vous exécutez des scripts Windows PowerShell sur cet ordinateur, ouvrez une fenêtre d’invite de commandes avec des privilèges d’administrateur et tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e568-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="6e568-163">Connectez-vous à Azure en utilisant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="6e568-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="6e568-164">Lorsque vous y êtes invité, indiquez votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6e568-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="6e568-165">Notez que lorsque vous automatisez le script, cette méthode de renseignement des informations d’identification Azure ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="6e568-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="6e568-166">À la place, vous devez utiliser le fichier .publishsettings pour fournir des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="6e568-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="6e568-167">Une fois seulement, vous utilisez la commande **Get-AzurePublishSettingsFile** pour télécharger le fichier à partir d’Azure. Ensuite, vous utilisez **Import-AzurePublishSettingsFile** pour importer le fichier.</span><span class="sxs-lookup"><span data-stu-id="6e568-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="6e568-168">Pour des instructions détaillées, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e568-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="6e568-169">(Facultatif) Si vous souhaitez créer des ressources Azure telles que la machine virtuelle, la base de données et le site web sans publier votre application web, utilisez la commande **Publish-WebApplication.ps1** avec l’argument **-Configuration** défini dans le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="6e568-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="6e568-170">Cette ligne de commande utilise le fichier de configuration JSON pour déterminer les ressources à créer.</span><span class="sxs-lookup"><span data-stu-id="6e568-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="6e568-171">Étant donné qu’elle utilise les paramètres par défaut pour les autres arguments de ligne de commande, elle crée les ressources, mais ne publie pas votre application web.</span><span class="sxs-lookup"><span data-stu-id="6e568-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="6e568-172">L’option –Verbose vous donne plus d’informations sur ce qui se passe.</span><span class="sxs-lookup"><span data-stu-id="6e568-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="6e568-173">Utilisez la commande **Publish-WebApplication.ps1** comme indiqué dans l’un des exemples suivants pour appeler le script et publier votre application web.</span><span class="sxs-lookup"><span data-stu-id="6e568-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="6e568-174">Si vous souhaitez remplacer les paramètres par défaut de tout autre argument, comme le nom de l’abonnement, le nom du package de publication, les informations d’identification de la machine virtuelle ou les informations d’identification du serveur de base de données, vous pouvez spécifier ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="6e568-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="6e568-175">Utilisez l’option **–Verbose** pour afficher plus d’informations sur la progression du processus de publication.</span><span class="sxs-lookup"><span data-stu-id="6e568-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="6e568-176">Si vous créez une machine virtuelle, la commande ressemble à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="6e568-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="6e568-177">Cet exemple montre également comment spécifier les informations d’identification pour plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="6e568-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="6e568-178">Pour les machines virtuelles créées par ces scripts, le certificat SSL n’est pas d’une autorité racine de confiance.</span><span class="sxs-lookup"><span data-stu-id="6e568-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="6e568-179">Par conséquent, vous devez utiliser l’option **–AllowUntrusted** .</span><span class="sxs-lookup"><span data-stu-id="6e568-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="6e568-180">Le script peut créer des bases de données, mais il ne crée pas de serveurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="6e568-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="6e568-181">Si vous souhaitez créer un serveur de base de données, vous pouvez utiliser la fonction **New-AzureSqlDatabaseServer** du module Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="6e568-182">Personnalisation et extension des scripts de publication</span><span class="sxs-lookup"><span data-stu-id="6e568-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="6e568-183">Vous pouvez personnaliser le script de publication et le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="6e568-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="6e568-184">Les fonctions dans le module Windows PowerShell **AzureWebAppPublishModule.psm1** ne sont pas destinées à être modifiées.</span><span class="sxs-lookup"><span data-stu-id="6e568-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="6e568-185">Si vous souhaitez simplement spécifier une autre base de données ou modifier certaines propriétés de la machine virtuelle, modifiez le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="6e568-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="6e568-186">Si vous souhaitez étendre la fonctionnalité de script pour automatiser la création et le test de votre projet, vous pouvez implémenter les stubs de fonction dans **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="6e568-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="6e568-187">Pour automatiser la création de votre projet, ajoutez le code appelant MSBuild sur `New-WebDeployPackage` , comme illustré dans cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="6e568-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="6e568-188">Le chemin d’accès à la commande MSBuild est différent selon la version de Visual Studio que vous avez installée.</span><span class="sxs-lookup"><span data-stu-id="6e568-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="6e568-189">Pour obtenir le chemin d’accès correct, vous pouvez utiliser la fonction **Get-MSBuildCmd**, comme illustré dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="6e568-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="6e568-190">Pour automatiser la création de votre projet</span><span class="sxs-lookup"><span data-stu-id="6e568-190">To automate building your project</span></span>
1. <span data-ttu-id="6e568-191">Ajoutez le paramètre `$ProjectFile` dans la section des paramètres globaux.</span><span class="sxs-lookup"><span data-stu-id="6e568-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="6e568-192">Copiez la fonction `Get-MSBuildCmd` dans votre fichier de script.</span><span class="sxs-lookup"><span data-stu-id="6e568-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="6e568-193">Remplacez `New-WebDeployPackage` avec le code suivant et remplacez les espaces réservés dans la ligne créant `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="6e568-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="6e568-194">Ce code est destiné à Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6e568-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="6e568-195">Si vous utilisez Visual Studio 2013, remplacez la propriété **VisualStudioVersion** par une valeur inférieure à `12.0`.</span><span class="sxs-lookup"><span data-stu-id="6e568-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="6e568-196">Pour générer votre application web, utilisez MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="6e568-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="6e568-197">Pour obtenir de l’aide, reportez-vous à la section Référence de ligne de commande MSBuild à l’adresse : [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="6e568-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="6e568-198">Démarrez l’exécution de la commande build</span><span class="sxs-lookup"><span data-stu-id="6e568-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="6e568-199">Appelez la fonction `New-WebDeployPackage` avant cette ligne : `$Config = Read-ConfigFile $Configuration` pour les applications web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6e568-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="6e568-200">Appelez le script personnalisé à partir de la ligne de commande à l’aide de la transmission de l’argument `$Project`, comme dans la ligne de commande en exemple suivante.</span><span class="sxs-lookup"><span data-stu-id="6e568-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="6e568-201">Pour automatiser le test de votre application, ajoutez le code à `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="6e568-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="6e568-202">Veillez à supprimer les marques de commentaire des lignes dans **Publish-WebApplication.ps1** où ces fonctions sont appelées.</span><span class="sxs-lookup"><span data-stu-id="6e568-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="6e568-203">Si vous ne fournissez pas d’implémentation, vous pouvez créer votre projet manuellement avec Visual Studio, puis exécuter le script de publication pour publier dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="6e568-204">Résumé de la fonction de publication</span><span class="sxs-lookup"><span data-stu-id="6e568-204">Publishing function summary</span></span>
<span data-ttu-id="6e568-205">Pour obtenir de l’aide pour les fonctions que vous pouvez utiliser à l’invite de commande Windows PowerShell, utilisez la commande `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="6e568-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="6e568-206">L’aide inclut de l’aide sur les paramètres et des exemples.</span><span class="sxs-lookup"><span data-stu-id="6e568-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="6e568-207">Le même texte d’aide figure également dans les fichiers source du script, **AzureWebAppPublishModule.psm1** et **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="6e568-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="6e568-208">Le script et l’aide sont localisés dans votre langue Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e568-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="6e568-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="6e568-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="6e568-210">Nom de la fonction</span><span class="sxs-lookup"><span data-stu-id="6e568-210">Function name</span></span> | <span data-ttu-id="6e568-211">Description</span><span class="sxs-lookup"><span data-stu-id="6e568-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e568-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="6e568-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="6e568-213">Crée une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="6e568-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="6e568-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="6e568-215">Crée des bases de données SQL Azure à partir des valeurs du fichier de configuration JSON généré par Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e568-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="6e568-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="6e568-216">Add-AzureVM</span></span> |<span data-ttu-id="6e568-217">Crée une machine virtuelle Azure et renvoie l’URL de la machine virtuelle déployée.</span><span class="sxs-lookup"><span data-stu-id="6e568-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="6e568-218">La fonction définit les conditions préalables, puis appelle la fonction **New-AzureVM** (module Azure) pour créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="6e568-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="6e568-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="6e568-220">Ajoute de nouveaux points de terminaison d’entrée à une machine virtuelle et renvoie la machine virtuelle avec le nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6e568-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="6e568-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="6e568-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="6e568-222">Crée un compte de stockage Azure dans l’abonnement actif.</span><span class="sxs-lookup"><span data-stu-id="6e568-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="6e568-223">Le nom du compte commence par « devtest » et est suivi d’une chaîne alphanumérique unique.</span><span class="sxs-lookup"><span data-stu-id="6e568-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="6e568-224">La fonction renvoie le nom du nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6e568-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="6e568-225">Vous devez spécifier un emplacement ou un groupe d’affinités pour le nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6e568-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="6e568-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="6e568-226">Add-AzureWebsite</span></span> |<span data-ttu-id="6e568-227">Crée un site web avec le nom et l’emplacement spécifiés.</span><span class="sxs-lookup"><span data-stu-id="6e568-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="6e568-228">Cette fonction appelle la fonction **New-AzureWebsite** dans le module Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="6e568-229">Si l’abonnement ne contient pas déjà un site web avec le nom spécifié, cette fonction crée le site web et renvoie un objet de site web.</span><span class="sxs-lookup"><span data-stu-id="6e568-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="6e568-230">Sinon, la valeur renvoyée est `$null`.</span><span class="sxs-lookup"><span data-stu-id="6e568-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="6e568-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="6e568-231">Backup-Subscription</span></span> |<span data-ttu-id="6e568-232">Enregistre l’abonnement Azure actif dans la variable `$Script:originalSubscription` dans la portée du script. Cette fonction enregistre l’abonnement Azure actif (tel qu’obtenu par `Get-AzureSubscription -Current`) et son compte de stockage, ainsi que l’abonnement modifié par ce script (stocké dans la variable `$UserSpecifiedSubscription`) et son compte de stockage, dans la portée de script.</span><span class="sxs-lookup"><span data-stu-id="6e568-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="6e568-233">En enregistrant les valeurs, vous pouvez utiliser une fonction telle que `Restore-Subscription` pour restaurer l’abonnement actif d’origine et son compte de stockage à l’état actif, si ce dernier a changé.</span><span class="sxs-lookup"><span data-stu-id="6e568-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="6e568-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="6e568-234">Find-AzureVM</span></span> |<span data-ttu-id="6e568-235">Obtient la machine virtuelle Azure spécifiée.</span><span class="sxs-lookup"><span data-stu-id="6e568-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="6e568-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="6e568-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="6e568-237">Indique la date et l’heure avant un message.</span><span class="sxs-lookup"><span data-stu-id="6e568-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="6e568-238">Cette fonction est conçue pour les messages écrits dans les flux Error et Verbose.</span><span class="sxs-lookup"><span data-stu-id="6e568-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="6e568-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="6e568-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="6e568-240">Assemble une chaîne de connexion pour se connecter à une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="6e568-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="6e568-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="6e568-242">Renvoie le nom du premier compte de stockage avec le modèle de nom devtest *(non sensible à la casse) dans l’emplacement ou le groupe d’affinités spécifié. Si le compte de stockage devtest* ne correspond pas à l’emplacement ou au groupe d’affinités, la fonction l’ignore.</span><span class="sxs-lookup"><span data-stu-id="6e568-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="6e568-243">Vous devez spécifier un emplacement ou un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="6e568-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="6e568-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="6e568-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="6e568-245">Renvoie une commande pour exécuter l’outil MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="6e568-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="6e568-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="6e568-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="6e568-247">Recherche ou crée une machine virtuelle dans l’abonnement qui correspond aux valeurs dans le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="6e568-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="6e568-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="6e568-248">Publish-WebPackage</span></span> |<span data-ttu-id="6e568-249">Utilise MsDeploy.exe et un fichier. zip de package de publication web pour déployer des ressources sur un site web.</span><span class="sxs-lookup"><span data-stu-id="6e568-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="6e568-250">Cette fonction ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="6e568-250">This function doesn't generate any output.</span></span> <span data-ttu-id="6e568-251">Si l’appel de MSDeploy.exe échoue, la fonction lève une exception.</span><span class="sxs-lookup"><span data-stu-id="6e568-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="6e568-252">Pour obtenir une sortie plus détaillée, utilisez l’option **-Verbose**.</span><span class="sxs-lookup"><span data-stu-id="6e568-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="6e568-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="6e568-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="6e568-254">Vérifie les valeurs des paramètres, puis appelle la fonction **Publish-WebPackage** .</span><span class="sxs-lookup"><span data-stu-id="6e568-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="6e568-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6e568-255">Read-ConfigFile</span></span> |<span data-ttu-id="6e568-256">Valide le fichier de configuration JSON et renvoie une table de hachage des valeurs sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="6e568-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="6e568-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="6e568-257">Restore-Subscription</span></span> |<span data-ttu-id="6e568-258">Réinitialise l’abonnement actif sur l’abonnement d’origine.</span><span class="sxs-lookup"><span data-stu-id="6e568-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="6e568-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="6e568-259">Test-AzureModule</span></span> |<span data-ttu-id="6e568-260">Renvoie `$true` si la version du module Azure installé est 0.7.4 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="6e568-261">Renvoie `$false` si le module n’est pas installé ou s’il s’agit d’une version antérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="6e568-262">Cette fonction n’a pas de paramètres.</span><span class="sxs-lookup"><span data-stu-id="6e568-262">This function has no parameters.</span></span> |
| <span data-ttu-id="6e568-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="6e568-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="6e568-264">Renvoie `$true` si la version du module Azure est 0.7.4 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="6e568-265">Renvoie `$false` si le module n’est pas installé ou s’il s’agit d’une version antérieure.</span><span class="sxs-lookup"><span data-stu-id="6e568-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="6e568-266">Cette fonction n’a pas de paramètres.</span><span class="sxs-lookup"><span data-stu-id="6e568-266">This function has no parameters.</span></span> |
| <span data-ttu-id="6e568-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="6e568-267">Test-HttpsUrl</span></span> |<span data-ttu-id="6e568-268">Convertit l’URL d’entrée en un objet System.Uri.</span><span class="sxs-lookup"><span data-stu-id="6e568-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="6e568-269">Renvoie `$True` si l’URL est absolue et que son schéma est https.</span><span class="sxs-lookup"><span data-stu-id="6e568-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="6e568-270">Renvoie `$false` si l’URL est relative, que son schéma n’est pas HTTPS ou que la chaîne d’entrée ne peut pas être convertie en URL.</span><span class="sxs-lookup"><span data-stu-id="6e568-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="6e568-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="6e568-271">Test-Member</span></span> |<span data-ttu-id="6e568-272">Renvoie `$true` si une propriété ou méthode est un membre de l’objet.</span><span class="sxs-lookup"><span data-stu-id="6e568-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="6e568-273">Sinon, renvoie `$false`.</span><span class="sxs-lookup"><span data-stu-id="6e568-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="6e568-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="6e568-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="6e568-275">Écrit un message d’erreur préfixé avec l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="6e568-276">Cette fonction appelle la fonction **Format-DevTestMessageWithTime** à indiquer l’heure avant d’écrire le message dans le flux Error.</span><span class="sxs-lookup"><span data-stu-id="6e568-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="6e568-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="6e568-277">Write-HostWithTime</span></span> |<span data-ttu-id="6e568-278">Écrit un message dans le programme hôte (**Write-Host**) préfixé avec l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="6e568-279">L’effet de l’écriture dans le programme hôte varie.</span><span class="sxs-lookup"><span data-stu-id="6e568-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="6e568-280">La plupart des programmes qui hébergent Windows PowerShell écrivent ces messages dans la sortie standard.</span><span class="sxs-lookup"><span data-stu-id="6e568-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="6e568-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="6e568-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="6e568-282">Écrit un message détaillé préfixé avec l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="6e568-283">Étant donné qu’il appelle **Write-Verbose**, le message s’affiche uniquement lorsque le script s’exécute avec le paramètre **Verbose** ou lorsque la préférence **VerbosePreference** est définie sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="6e568-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="6e568-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="6e568-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="6e568-285">Nom de la fonction</span><span class="sxs-lookup"><span data-stu-id="6e568-285">Function name</span></span> | <span data-ttu-id="6e568-286">Description</span><span class="sxs-lookup"><span data-stu-id="6e568-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e568-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="6e568-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="6e568-288">Crée des ressources Azure, comme un site web ou une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6e568-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="6e568-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="6e568-289">New-WebDeployPackage</span></span> |<span data-ttu-id="6e568-290">Cette fonction n’est pas implémentée.</span><span class="sxs-lookup"><span data-stu-id="6e568-290">This function isn't implemented.</span></span> <span data-ttu-id="6e568-291">Vous pouvez ajouter des commandes à cette fonction pour créer votre projet.</span><span class="sxs-lookup"><span data-stu-id="6e568-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="6e568-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="6e568-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="6e568-293">Publie une application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6e568-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="6e568-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="6e568-294">Publish-WebApplication</span></span> |<span data-ttu-id="6e568-295">Crée et déploie des applications web, des machines virtuelles, des bases de données SQL et des comptes de stockage pour un projet web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e568-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="6e568-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="6e568-296">Test-WebApplication</span></span> |<span data-ttu-id="6e568-297">Cette fonction n’est pas implémentée.</span><span class="sxs-lookup"><span data-stu-id="6e568-297">This function isn't implemented.</span></span> <span data-ttu-id="6e568-298">Vous pouvez ajouter des commandes à cette fonction pour tester votre application.</span><span class="sxs-lookup"><span data-stu-id="6e568-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e568-299">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e568-299">Next steps</span></span>
<span data-ttu-id="6e568-300">Pour en savoir plus sur l’écriture de scripts PowerShell lisez [Écriture de scripts avec Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) et consultez d’autres scripts Azure PowerShell sur le [Centre de scripts](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="6e568-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
