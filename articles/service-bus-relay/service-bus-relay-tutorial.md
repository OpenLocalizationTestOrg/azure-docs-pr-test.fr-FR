---
title: didacticiel de Service Bus Relay WCF aaaAzure | Documents Microsoft
description: "Créez une application cliente et un service Service Bus à l’aide de WCF Relay."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="4a272-103">Didacticiel Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="4a272-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="4a272-104">Ce didacticiel décrit comment toobuild relayer un service WCF simple application cliente et le service à l’aide de relais d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4a272-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="4a272-105">Pour obtenir un didacticiel similaire utilisant la [messagerie Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consultez [Bien démarrer avec les files d’attente Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="4a272-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="4a272-106">Ce didacticiel vous donne une présentation des étapes hello toocreate requis une application client et le service de relais de WCF.</span><span class="sxs-lookup"><span data-stu-id="4a272-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="4a272-107">À l’instar de leurs homologues WCF d’origine, un service est une construction qui expose un ou plusieurs points de terminaison, chacun d’entre eux exposant une ou plusieurs opérations de service.</span><span class="sxs-lookup"><span data-stu-id="4a272-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="4a272-108">point de terminaison Hello d’un service spécifie une adresse où le service de hello peut être trouvé, une liaison qui contient des informations de hello qu’un client doit communiquer avec le service hello et un contrat qui définit les fonctionnalités de hello fournies par les clients du service tooits hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="4a272-109">Hello principale différence entre WCF et WCF relais est que ce point de terminaison hello est exposé dans le cloud hello et non localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4a272-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="4a272-110">Une fois que vous travaillez via la séquence hello de rubriques dans ce didacticiel, vous devez un service en cours d’exécution et un client qui peut appeler des opérations du service de hello hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="4a272-111">Hello première rubrique Comment tooset un compte.</span><span class="sxs-lookup"><span data-stu-id="4a272-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="4a272-112">les étapes suivantes Hello décrivent comment toodefine un service qui utilise un contrat, comment tooimplement hello service, et comment tooconfigure hello service dans le code.</span><span class="sxs-lookup"><span data-stu-id="4a272-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="4a272-113">Elles décrivent également comment toohost et exécuter le service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="4a272-114">Hello service qui est créé est auto-hébergé et hello client et le service exécutent sur hello même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4a272-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="4a272-115">Vous pouvez configurer le service de hello à l’aide de code ou un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="4a272-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="4a272-116">trois étapes finales de Hello décrivent comment toocreate une application cliente, configurez l’application cliente de hello et créer et utiliser un client que vous pouvez accéder aux fonctionnalités hello d’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a272-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4a272-117">Prerequisites</span></span>

<span data-ttu-id="4a272-118">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="4a272-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="4a272-119">[Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="4a272-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="4a272-120">Ce didacticiel utilise Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4a272-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="4a272-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4a272-121">An active Azure account.</span></span> <span data-ttu-id="4a272-122">Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4a272-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="4a272-123">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4a272-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="4a272-124">Création d'un espace de noms de service</span><span class="sxs-lookup"><span data-stu-id="4a272-124">Create a service namespace</span></span>

<span data-ttu-id="4a272-125">première étape de Hello est toocreate un espace de noms et tooobtain un [Signature d’accès partagé (SAS)](../service-bus-messaging/service-bus-sas.md) clé.</span><span class="sxs-lookup"><span data-stu-id="4a272-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="4a272-126">Un espace de noms fournit une limite d’application pour chaque application exposée via le service de relais hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="4a272-127">Une clé SAS est générée automatiquement par le système de hello lors de la création d’un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="4a272-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="4a272-128">combinaison de Hello d’espace de noms de service et la clé SAP fournit des informations d’identification de hello pour l’application de tooan tooauthenticate Azure access.</span><span class="sxs-lookup"><span data-stu-id="4a272-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="4a272-129">Suivez hello [ici les instructions](relay-create-namespace-portal.md) toocreate un espace de noms de relais.</span><span class="sxs-lookup"><span data-stu-id="4a272-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="4a272-130">Définition d’un contrat de service WCF</span><span class="sxs-lookup"><span data-stu-id="4a272-130">Define a WCF service contract</span></span>

