---
title: aaaCache fournisseur de Cache de sortie ASP.NET
description: "Découvrez comment faire à l’aide d’Azure Redis Cache de sortie de Page ASP.NET toocache"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Fournisseur de caches de sortie ASP.NET pour le Cache Redis Azure
Hello fournisseur est un mécanisme de stockage d’out-of-process pour les données du cache de sortie. Ces données concernent spécialement les réponses HTTP complètes (mise en cache de la sortie de pages). fournisseur de Hello se connecte au hello nouvelle sortie cache fournisseur point d’extensibilité qui a été introduit dans ASP.NET 4.

toouse hello Redis d’un fournisseur de Cache de sortie, tout d’abord configurer votre cache, puis configurez votre application ASP.NET à l’aide du package NuGet du fournisseur du Cache de sortie Redis de hello. Cette rubrique fournit des conseils sur la configuration de votre hello de toouse application fournisseur. Pour plus d’informations sur la création et la configuration d’une instance de Cache Redis Azure, consultez la section [Création d’un cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Stocker la sortie de la page ASP.NET dans le cache de hello
tooconfigure une application cliente dans Visual Studio à l’aide du package NuGet d’état de Session du Cache Redis de hello, cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.

Exécution hello après une commande à partir de hello `Package Manager Console` fenêtre.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

package NuGet du fournisseur du Cache de sortie Redis de Hello a une dépendance sur le package StackExchange.Redis.StrongName de hello. Si le package StackExchange.Redis.StrongName de hello n’est pas présent dans votre projet, il est installé. Pour plus d’informations sur le package NuGet du fournisseur du Cache de sortie Redis de hello, consultez hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) page de NuGet.

>[!NOTE]
>Dans Ajout toohello fort package StackExchange.Redis.StrongName, également hello StackExchange.Redis sans nom fort version existe. Si votre projet utilise la version de StackExchange.Redis sans nom fort hello que vous devez le désinstaller, sinon vous des conflits de noms dans votre projet. Pour plus d’informations sur ces packages, consultez la section [Configuration des clients de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet package télécharge et ajoute hello requis assembly référence et ajoute des hello suivant la section dans votre fichier web.config. Cette section contient la configuration requise de hello pour votre hello de toouse ASP.NET application fournisseur.

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

Hello commenté section fournit un exemple des attributs de hello et des exemples de paramètres pour chaque attribut.

Configurer les attributs de hello avec des valeurs hello du Panneau de cache dans le portail de Microsoft Azure hello et configurer hello autres valeurs selon vos besoins. Pour obtenir des instructions sur l’accès aux propriétés de votre cache, consultez la section [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).

* **host** : spécifiez le point de terminaison de votre cache.
* **port** – utilisez votre port non-SSL ou votre port SSL, en fonction des paramètres ssl de hello.
* **accessKey** – utilisez clé hello principal ou secondaire de votre cache.
* **SSL** : true si vous voulez toosecure les communications de cache/client avec ssl ; sinon, false. Être vraiment toospecify hello correct.
  * port non-SSL de Hello est désactivé par défaut pour les nouveaux caches. Spécifiez true pour cette hello toouse de paramètre port SSL. Pour plus d’informations sur l’activation du port de hello non-SSL, consultez hello [Ports d’accès](cache-configure.md#access-ports) section Bonjour [configurer un cache](cache-configure.md) rubrique.
* **databaseId** – spécifié le toouse de la base de données pour le cache des données de sortie. Si non spécifié, la valeur par défaut 0 hello est utilisé.
* **applicationName** : les clés sont stockées dans redis sous `<AppName>_<SessionId>_Data`. Ce schéma d’affectation de noms permet hello de tooshare plusieurs applications même clé. Ce paramètre est facultatif. Si vous n’indiquez aucune valeur, une valeur par défaut sera utilisée.
* **connectionTimeoutInMilliseconds** : ce paramètre vous permet de connectTimeout de hello toooverride définition dans le client StackExchange.Redis de hello. Si non spécifié, le paramètre connectTimeout 5000 hello par défaut est utilisé. Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : ce paramètre vous permet de syncTimeout de hello toooverride définition dans le client StackExchange.Redis de hello. Si non spécifié, la valeur syncTimeout 1000 hello par défaut est utilisée. Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Ajouter une page de tooeach directive OutputCache pour laquelle vous souhaitez la sortie de hello toocache.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

Dans l’exemple précédent de hello, hello mises en cache les données de page reste dans le cache de hello pendant 60 secondes, et une version différente de la page de hello est mis en cache pour chaque combinaison de paramètres. Pour plus d’informations sur la directive OutputCache de hello, consultez [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

Une fois ces étapes effectuées, votre application est configurée toouse hello fournisseur.

## <a name="next-steps"></a>Étapes suivantes
Extraire hello [fournisseur d’état de Session ASP.NET pour le Cache Redis Azure](cache-aspnet-session-state-provider.md).

