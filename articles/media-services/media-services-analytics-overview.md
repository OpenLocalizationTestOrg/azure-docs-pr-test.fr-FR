---
title: aaaMedia Analytique sur une plateforme de Media Services hello | Documents Microsoft
description: "Présentation de la version préliminaire publique de Media Analytics, un ensemble de services de reconnaissance vocale et de vision par ordinateur destinés aux entreprises et répondant aux exigences de conformité, de sécurité et de présence mondiale"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Analytique multimédia sur la plateforme de Media Services hello
## <a name="overview"></a>Vue d'ensemble
Plusieurs organisations utilisent vidéo comme hello tootrain moyenne par défaut leurs employés, retenir leurs clients et les fonctions commerciales de document. Le cloud computing offre un moyen toostore, flux et accéder à ces fichiers multimédias volumineux. Mais comme bibliothèque d’une société de contenu vidéo augmente, il doit aussi efficaces de l’extraction d’informations à partir du contenu de hello. 

tooaddress ce besoin croissant, Azure Media Services offre Azure Media Analytique. Support Analytique est une collection de composants de la reconnaissance vocale et de la vision qui rend plus facile pour les organisations et les entreprises tooderive d’informations exploitables à partir de leurs fichiers vidéos. Générée à l’aide de composants de la plateforme hello core Media Services, support Analytique peut gérer media à grande échelle sur le premier jour de traitement.

Avec Media Analytics, les développeurs peuvent rapidement ajouter des fonctionnalités avancées aux applications. Il fournit les environnements d’entreprise complet hello, conformité, la sécurité et portée requis par les organisations de grande taille.

Hello diagramme suivant montre Analytique de support et d’autres parties principales de plateforme de Media Services hello. 

