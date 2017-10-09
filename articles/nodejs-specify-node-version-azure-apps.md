---
title: aaaSpecifying une Version de Node.js
description: "Découvrez comment toospecify hello version de Node.js utilisé par les Sites Web Azure et les Services de Cloud"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="70e6c-103">Spécification d'une version Node.js dans une application Azure</span><span class="sxs-lookup"><span data-stu-id="70e6c-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="70e6c-104">Lorsque vous hébergez une application Node.js, vous souhaiterez peut-être tooensure que votre application utilise une version spécifique de Node.js.</span><span class="sxs-lookup"><span data-stu-id="70e6c-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="70e6c-105">Il existe plusieurs façons tooaccomplish cela pour les applications hébergées sur Azure.</span><span class="sxs-lookup"><span data-stu-id="70e6c-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="70e6c-106">Versions par défaut</span><span class="sxs-lookup"><span data-stu-id="70e6c-106">Default versions</span></span>
<span data-ttu-id="70e6c-107">Hello Node.js versions fournies par Azure sont constamment mises à jour.</span><span class="sxs-lookup"><span data-stu-id="70e6c-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="70e6c-108">Sauf indication contraire, hello version par défaut qui est spécifiée dans hello `WEBSITE_NODE_DEFAULT_VERSION` variable d’environnement sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="70e6c-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="70e6c-109">toooverride cette valeur par défaut, suivez les étapes hello dans les sections suivantes de cet article</span><span class="sxs-lookup"><span data-stu-id="70e6c-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="70e6c-110">Si vous hébergez votre application dans un Service de Cloud Azure (rôle web ou de travail), et il est hello la première fois que vous avez déployé application hello, Azure tentera toouse hello la même version de Node.js que vous avez installé sur votre environnement de développement si il correspond à une des versions par défaut de hello disponibles sur Azure.</span><span class="sxs-lookup"><span data-stu-id="70e6c-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="70e6c-111">Contrôle de version avec package.json</span><span class="sxs-lookup"><span data-stu-id="70e6c-111">Versioning with package.json</span></span>
<span data-ttu-id="70e6c-112">Vous pouvez spécifier la version de hello de toobe Node.js utilisée en ajoutant hello suivant tooyour **package.json** fichier :</span><span class="sxs-lookup"><span data-stu-id="70e6c-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="70e6c-113">Où *version* est toouse numéro de version spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="70e6c-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="70e6c-114">Vous pouvez spécifier des conditions plus complexes, telles que :</span><span class="sxs-lookup"><span data-stu-id="70e6c-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="70e6c-115">Étant donné que 0.6.22 n’est pas une des versions hello disponibles dans l’environnement d’hébergement de hello, hello version la plus récente de hello 0,8 série disponible sera utilisé à la place - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="70e6c-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="70e6c-116">Contrôle de version des sites web avec les paramètres d'application</span><span class="sxs-lookup"><span data-stu-id="70e6c-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="70e6c-117">Si vous hébergez une application hello dans un site Web, vous pouvez définir la variable d’environnement hello **WEBSITE_NODE_DEFAULT_VERSION** toohello les version souhaitée.</span><span class="sxs-lookup"><span data-stu-id="70e6c-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="70e6c-118">Contrôle de version des services cloud avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="70e6c-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="70e6c-119">Si vous hébergez l’application hello dans un Service Cloud et que vous déployez application hello à l’aide d’Azure PowerShell, vous pouvez remplacer la version de Node.js hello par défaut à l’aide de hello **Set-AzureServiceProjectRole** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70e6c-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="70e6c-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="70e6c-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="70e6c-121">Paramètres de hello Bonjour ci-dessus instruction respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="70e6c-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="70e6c-122">Vous pouvez vérifier la version correcte de hello de Node.js a été sélectionnée en vérifiant hello **moteurs** propriété de votre rôle **package.json**.</span><span class="sxs-lookup"><span data-stu-id="70e6c-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="70e6c-123">Vous pouvez également utiliser hello **Get-AzureServiceProjectRoleRuntime** tooretrieve une liste des versions de Node.js disponibles pour les applications hébergées en tant qu’un Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="70e6c-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="70e6c-124">Vérifiez toujours la version hello de Node.js dépend de votre projet est dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="70e6c-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="70e6c-125">Utilisation d'une version personnalisée avec Azure Websites</span><span class="sxs-lookup"><span data-stu-id="70e6c-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="70e6c-126">Azure fournit plusieurs versions par défaut de Node.js, vous souhaiterez toouse une version qui n’est pas fournie par défaut.</span><span class="sxs-lookup"><span data-stu-id="70e6c-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="70e6c-127">Si votre application est hébergée comme un site Web Azure, vous pouvez le faire à l’aide de hello **iisnode.yml** fichier.</span><span class="sxs-lookup"><span data-stu-id="70e6c-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="70e6c-128">Hello suit Guide hello processus d’à l’aide d’une version personnalisée de Node.Js avec un site Web Azure :</span><span class="sxs-lookup"><span data-stu-id="70e6c-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="70e6c-129">Créer un nouveau répertoire et créez ensuite un **server.js** fichier dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="70e6c-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="70e6c-130">Hello **server.js** fichier doit contenir les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="70e6c-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="70e6c-131">Cette action affiche la version de Node.js hello utilisée lorsque vous parcourez le site Web de hello.</span><span class="sxs-lookup"><span data-stu-id="70e6c-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="70e6c-132">Créer un nouveau site Web et le nom de la note hello du site de hello.</span><span class="sxs-lookup"><span data-stu-id="70e6c-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="70e6c-133">Par exemple, suivant de hello utilise hello [des outils de ligne de commande Azure] toocreate un site Web Azure nommé **monsiteweb**et que vous activez un référentiel Git pour le site Web de hello.</span><span class="sxs-lookup"><span data-stu-id="70e6c-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="70e6c-134">Créer un nouveau répertoire nommé **bin** en tant qu’enfant du répertoire hello contenant hello **server.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="70e6c-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="70e6c-135">Télécharger une version spécifique de hello **node.exe** (version de Windows hello) que vous souhaitez toouse avec votre application.</span><span class="sxs-lookup"><span data-stu-id="70e6c-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="70e6c-136">Par exemple, hello suivant utilise **curl** version de toodownload 0.8.1 :</span><span class="sxs-lookup"><span data-stu-id="70e6c-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="70e6c-137">Enregistrer hello **node.exe** fichier hello **bin** dossier créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="70e6c-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="70e6c-138">Créer un **iisnode.yml** fichier Bonjour même répertoire que hello **server.js** et puis ajoutez hello suivant toohello contenu **iisnode.yml** fichier :</span><span class="sxs-lookup"><span data-stu-id="70e6c-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="70e6c-139">Ce chemin d’accès est où hello **node.exe** fichier au sein de votre projet se trouve une fois que vous avez publié votre application de toohello site Web Azure.</span><span class="sxs-lookup"><span data-stu-id="70e6c-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="70e6c-140">Publiez votre application.</span><span class="sxs-lookup"><span data-stu-id="70e6c-140">Publish your application.</span></span> <span data-ttu-id="70e6c-141">Par exemple, étant donné que j’ai créé un nouveau site Web avec le paramètre hello--git précédemment, hello commandes suivantes seront ajoutez hello application fichiers toomy référentiel Git et les transmettre de référentiel de site Web toohello :</span><span class="sxs-lookup"><span data-stu-id="70e6c-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="70e6c-142">Après la publication de l’application hello, ouvrez le site Web de hello dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="70e6c-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="70e6c-143">Le message suivant doit apparaître : « Hello from Azure running node version: v0.8.1 ».</span><span class="sxs-lookup"><span data-stu-id="70e6c-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="70e6c-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70e6c-144">Next Steps</span></span>
<span data-ttu-id="70e6c-145">Maintenant que vous comprenez comment la version de hello toospecify de Node.js utilisées par votre application, découvrez comment trop[fonctionnent avec les modules], [générer et déployer un Site Web de Node.js](app-service-web/app-service-web-get-started-nodejs.md), et [comment toouse hello Azure Outils de ligne de commande pour Mac et Linux].</span><span class="sxs-lookup"><span data-stu-id="70e6c-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="70e6c-146">Pour plus d’informations, consultez hello [centre de développement Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="70e6c-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[comment toouse hello Azure Outils de ligne de commande pour Mac et Linux]:cli-install-nodejs.md
[des outils de ligne de commande Azure]:cli-install-nodejs.md
[fonctionnent avec les modules]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
