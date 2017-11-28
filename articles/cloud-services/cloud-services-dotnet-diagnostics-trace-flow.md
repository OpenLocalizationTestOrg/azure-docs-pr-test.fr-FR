---
title: flux de hello aaaTrace dans une Application de Services de Cloud avec Azure Diagnostics | Documents Microsoft
description: "Ajouter le traçage messages tooan Azure toohelp le débogage des applications, mesurer les performances, analyse, analyse du trafic et bien plus encore."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="acddf-103">Flux de hello de trace d’une application de Services de Cloud avec Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="acddf-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="acddf-104">Le suivi est un moyen pour vous toomonitor hello l’exécution de votre application pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="acddf-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="acddf-105">Vous pouvez utiliser hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), et [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) toorecord des informations sur les erreurs de classes et exécution de l’application dans des journaux, des fichiers texte ou autres appareils pour une analyse ultérieure.</span><span class="sxs-lookup"><span data-stu-id="acddf-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="acddf-106">Pour plus d’informations sur le suivi, consultez [Applications de suivi et instrumentation](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="acddf-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="acddf-107">Utilisez les instructions et commutateurs de suivi</span><span class="sxs-lookup"><span data-stu-id="acddf-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="acddf-108">Le traçage d’implémenter dans votre application de Services de cloud computing en ajoutant hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configuration de l’application et apporté des appels tooSystem.Diagnostics.Trace ou à System.Diagnostics.Debug dans votre code de l’application.</span><span class="sxs-lookup"><span data-stu-id="acddf-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="acddf-109">Utilisez un fichier configuration hello *app.config* pour les rôles de travail et hello *web.config* pour les rôles web.</span><span class="sxs-lookup"><span data-stu-id="acddf-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="acddf-110">Lorsque vous créez un nouveau service hébergé à l’aide d’un modèle Visual Studio, les Diagnostics Azure est automatiquement ajouté toohello projet et hello DiagnosticMonitorTraceListener est ajouté le fichier de configuration approprié toohello pour les rôles hello que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="acddf-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="acddf-111">Pour plus d’informations sur le placement des instructions de trace, consultez [Comment : ajouter des instructions de Trace tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="acddf-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="acddf-112">En plaçant des [Commutateurs de suivi](https://msdn.microsoft.com/library/3at424ac.aspx) dans votre code, vous pouvez contrôler le traçage et son importance.</span><span class="sxs-lookup"><span data-stu-id="acddf-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="acddf-113">Cela vous permet de surveiller l’état de hello de votre application dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="acddf-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="acddf-114">ce qui est particulièrement important dans une application qui utilise plusieurs composants s’exécutant sur plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="acddf-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="acddf-115">Pour plus d’informations, consultez la rubrique [Procédure : configuration de commutateurs de trace](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="acddf-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="acddf-116">Configurer un écouteur de suivi hello dans une application Windows Azure</span><span class="sxs-lookup"><span data-stu-id="acddf-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="acddf-117">Trace, Debug et TraceSource, vous demander de configurer « écouteurs » toocollect et messages hello enregistrements qui sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="acddf-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="acddf-118">Les écouteurs recueillent, stockent et acheminent les messages de suivi.</span><span class="sxs-lookup"><span data-stu-id="acddf-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="acddf-119">Elles indiquent hello suivi sortie tooan cible appropriée, telle qu’un journal, une fenêtre ou un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="acddf-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="acddf-120">Diagnostics Azure utilise hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="acddf-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="acddf-121">Avant d’effectuer hello suivant la procédure, vous devez initialiser hello moniteur de diagnostic Azure.</span><span class="sxs-lookup"><span data-stu-id="acddf-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="acddf-122">toodo, consultez [activation des Diagnostics dans Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="acddf-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="acddf-123">Notez que si vous utilisez des modèles hello fournis par Visual Studio, hello configuration du port d’écoute hello est ajoutée automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="acddf-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="acddf-124">Ajouter un écouteur de suivi</span><span class="sxs-lookup"><span data-stu-id="acddf-124">Add a trace listener</span></span>
1. <span data-ttu-id="acddf-125">Ouvrez le fichier web.config ou app.config de hello pour votre rôle.</span><span class="sxs-lookup"><span data-stu-id="acddf-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="acddf-126">Ajoutez hello fichier toohello de code suivant.</span><span class="sxs-lookup"><span data-stu-id="acddf-126">Add hello following code toohello file.</span></span> <span data-ttu-id="acddf-127">Modifier hello Version attribut toouse hello numéro de version de l’assembly que vous référencez hello.</span><span class="sxs-lookup"><span data-stu-id="acddf-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="acddf-128">version de l’assembly Hello ne change pas nécessairement avec chaque version de Windows Azure SDK sauf s’il existe des mises à jour tooit.</span><span class="sxs-lookup"><span data-stu-id="acddf-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="acddf-129">Assurez-vous que vous avez un toohello de référence de projet Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="acddf-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="acddf-130">Numéro de version de mise à jour hello dans xml hello au-dessus de version de hello toomatch de hello référencé Microsoft.WindowsAzure.Diagnostics assembly.</span><span class="sxs-lookup"><span data-stu-id="acddf-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="acddf-131">Enregistrez le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="acddf-131">Save hello config file.</span></span>

<span data-ttu-id="acddf-132">Pour plus d’informations sur les écouteurs, consultez [Suivi des écouteurs](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="acddf-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="acddf-133">Après avoir terminé le port d’écoute hello étapes tooadd hello, vous pouvez ajouter le code de tooyour instructions de trace.</span><span class="sxs-lookup"><span data-stu-id="acddf-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="acddf-134">code de tooyour tooadd trace instruction</span><span class="sxs-lookup"><span data-stu-id="acddf-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="acddf-135">Ouvrez un fichier source pour votre application.</span><span class="sxs-lookup"><span data-stu-id="acddf-135">Open a source file for your application.</span></span> <span data-ttu-id="acddf-136">Par exemple, hello <RoleName>fichier .cs pour le rôle de travail hello ou rôle web.</span><span class="sxs-lookup"><span data-stu-id="acddf-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="acddf-137">Ajoutez hello qui suit à l’aide d’instruction si elle n’a pas déjà été ajoutée :</span><span class="sxs-lookup"><span data-stu-id="acddf-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="acddf-138">Ajoutez les instructions Trace où vous souhaitez des informations de toocapture état hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="acddf-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="acddf-139">Vous pouvez utiliser une variété de sortie de hello tooformat méthodes Hello instruction de Trace.</span><span class="sxs-lookup"><span data-stu-id="acddf-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="acddf-140">Pour plus d’informations, consultez [Comment : ajouter des instructions de Trace tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="acddf-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="acddf-141">Enregistrez le fichier de source de hello.</span><span class="sxs-lookup"><span data-stu-id="acddf-141">Save hello source file.</span></span>

