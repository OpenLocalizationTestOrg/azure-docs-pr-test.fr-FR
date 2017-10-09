---
title: io.js de toouse aaaHow avec Azure App Service Web Apps
description: "Découvrez comment toouse une application web dans Azure App Service avec io.js."
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="f6d10-103">Comment io.js toouse avec Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="f6d10-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="f6d10-104">branchement de nœud populaires Hello [io.js] fonctionnalités de projet de Node.js de tooJoyent différences différents, y compris un modèle de gouvernance plus ouvert, un cycle de publication plus rapide et une adoption plus rapide de nouvelles fonctionnalités JavaScript expérimentales.</span><span class="sxs-lookup"><span data-stu-id="f6d10-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="f6d10-105">Bien que de nombreuses versions de Node.js soient préinstallées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps, il accepte aussi les binaires Node.js fournis par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f6d10-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="f6d10-106">Cet article décrit deux méthodes l’activation hello de io.js sur les applications Web App Service : hello l’utilisation d’un script de déploiement étendue, qui configure automatiquement la version la plus récente disponible io.js toouse Azure hello, ainsi que le chargement manuel d’un fichier binaire io.js hello.</span><span class="sxs-lookup"><span data-stu-id="f6d10-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="f6d10-107">Utilisation d'un script de déploiement</span><span class="sxs-lookup"><span data-stu-id="f6d10-107">Using a Deployment Script</span></span>
<span data-ttu-id="f6d10-108">Lors du déploiement d’une application Node.js, les applications Web App Service s’exécute un nombre de petites commandes tooensure qui hello environnement est correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="f6d10-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="f6d10-109">À l’aide d’un script de déploiement, ce processus peut être téléchargement de hello tooinclude personnalisé et de la configuration de io.js.</span><span class="sxs-lookup"><span data-stu-id="f6d10-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="f6d10-110">Hello [io.js Script de déploiement](https://github.com/felixrieseberg/iojs-azure) est disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6d10-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="f6d10-111">io.js tooenable sur votre application web, il suffit de copier **.deployment**, **deploy.cmd** et **IISNode.yml** racine toohello de votre dossier d’application et déployer des applications de tooWeb.</span><span class="sxs-lookup"><span data-stu-id="f6d10-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="f6d10-112">premier fichier de Hello, **.deployment**, fait en sorte que les applications Web toorun **deploy.cmd** lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6d10-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="f6d10-113">Ce script s’exécute toutes les étapes habituelles hello pour une application Node.js, mais télécharge aussi la version la plus récente de io.js hello.</span><span class="sxs-lookup"><span data-stu-id="f6d10-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="f6d10-114">Enfin, **IISNode.yml** Configure Web Apps toouse hello simplement téléchargé io.js binaire au lieu d’un binaire Node.js préinstallé.</span><span class="sxs-lookup"><span data-stu-id="f6d10-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="f6d10-115">tooupdate hello utilisé io.js binaire, simplement redéployez l’application - script de hello télécharge une nouvelle version de io.js que chaque application hello de temps unique est déployée.</span><span class="sxs-lookup"><span data-stu-id="f6d10-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="f6d10-116">Utilisation de l'installation manuelle</span><span class="sxs-lookup"><span data-stu-id="f6d10-116">Using Manual Installation</span></span>
<span data-ttu-id="f6d10-117">une installation manuelle d’une version personnalisée io.js Hello comprend uniquement deux étapes.</span><span class="sxs-lookup"><span data-stu-id="f6d10-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="f6d10-118">Commencez par télécharger hello **win-x64** binaire directement à partir de hello [io.js distribution].</span><span class="sxs-lookup"><span data-stu-id="f6d10-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="f6d10-119">Deux fichiers sont nécessaires : **iojs.exe** et **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="f6d10-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="f6d10-120">Enregistrer les deux fichiers dossier tooa à l’intérieur de votre application web, par exemple dans **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="f6d10-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="f6d10-121">tooconfigure Web Apps toouse **iojs.exe** au lieu d’une version préinstallée de nœud, créez un **IISNode.yml** à la racine de hello de votre application et ajoutez hello ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="f6d10-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="f6d10-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6d10-122">Next Steps</span></span>
<span data-ttu-id="f6d10-123">Dans cet article, vous avez appris comment io.js toouse avec les applications Web App Service, à l’aide fournie scripts de déploiement, ainsi que l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="f6d10-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6d10-124">io.js fait l'objet d'un développement intense et est plus souvent mis à jour que Node.js.</span><span class="sxs-lookup"><span data-stu-id="f6d10-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="f6d10-125">Il est possible qu’un certain nombre de modules Node.js ne fonctionnent pas avec io.js. Consultez la rubrique consacrée à [io.js sur GitHub] pour résoudre les problèmes éventuels.</span><span class="sxs-lookup"><span data-stu-id="f6d10-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f6d10-126">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="f6d10-126">What's changed</span></span>
* <span data-ttu-id="f6d10-127">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f6d10-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="f6d10-128">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="f6d10-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f6d10-129">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="f6d10-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distribution]: https://iojs.org/dist/
[io.js sur GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
