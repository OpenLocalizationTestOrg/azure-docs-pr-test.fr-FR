---
title: "Configurer un environnement de développement pour les microservices Azure | Microsoft Docs"
description: "Installez le runtime, le kit de développement logiciel et créez un cluster de développement local. Une fois l’installation terminée, vous serez prêt à créer des applications."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: f0c6957217c21bdfd76498944e248fc808f2d271
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="3da0c-104">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="3da0c-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3da0c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="3da0c-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="3da0c-106">Linux</span><span class="sxs-lookup"><span data-stu-id="3da0c-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="3da0c-107">OSX</span><span class="sxs-lookup"><span data-stu-id="3da0c-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="3da0c-108">Pour générer et exécuter des [applications Azure Service Fabric][1] sur votre ordinateur de développement, installez le runtime, le Kit de développement logiciel (SDK) et les outils.</span><span class="sxs-lookup"><span data-stu-id="3da0c-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="3da0c-109">Vous devez également activer l’exécution des scripts Windows PowerShell inclus dans le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="3da0c-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3da0c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3da0c-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="3da0c-111">Versions du système d’exploitation prises en charge</span><span class="sxs-lookup"><span data-stu-id="3da0c-111">Supported operating system versions</span></span>
<span data-ttu-id="3da0c-112">Les versions de système d’exploitation prises en charge pour le développement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3da0c-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="3da0c-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3da0c-113">Windows 7</span></span>
* <span data-ttu-id="3da0c-114">Windows 8 et Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3da0c-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="3da0c-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3da0c-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="3da0c-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3da0c-116">Windows Server 2016</span></span>
* <span data-ttu-id="3da0c-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="3da0c-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="3da0c-118">Windows 7 inclut uniquement Windows PowerShell 2.0 par défaut.</span><span class="sxs-lookup"><span data-stu-id="3da0c-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="3da0c-119">Les applets de commande PowerShell de Service Fabric nécessitent PowerShell 3.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3da0c-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="3da0c-120">Vous pouvez [télécharger Windows PowerShell 5.0][powershell5-download] à partir du Centre de téléchargement Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3da0c-120">You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.</span></span>
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="3da0c-121">Installer le Kit de développement logiciel (SDK) et les outils</span><span class="sxs-lookup"><span data-stu-id="3da0c-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="3da0c-122">Pour utiliser Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3da0c-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="3da0c-123">Les outils Service Fabric font partie de la charge de travail de développement et de gestion Azure dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3da0c-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="3da0c-124">Activez cette charge de travail dans le cadre de votre installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3da0c-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="3da0c-125">En outre, vous devez installer le Kit de développement logiciel (SDK) Microsoft Azure Service Fabric, à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="3da0c-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="3da0c-126">[Installer le Kit de développement logiciel (SDK) Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="3da0c-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="3da0c-127">Pour utiliser Visual Studio 2015 (requiert Visual Studio 2015 Update 2 ou une version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="3da0c-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="3da0c-128">Pour Visual Studio 2015, les outils Service Fabric sont installés avec le Kit de développement logiciel (SDK), à l’aide de Web Platform Installer :</span><span class="sxs-lookup"><span data-stu-id="3da0c-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="3da0c-129">[Installer le Kit de développement logiciel (SDK) et les outils de Microsoft Azure Service Fabric][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="3da0c-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="3da0c-130">Installation du Kit de développement logiciel (SDK) uniquement</span><span class="sxs-lookup"><span data-stu-id="3da0c-130">SDK installation only</span></span>
<span data-ttu-id="3da0c-131">Si vous avez uniquement besoin du SDK, vous pouvez installer ce package :</span><span class="sxs-lookup"><span data-stu-id="3da0c-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="3da0c-132">[Installer le Kit de développement logiciel (SDK) Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="3da0c-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="3da0c-133">Les versions actuelles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3da0c-133">The current versions are:</span></span>
* <span data-ttu-id="3da0c-134">Kit de développement logiciel (SDK) Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="3da0c-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="3da0c-135">Runtime Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="3da0c-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="3da0c-136">Outils Service Fabric pour Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="3da0c-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="3da0c-137">Visual Studio 2017 Update 2 inclut les outils Service Fabric pour Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="3da0c-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="3da0c-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) inclut les outils Service Fabric pour Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="3da0c-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="3da0c-139">Pour obtenir la liste des versions prises en charge, consultez l’article [Service Fabric support (Options de prise en charge de Service Fabric)](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="3da0c-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="3da0c-140">Activer l'exécution du script PowerShell</span><span class="sxs-lookup"><span data-stu-id="3da0c-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="3da0c-141">Service Fabric utilise des scripts Windows PowerShell pour créer un cluster de développement local et déployer des applications à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3da0c-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="3da0c-142">Par défaut, Windows bloque l’exécution de ces scripts.</span><span class="sxs-lookup"><span data-stu-id="3da0c-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="3da0c-143">Pour les activer, vous devez modifier votre stratégie d'exécution PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3da0c-143">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="3da0c-144">Ouvrez PowerShell en tant qu'administrateur et entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3da0c-144">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="3da0c-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3da0c-145">Next steps</span></span>
<span data-ttu-id="3da0c-146">Maintenant que vous avez fini de configurer votre environnement de développement, commencez à créer et à exécuter des applications.</span><span class="sxs-lookup"><span data-stu-id="3da0c-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="3da0c-147">Créer votre première application Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3da0c-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="3da0c-148">Découvrez comment déployer et gérer des applications sur votre cluster local</span><span class="sxs-lookup"><span data-stu-id="3da0c-148">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="3da0c-149">En savoir plus sur les modèles de programmation : acteurs fiables et services fiables</span><span class="sxs-lookup"><span data-stu-id="3da0c-149">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="3da0c-150">Consulter les exemples de code Service Fabric sur GitHub</span><span class="sxs-lookup"><span data-stu-id="3da0c-150">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="3da0c-151">Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="3da0c-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="3da0c-152">Suivre le parcours d’apprentissage Service Fabric pour une introduction générale à la plate-forme</span><span class="sxs-lookup"><span data-stu-id="3da0c-152">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="3da0c-153">En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="3da0c-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<span data-ttu-id="3da0c-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Page de campagne Service Fabric"</span><span class="sxs-lookup"><span data-stu-id="3da0c-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"</span></span>
<span data-ttu-id="3da0c-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span><span class="sxs-lookup"><span data-stu-id="3da0c-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span></span>
<span data-ttu-id="3da0c-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Lien WebPI VS 2015"</span><span class="sxs-lookup"><span data-stu-id="3da0c-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"</span></span>
<span data-ttu-id="3da0c-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Lien WebPI Dev15"</span><span class="sxs-lookup"><span data-stu-id="3da0c-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"</span></span>
<span data-ttu-id="3da0c-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Lien WebPI du Kit de développement logiciel principal"</span><span class="sxs-lookup"><span data-stu-id="3da0c-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"</span></span>
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
