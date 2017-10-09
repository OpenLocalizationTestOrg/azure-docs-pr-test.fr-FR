---
title: "aaaCreate avancée d’encodage des flux de travail avec le Concepteur de flux de travail | Documents Microsoft"
description: "Découvrez comment toocreate avancé codage des flux de travail avec le Concepteur de flux de travail."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>Créer des flux de travail d’encodage avancé avec le Concepteur de flux de travail
## <a name="overview"></a>Vue d'ensemble
Hello **le Concepteur de flux de travail** est un outil de bureau Windows qui est utilisé toodesign build et flux de travail personnalisés pour l’encodage avec **Workflow d’encodeur multimédia Premium**.
À l’aide des hello de l’outil Concepteur de flux de travail hello, vous pouvez concevoir et créer des flux de travail complexes qui s’exécutera dans **Media Encoder Premium**.  

Les workflows peuvent inclure la logique de décision de client et créer une branche basée sur les propriétés du fichier de source d’entrée hello. Vous pouvez créer des flux de travail avec des propriétés substituables et les valeurs dynamiques toomake même hello plus complexes encodage tâches facile toorepeat et personnaliser dans le cloud de hello.

Exemples de flux de travail que vous pouvez créer :

* La décision des flux de travail qui contrôlent le contenu source hello pour la résolution et d’encode les pistes de sortie de hello souhaité uniquement.  Il s’agit helfpul en éliminant les pistes hello gaspillé qui sont générés par l’interpolation source de hello contenu par inadvertance.
* Plusieurs fichiers d’entrée peuvent être utilisé toosupport légendes, superpositions et liaison contenu ensemble. 

Cet outil peut également être toomodify utilisé notre [publié le flux de travail](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> tooget votre copie de l’outil du Concepteur de Workflow hello, veuillez contacter mepd@microsoft.com.
> 
> 

Une fois créé, un fichier de flux de travail peut être téléchargé comme ressource et être utilisé pour l'encodage de fichiers multimédias. Pour plus d’informations sur la façon de tooencode avec **Workflow d’encodeur multimédia Premium** à l’aide de **.NET**, consultez [avancé encodage avec Workflow d’encodeur multimédia Premium](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Modifier des flux de travail existants
Hello par défaut [publié le flux de travail](media-services-workflow-designer.md#existing_workflows) peut être modifié à l’aide du Concepteur de hello. Vous pouvez obtenir par défaut de hello les fichiers de flux de travail [ici](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). dossier de Hello contient également la description hello de ces fichiers.

Hello suivant vidéos montrent comment toouse hello concepteur.

### <a name="day-1--getting-started"></a>Jour 1 : prise en main
La vidéo du jour 1 présente :

* Vue d'ensemble du concepteur
* Flux de travail de base : « Hello World »
* Création de plusieurs fichiers de sortie MP4 à utiliser avec la diffusion en continu d’Azure Media Services

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Jour 2
La vidéo du jour 2 présente :

* Divers scénarios de fichiers source : gestion des fichiers audio
* Flux de travail avec une logique avancée
* Étapes du graphique

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>Jour 3
La vidéo du jour 3 présente :

* Création de scripts de flux de travail/de modèles
* Restrictions avec hello encodeur actuel
* Questions et réponses  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Si vous devez prendre en charge ou avez des questions sur la création de flux de travail personnalisés dans le Concepteur de flux de travail hello, envoyez un courrier électronique toomepd@microsoft.com.

## <a name="see-also"></a>Voir aussi
[Vidéos de formation pour le Concepteur de flux de travail Azure Premium Encoder](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

