---
title: build aaaCommand en ligne pour Azure | Documents Microsoft
description: "Génération en ligne de commande pour Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a><span data-ttu-id="e9999-103">Génération de projets Azure à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="e9999-103">Building Azure projects from hello command line</span></span>
<span data-ttu-id="e9999-104">À l’aide de hello Microsoft Build Engine (MSBuild), vous pouvez générer des produits dans des environnements de laboratoire de génération où Visual Studio n’est pas installé.</span><span class="sxs-lookup"><span data-stu-id="e9999-104">Using hello Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span></span> <span data-ttu-id="e9999-105">MSBuild utilise pour les fichiers projet un format XML extensible et entièrement pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e9999-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span></span> <span data-ttu-id="e9999-106">À l’aide du format de fichier hello MSBuild, vous pouvez décrire les éléments doivent être générées pour un ou plusieurs plateformes et configurations.</span><span class="sxs-lookup"><span data-stu-id="e9999-106">Using hello MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span></span>

<span data-ttu-id="e9999-107">Vous pouvez également exécuter MSBuild à la ligne de commande hello et cette rubrique décrit cette approche.</span><span class="sxs-lookup"><span data-stu-id="e9999-107">You can also run MSBuild at hello command line, and this topic describes that approach.</span></span> <span data-ttu-id="e9999-108">En définissant des propriétés sur la ligne de commande hello, vous pouvez créer des configurations spécifiques d’un projet.</span><span class="sxs-lookup"><span data-stu-id="e9999-108">By setting properties on hello command line, you can build specific configurations of a project.</span></span> <span data-ttu-id="e9999-109">De même, vous pouvez également définir des cibles de hello MSBuild génère.</span><span class="sxs-lookup"><span data-stu-id="e9999-109">Similarly, you can also define hello targets that MSBuild builds.</span></span> <span data-ttu-id="e9999-110">Pour plus d’informations sur les paramètres de ligne de commande et MSBuild, consultez la page [Référence de la ligne de commande MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9999-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

## <a name="msbuild-parameters"></a><span data-ttu-id="e9999-111">Paramètres MSBuild</span><span class="sxs-lookup"><span data-stu-id="e9999-111">MSBuild parameters</span></span>
<span data-ttu-id="e9999-112">toocreate de façon la plus simple Hello un package est toorun MSBuild avec hello `/t:Publish` option.</span><span class="sxs-lookup"><span data-stu-id="e9999-112">hello simplest way toocreate a package is toorun MSBuild with hello `/t:Publish` option.</span></span> <span data-ttu-id="e9999-113">Par défaut, cette commande crée un répertoire dans la relation toohello racine dossier hello projet, tel que `<ProjectDirectory>\bin\Configuration\app.publish\`.</span><span class="sxs-lookup"><span data-stu-id="e9999-113">By default, this command creates a directory in relation toohello root folder for hello project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span></span> <span data-ttu-id="e9999-114">Lorsque vous générez un projet Windows Azure, deux fichiers sont générés : hello du fichier de package lui-même et le fichier de configuration associé hello :</span><span class="sxs-lookup"><span data-stu-id="e9999-114">When you build an Azure project, two files are generated: hello package file itself and hello accompanying configuration file:</span></span>

* <span data-ttu-id="e9999-115">Fichier de package (`project.cspkg`)</span><span class="sxs-lookup"><span data-stu-id="e9999-115">Package File (`project.cspkg`)</span></span>
* <span data-ttu-id="e9999-116">Fichier de configuration (`ServiceConfiguration.TargetProfile.cscfg`)</span><span class="sxs-lookup"><span data-stu-id="e9999-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span></span>

<span data-ttu-id="e9999-117">Par défaut, tous les projets Azure comprennent un fichier de configuration de service pour les versions locales (débogage) et un autre pour les versions cloud (gestion intermédiaire ou production).</span><span class="sxs-lookup"><span data-stu-id="e9999-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span></span> <span data-ttu-id="e9999-118">Mais vous pouvez ajouter ou supprimer des fichiers de configuration de service selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e9999-118">However, you can add or remove service-configuration files as needed.</span></span> <span data-ttu-id="e9999-119">Lorsque vous créez un package dans Visual Studio, vous êtes invité le tooinclude du fichier de configuration de service en même temps que le package de hello.</span><span class="sxs-lookup"><span data-stu-id="e9999-119">When you build a package within Visual Studio, you are asked which service-configuration file tooinclude alongside hello package.</span></span> <span data-ttu-id="e9999-120">Lorsque vous générez un package à l’aide de MSBuild, le fichier de configuration du service local hello est inclus par défaut.</span><span class="sxs-lookup"><span data-stu-id="e9999-120">When you build a package by using MSBuild, hello local service-configuration file is included by default.</span></span> <span data-ttu-id="e9999-121">fichier tooinclude une configuration de service différents, jeu hello `TargetProfile` propriété Hello commande MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span><span class="sxs-lookup"><span data-stu-id="e9999-121">tooinclude a different service-configuration file, set hello `TargetProfile` property of hello MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span></span>

<span data-ttu-id="e9999-122">Si vous souhaitez toouse un autre répertoire pour hello stocké des fichiers de configuration et de package, définir le chemin à l’aide de hello hello `/p:PublishDir=Directory\` option, y compris hello séparateur de barre oblique inverse de fin.</span><span class="sxs-lookup"><span data-stu-id="e9999-122">If you want toouse an alternate directory for hello stored package and configuration files, set hello path by using hello `/p:PublishDir=Directory\` option, including hello trailing backslash separator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9999-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9999-123">Next steps</span></span>
<span data-ttu-id="e9999-124">Une fois le package de hello est créé, vous pouvez le déployer tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e9999-124">After hello package is built, you can deploy it tooAzure.</span></span> <span data-ttu-id="e9999-125">Pour obtenir un didacticiel qui montre comment tooautomate ce processus, consultez [livraison continue pour les Services de Cloud dans Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="e9999-125">For a tutorial that demonstrates how tooautomate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span></span>
