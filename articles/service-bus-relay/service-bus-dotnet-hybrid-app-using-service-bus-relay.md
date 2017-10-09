---
title: aaaAzure application de sur le site/cloud hybride de relais de WCF (.NET) | Documents Microsoft
description: "Découvrez comment application hybride de toocreate un .NET sur le site/cloud à l’aide de relais WCF de Azure."
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
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="ec1f1-103">Application .NET locale/de cloud hybride avec Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="ec1f1-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="ec1f1-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="ec1f1-104">Introduction</span></span>

<span data-ttu-id="ec1f1-105">Cet article explique comment toobuild hybride cloud application avec Microsoft Azure et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="ec1f1-106">didacticiel de Hello suppose que vous n’avez aucune expérience préalable à l’aide d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="ec1f1-107">Vous devez en moins de 30 minutes, une application qui utilise plusieurs ressources Azure et en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="ec1f1-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-108">You will learn:</span></span>

* <span data-ttu-id="ec1f1-109">Comment toocreate ou adapter un service web existant pour la consommation par une solution web.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="ec1f1-110">Comment les données toouse hello Azure WCF relais service tooshare entre une application Windows Azure et un service web hébergé ailleurs.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="ec1f1-111">Avantages de l’utilisation d’Azure Relay pour les solutions hybrides</span><span class="sxs-lookup"><span data-stu-id="ec1f1-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="ec1f1-112">Les solutions d’entreprise sont généralement composées d’une combinaison de code personnalisé écrit tootackle nouvelle et besoins uniques et les fonctionnalités existantes fournies par les solutions et les systèmes qui sont déjà en place.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="ec1f1-113">Architectes de solutions commencent cloud de hello toouse pour gérer plus facilement les exigences de mise à l’échelle et de réduction des coûts opérationnels.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="ec1f1-114">Ce faisant, ils recherchent que les ressources de service existantes souhaite tooleverage comme blocs de construction pour leurs solutions sont à l’intérieur du pare-feu d’entreprise de hello et à l’extérieur facile atteint pour l’accès par la solution de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="ec1f1-115">De nombreux services internes ne sont pas créées ou hébergées de façon qu’elles peuvent être facilement exposées en périphérie du réseau d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="ec1f1-116">[Relais Azure](https://azure.microsoft.com/services/service-bus/) est conçu pour hello cas d’utilisation des services web de Windows Communication Foundation (WCF) existants et de les mettre des services accessibles en toute sécurité toosolutions qui résident en dehors du périmètre de l’entreprise hello sans nécessiter de infrastructure de réseau d’entreprise toohello modifications contraignant.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="ec1f1-117">Ces services de relais se trouvent toujours dans leur environnement existant, mais ils déléguer l’écoute entrant sessions et demandes toohello hébergé dans le cloud service de relais.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="ec1f1-118">Azure Relay protège également ces services de tout accès non autorisé à l’aide de l’authentification par [signature d’accès partagé](../service-bus-messaging/service-bus-sas.md) (SAP).</span><span class="sxs-lookup"><span data-stu-id="ec1f1-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="ec1f1-119">Scénario de la solution</span><span class="sxs-lookup"><span data-stu-id="ec1f1-119">Solution scenario</span></span>
<span data-ttu-id="ec1f1-120">Dans ce didacticiel, vous allez créer un site Web ASP.NET qui permet de vous toosee une liste de produits dans la page stock de produit hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="ec1f1-121">Hello est supposé contenir des informations produit dans un système local existant et d’utilise Azure relais tooreach dans ce système.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="ec1f1-122">La simulation met en scène un service Web exécuté dans une simple application console et appuyé par un ensemble de produits en mémoire.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="ec1f1-123">Vous toorun en mesure de cette application de console sur votre ordinateur et déployez un rôle web de hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="ec1f1-124">En procédant ainsi, vous verrez comment les rôles de web hello en hello centre de données Azure appellera en effet sur votre ordinateur, même si votre ordinateur se trouvera certainement derrière des pare-feu au moins une et une couche de traduction d’adresse réseau.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="ec1f1-125">Configuration d’environnement de développement hello</span><span class="sxs-lookup"><span data-stu-id="ec1f1-125">Set up hello development environment</span></span>

