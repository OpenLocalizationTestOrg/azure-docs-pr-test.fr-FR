---
title: "aaaMicrosoft outil de modélisation des menaces - Azure | Documents Microsoft"
description: "page principale pour hello Microsoft Threat outil modélisation, contenant des informations sur la mise en route avec l’outil hello, y compris les processus de modélisation des menaces hello"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="938f5-103">Outil Microsoft de modélisation des menaces</span><span class="sxs-lookup"><span data-stu-id="938f5-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="938f5-104">Hello, outil de modélisation des menaces est un élément essentiel du hello du cycle de vie de développement de sécurité Microsoft (SDL).</span><span class="sxs-lookup"><span data-stu-id="938f5-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="938f5-105">Il permet aux logiciels architectes tooidentify et d’atténuer les problèmes de sécurité potentiels au plus tôt, lorsqu’ils sont relativement facile et plus économique tooresolve.</span><span class="sxs-lookup"><span data-stu-id="938f5-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="938f5-106">Par conséquent, il réduit considérablement les coût total de hello du développement.</span><span class="sxs-lookup"><span data-stu-id="938f5-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="938f5-107">En outre, nous avons conçu outil de hello avec des experts de sécurité à l’esprit, facilitant la modélisation des menaces pour tous les développeurs en fournissant des indications précises sur la création et l’analyse des modèles de menace.</span><span class="sxs-lookup"><span data-stu-id="938f5-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="938f5-108">outil de Hello permet à tout utilisateur :</span><span class="sxs-lookup"><span data-stu-id="938f5-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="938f5-109">Communiquer sur la conception de la sécurité de leurs systèmes hello</span><span class="sxs-lookup"><span data-stu-id="938f5-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="938f5-110">Analyser ces conceptions afin de détecter d’éventuels problèmes de sécurité par le biais d’une méthodologie éprouvée</span><span class="sxs-lookup"><span data-stu-id="938f5-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="938f5-111">Proposer et gérer des mesures de correction pour les problèmes de sécurité</span><span class="sxs-lookup"><span data-stu-id="938f5-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="938f5-112">Voici quelques outils fonctionnalités et innovations, tooname simplement quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="938f5-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="938f5-113">**Automatisation :** conseils et commentaires sur le dessin d’un modèle</span><span class="sxs-lookup"><span data-stu-id="938f5-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="938f5-114">**STRIDE per Element :** analyse guidée des menaces et des mesures de correction</span><span class="sxs-lookup"><span data-stu-id="938f5-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="938f5-115">**Création de rapports :** activités de sécurité et de test dans la phase de vérification hello</span><span class="sxs-lookup"><span data-stu-id="938f5-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="938f5-116">**Méthodologie unique :** toobetter d’utilisateurs permet de visualiser et comprendre les menaces</span><span class="sxs-lookup"><span data-stu-id="938f5-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="938f5-117">**Conçu pour les développeurs et centré sur le logiciel :** de nombreuses approches sont centrées sur les ressources ou les personnes malveillantes.</span><span class="sxs-lookup"><span data-stu-id="938f5-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="938f5-118">Nous sommes centrés sur le logiciel.</span><span class="sxs-lookup"><span data-stu-id="938f5-118">We are centered on software.</span></span> <span data-ttu-id="938f5-119">Nous nous appuyons sur les activités que connaissent tous les architectes et développeurs de logiciels, par exemple le dessin d’images pour l’architecture logicielle</span><span class="sxs-lookup"><span data-stu-id="938f5-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="938f5-120">**Le focus sur l’analyse de la conception :** hello terme « modélisation des menaces » peut faire référence tooeither de spécifications ou une technique d’analyse de conception.</span><span class="sxs-lookup"><span data-stu-id="938f5-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="938f5-121">Parfois, il fait référence tooa de mélange complexe de hello deux.</span><span class="sxs-lookup"><span data-stu-id="938f5-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="938f5-122">modélisation de toothreat approche Hello SDL Microsoft est une technique d’analyse de conception ayant le focus</span><span class="sxs-lookup"><span data-stu-id="938f5-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="938f5-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="938f5-123">Next steps</span></span>

<span data-ttu-id="938f5-124">tableau Hello ci-dessous contient tooget les liens importants ; vous avez commencé avec hello outil de modélisation des menaces :</span><span class="sxs-lookup"><span data-stu-id="938f5-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="938f5-125">Étape</span><span class="sxs-lookup"><span data-stu-id="938f5-125">Step</span></span>  | <span data-ttu-id="938f5-126">Description</span><span class="sxs-lookup"><span data-stu-id="938f5-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="938f5-127">**1**</span><span class="sxs-lookup"><span data-stu-id="938f5-127">**1**</span></span> | [<span data-ttu-id="938f5-128">Télécharger hello outil de modélisation des menaces</span><span class="sxs-lookup"><span data-stu-id="938f5-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="938f5-129">**2**</span><span class="sxs-lookup"><span data-stu-id="938f5-129">**2**</span></span> | [<span data-ttu-id="938f5-130">Lire notre guide pour bien démarrer</span><span class="sxs-lookup"><span data-stu-id="938f5-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="938f5-131">**3**</span><span class="sxs-lookup"><span data-stu-id="938f5-131">**3**</span></span> | [<span data-ttu-id="938f5-132">Se familiariser avec les fonctionnalités de hello</span><span class="sxs-lookup"><span data-stu-id="938f5-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="938f5-133">**4**</span><span class="sxs-lookup"><span data-stu-id="938f5-133">**4**</span></span> | [<span data-ttu-id="938f5-134">En savoir plus sur les catégories de menaces générées</span><span class="sxs-lookup"><span data-stu-id="938f5-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="938f5-135">**5**</span><span class="sxs-lookup"><span data-stu-id="938f5-135">**5**</span></span> | [<span data-ttu-id="938f5-136">Rechercher des solutions d’atténuation toogenerated menaces</span><span class="sxs-lookup"><span data-stu-id="938f5-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="938f5-137">Ressources</span><span class="sxs-lookup"><span data-stu-id="938f5-137">Resources</span></span>

<span data-ttu-id="938f5-138">Voici quelques anciens articles toothreat toujours applicables modélisation aujourd'hui :</span><span class="sxs-lookup"><span data-stu-id="938f5-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="938f5-139">L’article sur l’Importance de la modélisation des menaces de hello</span><span class="sxs-lookup"><span data-stu-id="938f5-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="938f5-140">Formation publiée par Trustworthy Computing</span><span class="sxs-lookup"><span data-stu-id="938f5-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="938f5-141">Découvrez le travail de quelques experts de l’outil de modélisation des menaces :</span><span class="sxs-lookup"><span data-stu-id="938f5-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="938f5-142">Threats Manager (Gestionnaire de menaces)</span><span class="sxs-lookup"><span data-stu-id="938f5-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="938f5-143">Blog sur la sécurité de Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="938f5-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)