---
title: Utilisation de io.js avec Azure App Service Web Apps
description: "Apprenez à utiliser une application web dans Azure App Service avec io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="b57c4-103">Utilisation de io.js avec Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="b57c4-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="b57c4-104">L'embranchement (ou « fork » en anglais) bien connu de Node, [io.js] , se différencie du projet Node.js de Joyent sur plusieurs points, avec notamment un modèle de gouvernance plus ouvert, un cycle de développement plus rapide et une adoption plus rapide des fonctionnalités nouvelles et expérimentales de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b57c4-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="b57c4-105">Bien que de nombreuses versions de Node.js soient préinstallées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps, il accepte aussi les binaires Node.js fournis par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b57c4-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="b57c4-106">Cet article décrit deux méthodes permettant l’utilisation de io.js sur App Service Web Apps : l'utilisation d'un script de déploiement étendu, qui configure automatiquement Azure pour utiliser la dernière version disponible de io.js, ainsi que le téléchargement manuel d'un binaire io.js.</span><span class="sxs-lookup"><span data-stu-id="b57c4-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="b57c4-107">Utilisation d'un script de déploiement</span><span class="sxs-lookup"><span data-stu-id="b57c4-107">Using a Deployment Script</span></span>
<span data-ttu-id="b57c4-108">À l'occasion du déploiement d'une application Node.js, App Service Web Apps exécute un certain nombre de petites commandes pour s'assurer que l'environnement est configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="b57c4-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="b57c4-109">En utilisant un script de déploiement, ce processus peut être personnalisé pour inclure le téléchargement et la configuration de io.js.</span><span class="sxs-lookup"><span data-stu-id="b57c4-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="b57c4-110">Le [script de déploiement de io.js](https://github.com/felixrieseberg/iojs-azure) est disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="b57c4-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="b57c4-111">Pour activer io.js sur votre application web, il vous suffit de copier **.deployment**, **deploy.cmd** et **IISNode.yml** à la racine du dossier de votre application et de le déployer vers Web Apps.</span><span class="sxs-lookup"><span data-stu-id="b57c4-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="b57c4-112">Le premier fichier, **.deployment**, donne comme instruction à Web Apps d’exécuter **deploy.cmd** au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="b57c4-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="b57c4-113">Ce script exécute non seulement toutes les étapes habituelles pour une application Node.js, mais télécharge aussi la dernière version de io.js.</span><span class="sxs-lookup"><span data-stu-id="b57c4-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="b57c4-114">Enfin, **IISNode.yml** configure Web Apps pour qu'il utilise le binaire io.js que vous venez de télécharger à la place d'un binaire Node.js préinstallé.</span><span class="sxs-lookup"><span data-stu-id="b57c4-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="b57c4-115">Pour mettre à jour le binaire io.js utilisé, il vous suffit de redéployer votre application (le script télécharge une nouvelle version de io.js chaque fois que l'application est déployée).</span><span class="sxs-lookup"><span data-stu-id="b57c4-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="b57c4-116">Utilisation de l'installation manuelle</span><span class="sxs-lookup"><span data-stu-id="b57c4-116">Using Manual Installation</span></span>
<span data-ttu-id="b57c4-117">L'installation manuelle d'une version personnalisée de io.js se fait en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="b57c4-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="b57c4-118">Tout d'abord, téléchargez le binaire **win-x64** directement à partir de la [distribution io.js].</span><span class="sxs-lookup"><span data-stu-id="b57c4-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="b57c4-119">Deux fichiers sont nécessaires : **iojs.exe** et **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="b57c4-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="b57c4-120">Enregistrez ces deux fichiers dans un dossier à l'intérieur de votre application web, par exemple, dans **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="b57c4-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="b57c4-121">Pour faire en sorte que Web Apps utilise **iojs.exe** à la place d’une version préinstallée de Node, créez un fichier **IISNode.yml** à la racine de votre application et ajoutez la ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="b57c4-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="b57c4-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b57c4-122">Next Steps</span></span>
<span data-ttu-id="b57c4-123">Dans cet article, vous avez appris à utiliser io.js avec App Service Web Apps, en utilisant à la fois les scripts de déploiement fournis et l'installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="b57c4-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="b57c4-124">io.js fait l'objet d'un développement intense et est plus souvent mis à jour que Node.js.</span><span class="sxs-lookup"><span data-stu-id="b57c4-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="b57c4-125">Il est possible qu’un certain nombre de modules Node.js ne fonctionnent pas avec io.js. Consultez la rubrique consacrée à [io.js sur GitHub] pour résoudre les problèmes éventuels.</span><span class="sxs-lookup"><span data-stu-id="b57c4-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b57c4-126">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="b57c4-126">What's changed</span></span>
* <span data-ttu-id="b57c4-127">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b57c4-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="b57c4-128">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="b57c4-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b57c4-129">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="b57c4-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="b57c4-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="b57c4-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="b57c4-131">[distribution io.js]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="b57c4-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="b57c4-132">[io.js sur GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="b57c4-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