![Flux de travail VOD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

Les processeurs multimédias Media Analytics créent des fichiers MP4 ou JSON. Si un processeur multimédia génère un fichier MP4, vous pouvez télécharger progressivement les fichier hello. Si un processeur multimédia génère un fichier JSON, vous pouvez télécharger le fichier de hello à partir du stockage d’objets Blob Azure. 

## <a name="media-analytics-services"></a>Services Media Analytics

### <a name="indexer"></a>Indexeur
Avec Azure Media Indexer, vous pouvez activer la recherche pour du contenu et générer des pistes de sous-titrage. Version précédente toohello comparés, Azure Media Indexer en version préliminaire 2 prend en charge les langage plus rapide d’indexation et plus large. Les langues prises en charge sont l’anglais, l’espagnol, le français, l’allemand, l’italien, le chinois, le portugais et l’arabe. Pour obtenir des informations détaillées et des exemples, consultez [Traiter les vidéos avec l’Indexeur multimédia Azure 2](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse combine stabilisation vidéo et capacité séquentiel toocreate rapide, utilisable à partir de votre contenu sous forme longue. Outre la création intermittente, vous pouvez utiliser les vidéos stables de Hyperlapse toocreate de vidéos tremblement capturées à l’aide de téléphones et de caméscopes. Pour obtenir des informations détaillées et des exemples, consultez [Fichiers multimédia hyperlapse avec Azure Media Hyperlapse](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Motion Detector
Vous pouvez utiliser le mouvement de toodetect de détecteur de mouvement dans une vidéo avec des arrière-plans STATIONNAIRES. Cela rend possible toocheck de faux positifs sur les événements de mouvement détectées par des caméras de surveillance. Pour obtenir des informations détaillées et des exemples, consultez [Détection de mouvement pour Azure Media Analytics](media-services-motion-detection.md).
### <a name="face-detector"></a>Face Detector
Avec Face Detector, vous pouvez détecter les visages et les émotions qui y sont exprimées, comme la joie, la tristesse et la surprise. Ce service est très utile dans plusieurs secteurs d’activité, comme expliqué plus tard, notamment pour l’agrégation et l’analyse des réactions des personnes participant à un événement. Pour obtenir des informations détaillées et des exemples, consultez [Détection des visages et des émotions pour Azure Media Analytics](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Video Summarization (Création de résumés de vidéos)
Synthèse vidéo peut vous aider à créer des résumés de vidéos long en sélectionnant automatiquement extraits intéressantes à partir de la vidéo source de hello. Cette capacité est utile lorsque vous souhaitez tooprovide un aperçu rapide de quel tooexpect dans une vidéo longue. Pour plus d’informations et d’exemples, consultez [synthèse vidéo de miniatures de vidéo utiliser Azure Media toocreate](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Reconnaissance optique de caractères
Avec Azure Media OCR (reconnaissance optique de caractères), vous pouvez convertir le contenu texte de fichiers vidéo en un texte numérique modifiable et pouvant faire l’objet d’une recherche. Vous pouvez automatiser extraction hello de métadonnées significatives à partir de signal vidéo de hello de votre support.
### <a name="scalable-face-redaction"></a>Rédaction de face évolutive
Azure Media Redactor est un processeur multimédia Media Analytique qui offre la rédaction de face évolutives dans le cloud de hello. À l’aide de rédaction de face, vous pouvez modifier votre vidéo tooblur de face d’individus sélectionnés. Vous pouvez choisir le service de rédaction de face toouse hello dans les médias ou la sécurité publique est impliquée. Quelques minutes de film qui contient plusieurs polices peuvent prendre des heures tooredact manuellement, mais avec ce service, face rédaction prend seulement quelques étapes simples. Pour plus d’informations, consultez hello [procéder faces avec Azure Media Analytique](media-services-face-redaction.md) l’article.

## <a name="common-scenarios"></a>Scénarios courants
Media Analytics peut aider les organisations et entreprises à mieux exploiter et cibler leurs contenus vidéo et à améliorer la gestion des gros volumes de contenus vidéo. Voici quelques exemples de scénario :

* **Centres d’appel**. Même avec l’apparition de hello de médias sociaux, centres d’appels client facilitent encore un grand pourcentage des transactions du service clientèle. Codé dans ces données audio sont une grande quantité d’informations sur le client qui peuvent être analysées tooachieve satisfaction des clients plus élevée. Avec Media Indexer, les organisations peuvent extraire du texte et créer des index de recherche et des tableaux de bord. Ils peuvent ensuite extraire des informations sur les réclamations, les causes des réclamations et autres données pertinentes.
* **Modération du contenu généré par les utilisateurs**. À partir des services de médias prises toopolice, de nombreuses organisations possèdent des portails publics qui acceptent généré par l’utilisateur les supports tels que des vidéos et des images. volume Hello de contenu peut grimper toounexpected événements d’échéance. Dans ces scénarios, il est difficile tooconduct révisions du manuel efficace du contenu de manière correcte. Les clients peuvent reposer sur toofocus du service de modération de contenu hello sur le contenu qui est approprié.
* **Surveillance**. Hello s’accompagne de croissance en cours d’utilisation des caméras IP un inventaire croissant de vidéo de surveillance. Examen manuel de vidéo de surveillance est toohuman intensive et susceptible d’engendrer des erreurs au moment. Support Analytique fournit des services tels que la détection de mouvement, la détection de visage et Hyperlapse toomake hello processus de révision, la gestion et création dérivés plus facile.

## <a name="media-analytics-media-processors"></a>Processeurs multimédia Media Analytics
Cette section processeurs multimédias de listes hello Media Analytique et montre comment tooget un objet de processeur (MP) multimédia toouse .NET ou REST.

### <a name="mp-names"></a>Noms MP
* Azure Media Indexer 2 Preview
* Azure Media Indexer
* Azure Media Hyperlapse
* Détecteur de visage Azure Media
* Détecteur de mouvement Azure Media
* Miniatures vidéo Azure Media
* Azure Media OCR

### <a name="net"></a>.NET
Hello après la fonction prend hello spécifié MP noms et retourne un objet de pack d’administration.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
Demande :

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Réponse :

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Démonstrations
Consultez les [Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articles connexes
Consultez [l’Annonce concernant Media Services Analytics](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
