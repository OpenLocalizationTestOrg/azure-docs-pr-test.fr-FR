---
title: Application hybride Azure WCF Relay locale/dans le cloud (.NET) | Microsoft Docs
description: "Découvrez comment créer une application hybride locale/de cloud .NET à l’aide d’Azure WCF Relay."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="82a0e-103">Application .NET locale/de cloud hybride avec Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="82a0e-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="82a0e-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="82a0e-104">Introduction</span></span>

<span data-ttu-id="82a0e-105">Cet article montre comment créer une application cloud hybride avec Microsoft Azure et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="82a0e-106">Le didacticiel part du principe que vous n’avez pas d’expérience en tant qu’utilisateur d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82a0e-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="82a0e-107">En moins de 30 minutes, vous disposez d’une application qui utilise plusieurs ressources Azure s’exécutant dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="82a0e-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="82a0e-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="82a0e-108">You will learn:</span></span>

* <span data-ttu-id="82a0e-109">créer ou adapter un service Web existant qui sera utilisé par une solution Web ;</span><span class="sxs-lookup"><span data-stu-id="82a0e-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="82a0e-110">utiliser le service Azure WCF Relay pour partager des données entre une application Azure et un service web hébergé ailleurs.</span><span class="sxs-lookup"><span data-stu-id="82a0e-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="82a0e-111">Avantages de l’utilisation d’Azure Relay pour les solutions hybrides</span><span class="sxs-lookup"><span data-stu-id="82a0e-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="82a0e-112">Les solutions d'entreprise se composent généralement d'une combinaison de code personnalisé écrit pour répondre aux exigences nouvelles et uniques de l'entreprise ainsi qu'aux fonctionnalités existantes offertes par des solutions et des systèmes déjà en place.</span><span class="sxs-lookup"><span data-stu-id="82a0e-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="82a0e-113">Les architectes de solutions commencent à utiliser le cloud, car celui-ci permet de gérer plus facilement les exigences de mise à l'échelle tout en offrant des coûts opérationnels faibles.</span><span class="sxs-lookup"><span data-stu-id="82a0e-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="82a0e-114">Ainsi, ils découvrent que les ressources des services existants qu'ils souhaiteraient exploiter comme des blocs de construction pour leurs solutions se situent à l'intérieur du pare-feu d'entreprise et hors de portée pour une solution cloud.</span><span class="sxs-lookup"><span data-stu-id="82a0e-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="82a0e-115">Bon nombre de services internes ne sont pas créés ni hébergés pour être facilement exposés dans le périmètre du réseau d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="82a0e-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="82a0e-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) est conçu pour rendre accessibles les services web WCF (Windows Communication Foundation) existants, d’une manière sécurisée, aux solutions qui résident à l’extérieur du périmètre de l’entreprise, sans exiger de modifications intrusives de l’infrastructure de réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="82a0e-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="82a0e-117">Ces services de relais sont toujours hébergés dans leur environnement existant, mais ils délèguent l’écoute des sessions et demandes entrantes au service de relais hébergé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="82a0e-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="82a0e-118">Azure Relay protège également ces services de tout accès non autorisé à l’aide de l’authentification par [signature d’accès partagé](../service-bus-messaging/service-bus-sas.md) (SAP).</span><span class="sxs-lookup"><span data-stu-id="82a0e-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="82a0e-119">Scénario de la solution</span><span class="sxs-lookup"><span data-stu-id="82a0e-119">Solution scenario</span></span>
<span data-ttu-id="82a0e-120">Dans ce didacticiel, vous allez créer un site web ASP.NET qui vous permet de voir une liste de produits sur la page d’inventaire des produits.</span><span class="sxs-lookup"><span data-stu-id="82a0e-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="82a0e-121">Ce didacticiel part du principe que vous disposez des informations sur les produits dans un système local existant, et utilise Azure Relay pour atteindre ce système.</span><span class="sxs-lookup"><span data-stu-id="82a0e-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="82a0e-122">La simulation met en scène un service Web exécuté dans une simple application console et appuyé par un ensemble de produits en mémoire.</span><span class="sxs-lookup"><span data-stu-id="82a0e-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="82a0e-123">Vous allez pouvoir exécuter cette application console sur votre propre ordinateur et déployer le rôle Web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="82a0e-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="82a0e-124">Ainsi, vous verrez comment procède le rôle Web en cours d'exécution dans le centre de données Azure pour appeler votre ordinateur, même si ce dernier réside certainement derrière au moins un pare-feu et une couche de traduction d'adresses réseau (NAT, network address translation).</span><span class="sxs-lookup"><span data-stu-id="82a0e-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="82a0e-125">Configuration de l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="82a0e-125">Set up the development environment</span></span>

