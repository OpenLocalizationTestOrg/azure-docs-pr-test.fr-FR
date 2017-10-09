---
title: "aaaAnalyze votre média à l’aide de hello le portail Azure | Documents Microsoft"
description: "Cette rubrique explique comment tooprocess votre média avec des processeurs multimédias de support Analytique (PA) à l’aide de hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analyser votre média à l’aide de hello portail Azure
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Vue d'ensemble
Analytique de Services de support Azure est une collection de composants vocale et de la vision (à l’échelle de l’entreprise, la conformité, de sécurité et portée globale) qui le rendent plus facile pour les organisations et les entreprises tooderive d’informations exploitables à partir de leurs fichiers vidéos. Pour une présentation plus détaillée d’Azure Media Services Analytics, consultez [cette](media-services-analytics-overview.md) rubrique. 

Cette rubrique explique comment tooprocess votre média avec des processeurs multimédias de support Analytique (PA) à l’aide de hello portail Azure. Les processeurs multimédia Media Analytics créent des fichiers MP4 ou JSON. Si un processeur multimédia produit un fichier MP4, vous pouvez télécharger progressivement les fichier hello. Si un processeur multimédia produit un fichier JSON, vous pouvez télécharger le fichier de hello de hello stockage d’objets blob Azure. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Choisissez un élément multimédia que vous souhaitez tooanalyze
1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Bonjour **paramètres** fenêtre, sélectionnez **actifs**.  
   .
    ![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Asset hello SELECT que vous aimeriez hello tooanalyze et appuyez sur **analyser** bouton.
   
    ![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. Bonjour **processus multimédia ayant Media Analytique** fenêtre, le processeur de hello select. 
   
    rest Hello d’article de hello explique pourquoi et comment toouse chaque processeur. 
5. Appuyez sur **créer** toohello démarrer une tâche.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Hello **Azure Media Indexer** processeur multimédia vous permet de toomake des fichiers multimédias et contenu de recherche, ainsi que pour générer des pistes de sous-titres. Cette section donne des informations sur les options que vous pouvez spécifier pour ce processeur multimédia.

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>language
toobe de langage naturel Hello reconnu dans le fichier multimédia de hello. Par exemple, anglais ou espagnol. 

### <a name="captions"></a>Sous-titres
Vous pouvez choisir un format de sous-titre qui sera généré à partir de votre contenu. Un travail d’indexation peut générer des fichiers de sous-titres Bonjour suivant formats :  

* **SAMI**
* **TTML**
* **WebVTT**

Les fichiers de sous-titres fermés dans ces formats peuvent être utilisés toomake audio et vidéo fichiers accessible toopeople malentendantes.

### <a name="aib-file"></a>Fichier AIB
Sélectionnez cette option si vous serez comme fichier de son Index Blob toogenerate hello pour une utilisation avec hello IFilter de serveur SQL personnalisée. Pour plus d’informations, consultez [ce](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.

### <a name="keywords"></a>Mots clés
Sélectionnez cette option si vous souhaitez que toogenerate un fichier XML de mots clés. Ce fichier contient des mots clés extraits à partir du contenu de reconnaissance vocale hello, avec la fréquence et les informations de décalage.

### <a name="job-name"></a>Nom du travail
Un nom convivial qui vous permet d’identifier la tâche de hello. [Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche. 

### <a name="output-file"></a>Fichier de sortie
Un nom convivial qui vous permet d’identifier le contenu de sortie hello. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse est un processeur multimédia qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d’un contenu de caméra à la première personne (first-person camera) ou d’action.  Pour plus d’informations, consultez [cette](media-services-hyperlapse-content.md) rubrique. Cette section donne des informations sur les options que vous pouvez spécifier pour ce processeur multimédia.

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Vitesse
Spécifiez la vitesse hello avec le toospeed vidéo d’entrée de hello. sortie de Hello est un format de stabilisation et temps écoulé associé de la vidéo d’entrée de hello.

### <a name="job-name"></a>Nom du travail
Un nom convivial qui vous permet d’identifier la tâche de hello. [Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche. 

### <a name="output-file"></a>Fichier de sortie
Un nom convivial qui vous permet d’identifier le contenu de sortie hello. 

## <a name="azure-media-face-detector"></a>Détecteur de visage Azure Media
Hello **Azure Media Face détecteur** le processeur multimédia (MP) vous permet de toocount, les mouvements de suivi et même la participation jauge audience et réaction via des expressions visages. Ce service présente deux fonctionnalités : 

* **Détection faciale**
  
    La détection faciale détecte et suit les visages humains au sein d’une vidéo. Plusieurs polices peuvent être détectées et par la suite être suivis comme ils sont en déplacement, avec hello heure et l’emplacement des métadonnées retournées dans un fichier JSON. Lors du suivi, il va tenter de toogive un toohello ID cohérent même sont confrontés lors de la personne de hello tourne autour de l’écran, même s’ils sont coupés ou laisser brièvement les frames de hello.
  
  > [!NOTE]
  > Ce service n’effectue pas la reconnaissance faciale. Une personne qui laisse le frame de hello ou devienne coupée pour trop longtemps recevra un nouvel ID lorsqu’elles retournent.
  > 
  > 
* **Détection d’émotions**
  
    Détection d’émotion est un composant facultatif de hello processeur multimédia de détection Face qui renvoie analysis sur plusieurs attributs émotionnels à partir de face hello détecté, y compris bonheur, leur, peur, colère et bien plus encore. 

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Mode de détection
Une des hello suivant des modes peut être utilisée par le processeur hello :

* détection faciale
* détection d’émotion par visage
* détection d’émotion agrégée

### <a name="job-name"></a>Nom du travail
Un nom convivial qui vous permet d’identifier la tâche de hello. [Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche. 

### <a name="output-file"></a>Fichier de sortie
Un nom convivial qui vous permet d’identifier le contenu de sortie hello. 

## <a name="azure-media-motion-detector"></a>Détecteur de mouvement Azure Media
Hello **détecteur de mouvement Azure Media** permet de processeur (MP) support tooefficiently de vous identifient des sections d’intérêt dans une vidéo sinon long et se déroule normalement. Détection de mouvement peut être utilisée sur caméra statique enregistrements tooidentify sections de la vidéo de hello où se produit le mouvement. Il génère un fichier JSON contenant des métadonnées avec les horodateurs et hello englobant la région où l’événement de hello s’est produite.

Cible des flux vidéo de sécurité, cette technologie est mouvement en mesure de toocategorize dans les événements pertinents et des faux positifs, tels que des changements d’éclairage et les ombres. Ainsi, vous toogenerate les alertes de sécurité à partir de flux de l’appareil photo sans recevoir des messages indésirables avec les événements non pertinentes sans fin, tout en étant instants tooextract en mesure d’intérêt de vidéos de surveillance très longs.

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Miniatures vidéo Azure Media
Ce processeur peut vous aider à créer des résumés de vidéos long en sélectionnant automatiquement extraits intéressantes à partir de la vidéo source de hello. Cela est utile lorsque vous souhaitez tooprovide un aperçu rapide de quel tooexpect dans une vidéo longue. Pour plus d’informations et d’exemples, consultez [utiliser Azure Media les miniatures vidéo tooCreate une synthèse de la vidéo](media-services-video-summarization.md)

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Nom du travail
Un nom convivial qui vous permet d’identifier la tâche de hello. [Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche. 

### <a name="output-file"></a>Fichier de sortie
Un nom convivial qui vous permet d’identifier le contenu de sortie hello. 

## <a name="next-steps"></a>Étapes suivantes
Afficher les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

