---
title: "aaaOverview de diffusion en continu à l’aide d’Azure Media Services | Documents Microsoft"
description: "Cette rubrique fournit une vue d’ensemble du streaming en direct à l’aide d’Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Vue d’ensemble du streaming en direct à l’aide d’Azure Media Services
## <a name="overview"></a>Vue d'ensemble
Lors de la remise en temps réel avec Azure Media Services, les événements de diffusion en continu hello suivant composants implique en général :

* Une caméra toobroadcast utilisé un événement.
* Un encodeur vidéo en direct qui convertit les signaux toostreams caméra hello envoyés tooa dynamique service de diffusion en continu.

    Éventuellement, plusieurs encodeurs live synchronisés. Événements qu’à la demande très haute disponibilité et la qualité de l’expérience, il est recommandé d’encodeurs redondants de tooemploy actif avec heure synchronisation tooachieve un basculement transparent sans perte de données en direct pour certaines critiques.
* Service de diffusion en continu live qui vous permet de hello toodo suivant :

  * Recevoir du contenu en direct à l’aide de différents protocoles de diffusion de vidéo en flux continu (par exemple RTMP ou Smooth Streaming),
  * Encoder votre flux en flux à débit adaptatif (facultatif)
  * Afficher un aperçu de votre flux en direct
  * enregistrement et le magasin de contenu hello ingéré dans l’ordre toobe transmis en continu ultérieur (vidéo à la demande)
  * Fournir du contenu hello via des protocoles de diffusion en continu courants (par exemple, MPEG DASH, Smooth Streaming, HLS) directement les clients tooyour ou tooa réseau de distribution de contenu (CDN) pour une distribution ultérieure.

**Microsoft Azure Media Services** (AMS) fournit hello capacité tooingest Encoder, afficher un aperçu, stocker et distribuer votre contenu de diffusion en continu en direct.

Lors de la remise de votre contenu toocustomers votre objectif est toodeliver une unité de toovarious vidéo haute qualité dans des conditions réseau différents. tooachieve, utilisez live encodeurs tooencode votre flux vidéo de flux tooa plusieurs débits (débit adaptatif).  tootake aux soins de diffusion en continu sur différents appareils, utilisez Media Services [empaquetage dynamique](media-services-dynamic-packaging-overview.md) toodynamically protocoles toodifferent de votre flux de données du nouveau package. Media Services prend en charge la remise de hello suivant des technologies de diffusion en continu de fichiers à débit adaptatif : HTTP Live Streaming (HLS), la diffusion en continu lisse, MPEG DASH.

Dans Azure Media Services, **canaux**, **programmes**, et **StreamingEndpoints** handle live de hello toutes les fonctionnalités, y compris la réception, le formatage, magnétoscope numérique, de diffusion en continu sécurité, l’évolutivité et la redondance.

Un **canal** représente un pipeline de traitement du contenu vidéo en flux continu. Un canal peut recevoir un live flux Bonjour suivant les méthodes d’entrée :

