---
title: "aaaSet d’un environnement de développement pour Azure microservices | Documents Microsoft"
description: "Installer le runtime de hello, Kit de développement logiciel et les outils et créer un cluster de développement local. Après avoir terminé cette installation, vous serez prêt toobuild applications."
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
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="4808a-104">Préparer votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="4808a-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4808a-105">Windows</span><span class="sxs-lookup"><span data-stu-id="4808a-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="4808a-106">Linux</span><span class="sxs-lookup"><span data-stu-id="4808a-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="4808a-107">OSX</span><span class="sxs-lookup"><span data-stu-id="4808a-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="4808a-108">toobuild et exécutez [les applications Azure Service Fabric] [ 1] sur votre ordinateur de développement, installez hello runtime, Kit de développement logiciel et les outils.</span><span class="sxs-lookup"><span data-stu-id="4808a-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="4808a-109">Vous devez également l’exécution de tooenable des scripts Windows PowerShell de hello inclus dans le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="4808a-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4808a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4808a-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="4808a-111">Versions du système d’exploitation prises en charge</span><span class="sxs-lookup"><span data-stu-id="4808a-111">Supported operating system versions</span></span>
<span data-ttu-id="4808a-112">Hello versions de système d’exploitation suivantes est prises en charge pour le développement :</span><span class="sxs-lookup"><span data-stu-id="4808a-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="4808a-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="4808a-113">Windows 7</span></span>
* <span data-ttu-id="4808a-114">Windows 8 et Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="4808a-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="4808a-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4808a-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="4808a-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4808a-116">Windows Server 2016</span></span>
* <span data-ttu-id="4808a-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4808a-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="4808a-118">Windows 7 inclut uniquement Windows PowerShell 2.0 par défaut.</span><span class="sxs-lookup"><span data-stu-id="4808a-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="4808a-119">Les applets de commande PowerShell de Service Fabric nécessitent PowerShell 3.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4808a-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="4808a-120">Vous pouvez [télécharger Windows PowerShell 5.0] [ powershell5-download] de hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="4808a-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="4808a-121">Installer les outils et Kit de développement logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="4808a-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="4808a-122">toouse Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4808a-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="4808a-123">Outils de l’infrastructure de service font partie de hello développement Azure et gestion de la charge de travail dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4808a-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="4808a-124">Activez cette charge de travail dans le cadre de votre installation de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4808a-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="4808a-125">En outre, vous devez tooinstall hello Microsoft Azure Service Fabric SDK, à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="4808a-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="4808a-126">[Installer hello Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="4808a-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="4808a-127">toouse Visual Studio 2015 (requiert Visual Studio 2015 Update 2 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="4808a-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="4808a-128">Pour Visual Studio 2015, les outils de l’infrastructure de Service sont installés avec hello SDK, à l’aide de hello Web Platform Installer :</span><span class="sxs-lookup"><span data-stu-id="4808a-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="4808a-129">[Installer les outils et hello Microsoft Azure Service Fabric SDK][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="4808a-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="4808a-130">Installation du Kit de développement logiciel (SDK) uniquement</span><span class="sxs-lookup"><span data-stu-id="4808a-130">SDK installation only</span></span>
<span data-ttu-id="4808a-131">Si vous devez uniquement hello SDK, vous pouvez installer ce package :</span><span class="sxs-lookup"><span data-stu-id="4808a-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="4808a-132">[Installer hello Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="4808a-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="4808a-133">les versions actuelles Hello sont :</span><span class="sxs-lookup"><span data-stu-id="4808a-133">hello current versions are:</span></span>
* <span data-ttu-id="4808a-134">Kit de développement logiciel (SDK) Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="4808a-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="4808a-135">Runtime Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="4808a-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="4808a-136">Outils Service Fabric pour Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="4808a-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="4808a-137">Visual Studio 2017 Update 2 inclut les outils Service Fabric pour Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="4808a-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="4808a-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) inclut les outils Service Fabric pour Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="4808a-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="4808a-139">Pour obtenir la liste des versions prises en charge, consultez l’article [Service Fabric support (Options de prise en charge de Service Fabric)](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="4808a-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="4808a-140">Activer l'exécution du script PowerShell</span><span class="sxs-lookup"><span data-stu-id="4808a-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="4808a-141">Service Fabric utilise des scripts Windows PowerShell pour créer un cluster de développement local et déployer des applications à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4808a-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="4808a-142">Par défaut, Windows bloque l’exécution de ces scripts.</span><span class="sxs-lookup"><span data-stu-id="4808a-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="4808a-143">tooenable les, vous devez modifier votre stratégie d’exécution PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4808a-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="4808a-144">Ouvrez PowerShell en tant qu’administrateur, puis entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4808a-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="4808a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4808a-145">Next steps</span></span>
<span data-ttu-id="4808a-146">Maintenant que vous avez fini de configurer votre environnement de développement, commencez à créer et à exécuter des applications.</span><span class="sxs-lookup"><span data-stu-id="4808a-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="4808a-147">Créer votre première application Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4808a-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="4808a-148">Découvrez comment toodeploy et gérer des applications sur votre cluster local</span><span class="sxs-lookup"><span data-stu-id="4808a-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="4808a-149">En savoir plus sur les modèles de programmation de hello : des Services fiables et Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="4808a-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="4808a-150">Consultez les exemples de code sur GitHub hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4808a-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="4808a-151">Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="4808a-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="4808a-152">Suivez hello Service Fabric est une plateforme de toohello introduction large tooget de chemin d’accès d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="4808a-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="4808a-153">En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="4808a-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Page de campagne Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Lien WebPI VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Lien WebPI Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Lien WebPI du Kit de développement logiciel principal"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
