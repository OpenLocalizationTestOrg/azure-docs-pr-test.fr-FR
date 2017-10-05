---
title: Didacticiel Azure Service Bus WCF Relay | Microsoft Docs
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
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="4deb7-103">Didacticiel Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="4deb7-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="4deb7-104">Ce didacticiel vous montre comment créer une application cliente et un service WCF Relay simples à l’aide d’Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="4deb7-105">Pour obtenir un didacticiel similaire utilisant la [messagerie Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consultez [Bien démarrer avec les files d’attente Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="4deb7-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="4deb7-106">Ce didacticiel vous offre une présentation des étapes requises pour créer une application cliente et une application de service WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="4deb7-107">À l’instar de leurs homologues WCF d’origine, un service est une construction qui expose un ou plusieurs points de terminaison, chacun d’entre eux exposant une ou plusieurs opérations de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="4deb7-108">Le point de terminaison de service spécifie une adresse où le service peut être trouvé, une liaison contenant les informations qu’un client doit communiquer avec le service et le contrat qui définit la fonctionnalité fournie par le service à ses clients.</span><span class="sxs-lookup"><span data-stu-id="4deb7-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="4deb7-109">La principale différence entre WCF et WCF Relay est que le point de terminaison est exposé dans le cloud et non localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4deb7-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="4deb7-110">Lorsque vous avez exécuté la suite des rubriques présentes dans ce tutoriel, vous obtenez un service en cours de fonctionnement, et un client peut invoquer les opérations du service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="4deb7-111">La première rubrique décrit comment configurer un compte.</span><span class="sxs-lookup"><span data-stu-id="4deb7-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="4deb7-112">Les étapes suivantes décrivent comment définir un service utilisant un contrat, comment implémenter ledit service et comment le configurer dans le code.</span><span class="sxs-lookup"><span data-stu-id="4deb7-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="4deb7-113">Elles décrivent également comment héberger et exécuter le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="4deb7-114">Le service créé est auto hébergé et le client et le service s’exécutent sur le même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4deb7-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="4deb7-115">Vous pouvez configurer le service à l’aide d’un code ou d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="4deb7-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="4deb7-116">Les trois dernières étapes expliquent comment créer une application cliente, la configurer et créer et utiliser un client pouvant accéder à la fonctionnalité de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="4deb7-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4deb7-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4deb7-117">Prerequisites</span></span>

