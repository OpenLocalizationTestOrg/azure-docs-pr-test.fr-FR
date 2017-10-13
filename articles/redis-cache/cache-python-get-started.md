---
title: Utilisation du Cache Redis Azure avec Python | Microsoft Docs
description: Prise en main du Cache Redis Azure avec Python
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: cdbee52574d0ffbe82ef3dc98f2848f4d00ba2ff
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-python"></a>Utilisation du Cache Redis Azure avec Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Cette rubrique montre comment utiliser le Cache Redis Azure avec Python.

## <a name="prerequisites"></a>Composants requis
Installez [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Créer un Cache Redis sur Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a>Récupérer les clés d’accès et le nom hôte
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a>Activer le point de terminaison non SSL
Certains clients Redis ne prennent pas en charge SSL. Le [port non SSL est désactivé par défaut pour les nouvelles instances Cache Redis Azure](cache-configure.md#access-ports). Le [redis-py](https://github.com/andymccurdy/redis-py) ne prend pas en charge SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a>Ajouter un élément au cache et le récupérer
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


Remplacez `<name>` par le nom de votre cache, et `key` par votre clé d’accès.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
