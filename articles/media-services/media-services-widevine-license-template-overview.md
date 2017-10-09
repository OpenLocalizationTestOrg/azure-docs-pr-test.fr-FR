---
title: "vue d’ensemble des modèles de licence aaaWidevine | Documents Microsoft"
description: "Cette rubrique donne une vue d’ensemble d’un modèle de licence Widevine utilisé tooconfigure Widevine licences."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Vue d’ensemble du modèle de licence Widevine
## <a name="overview"></a>Vue d'ensemble
Azure Media Services vous permet maintenant des licences Widevine tooconfigure et de la demande. Lorsque le lecteur hello utilisateur final tente tooplay votre contenu Widevine protégé, une demande est envoyé toohello licence remise service tooobtain une licence. Si le service de licence hello approuve la demande de hello, il émet la licence hello qui est envoyé toohello client et peut être utilisé toodecrypt- and -play hello contenu spécifié.

La demande de licence Widevine se présente sous forme de message JSON.  

>[!NOTE]
> Vous pouvez choisir toocreate un message vide avec aucune valeurs simplement « {} » et un modèle de licence sera créé avec les valeurs par défaut. valeur par défaut de Hello fonctionne pour la plupart des cas. Par exemple, les scénarios de remise de licence MS nécessitent toujours les valeurs par défaut. Si vous avez besoin tooset hello « provider » et les valeurs de « content_id », un fournisseur doit correspondre à des informations d’identification de Widevine de Google.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>Message JSON
| Nom | Valeur | Description |
| --- | --- | --- |
| payload |Chaîne encodée Base64 |demande de licence Hello envoyée par un client. |
| content_id |Chaîne encodée Base64 |Identificateur utilisé tooderive KeyId(s) et clés de contenu pour chaque content_key_specs.track_type. |
| provider |string |Toolook utilisé des clés de contenu et des stratégies. Si la remise de clé MS est utilisée pour la remise de licence Widevine, ce paramètre est ignoré. |
| policy_name |string |Nom d'une stratégie précédemment enregistrée. Facultatif |
| allowed_track_types |enum |SD_ONLY ou SD_HD. Contrôle les clés de contenu à inclure dans une licence |
| content_key_specs |tableau de structures JSON, consultez **Spécifications de clé de contenu** ci-dessous |Un contrôle plus fin sur le contenu des clés tooreturn. Pour plus d'informations, consultez Spécifications de clé de contenu ci-dessous.  Une seule valeur allowed_track_types et content_key_specs peut être spécifiée. |
| use_policy_overrides_exclusively |booléen. true ou false |Utiliser les attributs de la stratégie spécifiés par policy_overrides et ignorer toutes les stratégies stockées précédemment. |
| policy_overrides |Structure JSON, consultez **Remplacements de stratégies** ci-dessous |Paramètres de stratégie pour cette licence.  En cas de hello cette ressource a une stratégie prédéfinie, ces valeurs spécifiés seront utilisés. |
| session_init |Structure JSON, consultez **Initialisation de la session** ci-dessous |Données facultatives passé toolicense. |
| parse_only |booléen. true ou false |demande de licence Hello est analysée, mais aucune licence n’est émise. Toutefois, la demande de licence de valeurs écran hello sont retournées dans la réponse de hello. |

## <a name="content-key-specs"></a>Spécifications de clé de contenu
Si une stratégie préexistante existe, il n’existe aucun toospecify besoin de hello valeur hello spécification de clé de contenu.  stratégie préexistant de Hello associée à ce contenu sera utilisé toodetermine hello sortie protection telles que HDCP et CGMS.  Si une stratégie déjà existante n’est pas inscrit avec le serveur de licences Widevine de hello, fournisseur de contenu hello peut injecter des valeurs de hello dans la demande de licence hello.   

Chaque content_key_specs doit être spécifié pour toutes les pistes, quel que soit hello option use_policy_overrides_exclusively. 

| Nom | Valeur | Description |
| --- | --- | --- |
| content_key_specs. track_type |string |Un nom de type de piste. Si content_key_specs est spécifié dans la demande de licence hello, assurez-vous que toospecify que tous le suivi types explicitement. Échec toodo entraînerait échec tooplayback dernières 10 secondes. |
| content_key_specs  <br/> security_level |uint32 |Définit la configuration requise de robustesse du client pour la lecture. <br/> 1 - Chiffrement whitebox logiciel requis. <br/> 2 - Chiffrement logiciel et décodeur masqué requis. <br/> 3 - opérations de matériel et de services de chiffrement de clé hello doivent être effectuées dans un environnement d’exécution approuvé sauvegardées matériel. <br/> 4 - hello chiffrement et de décodage du contenu doit être effectuée dans un environnement d’exécution approuvé sauvegardées matériel.  <br/> 5 - hello crypto, décodage et tous les gestion des média hello (compressé et décompressé) doit être gérée dans un environnement d’exécution approuvé sauvegardées matériel. |
| content_key_specs <br/> required_output_protection.hdc |string - une des options : HDCP_NONE, HDCP_V1, HDCP_V2 |Indique si HDCP est requis |
| content_key_specs <br/>key |Chaîne  <br/>encodée Base64 |Toouse de clé de contenu pour cette piste. Si spécifié, hello track_type ou ID est requis.  Cette option permet de fournisseur de contenu hello tooinject clé de contenu hello pour cette piste au lieu de laisser le serveur de licences Widevine générer ou de recherche d’une clé. |
| content_key_specs.key_id |Chaîne binaire encodée Base64, 16 octets |Identificateur unique pour la clé de hello. |

