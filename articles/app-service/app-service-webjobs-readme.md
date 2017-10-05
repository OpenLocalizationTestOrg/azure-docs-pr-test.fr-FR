---
title: WebJobs dans Azure App Service
description: "Découvrez comment créer des tâches WebJobs pour exécuter des tests en arrière-plan, interagir avec des services tels que Storage et Service Bus, et créer des tâches planifiées."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="8fbaa-103">Utilisation de WebJobs dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8fbaa-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="8fbaa-104">Cet article fournit des liens vers des ressources de documentation sur l’utilisation d’Azure WebJobs et du Kit de développement logiciel (SDK) Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="8fbaa-105">Azure WebJobs permet d’exécuter facilement des scripts ou des programmes sous la forme de processus d’arrière-plan dans [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="8fbaa-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="8fbaa-106">Vous pouvez télécharger et exécuter un fichier exécutable comme cmd, bat, exe (.NET), ps1, sh, php, py, js et jar.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="8fbaa-107">Ces programmes s’exécutent en tant que tâches WebJobs selon une planification (cron) ou en continu.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="8fbaa-108">Le Kit de développement logiciel (SDK) Azure WebJobs facilite l’utilisation d’Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="8fbaa-109">Il comporte un système de liaison et de déclencheur qui fonctionne avec les objets blob Microsoft Azure Storage, les files d’attente et les tables ainsi que les files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="8fbaa-110">La création, le déploiement et la gestion des tâches web WebJobs sont parfaitement compatibles avec les outils intégrés dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="8fbaa-111">Vous pouvez créer les tâches web WebJobs à partir de modèles, les publier et les gérer (exécuter/arrêter/analyser/déboguer).</span><span class="sxs-lookup"><span data-stu-id="8fbaa-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="8fbaa-112">Le tableau de bord WebJobs dans le portail Azure fournit de puissantes fonctionnalités de gestion qui vous donnent un contrôle total sur l’exécution des tâches WebJobs, notamment la possibilité d’appeler des fonctions individuelles dans WebJobs.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="8fbaa-113">Le tableau de bord affiche également les runtimes de fonction et la sortie d'enregistrement.</span><span class="sxs-lookup"><span data-stu-id="8fbaa-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

