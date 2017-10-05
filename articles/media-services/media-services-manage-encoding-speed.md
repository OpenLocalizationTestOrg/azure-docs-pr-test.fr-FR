---
title: "Gérer la rapidité et la simultanéité de votre encodage avec Azure Media Services | Microsoft Docs"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Gérer la vitesse et la simultanéité de votre encodage

Cet article donne un bref aperçu de la manière dont vous pouvez gérer la rapidité et la simultanéité de vos travaux/tâches d’encodage.

## <a name="overview"></a>Vue d’ensemble

Dans Media Services, un **Type d’unité réservée** détermine la vitesse à laquelle vos tâches de traitement multimédia sont traitées. Vous pouvez choisir entre les types d’unités réservées suivantes : **S1**, **S2** ou **S3**. Par exemple, un même travail d’encodage s’exécute plus rapidement quand vous utilisez le type d’unité réservée **S2** que le type **S1**. La rubrique relative à la [mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md) contient un tableau qui vous aide à prendre une décision lors du choix entre les différentes vitesses d’encodage.

En plus de spécifier le type d’unité réservée, vous pouvez approvisionner votre compte avec des **unités réservées**. Le nombre d’unités réservées approvisionnées détermine le nombre de tâches de média qui peuvent être traitées simultanément dans un compte donné. Si, par exemple, votre compte a cinq unités réservées, les cinq tâches multimédias sont exécutées simultanément tant qu’il y a des tâches à traiter. Les autres tâches restent dans la file d'attente et sont sélectionnées séquentiellement pour le traitement quand l'exécution d'une tâche se termine. Si aucune unité réservée n'est approvisionnée pour un compte donné, les tâches sont sélectionnées séquentiellement. Dans ce cas, le temps d'attente entre l'achèvement d'une tâche et le démarrage de la suivante dépend de la disponibilité des ressources dans le système.

Pour obtenir des informations détaillées et des exemples sur la manière de mettre à l’échelle les unités d’encodage, consultez [cette rubrique](media-services-scale-media-processing-overview.md).

## <a name="next-step"></a>Étape suivante

[Mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

