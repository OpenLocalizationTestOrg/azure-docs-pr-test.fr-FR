---
title: Assurer le suivi du flux dans une application Cloud Services avec Diagnostics Azure | Microsoft Docs
description: "Ajouter des messages de suivi à une application Azure pour aider au débogage, à la mesure des performances, à la surveillance, à l’analyse du trafic et bien plus encore."
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
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="2058f-103">Assurer le suivi du flux dans une application Cloud Services avec Diagnostics Azure</span><span class="sxs-lookup"><span data-stu-id="2058f-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="2058f-104">Le suivi est un moyen de surveiller l’exécution de votre application pendant son exécution .</span><span class="sxs-lookup"><span data-stu-id="2058f-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="2058f-105">Vous pouvez utiliser les classes [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) et [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) pour enregistrer des informations relatives aux erreurs et à l’exécution des applications dans des journaux, des fichiers texte ou d’autres périphériques pour une analyse ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2058f-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="2058f-106">Pour plus d’informations sur le suivi, consultez [Applications de suivi et instrumentation](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="2058f-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="2058f-107">Utilisez les instructions et commutateurs de suivi</span><span class="sxs-lookup"><span data-stu-id="2058f-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="2058f-108">Mettez en œuvre le suivi dans votre application Cloud Services en ajoutant [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) à la configuration d’application et en lançant des appels vers System.Diagnostics.Trace ou vers System.Diagnostics.Debug dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="2058f-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="2058f-109">Utilisez le fichier de configuration *app.config* pour les rôles de travail et le fichier *web.config* pour les rôles web.</span><span class="sxs-lookup"><span data-stu-id="2058f-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="2058f-110">Lorsque vous créez un nouveau service hébergé à l’aide d’un modèle Visual Studio, Azure Diagnostics est automatiquement ajouté au projet et DiagnosticMonitorTraceListener est ajouté au fichier de configuration approprié pour les rôles que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="2058f-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="2058f-111">Pour plus d’informations sur le placement des instructions de suivi, consultez [Procédure : ajouter des instructions de suivi au Code d’application](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="2058f-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="2058f-112">En plaçant des [Commutateurs de suivi](https://msdn.microsoft.com/library/3at424ac.aspx) dans votre code, vous pouvez contrôler le traçage et son importance.</span><span class="sxs-lookup"><span data-stu-id="2058f-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="2058f-113">Vous pouvez ainsi surveiller l’état de votre application dans un environnement de production,</span><span class="sxs-lookup"><span data-stu-id="2058f-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="2058f-114">ce qui est particulièrement important dans une application qui utilise plusieurs composants s’exécutant sur plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="2058f-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="2058f-115">Pour plus d’informations, consultez la rubrique [Procédure : configuration de commutateurs de trace](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="2058f-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="2058f-116">Configurer l’écouteur de suivi dans une application Azure</span><span class="sxs-lookup"><span data-stu-id="2058f-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="2058f-117">Trace, Debug et TraceSource nécessitent que vous définissiez des « écouteurs » pour recueillir et enregistrer les messages qui sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="2058f-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="2058f-118">Les écouteurs recueillent, stockent et acheminent les messages de suivi.</span><span class="sxs-lookup"><span data-stu-id="2058f-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="2058f-119">Ils orientent la sortie de suivi vers une cible appropriée, par exemple un journal, une fenêtre ou un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="2058f-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="2058f-120">Azure Diagnostics utilise la classe [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2058f-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="2058f-121">Avant d’exécuter la procédure suivante, vous devez initialiser le moniteur de diagnostic Azure.</span><span class="sxs-lookup"><span data-stu-id="2058f-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="2058f-122">Pour ce faire, voir [Activation des diagnostics dans Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2058f-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="2058f-123">Notez que si vous utilisez les modèles fournis par Visual Studio, la configuration de l’écouteur est automatiquement ajoutée pour vous.</span><span class="sxs-lookup"><span data-stu-id="2058f-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="2058f-124">Ajouter un écouteur de suivi</span><span class="sxs-lookup"><span data-stu-id="2058f-124">Add a trace listener</span></span>
1. <span data-ttu-id="2058f-125">Ouvrez le fichier web.config ou app.config correspondant à votre rôle.</span><span class="sxs-lookup"><span data-stu-id="2058f-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="2058f-126">Ajoutez le code suivant au fichier.</span><span class="sxs-lookup"><span data-stu-id="2058f-126">Add the following code to the file.</span></span> <span data-ttu-id="2058f-127">Modifiez l’attribut de version pour utiliser le numéro de version de l’assembly que vous référencez.</span><span class="sxs-lookup"><span data-stu-id="2058f-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="2058f-128">La version d’assembly ne change pas nécessairement avec chaque version du Kit de développement logiciel (SDK) Azure sauf s’il existe des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="2058f-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
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
   > <span data-ttu-id="2058f-129">Assurez-vous de disposer d’une référence de projet à l’assembly Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="2058f-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="2058f-130">Mettre à jour le numéro de version dans le document xml ci-dessus pour correspondre à la version de l’assembly Microsoft.WindowsAzure.Diagnostics référencé.</span><span class="sxs-lookup"><span data-stu-id="2058f-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="2058f-131">Enregistrez le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="2058f-131">Save the config file.</span></span>

<span data-ttu-id="2058f-132">Pour plus d’informations sur les écouteurs, consultez [Suivi des écouteurs](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="2058f-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="2058f-133">Une fois les opérations destinées à ajouter l’écouteur terminées, vous pouvez ajouter des instructions de suivi à votre code.</span><span class="sxs-lookup"><span data-stu-id="2058f-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="2058f-134">Pour ajouter des instructions de suivi à votre code</span><span class="sxs-lookup"><span data-stu-id="2058f-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="2058f-135">Ouvrez un fichier source pour votre application.</span><span class="sxs-lookup"><span data-stu-id="2058f-135">Open a source file for your application.</span></span> <span data-ttu-id="2058f-136">Par exemple, le fichier <RoleName>.cs pour le rôle de travail ou le rôle web.</span><span class="sxs-lookup"><span data-stu-id="2058f-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="2058f-137">Ajoutez le code suivant à l’aide d’une instruction s’il n’a pas été encore ajouté :</span><span class="sxs-lookup"><span data-stu-id="2058f-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="2058f-138">Ajoutez les instructions de suivi à l’endroit où vous souhaitez capturer des informations sur l’état de votre application.</span><span class="sxs-lookup"><span data-stu-id="2058f-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="2058f-139">Vous pouvez utiliser différentes méthodes pour mettre en forme la sortie de l’instruction de suivi.</span><span class="sxs-lookup"><span data-stu-id="2058f-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="2058f-140">Pour plus d’informations, consultez [Procédure : Ajout d’instructions de suivi au code d’application](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="2058f-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="2058f-141">Enregistrez le fichier source.</span><span class="sxs-lookup"><span data-stu-id="2058f-141">Save the source file.</span></span>

