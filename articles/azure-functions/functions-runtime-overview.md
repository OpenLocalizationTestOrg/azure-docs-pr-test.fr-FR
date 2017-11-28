---
title: "Vue d’ensemble du runtime d’Azure Functions | Microsoft Docs"
description: "Vue d’ensemble du runtime d’Azure Functions en version préliminaire"
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
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="5b015-103">Vue d’ensemble du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5b015-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="5b015-104">Le runtime d’Azure Functions vous fournit une nouvelle façon de tirer parti de la simplicité et de la flexibilité du modèle de programmation Azure Functions sur site.</span><span class="sxs-lookup"><span data-stu-id="5b015-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="5b015-105">Basé sur les mêmes racines open source qu’Azure Functions, le runtime d’Azure Functions est déployé sur site pour fournir une expérience de développement quasiment identique à celle du service cloud.</span><span class="sxs-lookup"><span data-stu-id="5b015-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Portail du runtime d’Azure Functions en version préliminaire][1]

<span data-ttu-id="5b015-107">Le runtime d’Azure Functions vous permet de découvrir Azure Functions avant même d’adopter le cloud.</span><span class="sxs-lookup"><span data-stu-id="5b015-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="5b015-108">De cette façon, les ressources de code que vous créez peuvent ensuite être dirigées sur le cloud lors de la migration.</span><span class="sxs-lookup"><span data-stu-id="5b015-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="5b015-109">Le runtime vous donne également accès à de nouvelles options, comme l’utilisation de la puissance de calcul de secours de vos ordinateurs locaux pour exécuter des traitements par lots pendant la nuit.</span><span class="sxs-lookup"><span data-stu-id="5b015-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="5b015-110">Vous pouvez également utiliser des appareils au sein de votre organisation pour envoyer de manière conditionnelle des données à d’autres systèmes, sur site et sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="5b015-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="5b015-111">Le runtime d’Azure Functions se compose de deux éléments :</span><span class="sxs-lookup"><span data-stu-id="5b015-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="5b015-112">Rôle de gestion du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5b015-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="5b015-113">Rôle de travail du runtime d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5b015-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="5b015-114">Rôle de gestion d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5b015-114">Azure Functions Management Role</span></span>

<span data-ttu-id="5b015-115">Le rôle de gestion d’Azure Functions fournit un hôte pour la gestion de vos fonctions sur site.</span><span class="sxs-lookup"><span data-stu-id="5b015-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="5b015-116">Ce rôle effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b015-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="5b015-117">Hébergement du portail de gestion d’Azure Functions, qui est identique à celui que vous voyez dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5b015-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5b015-118">Il vous permet de développer vos fonctions de la même manière que vous le feriez dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b015-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="5b015-119">Répartition des fonctions entre plusieurs Workers Functions.</span><span class="sxs-lookup"><span data-stu-id="5b015-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="5b015-120">Mise à disposition d’un point de terminaison de publication pour vous permettre de publier vos fonctions directement à partir de Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5b015-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="5b015-121">Rôle de travail d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5b015-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="5b015-122">Les rôles de travail d’Azure Functions sont déployés dans des conteneurs Windows et c’est là que le code de votre fonction s’exécute.</span><span class="sxs-lookup"><span data-stu-id="5b015-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="5b015-123">Vous pouvez déployer plusieurs rôles de travail au sein de votre organisation. Il s’agit là d’une solution clé grâce à laquelle les clients peuvent utiliser la puissance de calcul de secours.</span><span class="sxs-lookup"><span data-stu-id="5b015-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="5b015-124">Configuration minimale requise</span><span class="sxs-lookup"><span data-stu-id="5b015-124">Minimum Requirements</span></span>

<span data-ttu-id="5b015-125">Pour bien démarrer avec le runtime d’Azure Functions, vous devez disposer d’un ordinateur **Windows Server 2016 ou Windows 10 Creators Update** avec accès à une instance **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="5b015-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b015-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b015-126">Next Steps</span></span>

<span data-ttu-id="5b015-127">Installer la [version préliminaire du runtime d’Azure Functions](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="5b015-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
