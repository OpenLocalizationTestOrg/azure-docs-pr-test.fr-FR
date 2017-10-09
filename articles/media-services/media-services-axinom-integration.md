---
title: aaaUsing Axinom toodeliver Widevine licences tooAzure Media Services | Documents Microsoft
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) toodeliver un flux qui est chiffré dynamiquement par AMS avec PlayReady et Widevine DRMs. la licence PlayReady Hello est fourni à partir du serveur de licences PlayReady de Media Services et les licences Widevine sont remis par le serveur de licences Axinom."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>À l’aide de tooAzure de licences Widevine Axinom toodeliver Media Services
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Azure Media Services (AMS) a ajouté la protection dynamique Google Widevine (voir le [blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) pour plus de détails). En outre, Azure Media Player (AMP) a ajouté la prise en charge de Widevine (voir [Document AMP](http://amp.azure.net/libs/amp/latest/docs/) pour plus d’informations). Il s’agit d’un succès majeur en matière de diffusion en continu de contenu DASH protégé par CENC avec DRM multi-natif (PlayReady et Widevine) sur les navigateurs modernes équipés de MSE et EME.

À compter de hello Media Services .NET SDK version 3.5.2, Media Services permet de vous tooconfigure Widevine modèle de licence et obtenir des licences Widevine. Vous pouvez également utiliser hello suivant toohelp de partenaires AMS vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Cet article décrit comment toointegrate et test Widevine de licence serveur géré par Axinom. Il aborde plus précisément :  

* la configuration d’un chiffrement commun dynamique avec DRM multiples (PlayReady et Widevine) avec les URL d’acquisition de licences correspondantes ;
* Générer un jeton JWT dans l’ordre toomeet hello licence configuration requise du serveur ;
* le développement d’une application Azure Media Player gérant l’acquisition de licence avec l’authentification de jetons JWT ;

Hello complète du système et hello du flux de code clé, key, la valeur initiale de clé, jeton JTW et ses revendications peut être décrit au mieux par hello suivant schéma de contenu.

![DASH et CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Protection de contenu
Pour la configuration de protection dynamique et la stratégie de distribution de clés, consultez les blogs de Mingfei : [comment empaquetage de Widevine tooconfigure avec Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

Vous pouvez configurer la protection CENC dynamique avec multi-DRM pour tiret de diffusion en continu des éléments suivants de hello :

1. Protection PlayReady pour MS Edge et IE11, qui peut présenter des restrictions en matière d’autorisation de jeton. stratégie de restriction token Hello doit être accompagnée d’un jeton émis par un Service (jeton de sécurité), tels qu’Azure Active Directory ;
2. Widevine protection pour Chrome, qui peut exiger l’authentification des jetons avec le jeton émis par un autre STS. 

Veuillez consulter la rubrique [Génération de jetons JWT](media-services-axinom-integration.md#jwt-token-generation) pour savoir pourquoi Azure Active Directory ne peut pas servir de STS pour un serveur de licences Widevine d’Axinom.

### <a name="considerations"></a>Considérations
1. Vous devez utiliser hello Qu'axinom spécifié la valeur initiale de clé (8888000000000000000000000000000000000000) et votre généré sélectionné clé ID toogenerate hello contenu ou la clé pour la configuration du service de distribution de clés. Serveur de licences Axinom émettra contenant les clés de contenu en fonction de toutes les licences sur hello même valeur initiale, qui est valide pour le test et de production de clé.
2. URL d’acquisition de licences Widevine Hello pour le test : [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). HTTP et HTTS sont tous les deux autorisés.

## <a name="azure-media-player-preparation"></a>Préparation d’Azure Media Player
AMP 1.4.0 prend en charge la lecture de contenu AMS qui est empaqueté dynamiquement avec les DRM de PlayReady et Widevine.
Si le serveur de licences Widevine ne requiert pas l’authentification des jetons, aucune est supplémentaires, que vous devez toodo tootest un tiret de contenu protégé par Widevine. Pour obtenir un exemple, équipe de hello AMP fournit un simple [exemple](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), où vous pouvez voir qu’il fonctionne dans Edge et IE11 avec PlayReady et Chrome avec Widevine.
serveur de licences Widevine Hello fournie par Axinom requiert l’authentification des jetons Web JSON. un jeton JWT Hello doit toobe envoyé avec la demande de licence via un en-tête HTTP « X-AxDRM-Message ». Pour cela, vous devez hello tooadd suivant javascript dans la page web de hello AMP d’hébergement avant de définir l’option source hello :

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

reste de Hello du code de l’AMP est API AMP standard comme dans les documents AMP [ici](http://amp.azure.net/libs/amp/latest/docs/).

Notez que hello ci-dessus javascript pour le paramètre d’en-tête d’autorisation personnalisée est toujours une approche à court terme avant officielle hello approche à long terme de gestion du matériel est libérée.

## <a name="jwt-token-generation"></a>Génération de jetons JWT
Le serveur de licences Axinom Widevine fourni par Axinom requiert l’authentification de jeton JWT. En outre, une des revendications hello dans un jeton JWT hello est d’un type complexe au lieu du type de données primitif.

Malheureusement, Azure AD ne peut émettre que des jetons JWT avec des types primitifs. De même, les API .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler et JwtPayload) vous permet uniquement type d’objet complexe tooinput en tant que revendications. Toutefois, hello revendications sont encore sérialisées en tant que chaîne. Par conséquent, nous ne pouvons pas utiliser hello deux pour le jeton JWT hello génération de demande de licences Widevine.

De John Sheehan [package Nuget de JWT](https://www.nuget.org/packages/JWT) répond aux hello besoins, nous allons toouse ce package Nuget.

Ci-dessous figurent des code hello pour le jeton JWT génération hello requis revendications comme requis par le serveur de licences Axinom Widevine pour les tests :

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

Serveur de licences Axinom Widevine

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Considérations
1. Bien que le service de remise de licence PlayReady AMS exige que la chaîne de caractères « Bearer= » précède un jeton d’authentification, le serveur de licences Axinom Widevine ne l’utilise pas.
2. clé de communication Axinom Hello est utilisé comme clé de signature. Notez que cette clé hello est une chaîne hexadécimale, mais elle doit être traitée comme une série d’octets non une chaîne lors de l’encodage. Cela est possible par la méthode de hello ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Récupération de l’ID de clé
Vous avez peut-être remarqué que, dans le code hello pour générer un jeton Web JSON, ID de jeton, key est requis. Dans la mesure où un jeton JWT hello doit toobe prêt avant de charger le lecteur AMP, clés besoins ID toobe récupérée dans commande toogenerate un jeton JWT.

Évidemment, il existe plusieurs manières tooget contenir de clé de code. Par exemple, il est possible de stocker un ID de clé avec les métadonnées de contenu dans une base de données. Il est également possible d’extraire un ID de clé d’un fichier DASH MPD (Media Presentation Description). code Hello ci-dessous est pourquoi ce dernier.

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a>Résumé
Avec l’ajout le plus récent de prise en charge de Widevine dans la Protection de contenu Azure Media Services et Azure Media Player, nous ne pouvons tooimplement diffusion en continu de tiret + multiples native-DRM (PlayReady + Widevine) avec les deux service de licence PlayReady avec licence AMS et Widevine serveur à partir de Axinom pour hello suivant les navigateurs modernes :

* Chrome
* Microsoft Edge sous Windows 10
* IE 11 sous Windows 8.1et Windows 10
* (Desktop) de Firefox et Safari sur Mac (pas d’iOS) sont également pris en charge par Silverlight et hello même URL avec Azure Media Player

Hello paramètres suivants sont requis dans le serveur de licences hello mini-solution en tirant parti Axinom Widevine. À l’exception de clé ID, reste hello des paramètres fournis par Axinom en fonction de leur configuration de serveur Widevine.

| Paramètre | Utilisation |
| --- | --- |
| ID de clé de communication |Doit être inclus en tant que valeur de revendication hello « com_key_id » dans le jeton Web JSON (voir [cela](media-services-axinom-integration.md#jwt-token-generation) section). |
| Clé de communication |Doit être utilisé comme clé de signature du jeton Web JSON de hello (consultez [cela](media-services-axinom-integration.md#jwt-token-generation) section). |
| Amorce de clé |Doit être clé de contenu toogenerate utilisé avec n’importe quelle donnée contenu ID de clé (voir [cela](media-services-axinom-integration.md#content-protection) section). |
| URL d’acquisition de licence Widevine. |Doit être utilisé dans la configuration de la stratégie de remise de l’élément multimédia pour la diffusion en streaming DASH (consultez [cette](media-services-axinom-integration.md#content-protection) section). |
| ID de clé de contenu |Doit être inclus dans le cadre de valeur hello de revendication de Message du droit de jeton Web JSON (voir [cela](media-services-axinom-integration.md#jwt-token-generation) section). |

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Remerciements
Nous aimerions hello tooacknowledge suivant des personnes qui ont contribué à la création de ce document : Kristjan Jõgi de Axinom et Mingfei Yan Amit Rajput.

