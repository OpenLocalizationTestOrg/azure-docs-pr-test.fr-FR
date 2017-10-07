---
title: "sécurité aaaIntegrate dans vos conceptions architecturales Azure | Documents Microsoft"
description: " Cet article va vous aider à comprendre l’architecture de services d’application et hello sur Azure toomake il plus facile sécurité toointegrate dans la conception et d’implémentation. "
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
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="e0f85-103">Architecture des applications sur Azure</span><span class="sxs-lookup"><span data-stu-id="e0f85-103">Application architecture on Azure</span></span>
<span data-ttu-id="e0f85-104">toohelp sécuriser vos solutions cloud sur Microsoft Azure, développés à architecture est critique.</span><span class="sxs-lookup"><span data-stu-id="e0f85-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="e0f85-105">Une bonne connaissance de l’architecture des services et des applications est bénéfique pour les architectes, les concepteurs et les responsables de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="e0f85-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="e0f85-106">Cette base vous aide à comprendre tous les composants hello de vos solutions de cloud et le rendre plus facile de la sécurité toointegrate à tous les aspects de votre conception et d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="e0f85-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="e0f85-107">Nous avons hello suivant toohelp vous avec votre architecture enquêtes et les conceptions :</span><span class="sxs-lookup"><span data-stu-id="e0f85-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="e0f85-108">Éléments d’infographie relatifs à l’architecture</span><span class="sxs-lookup"><span data-stu-id="e0f85-108">Architectural infographics</span></span>
* <span data-ttu-id="e0f85-109">Plans d’architecture</span><span class="sxs-lookup"><span data-stu-id="e0f85-109">Architectural blueprints</span></span>
* <span data-ttu-id="e0f85-110">Jeu de symboles Cloud et Enterprise</span><span class="sxs-lookup"><span data-stu-id="e0f85-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="e0f85-111">Modèle 3D Blueprint Visio</span><span class="sxs-lookup"><span data-stu-id="e0f85-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="e0f85-112">Éléments d’infographie relatifs à l’architecture</span><span class="sxs-lookup"><span data-stu-id="e0f85-112">Architectural infographics</span></span>
<span data-ttu-id="e0f85-113">Microsoft publie plusieurs affiches/éléments d’infographie relatifs à l’architecture.</span><span class="sxs-lookup"><span data-stu-id="e0f85-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="e0f85-114">À savoir :</span><span class="sxs-lookup"><span data-stu-id="e0f85-114">They include:</span></span>

* [<span data-ttu-id="e0f85-115">Génération d’applications Cloud réalistes</span><span class="sxs-lookup"><span data-stu-id="e0f85-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="e0f85-116">Mise à l’échelle des services Cloud</span><span class="sxs-lookup"><span data-stu-id="e0f85-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="e0f85-117">Plans d’architecture</span><span class="sxs-lookup"><span data-stu-id="e0f85-117">Architectural blueprints</span></span>
<span data-ttu-id="e0f85-118">Microsoft publie un ensemble de haut niveau [architecturaux](http://aka.ms/azblueprints) montrant comment toobuild des types spécifiques de systèmes à l’aide des produits Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0f85-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="e0f85-119">Chaque plan inclut les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e0f85-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="e0f85-120">Fichier 2D Visio 2003 plat que vous pouvez télécharger et modifier.</span><span class="sxs-lookup"><span data-stu-id="e0f85-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="e0f85-121">Perspective 3D colorés PDF fichier toointroduce hello plan accessible sans publics</span><span class="sxs-lookup"><span data-stu-id="e0f85-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="e0f85-122">Vidéo pour vous aider à la version 3D hello</span><span class="sxs-lookup"><span data-stu-id="e0f85-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="e0f85-123">Jeu de symboles Cloud et Enterprise</span><span class="sxs-lookup"><span data-stu-id="e0f85-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="e0f85-124">[Afficher hello Visio et des symboles vidéo de formation](http://aka.ms/CnESymbolsVideo) , puis [télécharger hello Cloud et le symbole de l’entreprise](http://aka.ms/CnESymbols) toohelp créer des documents techniques qui décrivent Azure, Windows Server, SQL Server et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e0f85-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="e0f85-125">Vous pouvez utiliser les symboles hello dans les diagrammes d’architecture, supports de formation, des présentations, les feuilles de données, graphisme d’information, livres blancs et même la documentation tierce si hello book trains personnes toouse les produits Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0f85-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="e0f85-126">Toutefois, ils ne sont pas destinés à être utilisés dans les interfaces utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e0f85-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="e0f85-127">Modèle 3D Blueprint Visio</span><span class="sxs-lookup"><span data-stu-id="e0f85-127">3D blueprint Visio template</span></span>
<span data-ttu-id="e0f85-128">Hello versions 3D de hello [plans d’Architecture](http://aka.ms/azblueprints) ont été initialement créé dans un outil non Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0f85-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="e0f85-129">Un nouveau modèle Visio 2013 (et versions ultérieures) a été publié le 5 août 2015 dans le cadre d’un [cours de certification d’architecture Microsoft distribué sur EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="e0f85-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="e0f85-130">Hello modèle est également disponible en dehors du cours de hello.</span><span class="sxs-lookup"><span data-stu-id="e0f85-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="e0f85-131">[Afficher la vidéo de formation hello](http://aka.ms/3dBlueprintTemplateVideo) premier afin de savoir ce qu’il peut faire</span><span class="sxs-lookup"><span data-stu-id="e0f85-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="e0f85-132">Télécharger hello [Microsoft 3d modèle Visio de plan](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="e0f85-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="e0f85-133">Télécharger hello [Cloud et les symboles de l’entreprise](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse avec un modèle 3D de hello</span><span class="sxs-lookup"><span data-stu-id="e0f85-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
