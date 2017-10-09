---
title: aaaUsing les environnements de Test et les Scripts Windows PowerShell tooPublish tooDev | Documents Microsoft
description: "Découvrez comment toouse Windows PowerShell scripts à partir d’environnements de test et de toodevelopment de toopublish de Visual Studio."
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
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="15cd9-103">À l’aide de Windows PowerShell scripts des environnements de test et de toodev de toopublish</span><span class="sxs-lookup"><span data-stu-id="15cd9-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="15cd9-104">Lorsque vous créez une application web dans Visual Studio, vous pouvez générer un script Windows PowerShell que vous pouvez utiliser la publication hello tooautomate ultérieure de tooAzure de votre site Web comme une application Web dans Azure App Service ou une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="15cd9-105">Vous pouvez modifier et étendre des besoins de votre script Windows PowerShell de hello dans toosuit de l’éditeur Visual Studio hello ou intégrer le script de hello avec la build existante, de test et des scripts de publication.</span><span class="sxs-lookup"><span data-stu-id="15cd9-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="15cd9-106">À l’aide de ces scripts, vous pouvez configurer des versions personnalisées (également connues comme environnements de développement et de test) de votre site pour une utilisation temporaire.</span><span class="sxs-lookup"><span data-stu-id="15cd9-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="15cd9-107">Par exemple, vous pourrez configurer une version particulière de votre site Web sur une machine virtuelle Azure ou sur hello staging emplacement sur un site Web de toorun une suite de tests, reproduire un bogue, tester un correctif, évaluer une proposition de modification ou configurer un environnement personnalisé pour une démonstration ou une présentation.</span><span class="sxs-lookup"><span data-stu-id="15cd9-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="15cd9-108">Une fois que vous avez créé un script qui publie votre projet, vous pouvez recréer des environnements identiques en réexécutant le script de hello en fonction des besoins, ou exécuter les script hello avec votre propre build de votre toocreate d’application web un environnement personnalisé pour le test.</span><span class="sxs-lookup"><span data-stu-id="15cd9-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="15cd9-109">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="15cd9-109">What you need</span></span>
* <span data-ttu-id="15cd9-110">Kit de développement logiciel (SDK) Azure 2.3 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="15cd9-111">Pour plus d’informations, consultez [Téléchargements Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) .</span><span class="sxs-lookup"><span data-stu-id="15cd9-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="15cd9-112">Vous n’avez pas besoin de hello Azure SDK toogenerate hello des scripts pour les projets web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="15cd9-113">Cette fonctionnalité s’adresse aux projets web, et non aux rôles web dans les services cloud.</span><span class="sxs-lookup"><span data-stu-id="15cd9-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="15cd9-114">Azure PowerShell 0.7.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="15cd9-115">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="15cd9-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="15cd9-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="15cd9-117">Outils supplémentaires</span><span class="sxs-lookup"><span data-stu-id="15cd9-117">Additional tools</span></span>
<span data-ttu-id="15cd9-118">Des outils et ressources supplémentaires sont disponibles pour l’utilisation de PowerShell dans Visual Studio pour le développement Azure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="15cd9-119">Consultez [Outils PowerShell pour Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="15cd9-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="15cd9-120">Génération de hello publier des scripts</span><span class="sxs-lookup"><span data-stu-id="15cd9-120">Generating hello publish scripts</span></span>
<span data-ttu-id="15cd9-121">Vous pouvez générer hello publier des scripts pour une machine virtuelle qui héberge votre site Web lorsque vous créez un nouveau projet en suivant [ces instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15cd9-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="15cd9-122">Vous pouvez également [Générer des scripts de publication pour les applications web dans Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="15cd9-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="15cd9-123">Scripts générés par Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15cd9-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="15cd9-124">Visual Studio génère un dossier au niveau solution appelé **PublishScripts** qui contient deux fichiers de Windows PowerShell, un script de publication pour votre machine virtuelle ou site Web et un module qui contient les fonctions que vous pouvez utiliser Bonjour scripts.</span><span class="sxs-lookup"><span data-stu-id="15cd9-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="15cd9-125">Visual Studio génère également un fichier au format JSON hello qui spécifie les détails de hello de projet que vous déployez hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="15cd9-126">Script de publication Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="15cd9-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="15cd9-127">Hello du script de publication contient des étapes de déploiement d’ordinateur virtuel ou le site Web de tooa de publication.</span><span class="sxs-lookup"><span data-stu-id="15cd9-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="15cd9-128">Visual Studio propose la coloration de syntaxe pour le développement de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15cd9-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="15cd9-129">Aide pour les fonctions hello est disponible, et vous pouvez modifier librement les fonctions hello dans hello script toosuit vos besoins.</span><span class="sxs-lookup"><span data-stu-id="15cd9-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="15cd9-130">Module Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="15cd9-130">Windows PowerShell module</span></span>
<span data-ttu-id="15cd9-131">Hello Windows PowerShell module généré par Visual Studio contient les fonctions hello publier utilise de script.</span><span class="sxs-lookup"><span data-stu-id="15cd9-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="15cd9-132">Ces sont des fonctions Azure PowerShell et ne sont pas prévu toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="15cd9-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="15cd9-133">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="15cd9-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="15cd9-134">Fichier de configuration JSON</span><span class="sxs-lookup"><span data-stu-id="15cd9-134">JSON configuration file</span></span>
<span data-ttu-id="15cd9-135">fichier JSON de Hello est créé dans hello **Configurations** dossier et contient des données de configuration qui spécifie exactement le tooAzure toodeploy de ressources.</span><span class="sxs-lookup"><span data-stu-id="15cd9-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="15cd9-136">nom de Hello du fichier hello généré par Visual Studio est projet-nom-WAWS-dev.JSON si vous avez créé un site Web ou un projet nom-VM-dev.JSON si vous avez créé une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="15cd9-137">Voici un exemple de fichier de configuration JSON généré lorsque vous créez un site web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="15cd9-138">La plupart des valeurs de hello est explicite.</span><span class="sxs-lookup"><span data-stu-id="15cd9-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="15cd9-139">nom du site Web Hello est généré par Azure, qui peut correspondre pas à votre nom de projet.</span><span class="sxs-lookup"><span data-stu-id="15cd9-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="15cd9-140">Lorsque vous créez une machine virtuelle, fichier de configuration JSON hello recherche similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="15cd9-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="15cd9-141">Notez qu’un service cloud est créé en tant que conteneur pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="15cd9-142">machine virtuelle de Hello contient des points de terminaison habituels hello pour l’accès web via HTTP et HTTPS, ainsi que les points de terminaison pour Web Deploy, qui vous permet de publier le site Web de toohello à partir de votre ordinateur local, Bureau à distance et Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15cd9-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="15cd9-143">Vous pouvez modifier hello JSON configuration toochange que se passe-t-il lorsque vous exécutez hello publier des scripts.</span><span class="sxs-lookup"><span data-stu-id="15cd9-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="15cd9-144">Hello `cloudService` et `virtualMachine` sections sont requises, mais vous pouvez supprimer hello `databases` section si vous n’avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="15cd9-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="15cd9-145">propriétés Hello vides dans le fichier de configuration par défaut hello généré par Visual Studio sont facultatifs ; ceux qui ont des valeurs dans le fichier de configuration par défaut hello sont requis.</span><span class="sxs-lookup"><span data-stu-id="15cd9-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="15cd9-146">Si vous avez un site Web qui a plusieurs environnements de déploiement (ou emplacements) plutôt qu’un site de production unique dans Azure, vous pouvez inclure le nom d’emplacement hello dans nom hello du site Web de hello dans le fichier de configuration JSON hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="15cd9-147">Par exemple, si vous avez un site Web nommé **monsite** et un emplacement correspondant se nomme **test** hello URI est monsite-test.cloudapp.net, mais toouse nom correct de hello dans le fichier de configuration hello est MySite (test) .</span><span class="sxs-lookup"><span data-stu-id="15cd9-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="15cd9-148">Vous pouvez uniquement le faire si les emplacements et le site Web de hello existent déjà dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="15cd9-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="15cd9-149">Si elles n’existent pas, créer un site Web de hello en exécutant le script de hello sans spécifier l’emplacement de hello, puis créez emplacement hello Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), et avant d’exécuter les script hello avec le nom du site Web modifié hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="15cd9-150">Pour plus d’informations sur les emplacements de déploiement pour les applications web, consultez [Configurer des environnements intermédiaires pour les applications web dans Azure App Service](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="15cd9-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="15cd9-151">Comment toorun hello publier des scripts</span><span class="sxs-lookup"><span data-stu-id="15cd9-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="15cd9-152">Si vous n’avez jamais exécuté un script Windows PowerShell avant, vous devez d’abord définir hello exécution stratégie tooenable scripts toorun.</span><span class="sxs-lookup"><span data-stu-id="15cd9-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="15cd9-153">Il s’agit d’un utilisateur de tooprevent fonctionnalité sécurité de l’exécution de scripts Windows PowerShell s’ils sont vulnérable toomalware ou virus impliquant l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="15cd9-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="15cd9-154">Exécutez le script de hello</span><span class="sxs-lookup"><span data-stu-id="15cd9-154">Run hello script</span></span>
1. <span data-ttu-id="15cd9-155">Créer un package de déploiement Web hello pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="15cd9-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="15cd9-156">Un package Web Deploy est une archive compressée (fichier .zip) qui contiennent les fichiers que vous souhaitez un ordinateur virtuel ou le site Web de tooyour toocopy.</span><span class="sxs-lookup"><span data-stu-id="15cd9-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="15cd9-157">Vous pouvez créer des packages Web Deploy dans Visual Studio pour toute application web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Créer un package Web Deploy](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="15cd9-159">Pour plus d’informations, consultez [Comment : créer un package de déploiement web dans Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="15cd9-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="15cd9-160">Vous pouvez également automatiser la création de hello de votre package Web Deploy, comme décrit dans la section de hello **publier des scripts de personnalisation et extension hello** plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="15cd9-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="15cd9-161">Dans **l’Explorateur de solutions**, ouvrez le menu contextuel de hello pour le script de hello, puis choisissez **ouvrir avec PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="15cd9-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="15cd9-162">S’il s’agit hello première fois que vous exécutez des scripts Windows PowerShell sur cet ordinateur, ouvrez une fenêtre d’invite de commandes avec des privilèges d’administrateur et hello type commande suivante :</span><span class="sxs-lookup"><span data-stu-id="15cd9-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="15cd9-163">Connexion tooAzure à l’aide de hello la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="15cd9-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="15cd9-164">Lorsque vous y êtes invité, indiquez votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="15cd9-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="15cd9-165">Notez que cette méthode de fournir des informations d’identification Azure ne fonctionne pas lorsque vous automatisez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="15cd9-166">Au lieu de cela, vous devez utiliser les informations d’identification du tooprovide fichier .publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="15cd9-167">Une fois seulement, vous utilisez commande hello **Get-AzurePublishSettingsFile** hello de toodownload à partir de Azure et par la suite utiliser **Import-AzurePublishSettingsFile** fichier de hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="15cd9-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="15cd9-168">Pour obtenir des instructions détaillées, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15cd9-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="15cd9-169">(Facultatif) Si vous souhaitez toocreate Azure ressources telles que la machine virtuelle de hello, base de données et du site Web sans avoir à publier votre application web, utilisent hello **Publish-WebApplication.ps1** avec hello **-Configuration** argument défini toohello fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="15cd9-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="15cd9-170">Cette commande utilise toodetermine de fichier de configuration de JSON hello le toocreate de ressources.</span><span class="sxs-lookup"><span data-stu-id="15cd9-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="15cd9-171">Car elle utilise les paramètres par défaut de hello pour les autres arguments de ligne de commande, il crée des ressources de hello, mais ne publie pas votre application web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="15cd9-172">Hello – Verbose vous donne plus d’informations sur ce qui se passe.</span><span class="sxs-lookup"><span data-stu-id="15cd9-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="15cd9-173">Hello d’utilisation **Publish-WebApplication.ps1** commande comme indiqué dans un des exemples tooinvoke hello script suivant de hello et publier votre application web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="15cd9-174">Si vous devez les paramètres par défaut toooverride hello des hello autres arguments, comme le nom de l’abonnement hello, nom du package, les informations d’identification de l’ordinateur virtuel ou les informations d’identification du serveur de base de données de publication, vous pouvez spécifier ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="15cd9-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="15cd9-175">Hello d’utilisation **– Verbose** option toosee plus d’informations sur la progression de hello Hello processus de publication.</span><span class="sxs-lookup"><span data-stu-id="15cd9-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="15cd9-176">Si vous créez une machine virtuelle, commande hello ressemble à hello suivant.</span><span class="sxs-lookup"><span data-stu-id="15cd9-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="15cd9-177">Cet exemple montre également comment toospecify hello les informations d’identification pour plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="15cd9-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="15cd9-178">Pour hello machines virtuelles créées par ces scripts, certificats SSL de hello n’est pas à partir d’une autorité racine approuvée.</span><span class="sxs-lookup"><span data-stu-id="15cd9-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="15cd9-179">Par conséquent, vous devez toouse hello **– AllowUntrusted** option.</span><span class="sxs-lookup"><span data-stu-id="15cd9-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="15cd9-180">script de Hello peut créer des bases de données, mais il ne crée pas de serveurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="15cd9-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="15cd9-181">Si vous voulez toocreate un serveur de base de données, vous pouvez utiliser hello **New-AzureSqlDatabaseServer** fonction Bonjour module Azure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="15cd9-182">Personnalisation et extension hello publier des scripts</span><span class="sxs-lookup"><span data-stu-id="15cd9-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="15cd9-183">Vous pouvez personnaliser hello publier le script et le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="15cd9-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="15cd9-184">Hello des fonctions dans le module Windows PowerShell de hello **AzureWebAppPublishModule.psm1** ne sont pas prévu toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="15cd9-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="15cd9-185">Simplement toospecify une autre base de données ou modifier certaines propriétés hello de machine virtuelle de hello, modifier le fichier de configuration JSON hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="15cd9-186">Si vous souhaitez tooextend hello de hello script tooautomate génération et test de votre projet, vous pouvez implémenter les stubs de fonction dans **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="15cd9-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="15cd9-187">tooautomate création de votre projet, ajoutez le code appelant MSBuild trop`New-WebDeployPackage` comme indiqué dans cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="15cd9-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="15cd9-188">chemin d’accès de Hello toohello commande MSBuild est différente selon la version hello de Visual Studio que vous avez installé.</span><span class="sxs-lookup"><span data-stu-id="15cd9-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="15cd9-189">tooget hello chemin d’accès correct, vous pouvez utiliser la fonction de hello **Get-MSBuildCmd**, comme illustré dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="15cd9-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="15cd9-190">tooautomate générer votre projet</span><span class="sxs-lookup"><span data-stu-id="15cd9-190">tooautomate building your project</span></span>
1. <span data-ttu-id="15cd9-191">Ajouter hello `$ProjectFile` paramètre dans la section des paramètres globaux hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="15cd9-192">Copier la fonction hello `Get-MSBuildCmd` dans votre fichier de script.</span><span class="sxs-lookup"><span data-stu-id="15cd9-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="15cd9-193">Remplacez `New-WebDeployPackage` avec hello de code suivant et remplacez les espaces réservés de hello lors de la construction de ligne hello `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="15cd9-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="15cd9-194">Ce code est destiné à Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="15cd9-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="15cd9-195">Si vous utilisez Visual Studio 2013, modifiez hello **VisualStudioVersion** propriété ci-dessous trop`12.0`.</span><span class="sxs-lookup"><span data-stu-id="15cd9-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="15cd9-196">toobuild votre application web, utilisez MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="15cd9-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="15cd9-197">Pour obtenir de l’aide, reportez-vous à la section Référence de ligne de commande MSBuild à l’adresse : [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="15cd9-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="15cd9-198">Démarrer l’exécution de la commande de génération hello</span><span class="sxs-lookup"><span data-stu-id="15cd9-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="15cd9-199">Appelez hello `New-WebDeployPackage` fonction avant cette ligne : `$Config = Read-ConfigFile $Configuration` pour les applications web ou `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` pour les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="15cd9-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="15cd9-200">Appeler script hello personnalisé à partir de la ligne de commande à l’aide de passage hello `$Project` argument, comme dans hello suivant l’exemple de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="15cd9-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="15cd9-201">tooautomate test de votre application, ajoutez le code trop`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="15cd9-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="15cd9-202">Être toouncomment que les lignes hello dans **Publish-WebApplication.ps1** dans lesquelles ces fonctions sont appelées.</span><span class="sxs-lookup"><span data-stu-id="15cd9-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="15cd9-203">Si vous ne fournissez pas d’implémentation, vous pouvez créer manuellement votre projet avec Visual Studio, et puis exécution hello publier tooAzure toopublish de script.</span><span class="sxs-lookup"><span data-stu-id="15cd9-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="15cd9-204">Résumé de la fonction de publication</span><span class="sxs-lookup"><span data-stu-id="15cd9-204">Publishing function summary</span></span>
<span data-ttu-id="15cd9-205">aide tooget pour les fonctions que vous pouvez utiliser à l’invite de commandes Windows PowerShell hello, utilisez la commande hello `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="15cd9-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="15cd9-206">aide de Hello inclut des exemples et l’aide du paramètre.</span><span class="sxs-lookup"><span data-stu-id="15cd9-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="15cd9-207">Hello même aide figure également dans les fichiers sources de script hello **AzureWebAppPublishModule.psm1** et **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="15cd9-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="15cd9-208">aide et script de hello est localisées dans votre langage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15cd9-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="15cd9-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="15cd9-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="15cd9-210">Nom de la fonction</span><span class="sxs-lookup"><span data-stu-id="15cd9-210">Function name</span></span> | <span data-ttu-id="15cd9-211">Description</span><span class="sxs-lookup"><span data-stu-id="15cd9-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15cd9-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="15cd9-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="15cd9-213">Crée une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="15cd9-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="15cd9-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="15cd9-215">Crée les bases de données SQL Azure à partir de valeurs hello hello fichier de configuration JSON généré par Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15cd9-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="15cd9-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="15cd9-216">Add-AzureVM</span></span> |<span data-ttu-id="15cd9-217">Crée une machine virtuelle Azure et renvoie le QU'URL de hello Hello déployé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="15cd9-218">Hello fonction définit les conditions préalables de hello et puis hello d’appels **New-AzureVM** fonction (module Azure) toocreate un nouvel ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="15cd9-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="15cd9-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="15cd9-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="15cd9-220">Ajoute le nouvel ordinateur virtuel de tooa des points de terminaison d’entrée et retourne la machine virtuelle, hello avec nouveau point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="15cd9-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="15cd9-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="15cd9-222">Crée un nouveau compte de stockage Azure dans l’abonnement actif de hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="15cd9-223">nom de Hello du compte de hello commence par « devtest » suivi d’une chaîne alphanumérique unique.</span><span class="sxs-lookup"><span data-stu-id="15cd9-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="15cd9-224">fonction Hello retourne le nom hello du nouveau compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="15cd9-225">Vous devez spécifier un emplacement ou un groupe d’affinités pour le nouveau compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="15cd9-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="15cd9-226">Add-AzureWebsite</span></span> |<span data-ttu-id="15cd9-227">Crée un site Web avec l’emplacement et le nom spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="15cd9-228">Cette fonction appelle hello **New-AzureWebsite** fonction Bonjour module Azure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="15cd9-229">Si l’abonnement de hello n’inclut pas déjà un site Web avec le nom spécifié de hello, cette fonction crée le site Web de hello et retourne un objet de site Web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="15cd9-230">Sinon, la valeur renvoyée est `$null`.</span><span class="sxs-lookup"><span data-stu-id="15cd9-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="15cd9-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="15cd9-231">Backup-Subscription</span></span> |<span data-ttu-id="15cd9-232">Enregistre hello abonnement Azure actuel Bonjour `$Script:originalSubscription` variable dans l’étendue du script. Cette fonction enregistre l’abonnement Azure hello (tels qu’obtenus par `Get-AzureSubscription -Current`) et son compte de stockage et abonnement hello modifié par ce script (stocké dans la variable de hello `$UserSpecifiedSubscription`) et son compte de stockage, dans l’étendue du script.</span><span class="sxs-lookup"><span data-stu-id="15cd9-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="15cd9-233">En enregistrant les valeurs hello, vous pouvez utiliser une fonction, tels que `Restore-Subscription`, toorestore hello d’origine abonnement et stockage compte toocurrent état actuel si l’état actuel de hello a changé.</span><span class="sxs-lookup"><span data-stu-id="15cd9-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="15cd9-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="15cd9-234">Find-AzureVM</span></span> |<span data-ttu-id="15cd9-235">Obtient hello spécifié de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="15cd9-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="15cd9-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="15cd9-237">Ajoute un message tooa date et l’heure d’appel.</span><span class="sxs-lookup"><span data-stu-id="15cd9-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="15cd9-238">Cette fonction est conçue pour les messages écrits toohello des flux d’erreurs et de commentaires.</span><span class="sxs-lookup"><span data-stu-id="15cd9-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="15cd9-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="15cd9-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="15cd9-240">Assemble une base de données de connexion chaîne tooconnect tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="15cd9-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="15cd9-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="15cd9-242">Retourne hello nom hello premier du compte de stockage avec le modèle de nom hello « devtest*» (la casse) dans le groupe hello emplacement ou d’affinités spécifié. Si hello « devtest*« compte de stockage ne correspond pas à groupe d’affinités ou emplacement de hello, hello fonction l’ignore.</span><span class="sxs-lookup"><span data-stu-id="15cd9-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="15cd9-243">Vous devez spécifier un emplacement ou un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="15cd9-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="15cd9-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="15cd9-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="15cd9-245">Retourne un outil de commande toorun hello MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="15cd9-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="15cd9-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="15cd9-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="15cd9-247">Recherche ou crée un ordinateur virtuel dans l’abonnement hello qui correspond aux valeurs hello dans le fichier de configuration JSON hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="15cd9-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="15cd9-248">Publish-WebPackage</span></span> |<span data-ttu-id="15cd9-249">Utilise MsDeploy.exe et un site web publient le package. ZIP fichier toodeploy ressources tooa site Web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="15cd9-250">Cette fonction ne génère aucune sortie.</span><span class="sxs-lookup"><span data-stu-id="15cd9-250">This function doesn't generate any output.</span></span> <span data-ttu-id="15cd9-251">Si hello appel tooMSDeploy.exe échoue, la fonction hello lève une exception.</span><span class="sxs-lookup"><span data-stu-id="15cd9-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="15cd9-252">tooget plus les résultats détaillés, utilisez hello **-Verbose** option.</span><span class="sxs-lookup"><span data-stu-id="15cd9-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="15cd9-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="15cd9-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="15cd9-254">Vérifie les valeurs de paramètre hello et appelle ensuite hello **Publish-WebPackage** (fonction).</span><span class="sxs-lookup"><span data-stu-id="15cd9-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="15cd9-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="15cd9-255">Read-ConfigFile</span></span> |<span data-ttu-id="15cd9-256">Valide le fichier de configuration JSON hello et retourne une table de hachage des valeurs sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="15cd9-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="15cd9-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="15cd9-257">Restore-Subscription</span></span> |<span data-ttu-id="15cd9-258">Réinitialise l’abonnement d’origine hello actuel abonnement toohello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="15cd9-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="15cd9-259">Test-AzureModule</span></span> |<span data-ttu-id="15cd9-260">Retourne `$true` si hello installé Azure module version 0.7.4 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="15cd9-261">Retourne `$false` si le module de hello n’est pas installé ou est une version antérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="15cd9-262">Cette fonction n’a pas de paramètres.</span><span class="sxs-lookup"><span data-stu-id="15cd9-262">This function has no parameters.</span></span> |
| <span data-ttu-id="15cd9-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="15cd9-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="15cd9-264">Retourne `$true` si hello hello module Azure est 0.7.4 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="15cd9-265">Retourne `$false` si le module de hello n’est pas installé ou est une version antérieure.</span><span class="sxs-lookup"><span data-stu-id="15cd9-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="15cd9-266">Cette fonction n’a pas de paramètres.</span><span class="sxs-lookup"><span data-stu-id="15cd9-266">This function has no parameters.</span></span> |
| <span data-ttu-id="15cd9-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="15cd9-267">Test-HttpsUrl</span></span> |<span data-ttu-id="15cd9-268">Convertit l’objet de hello d’entrée URL tooa System.Uri.</span><span class="sxs-lookup"><span data-stu-id="15cd9-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="15cd9-269">Retourne `$True` si hello URL est absolue et son schéma est https.</span><span class="sxs-lookup"><span data-stu-id="15cd9-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="15cd9-270">Retourne `$false` si hello URL est relative, son schéma n’est pas HTTPS ou hello la chaîne d’entrée doit être converti tooa URL.</span><span class="sxs-lookup"><span data-stu-id="15cd9-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="15cd9-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="15cd9-271">Test-Member</span></span> |<span data-ttu-id="15cd9-272">Retourne `$true` si une propriété ou méthode est un membre d’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="15cd9-273">Sinon, renvoie `$false`.</span><span class="sxs-lookup"><span data-stu-id="15cd9-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="15cd9-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="15cd9-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="15cd9-275">Écrit un message d’erreur hello précédé de l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="15cd9-276">Cette fonction appelle hello **Format-DevTestMessageWithTime** fonction tooprepend durée hello time avant d’écrire le flux d’erreur hello message toohello.</span><span class="sxs-lookup"><span data-stu-id="15cd9-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="15cd9-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="15cd9-277">Write-HostWithTime</span></span> |<span data-ttu-id="15cd9-278">Écrit un programme hôte de message toohello (**Write-Host**) hello précédé de l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="15cd9-279">effet Hello de l’écriture de programme de l’hôte toohello varie.</span><span class="sxs-lookup"><span data-stu-id="15cd9-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="15cd9-280">La plupart des programmes qui hébergent Windows PowerShell écrire ces messages toostandard sortie.</span><span class="sxs-lookup"><span data-stu-id="15cd9-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="15cd9-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="15cd9-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="15cd9-282">Écrit un message détaillé précédé de hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="15cd9-283">Étant donné qu’il appelle **Write-Verbose**, message de type hello affiche uniquement lorsque le script de hello est exécuté avec hello **Verbose** paramètre ou lorsque hello **VerbosePreference** préférence est définir trop**continuer**.</span><span class="sxs-lookup"><span data-stu-id="15cd9-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="15cd9-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="15cd9-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="15cd9-285">Nom de la fonction</span><span class="sxs-lookup"><span data-stu-id="15cd9-285">Function name</span></span> | <span data-ttu-id="15cd9-286">Description</span><span class="sxs-lookup"><span data-stu-id="15cd9-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15cd9-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="15cd9-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="15cd9-288">Crée des ressources Azure, comme un site web ou une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15cd9-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="15cd9-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="15cd9-289">New-WebDeployPackage</span></span> |<span data-ttu-id="15cd9-290">Cette fonction n’est pas implémentée.</span><span class="sxs-lookup"><span data-stu-id="15cd9-290">This function isn't implemented.</span></span> <span data-ttu-id="15cd9-291">Vous pouvez ajouter des commandes dans cette toobuild fonction votre projet.</span><span class="sxs-lookup"><span data-stu-id="15cd9-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="15cd9-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="15cd9-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="15cd9-293">Publie un tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="15cd9-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="15cd9-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="15cd9-294">Publish-WebApplication</span></span> |<span data-ttu-id="15cd9-295">Crée et déploie des applications web, des machines virtuelles, des bases de données SQL et des comptes de stockage pour un projet web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15cd9-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="15cd9-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="15cd9-296">Test-WebApplication</span></span> |<span data-ttu-id="15cd9-297">Cette fonction n’est pas implémentée.</span><span class="sxs-lookup"><span data-stu-id="15cd9-297">This function isn't implemented.</span></span> <span data-ttu-id="15cd9-298">Vous pouvez ajouter des commandes dans cette tootest fonction votre application.</span><span class="sxs-lookup"><span data-stu-id="15cd9-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="15cd9-299">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15cd9-299">Next steps</span></span>
<span data-ttu-id="15cd9-300">En savoir plus sur les scripts PowerShell en lisant [écriture de scripts avec Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) et consultez les autres scripts Azure PowerShell à hello [centre de scripts](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="15cd9-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
