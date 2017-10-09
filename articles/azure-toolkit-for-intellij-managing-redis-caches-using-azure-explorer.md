---
title: "à l’aide de Caches de Redis aaaManaging hello Explorateur Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toomanage votre redis Azure met en cache à l’aide de hello Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a>Gestion des Caches Redis à l’aide de hello Explorateur Azure pour IntelliJ

Hello Explorateur Azure, qui fait partie de hello Azure Toolkit pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour la gestion de redis caches leur compte Azure, à l’intérieur de hello IntelliJ IDE.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Créer un cache Redis à l’aide d’IntelliJ

Hello suit vous guide tout hello étapes toocreate un cache redis à l’aide de hello Explorateur Azure.

1. Se connecter tooyour compte Azure à l’aide des étapes de hello Bonjour [signe dans des Instructions pour hello Azure Toolkit pour IntelliJ] l’article.

1. Bonjour **Explorateur Azure** fenêtre de l’outil, développez hello **Azure** nœud, avec le bouton droit **les Caches Redis**, puis cliquez sur **créer un Cache Redis**.

   ![Option de menu Créer un cache Redis][CR01]

1. Hello lorsque **nouveau Cache Redis** boîte de dialogue s’affiche, spécifiez hello options suivantes :

   ![Boîte de dialogue de création de cache Redis][CR02]

   a. **Nom DNS**: Spécifie le sous-domaine DNS hello cache redis nouveau hello, qui sont trop précédés du signe «. redis.cache.windows .net », par exemple : *wingtiptoys.redis.cache.windows.net*.

   b. **Abonnement**: Spécifie hello abonnement Azure toouse souhaité pour le cache redis nouveau hello.

   c. **Groupe de ressources**: Spécifie le groupe de ressources hello pour votre cache redis ; vous devez toochoose une des options suivantes de hello :
      * **Créer nouveau**: Spécifie que vous souhaitez toocreate un groupe de ressources.
      * **Utiliser existant** : spécifie que vous allez choisir à partir d’une liste de groupes de ressources associés à votre compte Azure.

   d. **Emplacement**: Spécifie l’emplacement de hello où votre cache redis est créé ; par exemple, *ouest des États-Unis*.

   e. **Niveau de tarification**: Spécifie le niveau tarifaire votre cache redis utilise ; ce paramètre détermine le nombre de hello de connexions clientes. (Pour plus d’informations, consultez [Tarification du Cache Redis].)

   f. **Port non-SSL** : spécifie si le cache Redis autorise les connexions non-SSL ; par défaut, seules les connexions SSL sont autorisées.

1. Une fois que vous avez spécifié tous les paramètres du cache Redis, cliquez sur **OK**.

Une fois que votre cache redis a été créé, il s’affichera dans hello Explorateur Azure.

   ![Cache Redis dans l’Explorateur Azure][CR03]

> [!NOTE]
>
> Pour plus d’informations sur la configuration de votre Azure des paramètres de cache redis, consultez [comment tooconfigure le Cache Redis Azure].
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a>Afficher les propriétés de hello pour votre Cache Redis dans IntelliJ

1. Hello Explorateur Azure, avec le bouton droit de votre cache redis et cliquez sur **afficher les propriétés**.

   ![Azure Explorer toodisplay propriétés du menu contextuel pour un cache redis][SP01]

1. Hello Explorateur Azure affiche les propriétés de hello pour votre cache redis.

   ![Propriétés du cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Supprimer votre cache Redis à l’aide d’IntelliJ

1. Hello Explorateur Azure, avec le bouton droit de votre cache redis et cliquez sur **supprimer**.

   ![Azure toodelete menu de contexte Explorer un cache redis][DE01]

1. Cliquez sur **Oui** lorsque vous y êtes invité toodelete votre cache redis.

   ![Invite de suppression d’un cache Redis][DE02]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Pour plus d’informations sur les caches redis Azure, les paramètres de configuration et la tarification, consultez hello suivant liens :

* [Cache Redis Azure]
* [Documentation du Cache Redis]
* [Tarification du Cache Redis]
* [comment tooconfigure le Cache Redis Azure]

<!-- URL List -->

[Tarification du Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis Azure]: https://azure.microsoft.com/services/cache/
[Documentation du Cache Redis]: ./redis-cache/index.md
[comment tooconfigure le Cache Redis Azure]: ./redis-cache/cache-configure.md
[signe dans des Instructions pour hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