<span data-ttu-id="4a272-131">contrat de service Hello spécifie quelles opérations (hello web service la terminologie des méthodes ou des fonctions) hello service prend en charge.</span><span class="sxs-lookup"><span data-stu-id="4a272-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="4a272-132">Les contrats sont créés en définissant une interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="4a272-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="4a272-133">Chaque méthode dans l’interface hello correspond l’opération de service spécifique tooa.</span><span class="sxs-lookup"><span data-stu-id="4a272-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="4a272-134">Chaque interface doit avoir hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribut appliqué tooit, et chaque opération doit avoir hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit de l’attribut est appliqué.</span><span class="sxs-lookup"><span data-stu-id="4a272-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="4a272-135">Si une méthode dans une interface qui possède hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribut n’a pas de hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) d’attribut, cette méthode n’est pas exposée.</span><span class="sxs-lookup"><span data-stu-id="4a272-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="4a272-136">code Hello pour ces tâches est fourni dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="4a272-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="4a272-137">Pour obtenir une présentation plus large des contrats et des services, consultez [conception et implémentation de Services](https://msdn.microsoft.com/library/ms729746.aspx) Bonjour documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="4a272-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="4a272-138">Création d’un contrat de relais avec une interface</span><span class="sxs-lookup"><span data-stu-id="4a272-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="4a272-139">Ouvrez Visual Studio en tant qu’administrateur en cliquant sur le programme hello Bonjour **Démarrer** menu et en sélectionnant **exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4a272-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="4a272-140">Créez un projet d’application de console.</span><span class="sxs-lookup"><span data-stu-id="4a272-140">Create a new console application project.</span></span> <span data-ttu-id="4a272-141">Cliquez sur hello **fichier** menu et sélectionnez **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="4a272-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="4a272-142">Bonjour **nouveau projet** boîte de dialogue, cliquez sur **Visual C#** (si **Visual C#** n’apparaît pas, regardez sous **autres langages**).</span><span class="sxs-lookup"><span data-stu-id="4a272-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="4a272-143">Cliquez sur hello **l’application Console (.NET Framework)** modèle et nommez-le **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="4a272-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="4a272-144">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="4a272-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="4a272-145">Installez le package NuGet Service Bus de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="4a272-146">Ce package ajoute automatiquement des références toohello Service Bus bibliothèques, ainsi que hello WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="4a272-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="4a272-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) est l’espace de noms hello qui vous permet de tooprogrammatically accès hello fonctionnalités de base de WCF.</span><span class="sxs-lookup"><span data-stu-id="4a272-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="4a272-148">Service Bus utilise de nombreux hello objets et attributs WCF toodefine de contrats de service.</span><span class="sxs-lookup"><span data-stu-id="4a272-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="4a272-149">Dans l’Explorateur de solutions, cliquez sur le projet de hello, puis cliquez sur **gérer les Packages NuGet...** . Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="4a272-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="4a272-150">Vérifiez que nom du projet hello est sélectionné dans hello **versions** boîte.</span><span class="sxs-lookup"><span data-stu-id="4a272-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="4a272-151">Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="4a272-152">Dans l’Explorateur de solutions, double-cliquez sur tooopen de fichier Program.cs hello il dans l’éditeur de hello, s’il n’est pas déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="4a272-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="4a272-153">Ajoutez hello qui suit à l’aide d’instructions haut hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="4a272-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="4a272-154">Nom d’espace de noms hello modification de son nom par défaut de **EchoService** trop**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="4a272-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4a272-155">Ce didacticiel utilise l’espace de noms hello c# **Microsoft.ServiceBus.Samples**, qui est l’espace de noms hello Hello basé sur le contrat de type est utilisé dans le fichier de configuration hello Bonjour managé [configurer le client WCF hello](#configure-the-wcf-client) étape.</span><span class="sxs-lookup"><span data-stu-id="4a272-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="4a272-156">Vous pouvez spécifier n’importe quel espace de noms lorsque vous générez cet exemple ; Toutefois, didacticiel de hello ne fonctionnera pas, sauf si vous modifiez hello des espaces de noms de contrat de hello et le service en conséquence, dans le fichier de configuration d’application hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="4a272-157">espace de noms Hello spécifié dans hello App.config fichier doit être même hello comme espace de noms hello spécifié dans vos fichiers c#.</span><span class="sxs-lookup"><span data-stu-id="4a272-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="4a272-158">Directement après hello `Microsoft.ServiceBus.Samples` déclaration d’espace de noms, mais dans l’espace de noms hello, définir une nouvelle interface nommée `IEchoContract` et appliquer hello `ServiceContractAttribute` interface de toohello d’attribut avec une valeur de l’espace de noms de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="4a272-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="4a272-159">valeur d’espace de noms Hello diffère de l’espace de noms hello que vous utilisez dans la portée de votre code hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="4a272-160">Au lieu de cela, la valeur d’espace de noms hello est utilisé comme identificateur unique pour ce contrat.</span><span class="sxs-lookup"><span data-stu-id="4a272-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="4a272-161">Une spécification explicite de l’espace de noms hello empêche l’espace de noms par défaut hello Ajout toohello le nom de contrat.</span><span class="sxs-lookup"><span data-stu-id="4a272-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="4a272-162">Collez hello après le code après la déclaration d’espace de noms hello :</span><span class="sxs-lookup"><span data-stu-id="4a272-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="4a272-163">En général, les noms de contrat de service hello contient un schéma d’affectation de noms qui inclut des informations de version.</span><span class="sxs-lookup"><span data-stu-id="4a272-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="4a272-164">Y compris les informations de version dans les noms de contrat de service hello permet des principales modifications apportées aux services tooisolate en définissant un nouveau contrat de service avec un espace de noms et d’exposer sur un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4a272-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="4a272-165">De cette manière, les clients peuvent continuer toouse hello ancien contrat de service sans avoir toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4a272-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="4a272-166">Les informations de version peuvent se composer d’une date ou un numéro de version.</span><span class="sxs-lookup"><span data-stu-id="4a272-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="4a272-167">Pour plus d’informations, consultez la rubrique [Contrôle de version des services](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="4a272-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="4a272-168">Pour des raisons de hello de ce didacticiel, hello jeu de noms de contrat de service hello d’affectation de noms ne contient pas d’informations de version.</span><span class="sxs-lookup"><span data-stu-id="4a272-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="4a272-169">Au sein de hello `IEchoContract` l’interface, déclarez une méthode pour hello d’opération unique hello `IEchoContract` expose contrat Bonjour interface et appliquez hello `OperationContractAttribute` attribut toohello méthode tooexpose dans le cadre de hello relais WCF public contrat, comme suit :</span><span class="sxs-lookup"><span data-stu-id="4a272-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="4a272-170">Directement après hello `IEchoContract` définition d’interface, déclarez un canal qui hérite à la fois `IEchoContract` et également toohello `IClientChannel` de l’interface, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="4a272-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="4a272-171">Un canal est l’objet WCF de hello via lequel clients et hôtes de hello transmettent informations tooeach autres.</span><span class="sxs-lookup"><span data-stu-id="4a272-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="4a272-172">Une version ultérieure, vous écrirez du code par rapport aux informations de tooecho hello canal entre deux applications de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="4a272-173">À partir de hello **générer** menu, cliquez sur **générer la Solution** ou appuyez sur **Ctrl + Maj + B** précision de hello tooconfirm de votre travail jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="4a272-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="4a272-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="4a272-174">Example</span></span>

<span data-ttu-id="4a272-175">Hello suivant de code montre une interface de base qui définit un contrat WCF relais.</span><span class="sxs-lookup"><span data-stu-id="4a272-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="4a272-176">Maintenant que hello interface est créée, vous pouvez implémenter l’interface de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="4a272-177">Contrat de mettre en œuvre hello WCF</span><span class="sxs-lookup"><span data-stu-id="4a272-177">Implement hello WCF contract</span></span>

<span data-ttu-id="4a272-178">Création d’un relais Azure nécessite que vous créez tout d’abord le contrat hello, qui est défini à l’aide d’une interface.</span><span class="sxs-lookup"><span data-stu-id="4a272-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="4a272-179">Pour plus d’informations sur la création d’interface de hello, reportez-vous à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="4a272-180">étape suivante de Hello est interface de hello tooimplement.</span><span class="sxs-lookup"><span data-stu-id="4a272-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="4a272-181">Cela implique la création d’une classe nommée `EchoService` qui implémente hello défini par l’utilisateur `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="4a272-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="4a272-182">Une fois que vous implémentez hello interface, vous configurez interface hello à l’aide d’un fichier de configuration App.config.</span><span class="sxs-lookup"><span data-stu-id="4a272-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="4a272-183">fichier de configuration Hello contient les informations nécessaires pour l’application hello, telles que nom hello du service de hello, nom hello du contrat de hello et type hello du protocole est toocommunicate utilisé avec le service de relais hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="4a272-184">code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="4a272-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="4a272-185">Pour une description plus générale comment tooimplement un service de contrat, consultez [implémentation de contrats de Service](https://msdn.microsoft.com/library/ms733764.aspx) Bonjour documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="4a272-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="4a272-186">Créer une nouvelle classe nommée `EchoService` directement après la définition de hello Hello `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="4a272-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="4a272-187">Hello `EchoService` classe implémente hello `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="4a272-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="4a272-188">Implémentations d’interface tooother similaires, vous pouvez implémenter la définition de hello dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="4a272-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="4a272-189">Toutefois, pour ce didacticiel, hello se trouve dans le même fichier de définition d’interface hello et hello de hello `Main` (méthode).</span><span class="sxs-lookup"><span data-stu-id="4a272-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="4a272-190">Appliquer hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribut toohello `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="4a272-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="4a272-191">attribut de Hello Spécifie l’espace de noms et le nom du service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="4a272-192">Après cela, hello `EchoService` classe se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="4a272-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="4a272-193">Hello d’implémenter `Echo` méthode définie dans hello `IEchoContract` interface Bonjour `EchoService` classe.</span><span class="sxs-lookup"><span data-stu-id="4a272-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="4a272-194">Cliquez sur **générer**, puis cliquez sur **générer la Solution** précision de hello tooconfirm de votre travail.</span><span class="sxs-lookup"><span data-stu-id="4a272-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="4a272-195">Définir la configuration de hello pour l’hôte de service hello</span><span class="sxs-lookup"><span data-stu-id="4a272-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="4a272-196">fichier de configuration Hello est un fichier de configuration WCF tooa très similaire.</span><span class="sxs-lookup"><span data-stu-id="4a272-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="4a272-197">Il inclut le nom du service hello, point de terminaison (autrement dit, la location de hello qui expose des relais de Azure pour les clients et les hôtes toocommunicate entre eux) et hello liaison (type hello du protocole qui est utilisé toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="4a272-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="4a272-198">Hello principale différence est que ce point de terminaison de service configuré fait référence tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) liaison, ce qui ne fait pas partie de hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4a272-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="4a272-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) est une des liaisons de hello définies par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="4a272-200">Dans **l’Explorateur de solutions**, double-cliquez sur tooopen de fichier App.config hello dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="4a272-201">Bonjour `<appSettings>` élément, remplacez les espaces réservés de hello par nom de hello de votre espace de noms de service et hello clé SAP que vous avez copié dans une étape antérieure.</span><span class="sxs-lookup"><span data-stu-id="4a272-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="4a272-202">Au sein de hello `<system.serviceModel>` balises, ajoutez un `<services>` élément.</span><span class="sxs-lookup"><span data-stu-id="4a272-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="4a272-203">Vous pouvez définir plusieurs applications de relais dans un même fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="4a272-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="4a272-204">Toutefois, ce didacticiel n’en définit qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="4a272-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="4a272-205">Au sein de hello `<services>` élément, ajouter un `<service>` nom_élément toodefine hello du service de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="4a272-206">Au sein de hello `<service>` élément, définir l’emplacement hello de contrat de point de terminaison hello et également hello type de liaison pour le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="4a272-207">point de terminaison Hello définit où les clients hello recherche hello hôte application.</span><span class="sxs-lookup"><span data-stu-id="4a272-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="4a272-208">Plus tard, le didacticiel de hello utilise cette toocreate étape un URI qui expose entièrement hôte hello via Azure relais.</span><span class="sxs-lookup"><span data-stu-id="4a272-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="4a272-209">liaison de Hello déclare que nous utilisons comme hello toocommunicate protocole avec le service de relais hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="4a272-210">À partir de hello **générer** menu, cliquez sur **générer la Solution** précision de hello tooconfirm de votre travail.</span><span class="sxs-lookup"><span data-stu-id="4a272-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="4a272-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="4a272-211">Example</span></span>

<span data-ttu-id="4a272-212">Hello de code suivant illustre implémentation hello hello du contrat de service.</span><span class="sxs-lookup"><span data-stu-id="4a272-212">hello following code shows hello implementation of hello service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="4a272-213">Hello de code suivant montre hello de base format de fichier App.config hello avec hôte de service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="4a272-214">Héberger et exécuter un tooregister de service web de base avec le service de relais hello</span><span class="sxs-lookup"><span data-stu-id="4a272-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="4a272-215">Cette étape décrit comment toorun Azure relais service.</span><span class="sxs-lookup"><span data-stu-id="4a272-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="4a272-216">Créer des informations d’identification de relais hello</span><span class="sxs-lookup"><span data-stu-id="4a272-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="4a272-217">Dans `Main()`, créez deux variables dans l’espace de noms toostore hello et hello clé SAP qui sont lus à partir de la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="4a272-218">la clé SAS Hello sera utilisé tooaccess ultérieure de votre projet.</span><span class="sxs-lookup"><span data-stu-id="4a272-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="4a272-219">espace de noms Hello est passé en tant que paramètre trop`CreateServiceUri` toocreate un URI de service.</span><span class="sxs-lookup"><span data-stu-id="4a272-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="4a272-220">À l’aide un [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) d’objet, déclarez que vous utiliserez une clé SAP en tant que type d’informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="4a272-221">Ajoutez hello après le code directement après le code hello ajoutée dans la dernière étape de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="4a272-222">Créer une adresse de base pour le service de hello</span><span class="sxs-lookup"><span data-stu-id="4a272-222">Create a base address for hello service</span></span>

<span data-ttu-id="4a272-223">Après le code hello ajouté dans la dernière étape de hello, créer un `Uri` instance hello adresse de base du service de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="4a272-224">Cet URI Spécifie le modèle de Service Bus hello, espace de noms hello et un chemin d’accès de hello d’interface de service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="4a272-225">« sb » est une abréviation pour le schéma de Service Bus hello et indique que nous utilisons TCP comme protocole de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="4a272-226">Cela était aussi indiqué précédemment dans le fichier de configuration hello lorsque [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) a été spécifié en tant que liaison de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="4a272-227">Pour ce didacticiel, hello URI est `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="4a272-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="4a272-228">Créer et configurer l’hôte de service hello</span><span class="sxs-lookup"><span data-stu-id="4a272-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="4a272-229">Définir le mode de connectivité hello trop`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="4a272-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="4a272-230">mode de connectivité Hello décrit hello protocole hello service utilise toocommunicate avec le service de relais hello ; HTTP ou TCP.</span><span class="sxs-lookup"><span data-stu-id="4a272-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="4a272-231">À l’aide du paramètre par défaut de hello `AutoDetect`, service de hello tente tooconnect tooAzure relais via HTTP, TCP, si elle est disponible et si TCP n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="4a272-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="4a272-232">Notez que cela diffère de service du protocole de hello hello spécifie pour la communication client.</span><span class="sxs-lookup"><span data-stu-id="4a272-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="4a272-233">Ce protocole est déterminé par la liaison hello utilisée.</span><span class="sxs-lookup"><span data-stu-id="4a272-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="4a272-234">Par exemple, un service peut utiliser hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) liaison, ce qui indique que son point de terminaison communique avec les clients via HTTP.</span><span class="sxs-lookup"><span data-stu-id="4a272-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="4a272-235">Que le même service pourrait spécifier **ConnectivityMode.AutoDetect** afin que le service de hello communique avec Azure relais sur TCP.</span><span class="sxs-lookup"><span data-stu-id="4a272-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="4a272-236">Créer un hôte de service hello, à l’aide de hello QU'URI créé précédemment dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4a272-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="4a272-237">hôte de service Hello est un objet hello WCF qui instancie le service de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="4a272-238">Ici, vous lui passez le type de hello du service, vous souhaitez toocreate (un `EchoService` type) et également les adresses toohello auquel vous souhaitez que le service de hello tooexpose.</span><span class="sxs-lookup"><span data-stu-id="4a272-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="4a272-239">Haut hello du fichier Program.cs de hello, ajoutez des références trop[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) et [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="4a272-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="4a272-240">Dans `Main()`, configurer le point de terminaison hello tooenable un accès public.</span><span class="sxs-lookup"><span data-stu-id="4a272-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="4a272-241">Cette étape informe service de relais hello que votre application peut être trouvée publiquement en examinant le flux ATOM de hello pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="4a272-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="4a272-242">Si vous définissez **DiscoveryType** trop**privé**, un client sera toujours les service de hello en mesure de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="4a272-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="4a272-243">Toutefois, les service hello apparaîtrait pas lorsqu’il recherche l’espace de noms de relais hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="4a272-244">Au lieu de cela, les clients hello aurait le chemin d’accès au point de terminaison tooknow hello au préalable.</span><span class="sxs-lookup"><span data-stu-id="4a272-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="4a272-245">Appliquer les service hello toohello points de terminaison de service définis dans le fichier App.config hello les informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="4a272-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="4a272-246">Comme indiqué dans l’étape précédente de hello, vous pouvez avoir déclaré plusieurs services et les points de terminaison dans le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="4a272-247">Si vous aviez, ce code traversent fichier de configuration hello et de recherche pour chaque point de terminaison toowhich, il doit s’appliquer à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4a272-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="4a272-248">Toutefois, pour ce didacticiel, fichier de configuration hello a uniquement un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4a272-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="4a272-249">Hôte de service hello ouvert</span><span class="sxs-lookup"><span data-stu-id="4a272-249">Open hello service host</span></span>

1. <span data-ttu-id="4a272-250">Ouvrez hello service.</span><span class="sxs-lookup"><span data-stu-id="4a272-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="4a272-251">Informer l’utilisateur hello hello service est en cours d’exécution et expliquez comment tooshut service de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="4a272-252">Lorsque vous avez terminé, fermez l’hôte de service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="4a272-253">Appuyez sur **Ctrl + Maj + B** projet hello de toobuild.</span><span class="sxs-lookup"><span data-stu-id="4a272-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="4a272-254">Exemple</span><span class="sxs-lookup"><span data-stu-id="4a272-254">Example</span></span>

<span data-ttu-id="4a272-255">Une fois terminé, votre code de service doit se présenter ainsi.</span><span class="sxs-lookup"><span data-stu-id="4a272-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="4a272-256">code de Hello inclut contrat de service hello et l’implémentation des étapes précédentes dans le didacticiel de hello et hôtes hello service dans une application console.</span><span class="sxs-lookup"><span data-stu-id="4a272-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="4a272-257">Créer un client WCF hello contrat de service</span><span class="sxs-lookup"><span data-stu-id="4a272-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="4a272-258">étape suivante de Hello est toocreate une application cliente et définir le contrat de service hello vous allez implémenter dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4a272-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="4a272-259">Notez que plusieurs de ces étapes ressemblent aux étapes de hello utilisées toocreate un service : définition d’un contrat, la modification d’un fichier App.config de fichiers, à l’aide du service de relais tooconnect toohello informations d’identification et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4a272-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="4a272-260">code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="4a272-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="4a272-261">Créez un projet dans la solution Visual Studio actuelle de hello pour les clients hello de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="4a272-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="4a272-262">Dans l’Explorateur de solutions, dans hello même solution qui contient le service de hello, cliquez sur la solution actuelle de hello (pas le projet hello), puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4a272-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="4a272-263">Puis cliquez sur **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="4a272-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="4a272-264">Bonjour **ajouter un nouveau projet** boîte de dialogue, cliquez sur **Visual C#** (si **Visual C#** n’apparaît pas, regardez sous **autres langages**), sélectionnez hello **L’application console (.NET Framework)** modèle et nommez-le **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4a272-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="4a272-265">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a272-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="4a272-266">Dans l’Explorateur de solutions, double-cliquez sur le fichier Program.cs hello hello **EchoClient** tooopen dans l’éditeur hello, s’il n’est pas déjà ouvrir de projet.</span><span class="sxs-lookup"><span data-stu-id="4a272-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="4a272-267">Nom d’espace de noms hello modification de son nom par défaut de `EchoClient` trop`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="4a272-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="4a272-268">Installer hello [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): dans l’Explorateur de solutions, cliquez sur hello **EchoClient** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4a272-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="4a272-269">Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="4a272-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="4a272-270">Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="4a272-271">Ajouter un `using` instruction pour hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) espace de noms dans le fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="4a272-272">Ajouter des noms de toohello de définition de contrat de service de hello, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4a272-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="4a272-273">Notez que cette définition est identique toohello utilisé Bonjour **Service** projet.</span><span class="sxs-lookup"><span data-stu-id="4a272-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="4a272-274">Vous devez ajouter ce code en haut de hello Hello `Microsoft.ServiceBus.Samples` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="4a272-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="4a272-275">Appuyez sur **Ctrl + Maj + B** client de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="4a272-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="4a272-276">Exemple</span><span class="sxs-lookup"><span data-stu-id="4a272-276">Example</span></span>

