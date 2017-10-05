---
title: "À propos d’Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment DevTest Labs peut faciliter la création, la gestion et la surveillance des machines virtuelles Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="74916-103">À propos d’Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="74916-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="74916-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="74916-104">Overview</span></span>
<span data-ttu-id="74916-105">Les développeurs et testeurs cherchent à résoudre les problèmes de retards dans la création et la gestion de leurs environnements en accédant au cloud.</span><span class="sxs-lookup"><span data-stu-id="74916-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="74916-106">Azure résout ces problèmes et permet le libre-service dans une nouvelle structure économique.</span><span class="sxs-lookup"><span data-stu-id="74916-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="74916-107">Toutefois, les développeurs et testeurs doivent toujours consacrer beaucoup de temps à configurer leurs environnements en libre-service.</span><span class="sxs-lookup"><span data-stu-id="74916-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="74916-108">En outre, les décideurs ne savent pas précisément comment exploiter le cloud afin d’optimiser leurs économies tout en allégeant le fardeau administratif.</span><span class="sxs-lookup"><span data-stu-id="74916-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="74916-109">Azure DevTest Labs est un service permettant aux développeurs et aux testeurs de créer rapidement des environnements dans Azure tout en réduisant le temps perdu et les coûts.</span><span class="sxs-lookup"><span data-stu-id="74916-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="74916-110">Vous pouvez tester la dernière version de votre application en approvisionnant rapidement des environnements Windows et Linux à l’aide d’artefacts et de modèles réutilisables.</span><span class="sxs-lookup"><span data-stu-id="74916-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="74916-111">DevTest Labs facilite l’intégration de votre pipeline de déploiement pour approvisionner des environnements à la demande.</span><span class="sxs-lookup"><span data-stu-id="74916-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="74916-112">Faites évoluer votre test de charge de travail en approvisionnant plusieurs agents de test et créez des environnements pré-approvisionnés pour des formations et des démonstrations.</span><span class="sxs-lookup"><span data-stu-id="74916-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="74916-113">DevTest Labs offre les avantages suivants lors de la création, de la configuration et de la gestion des environnements de test et de développement dans le cloud :</span><span class="sxs-lookup"><span data-stu-id="74916-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="74916-114">Libre-service convivial</span><span class="sxs-lookup"><span data-stu-id="74916-114">Worry-free self-service</span></span>
<span data-ttu-id="74916-115">DevTest Labs facilite le contrôle des coûts en vous permettant de définir des stratégies pour votre laboratoire, comme le nombre de machines virtuelles par utilisateur et par laboratoire.</span><span class="sxs-lookup"><span data-stu-id="74916-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="74916-116">DevTest Labs vous permet également de créer des stratégies pour arrêter et démarrer automatiquement vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="74916-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="74916-117">Vos applications sont prêtes pour le test en un clin d’œil</span><span class="sxs-lookup"><span data-stu-id="74916-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="74916-118">DevTest Labs vous permet de créer des environnements pré-approvisionnés avec tous les éléments dont votre équipe a besoin pour commencer à développer et à tester des applications.</span><span class="sxs-lookup"><span data-stu-id="74916-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="74916-119">Il vous suffit de revendiquer les environnements où la dernière version fonctionnelle de votre application est installée et de commencer à travailler directement.</span><span class="sxs-lookup"><span data-stu-id="74916-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="74916-120">Vous pouvez également utiliser des conteneurs pour créer plus rapidement et facilement des environnements.</span><span class="sxs-lookup"><span data-stu-id="74916-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="74916-121">Créez, réutilisez</span><span class="sxs-lookup"><span data-stu-id="74916-121">Create once, use everywhere</span></span>
<span data-ttu-id="74916-122">Capturez et partagez les artefacts et modèles d’environnement au sein de votre équipe ou organisation, tout cela dans le contrôle du code source, pour créer facilement des environnements de développement et de test.</span><span class="sxs-lookup"><span data-stu-id="74916-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="74916-123">Intégré à votre chaîne d’outils existante</span><span class="sxs-lookup"><span data-stu-id="74916-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="74916-124">Tirez parti des plug-ins prêts à l’emploi ou de notre API pour approvisionner des environnement de développement/test directement à partir de votre outil d’intégration continue préféré, d’un environnement de développement intégré ou d’un pipeline de mise en production automatisé.</span><span class="sxs-lookup"><span data-stu-id="74916-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="74916-125">Vous pouvez également utiliser notre outil en ligne de commande complet.</span><span class="sxs-lookup"><span data-stu-id="74916-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="74916-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74916-126">Next steps</span></span>
[<span data-ttu-id="74916-127">Concepts de DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="74916-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

