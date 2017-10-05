---
title: Journaux de diffusion en continu et console
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="97b38-103">Journaux en continu et console</span><span class="sxs-lookup"><span data-stu-id="97b38-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="97b38-104">Journaux en continu</span><span class="sxs-lookup"><span data-stu-id="97b38-104">Streaming Logs</span></span>
<span data-ttu-id="97b38-105">Le **portail Azure** intègre une fonction d’affichage des journaux de diffusion en continu qui vous permet de suivre les événements de vos applications **App Service** en temps réel.</span><span class="sxs-lookup"><span data-stu-id="97b38-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="97b38-106">La configuration de cette fonction se fait en quelques étapes simples :</span><span class="sxs-lookup"><span data-stu-id="97b38-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="97b38-107">Écriture des suivis dans votre code</span><span class="sxs-lookup"><span data-stu-id="97b38-107">Write traces in your code</span></span>
* <span data-ttu-id="97b38-108">Activation des **journaux de diagnostic** pour votre application</span><span class="sxs-lookup"><span data-stu-id="97b38-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="97b38-109">Affichage du flux à partir de l’interface utilisateur **Journaux de streaming** dans le **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="97b38-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="97b38-110">Écriture des suivis dans votre code</span><span class="sxs-lookup"><span data-stu-id="97b38-110">How to write traces in your code</span></span>
<span data-ttu-id="97b38-111">L'écriture des suivis dans votre code est simple.</span><span class="sxs-lookup"><span data-stu-id="97b38-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="97b38-112">Dans C#, il suffit d'écrire le code suivant :</span><span class="sxs-lookup"><span data-stu-id="97b38-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="97b38-113">La classe Trace se trouve dans l'espace de noms System.Diagnostics</span><span class="sxs-lookup"><span data-stu-id="97b38-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="97b38-114">Dans une application node.js, vous pouvez écrire le code suivant pour atteindre le même résultat :</span><span class="sxs-lookup"><span data-stu-id="97b38-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="97b38-115">Activation et affichage des journaux en continu</span><span class="sxs-lookup"><span data-stu-id="97b38-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="97b38-116">![][BrowseSitesScreenshot] Les diagnostics sont activés par application.</span><span class="sxs-lookup"><span data-stu-id="97b38-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="97b38-117">Commencez par naviguer jusqu’au site pour lequel vous souhaitez activer cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="97b38-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="97b38-118">![][DiagnosticsLogs] À partir du menu Paramètres, faites défiler jusqu’à la section **Analyse** et cliquez sur **(1) Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="97b38-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="97b38-119">Puis **(2) activez** **Journal des applications (Filesystem)** ou **Journal des applications (Blob)** L’option **Niveau** vous permet de modifier le niveau de gravité des suivis à capturer.</span><span class="sxs-lookup"><span data-stu-id="97b38-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="97b38-120">Si vous souhaitez simplement vous familiariser avec la fonctionnalité, définissez-la sur **Verbose** pour être sûr que toutes vos instructions de suivi seront collectées.</span><span class="sxs-lookup"><span data-stu-id="97b38-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="97b38-121">Cliquez sur **SAVE** en haut du volet pour afficher les journaux.</span><span class="sxs-lookup"><span data-stu-id="97b38-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="97b38-122">Plus le **niveau de gravité** est élevé, plus les ressources consommées dans le journal sont importantes et plus vous obtiendrez de suivis.</span><span class="sxs-lookup"><span data-stu-id="97b38-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="97b38-123">Vérifiez que le **niveau de gravité** est configuré sur le niveau de détail approprié pour un site de production ou ayant un fort trafic.</span><span class="sxs-lookup"><span data-stu-id="97b38-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="97b38-124">![][StreamingLogsScreenshot] Pour afficher les **journaux de streaming** au sein du portail Azure, cliquez sur **(1) Flux de journaux** également dans la section **Analyse** du menu Paramètres.</span><span class="sxs-lookup"><span data-stu-id="97b38-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="97b38-125">Si des instructions de suivi sont en cours d’écriture sur votre application, vous devez les voir presque en temps réel dans les **(2) journaux de streaming**.</span><span class="sxs-lookup"><span data-stu-id="97b38-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="97b38-126">Console</span><span class="sxs-lookup"><span data-stu-id="97b38-126">Console</span></span>
<span data-ttu-id="97b38-127">Le **portail Azure** fournit un accès à la console à votre application.</span><span class="sxs-lookup"><span data-stu-id="97b38-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="97b38-128">Vous pouvez explorer le système de fichiers de l’application et exécuter les scripts powershell/cmd.</span><span class="sxs-lookup"><span data-stu-id="97b38-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="97b38-129">Lorsque vous exécutez des commandes de la console, vous dépendez des mêmes autorisations que pour votre code d’application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="97b38-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="97b38-130">Vous ne pouvez pas accéder aux répertoires protégés ni exécuter des scripts qui demandent des autorisations élevées.</span><span class="sxs-lookup"><span data-stu-id="97b38-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="97b38-131">![][ConsoleScreenshot] À partir du menu Paramètres, faites défiler jusqu’à la section **Outils de développement** et cliquez sur **Console (1)**. La **(2) console** s’ouvre alors à droite.</span><span class="sxs-lookup"><span data-stu-id="97b38-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="97b38-132">Pour vous familiariser avec la **console**, commencez par les commandes élémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="97b38-132">To get familiar with the **console**, try basic commands like:</span></span>

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
