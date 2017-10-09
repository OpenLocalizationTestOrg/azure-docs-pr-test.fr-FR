---
title: "aaaAzure vue d’ensemble de fonctions Runtime | Documents Microsoft"
description: "Vue d’ensemble de hello Azure en version préliminaire fonctions Runtime"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="f11d9-103">Vue d’ensemble du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f11d9-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="f11d9-104">Bonjour Azure fonctions Runtime fournit un moyen de nouveau pour vous tootake parti de hello simplicité et souplesse de fonctions d’Azure hello local de modèle de programmation.</span><span class="sxs-lookup"><span data-stu-id="f11d9-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="f11d9-105">Reposant sur hello même ouvrir des racines de la source comme fonctions d’Azure, Azure fonctions Runtime est tooprovide déployés localement un développement quasiment identique expérience en tant que service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="f11d9-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Portail du runtime d’Azure Functions en version préliminaire][1]

<span data-ttu-id="f11d9-107">Bonjour Azure fonctions Runtime fournit un moyen pour vous tooexperience Azure fonctions avant de les valider toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="f11d9-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="f11d9-108">De cette façon, les ressources de code hello que vous créez peuvent être utilisées avec le cloud de toohello vous lorsque vous migrez.</span><span class="sxs-lookup"><span data-stu-id="f11d9-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="f11d9-109">Hello runtime ouvre également de nouvelles options, telles que l’utilisation de puissance de calcul de rechange hello de vos processus de lot local ordinateurs toorun pendant la nuit.</span><span class="sxs-lookup"><span data-stu-id="f11d9-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="f11d9-110">Vous pouvez également utiliser des périphériques au sein de votre organisation tooconditionally envoi données tooother les systèmes, à la fois localement et dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f11d9-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="f11d9-111">Bonjour Azure fonctions Runtime comprend deux parties :</span><span class="sxs-lookup"><span data-stu-id="f11d9-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="f11d9-112">Rôle de gestion du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f11d9-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="f11d9-113">Rôle de travail du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f11d9-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="f11d9-114">Rôle de gestion d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f11d9-114">Azure Functions Management Role</span></span>

<span data-ttu-id="f11d9-115">Hello rôle de fonctions de gestion Azure fournit un hôte pour la gestion de vos fonctions localement hello.</span><span class="sxs-lookup"><span data-stu-id="f11d9-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="f11d9-116">Ce rôle effectue hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="f11d9-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="f11d9-117">Hébergement de hello fonctions portail de gestion, qui est hello hello identique à celle présentée dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f11d9-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f11d9-118">Ce vous permet de développer de vos fonctions dans hello même façon que vous le feriez dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f11d9-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="f11d9-119">Répartition des fonctions entre plusieurs Workers Functions.</span><span class="sxs-lookup"><span data-stu-id="f11d9-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="f11d9-120">Mise à disposition d’un point de terminaison de publication pour vous permettre de publier vos fonctions directement à partir de Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f11d9-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="f11d9-121">Rôle de travail d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f11d9-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="f11d9-122">Rôles de travail de fonctions Azure Hello sont déployés dans les conteneurs Windows et Voici où s’exécute votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="f11d9-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="f11d9-123">Vous pouvez déployer plusieurs rôles de travail au sein de votre organisation. Il s’agit là d’une solution clé grâce à laquelle les clients peuvent utiliser la puissance de calcul de secours.</span><span class="sxs-lookup"><span data-stu-id="f11d9-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="f11d9-124">Configuration minimale requise</span><span class="sxs-lookup"><span data-stu-id="f11d9-124">Minimum Requirements</span></span>

<span data-ttu-id="f11d9-125">tooget main hello Azure fonctions Runtime, vous devez disposer d’un ordinateur avec **Windows Server 2016 ou mise à jour de Windows 10 créateurs** avec accès tooa **SQL Server** instance.</span><span class="sxs-lookup"><span data-stu-id="f11d9-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f11d9-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f11d9-126">Next Steps</span></span>

<span data-ttu-id="f11d9-127">Installer hello [aperçu de l’exécution de fonctions Azure](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="f11d9-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
