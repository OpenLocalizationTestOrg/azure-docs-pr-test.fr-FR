---
title: "didacticiel de Bus REST aaaService à l’aide de relais de Azure | Documents Microsoft"
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
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="000f7-103">Didacticiel Azure WCF Relay REST</span><span class="sxs-lookup"><span data-stu-id="000f7-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="000f7-104">Ce didacticiel explique comment toobuild un relais Azure simple héberger application qui expose une interface basée sur REST.</span><span class="sxs-lookup"><span data-stu-id="000f7-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="000f7-105">REST permet à un client web, comme un navigateur web, hello tooaccess les demandes API Service Bus via HTTP.</span><span class="sxs-lookup"><span data-stu-id="000f7-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="000f7-106">didacticiel de Hello utilise tooconstruct de modèle programmation hello REST de Windows Communication Foundation (WCF) un service REST sur le Bus de Service.</span><span class="sxs-lookup"><span data-stu-id="000f7-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="000f7-107">Pour plus d’informations, consultez [modèle de programmation WCF REST](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) et [conception et implémentation de Services](/dotnet/framework/wcf/designing-and-implementing-services) Bonjour documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="000f7-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="000f7-108">Étape 1 : Création d’un espace de noms</span><span class="sxs-lookup"><span data-stu-id="000f7-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="000f7-109">à l’aide de toobegin hello des fonctionnalités de relais dans Azure, vous devez d’abord créer un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="000f7-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="000f7-110">Un espace de noms fournit un conteneur d’étendue pour l’adressage des ressources Azure au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="000f7-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="000f7-111">Suivez hello [ici les instructions](relay-create-namespace-portal.md) toocreate un espace de noms de relais.</span><span class="sxs-lookup"><span data-stu-id="000f7-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="000f7-112">Étape 2 : Définir un toouse de contrat de service WCF de basée sur REST avec Azure relais</span><span class="sxs-lookup"><span data-stu-id="000f7-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="000f7-113">Lorsque vous créez un service WCF REST-style, vous devez définir le contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="000f7-114">contrat de Hello spécifie quelles opérations hello hôte prend en charge.</span><span class="sxs-lookup"><span data-stu-id="000f7-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="000f7-115">Une opération de service peut être considérée comme une méthode de service web.</span><span class="sxs-lookup"><span data-stu-id="000f7-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="000f7-116">Les contrats sont créés en définissant une interface C++, C# ou Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="000f7-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="000f7-117">Chaque méthode dans l’interface hello correspond l’opération de service spécifique tooa.</span><span class="sxs-lookup"><span data-stu-id="000f7-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="000f7-118">Hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribut doit être appliqué tooeach interface et hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) l’attribut doit être appliqué tooeach opération.</span><span class="sxs-lookup"><span data-stu-id="000f7-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="000f7-119">Si une méthode dans une interface qui possède hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) n’a pas de hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), cette méthode n’est pas exposée.</span><span class="sxs-lookup"><span data-stu-id="000f7-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="000f7-120">code Hello utilisé pour ces tâches est indiqué dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="000f7-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="000f7-121">Hello principale différence entre un contrat WCF et d’un contrat de type REST est Ajout de hello d’une propriété de toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="000f7-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="000f7-122">Cette propriété permet de vous toomap une méthode dans la méthode d’interface tooa sur hello autre côté de l’interface de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="000f7-123">Dans ce cas, nous allons utiliser [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink un tooHTTP de la méthode GET.</span><span class="sxs-lookup"><span data-stu-id="000f7-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="000f7-124">Cela permet à Service Bus tooaccurately récupérer et d’interpréter les commandes envoyées toohello interface.</span><span class="sxs-lookup"><span data-stu-id="000f7-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="000f7-125">toocreate un contrat avec une interface</span><span class="sxs-lookup"><span data-stu-id="000f7-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="000f7-126">Ouvrez Visual Studio en tant qu’administrateur : programme de hello avec le bouton droit dans hello **Démarrer** menu, puis sur **exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="000f7-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="000f7-127">Créez un projet d’application de console.</span><span class="sxs-lookup"><span data-stu-id="000f7-127">Create a new console application project.</span></span> <span data-ttu-id="000f7-128">Cliquez sur hello **fichier** menu et sélectionnez **nouveau**, puis sélectionnez **projet**.</span><span class="sxs-lookup"><span data-stu-id="000f7-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="000f7-129">Bonjour **nouveau projet** boîte de dialogue, cliquez sur **Visual C#**, sélectionnez hello **Application Console** modèle et nommez-le **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="000f7-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="000f7-130">Utiliser la valeur par défaut hello **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="000f7-130">Use hello default **Location**.</span></span> <span data-ttu-id="000f7-131">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="000f7-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="000f7-132">Pour un projet C#, Visual Studio crée un fichier `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="000f7-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="000f7-133">Cette classe contient vide `Main()` méthode, requis pour un toobuild de projet d’application console correctement.</span><span class="sxs-lookup"><span data-stu-id="000f7-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="000f7-134">Ajouter des références tooService Bus et **System.ServiceModel.dll** projet toohello en installant le package NuGet Service Bus de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="000f7-135">Ce package ajoute automatiquement des références toohello Service Bus bibliothèques, ainsi que hello WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="000f7-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="000f7-136">Dans l’Explorateur de solutions, cliquez sur hello **ImageListener** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="000f7-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="000f7-137">Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="000f7-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="000f7-138">Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="000f7-139">Vous devez ajouter explicitement une référence trop**System.ServiceModel.Web.dll** toohello projet :</span><span class="sxs-lookup"><span data-stu-id="000f7-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="000f7-140">a.</span><span class="sxs-lookup"><span data-stu-id="000f7-140">a.</span></span> <span data-ttu-id="000f7-141">Dans l’Explorateur de solutions, cliquez sur hello **références** dossier sous le dossier du projet hello, puis cliquez sur **ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="000f7-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="000f7-142">b.</span><span class="sxs-lookup"><span data-stu-id="000f7-142">b.</span></span> <span data-ttu-id="000f7-143">Bonjour **ajouter une référence** boîte de dialogue, cliquez sur hello **Framework** onglet sur le côté gauche de hello et Bonjour **recherche** , tapez **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="000f7-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="000f7-144">Sélectionnez hello **System.ServiceModel.Web** case à cocher, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="000f7-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="000f7-145">Ajoutez hello suit `using` instructions haut hello du fichier Program.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="000f7-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) est l’espace de noms hello qui active l’accès par programme des fonctions toobasic de WCF.</span><span class="sxs-lookup"><span data-stu-id="000f7-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="000f7-147">Relais de WCF utilise de nombreux hello objets et les attributs des contrats de service WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="000f7-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="000f7-148">Vous utiliserez cet espace de noms dans la plupart de vos applications de relais.</span><span class="sxs-lookup"><span data-stu-id="000f7-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="000f7-149">De même, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) permettent de définir canal hello, qui est l’objet hello par le biais duquel vous communiquez avec le navigateur web du client relais d’Azure et hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="000f7-150">Enfin, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contient les types de hello qui vous permettent de toocreate les applications Web.</span><span class="sxs-lookup"><span data-stu-id="000f7-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="000f7-151">Renommer hello `ImageListener` espace de noms trop**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="000f7-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="000f7-152">Directement après hello accolade de déclaration d’espace de noms hello, définir une nouvelle interface nommée **IImageContract** et appliquer hello **ServiceContractAttribute** interface de toohello d’attribut avec un valeur de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="000f7-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="000f7-153">valeur d’espace de noms Hello diffère de l’espace de noms hello que vous utilisez dans la portée de votre code hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="000f7-154">valeur d’espace de noms Hello est utilisée comme identificateur unique pour ce contrat et doit disposer d’informations de version.</span><span class="sxs-lookup"><span data-stu-id="000f7-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="000f7-155">Pour plus d’informations, consultez la rubrique [Contrôle de version des services](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="000f7-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="000f7-156">Une spécification explicite de l’espace de noms hello empêche l’espace de noms par défaut hello Ajout toohello le nom de contrat.</span><span class="sxs-lookup"><span data-stu-id="000f7-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="000f7-157">Au sein de hello `IImageContract` l’interface, déclarez une méthode pour hello d’opération unique hello `IImageContract` expose contrat Bonjour interface et appliquez hello `OperationContractAttribute` attribut méthode toohello que vous souhaitez tooexpose dans le cadre de hello public Service Bus contrat.</span><span class="sxs-lookup"><span data-stu-id="000f7-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="000f7-158">Bonjour **OperationContract** d’attribut, ajouter hello **WebGet** valeur.</span><span class="sxs-lookup"><span data-stu-id="000f7-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="000f7-159">Cette opération active hello tooroute de service de relais HTTP GET demande trop`GetImage`et hello tootranslate retournent des valeurs de `GetImage` dans une réponse HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="000f7-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="000f7-160">Plus loin dans le didacticiel de hello, vous allez utiliser un tooaccess de navigateur web de cette méthode et une image de hello toodisplay dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="000f7-161">Directement après hello `IImageContract` définition, déclarez un canal qui hérite à la fois hello `IImageContract` et `IClientChannel` interfaces.</span><span class="sxs-lookup"><span data-stu-id="000f7-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="000f7-162">Un canal est l’objet WCF de hello via lequel client et le service de hello transmettent informations tooeach autres.</span><span class="sxs-lookup"><span data-stu-id="000f7-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="000f7-163">Une version ultérieure, vous allez créer le canal de hello dans votre application hôte.</span><span class="sxs-lookup"><span data-stu-id="000f7-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="000f7-164">Relais Azure utilise ensuite ce canal toopass hello requêtes GET HTTP hello navigateur tooyour **GetImage** implémentation.</span><span class="sxs-lookup"><span data-stu-id="000f7-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="000f7-165">relais de Hello utilise également hello de hello canal tootake **GetImage** valeur de retour et la traduire en réponse HTTP GETRESPONSE du navigateur client hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="000f7-166">À partir de hello **générer** menu, cliquez sur **générer la Solution** précision de hello tooconfirm de votre travail jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="000f7-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="000f7-167">Exemple</span><span class="sxs-lookup"><span data-stu-id="000f7-167">Example</span></span>
<span data-ttu-id="000f7-168">Hello suivant de code montre une interface de base qui définit un contrat WCF relais.</span><span class="sxs-lookup"><span data-stu-id="000f7-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="000f7-169">Étape 3 : Implémenter un toouse de contrat de service WCF de basée sur REST Service Bus</span><span class="sxs-lookup"><span data-stu-id="000f7-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="000f7-170">Création d’un service de relais WCF de type REST nécessite que vous créez tout d’abord le contrat hello, qui est défini à l’aide d’une interface.</span><span class="sxs-lookup"><span data-stu-id="000f7-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="000f7-171">étape suivante de Hello est interface de hello tooimplement.</span><span class="sxs-lookup"><span data-stu-id="000f7-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="000f7-172">Cela implique la création d’une classe nommée **ImageService** qui implémente hello défini par l’utilisateur **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="000f7-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="000f7-173">Une fois que vous implémentez le contrat de hello, vous configurez interface hello à l’aide d’un fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="000f7-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="000f7-174">fichier de configuration Hello contient les informations nécessaires pour l’application hello, telles que nom hello du service de hello, nom hello du contrat de hello et type hello du protocole est toocommunicate utilisé avec le service de relais hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="000f7-175">code de Hello utilisé pour ces tâches est fourni dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="000f7-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="000f7-176">Comme les étapes précédentes hello, il existe très peu de différences entre l’implémentation d’un contrat de type REST et un contrat de relais de WCF.</span><span class="sxs-lookup"><span data-stu-id="000f7-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="000f7-177">contrat de Service Bus tooimplement un style de REST</span><span class="sxs-lookup"><span data-stu-id="000f7-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="000f7-178">Créer une nouvelle classe nommée **ImageService** directement après la définition de hello Hello **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="000f7-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="000f7-179">Hello **ImageService** classe implémente hello **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="000f7-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="000f7-180">Implémentations d’interface tooother similaires, vous pouvez implémenter la définition de hello dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="000f7-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="000f7-181">Toutefois, pour ce didacticiel, mise en œuvre hello s’affiche dans hello même fichier en tant que définition d’interface hello et `Main()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="000f7-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="000f7-182">Appliquer hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribut toohello **IImageService** tooindicate de classe qui hello classe est une implémentation d’un contrat WCF.</span><span class="sxs-lookup"><span data-stu-id="000f7-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="000f7-183">Comme mentionné précédemment, cet espace de noms n'est pas un espace de noms standard.</span><span class="sxs-lookup"><span data-stu-id="000f7-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="000f7-184">Au lieu de cela, il fait partie de la hello architecture WCF qui identifie le contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="000f7-185">Pour plus d’informations, consultez hello [les noms de contrat de données](https://msdn.microsoft.com/library/ms731045.aspx) rubrique Bonjour documentation WCF.</span><span class="sxs-lookup"><span data-stu-id="000f7-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="000f7-186">Ajoutez un projet de tooyour image .jpg.</span><span class="sxs-lookup"><span data-stu-id="000f7-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="000f7-187">Il s’agit d’une image par hello service Bonjour réception de navigateur.</span><span class="sxs-lookup"><span data-stu-id="000f7-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="000f7-188">Cliquez avec le bouton droit sur votre projet, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="000f7-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="000f7-189">Cliquez ensuite sur **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="000f7-189">Then click **Existing Item**.</span></span> <span data-ttu-id="000f7-190">Hello d’utilisation **ajouter un élément existant** tooan de toobrowse de boîte de dialogue appropriée .jpg, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="000f7-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="000f7-191">Lorsque vous ajoutez un fichier de hello, assurez-vous que **tous les fichiers** est sélectionné dans toohello suivant de liste déroulante hello **nom de fichier :** champ.</span><span class="sxs-lookup"><span data-stu-id="000f7-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="000f7-192">reste Hello de ce didacticiel part du principe que hello nom d’image de hello est « image.jpg ».</span><span class="sxs-lookup"><span data-stu-id="000f7-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="000f7-193">Si vous avez un autre fichier, vous ont image de hello toorename, ou modifier votre toocompensate de code.</span><span class="sxs-lookup"><span data-stu-id="000f7-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="000f7-194">toomake que ce service en cours d’exécution de hello trouverez hello image fichier, en **l’Explorateur de solutions** avec le bouton droit de fichier d’image hello, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="000f7-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="000f7-195">Bonjour **propriétés** volet, définissez **copier tooOutput active** trop**Copier si plus récent**.</span><span class="sxs-lookup"><span data-stu-id="000f7-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="000f7-196">Ajouter une référence toohello **System.Drawing.dll** toohello de l’assembly de projet et également ajouter suivant hello associés `using` instructions.</span><span class="sxs-lookup"><span data-stu-id="000f7-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="000f7-197">Bonjour **ImageService** classe, ajoutez hello suivants constructeur que les charges hello bitmap et prépare toosend toohello navigateur du client.</span><span class="sxs-lookup"><span data-stu-id="000f7-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
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
7. <span data-ttu-id="000f7-198">Directement après le code précédent de hello, ajoutez hello suivant **GetImage** méthode Bonjour **ImageService** message tooreturn HTTP de classe qui contient l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
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
   
    <span data-ttu-id="000f7-199">Cette implémentation utilise **MemoryStream** tooretrieve hello image et la préparer pour la diffusion en continu toohello navigateur.</span><span class="sxs-lookup"><span data-stu-id="000f7-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="000f7-200">Démarre la position du flux hello à zéro, déclare le contenu du flux au format jpeg hello et transmet les informations de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="000f7-201">À partir de hello **générer** menu, cliquez sur **générer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="000f7-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="000f7-202">configuration de hello toodefine pour l’exécution du service web de hello sur Service Bus</span><span class="sxs-lookup"><span data-stu-id="000f7-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="000f7-203">Dans **l’Explorateur de solutions**, double-cliquez sur **App.config** tooopen dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="000f7-204">Hello **App.config** fichier inclut le nom du service hello, point de terminaison (autrement dit, hello emplacement du relais de Azure expose pour que les clients et les hôtes toocommunicate entre eux) et liaison (type hello du protocole qui est utilisé toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="000f7-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="000f7-205">Hello principale différence ici est ce point de terminaison de service hello configuré fait référence tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) liaison.</span><span class="sxs-lookup"><span data-stu-id="000f7-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="000f7-206">Hello `<system.serviceModel>` XML est un élément WCF qui définit un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="000f7-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="000f7-207">Ici, il est le point de terminaison et le nom du service utilisé toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="000f7-208">Bas hello hello `<system.serviceModel>` élément (mais toujours compris `<system.serviceModel>`), ajoutez un `<bindings>` élément ayant hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="000f7-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="000f7-209">Définit les liaisons hello utilisées dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="000f7-210">Vous pouvez définir plusieurs liaisons, mais pour ce didacticiel, vous n’en définissez qu'une seule.</span><span class="sxs-lookup"><span data-stu-id="000f7-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="000f7-211">code de précédent Hello définit un relais WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) la liaison avec **relayClientAuthenticationType** défini trop**aucun**.</span><span class="sxs-lookup"><span data-stu-id="000f7-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="000f7-212">Ce paramètre indique qu'un point de terminaison utilisant cette liaison ne nécessite aucune information d'identification du client.</span><span class="sxs-lookup"><span data-stu-id="000f7-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="000f7-213">Après avoir hello `<bindings>` élément, ajouter un `<services>` élément.</span><span class="sxs-lookup"><span data-stu-id="000f7-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="000f7-214">Les liaisons toohello similaires, vous pouvez définir plusieurs services dans un seul fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="000f7-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="000f7-215">Toutefois, pour ce didacticiel, vous n’en définissez qu'un seul.</span><span class="sxs-lookup"><span data-stu-id="000f7-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="000f7-216">Cette étape configure un service qui utilise la valeur par défaut hello défini précédemment **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="000f7-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="000f7-217">Il utilise également la valeur par défaut hello **sbTokenProvider**, qui est défini dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="000f7-218">Après avoir hello `<services>` élément, créer un `<behaviors>` élément avec hello suivant le contenu, en remplaçant « SAS_KEY » avec hello *Signature d’accès partagé* clé (SAS) vous avez préalablement obtenu à partir de hello [portail Azure ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="000f7-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="000f7-219">Toujours dans le fichier App.config, Bonjour `<appSettings>` élément, la valeur de chaîne de connexion entière de hello remplacer avec la chaîne de connexion hello obtenu à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="000f7-220">À partir de hello **générer** menu, cliquez sur **générer la Solution** toobuild hello ensemble de la solution.</span><span class="sxs-lookup"><span data-stu-id="000f7-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="000f7-221">Exemple</span><span class="sxs-lookup"><span data-stu-id="000f7-221">Example</span></span>
<span data-ttu-id="000f7-222">implémentation du service et de contrat hello pour un service basé sur REST qui est en cours d’exécution sur le Bus de Service à l’aide de hello affiche Hello suivant **WebHttpRelayBinding** liaison.</span><span class="sxs-lookup"><span data-stu-id="000f7-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="000f7-223">Hello suivant montre fichier App.config de hello associé hello service.</span><span class="sxs-lookup"><span data-stu-id="000f7-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
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

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="000f7-224">Étape 4 : Hôte hello basée sur REST de WCF service toouse Azure relais</span><span class="sxs-lookup"><span data-stu-id="000f7-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="000f7-225">Cette étape décrit comment toorun un site web de service à l’aide d’une application console avec WCF relais.</span><span class="sxs-lookup"><span data-stu-id="000f7-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="000f7-226">Une liste complète de code hello écrite dans cette étape est fournie dans l’exemple hello hello procédure.</span><span class="sxs-lookup"><span data-stu-id="000f7-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="000f7-227">toocreate une adresse de base pour le service de hello</span><span class="sxs-lookup"><span data-stu-id="000f7-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="000f7-228">Bonjour `Main()` déclaration de fonction, de créer un espace de noms toostore variable hello de votre projet.</span><span class="sxs-lookup"><span data-stu-id="000f7-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="000f7-229">Assurez-vous que tooreplace `yourNamespace` nom hello d’espace de noms de relais hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="000f7-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="000f7-230">Service Bus utilise le nom hello de votre espace de noms de toocreate un URI unique.</span><span class="sxs-lookup"><span data-stu-id="000f7-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="000f7-231">Créer un `Uri` instance hello adresse de base du service de hello qui est basé sur l’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="000f7-232">toocreate et configurer l’hôte de service web hello</span><span class="sxs-lookup"><span data-stu-id="000f7-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="000f7-233">Créer un hôte de service web hello, à l’aide d’adresse d’URI hello créé précédemment dans cette section.</span><span class="sxs-lookup"><span data-stu-id="000f7-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="000f7-234">hôte de service Hello est un objet hello WCF qui instancie l’application hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="000f7-235">Cet exemple transmet les type hello d’hôte souhaité toocreate (un **ImageService**), et également hello adresse auquel vous souhaitez que l’application hôte de hello tooexpose.</span><span class="sxs-lookup"><span data-stu-id="000f7-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="000f7-236">hôte de service web toorun hello</span><span class="sxs-lookup"><span data-stu-id="000f7-236">toorun hello web service host</span></span>
1. <span data-ttu-id="000f7-237">Ouvrez hello service.</span><span class="sxs-lookup"><span data-stu-id="000f7-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="000f7-238">service de Hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="000f7-238">hello service is now running.</span></span>
2. <span data-ttu-id="000f7-239">Afficher un message indiquant que hello service s’exécute, et comment toostop hello service.</span><span class="sxs-lookup"><span data-stu-id="000f7-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="000f7-240">Lorsque vous avez terminé, fermez l’hôte de service hello.</span><span class="sxs-lookup"><span data-stu-id="000f7-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="000f7-241">Exemple</span><span class="sxs-lookup"><span data-stu-id="000f7-241">Example</span></span>
<span data-ttu-id="000f7-242">Hello, l’exemple suivant inclut le contrat de service hello et l’implémentation des étapes précédentes dans hello didacticiel et héberge hello le service dans une application console.</span><span class="sxs-lookup"><span data-stu-id="000f7-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="000f7-243">Compilez hello après le code dans un fichier exécutable nommé ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="000f7-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="000f7-244">Compiler le code hello</span><span class="sxs-lookup"><span data-stu-id="000f7-244">Compiling hello code</span></span>
<span data-ttu-id="000f7-245">Après avoir généré la solution de hello, procédez comme hello suivant toorun hello application :</span><span class="sxs-lookup"><span data-stu-id="000f7-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="000f7-246">Appuyez sur **F5**, ou recherchez l’emplacement du fichier exécutable toohello (ImageListener\bin\Debug\ImageListener.exe), service de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="000f7-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="000f7-247">Conserver en cours d’exécution application hello, étape suivante de tooperform hello est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="000f7-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="000f7-248">Copiez et collez l’adresse hello à partir de l’invite de commandes hello dans une image de hello toosee navigateur.</span><span class="sxs-lookup"><span data-stu-id="000f7-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="000f7-249">Lorsque vous avez terminé, appuyez sur **entrée** dans fenêtre d’invite de commandes hello tooclose hello application.</span><span class="sxs-lookup"><span data-stu-id="000f7-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="000f7-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="000f7-250">Next steps</span></span>
<span data-ttu-id="000f7-251">Maintenant que vous avez créé une application qui utilise le service de relais Service Bus hello, consultez hello suivant toolearn articles plus sur Azure relais :</span><span class="sxs-lookup"><span data-stu-id="000f7-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="000f7-252">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="000f7-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="000f7-253">Vue d’ensemble d’Azure Relay</span><span class="sxs-lookup"><span data-stu-id="000f7-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="000f7-254">Comment toouse hello WCF de relais service avec .NET</span><span class="sxs-lookup"><span data-stu-id="000f7-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
