---
title: "aaaConfigure une chaîne de connexion pour le stockage Azure | Documents Microsoft"
description: "Configurez une chaîne de connexion pour un compte de stockage Azure. Une chaîne de connexion contient des informations de hello nécessaire tooauthenticate accéder au compte de stockage tooa à partir de votre application lors de l’exécution."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Configuration des chaînes de connexion Stockage Azure

Une chaîne de connexion inclut les informations d’authentification hello requises pour vos données d’application tooaccess dans un compte de stockage Azure lors de l’exécution. Vous pouvez configurer les chaînes de connexion pour effectuer les opérations suivantes :

* Se connecter toohello émulateur de stockage Azure.
* Accès à un compte de stockage dans Azure
* Accès aux ressources spécifiées dans Azure via une signature d’accès partagé (SAS).

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Récupération de votre chaîne de connexion
Votre application doit la chaîne de connexion tooaccess hello au runtime tooauthenticate demandes formulées tooAzure stockage. Plusieurs options vous permettant de stocker votre chaîne de connexion s’offrent à vous :

* Une application en cours d’exécution sur le bureau de hello ou sur un appareil peut stocker la chaîne de connexion hello dans un **app.config** ou **web.config** fichier. Ajouter toohello de chaîne de connexion hello **AppSettings** section dans ces fichiers.
* Une application en cours d’exécution dans un service cloud Azure peut stocker la chaîne de connexion de hello Bonjour [fichier de schéma (.cscfg) de configuration de service Azure](https://msdn.microsoft.com/library/ee758710.aspx). Ajouter toohello de chaîne de connexion hello **ConfigurationSettings** section du fichier de configuration de service hello.
* Vous pouvez utiliser votre chaîne de connexion directement dans votre code. Cependant, le plus souvent, nous vous recommandons de stocker votre chaîne de connexion dans un fichier de configuration.

Le stockage de votre chaîne de connexion dans un fichier de configuration rend tooswitch de chaîne de connexion de hello tooupdate facile entre l’émulateur de stockage hello et un compte de stockage Azure dans le cloud de hello. Il vous suffit d’environnement cible de tooedit hello connexion chaîne toopoint tooyour.

Vous pouvez utiliser hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess votre connexion de chaîne lors de l’exécution, quelle que soit l’où votre application est en cours d’exécution.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Créer une chaîne de connexion pour l’émulateur de stockage hello
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

Pour plus d’informations sur l’émulateur de stockage hello, consultez [utiliser l’émulateur de stockage Azure hello pour le développement et test](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Création d’une chaîne de connexion pour un compte de stockage Azure
mettre en forme toocreate une chaîne de connexion pour votre compte de stockage Azure, suivant de hello d’utilisation. Indiquer si vous souhaitez que le compte de stockage tooconnect toohello via HTTPS (recommandé) ou HTTP, remplacez `myAccountName` avec nom hello de votre compte de stockage, puis remplacez `myAccountKey` avec votre clé d’accès de compte :

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Par exemple, votre chaîne de connexion peut ressembler à ceci :

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Même si le stockage Azure prend en charge HTTP et HTTPS au sein d’une chaîne de connexion, nous vous *conseillons vivement d’utiliser HTTPS*.

> [!TIP]
> Vous pouvez trouver des chaînes de connexion de votre compte de stockage Bonjour [portail Azure](https://portal.azure.com). Accédez trop**paramètres** > **clés d’accès** dans les chaînes de connexion de votre compte de stockage menu Panneau toosee pour les deux clés d’accès primaire et secondaire.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Création d’une chaîne de connexion à l’aide d’une signature d’accès partagé
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Création d’une chaîne de connexion pour un point de terminaison de stockage explicite
Vous pouvez spécifier des points de terminaison de service explicite dans votre chaîne de connexion au lieu d’utiliser des points de terminaison par défaut hello. toocreate une chaîne de connexion qui spécifie un point de terminaison explicite, spécifiez hello point de terminaison complet pour chaque service, y compris la spécification de protocole hello (HTTPS (recommandé) ou HTTP), Bonjour suivant le format :

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Un scénario dans lequel vous souhaitez toospecify un point de terminaison explicite est lorsque vous avez mappé votre tooa de point de terminaison de stockage Blob [domaine personnalisé](../blobs/storage-custom-domain-name.md). Dans ce cas, vous pouvez spécifier votre point de terminaison personnalisé pour le stockage Blob dans votre chaîne de connexion. Vous pouvez éventuellement spécifier de points de terminaison par défaut de hello pour hello autres services si votre application les utilise.

Voici un exemple de chaîne de connexion qui spécifie un point de terminaison explicite pour hello service Blob :

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

Cet exemple spécifie les points de terminaison explicites pour tous les services, y compris un domaine personnalisé pour hello service Blob :

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

les valeurs de point de terminaison Hello dans une chaîne de connexion sont des services de stockage toohello URI demande de hello tooconstruct utilisés et dictent écran hello de n’importe quel URI renvoyés tooyour code.

Si vous avez mappé un domaine personnalisé de tooa de point de terminaison de stockage et que vous omettez ce point de terminaison à partir d’une chaîne de connexion, puis vous ne serez pas en mesure de toouse cette connexion données de type string tooaccess dans ce service à partir de votre code.

> [!IMPORTANT]
> Les valeurs des points de terminaison de service dans vos chaînes de connexion doivent être des URI correctement formés, notamment `https://` (recommandé) ou `http://`. Étant donné que le stockage Azure ne prend pas en charge HTTPS pour les domaines personnalisés, vous *doit* spécifier `http://` pour n’importe quel point de terminaison URI qui pointe de domaine personnalisé de tooa.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Création d’une chaîne de connexion avec un suffixe de point de terminaison
toocreate une chaîne de connexion pour un service de stockage dans des régions ou des instances avec des suffixes de point de terminaison différent, comme pour la Chine de Azure ou Azure Government, hello utilisation suivant le format de chaîne de connexion. Indiquer si vous souhaitez que le compte de stockage tooconnect toohello via HTTPS (recommandé) ou HTTP, remplacez `myAccountName` avec nom hello de votre compte de stockage, remplacez `myAccountKey` avec votre clé d’accès de compte, puis remplacez `mySuffix` par hello URI suffixe :

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Voici un exemple de chaîne de connexion pour des services de stockage dans Azure China :

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Analyse d’une chaîne de connexion
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Étapes suivantes
* [Utiliser l’émulateur de stockage Azure hello pour le développement et test](storage-use-emulator.md)
* [Explorateurs du stockage Azure](storage-explorers.md)
* [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md)