* Un encodeur dynamique local envoie plusieurs débits **RTMP** ou **Smooth Streaming** (MP4 fragmenté) toohello canal qui est configuré pour **pass-through** remise. Hello **pass-through** la remise est lorsque les flux hello ingéré passent **canal**s sans traitement supplémentaire. Vous pouvez utiliser hello suivant encodeurs en temps réel qui produisent plusieurs débits binaires de la diffusion en continu lisse : MediaExcel Ateme, imaginez, Envivio, Cisco et Communications élémentaire. Hello suivants encodeurs en temps réel de sortie RTMP : transcodeurs Adobe Flash Media en direct encodeur (FMLE), Telestream Wirecast, Haivision, Teradek et Tricaster.  Un encodeur en temps réel peut également envoyer un canal tooa du flux à débit binaire unique qui n’est pas activée pour l’encodage live, mais qui n’est pas recommandé. Lorsqu’il est demandé, Media Services diffuse hello flux toocustomers.

  > [!NOTE]
  > À l’aide d’une méthode directe est moyen le plus économique hello toodo la diffusion en continu lorsque vous effectuez plusieurs événements sur une longue période de temps, et que vous avez déjà investi dans encodeurs locaux. Consultez les détails de la [tarification](https://azure.microsoft.com/pricing/details/media-services/) .
  > 
  > 
* Un encodeur dynamique local envoie un flux unique à plusieurs débits canal toohello est activé tooperform live encodage avec Media Services dans un des hello suivant formats : RTMP ou Smooth Streaming (MP4 fragmenté). RTP (MPEG-TS) est également pris en charge, si vous disposez d’un centre de données Azure toohello connexion dédiée. Hello suivant encodeurs en temps réel avec RTMP connus toowork avec des canaux de ce type de sortie : Telestream Wirecast, FMLE. Hello canal effectue ensuite l’encodage dynamique de hello entrant à débit binaire unique flux tooa débits (adaptatif) flux vidéo. Lorsqu’il est demandé, Media Services diffuse hello flux toocustomers.

En commençant avec la version de hello 2.10 de Media Services, lorsque vous créez un canal, vous pouvez spécifier la façon dont vous souhaitez pour votre flux d’entrée du canal tooreceive hello et si vous souhaitez que pour hello canal tooperform live codage de votre flux de données. Deux options s'offrent à vous :

* **Aucun** (pass-through) : spécifiez cette valeur, si vous envisagez de toouse un encodeur dynamique local qui produira des flux de débits (un flux direct). Dans ce cas, les flux entrants hello transmis toohello de sortie sans encodage. Il s’agit de comportement hello d’une version antérieure too2.10 de canal.  
* **Standard** – choisissez cette valeur, si vous envisagez de toouse Media Services tooencode votre flux de débits toomulti de flux en continu à débit binaire unique. Cette méthode est plus économique pour une mise à l’échelle rapide pour les événements peu fréquents. N’oubliez pas qu’il existe un impact sur la facturation pour l’encodage dynamique et vous devez vous rappeler que sans toucher à un canal en direct de codage de hello état « Actif » occasionnent des frais de facturation.  Il est recommandé d’arrêter immédiatement vos canaux en cours d’exécution après votre événement de diffusion en continu en direct est tooavoid complète des frais supplémentaires de toutes les heures.

## <a name="comparison-of-channel-types"></a>Comparaison des types de canaux
Tableau suivant fournit un guide toocomparing hello deux types de canaux de prise en charge par Media Services

| Fonctionnalité | Canal pass-through | Canal standard |
| --- | --- | --- |
| Entrée de transmission unique est encodée en plusieurs débits binaires dans le cloud de hello |Non |OUI |
| Résolution maximale, nombre de couches |1080p, 8 couches, plus de 60 i/s |720p, 6 couches, 30 i/s |
| Protocoles d’entrée |RTMP, Smooth Streaming |RTMP, Smooth Streaming et RTP |
| Prix |Consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/media-services/) , puis cliquez sur l’onglet « Vidéo Live » |Consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/media-services/) |
| Durée maximale |24 x 7 |8 heures |
| Prise en charge de l’insertion d’ardoises |Non |OUI |
| Prise en charge de la signalisation des annonces |Non |OUI |
| Légendes CEA 608/708 pass-through |OUI |Oui |
| Toorecover possibilité de blocages brèves dans la contribution de flux |Oui |Non (défaillance du canal après plus de six secondes sans données d’entrée) |
| Prise en charge des groupes d’images d’entrée non uniformes |OUI |Non. L’entrée doit être constituée de groupes d’images fixes de deux secondes |
| Prise en charge de l’entrée à fréquence d’images variable |OUI |Non. L’entrée doit avoir une fréquence d’images fixe.<br/>Les variations mineures sont tolérées, par exemple pendant les scènes à mouvement élevé. Mais encodeur ne peut pas supprimer too10 frames par seconde. |
| Auto-fermeture des canaux en cas de perte du flux d’entrée |Non |Après 12 heures si aucun programme n’est en cours d’exécution |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Utilisation de canaux recevant un flux continu à débit binaire multiple provenant d’encodeurs locaux (pass-through)
Hello diagramme suivant montre hello de plateforme de hello AMS des composants principaux impliqués dans hello **pass-through** flux de travail.

