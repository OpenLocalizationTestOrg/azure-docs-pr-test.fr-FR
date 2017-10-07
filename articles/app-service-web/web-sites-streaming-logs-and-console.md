---
title: les journaux aaaStreaming et console
description: Vue d'ensemble des journaux et de la console de diffusion en continu
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="2ef29-103">Journaux de diffusion en continu et hello Console</span><span class="sxs-lookup"><span data-stu-id="2ef29-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="2ef29-104">Journaux en continu</span><span class="sxs-lookup"><span data-stu-id="2ef29-104">Streaming Logs</span></span>
<span data-ttu-id="2ef29-105">Hello **portail Azure** fournit une visionneuse du journal en continu intégrée qui vous permet d’afficher les événements de suivi à partir de votre **du Service d’applications** applications en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2ef29-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="2ef29-106">La configuration de cette fonction se fait en quelques étapes simples :</span><span class="sxs-lookup"><span data-stu-id="2ef29-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="2ef29-107">Écriture des suivis dans votre code</span><span class="sxs-lookup"><span data-stu-id="2ef29-107">Write traces in your code</span></span>
* <span data-ttu-id="2ef29-108">Activation des **journaux de diagnostic** pour votre application</span><span class="sxs-lookup"><span data-stu-id="2ef29-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="2ef29-109">Flux de hello vue à partir d’intégrées de hello **journaux de diffusion en continu** UI Bonjour **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ef29-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="2ef29-110">Comment toowrite effectue le suivi dans votre code</span><span class="sxs-lookup"><span data-stu-id="2ef29-110">How toowrite traces in your code</span></span>
<span data-ttu-id="2ef29-111">L'écriture des suivis dans votre code est simple.</span><span class="sxs-lookup"><span data-stu-id="2ef29-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="2ef29-112">En c#, il est aussi simple que l’écriture hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="2ef29-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="2ef29-113">Hello classe Trace réside dans l’espace de noms System.Diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="2ef29-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="2ef29-114">Dans une application node.js, vous pouvez écrire ce code tooachieve hello même résultat :</span><span class="sxs-lookup"><span data-stu-id="2ef29-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="2ef29-115">Comment tooenable et vue hello des journaux de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="2ef29-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="2ef29-116">![][BrowseSitesScreenshot] Les diagnostics sont activés par application.</span><span class="sxs-lookup"><span data-stu-id="2ef29-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="2ef29-117">Commencez par parcourir le site de toohello que vous aimeriez tooenable cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2ef29-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="2ef29-118">![][DiagnosticsLogs]À partir du menu Paramètres, faites défiler la liste toohello **analyse** section, puis cliquez sur **(1) des journaux de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="2ef29-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="2ef29-119">Puis **(2) activer** **journalisation des applications (système de fichiers)** ou **journalisation des applications (blob)** hello **niveau** option vous permet de modifier hello niveau de gravité de traces toocapture.</span><span class="sxs-lookup"><span data-stu-id="2ef29-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="2ef29-120">Si vous essayez simplement tooget familiarisé avec la fonctionnalité de hello, définissez le niveau de hello trop**Verbose** tooensure toutes vos instructions de trace sont collectées.</span><span class="sxs-lookup"><span data-stu-id="2ef29-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="2ef29-121">Cliquez sur **enregistrer** haut hello Panneau de hello et que vous êtes prêt tooview journaux.</span><span class="sxs-lookup"><span data-stu-id="2ef29-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="2ef29-122">Bonjour supérieur Bonjour **au niveau de gravité** hello davantage de ressources sont consommé toolog et hello plus traces produites.</span><span class="sxs-lookup"><span data-stu-id="2ef29-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="2ef29-123">Assurez-vous que **au niveau de gravité** est toohello configuré un niveau de détail approprié pour une production ou les sites à trafic important.</span><span class="sxs-lookup"><span data-stu-id="2ef29-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="2ef29-124">![][StreamingLogsScreenshot]tooview hello **journaux de diffusion en continu** dans hello portail Azure, cliquez sur **flux du journal (1)** également dans hello **analyse** section du menu Paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="2ef29-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="2ef29-125">Si votre application écrit activement les instructions de trace, vous devez les voir Bonjour **de diffusion en continu (2) connecte à l’interface utilisateur** quasiment en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2ef29-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="2ef29-126">Console</span><span class="sxs-lookup"><span data-stu-id="2ef29-126">Console</span></span>
<span data-ttu-id="2ef29-127">Hello **portail Azure** fournit à l’application de console accès tooyour.</span><span class="sxs-lookup"><span data-stu-id="2ef29-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="2ef29-128">Vous pouvez explorer le système de fichiers de l’application et exécuter les scripts powershell/cmd.</span><span class="sxs-lookup"><span data-stu-id="2ef29-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="2ef29-129">Vous sont liés par hello autorisations mêmes définies en tant que code de votre application en cours d’exécution lors de l’exécution de commandes de la console.</span><span class="sxs-lookup"><span data-stu-id="2ef29-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="2ef29-130">Répertoires de tooprotected Access ou des scripts en cours d’exécution qui nécessitent des autorisations élevées est bloquée.</span><span class="sxs-lookup"><span data-stu-id="2ef29-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="2ef29-131">![][ConsoleScreenshot]À partir du menu Paramètres, faites défiler la liste trop**outils de développement** section, puis cliquez sur **Console (1)** et hello **(2) console** toohello droite s’ouvre l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ef29-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="2ef29-132">tooget familiarisé avec hello **console**, essayez les commandes de base telles que :</span><span class="sxs-lookup"><span data-stu-id="2ef29-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
