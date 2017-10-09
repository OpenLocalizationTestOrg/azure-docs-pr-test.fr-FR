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
# <a name="prepare-your-development-environment"></a>Préparer votre environnement de développement
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild et exécutez [les applications Azure Service Fabric] [ 1] sur votre ordinateur de développement, installez hello runtime, Kit de développement logiciel et les outils. Vous devez également l’exécution de tooenable des scripts Windows PowerShell de hello inclus dans le Kit de développement logiciel de hello.

## <a name="prerequisites"></a>Composants requis
### <a name="supported-operating-system-versions"></a>Versions du système d’exploitation prises en charge
Hello versions de système d’exploitation suivantes est prises en charge pour le développement :

* Windows 7
* Windows 8 et Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 inclut uniquement Windows PowerShell 2.0 par défaut. Les applets de commande PowerShell de Service Fabric nécessitent PowerShell 3.0 ou version ultérieure. Vous pouvez [télécharger Windows PowerShell 5.0] [ powershell5-download] de hello Microsoft Download Center.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Installer les outils et Kit de développement logiciel de hello
### <a name="toouse-visual-studio-2017"></a>toouse Visual Studio 2017
Outils de l’infrastructure de service font partie de hello développement Azure et gestion de la charge de travail dans Visual Studio 2017. Activez cette charge de travail dans le cadre de votre installation de Visual Studio.
En outre, vous devez tooinstall hello Microsoft Azure Service Fabric SDK, à l’aide de Web Platform Installer.

* [Installer hello Microsoft Azure Service Fabric SDK][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (requiert Visual Studio 2015 Update 2 ou version ultérieure)
Pour Visual Studio 2015, les outils de l’infrastructure de Service sont installés avec hello SDK, à l’aide de hello Web Platform Installer :

* [Installer les outils et hello Microsoft Azure Service Fabric SDK][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Installation du Kit de développement logiciel (SDK) uniquement
Si vous devez uniquement hello SDK, vous pouvez installer ce package :
* [Installer hello Microsoft Azure Service Fabric SDK][core-sdk]

les versions actuelles Hello sont :
* Kit de développement logiciel (SDK) Service Fabric 2.7.198
* Runtime Service Fabric 5.7.198
* Outils Service Fabric pour Visual Studio 2015 1.7.50721
* Visual Studio 2017 Update 2 inclut les outils Service Fabric pour Visual Studio 1.6.20170504
* Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) inclut les outils Service Fabric pour Visual Studio 1.7.20170721

Pour obtenir la liste des versions prises en charge, consultez l’article [Service Fabric support (Options de prise en charge de Service Fabric)](service-fabric-support.md).

## <a name="enable-powershell-script-execution"></a>Activer l'exécution du script PowerShell
Service Fabric utilise des scripts Windows PowerShell pour créer un cluster de développement local et déployer des applications à partir de Visual Studio. Par défaut, Windows bloque l’exécution de ces scripts. tooenable les, vous devez modifier votre stratégie d’exécution PowerShell. Ouvrez PowerShell en tant qu’administrateur, puis entrez hello de commande suivante :

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez fini de configurer votre environnement de développement, commencez à créer et à exécuter des applications.

* [Créer votre première application Service Fabric dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Découvrez comment toodeploy et gérer des applications sur votre cluster local](service-fabric-get-started-with-a-local-cluster.md)
* [En savoir plus sur les modèles de programmation de hello : des Services fiables et Reliable Actors](service-fabric-choose-framework.md)
* [Consultez les exemples de code sur GitHub hello Service Fabric](https://aka.ms/servicefabricsamples)
* [Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Suivez hello Service Fabric est une plateforme de toohello introduction large tooget de chemin d’accès d’apprentissage](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Page de campagne Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Lien WebPI VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Lien WebPI Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Lien WebPI du Kit de développement logiciel principal"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
