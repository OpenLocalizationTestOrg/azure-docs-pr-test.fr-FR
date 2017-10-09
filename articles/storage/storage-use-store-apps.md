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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Comment toouse le stockage Azure dans les applications du Windows Store
## <a name="overview"></a>Vue d'ensemble
Ce guide montre comment tooget démarrer avec le développement d’une application Windows Store qui utilise le stockage Azure.

## <a name="download-required-tools"></a>Téléchargement des outils nécessaires
* [Visual Studio](https://www.visualstudio.com/downloads/) rend facile toobuild, déboguer, localiser, empaqueter et déployer des applications du Windows Store. Visual Studio 2012 ou une version ultérieure est nécessaire.
* Hello [bibliothèque cliente de stockage Azure](https://www.nuget.org/packages/WindowsAzure.Storage) fournit une bibliothèque de classes Windows Runtime pour travailler avec le stockage Azure.
* [WCF données Services Tools pour applications du Windows Store](http://www.microsoft.com/download/details.aspx?id=30714) étend l’expérience d’ajouter une référence de Service hello avec prise en charge de OData côté client pour les applications du Windows Store dans Visual Studio.

## <a name="develop-apps"></a>Développement d'applications
### <a name="getting-ready"></a>Préparation
Créez un projet d'application Windows Store dans Visual Studio 2012 ou version ultérieure :

![store-apps-storage-vs-project][store-apps-storage-vs-project]

Ensuite, ajoutez une référence de toohello bibliothèque cliente de stockage Azure en cliquant sur **références**, puis sur **ajouter une référence**, puis accédez toohello bibliothèque cliente de stockage pour Windows Runtime que vous avez télécharger :

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>À l’aide de la bibliothèque hello avec hello Blob et les services de file d’attente
À ce stade, votre application est prête toocall hello services Blob et Azure file d’attente. Ajoutez hello suivant **à l’aide de** instructions afin que les types de stockage Azure peuvent être référencés directement :

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Ensuite, ajoutez une page tooyour de bouton. Ajouter hello suivant code tooits **cliquez sur** événement et modifier votre méthode de gestionnaire d’événements à l’aide de hello [mot clé async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Ce code suppose que vous disposez de deux variables de chaîne, *accountName* et *accountKey*. Ils représentent nom hello de votre compte et hello clé compte de stockage qui est associée à ce compte.

Générez et exécutez l’application hello. En cliquant sur bouton de hello vérifie si un conteneur nommé *container1* existe dans votre compte, puis le créer dans le cas contraire.

### <a name="using-hello-library-with-hello-table-service"></a>À l’aide de la bibliothèque de hello hello service de Table
Les types qui sont toocommunicate utilisé avec le service de Table Azure hello dépendent de WCF Data Services pour la bibliothèque d’applications du Windows Store hello. Ensuite, ajoutez qu'une référence toohello requis les bibliothèques WCF à l’aide de hello Console du Gestionnaire de Package :

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Utilisez hello suivant commande toopoint toohello du Gestionnaire de Package emplacement sur votre ordinateur :

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Cette commande ajoute automatiquement le projet de tooyour toutes les références requises. Si vous ne souhaitez pas toouse hello Console du Gestionnaire de Package, vous pouvez ajouter un dossier de NuGet de Services de données WCF hello dans votre liste de toohello ordinateur local des sources de package et ajouter ensuite référence hello via hello l’interface utilisateur, comme décrit dans [la gestion de l’aide de Packages NuGet boîte de dialogue de Hello](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Lorsque vous avez référencé package NuGet de Services de données WCF de hello, modifiez le code hello dans votre bouton **cliquez sur** événement :

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Ce code vérifie qu'une table nommée *table1* existe dans votre compte puis la crée si ce n'est pas le cas.

Vous pouvez également ajouter une référence tooMicrosoft.WindowsAzure.Storage.Table.dll, qui est disponible dans le même package que vous avez téléchargé de hello. Cette bibliothèque contient des fonctionnalités supplémentaires, telles qu'une sérialisation basée sur la réflexion et des requêtes génériques. Notez que cette bibliothèque ne prend pas en charge le code JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