<span data-ttu-id="ec1f1-126">Avant de commencer à développer des applications Azure, téléchargez les outils hello et configurer votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="ec1f1-127">Installer hello Azure SDK pour .NET à partir de hello SDK [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ec1f1-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="ec1f1-128">Bonjour **.NET** colonne, cliquez sur la version de hello de [Visual Studio](http://www.visualstudio.com) que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="ec1f1-129">Hello étapes dans ce didacticiel, utilisez Visual Studio 2015, mais ils fonctionnent également avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="ec1f1-130">Lorsque vous y êtes invité toorun ou enregistrer le programme d’installation Bonjour, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="ec1f1-131">Bonjour **Web Platform Installer**, cliquez sur **installer** et poursuivre l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="ec1f1-132">Une fois l’installation de hello est terminée, vous devez tous les éléments nécessaires toostart toodevelop hello application.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="ec1f1-133">Hello SDK inclut des outils qui vous permettent de développer facilement des applications Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="ec1f1-134">Créer un espace de noms</span><span class="sxs-lookup"><span data-stu-id="ec1f1-134">Create a namespace</span></span>

<span data-ttu-id="ec1f1-135">à l’aide de toobegin hello des fonctionnalités de relais dans Azure, vous devez d’abord créer un espace de noms de service.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="ec1f1-136">Un espace de noms fournit un conteneur d’étendue pour l’adressage des ressources Azure au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="ec1f1-137">Suivez hello [ici les instructions](relay-create-namespace-portal.md) toocreate un espace de noms de relais.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="ec1f1-138">Création d’un serveur local</span><span class="sxs-lookup"><span data-stu-id="ec1f1-138">Create an on-premises server</span></span>

<span data-ttu-id="ec1f1-139">Vous créez d'abord un système local de catalogue de produits (fictif).</span><span class="sxs-lookup"><span data-stu-id="ec1f1-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="ec1f1-140">Il sera relativement simple ; Vous pouvez voir cela comme représentant un système de catalogue produit réel local avec une surface de service complet que nous essayons de toointegrate.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="ec1f1-141">Ce projet est une application de console Visual Studio et utilise hello [package NuGet d’Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello bibliothèques Service Bus et les paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="ec1f1-142">Créer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="ec1f1-142">Create hello project</span></span>

1. <span data-ttu-id="ec1f1-143">Avec les privilèges d’administrateur, démarrez Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="ec1f1-144">toodo, cliquez sur icône du programme Visual Studio hello, puis cliquez sur **exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="ec1f1-145">Dans Visual Studio, sur hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="ec1f1-146">Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="ec1f1-147">Bonjour **nom** zone, entrez un nom hello **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="ec1f1-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="ec1f1-148">Cliquez sur **OK** toocreate hello **ProductsServer** projet.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="ec1f1-149">Si vous avez déjà installé le Gestionnaire de package NuGet hello pour Visual Studio, ignorer l’étape suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="ec1f1-150">Sinon, accédez à [NuGet][NuGet], puis cliquez sur [Installer NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span><span class="sxs-lookup"><span data-stu-id="ec1f1-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="ec1f1-151">Suivez le Gestionnaire de package NuGet hello invites tooinstall hello, puis redémarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="ec1f1-152">Dans l’Explorateur de solutions, cliquez sur hello **ProductsServer** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="ec1f1-153">Cliquez sur hello **Parcourir** onglet, puis recherchez `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="ec1f1-154">Sélectionnez hello **WindowsAzure.ServiceBus** package.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="ec1f1-155">Cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="ec1f1-156">Notez que hello client assemblys requis sont désormais référencés.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="ec1f1-157">Ajoutez une nouvelle classe pour votre contrat de produit.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-157">Add a new class for your product contract.</span></span> <span data-ttu-id="ec1f1-158">Dans l’Explorateur de solutions, cliquez sur hello **ProductsServer** projet puis cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="ec1f1-159">Bonjour **nom** zone, entrez un nom hello **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="ec1f1-160">Cliquez ensuite sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-160">Then click **Add**.</span></span>
10. <span data-ttu-id="ec1f1-161">Dans **ProductsContract.cs**, remplacer la définition d’espace de noms de hello par hello suivant de code, qui définit le contrat hello pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
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
11. <span data-ttu-id="ec1f1-162">Dans le fichier Program.cs, remplacez définition d’espace de noms hello hello suivant du code qui ajoute le service de profil hello et hôte hello pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
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

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="ec1f1-163">Dans l’Explorateur de solutions, double-cliquez sur hello **App.config** tooopen de fichiers dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="ec1f1-164">En bas de hello Hello `<system.ServiceModel>` élément (mais toujours compris `<system.ServiceModel>`), ajouter hello suivant le code XML.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="ec1f1-165">Être vraiment tooreplace *yourServiceNamespace* avec nom hello de votre espace de noms et *yourKey* avec la clé SAS hello extrait précédemment à partir du portail de hello :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

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
13. <span data-ttu-id="ec1f1-166">Toujours dans le fichier App.config, Bonjour `<appSettings>` élément, la valeur de chaîne de connexion de hello remplacer avec la chaîne de connexion hello obtenu à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="ec1f1-167">Appuyez sur **Ctrl + Maj + B** ou à partir de hello **générer** menu, cliquez sur **générer la Solution** toobuild hello application et vérifier la précision de hello de votre travail jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="ec1f1-168">Création d’une application ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ec1f1-168">Create an ASP.NET application</span></span>

<span data-ttu-id="ec1f1-169">Dans cette section, vous allez générer une application ASP.NET simple qui affiche des données récupérées de votre service de produit.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="ec1f1-170">Créer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="ec1f1-170">Create hello project</span></span>

1. <span data-ttu-id="ec1f1-171">Vérifiez que Visual Studio fonctionne avec les privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="ec1f1-172">Dans Visual Studio, sur hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="ec1f1-173">Dans **Modèles installés**, sous **Visual C#**, cliquez sur **Application web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="ec1f1-174">Projet de hello nom **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="ec1f1-175">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="ec1f1-176">À partir de hello **modèles ASP.NET** liste Bonjour **nouvelle Application Web ASP.NET** boîte de dialogue, cliquez sur **MVC**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="ec1f1-177">Cliquez sur hello **modifier l’authentification** bouton.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="ec1f1-178">Bonjour **modifier l’authentification** boîte de dialogue zone, vérifiez que **aucune authentification** est sélectionné, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="ec1f1-179">Pour ce didacticiel, vous déployez une application qui n’a pas besoin de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="ec1f1-180">Dans hello **nouvelle Application Web ASP.NET** boîte de dialogue, cliquez sur **OK** toocreate hello MVC application.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="ec1f1-181">Vous devez maintenant configurer les ressources Azure d’une nouvelle application web.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="ec1f1-182">Suivez les étapes de hello Bonjour [section tooAzure de cet article de la publication](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ec1f1-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="ec1f1-183">Ensuite, retourner toothis didacticiel et continuer toohello prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="ec1f1-184">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Modèles**, puis cliquez sur **Ajouter** et sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="ec1f1-185">Bonjour **nom** zone, entrez un nom hello **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="ec1f1-186">Cliquez ensuite sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="ec1f1-187">Modifier l’application web de hello</span><span class="sxs-lookup"><span data-stu-id="ec1f1-187">Modify hello web application</span></span>

1. <span data-ttu-id="ec1f1-188">Dans le fichier de Product.cs hello dans Visual Studio, remplacez définition d’espace de noms existante hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
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
2. <span data-ttu-id="ec1f1-189">Dans l’Explorateur de solutions, développez hello **contrôleurs** dossier, puis double-cliquez sur hello **HomeController.cs** tooopen de fichiers dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="ec1f1-190">Dans **HomeController.cs**, remplacez définition d’espace de noms existante hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="ec1f1-191">Dans l’Explorateur de solutions, développez le dossier Views\Shared de hello, puis double-cliquez sur **_Layout.cshtml** tooopen dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="ec1f1-192">Remplacez toutes les occurrences de **mon Application ASP.NET** trop**produits LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="ec1f1-193">Supprimer hello **accueil**, **sur**, et **Contact** des liens.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="ec1f1-194">Bonjour l’exemple suivant, supprimer les code hello mis en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="ec1f1-195">Dans l’Explorateur de solutions, développez le dossier Views\Home de hello, puis double-cliquez sur **Index.cshtml** tooopen dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="ec1f1-196">Remplacez hello tout contenu de fichier de hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-196">Replace hello entire contents of hello file with hello following code.</span></span>

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
8. <span data-ttu-id="ec1f1-197">précision de hello tooverify de votre travail jusqu'à présent, vous pouvez appuyer sur **Ctrl + Maj + B** projet hello de toobuild.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="ec1f1-198">Exécuter des application hello localement</span><span class="sxs-lookup"><span data-stu-id="ec1f1-198">Run hello app locally</span></span>

<span data-ttu-id="ec1f1-199">Exécutez tooverify application hello qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="ec1f1-200">Vérifiez que **ProductsPortal** est le projet actif de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="ec1f1-201">Cliquez sur le nom de projet hello dans l’Explorateur de solutions et sélectionnez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="ec1f1-202">Dans Visual Studio, appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="ec1f1-203">Votre application doit s’exécuter dans un navigateur :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="ec1f1-204">Rassembler les pièces hello</span><span class="sxs-lookup"><span data-stu-id="ec1f1-204">Put hello pieces together</span></span>

<span data-ttu-id="ec1f1-205">étape suivante de Hello est toohook serveur produits hello local hello application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="ec1f1-206">Si elle n’est pas déjà ouvert, dans Visual Studio rouvrez hello **ProductsPortal** projet que vous avez créé dans hello [créer une application ASP.NET](#create-an-aspnet-application) section.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="ec1f1-207">Étape toohello similaire dans la section « Création d’un serveur local » de hello, ajouter des références de projet hello NuGet package toohello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="ec1f1-208">Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="ec1f1-209">Recherche de « Service Bus » et sélectionnez hello **WindowsAzure.ServiceBus** élément.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="ec1f1-210">Terminer l’installation de hello, puis fermez cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="ec1f1-211">Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** de projet, puis cliquez sur **ajouter**, puis **élément existant**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="ec1f1-212">Accédez toohello **ProductsContract.cs** fichier hello **ProductsServer** projet console.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="ec1f1-213">Cliquez sur toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="ec1f1-214">Cliquez sur hello bas suivant trop**ajouter**, puis cliquez sur **ajouter en tant que lien**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="ec1f1-215">Ouvrez maintenant hello **HomeController.cs** de fichiers dans l’éditeur de Visual Studio hello et remplacez hello espace de noms définition par hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="ec1f1-216">Être vraiment tooreplace *yourServiceNamespace* avec nom hello de votre espace de noms de service et *yourKey* avec votre clé SAP.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="ec1f1-217">Cette opération activera hello client toocall hello services locaux, obtenir de résultats de l’appel de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

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
           // Declare hello channel factory.
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
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="ec1f1-218">Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** solution (Assurez-vous que tooright clic hello solution, pas hello projet).</span><span class="sxs-lookup"><span data-stu-id="ec1f1-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="ec1f1-219">Cliquez sur **Ajouter**, puis sur **Projet existant**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="ec1f1-220">Accédez toohello **ProductsServer** de projet, puis double-cliquez sur hello **ProductsServer.csproj** tooadd du fichier solution il.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="ec1f1-221">**ProductsServer** doit être en cours d’exécution dans les données de commande toodisplay hello **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="ec1f1-222">Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** solution et cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="ec1f1-223">Hello **Pages de propriétés** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="ec1f1-224">Dans hello côté gauche, cliquez sur **projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="ec1f1-225">Sur le côté droit de hello, cliquez sur **plusieurs projets de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="ec1f1-226">Vérifiez que **ProductsServer** et **ProductsPortal** apparaissent dans cet ordre, avec **Démarrer** défini en tant qu’action hello pour les deux.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="ec1f1-227">Toujours en hello **propriétés** boîte de dialogue, cliquez sur **dépendances du projet** sur hello côté gauche.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="ec1f1-228">Bonjour **projets** , cliquez sur **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="ec1f1-229">Vérifiez que **ProductsPortal** n’est pas sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="ec1f1-230">Bonjour **projets** , cliquez sur **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="ec1f1-231">Vérifiez que **ProductsServer** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="ec1f1-232">Cliquez sur **OK** Bonjour **Pages de propriétés** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="ec1f1-233">Exécutez le projet de hello localement</span><span class="sxs-lookup"><span data-stu-id="ec1f1-233">Run hello project locally</span></span>

<span data-ttu-id="ec1f1-234">Appuyez sur tootest hello localement application, dans Visual Studio **F5**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="ec1f1-235">serveur local de Hello (**ProductsServer**) doit démarrer en premier, puis hello **ProductsPortal** application doit démarrer dans une fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="ec1f1-236">Cette fois-ci, vous verrez que l’inventaire produits hello répertorie les données récupérées à partir du système de hello produit service local.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="ec1f1-237">Appuyez sur **Actualiser** sur hello **ProductsPortal** page.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="ec1f1-238">Chaque fois que vous actualisez la page de hello, vous verrez hello server application affiche un message lorsque `GetProducts()` de **ProductsServer** est appelée.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="ec1f1-239">Fermez les deux applications avant de poursuivre la procédure toohello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="ec1f1-240">Déployer le projet hello ProductsPortal tooan l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="ec1f1-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="ec1f1-241">étape suivante de Hello est toorepublish hello Azure Web app **ProductsPortal** serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="ec1f1-242">Hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-242">Do hello following:</span></span>

1. <span data-ttu-id="ec1f1-243">Dans l’Explorateur de solutions, cliquez sur hello **ProductsPortal** le projet, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="ec1f1-244">Ensuite, cliquez sur **publier** sur hello **publier** page.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ec1f1-245">Vous pouvez voir un message d’erreur dans la fenêtre du navigateur hello lorsque hello **ProductsPortal** projet web est lancé automatiquement après le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="ec1f1-246">Cela est prévu et se produit parce que hello **ProductsServer** application n’est pas encore exécuté.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="ec1f1-247">Copier l’URL de hello hello déployé l’application web, car vous en aurez besoin URL hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="ec1f1-248">Vous pouvez également obtenir cette URL à partir de la fenêtre d’activité de Service d’application Azure hello dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="ec1f1-249">Fermez Bonjour Bonjour du toostop fenêtre de navigateur exécutant l’application.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="ec1f1-250">Définition de ProductsPortal en tant qu’application web</span><span class="sxs-lookup"><span data-stu-id="ec1f1-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="ec1f1-251">Avant l’exécution de l’application hello dans le cloud de hello, vous devez vous assurer que **ProductsPortal** est lancé au sein de Visual Studio en tant qu’une application web.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="ec1f1-252">Dans Visual Studio, avec le bouton droit hello **ProductsPortal** de projet, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="ec1f1-253">Dans la colonne de gauche hello, cliquez sur **Web**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="ec1f1-254">Bonjour **Action de démarrage** , cliquez sur hello **démarrer l’URL** bouton, puis dans la zone de texte hello entrez hello URL pour votre application web déployée précédemment ; par exemple, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="ec1f1-255">À partir de hello **fichier** menu dans Visual Studio, cliquez sur **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="ec1f1-256">À partir du menu Générer de hello dans Visual Studio, cliquez sur **régénérer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="ec1f1-257">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="ec1f1-257">Run hello application</span></span>

1. <span data-ttu-id="ec1f1-258">Appuyez sur F5 toobuild et exécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="ec1f1-259">serveur local de Hello (hello **ProductsServer** application console) doit démarrer en premier, puis hello **ProductsPortal** application doit démarrer dans une fenêtre de navigateur, comme indiqué dans hello suivant l’écran capture de.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="ec1f1-260">Notez à nouveau que l’inventaire produits hello répertorie les données récupérées à partir du système de hello produit service local et les affiche dans l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="ec1f1-261">Vérifiez que hello-URL-toomake qui **ProductsPortal** est en cours d’exécution dans le cloud hello, comme une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="ec1f1-262">Hello **ProductsServer** application console doit être en cours d’exécution et en mesure de tooserve hello données toohello **ProductsPortal** application.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="ec1f1-263">Si le navigateur de hello affiche une erreur, attendez quelques secondes plus pour **ProductsServer** tooload et hello complet suivant du message.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="ec1f1-264">Appuyez sur **Actualiser** dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="ec1f1-265">Dans le navigateur de hello, appuyez sur **Actualiser** sur hello **ProductsPortal** page.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="ec1f1-266">Chaque fois que vous actualisez la page de hello, vous verrez hello server application affiche un message lorsque `GetProducts()` de **ProductsServer** est appelée.</span><span class="sxs-lookup"><span data-stu-id="ec1f1-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="ec1f1-267">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec1f1-267">Next steps</span></span>

<span data-ttu-id="ec1f1-268">toolearn en savoir plus sur Azure relais, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="ec1f1-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="ec1f1-269">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="ec1f1-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="ec1f1-270">Comment toouse de relais</span><span class="sxs-lookup"><span data-stu-id="ec1f1-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