![Flux de travail live](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Pour plus d’informations, consultez [Utilisation des canaux recevant un flux dynamique à débit binaire multiple provenant d’encodeurs locaux](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Utilisation de canaux qui sont activés tooperform dynamique encodage avec Azure Media Services
Hello diagramme suivant montre hello principales parties de plateforme de AMS hello impliqués dans le flux de travail de diffusion en continu Live où un canal est activé tooperform dynamique encodage avec Media Services.

![Flux de travail live](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Pour plus d’informations, consultez [utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Description d’un canal et de ses composants associés
### <a name="channel"></a>canal
Dans Media Services, les [canaux](https://docs.microsoft.com/rest/api/media/operations/channel)sont responsables du traitement du contenu de vidéo en flux continu. Un canal fournit un point de terminaison d’entrée (URL de réception) que vous fournissez ensuite tooa TRANSCODEUR en temps réel. canal de Hello reçoit des flux d’entrée live d’hello TRANSCODEUR en temps réel et la rend disponible pour la diffusion en continu via un ou plusieurs Streamingendpoint. Les canaux fournissent également un aperçu point de terminaison (URL d’aperçu) que vous utilisez toopreview et validez votre flux de données avant de poursuivre le traitement et de remise.

Vous pouvez obtenir hello réception URL et l’URL d’aperçu hello lorsque vous créez le canal de hello. tooget ces URL, le canal de hello n’a pas toobe en état de hello a démarré. Lorsque vous êtes prêt toostart transmettre des données à partir d’un TRANSCODEUR en temps réel à un canal de hello, hello doit être démarré. Une fois que hello TRANSCODEUR en temps réel démarre la réception de données, vous pouvez afficher un aperçu de votre flux de données.

Chaque compte Media Services peut contenir plusieurs canaux, plusieurs programmes et plusieurs StreamingEndpoints. Selon les besoins de la bande passante et la sécurité des hello, les services StreamingEndpoint peuvent être dédié tooone canaux ou plus. N’importe quel StreamingEndpoint peut assurer l’extraction à partir de n’importe quel canal.

### <a name="program"></a>Programme
A [programme](https://docs.microsoft.com/rest/api/media/operations/program) permet la publication toocontrol hello et stockage des segments dans un flux en direct. Les canaux gèrent des programmes. Hello relation de canal et le programme est très similaire tootraditional média, où un canal possède un flux constant de contenu et un programme est événements étendue toosome a expiré sur le canal.
Vous pouvez spécifier le nombre de hello d’heures que vous voulez tooretain hello enregistrée contenu pour le programme de hello en définissant un hello **ArchiveWindowLength** propriété. Cette valeur peut être définie à partir d’un minimum de 5 minutes tooa 25 heures maximum.

ArchiveWindowLength détermine également hello durée maximale pendant laquelle les clients peuvent effectuer des recherches dans le temps à partir de la position de diffusion en continu hello actuel. Programmes peuvent s’exécuter sur la durée spécifiée hello, mais le contenu qui se trouve derrière la longueur de la fenêtre hello est ignoré en permanence. La valeur de cette propriété détermine également la durée pendant laquelle hello client manifestes peuvent atteindre.

Chaque programme est associé à un élément multimédia. programme de hello toopublish vous devez créer un localisateur pour hello associés actif. Ce localisateur activera toobuild une URL de diffusion en continu que vous pouvez fournir tooyour clients.

Un canal prend en charge jusqu'à toothree qui s’exécutent simultanément des programmes, vous pouvez créer plusieurs archives de hello même flux entrant. Cela vous permet de toopublish et archivage de différentes parties d’un événement en fonction des besoins. Par exemple, vos exigences d’entreprise est tooarchive 6 heures d’un programme, mais toobroadcast uniquement les 10 dernières minutes. tooaccomplish, vous devez toocreate deux des programmes qui s’exécutent simultanément. Un programme a la valeur tooarchive d’événement de hello les 6 heures, mais les programme hello ne sont pas publié. Hello autre programme est ensemble tooarchive pendant 10 minutes et ce programme est publié.

## <a name="billing-implications"></a>Implications de facturation
Un canal commence dès que l’état de transition trop « Running » via hello API de facturation.  

Hello tableau suivant montre comment mappent les États des canaux États toobilling Bonjour API et portail Azure. Notez que les États hello sont légèrement différentes entre hello API et UX de portail. Dès qu’un canal est en état hello « En cours d’exécution » via hello API ou dans hello « Prêt » ou « Streaming » Bonjour portail Azure, la facturation sera active.

Canal de hello toostop de facturation vous davantage, vous avez tooStop hello canal via les API de hello ou Bonjour portail Azure.
Vous êtes responsable de l’arrêt de vos canaux lorsque vous avez terminé avec le canal de hello. Canal de hello toostop échec entraînera la facturation continue.

> [!NOTE]
> Lorsque vous travaillez avec des canaux Standard, AMS automatique fermeture des canaux qui sont toujours en état « Actif » de 12 heures, une fois que les flux d’entrée hello sont perdue et aucun programme en cours d’exécution. Toutefois, vous êtes toujours facturé pour hello de temps hello que canal était en état « Actif ».
>
>

### <a id="states"></a>États de canal ainsi que leur mappage toohello en mode de facturation
état actuel de Hello d’un canal. Les valeurs possibles incluent :

* **Arrêté**. Il s’agit état initial de hello Hello canal après sa création (sauf si le démarrage automatique a été sélectionné dans le portail de hello.) Aucune facturation ne survient dans cet état. Dans cet état, les propriétés de canal hello peuvent être mis à jour, mais de diffusion en continu n’est pas autorisée.
* **Démarrage en cours**. Hello canal est en cours de démarrage. Aucune facturation ne survient dans cet état. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état. Si une erreur se produit, hello canal retourne toohello état arrêté.
* **Exécution en cours**. Hello canal est capable de traiter des flux live. Il facture désormais l'utilisation. Vous devez arrêter tooprevent de canal hello davantage de facturation.
* **En cours d’arrêt**. Hello canal est en cours d’arrêt. Aucune facturation ne survient dans cet état de transition. Aucune mise à jour ou diffusion en continu n’est autorisée durant cet état.
* **Suppression en cours**. Hello canal est en cours de suppression. Aucune facturation ne survient dans cet état de transition. Aucune mise à jour ni aucun streaming ne sont autorisés durant cet état.

Hello tableau suivant montre comment canal indique le mode de facturation toohello mappage.

| État du canal | Indicateurs de l’interface utilisateur du portail | Existe-t-il une facturation ? |
| --- | --- | --- |
| Démarrage en cours |Démarrage en cours |Aucun (état transitoire) |
| Exécution en cours |Prêt (pas de programmes en cours d’exécution)<br/>ou<br/>Diffusion en continu (au moins un programme en cours d'exécution) |OUI |
| En cours d’arrêt |En cours d’arrêt |Aucun (état transitoire) |
| Arrêté |Arrêté |Non |

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Rubriques connexes
[Spécification d’ingestion en direct au format MP4 fragmenté Azure Media Services](media-services-fmp4-live-ingest-overview.md)

[Utilisation de canaux est à activé tooPerform Live encodage avec Azure Media Services](media-services-manage-live-encoder-enabled-channels.md)

[Utilisation des canaux recevant un flux dynamique à débit binaire multiple provenant d’encodeurs locaux](media-services-live-streaming-with-onprem-encoders.md)

[Quotas et limitations](media-services-quotas-and-limitations.md)  

[Concepts Azure Media Services](media-services-concepts.md)
