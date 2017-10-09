---
title: "vitesse de gérer aaa et l’accès simultané de votre encodage avec Azure Media Services | Documents Microsoft"
description: "Cet article donne un bref aperçu de la manière dont vous pouvez gérer la rapidité et la simultanéité de vos travaux/tâches d’encodage avec Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Gérer la vitesse et la simultanéité de votre encodage

Cet article donne un bref aperçu de la manière dont vous pouvez gérer la rapidité et la simultanéité de vos travaux/tâches d’encodage.

## <a name="overview"></a>Vue d'ensemble

Dans Media Services, un **Type d’unité réservée** détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités. Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : **S1**, **S2**, ou **S3**. Par exemple, les hello même travail d’encodage s’exécute plus rapidement lorsque vous utilisez hello **S2** type d’unité réservée comparer toohello **S1** type. Hello [mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md) rubrique illustre une table qui vous permet de prendre de décision lors du choix entre différentes vitesses de codage.

En outre toospecifying hello réservé type d’unité, vous pouvez spécifier tooprovision votre compte avec **unités réservées**. nombre Hello d’unités réservées configurées détermine le nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné. Par exemple, si votre compte dispose de cinq unités réservées, puis les tâches de cinq support exécuter simultanément à condition qu’il sont toobe tâches traitée. les tâches restantes Hello attendent dans la file d’attente hello et sont collectées de manière séquentielle pour traitement lorsqu’une tâche en cours d’exécution se termine. Si aucune unité réservée n'est approvisionnée pour un compte donné, les tâches sont sélectionnées séquentiellement. Dans ce cas, hello délai entre une fin de tâche et hello ensuite démarrage dépendront de disponibilité hello des ressources dans le système de hello.

Pour plus d’informations et des exemples qui montrent comment les unités d’encodage tooscale, consultez [cela](media-services-scale-media-processing-overview.md) rubrique.

## <a name="next-step"></a>Étape suivante

[Mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

