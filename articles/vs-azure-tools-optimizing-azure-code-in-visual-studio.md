---
title: aaaOptimizing votre Azure de code dans Visual Studio | Documents Microsoft
description: "Découvrez comment les outils d'optimisation du code Azure dans Visual Studio peuvent rendre votre code plus robuste et plus performant."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="19c68-103">Optimisation de votre code Azure</span><span class="sxs-lookup"><span data-stu-id="19c68-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="19c68-104">Quand vous programmez des applications qui utilisent Microsoft Azure, il existe certaines pratiques de codage que vous devez suivre toohelp éviter les problèmes d’évolutivité de l’application, les comportements et les performances dans un environnement de cloud.</span><span class="sxs-lookup"><span data-stu-id="19c68-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="19c68-105">Microsoft fournit un outil Azure Code Analysis, qui reconnaît et identifie plusieurs des problèmes couramment rencontrés et qui vous aide à les résoudre.</span><span class="sxs-lookup"><span data-stu-id="19c68-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="19c68-106">Vous pouvez télécharger l’outil hello dans Visual Studio via NuGet.</span><span class="sxs-lookup"><span data-stu-id="19c68-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="19c68-107">Règles d’Azure Code Analysis</span><span class="sxs-lookup"><span data-stu-id="19c68-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="19c68-108">outil d’analyse du Code Azure Hello utilise hello suivant les règles tooautomatically indicateur votre code lorsqu’il détecte des performances en évitant les problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="19c68-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="19c68-109">Les problèmes détectés apparaissent sous la forme d’avertissements ou d’erreurs du compilateur.</span><span class="sxs-lookup"><span data-stu-id="19c68-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="19c68-110">Code corrections ou suggestions tooresolve hello avertissement ou erreur sont souvent fournis via une icône d’ampoule.</span><span class="sxs-lookup"><span data-stu-id="19c68-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="19c68-111">Évitez d'utiliser le mode d'état de session (in-process) par défaut</span><span class="sxs-lookup"><span data-stu-id="19c68-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="19c68-112">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-112">ID</span></span>
<span data-ttu-id="19c68-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="19c68-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="19c68-114">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-114">Description</span></span>
<span data-ttu-id="19c68-115">Si vous utilisez le mode d’état de session (in-process) par défaut hello pour les applications cloud, vous risquez de perdre l’état de session.</span><span class="sxs-lookup"><span data-stu-id="19c68-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="19c68-116">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-117">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-117">Reason</span></span>
<span data-ttu-id="19c68-118">Par défaut, le mode d’état de session hello spécifié dans le fichier web.config de hello est in-process.</span><span class="sxs-lookup"><span data-stu-id="19c68-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="19c68-119">En outre, si aucune entrée n’est spécifiée dans le fichier de configuration hello, mode d’état de Session hello par défaut tooin-process.</span><span class="sxs-lookup"><span data-stu-id="19c68-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="19c68-120">mode de Hello in-process stocke l’état de session en mémoire sur le serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="19c68-121">Lorsqu’une instance est redémarrée ou une nouvelle instance est utilisée pour l’équilibrage de charge ou de la prise en charge du basculement, l’état de session stockée en mémoire sur le serveur web de hello hello n’est pas enregistré.</span><span class="sxs-lookup"><span data-stu-id="19c68-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="19c68-122">Cette situation empêche l’application hello évolutivité de sur le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="19c68-123">L’état de session ASP.NET prend en charge plusieurs options de stockage différentes pour les données d’état de session : InProc, StateServer, SQLServer, personnalisée et désactivée.</span><span class="sxs-lookup"><span data-stu-id="19c68-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="19c68-124">Il est recommandé que vous utiliserez personnalisé en mode toohost sur un magasin d’état de Session externe, tel que [fournisseur d’état de Session Azure pour Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="19c68-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-125">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-125">Solution</span></span>
<span data-ttu-id="19c68-126">Une solution recommandée est l’état de session toostore sur un service de cache géré.</span><span class="sxs-lookup"><span data-stu-id="19c68-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="19c68-127">Découvrez comment toouse [fournisseur d’état de Session Azure pour Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore votre état de session.</span><span class="sxs-lookup"><span data-stu-id="19c68-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="19c68-128">Vous pouvez également magasin d’état de session dans d’autres emplacements de tooensure que votre application est évolutive dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="19c68-129">toolearn plus d’informations sur les solutions alternatives, consultez [Modes d’état de Session](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="19c68-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="19c68-130">La méthode d'exécution ne doit pas être asynchrone</span><span class="sxs-lookup"><span data-stu-id="19c68-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="19c68-131">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-131">ID</span></span>
<span data-ttu-id="19c68-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="19c68-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="19c68-133">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-133">Description</span></span>
<span data-ttu-id="19c68-134">Créez des méthodes asynchrones (telles que [await](https://msdn.microsoft.com/library/hh156528.aspx)) en dehors de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode), puis d’appeler des méthodes hello asynchrone à partir de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="19c68-135">Déclaration hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) de la méthode async provoque travailleur de hello rôle tooenter une boucle de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="19c68-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="19c68-136">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-137">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-137">Reason</span></span>
<span data-ttu-id="19c68-138">Appel de méthodes asynchrones à l’intérieur de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode entraîne un rôle de travail hello cloud service runtime toorecycle hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="19c68-139">Lorsqu’un rôle de travail démarre, l’exécution du programme tous les a lieu à l’intérieur de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="19c68-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="19c68-140">Sortie hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode entraîne un travail de hello toorestart de rôle.</span><span class="sxs-lookup"><span data-stu-id="19c68-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="19c68-141">Lors de l’exécution du rôle de travail hello atteint la méthode async de hello, il répartit toutes les opérations après la méthode async de hello, puis retourne.</span><span class="sxs-lookup"><span data-stu-id="19c68-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="19c68-142">Cela provoque la travailleur de hello rôle tooexit de hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode) et redémarrez.</span><span class="sxs-lookup"><span data-stu-id="19c68-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="19c68-143">Dans l’itération suivante de hello d’exécution, rôle de travail hello atteint la méthode async hello et redémarre, à l’origine de travail de hello toorecycle rôle également.</span><span class="sxs-lookup"><span data-stu-id="19c68-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-144">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-144">Solution</span></span>
<span data-ttu-id="19c68-145">Placez toutes les opérations asynchrones en dehors de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="19c68-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="19c68-146">Ensuite, appelez la méthode async de hello refactorisé à partir d’à l’intérieur de hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode, telle que RunAsync () .wait.</span><span class="sxs-lookup"><span data-stu-id="19c68-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="19c68-147">outil d’analyse du Code Azure Hello peut vous aider à résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="19c68-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="19c68-148">Hello suivant extrait de code illustre le correctif de code hello pour résoudre ce problème :</span><span class="sxs-lookup"><span data-stu-id="19c68-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="19c68-149">Utiliser l’authentification de signature d’accès partagé Service Bus</span><span class="sxs-lookup"><span data-stu-id="19c68-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="19c68-150">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-150">ID</span></span>
<span data-ttu-id="19c68-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="19c68-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="19c68-152">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-152">Description</span></span>
<span data-ttu-id="19c68-153">Utilisez la signature d’accès partagé (SAP) pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="19c68-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="19c68-154">Le service de contrôle d’accès (ACS) est obsolète pour l’authentification Service Bus.</span><span class="sxs-lookup"><span data-stu-id="19c68-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="19c68-155">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-156">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-156">Reason</span></span>
<span data-ttu-id="19c68-157">Pour une sécurité renforcée, Azure Active Directory remplace l’authentification du service de contrôle d’accès (ACS) par l’authentification de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="19c68-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="19c68-158">Consultez [Azure Active Directory est hello future des services ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) pour plus d’informations sur le plan de transition hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-159">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-159">Solution</span></span>
<span data-ttu-id="19c68-160">Utilisez l’authentification de signature d’accès partagé dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="19c68-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="19c68-161">Bonjour à l’exemple suivant montre comment toouse un tooaccess jeton SAS existant un service bus espace de noms ou de l’entité.</span><span class="sxs-lookup"><span data-stu-id="19c68-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="19c68-162">Consultez hello rubriques pour plus d’informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="19c68-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="19c68-163">Pour une vue d’ensemble, consultez [Authentification de signature d’accès partagé avec Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="19c68-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="19c68-164">Comment toouse authentification de Signature d’accès partagé avec Service Bus</span><span class="sxs-lookup"><span data-stu-id="19c68-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="19c68-165">Pour un exemple de projet, consultez [Utilisation de l’authentification de signature d’accès partagé avec des abonnements Service Bus](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="19c68-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="19c68-166">Envisagez d’utiliser tooavoid de méthode OnMessage « receive loop »</span><span class="sxs-lookup"><span data-stu-id="19c68-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="19c68-167">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-167">ID</span></span>
<span data-ttu-id="19c68-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="19c68-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="19c68-169">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-169">Description</span></span>
<span data-ttu-id="19c68-170">tooavoid dans une « boucle de réception, » hello appelant **OnMessage** méthode est une meilleure solution pour la réception des messages que l’appelant hello **réception** (méthode).</span><span class="sxs-lookup"><span data-stu-id="19c68-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="19c68-171">Toutefois, si vous devez utiliser hello **réception** (méthode) et que vous spécifiez un délai d’attente par défaut serveur, vérifiez que temps d’attente serveur hello plus d’une minute.</span><span class="sxs-lookup"><span data-stu-id="19c68-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="19c68-172">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-173">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-173">Reason</span></span>
<span data-ttu-id="19c68-174">Lors de l’appel **OnMessage**, client de hello démarre une pompe de messages interne qui interroge en permanence la file d’attente hello ou un abonnement.</span><span class="sxs-lookup"><span data-stu-id="19c68-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="19c68-175">Cette pompe de messages contient une boucle infinie qui émet un appel tooreceive messages.</span><span class="sxs-lookup"><span data-stu-id="19c68-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="19c68-176">Si l’appel de hello expire, il émet un nouvel appel.</span><span class="sxs-lookup"><span data-stu-id="19c68-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="19c68-177">intervalle de délai d’attente Hello est déterminé par la valeur hello hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propriété Hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)qui est utilisé.</span><span class="sxs-lookup"><span data-stu-id="19c68-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="19c68-178">avantage de l’utilisation de Hello **OnMessage** comparées trop**réception** est que les utilisateurs n’ont pas toomanually vérifier les messages, gestion des exceptions, traiter plusieurs messages en parallèle et terminer hello messages.</span><span class="sxs-lookup"><span data-stu-id="19c68-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="19c68-179">Si vous appelez **réception** sans utiliser sa valeur par défaut, être vraiment hello *ServerWaitTime* valeur est plus d’une minute.</span><span class="sxs-lookup"><span data-stu-id="19c68-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="19c68-180">Paramètre *ServerWaitTime* toomore d’une minute empêche le serveur de hello n’expire pas avant la réception du message de type hello est entièrement.</span><span class="sxs-lookup"><span data-stu-id="19c68-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-181">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-181">Solution</span></span>
<span data-ttu-id="19c68-182">Consultez hello suivant des exemples de code pour les utilisations recommandées.</span><span class="sxs-lookup"><span data-stu-id="19c68-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="19c68-183">Pour plus d’informations, consultez [QueueClient.OnMessage (méthode) (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) et [QueueClient.Receive (méthode) (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="19c68-184">tooimprove des performances de hello Hello infrastructure de messagerie Azure, consultez le modèle de conception hello [manuel de la messagerie asynchrone](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="19c68-185">Hello Voici un exemple d’utilisation **OnMessage** tooreceive messages.</span><span class="sxs-lookup"><span data-stu-id="19c68-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="19c68-186">Hello Voici un exemple d’utilisation **réception** avec le serveur par défaut de hello du temps d’attente.</span><span class="sxs-lookup"><span data-stu-id="19c68-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="19c68-187">Hello Voici un exemple d’utilisation **réception** avec un serveur non définis par défaut du temps d’attente.</span><span class="sxs-lookup"><span data-stu-id="19c68-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="19c68-188">Envisagez d'utiliser les méthodes asynchrones de Service Bus</span><span class="sxs-lookup"><span data-stu-id="19c68-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="19c68-189">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-189">ID</span></span>
<span data-ttu-id="19c68-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="19c68-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="19c68-191">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-191">Description</span></span>
<span data-ttu-id="19c68-192">Utilisez des performances tooimprove de méthodes asynchrones Service Bus avec la messagerie répartie.</span><span class="sxs-lookup"><span data-stu-id="19c68-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="19c68-193">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-194">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-194">Reason</span></span>
<span data-ttu-id="19c68-195">Permet de simultanée de programmes d’application à l’aide de méthodes asynchrones, car l’exécution de chaque appel ne bloque pas les thread principal hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="19c68-196">Lors de l’utilisation des méthodes de messagerie Service Bus, les opérations (envoi, réception, suppression, etc.) prennent du temps.</span><span class="sxs-lookup"><span data-stu-id="19c68-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="19c68-197">Ce temps inclut traitement hello d’opération de hello en hello Service service Bus de latence de toohello d’ajout de la demande de hello et réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="19c68-198">nombre de hello tooincrease d’opérations par période, les opérations doivent s’exécuter simultanément.</span><span class="sxs-lookup"><span data-stu-id="19c68-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="19c68-199">Pour plus d’informations, consultez trop[meilleures pratiques pour les performances améliorations apportées à l’aide de messagerie répartie Service Bus](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-200">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-200">Solution</span></span>
<span data-ttu-id="19c68-201">Consultez [classe QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) pour plus d’informations sur comment toouse hello recommandé de méthode asynchrone.</span><span class="sxs-lookup"><span data-stu-id="19c68-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="19c68-202">tooimprove des performances de hello Hello infrastructure de messagerie Azure, consultez le modèle de conception hello [manuel de la messagerie asynchrone](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="19c68-203">Envisagez de partitionner les files d’attente et les rubriques Service Bus</span><span class="sxs-lookup"><span data-stu-id="19c68-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="19c68-204">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-204">ID</span></span>
<span data-ttu-id="19c68-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="19c68-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="19c68-206">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-206">Description</span></span>
<span data-ttu-id="19c68-207">Partitionnement des files d’attente et des rubriques Service Bus pour de meilleures performances avec la messagerie Service Bus.</span><span class="sxs-lookup"><span data-stu-id="19c68-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="19c68-208">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-209">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-209">Reason</span></span>
<span data-ttu-id="19c68-210">Partitionnement des rubriques et files d’attente Service Bus augmente les performances de débit et le service de disponibilité hello débit global d’une file d’attente partitionnée ou une rubrique est n’est plus limité par des performances d’un seul broker ou de la banque de messages hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="19c68-211">En outre, la panne temporaire d’un magasin de messagerie ne rend pas une rubrique ou une file d’attente partitionnée indisponible.</span><span class="sxs-lookup"><span data-stu-id="19c68-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="19c68-212">Pour plus d’informations, consultez la rubrique [Partitionnement des entités de messagerie](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-213">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-213">Solution</span></span>
<span data-ttu-id="19c68-214">Hello suivant extrait de code montre comment toopartition des entités de messagerie.</span><span class="sxs-lookup"><span data-stu-id="19c68-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="19c68-215">Pour plus d’informations, consultez [partitionné les files d’attente de Service Bus et rubriques | Blog de Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) et extraire hello [file d’attente de Microsoft Azure Service Bus partitionnée](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) exemple.</span><span class="sxs-lookup"><span data-stu-id="19c68-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="19c68-216">Ne pas définir SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="19c68-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="19c68-217">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-217">ID</span></span>
<span data-ttu-id="19c68-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="19c68-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="19c68-219">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-219">Description</span></span>
<span data-ttu-id="19c68-220">Évitez d’utiliser SharedAccessStartTimeset toohello heure actuelle tooimmediately démarrer hello stratégie d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="19c68-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="19c68-221">Vous ne devez tooset cette propriété si vous souhaitez que d’une stratégie d’accès partagé hello toostart ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="19c68-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="19c68-222">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-223">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-223">Reason</span></span>
<span data-ttu-id="19c68-224">La synchronisation de l’heure provoque une légère différence d’heure entre les centres de données.</span><span class="sxs-lookup"><span data-stu-id="19c68-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="19c68-225">Par exemple, il serait logique heure de début de paramètre hello une stratégie de stockage SAS car hello heure actuelle à l’aide de DateTime.Now ou une méthode similaire entraîne l’effet de tootake hello SAS stratégie immédiatement.</span><span class="sxs-lookup"><span data-stu-id="19c68-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="19c68-226">Toutefois, hello légère différence d’heure entre les centres de données peut entraîner des problèmes dans la mesure où certains centres peuvent être légèrement postérieure à l’heure de début de hello, tandis que d’autres sont en avance.</span><span class="sxs-lookup"><span data-stu-id="19c68-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="19c68-227">Par conséquent, hello stratégie de SAP peut expirer rapidement (ou même immédiatement) si la durée de vie de stratégie hello est trop faible.</span><span class="sxs-lookup"><span data-stu-id="19c68-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="19c68-228">Pour plus d’informations sur l’utilisation de la Signature d’accès partagé sur le stockage Azure, consultez [présentation de la Table SAS (Shared Access Signature) SAS de file d’attente de Site et mise à jour tooBlob SAS - Blog d’équipe Microsoft Azure Storage - accueil - Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-229">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-229">Solution</span></span>
<span data-ttu-id="19c68-230">Supprimez l’instruction hello qui définit l’heure de début hello de stratégie d’accès partagé de hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="19c68-231">outil d’analyse du Code Azure Hello fournit un correctif pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="19c68-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="19c68-232">Pour plus d’informations sur la gestion de la sécurité, consultez le modèle de conception hello [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="19c68-233">Hello suivant extrait de code illustre le correctif de code hello pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="19c68-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="19c68-234">Le délai d'expiration de la stratégie d'accès partagé doit être de plus de cinq minutes</span><span class="sxs-lookup"><span data-stu-id="19c68-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="19c68-235">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-235">ID</span></span>
<span data-ttu-id="19c68-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="19c68-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="19c68-237">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-237">Description</span></span>
<span data-ttu-id="19c68-238">Il peut y avoir jusqu'à cinq minutes de différence entre les centres de données situés à différents emplacements en raison de la condition tooa appelé « décalage d’horloge. » les horloges</span><span class="sxs-lookup"><span data-stu-id="19c68-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="19c68-239">jeton de stratégie tooprevent hello SAP à partir de la date d’expiration définie plus tôt que prévu, toobe de temps d’expiration hello plus de cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="19c68-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="19c68-240">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-241">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-241">Reason</span></span>
<span data-ttu-id="19c68-242">Centres de données situés à différents emplacements monde hello synchronisent à un signal d’horloge.</span><span class="sxs-lookup"><span data-stu-id="19c68-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="19c68-243">Étant donné que le temps requis pour l’horloge signal tootravel toodifferent des emplacements, il peut y avoir un écart de temps entre les centres de données à différents emplacements géographiques bien que tout est censé être synchronisé.</span><span class="sxs-lookup"><span data-stu-id="19c68-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="19c68-244">Cette différence peut affecter hello accès partagé début temps et expiration intervalle de stratégie.</span><span class="sxs-lookup"><span data-stu-id="19c68-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="19c68-245">Par conséquent, tooensure stratégie d’accès partagé prend effet immédiatement, ne spécifiez pas l’heure de début hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="19c68-246">En outre, veillez à délai d’expiration de hello est supérieure au délai d’expiration de 5 minutes tooprevent anticipée.</span><span class="sxs-lookup"><span data-stu-id="19c68-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="19c68-247">Pour plus d’informations sur l’utilisation de la Signature d’accès partagé sur le stockage Azure, consultez [présentation de la Table SAS (Shared Access Signature) SAS de file d’attente de Site et mise à jour tooBlob SAS - Blog d’équipe Microsoft Azure Storage - accueil - Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-248">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-248">Solution</span></span>
<span data-ttu-id="19c68-249">Pour plus d’informations sur la gestion de la sécurité, consultez le modèle de conception hello [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="19c68-250">Hello Voici un exemple de ne pas spécifier une heure de début de stratégie accès partagé.</span><span class="sxs-lookup"><span data-stu-id="19c68-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="19c68-251">Hello Voici un exemple de spécification d’une heure de début de stratégie accès partagé avec une durée d’expiration de stratégie supérieure à cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="19c68-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="19c68-252">Pour plus d'informations, consultez [Créer et utiliser une signature d’accès partagé](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="19c68-253">Utiliser CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="19c68-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="19c68-254">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-254">ID</span></span>
<span data-ttu-id="19c68-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="19c68-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="19c68-256">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-256">Description</span></span>
<span data-ttu-id="19c68-257">À l’aide de hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) classe pour les projets, telles que les sites Web Azure et services mobiles Azure ne présentent aucun problème d’exécution.</span><span class="sxs-lookup"><span data-stu-id="19c68-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="19c68-258">Comme meilleure pratique, cependant, il est une bonne idée de toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) de façon unifiée de gestion des configurations pour toutes les applications de Cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="19c68-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="19c68-259">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-260">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-260">Reason</span></span>
<span data-ttu-id="19c68-261">CloudConfigurationManager lit l’environnement d’application hello configuration fichier toohello approprié.</span><span class="sxs-lookup"><span data-stu-id="19c68-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="19c68-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="19c68-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="19c68-263">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-263">Solution</span></span>
<span data-ttu-id="19c68-264">Refactoriser votre hello toouse de code [classe CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="19c68-265">Un correctif pour résoudre ce problème est fourni par l’outil d’analyse de Code Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="19c68-266">Hello suivant extrait de code illustre le correctif de code hello pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="19c68-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="19c68-267">Replace</span><span class="sxs-lookup"><span data-stu-id="19c68-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="19c68-268">par</span><span class="sxs-lookup"><span data-stu-id="19c68-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="19c68-269">Voici un exemple de comment toostore hello le paramètre de configuration dans un fichier App.config ou Web.config.</span><span class="sxs-lookup"><span data-stu-id="19c68-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="19c68-270">Ajoutez la section appSettings toohello du paramètres hello hello du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="19c68-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="19c68-271">Hello Voici fichier Web.config de hello pour l’exemple de code précédent hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="19c68-272">Évitez d'utiliser des chaînes de connexion codées en dur</span><span class="sxs-lookup"><span data-stu-id="19c68-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="19c68-273">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-273">ID</span></span>
<span data-ttu-id="19c68-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="19c68-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="19c68-275">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-275">Description</span></span>
<span data-ttu-id="19c68-276">Si vous utilisez des chaînes de connexion codées en dur et que vous devez tooupdate les plus tard, vous disposez du code source de toomake modifications tooyour et recompiler l’application hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="19c68-277">Toutefois, si vous stockez vos chaînes de connexion dans un fichier de configuration, vous pouvez modifier les ultérieurement en mettant simplement à jour le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="19c68-278">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-279">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-279">Reason</span></span>
<span data-ttu-id="19c68-280">Le codage en dur les chaînes de connexion est une mauvaise pratique, car elle présente des problèmes lorsque les chaînes de connexion doivent toobe modifiée rapidement.</span><span class="sxs-lookup"><span data-stu-id="19c68-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="19c68-281">En outre, si hello doit toobe archivé toosource contrôle, les chaînes de connexion codées en dur introduisent des failles de sécurité dans la mesure où les chaînes de hello peuvent être affichées dans le code source de hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-282">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-282">Solution</span></span>
<span data-ttu-id="19c68-283">Stocker des chaînes de connexion dans les fichiers de configuration hello ou environnements Azure.</span><span class="sxs-lookup"><span data-stu-id="19c68-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="19c68-284">Pour les applications autonomes, utilisez les paramètres de chaîne de connexion toostore app.config.</span><span class="sxs-lookup"><span data-stu-id="19c68-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="19c68-285">Pour les applications web hébergé par IIS, utilisez les chaînes de connexion web.config toostore.</span><span class="sxs-lookup"><span data-stu-id="19c68-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="19c68-286">Pour les applications ASP.NET vNext, utilisez configuration.json toostore les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="19c68-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="19c68-287">Pour plus d’informations sur l’utilisation de fichiers de configuration comme web.config ou app.config, consultez la page [Conseils de configuration ASP.NET web](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="19c68-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="19c68-288">Pour plus d’informations sur le fonctionnement des variables d’environnement Azure, consultez [Sites web Microsoft Azure : Fonctionnement des chaînes d’application et des chaînes de connexion](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="19c68-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="19c68-289">Pour plus d’informations sur le stockage de la chaîne de connexion dans le contrôle de code source, consultez la rubrique [Éviter de placer des informations sensibles (par exemple, des chaînes de connexion) dans des fichiers stockés dans des référentiels de code source](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="19c68-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="19c68-290">Utiliser le fichier de configuration des diagnostics</span><span class="sxs-lookup"><span data-stu-id="19c68-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="19c68-291">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-291">ID</span></span>
<span data-ttu-id="19c68-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="19c68-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="19c68-293">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-293">Description</span></span>
<span data-ttu-id="19c68-294">Au lieu de configurer les paramètres de diagnostic dans votre code, par exemple à l’aide de hello Microsoft.WindowsAzure.Diagnostics API de programmation, vous devez configurer les paramètres de diagnostic dans le fichier de diagnostics.wadcfg hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="19c68-295">(ou diagnostics.wadcfgx si vous utilisez Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="19c68-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="19c68-296">Ce faisant, vous pouvez modifier les paramètres de diagnostic sans avoir toorecompile votre code.</span><span class="sxs-lookup"><span data-stu-id="19c68-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="19c68-297">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-298">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-298">Reason</span></span>
<span data-ttu-id="19c68-299">Avant Azure SDK 2.5 (qui utilise Azure diagnostics 1.3), Azure Diagnostics (WAD) peut être configuré à l’aide de différentes méthodes : ajout de son objet blob de configuration toohello dans le stockage, à l’aide du code impératif, une configuration déclarative ou par défaut de hello configuration.</span><span class="sxs-lookup"><span data-stu-id="19c68-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="19c68-300">Toutefois, hello préféré de façon tooconfigure diagnostics est toouse un fichier de configuration XML (diagnostics.wadcfg ou Diagnostics.wadcfgx pour le SDK 2.5 et versions ultérieures) dans un projet d’application hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="19c68-301">Dans cette approche, fichier de diagnostics.wadcfg hello complètement définit la configuration de hello et peut être mis à jour et redéployé à volonté.</span><span class="sxs-lookup"><span data-stu-id="19c68-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="19c68-302">Utilisation de hello du fichier de configuration diagnostics.wadcfg hello redémarrables avec hello des méthodes de programmation de la définition de configurations à l’aide de hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) classes peuvent entraîner des tooconfusion.</span><span class="sxs-lookup"><span data-stu-id="19c68-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="19c68-303">Consultez la rubrique [Initialiser ou modifier la configuration des diagnostics Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="19c68-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="19c68-304">Depuis WAD 1.3 (fourni avec Azure SDK 2.5), il n’est plus diagnostics tooconfigure du code toouse possible.</span><span class="sxs-lookup"><span data-stu-id="19c68-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="19c68-305">Par conséquent, vous pouvez fournir uniquement configuration hello lors de l’application ou extension de diagnostics hello de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="19c68-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-306">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-306">Solution</span></span>
<span data-ttu-id="19c68-307">Utilisez hello diagnostics concepteur toomove les paramètres de diagnostic toohello diagnostics configuration fichier de configuration (Diagnostics.wadcfg ou Diagnostics.wadcfgx pour le SDK 2.5 et versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="19c68-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="19c68-308">Il est également recommandé d’installer [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) et utiliser la fonctionnalité diagnostics de la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="19c68-309">Dans le menu contextuel hello rôle hello que vous souhaitez tooconfigure, choisissez Propriétés, puis onglet de Configuration hello.</span><span class="sxs-lookup"><span data-stu-id="19c68-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="19c68-310">Bonjour **Diagnostics** section, assurez-vous que hello **activer les Diagnostics** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="19c68-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="19c68-311">Choisissez hello **configurer** bouton.</span><span class="sxs-lookup"><span data-stu-id="19c68-311">Choose hello **Configure** button.</span></span>

   ![Option de hello activer les Diagnostics de l’accès à](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="19c68-313">Consultez [Configuration des diagnostics pour Azure Cloud Services et Azure Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="19c68-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="19c68-314">Éviter de déclarer les objets DbContext comme statiques</span><span class="sxs-lookup"><span data-stu-id="19c68-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="19c68-315">ID</span><span class="sxs-lookup"><span data-stu-id="19c68-315">ID</span></span>
<span data-ttu-id="19c68-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="19c68-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="19c68-317">Description</span><span class="sxs-lookup"><span data-stu-id="19c68-317">Description</span></span>
<span data-ttu-id="19c68-318">toosave mémoire, évitez de déclarer les objets DBContext comme statiques.</span><span class="sxs-lookup"><span data-stu-id="19c68-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="19c68-319">Pensez à partager vos idées et vos commentaires sur la page [Commentaires d’analyse du code Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="19c68-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="19c68-320">Motif</span><span class="sxs-lookup"><span data-stu-id="19c68-320">Reason</span></span>
<span data-ttu-id="19c68-321">Les objets DBContext contiennent hello des résultats de requête à partir de chaque appel.</span><span class="sxs-lookup"><span data-stu-id="19c68-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="19c68-322">Les objets DBContext statiques ne sont pas supprimés jusqu'à ce que le domaine d’application hello est déchargé.</span><span class="sxs-lookup"><span data-stu-id="19c68-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="19c68-323">Par conséquent, un objet DBContext statique peut consommer de grandes quantités de mémoire.</span><span class="sxs-lookup"><span data-stu-id="19c68-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="19c68-324">Solution</span><span class="sxs-lookup"><span data-stu-id="19c68-324">Solution</span></span>
<span data-ttu-id="19c68-325">Déclarer DBContext comme variable locale ou champ d’instance non statique, l’utiliser pour une tâche et le laisser être supprimé après utilisation.</span><span class="sxs-lookup"><span data-stu-id="19c68-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="19c68-326">Hello suivant l’exemple de classe de contrôleur MVC montre comment toouse hello DBContext objet.</span><span class="sxs-lookup"><span data-stu-id="19c68-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="19c68-327">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19c68-327">Next steps</span></span>
<span data-ttu-id="19c68-328">toolearn en savoir plus sur l’optimisation et la résolution des problèmes d’applications Azure, consultez [dépanner une application web dans Azure App Service à l’aide de Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="19c68-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
