---
title: aaaWebJobs dans Azure App Service
description: "Découvrez comment toobuild WebJobs toorun arrière-plan teste, interagir avec les services de stockage et de Service Bus et créer des tâches planifiées."
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
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="e0852-103">Utilisation de WebJobs dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e0852-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="e0852-104">Cet article lie toodocumentation des ressources concernant la manière toouse tâches Web Azure et hello du Kit de développement logiciel Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="e0852-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="e0852-105">Les tâches Web Azure fournissent un script de toorun facilement ou programmes en tant que processus d’arrière-plan sur [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e0852-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="e0852-106">Vous pouvez télécharger et exécuter un fichier exécutable comme cmd, bat, exe (.NET), ps1, sh, php, py, js et jar.</span><span class="sxs-lookup"><span data-stu-id="e0852-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="e0852-107">Ces programmes s’exécutent en tant que tâches WebJobs selon une planification (cron) ou en continu.</span><span class="sxs-lookup"><span data-stu-id="e0852-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="e0852-108">Hello WebJobs SDK rend plus facile toouse le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0852-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="e0852-109">Hello WebJobs SDK a une liaison et un système de déclencheur qui fonctionne avec Microsoft Azure Storage BLOB, files d’attente et Tables ainsi que les files d’attente de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e0852-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="e0852-110">La création, le déploiement et la gestion des tâches web WebJobs sont parfaitement compatibles avec les outils intégrés dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0852-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="e0852-111">Vous pouvez créer les tâches web WebJobs à partir de modèles, les publier et les gérer (exécuter/arrêter/analyser/déboguer).</span><span class="sxs-lookup"><span data-stu-id="e0852-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="e0852-112">tableau de bord WebJobs Hello Bonjour portail Azure fournit de puissantes fonctions de gestion qui vous donnent un contrôle total sur l’exécution de hello de tâches Web, y compris hello capacité tooinvoke des fonctions individuelles dans les tâches Web.</span><span class="sxs-lookup"><span data-stu-id="e0852-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="e0852-113">tableau de bord Hello affiche également les exécutions de la fonction et la sortie de journalisation.</span><span class="sxs-lookup"><span data-stu-id="e0852-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

