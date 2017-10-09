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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="c28ff-104">À l’aide de tooAzure de licences Widevine Axinom toodeliver Media Services</span><span class="sxs-lookup"><span data-stu-id="c28ff-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c28ff-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="c28ff-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="c28ff-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="c28ff-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c28ff-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c28ff-107">Overview</span></span>
<span data-ttu-id="c28ff-108">Azure Media Services (AMS) a ajouté la protection dynamique Google Widevine (voir le [blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) pour plus de détails).</span><span class="sxs-lookup"><span data-stu-id="c28ff-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="c28ff-109">En outre, Azure Media Player (AMP) a ajouté la prise en charge de Widevine (voir [Document AMP](http://amp.azure.net/libs/amp/latest/docs/) pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="c28ff-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="c28ff-110">Il s’agit d’un succès majeur en matière de diffusion en continu de contenu DASH protégé par CENC avec DRM multi-natif (PlayReady et Widevine) sur les navigateurs modernes équipés de MSE et EME.</span><span class="sxs-lookup"><span data-stu-id="c28ff-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="c28ff-111">À compter de hello Media Services .NET SDK version 3.5.2, Media Services permet de vous tooconfigure Widevine modèle de licence et obtenir des licences Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="c28ff-112">Vous pouvez également utiliser hello suivant toohelp de partenaires AMS vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="c28ff-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="c28ff-113">Cet article décrit comment toointegrate et test Widevine de licence serveur géré par Axinom.</span><span class="sxs-lookup"><span data-stu-id="c28ff-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="c28ff-114">Il aborde plus précisément :</span><span class="sxs-lookup"><span data-stu-id="c28ff-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="c28ff-115">la configuration d’un chiffrement commun dynamique avec DRM multiples (PlayReady et Widevine) avec les URL d’acquisition de licences correspondantes ;</span><span class="sxs-lookup"><span data-stu-id="c28ff-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="c28ff-116">Générer un jeton JWT dans l’ordre toomeet hello licence configuration requise du serveur ;</span><span class="sxs-lookup"><span data-stu-id="c28ff-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="c28ff-117">le développement d’une application Azure Media Player gérant l’acquisition de licence avec l’authentification de jetons JWT ;</span><span class="sxs-lookup"><span data-stu-id="c28ff-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="c28ff-118">Hello complète du système et hello du flux de code clé, key, la valeur initiale de clé, jeton JTW et ses revendications peut être décrit au mieux par hello suivant schéma de contenu.</span><span class="sxs-lookup"><span data-stu-id="c28ff-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH et CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="c28ff-120">Protection de contenu</span><span class="sxs-lookup"><span data-stu-id="c28ff-120">Content Protection</span></span>
<span data-ttu-id="c28ff-121">Pour la configuration de protection dynamique et la stratégie de distribution de clés, consultez les blogs de Mingfei : [comment empaquetage de Widevine tooconfigure avec Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="c28ff-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="c28ff-122">Vous pouvez configurer la protection CENC dynamique avec multi-DRM pour tiret de diffusion en continu des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="c28ff-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="c28ff-123">Protection PlayReady pour MS Edge et IE11, qui peut présenter des restrictions en matière d’autorisation de jeton.</span><span class="sxs-lookup"><span data-stu-id="c28ff-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="c28ff-124">stratégie de restriction token Hello doit être accompagnée d’un jeton émis par un Service (jeton de sécurité), tels qu’Azure Active Directory ;</span><span class="sxs-lookup"><span data-stu-id="c28ff-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="c28ff-125">Widevine protection pour Chrome, qui peut exiger l’authentification des jetons avec le jeton émis par un autre STS.</span><span class="sxs-lookup"><span data-stu-id="c28ff-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="c28ff-126">Veuillez consulter la rubrique [Génération de jetons JWT](media-services-axinom-integration.md#jwt-token-generation) pour savoir pourquoi Azure Active Directory ne peut pas servir de STS pour un serveur de licences Widevine d’Axinom.</span><span class="sxs-lookup"><span data-stu-id="c28ff-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="c28ff-127">Considérations</span><span class="sxs-lookup"><span data-stu-id="c28ff-127">Considerations</span></span>
1. <span data-ttu-id="c28ff-128">Vous devez utiliser hello Qu'axinom spécifié la valeur initiale de clé (8888000000000000000000000000000000000000) et votre généré sélectionné clé ID toogenerate hello contenu ou la clé pour la configuration du service de distribution de clés.</span><span class="sxs-lookup"><span data-stu-id="c28ff-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="c28ff-129">Serveur de licences Axinom émettra contenant les clés de contenu en fonction de toutes les licences sur hello même valeur initiale, qui est valide pour le test et de production de clé.</span><span class="sxs-lookup"><span data-stu-id="c28ff-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="c28ff-130">URL d’acquisition de licences Widevine Hello pour le test : [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="c28ff-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="c28ff-131">HTTP et HTTS sont tous les deux autorisés.</span><span class="sxs-lookup"><span data-stu-id="c28ff-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="c28ff-132">Préparation d’Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="c28ff-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="c28ff-133">AMP 1.4.0 prend en charge la lecture de contenu AMS qui est empaqueté dynamiquement avec les DRM de PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="c28ff-134">Si le serveur de licences Widevine ne requiert pas l’authentification des jetons, aucune est supplémentaires, que vous devez toodo tootest un tiret de contenu protégé par Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="c28ff-135">Pour obtenir un exemple, équipe de hello AMP fournit un simple [exemple](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), où vous pouvez voir qu’il fonctionne dans Edge et IE11 avec PlayReady et Chrome avec Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="c28ff-136">serveur de licences Widevine Hello fournie par Axinom requiert l’authentification des jetons Web JSON.</span><span class="sxs-lookup"><span data-stu-id="c28ff-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="c28ff-137">un jeton JWT Hello doit toobe envoyé avec la demande de licence via un en-tête HTTP « X-AxDRM-Message ».</span><span class="sxs-lookup"><span data-stu-id="c28ff-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="c28ff-138">Pour cela, vous devez hello tooadd suivant javascript dans la page web de hello AMP d’hébergement avant de définir l’option source hello :</span><span class="sxs-lookup"><span data-stu-id="c28ff-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="c28ff-139">reste de Hello du code de l’AMP est API AMP standard comme dans les documents AMP [ici](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="c28ff-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="c28ff-140">Notez que hello ci-dessus javascript pour le paramètre d’en-tête d’autorisation personnalisée est toujours une approche à court terme avant officielle hello approche à long terme de gestion du matériel est libérée.</span><span class="sxs-lookup"><span data-stu-id="c28ff-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="c28ff-141">Génération de jetons JWT</span><span class="sxs-lookup"><span data-stu-id="c28ff-141">JWT Token Generation</span></span>
<span data-ttu-id="c28ff-142">Le serveur de licences Axinom Widevine fourni par Axinom requiert l’authentification de jeton JWT.</span><span class="sxs-lookup"><span data-stu-id="c28ff-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="c28ff-143">En outre, une des revendications hello dans un jeton JWT hello est d’un type complexe au lieu du type de données primitif.</span><span class="sxs-lookup"><span data-stu-id="c28ff-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="c28ff-144">Malheureusement, Azure AD ne peut émettre que des jetons JWT avec des types primitifs.</span><span class="sxs-lookup"><span data-stu-id="c28ff-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="c28ff-145">De même, les API .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler et JwtPayload) vous permet uniquement type d’objet complexe tooinput en tant que revendications.</span><span class="sxs-lookup"><span data-stu-id="c28ff-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="c28ff-146">Toutefois, hello revendications sont encore sérialisées en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="c28ff-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="c28ff-147">Par conséquent, nous ne pouvons pas utiliser hello deux pour le jeton JWT hello génération de demande de licences Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="c28ff-148">De John Sheehan [package Nuget de JWT](https://www.nuget.org/packages/JWT) répond aux hello besoins, nous allons toouse ce package Nuget.</span><span class="sxs-lookup"><span data-stu-id="c28ff-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="c28ff-149">Ci-dessous figurent des code hello pour le jeton JWT génération hello requis revendications comme requis par le serveur de licences Axinom Widevine pour les tests :</span><span class="sxs-lookup"><span data-stu-id="c28ff-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

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

<span data-ttu-id="c28ff-150">Serveur de licences Axinom Widevine</span><span class="sxs-lookup"><span data-stu-id="c28ff-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="c28ff-151">Considérations</span><span class="sxs-lookup"><span data-stu-id="c28ff-151">Considerations</span></span>
1. <span data-ttu-id="c28ff-152">Bien que le service de remise de licence PlayReady AMS exige que la chaîne de caractères « Bearer= » précède un jeton d’authentification, le serveur de licences Axinom Widevine ne l’utilise pas.</span><span class="sxs-lookup"><span data-stu-id="c28ff-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="c28ff-153">clé de communication Axinom Hello est utilisé comme clé de signature.</span><span class="sxs-lookup"><span data-stu-id="c28ff-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="c28ff-154">Notez que cette clé hello est une chaîne hexadécimale, mais elle doit être traitée comme une série d’octets non une chaîne lors de l’encodage.</span><span class="sxs-lookup"><span data-stu-id="c28ff-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="c28ff-155">Cela est possible par la méthode de hello ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="c28ff-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="c28ff-156">Récupération de l’ID de clé</span><span class="sxs-lookup"><span data-stu-id="c28ff-156">Retrieving Key ID</span></span>
<span data-ttu-id="c28ff-157">Vous avez peut-être remarqué que, dans le code hello pour générer un jeton Web JSON, ID de jeton, key est requis.</span><span class="sxs-lookup"><span data-stu-id="c28ff-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="c28ff-158">Dans la mesure où un jeton JWT hello doit toobe prêt avant de charger le lecteur AMP, clés besoins ID toobe récupérée dans commande toogenerate un jeton JWT.</span><span class="sxs-lookup"><span data-stu-id="c28ff-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="c28ff-159">Évidemment, il existe plusieurs manières tooget contenir de clé de code.</span><span class="sxs-lookup"><span data-stu-id="c28ff-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="c28ff-160">Par exemple, il est possible de stocker un ID de clé avec les métadonnées de contenu dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="c28ff-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="c28ff-161">Il est également possible d’extraire un ID de clé d’un fichier DASH MPD (Media Presentation Description).</span><span class="sxs-lookup"><span data-stu-id="c28ff-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="c28ff-162">code Hello ci-dessous est pourquoi ce dernier.</span><span class="sxs-lookup"><span data-stu-id="c28ff-162">hello code below is for hello latter.</span></span>

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

## <a name="summary"></a><span data-ttu-id="c28ff-163">Résumé</span><span class="sxs-lookup"><span data-stu-id="c28ff-163">Summary</span></span>
<span data-ttu-id="c28ff-164">Avec l’ajout le plus récent de prise en charge de Widevine dans la Protection de contenu Azure Media Services et Azure Media Player, nous ne pouvons tooimplement diffusion en continu de tiret + multiples native-DRM (PlayReady + Widevine) avec les deux service de licence PlayReady avec licence AMS et Widevine serveur à partir de Axinom pour hello suivant les navigateurs modernes :</span><span class="sxs-lookup"><span data-stu-id="c28ff-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="c28ff-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="c28ff-165">Chrome</span></span>
* <span data-ttu-id="c28ff-166">Microsoft Edge sous Windows 10</span><span class="sxs-lookup"><span data-stu-id="c28ff-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="c28ff-167">IE 11 sous Windows 8.1et Windows 10</span><span class="sxs-lookup"><span data-stu-id="c28ff-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="c28ff-168">(Desktop) de Firefox et Safari sur Mac (pas d’iOS) sont également pris en charge par Silverlight et hello même URL avec Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="c28ff-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="c28ff-169">Hello paramètres suivants sont requis dans le serveur de licences hello mini-solution en tirant parti Axinom Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="c28ff-170">À l’exception de clé ID, reste hello des paramètres fournis par Axinom en fonction de leur configuration de serveur Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="c28ff-171">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c28ff-171">Parameter</span></span> | <span data-ttu-id="c28ff-172">Utilisation</span><span class="sxs-lookup"><span data-stu-id="c28ff-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="c28ff-173">ID de clé de communication</span><span class="sxs-lookup"><span data-stu-id="c28ff-173">Communication key ID</span></span> |<span data-ttu-id="c28ff-174">Doit être inclus en tant que valeur de revendication hello « com_key_id » dans le jeton Web JSON (voir [cela](media-services-axinom-integration.md#jwt-token-generation) section).</span><span class="sxs-lookup"><span data-stu-id="c28ff-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c28ff-175">Clé de communication</span><span class="sxs-lookup"><span data-stu-id="c28ff-175">Communication key</span></span> |<span data-ttu-id="c28ff-176">Doit être utilisé comme clé de signature du jeton Web JSON de hello (consultez [cela](media-services-axinom-integration.md#jwt-token-generation) section).</span><span class="sxs-lookup"><span data-stu-id="c28ff-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="c28ff-177">Amorce de clé</span><span class="sxs-lookup"><span data-stu-id="c28ff-177">Key seed</span></span> |<span data-ttu-id="c28ff-178">Doit être clé de contenu toogenerate utilisé avec n’importe quelle donnée contenu ID de clé (voir [cela](media-services-axinom-integration.md#content-protection) section).</span><span class="sxs-lookup"><span data-stu-id="c28ff-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="c28ff-179">URL d’acquisition de licence Widevine.</span><span class="sxs-lookup"><span data-stu-id="c28ff-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="c28ff-180">Doit être utilisé dans la configuration de la stratégie de remise de l’élément multimédia pour la diffusion en streaming DASH (consultez [cette](media-services-axinom-integration.md#content-protection) section).</span><span class="sxs-lookup"><span data-stu-id="c28ff-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="c28ff-181">ID de clé de contenu</span><span class="sxs-lookup"><span data-stu-id="c28ff-181">Content Key ID</span></span> |<span data-ttu-id="c28ff-182">Doit être inclus dans le cadre de valeur hello de revendication de Message du droit de jeton Web JSON (voir [cela](media-services-axinom-integration.md#jwt-token-generation) section).</span><span class="sxs-lookup"><span data-stu-id="c28ff-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="c28ff-183">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="c28ff-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c28ff-184">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="c28ff-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="c28ff-185">Remerciements</span><span class="sxs-lookup"><span data-stu-id="c28ff-185">Acknowledgments</span></span>
<span data-ttu-id="c28ff-186">Nous aimerions hello tooacknowledge suivant des personnes qui ont contribué à la création de ce document : Kristjan Jõgi de Axinom et Mingfei Yan Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="c28ff-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

