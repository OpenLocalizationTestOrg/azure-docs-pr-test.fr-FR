---
title: "application à plusieurs niveaux de aaa.NET à l’aide d’Azure Service Bus | Documents Microsoft"
description: "Un didacticiel .NET qui vous permet de développer une application à plusieurs niveaux dans Azure qui utilise toocommunicate de files d’attente Service Bus entre les couches."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="eb41d-103">Application multiniveau .NET avec les files d’attente Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="eb41d-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="eb41d-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="eb41d-104">Introduction</span></span>
<span data-ttu-id="eb41d-105">Développement de Microsoft Azure est facile à l’aide de Visual Studio et hello gratuit Azure SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="eb41d-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="eb41d-106">Ce didacticiel vous guide dans hello étapes toocreate une application qui utilise plusieurs ressources Azure en cours d’exécution dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="eb41d-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="eb41d-107">Vous allez apprendre suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="eb41d-107">You will learn hello following:</span></span>

* <span data-ttu-id="eb41d-108">Comment tooenable votre ordinateur pour le développement Azure avec un seul télécharger et installer.</span><span class="sxs-lookup"><span data-stu-id="eb41d-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="eb41d-109">Comment toodevelop de Visual Studio toouse pour Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41d-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="eb41d-110">Comment toocreate une application à plusieurs niveaux dans Azure à l’aide de rôles web et worker.</span><span class="sxs-lookup"><span data-stu-id="eb41d-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="eb41d-111">Comment toocommunicate entre les couches à l’aide de files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eb41d-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="eb41d-112">Dans ce didacticiel vous allez générer et exécuter l’application à plusieurs niveaux de hello dans un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41d-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="eb41d-113">frontal Hello est un rôle web d’ASP.NET MVC et back-end hello est un rôle de travail qui utilise une file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eb41d-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="eb41d-114">Vous pouvez créer hello même d’application à plusieurs niveaux avec frontal hello comme un projet web, qui est déployé tooan site Web Azure au lieu d’un service cloud.</span><span class="sxs-lookup"><span data-stu-id="eb41d-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="eb41d-115">Vous pouvez également essayer hello [application de .NET sur le site/cloud hybride](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="eb41d-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="eb41d-116">Hello capture d’écran suivante montre les application hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="eb41d-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="eb41d-117">Vue d’ensemble du scénario : communication entre les rôles</span><span class="sxs-lookup"><span data-stu-id="eb41d-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="eb41d-118">toosubmit un ordre de traitement, composant UI frontal hello, en cours d’exécution dans un rôle web de hello, doit interagir avec la logique de couche intermédiaire hello en cours d’exécution dans le rôle de travail hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="eb41d-119">Cet exemple utilise le Bus des services de messagerie pour les communications entre les couches de hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="eb41d-120">Utilisation du Service Bus entre hello central les couches web et de messagerie dissocie les deux composants.</span><span class="sxs-lookup"><span data-stu-id="eb41d-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="eb41d-121">En revanche toodirect (autrement dit, TCP ou HTTP), la messagerie de hello couche web ne connecte pas intermédiaire toohello directement. au lieu de cela, il pousse les unités de travail, sous forme de messages, dans Service Bus, ce qui les conserve jusqu'à ce que le niveau intermédiaire de hello est prêt tooconsume et de les traiter de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="eb41d-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="eb41d-122">Service Bus fournit la messagerie de deux entités toosupport répartie : files d’attente et rubriques.</span><span class="sxs-lookup"><span data-stu-id="eb41d-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="eb41d-123">Avec les files d’attente, chaque message envoyé à la file d’attente de toohello est consommée par un destinataire unique.</span><span class="sxs-lookup"><span data-stu-id="eb41d-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="eb41d-124">Rubriques prennent en charge le modèle de publication/abonnement hello dans lequel chaque message publié est mis abonnement disponible tooa inscrit auprès de hello rubrique.</span><span class="sxs-lookup"><span data-stu-id="eb41d-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="eb41d-125">Chaque abonnement gère de façon logique sa propre file d’attente de messages.</span><span class="sxs-lookup"><span data-stu-id="eb41d-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="eb41d-126">Abonnements peuvent également être configurés avec les règles de filtre qui restreignent hello ensemble de messages transmis à toothose de file d’attente d’abonnement hello qui correspondent au filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="eb41d-127">Hello exemple suivant utilise les files d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eb41d-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="eb41d-128">Ce mécanisme de communication présente plusieurs avantages par rapport à la messagerie directe :</span><span class="sxs-lookup"><span data-stu-id="eb41d-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="eb41d-129">**Découplage temporel.**</span><span class="sxs-lookup"><span data-stu-id="eb41d-129">**Temporal decoupling.**</span></span> <span data-ttu-id="eb41d-130">Avec le modèle de messagerie asynchrone hello, producteurs et consommateurs ne sont pas nécessairement en ligne à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="eb41d-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="eb41d-131">Bus de service fiable stocke les messages jusqu'à ce que le récepteur hello est prêt à les recevoir.</span><span class="sxs-lookup"><span data-stu-id="eb41d-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="eb41d-132">Cela permet aux composants de hello de hello distribué application toobe est déconnecté, soit volontairement, par exemple, pour maintenance ou en raison du blocage d’un composant tooa, sans affecter le système dans son ensemble.</span><span class="sxs-lookup"><span data-stu-id="eb41d-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="eb41d-133">En outre, hello consommation application suffit peut-être toocome en ligne à certaines heures de la journée de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="eb41d-134">**Nivellement de charge.**</span><span class="sxs-lookup"><span data-stu-id="eb41d-134">**Load leveling.**</span></span> <span data-ttu-id="eb41d-135">Dans de nombreuses applications, la charge système varie au fil du temps, alors que le temps de traitement de hello requis pour chaque unité de travail est généralement constant.</span><span class="sxs-lookup"><span data-stu-id="eb41d-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="eb41d-136">Fait message producteurs et consommateurs avec une file d’attente signifie que hello consommation d’application (traitement hello) seuls besoins toobe configuré tooaccommodate les charge moyenne plutôt que des pics de charge.</span><span class="sxs-lookup"><span data-stu-id="eb41d-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="eb41d-137">profondeur Hello de file d’attente hello augmente et diminue comme hello les charge entrante varie.</span><span class="sxs-lookup"><span data-stu-id="eb41d-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="eb41d-138">Cela plus économique en termes de quantité hello de charge de l’application hello infrastructure tooservice requis.</span><span class="sxs-lookup"><span data-stu-id="eb41d-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="eb41d-139">**Équilibrage de la charge.**</span><span class="sxs-lookup"><span data-stu-id="eb41d-139">**Load balancing.**</span></span> <span data-ttu-id="eb41d-140">Quand la charge augmente, plus de processus de travail peuvent être ajoutés tooread à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="eb41d-141">Chaque message est traité par un seul hello de processus de travail.</span><span class="sxs-lookup"><span data-stu-id="eb41d-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="eb41d-142">En outre, cette extraction d’équilibrage de charge permet une utilisation optimale des ordinateurs de travail hello même si les ordinateurs de travail diffèrent en termes de puissance de traitement, car ils extrairont les messages à leur propre taux maximal.</span><span class="sxs-lookup"><span data-stu-id="eb41d-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="eb41d-143">Ce modèle est appelé souvent hello *consommateur concurrent* modèle.</span><span class="sxs-lookup"><span data-stu-id="eb41d-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="eb41d-144">Hello les sections suivantes traite de code hello qui implémente cette architecture.</span><span class="sxs-lookup"><span data-stu-id="eb41d-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="eb41d-145">Configuration d’environnement de développement hello</span><span class="sxs-lookup"><span data-stu-id="eb41d-145">Set up hello development environment</span></span>
<span data-ttu-id="eb41d-146">Avant de commencer à développer des applications Azure, obtenez les outils hello et configurer votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="eb41d-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="eb41d-147">Installer hello Azure SDK pour .NET à partir de hello SDK [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="eb41d-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="eb41d-148">Bonjour **.NET** colonne, cliquez sur la version de hello de [Visual Studio](http://www.visualstudio.com) que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="eb41d-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="eb41d-149">Hello étapes dans ce didacticiel, utilisez Visual Studio 2015, mais ils fonctionnent également avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="eb41d-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="eb41d-150">Lorsque vous y êtes invité toorun ou enregistrer le programme d’installation Bonjour, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="eb41d-151">Bonjour **Web Platform Installer**, cliquez sur **installer** et poursuivre l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="eb41d-152">Une fois l’installation de hello est terminée, vous devez tous les éléments nécessaires toostart toodevelop hello application.</span><span class="sxs-lookup"><span data-stu-id="eb41d-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="eb41d-153">Hello SDK inclut des outils qui vous permettent de développer facilement des applications Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb41d-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="eb41d-154">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="eb41d-154">Create a namespace</span></span>
<span data-ttu-id="eb41d-155">étape suivante de Hello est toocreate un espace de noms de service et obtenir une clé de Signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="eb41d-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="eb41d-156">Un espace de noms fournit une limite d’application pour chaque application exposée via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eb41d-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="eb41d-157">Une clé SAS est générée par le système de hello lors de la création d’un espace de noms.</span><span class="sxs-lookup"><span data-stu-id="eb41d-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="eb41d-158">combinaison de Hello d’espace de noms et la clé SAP fournit des informations d’identification de hello pour l’application de Service Bus tooauthenticate access tooan.</span><span class="sxs-lookup"><span data-stu-id="eb41d-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="eb41d-159">Création d'un rôle web</span><span class="sxs-lookup"><span data-stu-id="eb41d-159">Create a web role</span></span>
<span data-ttu-id="eb41d-160">Dans cette section, vous générez des serveurs frontaux hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="eb41d-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="eb41d-161">Tout d’abord, vous créez des pages de hello par votre application.</span><span class="sxs-lookup"><span data-stu-id="eb41d-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="eb41d-162">Après cela, ajoutez le code qui soumet la file d’attente du Service Bus éléments tooa et affiche les informations d’état de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="eb41d-163">Créer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="eb41d-163">Create hello project</span></span>
1. <span data-ttu-id="eb41d-164">À l’aide des privilèges d’administrateur, démarrez Visual Studio : avec le bouton hello **Visual Studio** icône du programme, puis cliquez sur **exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="eb41d-165">émulateur de calcul Azure Hello, présenté plus loin dans cet article, nécessite que Visual Studio est démarré avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="eb41d-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="eb41d-166">Dans Visual Studio, sur hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="eb41d-167">Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Cloud**, puis sur **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="eb41d-168">Projet de hello nom **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="eb41d-169">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="eb41d-170">Dans les rôles **.NET Framework 4.5**, double-cliquez sur **Rôle Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="eb41d-171">Placez le curseur sur **WebRole1** sous **solution Azure Cloud Service**, sur l’icône de crayon hello et renommer le rôle web de hello trop**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="eb41d-172">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-172">Then click **OK**.</span></span> <span data-ttu-id="eb41d-173">(Entrez bien « Frontend » avec un « e » minuscule, et non « FrontEnd ».)</span><span class="sxs-lookup"><span data-stu-id="eb41d-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="eb41d-174">À partir de hello **nouveau projet ASP.NET** la boîte de dialogue hello **sélectionner un modèle** , cliquez sur **MVC**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="eb41d-175">Toujours en hello **nouveau projet ASP.NET** boîte de dialogue, cliquez sur hello **modifier l’authentification** bouton.</span><span class="sxs-lookup"><span data-stu-id="eb41d-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="eb41d-176">Bonjour **modifier l’authentification** boîte de dialogue, cliquez sur **aucune authentification**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="eb41d-177">Pour ce didacticiel, vous déployez une application qui n’a pas besoin de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb41d-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="eb41d-178">Dans hello **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="eb41d-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="eb41d-179">Dans **l’Explorateur de solutions**, Bonjour **FrontendWebRole** de projet, cliquez sur **références**, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="eb41d-180">Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="eb41d-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="eb41d-181">Sélectionnez hello **WindowsAzure.ServiceBus** du package, cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="eb41d-182">Notez que hello requis assemblys clients sont désormais référencés et des nouveaux fichiers de code ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="eb41d-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="eb41d-183">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Modèles** et cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="eb41d-184">Bonjour **nom** zone, entrez un nom hello **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="eb41d-185">Cliquez ensuite sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="eb41d-186">Écrire du code hello pour votre rôle web</span><span class="sxs-lookup"><span data-stu-id="eb41d-186">Write hello code for your web role</span></span>
<span data-ttu-id="eb41d-187">Dans cette section, vous créez hello différentes pages que votre application affiche.</span><span class="sxs-lookup"><span data-stu-id="eb41d-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="eb41d-188">Dans le fichier de OnlineOrder.cs hello dans Visual Studio, remplacez la définition de l’espace de noms existant hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="eb41d-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="eb41d-189">Dans l’**Explorateur de solutions**, double-cliquez sur **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="eb41d-190">Ajoutez hello suivant **à l’aide de** instructions haut hello hello tooinclude hello espaces de noms pour le modèle que vous venez de créer, ainsi que le Bus des services de fichiers.</span><span class="sxs-lookup"><span data-stu-id="eb41d-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="eb41d-191">Également dans le fichier HomeController.cs de hello dans Visual Studio, remplacez la définition de l’espace de noms existant hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="eb41d-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="eb41d-192">Ce code contient des méthodes de gestion de soumission hello de file d’attente de toohello éléments.</span><span class="sxs-lookup"><span data-stu-id="eb41d-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="eb41d-193">À partir de hello **générer** menu, cliquez sur **générer la Solution** précision de hello tootest de votre travail jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="eb41d-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="eb41d-194">Maintenant, créez la vue hello pour hello `Submit()` méthode que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="eb41d-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="eb41d-195">Avec le bouton droit dans hello `Submit()` (méthode) (surcharge hello de `Submit()` qui ne prend aucun paramètre), puis choisissez **ajouter une vue**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="eb41d-196">Une boîte de dialogue s’affiche pour la création de vue de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="eb41d-197">Bonjour **modèle** , choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="eb41d-198">Bonjour **classe de modèle** , cliquez sur hello **OnlineOrder** classe.</span><span class="sxs-lookup"><span data-stu-id="eb41d-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="eb41d-199">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-199">Click **Add**.</span></span>
8. <span data-ttu-id="eb41d-200">Maintenant, hello de modification affiche le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="eb41d-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="eb41d-201">Dans **l’Explorateur de solutions**, double-cliquez sur le **Views\Shared\\_Layout.cshtml** tooopen de fichiers dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="eb41d-202">Remplacez toutes les occurrences de **Mon application ASP.NET** par **LITWARE’S Products**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="eb41d-203">Supprimer hello **accueil**, **sur**, et **Contact** des liens.</span><span class="sxs-lookup"><span data-stu-id="eb41d-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="eb41d-204">Supprimer le code de hello mis en surbrillance :</span><span class="sxs-lookup"><span data-stu-id="eb41d-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="eb41d-205">Enfin, modifiez hello présentation page tooinclude des informations sur la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="eb41d-206">Dans **l’Explorateur de solutions**, double-cliquez sur le **Views\Home\Submit.cshtml** tooopen de fichiers dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="eb41d-207">Ajouter hello ligne après `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="eb41d-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="eb41d-208">Pour l’instant, hello `ViewBag.MessageCount` est vide.</span><span class="sxs-lookup"><span data-stu-id="eb41d-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="eb41d-209">Vous le remplirez plus tard.</span><span class="sxs-lookup"><span data-stu-id="eb41d-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="eb41d-210">Vous avez maintenant implémenté votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb41d-210">You now have implemented your UI.</span></span> <span data-ttu-id="eb41d-211">Vous pouvez appuyer sur **F5** toorun votre application et vérifiez qu’elle s’affiche comme prévu.</span><span class="sxs-lookup"><span data-stu-id="eb41d-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="eb41d-212">Écrire du code hello pour l’envoi de file d’attente du Service Bus éléments tooa</span><span class="sxs-lookup"><span data-stu-id="eb41d-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="eb41d-213">Maintenant, ajoutez le code pour l’envoi de file d’attente de tooa éléments.</span><span class="sxs-lookup"><span data-stu-id="eb41d-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="eb41d-214">Tout d’abord, vous créez une classe qui contient les informations de connexion à votre file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eb41d-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="eb41d-215">Ensuite, initialisez votre connexion à partir de Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="eb41d-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="eb41d-216">Enfin, mettre à jour de code de soumission hello que vous avez créé précédemment dans la file d’attente HomeController.cs tooactually submit éléments tooa Service Bus.</span><span class="sxs-lookup"><span data-stu-id="eb41d-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="eb41d-217">Dans **l’Explorateur de solutions**, avec le bouton droit **FrontendWebRole** (projet de hello avec le bouton droit, pas les rôles hello).</span><span class="sxs-lookup"><span data-stu-id="eb41d-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="eb41d-218">Cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="eb41d-219">Nom de classe hello **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="eb41d-220">Cliquez sur **ajouter** classe hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="eb41d-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="eb41d-221">Maintenant, ajoutez le code qui encapsule les informations de connexion hello et initialise la file d’attente du Service Bus tooa connexion hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="eb41d-222">Remplacez hello tout contenu de QueueConnector.cs par hello suivant de code et entrez des valeurs pour `your Service Bus namespace` (votre nom d’espace de noms) et `yourKey`, qui est hello **clé primaire** obtenu à partir de hello Azure portail.</span><span class="sxs-lookup"><span data-stu-id="eb41d-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="eb41d-223">Ensuite, assurez-vous que votre méthode **Initialize** est bien appelée.</span><span class="sxs-lookup"><span data-stu-id="eb41d-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="eb41d-224">Dans l’**Explorateur de solutions**, double-cliquez sur **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="eb41d-225">Ajouter hello suivant la ligne de code à fin hello Hello **Application_Start** (méthode).</span><span class="sxs-lookup"><span data-stu-id="eb41d-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="eb41d-226">Enfin, mettre à jour de code hello du web vous avez créé précédemment, pour soumettre les éléments toohello file.</span><span class="sxs-lookup"><span data-stu-id="eb41d-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="eb41d-227">Dans l’**Explorateur de solutions**, double-cliquez sur **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="eb41d-228">Hello de mise à jour `Submit()` (méthode) (surcharge hello qui ne prend aucun paramètre) comme suit tooget hello nombre de messages pour la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="eb41d-229">Hello de mise à jour `Submit(OnlineOrder order)` (méthode) (surcharge hello qui prend un paramètre) comme suit toosubmit commande file d’attente de toohello plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="eb41d-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="eb41d-230">Vous pouvez maintenant exécuter des application hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-230">You can now run hello application again.</span></span> <span data-ttu-id="eb41d-231">Chaque fois que vous soumettez une commande, nombre de messages hello augmente.</span><span class="sxs-lookup"><span data-stu-id="eb41d-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="eb41d-232">Créer le rôle de travail hello</span><span class="sxs-lookup"><span data-stu-id="eb41d-232">Create hello worker role</span></span>
<span data-ttu-id="eb41d-233">Vous allez maintenant créer rôle de travail hello qui traite les envois d’ordre hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="eb41d-234">Cet exemple utilise hello **rôle de travail avec file d’attente du Bus de Service** modèle de projet Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eb41d-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="eb41d-235">Vous avez déjà obtenu des informations d’identification hello requis à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="eb41d-236">Assurez-vous que vous êtes connecté à Visual Studio tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="eb41d-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="eb41d-237">Dans Visual Studio, dans **l’Explorateur de solutions** avec le bouton droit le **rôles** dossier sous hello **MultiTierApp** projet.</span><span class="sxs-lookup"><span data-stu-id="eb41d-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="eb41d-238">Cliquez sur **Ajouter**, puis sur **Nouveau projet de rôle de travail**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="eb41d-239">Hello **ajouter un nouveau projet de rôle** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="eb41d-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="eb41d-240">Bonjour **ajouter un nouveau projet de rôle** boîte de dialogue, cliquez sur **rôle de travail avec file d’attente du Bus de Service**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="eb41d-241">Bonjour **nom** boîte, projet de hello nom **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="eb41d-242">Cliquez ensuite sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-242">Then click **Add**.</span></span>
6. <span data-ttu-id="eb41d-243">Copier la chaîne de connexion hello que vous avez obtenue à l’étape 9 de Presse-papiers de toohello section hello « Créer un espace de noms Service Bus ».</span><span class="sxs-lookup"><span data-stu-id="eb41d-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="eb41d-244">Dans **l’Explorateur de solutions**, avec le bouton hello **OrderProcessingRole** créé à l’étape 5 (Assurez-vous que vous cliquez sur **OrderProcessingRole** sous **Rôles**, et pas hello classe).</span><span class="sxs-lookup"><span data-stu-id="eb41d-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="eb41d-245">Cliquez ensuite sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="eb41d-246">Sur hello **paramètres** onglet Hello **propriétés** boîte de dialogue, cliquez à l’intérieur de hello **valeur** boîte pour **Microsoft.ServiceBus.ConnectionString**, puis collez la valeur de point de terminaison hello copiée à l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="eb41d-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="eb41d-247">Créer un **OnlineOrder** classe toorepresent hello orders, comme les traiter à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="eb41d-248">Vous pouvez réutiliser une classe que vous avez déjà créée.</span><span class="sxs-lookup"><span data-stu-id="eb41d-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="eb41d-249">Dans **l’Explorateur de solutions**, avec le bouton hello **OrderProcessingRole** (icône avec le bouton droit de la classe de hello, pas les rôles hello) de classe.</span><span class="sxs-lookup"><span data-stu-id="eb41d-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="eb41d-250">Cliquez sur **Ajouter**, puis sur **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="eb41d-251">Recherchez le sous-dossier toohello pour **FrontendWebRole\Models**, puis double-cliquez sur **OnlineOrder.cs** tooadd il toothis projet.</span><span class="sxs-lookup"><span data-stu-id="eb41d-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="eb41d-252">Dans **WorkerRole.cs**, modifiez la valeur hello hello **QueueName** variable à partir de `"ProcessingQueue"` trop`"OrdersQueue"` comme indiqué dans hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="eb41d-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="eb41d-253">Ajoutez hello qui suit à l’aide d’instruction haut hello du fichier WorkerRole.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="eb41d-254">Bonjour `Run()` fonction, à l’intérieur de hello `OnMessage()` appeler, remplacez le contenu hello Hello `try` clause avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="eb41d-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="eb41d-255">Vous avez terminé l’application hello.</span><span class="sxs-lookup"><span data-stu-id="eb41d-255">You have completed hello application.</span></span> <span data-ttu-id="eb41d-256">Vous pouvez tester l’application complète hello en double-cliquant sur le projet de MultiTierApp hello dans l’Explorateur de solutions, en sélectionnant **définir comme projet de démarrage**, puis en appuyant sur F5.</span><span class="sxs-lookup"><span data-stu-id="eb41d-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="eb41d-257">Notez que le nombre de messages n’augmente pas, car le rôle de travail hello traite les éléments à partir de la file d’attente hello et les marque comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="eb41d-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="eb41d-258">Vous pouvez voir la sortie de trace hello de votre rôle de travail en consultant hello Azure Compute Emulator UI.</span><span class="sxs-lookup"><span data-stu-id="eb41d-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="eb41d-259">Cela en icône hello émulateur dans la zone de notification hello de votre barre des tâches et en sélectionnant **Show Compute Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="eb41d-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="eb41d-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb41d-260">Next steps</span></span>
<span data-ttu-id="eb41d-261">toolearn en savoir plus sur le Bus des services, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="eb41d-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="eb41d-262">[Documentation Azure Service Bus][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="eb41d-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="eb41d-263">[Page du service Service Bus][sbacom]</span><span class="sxs-lookup"><span data-stu-id="eb41d-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="eb41d-264">[Comment tooUse files d’attente du Bus de Service][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="eb41d-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="eb41d-265">toolearn en savoir plus sur les scénarios à plusieurs niveaux, consultez :</span><span class="sxs-lookup"><span data-stu-id="eb41d-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="eb41d-266">[Application multiniveau .NET avec tables, files d’attente et objets blob de stockage][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="eb41d-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
