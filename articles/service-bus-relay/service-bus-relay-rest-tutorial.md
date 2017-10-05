---
title: Didacticiel Service Bus REST utilisant Azure Relay | Microsoft Docs
description: "Créez une simple application hôte Azure Service Bus Relay présentant une interface de type REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="f41cb-103">Didacticiel Azure WCF Relay REST</span><span class="sxs-lookup"><span data-stu-id="f41cb-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="f41cb-104">Ce didacticiel explique comment créer une simple application hôte Azure Relay qui expose une interface de type REST.</span><span class="sxs-lookup"><span data-stu-id="f41cb-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="f41cb-105">REST permet à un client web, par exemple un navigateur web, d’accéder aux API Service Bus via des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="f41cb-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="f41cb-106">Le didacticiel utilise le modèle de programmation REST Windows Communication Foundation (WCF) pour construire un service REST sur Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f41cb-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="f41cb-107">Pour plus d’informations, consultez les rubriques [Modèle de programmation REST WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) et [Conception et implémentation de services](/dotnet/framework/wcf/designing-and-implementing-services) dans la documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="f41cb-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="f41cb-108">Étape 1 : Création d’un espace de noms</span><span class="sxs-lookup"><span data-stu-id="f41cb-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="f41cb-109">Pour commencer à utiliser les fonctionnalités de relais dans Azure, vous devez d’abord créer un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="f41cb-110">Un espace de noms fournit un conteneur d’étendue pour l’adressage des ressources Azure au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="f41cb-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="f41cb-111">Suivez les [instructions fournies ici](relay-create-namespace-portal.md) pour créer un espace de noms Relay.</span><span class="sxs-lookup"><span data-stu-id="f41cb-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="f41cb-112">Étape 2 : Définition d’un contrat de service REST WCF à utiliser avec Azure Relay</span><span class="sxs-lookup"><span data-stu-id="f41cb-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="f41cb-113">Lorsque vous créez un service de type REST WCF, vous devez définir le contrat.</span><span class="sxs-lookup"><span data-stu-id="f41cb-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="f41cb-114">Le contrat spécifie les opérations prises en charge par l'hôte.</span><span class="sxs-lookup"><span data-stu-id="f41cb-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="f41cb-115">Une opération de service peut être considérée comme une méthode de service web.</span><span class="sxs-lookup"><span data-stu-id="f41cb-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="f41cb-116">Les contrats sont créés en définissant une interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="f41cb-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="f41cb-117">Chaque méthode dans l'interface correspond à une opération de service spécifique.</span><span class="sxs-lookup"><span data-stu-id="f41cb-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="f41cb-118">L’attribut [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) doit être appliqué à chaque interface et l’attribut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) doit être appliqué à chaque opération.</span><span class="sxs-lookup"><span data-stu-id="f41cb-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="f41cb-119">Si une méthode dans une interface qui contient l’attribut [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) n’a pas l’attribut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), cette méthode n’est pas exposée.</span><span class="sxs-lookup"><span data-stu-id="f41cb-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="f41cb-120">Le code utilisé pour effectuer ces tâches est indiqué dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="f41cb-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="f41cb-121">La principale différence entre un contrat WCF et un contrat de type REST est l’ajout d’une propriété à l’attribut [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) : [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="f41cb-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="f41cb-122">Cette propriété vous permet de mapper une méthode dans votre interface à une méthode de l'autre côté de l'interface.</span><span class="sxs-lookup"><span data-stu-id="f41cb-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="f41cb-123">Dans ce cas, nous utiliserons [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) pour associer une méthode à HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="f41cb-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="f41cb-124">Cela permet à Service Bus de récupérer et d’interpréter correctement les commandes envoyées à l'interface.</span><span class="sxs-lookup"><span data-stu-id="f41cb-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="f41cb-125">Création d’un contrat avec une interface</span><span class="sxs-lookup"><span data-stu-id="f41cb-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="f41cb-126">Ouvrez Visual Studio en tant qu’administrateur : cliquez avec le bouton droit sur le programme dans le menu **Démarrer**, puis cliquez sur **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="f41cb-127">Créez un projet d’application de console.</span><span class="sxs-lookup"><span data-stu-id="f41cb-127">Create a new console application project.</span></span> <span data-ttu-id="f41cb-128">Cliquez sur le menu **Fichier**, sélectionnez **Nouveau**, puis **Projet**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="f41cb-129">Dans la boîte de dialogue **Nouveau projet**, cliquez sur **Visual C#**, sélectionnez le modèle **Application console** et nommez-le **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="f41cb-130">Utilisez **l’emplacement** par défaut.</span><span class="sxs-lookup"><span data-stu-id="f41cb-130">Use the default **Location**.</span></span> <span data-ttu-id="f41cb-131">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="f41cb-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="f41cb-132">Pour un projet C#, Visual Studio crée un fichier `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="f41cb-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="f41cb-133">Cette classe contient une méthode `Main()` vide, requise pour créer correctement un projet d’application console.</span><span class="sxs-lookup"><span data-stu-id="f41cb-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="f41cb-134">Ajoutez des références à Service Bus et **System.ServiceModel.dll** au projet en installant le package NuGet Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f41cb-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="f41cb-135">Ce package ajoute automatiquement des références aux bibliothèques Service Bus, ainsi qu’au WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="f41cb-136">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ImageListener**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="f41cb-137">Cliquez sur l’onglet **Parcourir**, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="f41cb-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="f41cb-138">Cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="f41cb-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="f41cb-139">Vous devez explicitement ajouter une référence à **System.ServiceModel.Web.dll** au projet :</span><span class="sxs-lookup"><span data-stu-id="f41cb-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="f41cb-140">a.</span><span class="sxs-lookup"><span data-stu-id="f41cb-140">a.</span></span> <span data-ttu-id="f41cb-141">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le dossier **Références**, puis cliquez sur **Ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="f41cb-142">b.</span><span class="sxs-lookup"><span data-stu-id="f41cb-142">b.</span></span> <span data-ttu-id="f41cb-143">Dans la boîte de dialogue **Ajouter une référence**, cliquez sur l’onglet **Framework** sur le côté gauche puis, dans la zone **Rechercher**, tapez **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="f41cb-144">Cochez la case **System.ServiceModel.Web**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="f41cb-145">Ajoutez les instructions `using` suivantes en haut du fichier Program.cs.</span><span class="sxs-lookup"><span data-stu-id="f41cb-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="f41cb-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) est l’espace de noms qui permet l’accès par programme aux fonctionnalités WCF de base.</span><span class="sxs-lookup"><span data-stu-id="f41cb-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="f41cb-147">WCF Relay utilise la plupart des objets et attributs de WCF pour définir des contrats de service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="f41cb-148">Vous utiliserez cet espace de noms dans la plupart de vos applications de relais.</span><span class="sxs-lookup"><span data-stu-id="f41cb-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="f41cb-149">De même, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) permet de définir le canal, qui est l’objet via lequel vous communiquez avec Azure Relay et le navigateur web client.</span><span class="sxs-lookup"><span data-stu-id="f41cb-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="f41cb-150">Enfin, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contient les types qui vous permettent de créer des applications web.</span><span class="sxs-lookup"><span data-stu-id="f41cb-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="f41cb-151">Renommez l’espace de noms `ImageListener` en **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="f41cb-152">Directement après l’accolade d’ouverture de la déclaration d’espace de noms, définissez une nouvelle interface nommée **IImageContract** et appliquez l’attribut **ServiceContractAttribute** à l’interface avec une valeur de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="f41cb-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="f41cb-153">La valeur de l'espace de noms diffère de l'espace de noms que vous utilisez dans l’ensemble de votre code.</span><span class="sxs-lookup"><span data-stu-id="f41cb-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="f41cb-154">La valeur de l'espace de noms est utilisée comme identificateur unique pour ce contrat et doit contenir des informations de version.</span><span class="sxs-lookup"><span data-stu-id="f41cb-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="f41cb-155">Pour plus d’informations, consultez la rubrique [Contrôle de version du service](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="f41cb-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="f41cb-156">Spécifier explicitement l'espace de noms empêche l'ajout au nom du contrat de la valeur d'espace de noms par défaut.</span><span class="sxs-lookup"><span data-stu-id="f41cb-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="f41cb-157">Dans l’interface `IImageContract`, déclarez une méthode pour une seule opération que le contrat `IImageContract` expose dans l’interface, puis appliquez l’attribut `OperationContractAttribute` à la méthode que vous souhaitez exposer dans le cadre du contrat Service Bus public.</span><span class="sxs-lookup"><span data-stu-id="f41cb-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="f41cb-158">En regard de l’attribut **OperationContract**, ajoutez la valeur **WebGet**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="f41cb-159">Cette opération permet au service de relais d’acheminer les demandes HTTP GET vers `GetImage`, et de convertir les valeurs `GetImage` renvoyées dans une réponse HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="f41cb-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="f41cb-160">Plus loin dans ce didacticiel, vous utiliserez un navigateur web pour accéder à cette méthode et pour afficher l'image dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="f41cb-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="f41cb-161">Directement après la définition de `IImageContract`, déclarez un canal qui hérite à la fois des interfaces `IImageContract` et `IClientChannel` :</span><span class="sxs-lookup"><span data-stu-id="f41cb-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="f41cb-162">Un canal est l'objet WCF par le biais duquel le service et le client se transmettent des informations.</span><span class="sxs-lookup"><span data-stu-id="f41cb-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="f41cb-163">Plus tard, vous créerez le canal dans votre application hôte.</span><span class="sxs-lookup"><span data-stu-id="f41cb-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="f41cb-164">Azure Relay utilise ensuite ce canal pour transmettre les requêtes HTTP GET du navigateur vers votre implémentation **GetImage**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="f41cb-165">Le relais utilise également ce canal pour extraire la valeur **GetImage** renvoyée et la traduire en une HTTP GETRESPONSE pour le navigateur client.</span><span class="sxs-lookup"><span data-stu-id="f41cb-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="f41cb-166">Dans le menu **Générer**, cliquez sur **Générer la solution** pour confirmer que votre travail est correct.</span><span class="sxs-lookup"><span data-stu-id="f41cb-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="f41cb-167">Exemple</span><span class="sxs-lookup"><span data-stu-id="f41cb-167">Example</span></span>
<span data-ttu-id="f41cb-168">Le code suivant montre une interface de base qui définit un contrat WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="f41cb-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="f41cb-169">Étape 3 : Implémentation d’un contrat de service REST WCF à utiliser avec Service Bus</span><span class="sxs-lookup"><span data-stu-id="f41cb-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="f41cb-170">La création d’un service WCF Relay de type REST nécessite la création au préalable du contrat défini à l’aide d’une interface.</span><span class="sxs-lookup"><span data-stu-id="f41cb-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="f41cb-171">L'étape suivante consiste à implémenter l'interface.</span><span class="sxs-lookup"><span data-stu-id="f41cb-171">The next step is to implement the interface.</span></span> <span data-ttu-id="f41cb-172">Cela implique la création d’une classe nommée **ImageService** qui implémente l’interface **IImageContract** définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f41cb-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="f41cb-173">Une fois le contrat implémenté, vous configurez ensuite l'interface à l'aide d'un fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="f41cb-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="f41cb-174">Le fichier de configuration contient les informations nécessaires à l’application, notamment le nom du service, le nom du contrat et le type de protocole utilisé pour communiquer avec le service de relais.</span><span class="sxs-lookup"><span data-stu-id="f41cb-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="f41cb-175">Le code utilisé pour effectuer ces tâches est fourni dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="f41cb-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="f41cb-176">Comme pour les étapes précédentes, il y a très peu de différences entre l’implémentation d’un contrat de type REST et un contrat WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="f41cb-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="f41cb-177">Implémentation d’un contrat Service Bus de type REST </span><span class="sxs-lookup"><span data-stu-id="f41cb-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="f41cb-178">Créez une classe nommée **ImageService** directement après la définition de l’interface **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="f41cb-179">La classe **ImageService** implémente l’interface **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="f41cb-180">Comme pour d'autres implémentations d'interface, vous pouvez implémenter la définition dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="f41cb-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="f41cb-181">Toutefois, pour ce didacticiel, l’implémentation apparaît dans le même fichier que la définition d’interface et la méthode `Main()`.</span><span class="sxs-lookup"><span data-stu-id="f41cb-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="f41cb-182">Appliquez l’attribut [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) à la classe **IImageService** pour indiquer que la classe est une implémentation d’un contrat WCF.</span><span class="sxs-lookup"><span data-stu-id="f41cb-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="f41cb-183">Comme mentionné précédemment, cet espace de noms n'est pas un espace de noms standard.</span><span class="sxs-lookup"><span data-stu-id="f41cb-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="f41cb-184">Il fait en effet partie de l'architecture WCF qui identifie le contrat.</span><span class="sxs-lookup"><span data-stu-id="f41cb-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="f41cb-185">Pour plus d’informations, consultez la rubrique [Noms des contrats de données](https://msdn.microsoft.com/library/ms731045.aspx) dans la documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="f41cb-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="f41cb-186">Ajoutez une image .jpg à votre projet.</span><span class="sxs-lookup"><span data-stu-id="f41cb-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="f41cb-187">Il s'agit d'une image que le service affiche dans le navigateur de réception.</span><span class="sxs-lookup"><span data-stu-id="f41cb-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="f41cb-188">Cliquez avec le bouton droit sur votre projet, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="f41cb-189">Cliquez ensuite sur **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-189">Then click **Existing Item**.</span></span> <span data-ttu-id="f41cb-190">Utilisez la boîte de dialogue **Ajouter un élément existant** pour accéder à un fichier .jpg approprié, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="f41cb-191">Lorsque vous ajoutez le fichier, assurez-vous que l’option **Tous les fichiers** est sélectionnée dans la liste déroulante en regard du champ **Nom de fichier :**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="f41cb-192">Le reste de ce didacticiel suppose que le nom de l'image est « image.jpg ».</span><span class="sxs-lookup"><span data-stu-id="f41cb-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="f41cb-193">Si vous avez un fichier différent, vous devrez renommer l'image ou modifier votre code pour compenser.</span><span class="sxs-lookup"><span data-stu-id="f41cb-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="f41cb-194">Pour vous assurer que le service en cours d’exécution est capable de trouver le fichier image, cliquez avec le bouton droit sur le fichier image dans **l’Explorateur de solutions**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="f41cb-195">Dans le volet **Propriétés**, définissez la valeur **Copier dans le répertoire de sortie** sur **Copier si plus récent**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="f41cb-196">Ajoutez une référence à l’assembly **System.Drawing.dll** au projet et ajoutez également les instructions `using` associées suivantes.</span><span class="sxs-lookup"><span data-stu-id="f41cb-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="f41cb-197">Dans la classe **ImageService**, ajoutez le constructeur suivant qui charge le bitmap et prépare son envoi au navigateur client.</span><span class="sxs-lookup"><span data-stu-id="f41cb-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="f41cb-198">Directement après le code précédent, ajoutez la méthode **GetImage** suivante à la classe **ImageService** afin de retourner un message HTTP contenant l’image.</span><span class="sxs-lookup"><span data-stu-id="f41cb-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="f41cb-199">Cette implémentation utilise **MemoryStream** pour récupérer l’image et la préparer pour la diffusion en continu vers le navigateur.</span><span class="sxs-lookup"><span data-stu-id="f41cb-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="f41cb-200">La diffusion en continu commence à la position zéro, déclare le contenu du flux au format jpeg et diffuse l'information.</span><span class="sxs-lookup"><span data-stu-id="f41cb-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="f41cb-201">Dans le menu **Générer**, cliquez sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="f41cb-202">Définition de la configuration pour l’exécution du service web sur Service Bus</span><span class="sxs-lookup"><span data-stu-id="f41cb-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="f41cb-203">Dans **l’Explorateur de solutions**, double-cliquez sur le fichier **App.config** pour l’ouvrir dans l’éditeur Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f41cb-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="f41cb-204">Le fichier **App.config** contient le nom du service, le point de terminaison (c’est-à-dire l’emplacement qu’Azure Relay expose aux clients et aux ordinateurs hôtes afin qu’ils communiquent entre eux) et la liaison (type de protocole utilisé pour communiquer).</span><span class="sxs-lookup"><span data-stu-id="f41cb-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="f41cb-205">La principale différence réside dans le fait que le point de terminaison de service configuré fait référence à une liaison [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding).</span><span class="sxs-lookup"><span data-stu-id="f41cb-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="f41cb-206">L’élément XML `<system.serviceModel>` est un élément WCF qui définit un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="f41cb-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="f41cb-207">Ici, il sert à définir le nom du service et le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f41cb-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="f41cb-208">En bas de l’élément `<system.serviceModel>` (mais toujours au sein de `<system.serviceModel>`), ajoutez un élément `<bindings>` avec le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="f41cb-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="f41cb-209">Cela définit les liaisons utilisées dans l'application.</span><span class="sxs-lookup"><span data-stu-id="f41cb-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="f41cb-210">Vous pouvez définir plusieurs liaisons, mais pour ce didacticiel, vous n’en définissez qu'une seule.</span><span class="sxs-lookup"><span data-stu-id="f41cb-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="f41cb-211">Le code précédent définit une liaison WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) avec **relayClientAuthenticationType** défini sur **Aucun**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="f41cb-212">Ce paramètre indique qu'un point de terminaison utilisant cette liaison ne nécessite aucune information d'identification du client.</span><span class="sxs-lookup"><span data-stu-id="f41cb-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="f41cb-213">Après l’élément `<bindings>`, ajoutez un élément `<services>`.</span><span class="sxs-lookup"><span data-stu-id="f41cb-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="f41cb-214">Comme pour les liaisons, vous pouvez définir plusieurs services dans un même fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="f41cb-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="f41cb-215">Toutefois, pour ce didacticiel, vous n’en définissez qu'un seul.</span><span class="sxs-lookup"><span data-stu-id="f41cb-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="f41cb-216">Cette étape configure un service qui utilise la valeur par défaut **webHttpRelayBinding** définie précédemment.</span><span class="sxs-lookup"><span data-stu-id="f41cb-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="f41cb-217">Il utilise également la valeur par défaut **sbTokenProvider**, définie dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="f41cb-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="f41cb-218">Après l’élément `<services>`, créez un élément `<behaviors>` avec le contenu suivant, en remplaçant « SAS_KEY » par la clé avec *signature d’accès partagé* (SAP) obtenue précédemment à partir du [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="f41cb-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="f41cb-219">Toujours dans le fichier App.config, dans l’élément `<appSettings>`, remplacez la valeur de la chaîne de connexion entière par la chaîne de connexion obtenue précédemment à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="f41cb-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="f41cb-220">Dans le menu **Générer**, cliquez sur **Générer la solution** pour générer la solution complète.</span><span class="sxs-lookup"><span data-stu-id="f41cb-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="f41cb-221">Exemple</span><span class="sxs-lookup"><span data-stu-id="f41cb-221">Example</span></span>
<span data-ttu-id="f41cb-222">Le code suivant montre l’implémentation du contrat et du service pour un service REST qui s’exécute sur Service Bus à l’aide de la liaison **WebHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="f41cb-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="f41cb-223">L'exemple suivant montre le fichier App.config associé au service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="f41cb-224">Étape 4 : Hébergement du service WCF REST pour utiliser Azure Relay</span><span class="sxs-lookup"><span data-stu-id="f41cb-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="f41cb-225">Cette étape décrit comment exécuter un service web à l’aide d’une application console avec WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="f41cb-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="f41cb-226">Une liste complète du code écrit dans cette étape est fournie dans l'exemple suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="f41cb-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="f41cb-227">Création d’une adresse de base pour le service</span><span class="sxs-lookup"><span data-stu-id="f41cb-227">To create a base address for the service</span></span>
1. <span data-ttu-id="f41cb-228">Dans la déclaration de fonction `Main()`, créez une variable pour stocker l’espace de noms de votre projet.</span><span class="sxs-lookup"><span data-stu-id="f41cb-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="f41cb-229">Assurez-vous de remplacer `yourNamespace` par le nom de l’espace de noms de service Relay créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f41cb-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="f41cb-230">Service Bus utilise le nom de votre espace de noms pour créer une adresse URI unique.</span><span class="sxs-lookup"><span data-stu-id="f41cb-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="f41cb-231">Créez une instance `Uri` pour l’adresse de base du service basé sur l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="f41cb-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="f41cb-232">Création et configuration de l'hôte de service web</span><span class="sxs-lookup"><span data-stu-id="f41cb-232">To create and configure the web service host</span></span>
* <span data-ttu-id="f41cb-233">Créez l'hôte de service web en utilisant l'adresse URI créée précédemment dans cette section.</span><span class="sxs-lookup"><span data-stu-id="f41cb-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="f41cb-234">L'hôte de service est l'objet WCF qui instancie l'application hôte.</span><span class="sxs-lookup"><span data-stu-id="f41cb-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="f41cb-235">Cet exemple transmet le type d’hôte que vous souhaitez créer (un élément **ImageService**) ainsi que l’adresse à laquelle vous souhaitez exposer l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="f41cb-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="f41cb-236">Exécution de l'hôte de service web</span><span class="sxs-lookup"><span data-stu-id="f41cb-236">To run the web service host</span></span>
1. <span data-ttu-id="f41cb-237">Ouvrez le service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="f41cb-238">Le service est maintenant actif.</span><span class="sxs-lookup"><span data-stu-id="f41cb-238">The service is now running.</span></span>
2. <span data-ttu-id="f41cb-239">Affichez un message indiquant que le service est en cours d'exécution et expliquant comment arrêter ce service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="f41cb-240">Lorsque vous avez terminé, fermez l'hôte de service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="f41cb-241">Exemple</span><span class="sxs-lookup"><span data-stu-id="f41cb-241">Example</span></span>
<span data-ttu-id="f41cb-242">L'exemple suivant inclut le contrat de service et l'implémentation des étapes précédentes du didacticiel et héberge le service dans une application console.</span><span class="sxs-lookup"><span data-stu-id="f41cb-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="f41cb-243">Compilez le code suivant dans un fichier exécutable nommé ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="f41cb-243">Compile the following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="f41cb-244">Compilation du code</span><span class="sxs-lookup"><span data-stu-id="f41cb-244">Compiling the code</span></span>
<span data-ttu-id="f41cb-245">Après avoir créé la solution, procédez comme suit pour exécuter l'application :</span><span class="sxs-lookup"><span data-stu-id="f41cb-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="f41cb-246">Appuyez sur **F5** ou accédez à l’emplacement du fichier exécutable (ImageListener\bin\Debug\ImageListener.exe), pour exécuter le service.</span><span class="sxs-lookup"><span data-stu-id="f41cb-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="f41cb-247">Ne fermez pas l’application en cours d’exécution, car l’étape suivante est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="f41cb-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="f41cb-248">Copiez et collez l'adresse à partir de l'invite de commande dans un navigateur pour afficher l'image.</span><span class="sxs-lookup"><span data-stu-id="f41cb-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="f41cb-249">Une fois que vous avez terminé, appuyez sur **Entrée** dans la fenêtre d’invite de commande pour fermer l’application.</span><span class="sxs-lookup"><span data-stu-id="f41cb-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f41cb-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f41cb-250">Next steps</span></span>
<span data-ttu-id="f41cb-251">Maintenant que vous avez créé une application qui utilise le service de relais Service Bus, consultez les articles suivants pour en savoir plus sur Azure Relay :</span><span class="sxs-lookup"><span data-stu-id="f41cb-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="f41cb-252">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="f41cb-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="f41cb-253">Vue d’ensemble d’Azure Relay</span><span class="sxs-lookup"><span data-stu-id="f41cb-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="f41cb-254">Guide pratique pour utiliser le service WCF Relay avec .NET</span><span class="sxs-lookup"><span data-stu-id="f41cb-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