<span data-ttu-id="4a272-277">Hello de code suivant affiche hello état actuel du fichier Program.cs de hello Bonjour **EchoClient** projet.</span><span class="sxs-lookup"><span data-stu-id="4a272-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="4a272-278">Configurer le client WCF de hello</span><span class="sxs-lookup"><span data-stu-id="4a272-278">Configure hello WCF client</span></span>

<span data-ttu-id="4a272-279">Dans cette étape, vous créez un fichier App.config pour une application cliente de base qui accède au service hello créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4a272-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="4a272-280">Ce fichier App.config définit le nom du point de terminaison hello, liaison et contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="4a272-281">code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="4a272-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="4a272-282">Dans l’Explorateur de solutions, Bonjour **EchoClient** de projet, double-cliquez sur **App.config** fichier hello de tooopen dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="4a272-283">Bonjour `<appSettings>` élément, remplacez les espaces réservés de hello par nom de hello de votre espace de noms de service et hello clé SAP que vous avez copié dans une étape antérieure.</span><span class="sxs-lookup"><span data-stu-id="4a272-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="4a272-284">Dans l’élément de system.serviceModel hello, ajoutez un `<client>` élément.</span><span class="sxs-lookup"><span data-stu-id="4a272-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="4a272-285">Cette étape montre que vous définissez une application client de type WCF.</span><span class="sxs-lookup"><span data-stu-id="4a272-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="4a272-286">Au sein de hello `client` élément, définissez le nom de hello, contrat et type de liaison pour le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="4a272-287">Cette étape définit le nom de hello du point de terminaison hello, contrat hello défini dans le service de hello et faits hello que hello d’application cliente utilise TCP toocommunicate avec Azure relais.</span><span class="sxs-lookup"><span data-stu-id="4a272-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="4a272-288">Hello nom de point de terminaison est utilisé dans hello étape suivante toolink cette configuration de point de terminaison avec l’URI du service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="4a272-289">Cliquez sur **Fichier**, puis sur **Tout enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4a272-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="4a272-290">Exemple</span><span class="sxs-lookup"><span data-stu-id="4a272-290">Example</span></span>

