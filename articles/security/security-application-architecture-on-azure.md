---
title: "Intégrer la sécurité dans vos conceptions architecturales Azure | Microsoft Docs"
description: " Cet article vous aidera à comprendre l’architecture des services et des applications sur Azure, afin de faciliter l’intégration de la sécurité dans la conception et l’implémentation. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 91e46d690d3e7c298bc3b4020cc383ca99c43c4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="30ab3-103">Architecture des applications sur Azure</span><span class="sxs-lookup"><span data-stu-id="30ab3-103">Application architecture on Azure</span></span>
<span data-ttu-id="30ab3-104">Pour sécuriser vos solutions cloud sur Microsoft Azure, vous devez disposer d’une base architecturale solide.</span><span class="sxs-lookup"><span data-stu-id="30ab3-104">To help secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="30ab3-105">Une bonne connaissance de l’architecture des services et des applications est bénéfique pour les architectes, les concepteurs et les responsables de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="30ab3-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="30ab3-106">Ces connaissances fondamentales vous aident à comprendre tous les composants de vos solutions cloud, et facilitent l’intégration de la sécurité dans tous les aspects de votre conception et de votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="30ab3-106">This foundational knowledge helps you understand all the components of your cloud-based solutions and make it easier to integrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="30ab3-107">Les éléments suivants sont conçus pour vous aider dans vos recherches et conceptions architecturales :</span><span class="sxs-lookup"><span data-stu-id="30ab3-107">We have the following to help you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="30ab3-108">Éléments d’infographie relatifs à l’architecture</span><span class="sxs-lookup"><span data-stu-id="30ab3-108">Architectural infographics</span></span>
* <span data-ttu-id="30ab3-109">Plans d’architecture</span><span class="sxs-lookup"><span data-stu-id="30ab3-109">Architectural blueprints</span></span>
* <span data-ttu-id="30ab3-110">Jeu de symboles Cloud et Enterprise</span><span class="sxs-lookup"><span data-stu-id="30ab3-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="30ab3-111">Modèle 3D Blueprint Visio</span><span class="sxs-lookup"><span data-stu-id="30ab3-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="30ab3-112">Éléments d’infographie relatifs à l’architecture</span><span class="sxs-lookup"><span data-stu-id="30ab3-112">Architectural infographics</span></span>
<span data-ttu-id="30ab3-113">Microsoft publie plusieurs affiches/éléments d’infographie relatifs à l’architecture.</span><span class="sxs-lookup"><span data-stu-id="30ab3-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="30ab3-114">À savoir :</span><span class="sxs-lookup"><span data-stu-id="30ab3-114">They include:</span></span>

* [<span data-ttu-id="30ab3-115">Génération d’applications Cloud réalistes</span><span class="sxs-lookup"><span data-stu-id="30ab3-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="30ab3-116">Mise à l’échelle des services Cloud</span><span class="sxs-lookup"><span data-stu-id="30ab3-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="30ab3-117">Plans d’architecture</span><span class="sxs-lookup"><span data-stu-id="30ab3-117">Architectural blueprints</span></span>
<span data-ttu-id="30ab3-118">Microsoft publie un ensemble de [plans d’architecture](http://aka.ms/azblueprints) de haut niveau qui montrent comment créer des types spécifiques de systèmes à l’aide des produits Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30ab3-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how to build specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="30ab3-119">Chaque plan inclut les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="30ab3-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="30ab3-120">Fichier 2D Visio 2003 plat que vous pouvez télécharger et modifier.</span><span class="sxs-lookup"><span data-stu-id="30ab3-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="30ab3-121">Fichier PDF de perspective 3D en couleur pour présenter le plan à un public moins technique.</span><span class="sxs-lookup"><span data-stu-id="30ab3-121">Colorful 3D perspective PDF file to introduce the blueprint to less technical audiences</span></span>
* <span data-ttu-id="30ab3-122">Vidéo qui vous guide dans la version 3D</span><span class="sxs-lookup"><span data-stu-id="30ab3-122">Video that walks through the 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="30ab3-123">Jeu de symboles Cloud et Enterprise</span><span class="sxs-lookup"><span data-stu-id="30ab3-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="30ab3-124">[Visionnez la vidéo de formation sur Visio et les symboles](http://aka.ms/CnESymbolsVideo), puis [téléchargez le jeu de symboles Cloud et Enterprise](http://aka.ms/CnESymbols) pour créer des documents techniques qui décrivent Azure, Windows Server, SQL Server, etc.</span><span class="sxs-lookup"><span data-stu-id="30ab3-124">[View the Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download the Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) to help create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="30ab3-125">Vous pouvez utiliser les symboles dans les diagrammes d’architecture, les supports de formation, les présentations, les fiches techniques, les infographies, les livres blancs et même les ouvrages tiers si le livre est destiné à former des personnes à l’utilisation des produits Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30ab3-125">You can use the symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if the book trains people to use Microsoft products.</span></span> <span data-ttu-id="30ab3-126">Toutefois, ils ne sont pas destinés à être utilisés dans les interfaces utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30ab3-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="30ab3-127">Modèle 3D Blueprint Visio</span><span class="sxs-lookup"><span data-stu-id="30ab3-127">3D blueprint Visio template</span></span>
<span data-ttu-id="30ab3-128">Les versions 3D des [plans d'architecture Microsoft](http://aka.ms/azblueprints) ont initialement été créées avec un outil autre que Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30ab3-128">The 3D versions of the [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="30ab3-129">Un nouveau modèle Visio 2013 (et versions ultérieures) a été publié le 5 août 2015 dans le cadre d’un [cours de certification d’architecture Microsoft distribué sur EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="30ab3-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="30ab3-130">Le modèle est également disponible en dehors du cours.</span><span class="sxs-lookup"><span data-stu-id="30ab3-130">The template is also available outside the course.</span></span>

* <span data-ttu-id="30ab3-131">[visionner la vidéo de formation](http://aka.ms/3dBlueprintTemplateVideo) afin de savoir ce qu'il peut faire.</span><span class="sxs-lookup"><span data-stu-id="30ab3-131">[View the training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="30ab3-132">Téléchargez le [modèle Microsoft 3D Blueprint Visio](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="30ab3-132">Download the [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="30ab3-133">Téléchargez les [symboles Cloud et Enterprise](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) à utiliser avec le modèle 3D.</span><span class="sxs-lookup"><span data-stu-id="30ab3-133">Download the [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) to use with the 3D template</span></span>