<span data-ttu-id="4deb7-118">Pour réaliser ce didacticiel, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4deb7-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="4deb7-119">[Microsoft Visual Studio 2015 ou une version ultérieure](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="4deb7-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="4deb7-120">Ce didacticiel utilise Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4deb7-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="4deb7-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4deb7-121">An active Azure account.</span></span> <span data-ttu-id="4deb7-122">Si vous n’en avez pas, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4deb7-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="4deb7-123">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4deb7-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="4deb7-124">Création d'un espace de noms de service</span><span class="sxs-lookup"><span data-stu-id="4deb7-124">Create a service namespace</span></span>

<span data-ttu-id="4deb7-125">La première étape consiste à créer un espace de noms et à obtenir une clé de [signature d’accès partagé (SAP)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="4deb7-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="4deb7-126">Un espace de noms fournit une limite d’application pour chaque application exposée via le service de relais.</span><span class="sxs-lookup"><span data-stu-id="4deb7-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="4deb7-127">Une clé SAP est automatiquement générée par le système lors de la création d’un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="4deb7-128">La combinaison de l’espace de noms de service et de la clé SAP fournit à Azure des informations d’identification permettant d’authentifier l’accès à une application.</span><span class="sxs-lookup"><span data-stu-id="4deb7-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="4deb7-129">Suivez les [instructions fournies ici](relay-create-namespace-portal.md) pour créer un espace de noms Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="4deb7-130">Définition d’un contrat de service WCF</span><span class="sxs-lookup"><span data-stu-id="4deb7-130">Define a WCF service contract</span></span>

<span data-ttu-id="4deb7-131">Le contrat de service spécifie les opérations (terminologie du service web pour les fonctions ou méthodes) que le service prend en charge.</span><span class="sxs-lookup"><span data-stu-id="4deb7-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="4deb7-132">Les contrats sont créés en définissant une interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="4deb7-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="4deb7-133">Chaque méthode dans l'interface correspond à une opération de service spécifique.</span><span class="sxs-lookup"><span data-stu-id="4deb7-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="4deb7-134">L’attribut [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) doit être appliqué à chaque interface et l’attribut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) doit être appliqué à chaque opération.</span><span class="sxs-lookup"><span data-stu-id="4deb7-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="4deb7-135">Si une méthode présente dans une interface contenant l’attribut [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) ne comporte pas l’attribut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), cette méthode n’est pas exposée.</span><span class="sxs-lookup"><span data-stu-id="4deb7-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="4deb7-136">Le code servant à effectuer ces tâches est fourni dans l’exemple qui suit la procédure.</span><span class="sxs-lookup"><span data-stu-id="4deb7-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="4deb7-137">Pour une description plus approfondie des contrats et des services, consultez [Conception et implémentation de services](https://msdn.microsoft.com/library/ms729746.aspx) dans la documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="4deb7-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="4deb7-138">Création d’un contrat de relais avec une interface</span><span class="sxs-lookup"><span data-stu-id="4deb7-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="4deb7-139">Ouvrez Visual Studio en tant qu’administrateur en cliquant avec le bouton droit sur le programme dans le menu **Démarrer**, puis sur **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="4deb7-140">Créez un projet d’application de console.</span><span class="sxs-lookup"><span data-stu-id="4deb7-140">Create a new console application project.</span></span> <span data-ttu-id="4deb7-141">Cliquez sur le menu **Fichier**, sélectionnez **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="4deb7-142">Dans la boîte de dialogue **Nouveau projet**, cliquez sur **Visual C#** (si **Visual C#** n’apparaît pas, regardez dans **Autres langages**).</span><span class="sxs-lookup"><span data-stu-id="4deb7-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="4deb7-143">Cliquez sur le modèle **Application Console (.NET Framework)** et nommez-le **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="4deb7-144">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="4deb7-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="4deb7-145">Installez le package NuGet Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4deb7-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="4deb7-146">Ce package ajoute automatiquement des références aux bibliothèques Service Bus, ainsi qu’au **System.ServiceModel** de WCF.</span><span class="sxs-lookup"><span data-stu-id="4deb7-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="4deb7-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) est l’espace de noms qui vous permet d’accéder par programme aux fonctionnalités WCF de base.</span><span class="sxs-lookup"><span data-stu-id="4deb7-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="4deb7-148">Service Bus utilise la plupart des objets et attributs de WCF pour définir des contrats de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="4deb7-149">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="4deb7-150">Cliquez sur l’onglet **Parcourir**, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="4deb7-151">Vérifiez que le nom du projet est spécifié dans la zone **Version(s)**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="4deb7-152">Cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4deb7-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="4deb7-153">Dans l’Explorateur de solutions, double-cliquez sur le fichier Program.cs pour l’ouvrir dans l’éditeur, si celui-ci n’est pas déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="4deb7-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="4deb7-154">Ajoutez les instructions using suivantes au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="4deb7-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="4deb7-155">Changez le nom de l’espace de noms du nom par défaut **EchoService** en **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4deb7-156">Ce didacticiel utilise l’espace de noms C# **Microsoft.ServiceBus.Samples**, qui est l’espace de noms du type géré par contrat utilisé dans le fichier de configuration à l’étape [Configurer le client WCF](#configure-the-wcf-client).</span><span class="sxs-lookup"><span data-stu-id="4deb7-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="4deb7-157">Vous pouvez spécifier n’importe quel espace de noms lorsque vous générez cet exemple ; toutefois, le didacticiel ne fonctionnera que si vous modifiez les espaces de noms du contrat et le service en conséquence, dans le fichier de configuration d’application de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="4deb7-158">L’espace de noms spécifié dans le fichier App.config doit être identique à l’espace de noms spécifié dans vos fichiers C#.</span><span class="sxs-lookup"><span data-stu-id="4deb7-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="4deb7-159">Définissez directement après la déclaration d’espace de noms `Microsoft.ServiceBus.Samples`, mais à l’intérieur de l’espace de noms, une nouvelle interface nommée `IEchoContract` et appliquez l’attribut `ServiceContractAttribute` à cette interface avec une valeur d’espace de noms de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="4deb7-160">La valeur de l'espace de noms diffère de l'espace de noms que vous utilisez dans l’ensemble de votre code.</span><span class="sxs-lookup"><span data-stu-id="4deb7-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="4deb7-161">En revanche, la valeur de l’espace de noms est utilisée comme identificateur unique pour ce contrat.</span><span class="sxs-lookup"><span data-stu-id="4deb7-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="4deb7-162">Spécifier explicitement l'espace de noms empêche l'ajout au nom du contrat de la valeur d'espace de noms par défaut.</span><span class="sxs-lookup"><span data-stu-id="4deb7-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="4deb7-163">Collez le code suivant après la déclaration de l’espace de noms :</span><span class="sxs-lookup"><span data-stu-id="4deb7-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="4deb7-164">En règle générale, l’espace de noms de contrat de service contient un schéma d’affectation de noms qui inclut des informations de version.</span><span class="sxs-lookup"><span data-stu-id="4deb7-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="4deb7-165">L’inclusion des informations de version dans l’espace de noms de contrat de service permet aux services d’isoler les modifications majeures en définissant un contrat de service avec un nouvel espace de noms et en l’exposant sur un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4deb7-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="4deb7-166">De cette manière, les clients peuvent continuer à utiliser l’ancien contrat de service sans avoir à procéder à la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4deb7-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="4deb7-167">Les informations de version peuvent se composer d’une date ou un numéro de version.</span><span class="sxs-lookup"><span data-stu-id="4deb7-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="4deb7-168">Pour plus d’informations, consultez la rubrique [Contrôle de version des services](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="4deb7-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="4deb7-169">Dans le cadre de ce didacticiel, le schéma d’affectation de noms de l’espace de noms de contrat de service ne contient pas les informations de version.</span><span class="sxs-lookup"><span data-stu-id="4deb7-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="4deb7-170">Dans l’interface `IEchoContract`, déclarez une méthode pour l’unique opération exposée par le contrat `IEchoContract` dans l’interface, puis appliquez l’attribut `OperationContractAttribute` à la méthode que vous souhaitez exposer dans le cadre du contrat WCF Relay public, de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="4deb7-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="4deb7-171">Directement après la définition de l’interface `IEchoContract`, déclarez un canal qui hérite à la fois de `IEchoContract` et de l’interface `IClientChannel`, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="4deb7-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="4deb7-172">Un canal est l’objet WCF par le biais duquel l’hôte et le client se transmettent des informations.</span><span class="sxs-lookup"><span data-stu-id="4deb7-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="4deb7-173">Par la suite , vous allez écrire du code par rapport au canal pour reprendre les informations entre les deux applications.</span><span class="sxs-lookup"><span data-stu-id="4deb7-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="4deb7-174">Dans le menu **Générer**, cliquez sur **Générer la solution** ou appuyez sur **Ctrl+Maj+B** pour confirmer que votre travail est correct jusqu’à présent.</span><span class="sxs-lookup"><span data-stu-id="4deb7-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="4deb7-175">Exemple</span><span class="sxs-lookup"><span data-stu-id="4deb7-175">Example</span></span>

<span data-ttu-id="4deb7-176">Le code suivant montre une interface de base qui définit un contrat WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="4deb7-177">Maintenant que l’interface est créée, vous pouvez implémenter l’interface.</span><span class="sxs-lookup"><span data-stu-id="4deb7-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="4deb7-178">Implémentation du contrat WCF</span><span class="sxs-lookup"><span data-stu-id="4deb7-178">Implement the WCF contract</span></span>

<span data-ttu-id="4deb7-179">La création d’un relais Azure nécessite la création au préalable du contrat défini à l’aide d’une interface.</span><span class="sxs-lookup"><span data-stu-id="4deb7-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="4deb7-180">Pour plus d’informations sur la création de l’interface, consultez l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="4deb7-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="4deb7-181">L'étape suivante consiste à implémenter l'interface.</span><span class="sxs-lookup"><span data-stu-id="4deb7-181">The next step is to implement the interface.</span></span> <span data-ttu-id="4deb7-182">Cela implique la création d’une classe nommée `EchoService` qui met en œuvre l’interface `IEchoContract` définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4deb7-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="4deb7-183">Une fois l’interface implémentée, vous configurez l’interface à l’aide d’un fichier de configuration App.config.</span><span class="sxs-lookup"><span data-stu-id="4deb7-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="4deb7-184">Le fichier de configuration contient les informations nécessaires à l’application, notamment le nom du service, le nom du contrat et le type de protocole utilisé pour communiquer avec le service de relais.</span><span class="sxs-lookup"><span data-stu-id="4deb7-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="4deb7-185">Le code utilisé pour effectuer ces tâches est fourni dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="4deb7-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="4deb7-186">Pour obtenir une description plus générale sur la manière d’implémenter un contrat de service, consultez [Implémentation de contrats de service](https://msdn.microsoft.com/library/ms733764.aspx) dans la documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="4deb7-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="4deb7-187">Créez une classe nommée `EchoService` directement après la définition de l’interface `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="4deb7-188">La classe `EchoService` implémente l’interface `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="4deb7-189">Comme pour d'autres implémentations d'interface, vous pouvez implémenter la définition dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="4deb7-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="4deb7-190">Toutefois, pour ce didacticiel, l’implémentation se situe dans le même fichier que la définition d’interface et la méthode `Main`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="4deb7-191">Appliquez l’attribut [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) à l’interface `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="4deb7-192">L’attribut spécifie le nom du service ainsi que son espace de noms.</span><span class="sxs-lookup"><span data-stu-id="4deb7-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="4deb7-193">Ensuite, la classe `EchoService` apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="4deb7-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="4deb7-194">Implémentez la méthode `Echo` définie dans l’interface `IEchoContract` dans la classe `EchoService`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="4deb7-195">Cliquez sur **Générer**, puis sur **Générer la solution** pour confirmer que votre travail est correct.</span><span class="sxs-lookup"><span data-stu-id="4deb7-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="4deb7-196">Définition de la configuration de l’hôte de service</span><span class="sxs-lookup"><span data-stu-id="4deb7-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="4deb7-197">Le fichier de configuration est très similaire à un fichier de configuration WCF.</span><span class="sxs-lookup"><span data-stu-id="4deb7-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="4deb7-198">Il contient le nom du service, le point de terminaison (c’est-à-dire l’emplacement qu’Azure Relay expose aux clients et aux ordinateurs hôtes afin qu’ils communiquent entre eux) et la liaison (type de protocole utilisé pour communiquer).</span><span class="sxs-lookup"><span data-stu-id="4deb7-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="4deb7-199">La principale différence réside dans le fait que le point de terminaison de service configuré fait référence à la liaison [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding), qui ne fait pas partie de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4deb7-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="4deb7-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) est l’une des liaisons définies par le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="4deb7-201">Dans **l’Explorateur de solutions**, double-cliquez sur le fichier App.config pour l’ouvrir dans l’éditeur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4deb7-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="4deb7-202">Dans l’élément `<appSettings>`, remplacez les espaces réservés par le nom de votre espace de noms de service et par la clé SAP que vous avez copiée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="4deb7-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="4deb7-203">Dans les balises `<system.serviceModel>`, ajouter un élément `<services>`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="4deb7-204">Vous pouvez définir plusieurs applications de relais dans un même fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="4deb7-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="4deb7-205">Toutefois, ce didacticiel n’en définit qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="4deb7-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="4deb7-206">Dans l’élément `<services>`, ajoutez un élément `<service>` pour définir le nom du service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="4deb7-207">Dans l’élément `<service>`, définissez l’emplacement du contrat de point de terminaison, ainsi que le type de liaison de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="4deb7-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="4deb7-208">Le point de terminaison définit l’emplacement où le client recherchera l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="4deb7-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="4deb7-209">Plus tard, le didacticiel utilise cette étape pour créer une URI qui expose entièrement l’hôte via Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="4deb7-210">La liaison déclare que nous utilisons TCP comme protocole pour communiquer avec le service de relais.</span><span class="sxs-lookup"><span data-stu-id="4deb7-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="4deb7-211">Dans le menu **Générer**, cliquez sur **Générer la solution** pour confirmer que votre travail est correct.</span><span class="sxs-lookup"><span data-stu-id="4deb7-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="4deb7-212">Exemple</span><span class="sxs-lookup"><span data-stu-id="4deb7-212">Example</span></span>

<span data-ttu-id="4deb7-213">Le code suivant illustre l’implémentation du contrat de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-213">The following code shows the implementation of the service contract.</span></span>

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

<span data-ttu-id="4deb7-214">L’exemple suivant montre le format de case du fichier App.config associé à l’hôte de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="4deb7-215">Hébergement et exécution d’un service web de base pour s’enregistrer auprès du service de relais</span><span class="sxs-lookup"><span data-stu-id="4deb7-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="4deb7-216">Cette étape décrit comment exécuter un service Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="4deb7-217">Création des informations d’identification du relais</span><span class="sxs-lookup"><span data-stu-id="4deb7-217">Create the relay credentials</span></span>

1. <span data-ttu-id="4deb7-218">Dans `Main()`, créez deux variables dans lesquelles stocker l’espace de noms et la clé SAS qui sont lues à partir de la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="4deb7-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="4deb7-219">La clé SAP sera utilisée ultérieurement pour accéder à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4deb7-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="4deb7-220">L’espace de noms est transmis en tant que paramètre à `CreateServiceUri` pour créer une URI de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="4deb7-221">À l’aide d’un objet [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior), déclarez que vous utiliserez une clé SAP en tant que type d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4deb7-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="4deb7-222">Ajoutez le code suivant directement après le code ajouté à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="4deb7-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="4deb7-223">Création d’une adresse de base pour le service</span><span class="sxs-lookup"><span data-stu-id="4deb7-223">Create a base address for the service</span></span>

<span data-ttu-id="4deb7-224">Après le code ajouté à l’étape précédente, créez une instance `Uri` pour l’adresse de base du service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="4deb7-225">Cette URI spécifie le schéma Service Bus, l’espace de noms et le chemin d’accès de l’interface de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="4deb7-226">« sb » est une abréviation pour le modèle Service Bus et indique que nous utilisons TCP comme protocole.</span><span class="sxs-lookup"><span data-stu-id="4deb7-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="4deb7-227">Cette information était précédemment indiquée dans le fichier de configuration, lorsque [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) a été spécifié en tant que liaison.</span><span class="sxs-lookup"><span data-stu-id="4deb7-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="4deb7-228">Pour ce didacticiel, l’URI est `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="4deb7-229">Création et configuration de l’hôte de service</span><span class="sxs-lookup"><span data-stu-id="4deb7-229">Create and configure the service host</span></span>

1. <span data-ttu-id="4deb7-230">Définissez le mode connectivité sur `AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="4deb7-231">Le mode de connectivité décrit le protocole que le service utilise pour communiquer avec le service de relais ; HTTP ou TCP.</span><span class="sxs-lookup"><span data-stu-id="4deb7-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="4deb7-232">Avec la valeur `AutoDetect` par défaut, le service tente de se connecter à Azure Relay via TCP s’il est disponible et HTTP dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="4deb7-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="4deb7-233">Notez que cela diffère du protocole du service spécifié pour la communication client.</span><span class="sxs-lookup"><span data-stu-id="4deb7-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="4deb7-234">Ce protocole est déterminé par la liaison utilisée.</span><span class="sxs-lookup"><span data-stu-id="4deb7-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="4deb7-235">Par exemple, un service peut utiliser la liaison [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx), qui indique que son point de terminaison communique avec les clients via HTTP.</span><span class="sxs-lookup"><span data-stu-id="4deb7-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="4deb7-236">Ce même service peut spécifier **ConnectivityMode.AutoDetect** de manière que le service communique avec Azure Relay via TCP.</span><span class="sxs-lookup"><span data-stu-id="4deb7-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="4deb7-237">Créez l’hôte de service, en utilisant l’URI créée précédemment dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4deb7-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="4deb7-238">L’hôte de service est l’objet WCF qui instancie le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="4deb7-239">Ici, vous transmettez le type de service que vous souhaitez créer (un type `EchoService`), ainsi que l’adresse à laquelle vous souhaitez exposer le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="4deb7-240">En haut du fichier Program.cs, ajoutez des références à [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) et [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="4deb7-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="4deb7-241">De retour dans `Main()`, configurez le point de terminaison pour activer l’accès public.</span><span class="sxs-lookup"><span data-stu-id="4deb7-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="4deb7-242">Cette étape informe le service de relais que votre application peut être trouvée publiquement en examinant le flux ATOM de votre projet.</span><span class="sxs-lookup"><span data-stu-id="4deb7-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="4deb7-243">Si vous définissez **DiscoveryType** sur **privé**, un client est toujours en mesure d’accéder au service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="4deb7-244">Toutefois, le service n’apparaît pas lorsqu’il recherche l’espace de noms Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="4deb7-245">Au lieu de ça, le client doit connaître le chemin d’accès du point de terminaison au préalable.</span><span class="sxs-lookup"><span data-stu-id="4deb7-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="4deb7-246">Appliquer les informations d’identification de service aux points de terminaison de service définis dans le fichier App.config :</span><span class="sxs-lookup"><span data-stu-id="4deb7-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="4deb7-247">Comme indiqué à l’étape précédente, il se peut que vous ayez déclaré plusieurs services et points de terminaison dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="4deb7-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="4deb7-248">Si c’est le cas, ce code traverse le fichier de configuration et recherche chaque point de terminaison auquel vos informations d’identification doivent être appliquées.</span><span class="sxs-lookup"><span data-stu-id="4deb7-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="4deb7-249">Toutefois, pour ce didacticiel, le fichier de configuration n’a qu’un seul point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4deb7-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="4deb7-250">Ouverture de l’hôte de service</span><span class="sxs-lookup"><span data-stu-id="4deb7-250">Open the service host</span></span>

1. <span data-ttu-id="4deb7-251">Ouvrez le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="4deb7-252">Informez l’utilisateur que le service est en cours d’exécution et expliquez comment arrêter le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="4deb7-253">Lorsque vous avez terminé, fermez l'hôte de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="4deb7-254">Appuyez sur **Ctrl+Maj+B** pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="4deb7-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="4deb7-255">Exemple</span><span class="sxs-lookup"><span data-stu-id="4deb7-255">Example</span></span>

<span data-ttu-id="4deb7-256">Une fois terminé, votre code de service doit se présenter ainsi.</span><span class="sxs-lookup"><span data-stu-id="4deb7-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="4deb7-257">Il comprend le contrat de service et l’implémentation des étapes précédentes du didacticiel, et héberge le service dans une application console.</span><span class="sxs-lookup"><span data-stu-id="4deb7-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

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

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="4deb7-258">Créer un client WCF pour le contrat de service</span><span class="sxs-lookup"><span data-stu-id="4deb7-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="4deb7-259">L’étape suivante consiste à créer une application cliente et à définir le contrat de service que vous allez implémenter au cours des étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4deb7-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="4deb7-260">Notez que plusieurs de ces étapes ressemblent aux étapes utilisées pour créer un service : définition d’un contrat, modification d’un fichier App.config à l’aide des informations d’identification servant à se connecter au service de relais et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4deb7-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="4deb7-261">Le code utilisé pour effectuer ces tâches est fourni dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="4deb7-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="4deb7-262">Créer un nouveau projet dans la solution Visual Studio en cours pour le client en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="4deb7-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="4deb7-263">Dans l’Explorateur de solutions, dans la solution qui contient le service, cliquez avec le bouton droit sur la solution actuelle (et non sur le projet), puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="4deb7-264">Puis cliquez sur **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="4deb7-265">Dans la boîte de dialogue **Ajouter un nouveau projet**, cliquez sur **Visual C#** (si **Visual C#** n’apparaît pas, regardez dans **Autres langages**), sélectionnez le modèle **Application console (.NET Framework)** et nommez-le **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="4deb7-266">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="4deb7-267">Dans l’Explorateur de solutions, double-cliquez sur le fichier Program.cs dans le projet **EchoClient** pour l’ouvrir dans l’éditeur, si celui-ci n’est pas déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="4deb7-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="4deb7-268">Remplacez le nom par défaut de l'espace de noms `EchoClient` par `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="4deb7-269">Installez le [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) : dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **EchoClient**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="4deb7-270">Cliquez sur l’onglet **Parcourir**, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="4deb7-271">Cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4deb7-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="4deb7-272">Ajoutez une instruction `using` pour l’espace de noms [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) dans le fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="4deb7-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="4deb7-273">Ajoutez la définition de contrat de service à l’espace de noms, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4deb7-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="4deb7-274">Notez que cette définition est identique à celle qui est utilisée dans le projet **Service**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="4deb7-275">Vous devez ajouter ce code en haut de l’espace de noms `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="4deb7-276">Appuyez sur **Ctrl+Maj+B** pour générer le client.</span><span class="sxs-lookup"><span data-stu-id="4deb7-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="4deb7-277">Exemple</span><span class="sxs-lookup"><span data-stu-id="4deb7-277">Example</span></span>

<span data-ttu-id="4deb7-278">Le code suivant montre l’état actuel du fichier Program.cs dans le projet **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

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

## <a name="configure-the-wcf-client"></a><span data-ttu-id="4deb7-279">Configurer le client WCF</span><span class="sxs-lookup"><span data-stu-id="4deb7-279">Configure the WCF client</span></span>

<span data-ttu-id="4deb7-280">Dans cette étape, vous allez créer une application cliente de base qui accède au service que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4deb7-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="4deb7-281">Ce fichier App.config définit le contrat, la liaison et le nom du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4deb7-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="4deb7-282">Le code utilisé pour effectuer ces tâches est fourni dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="4deb7-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="4deb7-283">Dans l’Explorateur de solutions, dans le projet **EchoClient**, double-cliquez sur **App.config** pour ouvrir le fichier dans l’éditeur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4deb7-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="4deb7-284">Dans l’élément `<appSettings>`, remplacez les espaces réservés par le nom de votre espace de noms de service et par la clé SAP que vous avez copiée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="4deb7-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="4deb7-285">Dans l’élément system.serviceModel, ajoutez un élément `<client>`.</span><span class="sxs-lookup"><span data-stu-id="4deb7-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="4deb7-286">Cette étape montre que vous définissez une application client de type WCF.</span><span class="sxs-lookup"><span data-stu-id="4deb7-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="4deb7-287">Dans l ’élément `client`, définissez le nom, le contrat et le type de liaison du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4deb7-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="4deb7-288">Cette étape définit le nom du point de terminaison, le contrat défini dans le service et le fait que l’application cliente utilise TCP pour communiquer avec Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="4deb7-289">Le nom de point de terminaison est utilisé dans l’étape suivante pour associer cette configuration de point de terminaison à l’URI de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="4deb7-290">Cliquez sur **Fichier**, puis sur **Tout enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="4deb7-291">Exemple</span><span class="sxs-lookup"><span data-stu-id="4deb7-291">Example</span></span>

<span data-ttu-id="4deb7-292">Le code suivant montre le fichier App.config correspondant au client Echo.</span><span class="sxs-lookup"><span data-stu-id="4deb7-292">The following code shows the App.config file for the Echo client.</span></span>

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

## <a name="implement-the-wcf-client"></a><span data-ttu-id="4deb7-293">Implémentation du client WCF</span><span class="sxs-lookup"><span data-stu-id="4deb7-293">Implement the WCF client</span></span>
<span data-ttu-id="4deb7-294">Dans cette étape, vous allez mettre en oeuvre une application cliente de base qui accède au service que vous avez créé précédemment dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4deb7-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="4deb7-295">Comme le service, le client effectue de nombreuses opérations similaires pour accéder à Azure Relay :</span><span class="sxs-lookup"><span data-stu-id="4deb7-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="4deb7-296">Définit le mode connectivité sur.</span><span class="sxs-lookup"><span data-stu-id="4deb7-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="4deb7-297">Crée l’URI qui localise le service hôte.</span><span class="sxs-lookup"><span data-stu-id="4deb7-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="4deb7-298">Définit les informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4deb7-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="4deb7-299">Applique les informations d’identification à la connexion.</span><span class="sxs-lookup"><span data-stu-id="4deb7-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="4deb7-300">Ouvre la connexion.</span><span class="sxs-lookup"><span data-stu-id="4deb7-300">Opens the connection.</span></span>
6. <span data-ttu-id="4deb7-301">Effectue les tâches spécifiques à l’application.</span><span class="sxs-lookup"><span data-stu-id="4deb7-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="4deb7-302">Ferme la connexion.</span><span class="sxs-lookup"><span data-stu-id="4deb7-302">Closes the connection.</span></span>

<span data-ttu-id="4deb7-303">Toutefois, une des principales différences réside dans le fait que l’application cliente utilise un canal pour se connecter au service de relais, tandis que le service utilise un appel à **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="4deb7-304">Le code utilisé pour effectuer ces tâches est fourni dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="4deb7-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="4deb7-305">Implémentation d’une application cliente</span><span class="sxs-lookup"><span data-stu-id="4deb7-305">Implement a client application</span></span>
1. <span data-ttu-id="4deb7-306">Définissez le mode de connectivité sur **AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="4deb7-307">Ajoutez le code suivant à la méthode `Main()` de l’application **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="4deb7-308">Définissez des variables pour stocker les valeurs de l’espace de noms de service et la clé SAS qui sont lues depuis la console.</span><span class="sxs-lookup"><span data-stu-id="4deb7-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="4deb7-309">Créez l’URI qui définit l’emplacement de l’hôte dans votre projet Relay.</span><span class="sxs-lookup"><span data-stu-id="4deb7-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="4deb7-310">Créez l’objet d’informations d’identification de votre point de terminaison d’espace de noms du service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="4deb7-311">Création de la structure de canaux qui charge la configuration décrite dans le fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="4deb7-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="4deb7-312">Une structure de canaux est un objet WCF qui crée un canal via lequel les services et les applications clients communiquent.</span><span class="sxs-lookup"><span data-stu-id="4deb7-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="4deb7-313">Appliquez les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4deb7-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="4deb7-314">Créer et ouvrir le canal au service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="4deb7-315">Écrire l’interface utilisateur de base et les fonctionnalités pour l’écho.</span><span class="sxs-lookup"><span data-stu-id="4deb7-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

    <span data-ttu-id="4deb7-316">Notez que le code utilise l’instance de l’objet de canal en tant que proxy pour le service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="4deb7-317">Fermez le canal ainsi que la structure.</span><span class="sxs-lookup"><span data-stu-id="4deb7-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="4deb7-318">Exemple</span><span class="sxs-lookup"><span data-stu-id="4deb7-318">Example</span></span>

<span data-ttu-id="4deb7-319">Une fois terminé, votre code doit se présenter ainsi : il montre comment créer une application client, comment appeler les opérations du service et comment fermer le client une fois l’appel d’opération terminé.</span><span class="sxs-lookup"><span data-stu-id="4deb7-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

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

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

## <a name="run-the-applications"></a><span data-ttu-id="4deb7-320">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="4deb7-320">Run the applications</span></span>

1. <span data-ttu-id="4deb7-321">Appuyez sur **Ctrl+Maj+B** pour générer la solution.</span><span class="sxs-lookup"><span data-stu-id="4deb7-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="4deb7-322">Ceci génère le projet client et le projet de service que vous avez créés aux étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="4deb7-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="4deb7-323">Avant d’exécuter l’application cliente, assurez-vous que l’application de service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4deb7-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="4deb7-324">Dans l’Explorateur de solutions dans Visual Studio, cliquez sur la solution **EchoService**, puis sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="4deb7-325">Dans la boîte de dialogue Propriétés de la solution, cliquez sur **Projet de démarrage**, puis sur le bouton **Plusieurs projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="4deb7-326">Assurez-vous que **EchoService** apparaît en premier dans la liste.</span><span class="sxs-lookup"><span data-stu-id="4deb7-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="4deb7-327">Définissez le champ **Action** sur **Démarrer** pour les projets **EchoService** et **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="4deb7-328">Cliquez sur **Dépendances du projet**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="4deb7-329">Dans le champ **Projets**, sélectionnez **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="4deb7-330">Dans le champ **Dépend de**, assurez-vous que l’option **EchoService** est activée.</span><span class="sxs-lookup"><span data-stu-id="4deb7-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="4deb7-331">Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="4deb7-332">Appuyez sur **F5** pour exécuter les deux projets.</span><span class="sxs-lookup"><span data-stu-id="4deb7-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="4deb7-333">Les deux fenêtres de console s’ouvrent et vous invitent à renseigner le nom de l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="4deb7-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="4deb7-334">Le service doit d’abord s’exécuter. Dans la fenêtre de console **EchoService**, entrez l’espace de noms, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="4deb7-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="4deb7-335">Ensuite, vous êtes invité à fournir votre clé SAS.</span><span class="sxs-lookup"><span data-stu-id="4deb7-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="4deb7-336">Entrez la clé SAS et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="4deb7-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="4deb7-337">Voici un exemple de sortie de la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="4deb7-337">Here is example output from the console window.</span></span> <span data-ttu-id="4deb7-338">Notez que les valeurs indiquées ici sont fournies à titre d’exemple uniquement.</span><span class="sxs-lookup"><span data-stu-id="4deb7-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="4deb7-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="4deb7-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="4deb7-340">L’application de service imprime l’adresse sur laquelle il écoute dans la fenêtre de console, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4deb7-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="4deb7-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="4deb7-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="4deb7-342">Dans la fenêtre de console **EchoClient**, entrez les mêmes informations que celles que vous avez entrées précédemment pour l’application de service.</span><span class="sxs-lookup"><span data-stu-id="4deb7-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="4deb7-343">Suivez les étapes précédentes pour saisir des valeurs identiques pour l’espace de noms de service et la clé SAP pour l’application cliente</span><span class="sxs-lookup"><span data-stu-id="4deb7-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="4deb7-344">Après avoir saisi ces valeurs, le client ouvre un canal au service et vous invite à saisir du texte, comme indiqué dans l’exemple de sortie de console suivante.</span><span class="sxs-lookup"><span data-stu-id="4deb7-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="4deb7-345">Saisissez du texte à envoyer à l’application de service, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="4deb7-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="4deb7-346">Ce texte est envoyé au service via l’opération de service Echo et apparaît dans la fenêtre de console de service comme dans l’exemple de sortie suivant.</span><span class="sxs-lookup"><span data-stu-id="4deb7-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="4deb7-347">L’application cliente reçoit la valeur de retour de l’opération `Echo`, qui est le texte d’origine, et l’imprime sur la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="4deb7-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="4deb7-348">Voici un exemple de sortie de la fenêtre de console du client.</span><span class="sxs-lookup"><span data-stu-id="4deb7-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="4deb7-349">Vous pouvez continuer d’envoyer des messages texte du client au service de cette manière.</span><span class="sxs-lookup"><span data-stu-id="4deb7-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="4deb7-350">Une fois que vous avez terminé, appuyez sur Entrée dans les fenêtres du client et de la console de service pour arrêter les des deux applications.</span><span class="sxs-lookup"><span data-stu-id="4deb7-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4deb7-351">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4deb7-351">Next steps</span></span>

<span data-ttu-id="4deb7-352">Ce didacticiel vous a montré comment créer une application cliente et un service Azure Relay à l’aide des fonctionnalités WCF Relay de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4deb7-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="4deb7-353">Pour obtenir un didacticiel similaire utilisant la [messagerie Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consultez [Bien démarrer avec les files d’attente Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="4deb7-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="4deb7-354">Pour en savoir plus sur Azure Relay, consultez les rubriques suivantes.</span><span class="sxs-lookup"><span data-stu-id="4deb7-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="4deb7-355">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="4deb7-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="4deb7-356">Vue d’ensemble d’Azure Relay</span><span class="sxs-lookup"><span data-stu-id="4deb7-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="4deb7-357">Guide pratique pour utiliser le service WCF Relay avec .NET</span><span class="sxs-lookup"><span data-stu-id="4deb7-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