<span data-ttu-id="4a272-291">Hello de code suivant montre fichier App.config de hello pour le client de Echo hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-291">hello following code shows hello App.config file for hello Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="4a272-292">Client de mettre en œuvre hello WCF</span><span class="sxs-lookup"><span data-stu-id="4a272-292">Implement hello WCF client</span></span>
<span data-ttu-id="4a272-293">Dans cette étape, vous implémentez une application cliente de base qui accède au service hello que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4a272-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="4a272-294">Service de toohello similaires, les clients hello effectue la plupart des hello même operations tooaccess Azure relais :</span><span class="sxs-lookup"><span data-stu-id="4a272-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="4a272-295">Définit le mode de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="4a272-296">Crée hello URI qui localise le service hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="4a272-297">Définit les informations d’identification de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="4a272-298">Applique la connexion de toohello hello informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4a272-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="4a272-299">Établit une connexion hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-299">Opens hello connection.</span></span>
6. <span data-ttu-id="4a272-300">Effectue des tâches spécifiques à l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="4a272-301">Ferme la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-301">Closes hello connection.</span></span>

<span data-ttu-id="4a272-302">Toutefois, une des principales différences de hello est que hello client application utilise un service de relais de canal tooconnect toohello, tandis que le service de hello utilise un appel trop**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="4a272-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="4a272-303">code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="4a272-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="4a272-304">Implémentation d’une application cliente</span><span class="sxs-lookup"><span data-stu-id="4a272-304">Implement a client application</span></span>
1. <span data-ttu-id="4a272-305">Définir le mode de connectivité hello trop**AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="4a272-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="4a272-306">Ajouter hello suivant du code à l’intérieur de hello `Main()` méthode Hello **EchoClient** application.</span><span class="sxs-lookup"><span data-stu-id="4a272-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="4a272-307">Définissez toohold hello les valeurs des variables pour l’espace de noms de service hello et la clé SAP qui sont lus à partir de la console de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="4a272-308">Créer hello URI qui définit l’emplacement de hello d’hôte de hello dans votre projet de relais.</span><span class="sxs-lookup"><span data-stu-id="4a272-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="4a272-309">Créer un objet d’informations d’identification hello pour votre point de terminaison de service espace de noms.</span><span class="sxs-lookup"><span data-stu-id="4a272-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="4a272-310">Créer la fabrication de canal hello qui charge la configuration hello décrite dans le fichier App.config hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="4a272-311">Une fabrique de canaux est un objet WCF qui crée un canal via lequel communiquent hello service et les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="4a272-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="4a272-312">Appliquer les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="4a272-313">Créez et ouvrez hello canal toohello service.</span><span class="sxs-lookup"><span data-stu-id="4a272-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="4a272-314">Écrire une interface utilisateur de base de hello et les fonctionnalités de l’écho de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="4a272-315">Notez que les code hello utilise instance hello d’objet de canal hello en tant que proxy pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="4a272-316">Fermer le canal de hello et fermer hello factory.</span><span class="sxs-lookup"><span data-stu-id="4a272-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="4a272-317">Exemple</span><span class="sxs-lookup"><span data-stu-id="4a272-317">Example</span></span>

