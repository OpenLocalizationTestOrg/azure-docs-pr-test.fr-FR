---
title: Utilisation du stockage Azure dans les applications Windows Store | Microsoft Docs
description: "Apprenez à créer une application Windows Store qui utilise les services Azure Blob Storage, Queue Storage, Table Storage et File Storage."
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
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="27a80-103">Utilisation d'Azure Storage dans les applications Windows Store</span><span class="sxs-lookup"><span data-stu-id="27a80-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="27a80-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="27a80-104">Overview</span></span>
<span data-ttu-id="27a80-105">Ce guide montre comment commencer le développement d'une application Windows Store utilisant Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="27a80-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="27a80-106">Téléchargement des outils nécessaires</span><span class="sxs-lookup"><span data-stu-id="27a80-106">Download required tools</span></span>
* <span data-ttu-id="27a80-107">[Visual Studio](https://www.visualstudio.com/downloads/) permet de générer, de déboguer, de localiser, de mettre en package et de déployer des applications Windows Store en toute simplicité.</span><span class="sxs-lookup"><span data-stu-id="27a80-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="27a80-108">Visual Studio 2012 ou une version ultérieure est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="27a80-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="27a80-109">La [bibliothèque cliente d’Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage) fournit une bibliothèque de classes Windows Runtime qui permet d’utiliser Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="27a80-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="27a80-110">[outils de services de données WCF pour applications Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) développent l’expérience Ajouter une référence de service avec la prise en charge OData côté client pour les applications Windows Store dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27a80-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="27a80-111">Développement d'applications</span><span class="sxs-lookup"><span data-stu-id="27a80-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="27a80-112">Préparation</span><span class="sxs-lookup"><span data-stu-id="27a80-112">Getting ready</span></span>
<span data-ttu-id="27a80-113">Créez un projet d'application Windows Store dans Visual Studio 2012 ou version ultérieure :</span><span class="sxs-lookup"><span data-stu-id="27a80-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="27a80-115">Ensuite, ajoutez une référence à la bibliothèque cliente Azure Storage. Pour cela, cliquez avec le bouton droit sur **Références**, choisissez **Ajouter une référence**, puis recherchez la bibliothèque cliente Storage pour Windows Runtime que vous avez téléchargée :</span><span class="sxs-lookup"><span data-stu-id="27a80-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="27a80-117">Utilisation de la bibliothèque avec les services blob et de file d'attente</span><span class="sxs-lookup"><span data-stu-id="27a80-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="27a80-118">À ce stade, votre application est prête à appeler les services Azure Blob et de file d'attente.</span><span class="sxs-lookup"><span data-stu-id="27a80-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="27a80-119">Ajoutez les instructions **using** suivantes afin que les types Azure Storage soient référencés directement :</span><span class="sxs-lookup"><span data-stu-id="27a80-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="27a80-120">Ensuite, ajoutez un bouton sur votre page.</span><span class="sxs-lookup"><span data-stu-id="27a80-120">Next, add a button to your page.</span></span> <span data-ttu-id="27a80-121">Ajoutez le code suivant dans son événement **Cliquer** et modifiez votre méthode de gestionnaire d'événements grâce au [mot clé async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="27a80-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="27a80-122">Ce code suppose que vous disposez de deux variables de chaîne, *accountName* et *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="27a80-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="27a80-123">Elles représentent le nom de votre compte de stockage et la clé de compte associée à ce compte.</span><span class="sxs-lookup"><span data-stu-id="27a80-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="27a80-124">Générez et exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="27a80-124">Build and run the application.</span></span> <span data-ttu-id="27a80-125">Si vous cliquez sur le bouton, l'application vérifiera si un conteneur nommé *container1* existe dans votre compte, puis le créera si ce n'est pas le cas.</span><span class="sxs-lookup"><span data-stu-id="27a80-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="27a80-126">Utilisation de la bibliothèque avec le service de Table</span><span class="sxs-lookup"><span data-stu-id="27a80-126">Using the library with the Table service</span></span>
<span data-ttu-id="27a80-127">Les types utilisés pour communiquer avec le service de Table Azure dépendent des services de données WCF pour la bibliothèque d'applications Windows Store.</span><span class="sxs-lookup"><span data-stu-id="27a80-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="27a80-128">Ensuite, ajoutez une référence aux bibliothèques WCF requises en utilisant la console du Gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="27a80-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="27a80-130">Utilisez la commande suivante pour faire pointer le Gestionnaire de package sur l'emplacement de votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="27a80-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="27a80-131">Cette commande ajoutera automatiquement toutes les références requises à votre projet.</span><span class="sxs-lookup"><span data-stu-id="27a80-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="27a80-132">Si vous ne souhaitez pas utiliser la console du Gestionnaire de package, vous pouvez ajouter le dossier NuGet de services de données WCF sur votre ordinateur local dans la liste des sources de package, puis ajouter la référence via l'interface utilisateur comme décrit dans [Gestion des packages NuGet à l'aide de la boîte de dialogue](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="27a80-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="27a80-133">Une fois le package NuGet de services de données WCF référencé, modifiez le code dans l'événement **Cliquer** de votre bouton :</span><span class="sxs-lookup"><span data-stu-id="27a80-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="27a80-134">Ce code vérifie qu'une table nommée *table1* existe dans votre compte puis la crée si ce n'est pas le cas.</span><span class="sxs-lookup"><span data-stu-id="27a80-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="27a80-135">Vous pouvez également ajouter une référence dans Microsoft.WindowsAzure.Storage.Table.dll, disponible dans le même package que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="27a80-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="27a80-136">Cette bibliothèque contient des fonctionnalités supplémentaires, telles qu'une sérialisation basée sur la réflexion et des requêtes génériques.</span><span class="sxs-lookup"><span data-stu-id="27a80-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="27a80-137">Notez que cette bibliothèque ne prend pas en charge le code JavaScript.</span><span class="sxs-lookup"><span data-stu-id="27a80-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
