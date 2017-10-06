---
title: "notes de publication de Services d’aaaMedia | Documents Microsoft"
description: Notes de publication de Media Services
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Notes de publication d'Azure Media Services
Ces notes de publication récapitulent les modifications par rapport aux précédentes versions et les problèmes connus.

> [!NOTE]
> Toohear de nos clients et nous concentrer sur la résolution des problèmes qui vous concernent. tooreport un problème ou poser des questions, veuillez la publier dans hello [Forum MSDN de Azure Media Services].
> 
> 

## <a id="issues"></a>Problèmes actuellement connus
### <a id="general_issues"></a>Problèmes généraux concernant Media Services
| Problème | Description |
| --- | --- |
| Plusieurs en-têtes HTTP courants ne sont pas fournies dans l’API REST de hello. |Si vous développez des applications de service de média à l’aide de hello API REST, vous constatez que certains champs d’en-tête HTTP courants (y compris le CLIENT-REQUEST-ID, REQUEST-ID et RETURN-CLIENT-REQUEST-ID) ne sont pas pris en charge. Hello en-têtes seront ajoutés dans une prochaine mise à jour. |
| L’encodage par pourcentage n’est pas autorisé. |Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé. Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ». En outre, il ne peut exister qu’un seul « . » pour l’extension de nom de fichier hello. |
| Hello méthode ListBlobs qui fait partie de la version du Kit de développement de stockage Azure hello 3.x échoue. |Media Services génère des URL SAS basées sur hello [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) version. Si vous souhaitez toouse SDK Azure Storage toolist objets BLOB dans un conteneur d’objets blob, utilisez hello [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) méthode fait partie de stockage Azure SDK version 2.x. Hello méthode ListBlobs qui fait partie de la version du Kit de développement de stockage Azure hello 3.x échoue. |
| Mécanisme de limitation de Media Services restreint l’utilisation des ressources pour les applications qui rendent excessive de demander un service toohello hello. service de Hello peut retourner le code d’état HTTP Service non disponible (503) hello. |Pour plus d’informations, consultez la description hello du code d’état HTTP 503 de hello Bonjour [Codes d’erreur Azure Media Services](media-services-encoding-error-codes.md) rubrique. |
| Lors de l’interrogation des entités, il existe une limite de 1000 entités retournées à la fois, car il est public reste v2 limite les résultats de too1000 de résultats de requête. |Vous devez toouse **ignorer** et **prendre** (.NET) / **haut** (REST), comme décrit dans [cet exemple .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) et [cette API REST exemple](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Certains clients peuvent provenir de sur un problème de balise de répétition dans le manifeste de diffusion en continu lisse hello. |Pour plus d’informations, consultez [cette](media-services-deliver-content-overview.md#known-issues) section. |
| Les objets du kit SDK Azure Media Services ne peuvent pas être sérialisés et, par conséquent, ne fonctionnent pas avec Azure Caching. |Si vous essayez de tooserialize hello assetcollection du SDK objet tooadd il tooAzure mise en cache, une exception est levée. |
| Les travaux d’encodage échouent avec une chaîne de message « Étape : DownloadFile. Code : System.NullReferenceException ». |workflow d’encodage standard Hello est tooupload d’entrée ou les fichiers vidéo tooan d’entrée actif et envoyer un ou plusieurs travaux d’encodage pour que d’entrée actif, sans autre modification d’entrée actif. Toutefois, si vous modifiez hello d’entrée actif (par exemple par ajout/suppression/changement de nom des fichiers dans hello actif), puis les tâches suivantes peuvent échouer avec une erreur DownloadFile. solution de contournement Hello est toodelete hello d’entrée actif et télécharger à nouveau d’entrée ou les fichiers tooa du nouvel élément multimédia. |

## <a id="rest_version_history"></a>Historique des versions de l’API REST
Pour plus d’informations sur hello historique de version d’API REST Media Services, consultez [référence d’API REST Azure Media Services].

## <a name="june-2017-release"></a>Version de juin 2017

Media Services prend désormais en charge l’[Authentification Azure Active Directory (Azure AD)](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Actuellement, Media Services prend en charge le modèle d’authentification hello Azure Access Control service. Toutefois, l’autorisation Access Control sera déconseillée à compter du 1er juin 2018. Nous vous recommandons de migrer modèle d’authentification Azure AD de toohello dès que possible.

## <a name="march-2017-release"></a>Version de mars 2017

Vous pouvez maintenant utiliser Azure Media Standard trop[générer automatiquement une échelle de la vitesse de transmission](media-services-autogen-bitrate-ladder-with-mes.md) en spécifiant la chaîne de présélection hello « Diffusion adaptative en continu » lors de la création d’une tâche d’encodage. « Diffusion en continu adaptative » est hello – présélection recommandée si vous souhaitez tooencode une vidéo de diffusion en continu avec Media Services. Si vous devez toocustomize un encodage prédéfinis pour votre scénario spécifique, vous pouvez commencer par [ces](media-services-mes-presets-overview.md) prédéfinis.

Vous pouvez maintenant utiliser Azure Media Standard ou Workflow d’encodeur multimédia Premium trop[créer une tâche de codage qui génère les segments fMP4](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Version de février 2017

À partir du 1er avril 2017, n’importe quel enregistrement de la tâche dans votre compte plu de 90 jours est automatiquement supprimé, ainsi que ses enregistrements de tâche associés, même si le nombre total de hello d’enregistrements est au-dessous du quota maximal de hello. Si vous avez besoin des informations de tâche/hello tooarchive, vous pouvez utiliser le code hello décrit [ici](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Version de janvier 2017

Dans Microsoft Azure Media Services (AMS), un **le point de terminaison de diffusion en continu** représente un service de diffusion en continu qui peut fournir du contenu directement de l’application de lecteur tooa client ou tooa réseau de distribution de contenu (CDN) pour une distribution ultérieure. Media Services fournit également une intégration transparente au CDN Azure. flux sortant de Hello à partir d’un service StreamingEndpoint peut être un flux en direct, d’une vidéo à la demande, ou le téléchargement progressif de votre élément multimédia dans votre compte Media Services. Chaque compte Azure Media Services comprend une valeur de point de terminaison de streaming par défaut. Streamingendpoint supplémentaires peut être créés sous le compte de hello. Il existe deux versions du point de terminaison de streaming : 1.0 et 2.0. À compter du 10 janvier 2017, les nouveaux comptes AMS incluront la version 2.0 du point de terminaison de streaming **par défaut**. Supplémentaire que vous ajoutez toothis compte des points de terminaison de diffusion en continu sera également la version 2.0. Cette modification n’affectera pas les comptes existants hello ; Streamingendpoint existant sera la version 1.0 et peut être mis à niveau tooversion 2.0. Avec cette modification, il y aura des changements de comportement, de facturation et de fonctionnalités (pour plus d’informations, consultez [cette rubrique](media-services-streaming-endpoints-overview.md)).

En outre, Azure Media Services depuis la version de hello 2.15, ajouté hello suivant l’entité de point de terminaison de diffusion en continu de propriétés toohello : **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Pour une présentation détaillée de ces propriétés, consultez [ceci](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Version de décembre 2016

Azure Media Services vous permet désormais tooaccess les données de télémétrie/métriques pour ses services. version actuelle de Hello de AMS vous permet de collecter les données de télémétrie de canal en direct, continu, et entités de l’Archive en direct. Pour plus d’informations, consultez [cette rubrique](media-services-telemetry-overview.md) .

## <a id="july_changes16"></a>Version de juillet 2016
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Fichier toomanifest de mises à jour (*. ISM) généré par l’encodage des tâches
Lorsqu’une tâche d’encodage est soumis tooMedia encodeur Standard ou encodeur multimédia Azure, la tâche d’encodage hello génère une [fichier manifeste de diffusion en continu](media-services-deliver-content-overview.md) (* .ism) fichier Bonjour de sortie actif. Avec la dernière version du service hello, syntaxe hello de ce fichier de manifeste de diffusion en continu a été mis à jour.

> [!NOTE]
> syntaxe Hello Hello de diffusion en continu le fichier manifeste (.ism) est réservé à un usage interne et est toochange sujet dans les versions futures. Veuillez ne modifier ou manipuler le contenu de hello de ce fichier.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Un nouveau manifeste de client (*. Fichier ISMC) est généré dans hello de sortie actif lorsqu’une tâche de codage génère un ou plusieurs fichiers MP4
Hello commençant par la dernière version du service hello, après l’achèvement de hello d’une tâche de codage qui génère un ou plusieurs fichiers MP4 fichiers, de sortie Qu'actif contient également un fichier de manifeste (*.ismc) de client en continu. fichier de .ismc de Hello contribue à améliorer les performances de hello de diffusion en continu dynamique. 

> [!NOTE]
> syntaxe Hello du fichier de manifeste (.ismc) de client hello est réservé à un usage interne et est toochange sujet dans les versions futures. Veuillez ne modifier ou manipuler le contenu de hello de ce fichier.
> 
> 

Pour plus d’informations, consultez [ce](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) blog.

### <a name="known-issues"></a>Problèmes connus
Certains clients peuvent provenir de sur un problème de balise de répétition dans le manifeste de diffusion en continu lisse hello. Pour plus d’informations, consultez [cette](media-services-deliver-content-overview.md#known-issues) section.

## <a id="apr_changes16"></a>Version d’avril 2016
### <a name="azure-media-analytics"></a>Azure Media Analytics
Azure Media Services a intégré Azure Media Analytics pour offrir des fonctionnalités vidéo performantes. Pour obtenir des informations détaillées, consultez [Vue d’ensemble d’Azure Media Services Analytics](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (préversion)
Maintenant vous permet de vous toodynamically chiffrer votre HTTP Live Streaming (HLS) de contenu avec Apple FairPlay d’Azure Media Services. Vous pouvez également utiliser AMS licence remise service toodeliver FairPlay licences tooclients. Pour plus d’informations, consultez [utiliser Azure Media Services tooStream votre contenu HLS protégé avec Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Version de février 2016
Hello dernière version du SDK Azure Media Services pour .NET (3.5.3) contient un correctif de bogue Widevine connexe. problème de Hello était : AssetDeliveryPolicy n’a pas pu être réutilisé pour plusieurs éléments multimédias chiffrés avec Widevine. Dans le cadre de cette hello bogue suivant la propriété a été ajoutée toohello SDK : **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Version de janvier 2016
Unités réservées d’encodage renommé tooreduce de confusion avec les noms de l’encodeur.

Hello basique, Standard et Premium unités réservées d’encodage sont renommés tooS1, S2, et réservées S3 unités, respectivement.  Les clients à l’aide de base RUs encodage aujourd'hui verront S1 en tant qu’étiquette hello dans le portail Azure (et, dans la nomenclature de hello), lors de la norme et Premium verront étiquettes hello S2 et S3 respectivement. 

## <a id="dec_changes_15"></a>Version de décembre 2015

### <a name="azure-media-encoder-deprecation-announcement"></a>Annonce de désapprobation d’Azure Media Encoder

Azure Media Encoder sera déconseillée à compter d’environ 12 mois à partir de la version de hello de Media Encoder Standard.

### <a name="azure-sdk-for-php"></a>Kit SDK Azure pour PHP
équipe de développement logiciel Azure SDK Hello publié une nouvelle version de hello [Azure SDK pour PHP](http://github.com/Azure/azure-sdk-for-php) package qui contient les nouvelles fonctionnalités et mises à jour pour Microsoft Azure Media Services. En particulier, hello Azure Media Services SDK pour PHP, maintenant prend en charge hello dernières [protection du contenu](media-services-content-protection-overview.md) fonctionnalités : chiffrement dynamique avec AES et gestion des droits numériques (PlayReady et Widevine) avec et sans restriction de jeton. Il prend également en charge la mise à l’échelle des [Unités d’encodage](media-services-dotnet-encoding-units.md).

Pour plus d'informations, consultez les pages suivantes :

* Hello [Microsoft Azure Media Services SDK pour PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blog.
* suivant de Hello [exemples de code](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp vous aider à démarrer rapidement :
  * **vodworkflow_aes.PHP**: il s’agit d’un fichier PHP qui montre comment toouse chiffrement dynamique AES-128 et le Service de remise de clés. Il est basé sur .NET, exemple hello expliquée dans [cela](media-services-protect-with-aes128.md) l’article.
  * **vodworkflow_aes.PHP**: il s’agit d’un fichier PHP qui montre comment toouse du chiffrement dynamique PlayReady et Service de remise de licences. Il est basé sur .NET, exemple hello expliquée dans [cela](media-services-protect-with-drm.md) l’article.
  * **scale_encoding_units.PHP**: il s’agit d’un fichier PHP qui montre comment l’encodage de tooscale réservés unité.

## <a id="nov_changes_15"></a>Version de novembre 2015
Azure Media Services propose désormais un service de remise de licence Google Widevine dans le cloud de hello. Pour plus d’informations, consultez trop[ce blog annonce](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Consultez également [ce didacticiel](media-services-protect-with-drm.md) et le [référentiel GitHub](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Notez que les services de distribution de licences Widevine fournis par Azure Media Services sont en version préliminaire. Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Version d’octobre 2015
Azure Media Services (AMS) est désormais dynamique Bonjour suivant des centres de données : Brésil Sud, Inde-ouest, l’Inde Sud et Inde centrale. Vous pouvez maintenant utiliser hello portail Azure trop[créer des comptes de Service multimédia](media-services-portal-create-account.md) et effectuer diverses tâches décrites [ici](https://azure.microsoft.com/documentation/services/media-services/). La fonctionnalité Live Encoding n'est cependant pas activée dans ces centres de données. En outre, tous les types d'unités réservées d'encodage ne sont pas disponibles dans ces centres de données.

* Sud du Brésil : seules les unités réservées d’encodage standard et de base sont disponibles.
* Ouest de l’Inde, sud de l’Inde et Inde centrale : seules les unités réservées d’encodage de base sont disponibles.

## <a id="september_changes_15"></a>Version de septembre 2015
* AMS maintenant offres hello capacité tooprotect vidéo à la demande (VOD) et des flux Live avec la technologie de gestion des droits numériques Widevine modulaire. Vous pouvez utiliser hello suivant remise services partenaires toohelp vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    Vous pouvez utiliser [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (depuis la version de hello 3.5.1) ou REST API tooconfigure votre toouse AssetDeliveryConfiguration Widevine.  
* AMS a ajouté la prise en charge des vidéos Apple ProRes. Vous pouvez à présent télécharger vos fichiers vidéos sources QuickTime qui utilisent Apple ProRes ou d’autres codecs. Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* Vous pouvez maintenant utiliser Media Encoder Standard toodo découpage inférieur et dynamique archive d’extraction. Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* Hello suivant le filtrage des mises à jour ont été apportée : 
  
  * Vous pouvez désormais utiliser le format Apple HTTP Live Streaming (HLS) avec filtre audio uniquement. Cette mise à jour vous permet de piste audio uniquement de tooremove en spécifiant (audio uniquement = false) dans l’URL de hello.
  * Lorsque vous définissez des filtres pour vos ressources, vous avez maintenant toocombine de capacité (too3 haut) plusieurs filtres dans une URL unique.
    
    Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) .
* AMS prend désormais en charge I-Frames dans HLS v4. La prise en charge d'I-Frame optimise les opérations d’avance rapide et de retour arrière. Par défaut, toutes les sorties HLS v4 incluent une sélection I-Frame (EXT-X-I-FRAME-STREAM-INF).
  
    Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) .

## <a id="august_changes_15"></a>Version d’août 2015
* Le kit SDK Azure Media Services pour Java V0.8.0 et de nouveaux exemples sont désormais disponibles. Pour plus d'informations, consultez les pages suivantes :
  
  * [Billet de blog](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Référentiel d’exemples Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Mise à jour d’Azure Media Player avec prise en charge des flux audio multiples. Pour plus d'informations, consultez les pages suivantes :
  * [Billet de blog](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Version de juillet 2015
* Annonce hello générales de Media Encoder Standard. Pour plus d’informations, consultez [ce billet de blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)
  
    Media Encoder Standard utilise les présélections décrites dans [cette](http://go.microsoft.com/fwlink/?LinkId=618336) section. Notez que lorsque vous utilisez une présélection de 4k encode, vous devez obtenir hello **Premium** réservé de type d’unité. Pour plus d’informations, consultez [comment tooScale codage](media-services-scale-media-processing-overview.md).
* Légendes en temps réel en direct avec Azure Media Services et Azure Media Player. Pour plus d’informations, consultez [ce billet de blog](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>Mises à jour du kit SDK .NET de Media Services
La version du kit SDK .NET Azure Media Services est maintenant 3.4.0.0. Hello suivant la fonctionnalité a été ajoutée dans cette version :  

* Prise en charge implémentée d'une archive en direct. Notez que vous ne pouvez pas télécharger un actif contenant une archive en direct.
* Prise en charge implémentée des filtres dynamiques.
* Fonctionnalité implémentée qui permet de conteneur de stockage tookeep utilisateurs lors de la suppression d’élément multimédia.
* Correctifs de bogues tooretry les paramètres associés dans les canaux.
* **Workflow d’encodeur multimédia premium** activé.

## <a id="june_changes_15"></a>Version de juin 2015
### <a name="media-services-net-sdk-updates"></a>Mises à jour du kit SDK .NET de Media Services
Le kit SDK Azure Media Services en est maintenant à la version 3.3.0.0. Hello suivant la fonctionnalité a été ajoutée dans cette version :  

* prise en charge de la spécification OpenId Connect Discovery,
* prise en charge de la gestion du renouvellement de clés côté fournisseur d’identité. 

Si vous utilisez un fournisseur d’identité qui expose le document de découverte OpenID Connect (hello procéder comme fournisseurs suivants : Azure Active Directory, Google, Salesforce), vous pouvez demander à tooobtain Azure Media Services clés pour la validation du jeton Web JSON à partir de signature OpenID se connecter à des spécifications de découverte. 

Pour plus d’informations, consultez [à l’aide de clés Json Web à partir de toowork spécification de découverte OpenID Connect avec JSON du jeton d’authentification dans Azure Media Services](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Version de mai 2015
Annonce hello nouvelles fonctions suivantes :

* [Une version préliminaire de l’encodage en temps réel avec Media Services Live](media-services-manage-live-encoder-enabled-channels.md)
* [Un manifeste dynamique](media-services-dynamic-manifest-overview.md)
* [Une version préliminaire du processeur multimédia Azure Media Hyperlapse](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Version d’avril 2015
### <a name="general-media-services-updates"></a>Mises à jour générales de Media Services
* [Annonce d’Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* En commençant par 2.10 de Media Services REST, les canaux sont tooingest configuré un protocole RTMP, sont créées avec principal et secondaire URL d’ingestion. Pour plus d’informations, consultez la rubrique [Configurations de l'entrée (réception) des canaux](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Mises à jour d’Azure Media Indexer
* Prise en charge de l’espagnol
* Nouveau format de configuration xml

Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Mises à jour du Kit de développement logiciel (SDK) .NET de Media Services
La version du Kit de développement logiciel (SDK) Azure Media Services est désormais la 3.2.0.0.

Hello Voici quelques-uns des client hello faisant face à des mises à jour :

* **Modification avec rupture**: modifié **TokenRestrictionTemplate.Issuer** et **TokenRestrictionTemplate.Audience** toobe de type chaîne.
* Les mises à jour liées toocreating des stratégies de nouvelle tentative personnalisée.
* Correctifs de bogues liés toouploading téléchargement de fichiers.
* Hello **MediaServicesCredentials** classe accepte désormais tooauthenticate de point de terminaison de contrôle accès primaire et secondaire par rapport.

## <a id="march_changes_15"></a>Version de mars 2015
### <a name="general-media-services-updates"></a>Mises à jour générales de Media Services
* Media Services assure à présent l’intégration au CDN Azure. hello toosupport hello integration, **CdnEnabled** propriété a été ajoutée trop**StreamingEndpoint**.  **CdnEnabled** peut être utilisée avec l’API REST à partir de la version 2.9 (pour plus d’informations, consultez la rubrique [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** peut être utilisée avec le Kit de développement logiciel (SDK) .NET à partir de la version 3.1.0.2 (pour plus d’informations, consultez la rubrique [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Annonce de **Media Encoder Premium Workflow**. Pour plus d’informations, consultez la page [Présentation de l’encodage Premium dans Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Version de février 2015
### <a name="general-media-services-updates"></a>Mises à jour générales de Media Services
La dernière version de l’API REST de Media Services est la version 2.9. À compter de cette version, vous pouvez activer hello intégration d’Azure CDN avec les points de terminaison de diffusion en continu. Pour plus d’informations, consultez la rubrique [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Version de janvier 2015
### <a name="general-media-services-updates"></a>Mises à jour générales de Media Services
Annonce de la disponibilité générale de la protection du contenu avec chiffrement dynamique. Pour plus d’informations, consultez [Azure Media Services améliore la sécurité de la diffusion en continu avec la disponibilité générale de la technologie de DRM](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/).

### <a name="media-services-net-sdk-updates"></a>Mises à jour du Kit de développement logiciel (SDK) .NET de Media Services
La version actuelle du Kit de développement logiciel (SDK) Azure Media Services est désormais la 3.1.0.1.

Cette version marque le constructeur de Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate hello par défaut comme obsolète. Hello nouveau constructeur prend TokenType en tant qu’argument.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Version de décembre 2014
### <a name="general-media-services-updates"></a>Mises à jour générales de Media Services
* Certaines mises à jour et nouvelles fonctionnalités ont été ajoutées processeur Azure toohello indexeur. Pour plus d’informations, consultez les [Notes de publication d’Azure Media Indexer 1.1.6.7](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/).
* Ajout d’une nouvelle API REST qui vous permet de tooupdate unités réservées d’encodage : [EncodingReservedUnitType avec reste](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Ajout de la prise en charge CORS pour le service de distribution des clés.
* Amélioration des performances d'interrogation des options de stratégie d'autorisation.
* Dans le centre de données en Chine, hello [URL de fourniture de clé](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) est désormais par client (comme dans d’autres centres de données).
* Ajout de la durée cible TLS automatique. Lors de la diffusion en continu, TLS est toujours empaquetée de façon dynamique. Par défaut, Media Services calcule automatiquement coefficient d’empaquetage de segment HLS (FragmentsPerSegment) en fonction de hello keyframe intervalle (KeyFrameInterval), également appelée tooas groupe d’images : groupe d’images, qui est reçu à partir de l’encodeur en temps réel de hello. Pour plus d'informations, consultez la page [Utilisation de la diffusion en continu Azure Media Services].

### <a name="media-services-net-sdk-updates"></a>Mises à jour du Kit de développement logiciel (SDK) .NET de Media Services
* [Kit de développement logiciel (SDK) Azure Media Services](http://www.nuget.org/packages/windowsazure.mediaservices/) est maintenant la 3.1.0.0.
* Mise à niveau hello .net SDK dépendance too.NET 4.5 Framework.
* Ajouter une nouvelle API qui permet de vous tooupdate unités réservées d’encodage. Pour plus d’informations, consultez la page [Mise à jour du type d’unité réservé et augmentation des RU d’encodage à l’aide de .NET](media-services-dotnet-encoding-units.md).
* Ajout de la prise en charge JWT (Jeton web JSON) de l'authentification des jetons. Pour plus d’informations, consultez la page [Authentification des jetons JWT dans Azure Media Services et chiffrement dynamique](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).
* Décalages relatifs ajoutés pour BeginDate et ExpirationDate dans le modèle de licence PlayReady hello.

## <a id="november_changes_14"></a>Version de novembre 2014
* Media Services vous permet désormais tooingest un live diffusion en continu lisse (FMP4) contenu via une connexion SSL. tooingest via le protocole SSL, assurez-vous que tooupdate hello tooHTTPS de l’URL de réception.  Notez qu’actuellement AMS ne prend pas en charge SSL avec les domaines personnalisés.  Pour plus d’informations sur la diffusion en continu en direct, consultez la page [Utilisation de la diffusion en continu Azure Media Services].
* Actuellement, vous ne pouvez pas ingérer un flux RTMP en direct sur une connexion SSL.
* Vous pouvez uniquement diffuser via le protocole SSL si hello point de terminaison à partir duquel vous distribuez votre contenu de diffusion en continu a été créé après le 10 septembre 2014. Si votre URL de diffusion en continu est basés sur hello de diffusion en continu des points de terminaison créés après le 10 septembre, hello URL contient « streaming.mediaservices.windows.net » (hello nouveau format). URL de diffusion en continu qui contiennent « origin.mediaservices.windows.net » (hello ancien format) ne prennent pas en charge SSL. Si votre URL est dans un ancien format de hello et souhaitez toostream en mesure de toobe via le protocole SSL, [créer un nouveau point de terminaison de diffusion en continu](media-services-portal-manage-streaming-endpoints.md). Utilisez des URL créés en fonction de hello new de diffusion en continu toostream de point de terminaison votre contenu via le protocole SSL.

## <a id="october_changes_14"></a>Version d’octobre 2014
### <a id="new_encoder_release"></a>Version de l’encodeur Media Services
Annonce hello nouvelle version de Media Services Azure Media Encoder. Avec hello dernière Azure Media Encoder vous payez uniquement pour sortie Go, mais sinon Nouvel encodeur de hello est compatible avec l’encodeur hello précédente de la fonctionnalité. Pour plus d'informations, consultez la page [Tarification – Media Services].

### <a id="oct_sdk"></a>Kit de développement logiciel (SDK) .NET de Media Services
La dernière version du package Extensions du Kit de développement logiciel (SDK) de Media Services pour .NET est la version 2.0.0.3.

La dernière version du Kit de développement logiciel (SDK) de Media Services pour .NET est la version 3.0.0.8.

Hello modifications suivantes ont été apportée :

* Refactorisation dans les classes de stratégie de nouvelles tentatives.
* Ajout d’en-têtes de demande utilisateur agent chaîne toohttp.
* Ajout de l'étape de génération de la restauration NuGet.
* Fixation scénario tests toouse x509 cert à partir du référentiel.
* Validation des paramètres lors de la mise à jour du canal et de la fin de la diffusion en continu.

### <a name="new-github-repository-toohost-media-services-samples"></a>Nouveaux exemples de Media Services toohost référentiel GitHub
Ces exemples se trouvent dans le [référentiel GitHub d’exemples Azure Media Services](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Version de septembre 2014
La dernière version des métadonnées REST de Media Services est la version 2.7. Pour plus d’informations sur hello dernières reste mises à jour, consultez [référence d’API REST Azure Media Services].

La dernière version du Kit de développement logiciel (SDK) de Media Services pour .NET est la version 3.0.0.7

### <a id="sept_14_breaking_changes"></a>Dernières modifications
* **Origine** a été renommé trop[StreamingEndpoint].
* Un changement de comportement de valeur par défaut hello lors de l’utilisation de hello **portail Azure** tooencode et publier des fichiers MP4.

Auparavant, lorsque vous utilisez hello portail classique Azure toopublish un seul fichier vidéo élément multimédia MP4 en une URL SAS serait créée (URL SAP permettent hello de toodownload vidéo à partir d’un stockage d’objets blob). Actuellement, lorsque vous utilisez hello portail classique Azure tooencode et que vous publiez ensuite un élément multimédia de vidéo MP4 à fichier unique, hello généré URL points tooan Azure Media Services point de terminaison de diffusion en continu.  Cette modification n’affecte pas les vidéos MP4 qui sont directement téléchargées tooMedia Services et publiées sans être encodées par Azure Media Services.

Vous avez actuellement hello suivant problème hello de toosolve deux options.

* Activer des unités de diffusion en continu et utiliser actif de mise en package dynamique toostream hello .mp4 en tant qu’une présentation de diffusion en continu lisse.
* Créer un toodownload url de SAP (ou lire progressivement) hello .mp4. Pour plus d’informations sur la façon toocreate un localisateur SAS, consultez [fourniture de contenu].

### <a id="sept_14_GA_changes"></a>Nouvelles fonctionnalités/nouveaux scénarios intégrés à la version grand public
* **Processeur d'indexation multimédia**. Pour plus d'informations, consultez la page [Indexation des fichiers multimédias avec Azure Media Indexer].
* Hello [StreamingEndpoint] entité vous permet désormais de noms de domaine personnalisé (hôte) tooadd.
  
    Pour un nom de domaine personnalisé toobe utilisé comme nom de point de terminaison de diffusion en continu de hello Media Services, vous devez tooyour de noms d’hôte personnalisé tooadd point de terminaison de diffusion en continu. Utilisez hello API REST Media Services ou le Kit de développement .NET tooadd noms d’hôtes personnalisés.
  
    Hello suivant considérations s’appliquent :
  
  * Vous devez être propriétaire de hello hello personnalisée du nom de domaine.
  * propriété Hello hello du nom de domaine doit être validée par Azure Media Services. domaine de hello toovalidate, créer un enregistrement CName qui mappe <MediaServicesAccountId>.<parent domain> tooverifydns. < zone-dns-mediaservices >. 
  * Vous devez créer un autre enregistrement CName qui mappe le nom d’hôte hello hôte personnalisé nom (par exemple, sports.contoso.com) tooyour Media Services de StreamingEndpont (par exemple, amstest.streaming.mediaservices.windows.net).

    Pour plus d’informations, consultez hello **CustomHostNames** propriété Bonjour [StreamingEndpoint] rubrique.

### <a id="sept_14_preview_changes"></a>Nouvelles fonctionnalités/scénarios qui font partie de la version préliminaire publique de hello
* Aperçu de la diffusion en continu. Pour plus d'informations, consultez la page [Utilisation de la diffusion en continu Azure Media Services].
* Service de distribution des clés. Pour plus d'informations, consultez la page [Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés].
* Chiffrement dynamique AES. Pour plus d'informations, consultez la page [Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés].
* Service de distribution des licences PlayReady. Pour plus d'informations, consultez la page [Utilisation du chiffrement dynamique et du service de distribution des licences PlayReady].
* Chiffrement dynamique PlayReady. Pour plus d'informations, consultez la page [Utilisation du chiffrement dynamique et du service de distribution des licences PlayReady].
* Modèle de licence PlayReady de Media Services. Pour plus d'informations, consultez la page [Présentation du modèle de licence PlayReady de Media Services].
* Diffusion en continu d'éléments multimédias à chiffrement de stockage. Pour plus d'informations, consultez la page [Diffusion en continu de contenu à chiffrement de stockage].

## <a id="august_changes_14"></a>Version d’août 2014
Lorsque vous encodez un élément multimédia, une ressource en sortie est générée à l’achèvement de la tâche de codage hello. Jusqu'à cette version, l'encodeur Media Services produisait des métadonnées sur les éléments multimédias de sortie. En commençant par cet encodeur de hello version génère également des métadonnées sur les éléments multimédias d’entrée. Pour plus d’informations, consultez hello [entrée métadonnées] et [sortie métadonnées] rubriques.

## <a id="july_changes_14"></a>Version de juillet 2014
Hello suivant les correctifs de bogues ont été apportée pour hello Azure Media Services Packager et chiffreur :

* Uniquement audio est lu lorsque transmultiplexage un tooHTTP de ressource archive en direct de la diffusion en continu : ce problème a été corrigé et maintenant audio et vidéo sont lus.
* Lors de l’empaquetage d’un chiffrement d’enveloppe AES 128 bits et de diffusion en continu de tooHTTP actif, les flux hello empaqueté ne sont pas lus sur les appareils Android : ce bogue a été résolu et les flux empaquetés hello est lu sur les appareils Android qui prennent en charge la diffusion en continu HTTP.

## <a id="may_changes_14"></a>Version de mai 2014
### <a id="may_14_changes"></a>Mises à jour générales de Media Services
Vous pouvez maintenant utiliser [empaquetage dynamique] toostream HTTP Live Streaming (HLS) v3. toostream HLS v3, ajoutez hello suivant le chemin d’accès du localisateur origine format toohello : * .ism/manifest(format=m3u8-aapl-v3). Pour plus d'informations, consultez le [blog de Nick Drouin].

Désormais, la mise en package dynamique prend également en charge la transmission du format HLS (v3 et v4) chiffré avec PlayReady sur la base de la diffusion en continu lisse statiquement chiffrée avec PlayReady. Pour plus d’informations sur la façon de tooencrypt Smooth Streaming avec PlayReady, consultez [protection contenu Smooth Streaming avec PlayReady].

### <a name="may_14_donnet_changes"></a>Mises à jour du Kit de développement logiciel (SDK) .NET de Media Services
Hello suivant améliorations est incluse dans hello version de Media Services .NET SDK 3.0.0.5 :

* Vitesse supérieure et meilleure résilience pour le chargement/téléchargement des éléments multimédias.
* Améliorations apportées à la logique de nouvelle tentative et à la gestion des exceptions temporaires : 
  
  * La détection des erreurs temporaires et la logique de nouvelle tentative ont été améliorées pour les exceptions déclenchées par l'interrogation, l'enregistrement des modifications et le chargement ou téléchargement de fichiers. 
  * En cas d'exceptions Web (par exemple, lors d'une demande de jeton ACS), vous noterez que les erreurs irrécupérables échouent plus rapidement maintenant.

Pour plus d’informations, consultez [logique de nouvelle tentative dans hello Media Services SDK pour .NET].

## <a id="april_changes_14"></a>Version de l’encodeur d’avril 2014
### <a name="april_14_enocer_changes"></a>Mises à jour de l’encodeur Media Services
* Prise en charge pour la réception de fichiers AVI créés à l’aide d’éditeur non linéaire de hello Grass Valley EDIUS, où hello vidéo est légèrement compressée à l’aide de codec de Grass Valley HQ/HQX. Pour plus d’informations, consultez [Grass Valley annonce EDIUS 7 Streaming via hello Cloud].
* Prise en charge supplémentaire pour spécifiant hello convention d’affectation de noms pour les fichiers hello produits par hello encodeur multimédia. Pour plus d’informations, consultez la page [Contrôle des noms de fichier de sortie de l'encodeur Media Services].
* Ajout de la prise en charge des superpositions vidéo et/ou audio. Pour plus d’informations, consultez la page [Création de superpositions].
* Ajout de la prise en charge de l'assemblage de plusieurs séquences vidéo. Pour plus d'informations, consultez la page [Assemblage de séquences vidéo].
* Correction d’un bogue lié tootranscoding de MP4s où hello audio était encodée avec MPEG-1 Audio layer 3 (aka MP3).

## <a id="jan_feb_changes_14"></a>Versions de janvier/février 2014
### <a name="jan_fab_14_donnet_changes"></a>Kit de développement logiciel (SDK) Azure Media Services pour .NET 3.0.0.1, 3.0.0.2 et 3.0.0.3
modifications Hello dans les versions 3.0.0.1 et 3.0.0.2 sont les suivantes :

* Résolution des problèmes liés à toousage des requêtes LINQ avec les instructions OrderBy.
* Division des solutions de test dans [GitHub] en tests unitaires et tests basés sur des scénarios.

Pour plus d’informations sur les modifications de hello, consultez : [libère d’Azure Media Services .NET SDK versions 3.0.0.1 et 3.0.0.2].

Hello modifications suivantes ont été apportée à la version 3.0.0.3 :

* Version de mise à niveau de stockage Azure dépendances toouse 3.0.3.0. 
* Problème de compatibilité descendante résolu pour les versions 3.0*.* . 

## <a id="december_changes_13"></a>Version de décembre 2013
### <a name="dec_13_donnet_changes"></a>Kit de développement logiciel (SDK) Azure Media Services pour .NET 3.0.0.0
> [!NOTE]
> Les versions 3.0.x.x ne présentent pas de compatibilité descendante avec les versions 2.4.x.x.
> 
> 

version la plus récente Hello Hello SDK Media Services est désormais 3.0.0.0. Vous pouvez télécharger le dernier package de hello de Nuget ou obtenir des bits hello de [GitHub].

À compter de hello SDK Media Services version 3.0.0.0, vous pouvez réutiliser hello [Azure Active Directory Access Control Service (ACS)] jetons. Pour plus d’informations, consultez hello « réutilisation des jetons contrôle d’accès Service » section Bonjour [connexion tooMedia Services avec hello Media Services SDK pour .NET] rubrique.

### <a name="dec_13_donnet_ext_changes"></a>Kit de développement logiciel (SDK) Azure Media Services pour .NET 2.0.0.0
Hello Extensions SDK Azure Media Services pour .NET est un ensemble de méthodes d’extension et fonctions d’assistance qui simplifieront votre code et le rendre plus facile toodevelop avec Azure Media Services. Vous pouvez obtenir les dernières informations hello de [Extensions de Azure Media Services .NET SDK].

## <a id="november_changes_13"></a>Version de novembre 2013
### <a name="nov_13_donnet_changes"></a>Modifications apportées au Kit de développement logiciel (SDK) Azure Media Services pour .NET
À compter de cette version, hello Media Services SDK pour .NET gère les erreurs temporaires qui peuvent se produire lors de la couche d’API REST Media Services appelle toohello.

## <a id="august_changes_13"></a>Version d’août 2013
### <a name="aug_13_powershell_changes"></a>Cmdlets PowerShell de Media Services incluses dans les outils du Kit de développement logiciel Azure
Hello suivant d’applets de commande PowerShell Media Services est désormais incluse dans [azure-sdk-tools].

* Get-AzureMediaServices 
  
    Par exemple, `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Par exemple, `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Par exemple, `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Par exemple, `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Version de juin 2013
### <a name="june_13_general_changes"></a>Modifications apportées à Azure Media Services
modifications de Hello mentionnées dans cette section sont mises à jour incluses dans hello que mises à jour de juin 2013 Media Services.

* Capacité toolink des comptes de stockage de plusieurs tooa compte Media Services. 
  
    StorageAccount
  
    Asset.StorageAccountName and Asset.StorageAccount
* Capacité tooupdate Job.Priority. 
* Entités et propriétés liées aux notifications : 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Travail
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Modifications apportées au Kit de développement logiciel (SDK) Azure Media Services pour .NET
Hello modifications suivantes sont incluses dans juin 2013 libère Media Services SDK. Hello dernière Media Services SDK est disponible sur GitHub.

* Depuis la version de hello 2.3.0.0, hello SDK Media Services prend en charge la liaison de plusieurs tooa de comptes de stockage compte Media Services. Hello API suivantes prennent en charge cette fonctionnalité :
  
    Hello IStorageAccount type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts propriété.
  
    Hello StorageAccount propriété.
  
    Hello StorageAccountName propriété.
  
    Pour plus d'informations, consultez la page [Gestion des éléments multimédias Media Services sur plusieurs comptes de stockage].
* API liées aux notifications. Depuis la version de hello 2.2.0.0 que vous avez des notifications du stockage de file d’attente hello capacité toolisten tooAzure. Pour plus d'informations, consultez la page [Gestion des notifications de travaux de Media Services].
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions propriété.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState type.
* Dépendance sur hello Client de stockage Azure SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Dépendance par rapport à OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>Version de décembre 2012
### <a name="dec_12_dotnet_changes"></a>Modifications apportées au Kit de développement logiciel (SDK) Azure Media Services pour .NET
* Intellisense : ajout de la documentation Intellisense manquante pour de nombreux types.
* Microsoft.Practices.TransientFaultHandling.Core : Résolution d’un problème où hello SDK était encore une dépendance tooan ancienne version de cet assembly. Hello SDK désormais référence la version 5.1.1209.1 de cet assembly.

Résout les problèmes détectés dans hello SDK de novembre 2012 :

* IAsset.Locators.Count : ce nombre est maintenant indiqué correctement sur les nouvelles interfaces IAsset après la suppression de tous les localisateurs.
* IAssetFile.ContentFileSize : cette valeur est maintenant définie correctement après un téléchargement par IAssetFile.Upload(filepath).
* IAssetFile.ContentFileSize : cette propriété peut désormais être définie pendant la création d'un fichier multimédia. Elle était jusqu'à présent en lecture seule.
* Iassetfile.upload (FilePath) : Résolution d’un problème où cette méthode de téléchargement synchrone a été levée hello l’erreur suivante lors du chargement des actifs de toohello plusieurs fichiers. Erreur de Hello a été « Échec de demande de hello tooauthenticate de serveur. Assurez-vous que valeur hello d’en-tête d’autorisation est formé correctement, notamment la signature de hello. »
* IAssetFile.UploadAsync : résolution du problème qui empêchait de télécharger simultanément plus de 5 fichiers.
* IAssetFile.UploadProgressChanged : Cet événement est désormais fourni par hello SDK.
* IAssetFile.DownloadAsync(string, BlobTransferClient, ILocator, CancellationToken) : cette surcharge de méthode est désormais fournie.
* IAssetFile.DownloadAsync : résolution du problème qui empêchait de télécharger simultanément plus de 5 fichiers.
* Iassetfile.Delete () : Résolution d’un problème où appel de delete peut lever une exception si aucun fichier n’a été chargé pour hello IAssetFile.
* Travaux : Résolution d’un problème où une « MP4 tooSmooth flux de données de tâche » avec une « tâche de Protection PlayReady » à l’aide d’un modèle de tâche de chaînage ne crée pas toutes les tâches du tout.
* Encryptionutils.getcertificatefromstore () : Cette méthode ne lève plus une exception de référence null en raison d’échecs de tooa recherche le certificat de hello basé sur les problèmes de configuration de certificat.

## <a id="november_changes_12"></a>Version de novembre 2012
Hello modifications mentionnées dans cette section ont été mises à jour incluses dans hello novembre 2012 (version 2.0.0.0) SDK. Ces modifications peuvent exiger un code écrit pour hello juin 2012 aperçu SDK version toobe modifier ou réécrire.

* Éléments multimédias
  
    IAsset.Create (assetname) est la fonction de création d’élément multimédia hello uniquement. IAsset.Create ne télécharge plus les fichiers dans le cadre de l’appel de méthode hello. Utilisez IAssetFile pour le téléchargement.
  
    méthode IAsset.Publish de Hello et valeur d’énumération AssetState.Publish hello ont été supprimées de hello Services SDK. Tous les codes qui dépendent de cette valeur doivent être réécrits.
* FileInfo
  
    Cette classe a été supprimée et remplacée par IAssetFile.
  
    IAssetFiles
  
    IAssetFile remplace FileInfo et présente un comportement différent. toouse, d’instancier l’objet IAssetFiles de hello, suivi d’un téléchargement du fichier à l’aide de hello Media Services SDK ou hello SDK Azure Storage. Hello suivant surcharges IAssetFile.Upload peut être utilisé :
  
  * Iassetfile.upload (FilePath) : Une méthode synchrone qui bloque le thread de hello et est recommandée uniquement lors du téléchargement d’un seul fichier.
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken) : méthode asynchrone. Il s’agit de mécanisme de téléchargement hello préféré. 
    
    Bogue connu : à l’aide de hello cancellationToken annule en effet téléchargement de hello ; Toutefois, état d’annulation hello des tâches de hello peut être un nombre d’états. Vous devez saisir et traiter les exceptions correctement.
* Localisateurs
  
    les versions spécifiques d’origine Hello ont été supprimées. contexte de Hello SAP spécifique. Locators.CreateSasLocator (asset, accessPolicy) seront marquées comme étant déconseillée ou supprimée en disponibilité générale. Consultez les localisateurs hello section sous nouvelles fonctionnalités pour le comportement de mise à jour.

## <a id="june_changes_12"></a>Version préliminaire de juin 2012
Hello suivant la fonctionnalité était nouvelle dans la version de novembre de hello de hello SDK.

* Suppression des entités
  
    IAsset, IAssetFile, ILocator, iaccesspolicy et IContentKey objets sont désormais supprimés au niveau de l’objet hello, c'est-à-dire IObject.Delete () au lieu de demander une suppression Bonjour Collection, qui est (objinstance).
* Localisateurs
  
    Les localisateurs doivent désormais être créés à l’aide de la méthode CreateLocator de hello et utiliser des valeurs d’énumération LocatorType.SAS ou LocatorType.OnDemandOrigin hello en tant qu’argument pour le type de localisateur spécifique de hello souhaité toocreate.
  
    Nouvelles propriétés ont été ajoutées tooLocators toomake il plus facile tooobtain URI utilisables pour votre contenu. Cette nouvelle conception des localisateurs était destinée à tooprovide plus de souplesse future extensibilité tierce, d’augmenter la facilité d’utilisation pour les applications clientes multimédia.
* Prise en charge de la méthode asynchrone
  
    Prise en charge asynchrone a été ajouté tooall méthodes.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Forum MSDN de Azure Media Services]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[référence d’API REST Azure Media Services]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[Tarification – Media Services]: http://azure.microsoft.com/pricing/details/media-services/
[entrée métadonnées]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[sortie métadonnées]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[fourniture de contenu]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[Indexation des fichiers multimédias avec Azure Media Indexer]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Utilisation de la diffusion en continu Azure Media Services]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[Utilisation du chiffrement dynamique et du service de distribution des licences PlayReady]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Présentation du modèle de licence PlayReady de Media Services]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[Diffusion en continu de contenu à chiffrement de stockage]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[empaquetage dynamique]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[blog de Nick Drouin]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[protection contenu Smooth Streaming avec PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[logique de nouvelle tentative dans hello Media Services SDK pour .NET]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Grass Valley annonce EDIUS 7 Streaming via hello Cloud]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[Contrôle des noms de fichier de sortie de l'encodeur Media Services]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[Création de superpositions]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Assemblage de séquences vidéo]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[libère d’Azure Media Services .NET SDK versions 3.0.0.1 et 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory Access Control Service (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[connexion tooMedia Services avec hello Media Services SDK pour .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Extensions de Azure Media Services .NET SDK]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Gestion des éléments multimédias Media Services sur plusieurs comptes de stockage]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[Gestion des notifications de travaux de Media Services]: http://msdn.microsoft.com/library/azure/dn261241.aspx