<span data-ttu-id="82a0e-126">Avant de commencer à développer votre application Azure, téléchargez les outils et configurez votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="82a0e-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="82a0e-127">Installez le Kit de développement logiciel (SDK) Azure pour .NET depuis la page des [téléchargements SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="82a0e-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="82a0e-128">Dans la colonne **.NET**, cliquez sur la version correspondant à votre version de [Visual Studio](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="82a0e-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="82a0e-129">Les étapes de ce didacticiel utilisent Visual Studio 2015, mais elles fonctionnent également avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="82a0e-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="82a0e-130">Lorsque vous êtes invité à exécuter ou à enregistrer le programme d’installation, cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="82a0e-131">Dans **Web Platform Installer**, cliquez sur **Installer**, puis poursuivez l’installation.</span><span class="sxs-lookup"><span data-stu-id="82a0e-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="82a0e-132">Une fois l’installation terminée, vous disposez de tous les éléments nécessaires pour commencer le développement de l’application.</span><span class="sxs-lookup"><span data-stu-id="82a0e-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="82a0e-133">Le Kit de développement logiciel (SDK) comprend des outils qui vous permettent de facilement développer des applications Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="82a0e-134">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="82a0e-134">Create a namespace</span></span>

<span data-ttu-id="82a0e-135">Pour commencer à utiliser les fonctionnalités de relais dans Azure, vous devez d’abord créer un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="82a0e-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="82a0e-136">Un espace de noms fournit un conteneur d’étendue pour l’adressage des ressources Azure au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="82a0e-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="82a0e-137">Suivez les [instructions fournies ici](relay-create-namespace-portal.md) pour créer un espace de noms Relay.</span><span class="sxs-lookup"><span data-stu-id="82a0e-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="82a0e-138">Création d’un serveur local</span><span class="sxs-lookup"><span data-stu-id="82a0e-138">Create an on-premises server</span></span>

<span data-ttu-id="82a0e-139">Vous créez d'abord un système local de catalogue de produits (fictif).</span><span class="sxs-lookup"><span data-stu-id="82a0e-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="82a0e-140">Cela est assez simple : représentez-vous un système réel de catalogue de produits local avec une surface complète de services que nous essayons d'intégrer.</span><span class="sxs-lookup"><span data-stu-id="82a0e-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="82a0e-141">Ce projet est une application console Visual Studio et utilise le [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) pour inclure les bibliothèques et les paramètres de configuration Service Bus.</span><span class="sxs-lookup"><span data-stu-id="82a0e-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="82a0e-142">Création du projet</span><span class="sxs-lookup"><span data-stu-id="82a0e-142">Create the project</span></span>

1. <span data-ttu-id="82a0e-143">Avec les privilèges d’administrateur, démarrez Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="82a0e-144">Pour cela, cliquez avec le bouton droit sur l’icône de programme Visual Studio, puis cliquez sur **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="82a0e-145">Dans Visual Studio, dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="82a0e-146">Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="82a0e-147">Dans la zone **Nom**, saisissez le nom **ProductsServer** :</span><span class="sxs-lookup"><span data-stu-id="82a0e-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="82a0e-148">Cliquez sur **OK** pour créer le projet **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="82a0e-149">Si vous avez déjà installé le gestionnaire de package NuGet pour Visual Studio, passez à l'étape suivante.</span><span class="sxs-lookup"><span data-stu-id="82a0e-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="82a0e-150">Sinon, accédez à [NuGet][NuGet], puis cliquez sur [Installer NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span><span class="sxs-lookup"><span data-stu-id="82a0e-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="82a0e-151">Suivez les invites pour installer le gestionnaire de package NuGet, puis redémarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="82a0e-152">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet**ProductsServer**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="82a0e-153">Cliquez sur l’onglet **Parcourir**, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="82a0e-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="82a0e-154">Sélectionnez le package **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="82a0e-155">Cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="82a0e-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="82a0e-156">Notez que les assemblys client nécessaires sont maintenant référencés.</span><span class="sxs-lookup"><span data-stu-id="82a0e-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="82a0e-157">Ajoutez une nouvelle classe pour votre contrat de produit.</span><span class="sxs-lookup"><span data-stu-id="82a0e-157">Add a new class for your product contract.</span></span> <span data-ttu-id="82a0e-158">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ProductsServer** et cliquez sur **Ajouter**, puis sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="82a0e-159">Dans la zone **Nom**, saisissez le nom **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="82a0e-160">Cliquez ensuite sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-160">Then click **Add**.</span></span>
10. <span data-ttu-id="82a0e-161">Dans **ProductsContract.cs**, remplacez la définition d’espace de noms existante par le code suivant, qui définit le contrat du service.</span><span class="sxs-lookup"><span data-stu-id="82a0e-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="82a0e-162">Dans Program.cs, remplacez la définition d’espace de noms existante par le code suivant, qui ajoute le service de profil et l’hôte correspondant :</span><span class="sxs-lookup"><span data-stu-id="82a0e-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="82a0e-163">Dans l’Explorateur de solutions, double-cliquez sur le fichier **App.config** pour l’ouvrir dans l’éditeur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="82a0e-164">En bas de l’élément `<system.ServiceModel>` (mais toujours au sein de `<system.ServiceModel>`), ajoutez le code XML suivant.</span><span class="sxs-lookup"><span data-stu-id="82a0e-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="82a0e-165">Veillez à remplacer *yourServiceNamespace* par le nom de votre espace de noms, et *yourKey*, par la clé SAS que vous avez récupérée précédemment sur le portail :</span><span class="sxs-lookup"><span data-stu-id="82a0e-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="82a0e-166">Toujours dans le fichier App.config, dans l’élément `<appSettings>`, remplacez la valeur de la chaîne de connexion par la chaîne de connexion obtenue précédemment à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="82a0e-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="82a0e-167">Appuyez sur **Ctrl+Maj+B** ou, dans le menu **Générer**, cliquez sur **Générer la solution** pour générer l’application et vérifier que votre travail est correct.</span><span class="sxs-lookup"><span data-stu-id="82a0e-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="82a0e-168">Création d’une application ASP.NET</span><span class="sxs-lookup"><span data-stu-id="82a0e-168">Create an ASP.NET application</span></span>

<span data-ttu-id="82a0e-169">Dans cette section, vous allez générer une application ASP.NET simple qui affiche des données récupérées de votre service de produit.</span><span class="sxs-lookup"><span data-stu-id="82a0e-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="82a0e-170">Création du projet</span><span class="sxs-lookup"><span data-stu-id="82a0e-170">Create the project</span></span>

1. <span data-ttu-id="82a0e-171">Vérifiez que Visual Studio fonctionne avec les privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="82a0e-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="82a0e-172">Dans Visual Studio, dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="82a0e-173">Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Application web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="82a0e-174">Nommez le projet **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="82a0e-175">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="82a0e-176">Dans la liste des **modèles ASP.NET** de la boîte de dialogue **Application web ASP.NET**, cliquez sur **MVC**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="82a0e-177">Cliquez sur le bouton **Modifier l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="82a0e-178">Dans la boîte de dialogue **Modifier l’authentification**, vérifiez que l’option **Aucune authentification** est sélectionnée et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="82a0e-179">Pour ce didacticiel, vous déployez une application qui n’a pas besoin de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82a0e-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="82a0e-180">De retour dans la boîte de dialogue **Nouvelle application web ASP.NET**, cliquez sur **OK** pour créer l’application MVC.</span><span class="sxs-lookup"><span data-stu-id="82a0e-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="82a0e-181">Vous devez maintenant configurer les ressources Azure d’une nouvelle application web.</span><span class="sxs-lookup"><span data-stu-id="82a0e-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="82a0e-182">Suivez les étapes de [publication sur Azure décrites dans cet article](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="82a0e-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="82a0e-183">Ensuite, revenez à ce didacticiel et passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="82a0e-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="82a0e-184">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Modèles**, puis cliquez sur **Ajouter** et sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="82a0e-185">Dans la zone **Nom**, saisissez le nom **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="82a0e-186">Cliquez ensuite sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="82a0e-187">Modification de l’application Web</span><span class="sxs-lookup"><span data-stu-id="82a0e-187">Modify the web application</span></span>

1. <span data-ttu-id="82a0e-188">Dans le fichier Product.cs dans Visual Studio, remplacez la définition d’espace de noms existante par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="82a0e-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="82a0e-189">Dans l’Explorateur de solutions, développez le dossier **Controllers** et double-cliquez sur le fichier **HomeController.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="82a0e-190">Dans le fichier **HomeController.cs**, remplacez la définition d’espace de noms par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="82a0e-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="82a0e-191">Dans l’Explorateur de solutions, développez le dossier Views\Shared, puis double-cliquez sur le fichier **_Layout.cshtml** pour l’ouvrir dans l’éditeur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="82a0e-192">Remplacez toutes les occurrences de **Mon application ASP.NET** par **LITWARE’s Products**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="82a0e-193">Supprimez les liens **Home**, **About** et **Contact**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="82a0e-194">Dans l’exemple suivant, supprimez le code en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="82a0e-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="82a0e-195">Dans l’Explorateur de solutions, développez le dossier Views\Home, puis double-cliquez sur le fichier **Index.cshtml** pour l’ouvrir dans l’éditeur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82a0e-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="82a0e-196">Remplacez tout le contenu du fichier par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="82a0e-196">Replace the entire contents of the file with the following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="82a0e-197">Pour vérifier la qualité de votre travail, appuyez sur **Ctrl+Maj+B** pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="82a0e-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="82a0e-198">Exécutez l’application localement.</span><span class="sxs-lookup"><span data-stu-id="82a0e-198">Run the app locally</span></span>

<span data-ttu-id="82a0e-199">Exécutez l'application afin de vérifier qu'elle fonctionne.</span><span class="sxs-lookup"><span data-stu-id="82a0e-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="82a0e-200">Assurez-vous que **ProductsPortal** est le projet actif.</span><span class="sxs-lookup"><span data-stu-id="82a0e-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="82a0e-201">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nom du projet, puis sélectionnez **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="82a0e-202">Dans Visual Studio, appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="82a0e-203">Votre application doit s’exécuter dans un navigateur :</span><span class="sxs-lookup"><span data-stu-id="82a0e-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="82a0e-204">Assemblage des éléments</span><span class="sxs-lookup"><span data-stu-id="82a0e-204">Put the pieces together</span></span>

<span data-ttu-id="82a0e-205">La prochaine étape consiste à raccorder le serveur de produits local et l’application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="82a0e-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="82a0e-206">S’il n’est pas déjà ouvert, rouvrez dans Visual Studio le projet **ProductsPortal** que vous avez créé dans la section [Création d’une application ASP.NET](#create-an-aspnet-application).</span><span class="sxs-lookup"><span data-stu-id="82a0e-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="82a0e-207">Comme vous l’avez fait dans la section « Création d’un serveur local », ajoutez le package NuGet aux références du projet.</span><span class="sxs-lookup"><span data-stu-id="82a0e-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="82a0e-208">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ProductsPortal**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="82a0e-209">Recherchez « Service Bus » et sélectionnez l’élément **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="82a0e-210">Ensuite, terminez l’installation et fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="82a0e-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="82a0e-211">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ProductsPortal**, cliquez sur **Ajouter**, puis sur **Élément existant**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="82a0e-212">Accédez au fichier **ProductsContract.cs** depuis le projet de console **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="82a0e-213">Cliquez sur ProductsContract.cs afin de le mettre en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="82a0e-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="82a0e-214">Cliquez sur la flèche vers le bas en regard de l’option **Ajouter**, puis cliquez sur **Ajouter en tant que lien**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="82a0e-215">Ouvrez à présent le fichier **HomeController.cs** dans l’éditeur Visual Studio, puis remplacez la définition d’espace de noms existante par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="82a0e-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="82a0e-216">Assurez-vous de remplacer *yourServiceNamespace* par le nom de votre espace de noms de service et *yourKey*, par votre clé SAP.</span><span class="sxs-lookup"><span data-stu-id="82a0e-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="82a0e-217">Le client peut alors appeler le service local, en renvoyant le résultat de l'appel.</span><span class="sxs-lookup"><span data-stu-id="82a0e-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare the channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="82a0e-218">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur la solution **ProductsPortal** (veillez à cliquer sur la solution et non sur le projet).</span><span class="sxs-lookup"><span data-stu-id="82a0e-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="82a0e-219">Cliquez sur **Ajouter**, puis sur **Projet existant**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="82a0e-220">Accédez au projet **ProductsServer**, puis double-cliquez sur le fichier solution **ProductsServer.csproj** pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="82a0e-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="82a0e-221">**ProductsServer** doit être en cours d’exécution pour afficher les données sur **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="82a0e-222">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur la solution **ProductsPortal**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="82a0e-223">La boîte de dialogue **Pages de propriétés** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="82a0e-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="82a0e-224">Sur le côté gauche, cliquez sur **Projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="82a0e-225">Sur le côté droit, cliquez sur **Plusieurs projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="82a0e-226">Vérifiez que **ProductsServer** et **ProductsPortal** apparaissent dans cet ordre et que leur action définie est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="82a0e-227">Toujours dans la boîte de dialogue **Propriétés**, cliquez sur **Dépendances du projet** sur le côté gauche.</span><span class="sxs-lookup"><span data-stu-id="82a0e-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="82a0e-228">Dans le menu déroulant **Projets**, cliquez sur **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="82a0e-229">Vérifiez que **ProductsPortal** n’est pas sélectionné.</span><span class="sxs-lookup"><span data-stu-id="82a0e-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="82a0e-230">Dans la liste **Projets**, cliquez sur **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="82a0e-231">Vérifiez que **ProductsServer** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="82a0e-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="82a0e-232">Cliquez sur **OK** dans la boîte de dialogue **Pages de propriétés**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="82a0e-233">Exécutez le projet localement.</span><span class="sxs-lookup"><span data-stu-id="82a0e-233">Run the project locally</span></span>

<span data-ttu-id="82a0e-234">Pour tester l’application localement dans Visual Studio, appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="82a0e-235">Le serveur local (**ProductsServer**) doit démarrer, puis l’application **ProductsPortal** doit se lancer dans une fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="82a0e-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="82a0e-236">À présent, vous voyez que l'inventaire de produits répertorie des données récupérées du système local de service de produit.</span><span class="sxs-lookup"><span data-stu-id="82a0e-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="82a0e-237">Appuyez sur **Actualiser** dans la page **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="82a0e-238">Chaque fois que vous actualisez la page, l’application de serveur affiche un message lors de l’appel de `GetProducts()` à partir de **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="82a0e-239">Fermez les deux applications avant de passer à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="82a0e-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="82a0e-240">Déploiement du projet ProductsPortal dans une application web Azure</span><span class="sxs-lookup"><span data-stu-id="82a0e-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="82a0e-241">L’étape suivante consiste à publier une nouvelle fois l’application web Azure frontale **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="82a0e-242">Effectuez les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="82a0e-242">Do the following:</span></span>

1. <span data-ttu-id="82a0e-243">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ProductsPortal**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="82a0e-244">Ensuite, cliquez sur **Publier** sur la page de **publication**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="82a0e-245">Un message d’erreur peut s’afficher dans la fenêtre du navigateur lorsque le projet web **ProductsPortal** est démarré automatiquement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="82a0e-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="82a0e-246">Ce comportement est normal. Il s’explique par le fait que l’application **ProductsServer** n’est pas encore en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="82a0e-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="82a0e-247">Copiez l’URL de l’application web déployée, car vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="82a0e-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="82a0e-248">Vous pouvez également obtenir cette URL à partir de la fenêtre Activité d’Azure App Service dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="82a0e-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="82a0e-249">Fermez la fenêtre du navigateur pour arrêter l’application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="82a0e-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="82a0e-250">Définition de ProductsPortal en tant qu’application web</span><span class="sxs-lookup"><span data-stu-id="82a0e-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="82a0e-251">Avant d’exécuter l’application dans le cloud, vous devez vous assurer que **ProductsPortal** est démarré dans Visual Studio en tant qu’application web.</span><span class="sxs-lookup"><span data-stu-id="82a0e-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="82a0e-252">Dans Visual Studio, cliquez avec le bouton droit sur le projet **ProductsPortal**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="82a0e-253">Dans la colonne de gauche, cliquez sur **Web**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="82a0e-254">Dans la section**Action de démarrage**, cliquez sur le bouton **URL de démarrage** puis, dans la zone de texte, entrez l’URL de l’application web précédemment déployée. Par exemple, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="82a0e-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="82a0e-255">Dans Visual Studio, dans le menu **Fichier**, cliquez sur **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="82a0e-256">Dans le menu Générer de Visual Studio, cliquez sur **Régénérer la solution**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="82a0e-257">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="82a0e-257">Run the application</span></span>

1. <span data-ttu-id="82a0e-258">Appuyez sur F5 pour générer et exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="82a0e-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="82a0e-259">Le serveur local (application de console **ProductsServer**) doit démarrer, puis l’application **ProductsPortal** doit se lancer dans une fenêtre de navigateur, comme le montre la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="82a0e-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="82a0e-260">Notez de nouveau que l’inventaire de produits répertorie les données récupérées à partir du système local du service du produit et les affiche dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="82a0e-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="82a0e-261">Vérifiez l’URL pour vous assurer que l’application **ProductsPortal** est exécutée dans le cloud comme une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="82a0e-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="82a0e-262">L’application console **ProductsServer** doit être en cours d’exécution et en mesure de fournir les données à l’application **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="82a0e-263">Si le navigateur affiche une erreur, patientez quelques secondes, le temps que **ProductsServer** se charge et affiche le message suivant.</span><span class="sxs-lookup"><span data-stu-id="82a0e-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="82a0e-264">Appuyez ensuite sur **Actualiser** dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="82a0e-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="82a0e-265">Dans le navigateur, appuyez sur **Actualiser** sur la page **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="82a0e-266">Chaque fois que vous actualisez la page, l’application de serveur affiche un message lors de l’appel de `GetProducts()` à partir de **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="82a0e-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="82a0e-267">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82a0e-267">Next steps</span></span>

<span data-ttu-id="82a0e-268">Pour en savoir plus sur Azure Relay, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="82a0e-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="82a0e-269">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="82a0e-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="82a0e-270">Utilisation de Relay</span><span class="sxs-lookup"><span data-stu-id="82a0e-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
