---
title: aaaHow toouse du Cache Redis Azure avec Python | Documents Microsoft
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
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a><span data-ttu-id="0320d-103">Comment toouse Azure Redis Cache avec Python</span><span class="sxs-lookup"><span data-stu-id="0320d-103">How toouse Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0320d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0320d-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="0320d-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0320d-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="0320d-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0320d-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="0320d-107">Java</span><span class="sxs-lookup"><span data-stu-id="0320d-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="0320d-108">Python</span><span class="sxs-lookup"><span data-stu-id="0320d-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="0320d-109">Cette rubrique vous indique comment tooget a démarré avec le Cache Redis Azure à l’aide de Python.</span><span class="sxs-lookup"><span data-stu-id="0320d-109">This topic shows you how tooget started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0320d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0320d-110">Prerequisites</span></span>
<span data-ttu-id="0320d-111">Installez [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="0320d-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="0320d-112">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="0320d-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="0320d-113">Récupérer les clés d’accès et nom d’hôte hello</span><span class="sxs-lookup"><span data-stu-id="0320d-113">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a><span data-ttu-id="0320d-114">Activer le point de terminaison non-SSL hello</span><span class="sxs-lookup"><span data-stu-id="0320d-114">Enable hello non-SSL endpoint</span></span>
<span data-ttu-id="0320d-115">Certains clients Redis ne prend pas en charge SSL et par hello de valeur par défaut [port non-SSL est désactivé pour les nouvelles instances de Cache Redis Azure](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="0320d-115">Some Redis clients don't support SSL, and by default hello [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="0320d-116">Au moment de hello de rédaction de cet article, hello [redis-pier](https://github.com/andymccurdy/redis-py) client ne prend pas en charge SSL.</span><span class="sxs-lookup"><span data-stu-id="0320d-116">At hello time of this writing, hello [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="0320d-117">Ajoutez un élément toohello mettre en cache et récupérer</span><span class="sxs-lookup"><span data-stu-id="0320d-117">Add something toohello cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="0320d-118">Remplacez `<name>` par le nom de votre cache, et `key` par votre clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="0320d-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