## <a name="policy-overrides"></a>Remplacements de stratégies
| Nom | Valeur | Description |
| --- | --- | --- |
| policy_overrides. can_play |booléen. true ou false |Indique que la lecture de hello du contenu est autorisée. La valeur par défaut est false. |
| policy_overrides. can_persist |booléen. true ou false |Indique cette licence hello peut être un stockage volatile toonon persistant pour une utilisation hors connexion. La valeur par défaut est false. |
| policy_overrides. can_renew |booléen, true ou false |Indique que le renouvellement de cette licence est autorisé. Si la valeur est true, la durée hello de licence de hello peut être étendue par pulsation. La valeur par défaut est false. |
| policy_overrides. license_duration_seconds |int64 |Indique la fenêtre de temps hello pour cette licence spécifique. La valeur 0 indique qu’il n’y a aucune durée de toohello limite. La valeur par défaut est 0. |
| policy_overrides. rental_duration_seconds |int64 |Indique la fenêtre de temps hello lors de la lecture est autorisée. La valeur 0 indique qu’il n’y a aucune durée de toohello limite. La valeur par défaut est 0. |
| policy_overrides. playback_duration_seconds |int64 |Hello d’affichage de la fenêtre de temps après le démarrage de la lecture au sein de la durée de licence hello. La valeur 0 indique qu’il n’y a aucune durée de toohello limite. La valeur par défaut est 0. |
| policy_overrides. renewal_server_url |string |Toutes les demandes de pulsation (renouvellement) de cette licence doivent être dirigées toohello spécifié l’URL. Ce champ est utilisé uniquement si can_renew a la valeur true. |
| policy_overrides. renewal_delay_seconds |int64 |Nombre de secondes après license_start_time avant la première tentative de renouvellement. Ce champ est utilisé uniquement si can_renew a la valeur true. La valeur par défaut est 0 |
| policy_overrides. renewal_retry_interval_seconds |int64 |Spécifie le délai de hello en secondes entre les demandes de renouvellement de licence suivants, en cas d’échec. Ce champ est utilisé uniquement si can_renew a la valeur true. |
| policy_overrides. renewal_recovery_duration_seconds |int64 |fenêtre Hello d’exécution, dans laquelle la lecture autorisée toocontinue lors de renouvellement est tentée, encore échoue en raison de problèmes toobackend avec le serveur de licences hello. La valeur 0 indique qu’il n’y a aucune durée de toohello limite. Ce champ est utilisé uniquement si can_renew a la valeur true. |
| policy_overrides. renew_with_usage |booléen, true ou false |Indique que cette licence hello est envoyée pour le renouvellement au démarrage de l’utilisation. Ce champ est utilisé uniquement si can_renew a la valeur true. |

## <a name="session-initialization"></a>Initialisation de la session
| Nom | Valeur | Description |
| --- | --- | --- |
| provider_session_token |Chaîne encodée Base64 |Ce jeton de session a été retourné dans la licence de hello et se trouvent dans les renouvellements suivants.  jeton de session Hello n’est pas persistante au-delà de sessions. |
| provider_client_token |Chaîne encodée Base64 |Client toosend jeton en réponse de licence hello.  Si la demande de licence hello contient un jeton du client, cette valeur est ignorée. jeton Hello du client est conservées au-delà de sessions de licence. |
| override_provider_client_token |booléen. true ou false |Si la demande de licence false et hello contient un jeton de client, utilisez jeton hello à partir de la demande de hello même si un jeton du client a été spécifié dans cette structure.  Si la valeur est true, utilisez toujours le jeton hello spécifié dans cette structure. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Configuration de vos licences Widevine à l'aide des types .NET
Media Services propose des API .NET qui vous permettent de configurer vos licences Widevine. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Classes définies dans hello Media Services .NET SDK
Hello Voici les définitions de ces types hello.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Exemple
Hello suivant montre l’exemple de comment toouse API .NET tooconfigure une licence Widevine simple.

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine](media-services-protect-with-drm.md)