<span data-ttu-id="4a272-318">Votre code terminé doit apparaître comme suit, montrant comment toocreate une application cliente, comment toocall hello les opérations du service de hello et comment tooclose hello client après l’opération de hello appellent est terminée.</span><span class="sxs-lookup"><span data-stu-id="4a272-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a><span data-ttu-id="4a272-319">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="4a272-319">Run hello applications</span></span>

1. <span data-ttu-id="4a272-320">Appuyez sur **Ctrl + Maj + B** solution de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="4a272-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="4a272-321">Cela génère le projet de client hello et de projet de service hello que vous avez créé dans les étapes précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="4a272-322">Avant l’application de client hello en cours d’exécution, il se peut que vous devez vous assurer que l’application de service hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="4a272-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="4a272-323">Dans l’Explorateur de solutions dans Visual Studio, avec le bouton droit hello **EchoService** solution, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4a272-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="4a272-324">Dans la boîte de dialogue de propriétés de solution de hello, cliquez sur **projet de démarrage**, puis cliquez sur hello **plusieurs projets de démarrage** bouton.</span><span class="sxs-lookup"><span data-stu-id="4a272-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="4a272-325">Assurez-vous que **EchoService** apparaît en premier dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="4a272-326">Ensemble hello **Action** zone pour les deux hello **EchoService** et **EchoClient** projets trop**Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="4a272-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="4a272-327">Cliquez sur **Dépendances du projet**.</span><span class="sxs-lookup"><span data-stu-id="4a272-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="4a272-328">Bonjour **projets** boîte, sélectionnez **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4a272-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="4a272-329">Bonjour **dépend** zone, assurez-vous que **EchoService** est activée.</span><span class="sxs-lookup"><span data-stu-id="4a272-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="4a272-330">Cliquez sur **OK** toodismiss hello **propriétés** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4a272-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="4a272-331">Appuyez sur **F5** toorun les deux projets.</span><span class="sxs-lookup"><span data-stu-id="4a272-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="4a272-332">Les deux fenêtres de console ouvrant et vous demander de nom d’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="4a272-333">Hello service doit s’exécuter en premier lieu, dans hello **EchoService** fenêtre console, entrez l’espace de noms hello et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4a272-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="4a272-334">Ensuite, vous êtes invité à fournir votre clé SAS.</span><span class="sxs-lookup"><span data-stu-id="4a272-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="4a272-335">Entrez la clé SAS hello et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="4a272-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="4a272-336">Voici un exemple de sortie à partir de la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-336">Here is example output from hello console window.</span></span> <span data-ttu-id="4a272-337">Notez que les valeurs de hello fournies ici sont par exemple uniquement.</span><span class="sxs-lookup"><span data-stu-id="4a272-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="4a272-338">`Your Service Namespace: myNamespace``Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="4a272-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="4a272-339">application de service Hello imprime toohello console fenêtre hello adresse sur lequel il est à l’écoute, comme dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4a272-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="4a272-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/``Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="4a272-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="4a272-341">Bonjour **EchoClient** fenêtre console, entrez hello les mêmes informations que vous avez entrées précédemment pour l’application de service hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="4a272-342">Suivez hello tooenter étapes précédentes de hello même espace de noms de service et les associations de sécurité des valeurs pour l’application cliente de hello de clé.</span><span class="sxs-lookup"><span data-stu-id="4a272-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="4a272-343">Après avoir entré ces valeurs, client de hello ouvre un canal toohello service et vous invite à entrer vous tooenter du texte comme indiqué dans hello exemple de sortie de console suivant.</span><span class="sxs-lookup"><span data-stu-id="4a272-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="4a272-344">Entrez une application de service de texte toosend toohello et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="4a272-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="4a272-345">Ce texte est envoyé à service toohello via une opération de service Echo de hello et apparaît dans la fenêtre de console de service hello comme hello suivant l’exemple de sortie.</span><span class="sxs-lookup"><span data-stu-id="4a272-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="4a272-346">application cliente de Hello reçoit la valeur de retour de hello Hello `Echo` opération, qui est le texte d’origine hello et imprime tooits fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="4a272-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="4a272-347">Hello Voici la sortie de la fenêtre de console cliente hello.</span><span class="sxs-lookup"><span data-stu-id="4a272-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="4a272-348">Vous pouvez continuer à envoyer des messages texte à partir du service de toohello hello client de cette manière.</span><span class="sxs-lookup"><span data-stu-id="4a272-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="4a272-349">Lorsque vous avez terminé, appuyez sur entrée dans hello client et service console windows tooend les deux applications.</span><span class="sxs-lookup"><span data-stu-id="4a272-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a272-350">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a272-350">Next steps</span></span>

<span data-ttu-id="4a272-351">Ce didacticiel a montré comment toobuild une application cliente de relais d’Azure et à l’aide du service hello fonctionnalités WCF relais du Bus de Service.</span><span class="sxs-lookup"><span data-stu-id="4a272-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="4a272-352">Pour obtenir un didacticiel similaire utilisant la [messagerie Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consultez [Bien démarrer avec les files d’attente Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="4a272-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="4a272-353">toolearn en savoir plus sur Azure relais, consultez hello rubriques suivantes.</span><span class="sxs-lookup"><span data-stu-id="4a272-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="4a272-354">Présentation de l’architecture d’Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="4a272-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="4a272-355">Vue d’ensemble d’Azure Relay</span><span class="sxs-lookup"><span data-stu-id="4a272-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="4a272-356">Comment toouse hello WCF de relais service avec .NET</span><span class="sxs-lookup"><span data-stu-id="4a272-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
