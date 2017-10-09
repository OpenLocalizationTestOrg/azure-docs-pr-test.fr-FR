---
title: aaaUse stockage Azure dans les applications du Windows Store | Documents Microsoft
description: "Découvrez comment toocreate du Windows Store application qui utilise le stockage d’objets Blob Azure, de file d’attente, de Table ou de fichier."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="73b91-103">Comment toouse le stockage Azure dans les applications du Windows Store</span><span class="sxs-lookup"><span data-stu-id="73b91-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="73b91-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="73b91-104">Overview</span></span>
<span data-ttu-id="73b91-105">Ce guide montre comment tooget démarrer avec le développement d’une application Windows Store qui utilise le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="73b91-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="73b91-106">Téléchargement des outils nécessaires</span><span class="sxs-lookup"><span data-stu-id="73b91-106">Download required tools</span></span>
* <span data-ttu-id="73b91-107">[Visual Studio](https://www.visualstudio.com/downloads/) rend facile toobuild, déboguer, localiser, empaqueter et déployer des applications du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="73b91-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="73b91-108">Visual Studio 2012 ou une version ultérieure est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="73b91-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="73b91-109">Hello [bibliothèque cliente de stockage Azure](https://www.nuget.org/packages/WindowsAzure.Storage) fournit une bibliothèque de classes Windows Runtime pour travailler avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="73b91-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="73b91-110">[WCF données Services Tools pour applications du Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) étend l’expérience d’ajouter une référence de Service hello avec prise en charge de OData côté client pour les applications du Windows Store dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73b91-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="73b91-111">Développement d'applications</span><span class="sxs-lookup"><span data-stu-id="73b91-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="73b91-112">Préparation</span><span class="sxs-lookup"><span data-stu-id="73b91-112">Getting ready</span></span>
<span data-ttu-id="73b91-113">Créez un projet d'application Windows Store dans Visual Studio 2012 ou version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="73b91-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="73b91-115">Ensuite, ajoutez une référence de toohello bibliothèque cliente de stockage Azure en cliquant sur **références**, puis sur **ajouter une référence**, puis accédez toohello bibliothèque cliente de stockage pour Windows Runtime que vous avez télécharger :</span><span class="sxs-lookup"><span data-stu-id="73b91-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="73b91-117">À l’aide de la bibliothèque hello avec hello Blob et les services de file d’attente</span><span class="sxs-lookup"><span data-stu-id="73b91-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="73b91-118">À ce stade, votre application est prête toocall hello services Blob et Azure file d’attente.</span><span class="sxs-lookup"><span data-stu-id="73b91-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="73b91-119">Ajoutez hello suivant **à l’aide de** instructions afin que les types de stockage Azure peuvent être référencés directement :</span><span class="sxs-lookup"><span data-stu-id="73b91-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="73b91-120">Ensuite, ajoutez une page tooyour de bouton.</span><span class="sxs-lookup"><span data-stu-id="73b91-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="73b91-121">Ajouter hello suivant code tooits **cliquez sur** événement et modifier votre méthode de gestionnaire d’événements à l’aide de hello [mot clé async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="73b91-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="73b91-122">Ce code suppose que vous disposez de deux variables de chaîne, *accountName* et *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="73b91-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="73b91-123">Ils représentent nom hello de votre compte et hello clé compte de stockage qui est associée à ce compte.</span><span class="sxs-lookup"><span data-stu-id="73b91-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="73b91-124">Générez et exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="73b91-124">Build and run hello application.</span></span> <span data-ttu-id="73b91-125">En cliquant sur bouton de hello vérifie si un conteneur nommé *container1* existe dans votre compte, puis le créer dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="73b91-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="73b91-126">À l’aide de la bibliothèque de hello hello service de Table</span><span class="sxs-lookup"><span data-stu-id="73b91-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="73b91-127">Les types qui sont toocommunicate utilisé avec le service de Table Azure hello dépendent de WCF Data Services pour la bibliothèque d’applications du Windows Store hello.</span><span class="sxs-lookup"><span data-stu-id="73b91-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="73b91-128">Ensuite, ajoutez qu'une référence toohello requis les bibliothèques WCF à l’aide de hello Console du Gestionnaire de Package :</span><span class="sxs-lookup"><span data-stu-id="73b91-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="73b91-130">Utilisez hello suivant commande toopoint toohello du Gestionnaire de Package emplacement sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="73b91-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="73b91-131">Cette commande ajoute automatiquement le projet de tooyour toutes les références requises.</span><span class="sxs-lookup"><span data-stu-id="73b91-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="73b91-132">Si vous ne souhaitez pas toouse hello Console du Gestionnaire de Package, vous pouvez ajouter un dossier de NuGet de Services de données WCF hello dans votre liste de toohello ordinateur local des sources de package et ajouter ensuite référence hello via hello l’interface utilisateur, comme décrit dans [la gestion de l’aide de Packages NuGet boîte de dialogue de Hello](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="73b91-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="73b91-133">Lorsque vous avez référencé package NuGet de Services de données WCF de hello, modifiez le code hello dans votre bouton **cliquez sur** événement :</span><span class="sxs-lookup"><span data-stu-id="73b91-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="73b91-134">Ce code vérifie qu'une table nommée *table1* existe dans votre compte puis la crée si ce n'est pas le cas.</span><span class="sxs-lookup"><span data-stu-id="73b91-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="73b91-135">Vous pouvez également ajouter une référence tooMicrosoft.WindowsAzure.Storage.Table.dll, qui est disponible dans le même package que vous avez téléchargé de hello.</span><span class="sxs-lookup"><span data-stu-id="73b91-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="73b91-136">Cette bibliothèque contient des fonctionnalités supplémentaires, telles qu'une sérialisation basée sur la réflexion et des requêtes génériques.</span><span class="sxs-lookup"><span data-stu-id="73b91-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="73b91-137">Notez que cette bibliothèque ne prend pas en charge le code JavaScript.</span><span class="sxs-lookup"><span data-stu-id="73b91-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
