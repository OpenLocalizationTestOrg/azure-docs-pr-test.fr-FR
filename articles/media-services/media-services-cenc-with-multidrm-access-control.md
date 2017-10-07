---
title: "CENC avec Multi-DRM et contrôle d’accès : une conception de référence et l’application sur Windows Azure et Azure Media Services | Microsoft Docs"
description: "Découvrez comment toolicensing hello Microsoft® Kit Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>CENC avec Multi-DRM et contrôle d’accès : une conception de référence et l’application sur Windows Azure et Azure Media Services
 
## <a name="introduction"></a>Introduction
Il est connu qu’il est une tâche complexe de toodesign et générer un sous-système de gestion des droits numériques pour une OTT ou en ligne de diffusion en continu de la solution. Et c’est une pratique courante pour les opérateurs/en ligne des fournisseurs vidéo toooutsource cette fournisseurs de services de gestion des droits numériques toospecialized partie. Hello ce document vise toopresent une conception de référence et l’implémentation du sous-système DRM de bout en bout dans OTT ou une solution de diffusion en continu en ligne.

lecteurs Hello ciblé de ce document sont ingénieurs travaillant dans le sous-système de gestion des droits numériques de OTT solutions en ligne de diffusion en continu/multi-cluster-screen ou tous les lecteurs intéressés par le sous-système de gestion des droits numériques. hypothèse de Hello est que les lecteurs sont familiarisés avec au moins une des technologies de gestion des droits numériques hello sur le marché hello, telles que PlayReady, Widevine, FairPlay ou Adobe accès.

Par DRM, nous entendons également CENC (chiffrement commun) avec multi-DRM. Une tendance majeure dans la diffusion en continu en ligne et de l’industrie OTT est toouse CENC avec multi-native-DRM sur différentes plateformes de client, qui est un décalage à partir de la tendance précédente de hello d’à l’aide d’un seul DRM et son client SDK pour différentes plateformes clientes. Lorsque vous utilisez CENC avec plusieurs native-DRM, PlayReady et Widevine sont chiffrées par hello [chiffrement commun (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) spécification.

avantages de Hello de CENC avec multi-DRM sont les suivantes :

1. réduction des frais de chiffrement dans la mesure où un seul traitement de chiffrement est utilisé, ciblant différentes plateformes avec ses DRM natifs ;
2. Réduit le coût de hello de la gestion des éléments multimédias chiffrés, car une seule copie d’éléments multimédias chiffrés est nécessaire ;
3. Élimine le coût de licence depuis hello native DRM client est généralement disponible sur la plateforme native du client DRM.

Microsoft a joué le rôle de promoteur actif de DASH et de CENC, tout comme d’autres acteurs majeurs du secteur. Microsoft Azure Media Services offre la prise en charge de DASH et CENC. Pour les dernières annonces, consultez les blogs de Mingfei : [Annonce d’une distribution de licence Google Widevine dans Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/) et [Azure Media Services ajoute un package Gooble Windevine pour la distribution de flux multi-DRM](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).  

### <a name="overview-of-this-article"></a>Présentation de cet article
objectif Hello de cet article inclut hello qui suit :

1. fourniture d’une conception de référence du sous-système de gestion des droits numériques avec CENC multi-DRM ;
2. fourniture d’une implémentation de référence sur la plateforme Microsoft Azure/Azure Media Services ;
3. Commentaires de certaines rubriques relatives à la conception et l’implémentation.

Dans l’article hello, « multi-DRM » couvre suivant de hello :

1. Microsoft PlayReady
2. Google Widevine
3. Apple FairPlay 

Hello tableau suivant récapitule application de plateforme native/native hello et les navigateurs pris en charge par chaque DRM.

| **Plateforme cliente** | **Prise en charge native de DRM** | **Navigateur/App** | **Formats de diffusion en continu** |
| --- | --- | --- | --- |
| **Téléviseurs intelligents, récepteurs d’opérateur, récepteurs OTT** |PlayReady principalement, et/ou Widevine, et/ou autres |Linux, Opera, WebKit, autre |Divers formats |
| **Appareils Windows 10 (PC Windows, tablettes Windows, Windows Phone, Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |DASH (pour HLS, PlayReady n’est pas pris en charge)<br/><br/>DASH, Smooth Streaming (pour HLS, PlayReady n’est pas pris en charge) |
| **Appareils Android (téléphone, tablette, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), clients OS X et Apple TV** |FairPlay |Safari 8+/EME |HLS |


Compte tenu de l’état actuel de hello de déploiement pour chaque DRM, un service souhaiterez généralement que vous devez tous les types hello de points de terminaison Bonjour meilleures tooimplement 2 ou 3-DRMs-toomake moyen.

Il existe un compromis entre la complexité hello de logique de service hello et complexité hello sur hello client côté tooreach un certain niveau de l’utilisateur d’expérience sur hello différents clients.

toomake votre sélection, gardez à l’esprit ces faits :

* PlayReady est implémenté en mode natif dans tous les appareils Windows, sur certains appareils Android, et est disponible via les kits de développement logiciel (SDK) sur pratiquement n'importe quelle plate-forme
* Widevine est implémenté en mode natif dans chaque appareil Android, dans Chrome, et dans certains autres appareils
* FairPlay est disponible uniquement sur iOS et les clients Mac OS ou via iTunes.

Par conséquent, une configuration multi-DRM standard serait :

* Option 1 : PlayReady et Widevine
* Option 2 : PlayReady, Widevine et FairPlay

## <a name="a-reference-design"></a>Une conception de référence
Dans cette section, nous allons examiner une conception de référence est agnostique tootechnologies utilisé tooimplement il.

Un sous-système DRM peut contenir hello suivant des composants :

1. Gestion des clés
2. Packaging DRM
3. Remise de licence DRM
4. Vérification des droits
5. Authentification/autorisation
6. Lecteur
7. Origine/CDN

Hello diagramme suivant illustre hello élevée au niveau d’interaction entre composants hello dans un sous-système de gestion des droits numériques.

![Sous-système de gestion des droits numériques avec CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Il existe trois base « couches » dans la conception de hello :

1. Couche back-office (en noir) qui n’est pas présentée à l’extérieur ;
2. Couche de « Réseau de périmètre » (bleu) contenant tous les points de terminaison hello exposés au public ;
3. Couche Internet Public (en bleu clair) contenant les réseaux de diffusion en continu et des lecteurs avec le trafic transitant par l’Internet public.

Il doit exister un outil de gestion de contenu pour le contrôle de la protection DRM, que le chiffrement soit statique ou dynamique. entrées Hello pour le chiffrement de la gestion des droits numériques doivent inclure :

1. le contenu vidéo MBR ;
2. la clé de contenu ;
3. URL d’acquisition de licence.

Durant la lecture, les flux de niveau élevé de hello est :

1. l’utilisateur est authentifié ;
2. Jeton d’autorisation est créé pour l’utilisateur de hello ;
3. Le contenu protégé par DRM (manifeste) est téléchargé tooplayer ;
4. Lecteur soumet des serveurs de licences d’acquisition demande toolicense avec l’ID de clé et l’autorisation jeton.

Avant de déplacer rubrique suivante toohello, quelques mots sur hello concevoir de gestion de clés.

| **ContentKey vers ressources** | **Scénario** |
| --- | --- |
| 1 à 1 |cas le plus simple Hello. Il fournit le plus grand contrôle de hello. Mais cette approche résulte en un coût plus élevé de remise la licence hello. Chaque ressource protégée nécessite au moins une licence. |
| 1 à plusieurs |Vous pouvez utiliser hello même contenu de clé pour plusieurs éléments multimédias. Par exemple, pour tous les actifs hello dans un groupe logique telle qu’un genre ou un sous-ensemble de genre (ou séquence génétique), vous pouvez utiliser une seule clé de contenu. |
| Plusieurs à 1 |Plusieurs clés de contenu sont nécessaires pour chaque élément multimédia. <br/><br/>Par exemple, si vous avez besoin de protection de CENC dynamique tooapply avec multi-DRM pour MPEG-DASH et le chiffrement AES-128 dynamique pour TLS, vous devez les deux clés de contenu distinctes, chacune avec son propre ContentKeyType. (Pour la clé de contenu de hello utilisée pour la protection de CENC dynamique, ContentKeyType.CommonEncryption doit être utilisé, alors que pour hello contenu clé utilisée pour le chiffrement dynamique AES-128, ContentKeyType.EnvelopeEncryption doit être utilisé.)<br/><br/>Un autre exemple, dans la protection de CENC de tiret de contenu, en théorie, une clé de contenu peut être utilisé tooprotect des flux vidéo et un autre flux audio contenu tooprotect clé. |
| Plusieurs – trop-plusieurs |Combinaison de hello au-dessus des deux scénarios : un seul jeu de contenu clés sont utilisées pour chacune des hello plusieurs éléments multimédias dans hello même actif « groupe ». |

Un autre facteur important tooconsider est hello de licences persistantes et non persistantes.

Pourquoi ces considérations sont-elles importantes ?

Ils ont la remise de toolicense impact direct si vous utilisez un cloud public pour la remise de la licence de coût. Prenons l’exemple hello suivant deux tooillustrate de cas de conception :

1. Abonnement mensuel : utilisation d’une licence persistante et d’un mappage clé à ressource 1 à plusieurs. Par exemple, pour toutes les vidéos d’enfants hello, nous utilisons une clé unique de contenu pour le chiffrement. Dans ce cas :

    Nombre total de licences requis pour tous les films/appareils = 1
2. Abonnement mensuel : utilisation d’une licence non persistante et du mappage 1 à 1 entre la clé de contenu et la ressource de contenu. Dans ce cas :

    Nombre total de licences requis pour tous les films/appareils = [nombre de films # regardés] x [# de séances]

Comme vous pouvez le voir, hello deux conceptions différentes entraîner licence très différente demander à modèles par conséquent, la remise de licence coût si le service de remise de licence est fourni par un cloud public comme Azure Media Services.

## <a name="mapping-design-tootechnology-for-implementation"></a>Tootechnology de conception de mappage pour l’implémentation
Ensuite, nous mapper notre tootechnologies conception générique sur la plateforme de Microsoft Azure/Azure Media Services, en spécifiant le toouse technologie pour chaque bloc de construction.

Hello tableau suivant montre le hello mappage :

| **Bloc de construction** | **Technology** |
| --- | --- |
| **Lecteur** |[Azure Media Player](https://azure.microsoft.com/services/media-services/media-player/) |
| **Fournisseur d’identité (IDP)** |Azure Active Directory |
| **Secure Token Service (Service d’émission de jeton de sécurité - STS)** |Azure Active Directory |
| **Flux de travail de Protection DRM** |Protection dynamique Azure Media Services |
| **Distribution de licence DRM** |1. Distribution de licence Azure Media Services (PlayReady, Widevine, FairPlay) ou <br/>2. Serveur de licences de Axinom, <br/>3. Serveur de licences PlayReady personnalisé |
| **Origine** |Point de terminaison des Services de diffusion multimédia en continu Azure |
| **Gestion des clés** |Inutile pour l’implémentation de référence |
| **Gestion de contenu** |Une application de console C# |

En d’autres termes, le fournisseur d’identité (IDP) et du STS (Service d’émission de jeton de sécurité - Secure Token Services) sera AD Azure. Nous utiliserons l’ [API de lecteur Azure Media](http://amp.azure.net/libs/amp/latest/docs/)comme lecteur. Azure Media Services et le lecteur Azure Media prend en charge DASH et CENC avec multi-DRM.

Hello ci-dessous diagramme illustre hello structure globale et du flux avec hello au-dessus de mappage de la technologie.

![CENC sur AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

Dans tooset d’ordre de chiffrement CENC dynamique, outil de gestion de contenu hello utilisera hello suivant entrées :

1. contenu ouvert ;
2. clé de contenu issue de la génération/la gestion de clé ;
3. URL d’acquisition de licence ;
4. liste d’informations fournie par Azure AD.

sortie Hello de l’outil de gestion de contenu hello sera :

1. ContentKeyAuthorizationPolicy contenant la spécification hello sur la remise de licences vérifie un jeton Web JSON et les spécifications de licences DRM ;
2. AssetDeliveryPolicy contient des spécifications au format streaming, la protection DRM et les URL d’acquisition de licence.

Pendant l’exécution, les flux hello sont comme ci-dessous :

1. au moment de l’authentification de l’utilisateur, un jeton JWT est généré ;
2. Une des revendications hello contenues dans un jeton JWT hello est revendication « groupes » contenant les ID d’objet groupe hello de « EntitledUserGroup ». Cette revendication sera utilisée pour le réussir la « vérification des droits ».
3. Manifeste du client télécharge le lecteur d’un CENC le contenu protégé et « voit » suivante de hello :

   1. ID de clé,
   2. contenu de Hello est CENC protégé,
   3. URL d’acquisition de licence.
4. Le lecteur effectue une demande d’acquisition de licence basée sur hello navigateur/DRM pris en charge. Dans la demande d’acquisition de licence hello, ID de clé et hello JWT jeton sera également envoyé. Service de remise de licences vérifie un jeton JWT hello et revendications hello contenues avant l’émission hello nécessaire de licence.

## <a name="implementation"></a>Implémentation
### <a name="implementation-procedures"></a>Procédures de mise en œuvre
implémentation de Hello inclura hello comme suit :

1. Préparer les éléments multimédias de test : encoder/package un test toomulti-vitesse de transmission vidéo fragmenté MP4 dans Azure Media Services. Cet actif n’est pas protégé par DRM. La protection DRM sera assurée par le biais d’une protection dynamique ultérieurement.
2. Créez l’ID de clé et une clé de contenu (éventuellement à partir d’une amorce de clé). Dans le cas présent, le système de gestion de clés n’est pas nécessaire dans la mesure où nous avons affaire à un seul ensemble d’ID de clés et de clé contenu pour plusieurs ressources de test ;
3. Utiliser les services de livraison AMS API tooconfigure multi-DRM licence pour un composant de test hello. Si vous utilisez des serveurs de licences personnalisés par votre entreprise ou des fournisseurs de votre société au lieu des services de licence dans Azure Media Services, vous pouvez ignorer cette étape et spécifier l’URL d’acquisition de licence à l’étape hello pour la configuration de la remise de la licence. Les API AMS est nécessaire toospecify détaillée de certaines configurations, notamment la restriction de la stratégie d’autorisation, les modèles de réponse pour les différents services de licences DRM, etc. de licence. À ce stade, hello portail Azure n’a pas encore fournir hello nécessaires de l’interface utilisateur pour cette configuration. Vous pouvez trouver des informations de niveau API et un exemple de code dans le document de Julia Kornich intitulé : [Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine](media-services-protect-with-drm.md).
4. Utilisez stratégie de livraison AMS API tooconfigure actif pour un composant de test hello. Vous pouvez trouver des informations de niveau API et un exemple de code dans le document de Julia Kornich intitulé : [Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine](media-services-protect-with-drm.md).
5. créer et modifier un client Azure Active Directory dans Azure ;
6. Créer plusieurs comptes d’utilisateurs et groupes dans votre locataire Azure Active Directory : vous devez créer au moins « EntitledUser » et d’ajouter un groupe d’utilisateurs toothis. Les utilisateurs de ce groupe passera la vérification des droits d’acquisition de licence, les utilisateurs pas dans ce groupe de contrôle d’authentification toopass échoue et qu’il ne sera pas en mesure de tooacquire une licence. Un membre de ce groupe « EntitledUser » est une revendication « groupes » requis dans un jeton JWT hello émis par Azure AD. Cette exigence de revendication doit être spécifiée pendant l’opération de configuration de services de distribution de licence multi-DRM.
7. Créez une application ASP.NET MVC qui hébergera votre lecteur vidéo. Cette application ASP.NET est protégée avec l’authentification des utilisateurs sur des locataires Azure Active Directory hello. Revendications appropriées seront incluses dans les jetons d’accès hello obtenus après l’authentification des utilisateurs. L’API OpenID Connect est recommandée pour cette étape. Vous devez hello tooinstall suivant les packages NuGet :
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. Créer un lecteur à l’aide d’ [API Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/). [ProtectionInfo API de Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/) vous permet de toospecify le toouse de technologie DRM sur une autre plateforme de gestion des droits numériques.
9. Matrice de test :

| **DRM** | **Browser** | **Résultat pour les utilisateurs autorisés** | **Résultat pour les utilisateurs non autorisés** |
| --- | --- | --- | --- |
| **PlayReady** |MS Edge ou IE11 sous Windows 10 |Réussite |Échec |
| **Widevine** |Chrome sous Windows 10 |Réussite |Échec |
| **FairPlay** |TBD | | |

George Trifonov, de l’équipe Azure Media Services, a écrit un blog fournissant la procédure détaillée de la configuration d’Azure Active Directory pour une application de lecteur MVC ASP.NET : [intégrer l’application Azure Media Services OWIN basée sur MVC avec Azure Active Directory et restreindre la distribution de clé de contenu en se fondant sur les revendications JWT](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George a également écrit un blog concernant la page [Authentification des jetons JWT dans Azure Media Services et chiffrement dynamique](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). Et voici son [exemple sur l’intégration d’Azure AD avec remise de clé Azure Media Services](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Pour plus d’informations, sur Azure Active Directory :

* Vous pouvez trouver des informations pour les développeurs dans [Guide du développeur Azure Active Directory](../active-directory/active-directory-developers-guide.md).
* Vous pouvez trouver des informations sur l’administrateur dans [Administrer votre annuaire Azure AD](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Des problèmes de mise en œuvre
Il existe des problèmes » » dans l’implémentation de hello. Nous espérons que hello suivant de la liste des « pièges » peut vous aider à résolution des problèmes si vous rencontrez des problèmes.

1. **Issuer** : l’URL doit se terminer par **« / »**.  

    **Audience** doit être hello lecteur identifiant client d’application et vous devez également ajouter **« / »** à fin hello d’URL de l’émetteur hello.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    Dans [JWT décodeur](http://jwt.calebb.net/), vous devez voir **aud** et **iss** comme ci-dessous dans un jeton JWT hello :

    ![1er piège](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Ajouter des autorisations toohello application AAD (sur l’onglet configurer de l’application hello). Cette opération est obligatoire pour chaque application (versions locales et déployées).

    ![2e piège](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Utiliser l’émetteur de droite hello dans la configuration de la protection de CENC dynamique :

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    qui suit Hello ne fonctionne pas :

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Hello GUID est l’ID de client hello AAD Hello GUID sont accessibles dans le menu contextuel de points de terminaison dans le portail Azure.
4. Octroi des autorisations de revendications de membre de groupe. Vérifiez que dans le fichier manifeste d’application AAD, nous avons suivant de hello

    « groupMembershipClaims » : « Tous », (valeur par défaut de hello est null)
5. Définition d’un TokenType approprié lors de la création de conditions de restriction.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Ajout de prenant en charge de JSON (AAD) en outre tooSWT (ACS), la valeur par défaut de hello TokenType est TokenType.JWT. Si vous utilisez SWT/ACS, vous devez définir tooTokenType.SWT.

## <a name="additional-topics-for-implementation"></a>Rubriques supplémentaires pour l’implémentation
Ensuite, nous aborderons certaines rubriques supplémentaires de notre conception et de l’implémentation.

### <a name="http-or-https"></a>HTTP ou HTTPS ?
Hello application de lecteur d’ASP.NET MVC nous générées doit prendre en charge suivantes d’hello :

1. Authentification des utilisateurs via Azure AD qui a besoin de toobe sous HTTPS ;
2. Échange de jeton JWT entre le client et Azure AD qui a besoin de toobe sous HTTPS ;
3. Acquisition de licence DRM par client hello qui est requis toobe sous HTTPS si la remise de la licence est fourni par Azure Media Services. Bien entendu, la suite de produits PlayReady n'impose pas le format HTTPS pour la distribution de licences. Si votre serveur de licences PlayReady se trouve en dehors d'Azure Media Services, vous pouvez utiliser HTTP ou HTTPS.

Par conséquent, hello application de lecteur ASP.NET utilisent le protocole HTTPS est recommandé. Cela signifie que hello Qu'azure Media Player sera sur une page sous HTTPS. Toutefois, pour la diffusion en continu nous préférons HTTP, par conséquent, nous devons tooconsider mixte les problèmes liés au contenu.

1. Le navigateur ne permet pas un contenu mixte. Cependant, les plug-ins tels que Silverlight et OSMF pour Smooth et DASH le permettent. Contenu mixte est un problème de sécurité : ce en raison de la menace de toohello de tooinject de capacité hello JS malveillants qui peut provoquer des hello toobe des données client exposés.  Navigateurs bloquent ce paramètre par défaut et jusqu'à présent hello seule façon toowork autour de hello (origine) côté serveur tooallow tous les domaines (quel que soit le protocole https ou http). Il ne s’agit probablement pas d’une idée judicieuse.
2. Il est préférable d’éviter les contenus mixtes : les deux doivent utiliser soit HTTP, soit utiliser HTTPS  Si du contenu mixte est lu, silverlightSS tech nécessite la suppression d’un avertissement de contenu mixte. flashSS tech traite le contenu mixte sans aucun avertissement.
3. Si votre point de terminaison de diffusion a été créé avant août 2014, il ne prend pas en charge HTTPS. Dans ce cas, créez et utilisez un nouveau point de terminaison pour le protocole HTTPS.

Dans l’implémentation de référence hello, pour le contenu protégé par DRM, application et la diffusion en continu sera sous HTTTPS. Pour ouvrir contenu, le lecteur hello ne doit pas l’authentification ou licence, afin que vous ayez hello liberty toouse HTTP ou HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Substitution de la clé de signature Azure Active Directory
Il s’agit d’un tootake point important en considération de votre implémentation. Si vous ne considérez pas cela dans votre implémentation, système de hello terminée sera finalement cessent de fonctionner complètement dans les 6 semaines au maximum.

Azure AD utilise une confiance industrie tooestablish standard entre lui-même et les applications à l’aide d’Azure AD. Azure AD utilise plus particulièrement une clé de signature se composant d’une paire clé publique-clé privée. Lorsque Azure AD crée un jeton de sécurité qui contient des informations sur l’utilisateur de hello, ce jeton est signé par Azure AD à l’aide de sa clé privée avant son envoi différé toohello application. tooverify hello jeton est valide et provient bien d’Azure AD, l’application hello doit valider la signature du jeton hello à l’aide de la clé publique de hello exposé par Azure AD, qui est contenue dans le document de métadonnées de fédération du locataire hello. Cette clé publique – et les hello à partir duquel il dérive de clé de signature – sont hello celui utilisé pour tous les locataires dans Azure AD.

Vous trouverez des informations détaillées sur la substitution de clé d’Azure AD dans le document de hello : [des informations importantes sur la substitution des clés de signature dans Azure AD](../active-directory/active-directory-signing-key-rollover.md).

Entre hello [paire de clés publique-privée](https://login.microsoftonline.com/common/discovery/keys/),

* la clé privée Hello est utilisée par Azure Active Directory toogenerate un jeton Web JSON ;
* clé publique de Hello est utilisée par une application, telles que les Services de remise de licences DRM dans AMS tooverify hello un jeton JWT ;

à des fins de sécurité, Azure Active Directory renouvelle ce certificat périodiquement (toutes les 6 semaines). En cas de violations de la sécurité, substitution de clé hello peut se produire chaque fois. Services de remise de licences hello dans AMS doivent clé publique de tooupdate hello utilisé comme Azure AD fait pivoter la paire de clés hello, sinon l’authentification des jetons dans AMS échoue et aucune licence n’est émis.

Pour ce faire, il faut définir TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument au moment de configurer les services de distribution de licence DRM.

Hello flux de jeton JWT est comme ci-dessous :

1. Azure AD émet un jeton JWT hello avec la clé privée de hello en cours pour un utilisateur authentifié ;
2. Lorsqu’un lecteur voit une CENC avec un contenu protégé par multi-DRM, il sera d’abord localiser un jeton JWT hello émis par Azure AD.
3. le lecteur de Hello envoie la demande d’acquisition de licence avec les services de livraison toolicense jeton hello JWT dans AMS ;
4. services de remise de licences Hello dans AMS utilisera hello en cours/valides clé publique du jeton de Azure AD tooverify hello Web JSON, avant d’émettre des licences.

Services de remise de licences DRM seront toujours vérifier pour la clé publique de hello en cours/valides à partir d’Azure AD. clé publique de Hello présentée par Azure AD seront clé hello permettant de vérifier un jeton JWT émis par Azure AD.

Que se passe-t-il si la substitution de clé hello se produit après AAD génère un jeton Web JSON, mais avant hello JWT jeton est envoyé par les lecteurs tooDRM licence remise services dans AMS pour la vérification ?

Car une clé peut être changée à tout moment, il est toujours plus d’une clé publique valide disponible dans le document de métadonnées de fédération hello. Distribution de licences Azure Media Services peut utiliser hello clés spécifiées dans le document de hello, dans la mesure où une clé peut être changée rapidement, un autre peut être son remplacement et ainsi de suite.

### <a name="where-is-hello-access-token"></a>Dans lequel l’est hello jeton d’accès ?
Si vous examinez comment une application web appelle une application API sous [identité de l’Application avec l’octroi des informations d’identification du Client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), flux d’authentification hello est comme ci-dessous :

1. Un utilisateur est connecté dans tooAzure AD dans l’application web de hello (voir hello [tooWeb de navigateur Web Application](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. point de terminaison d’autorisation Hello Azure AD redirige l’application hello utilisateur agent toohello précédent client avec un code d’autorisation. l’agent utilisateur de Hello retourne l’URI de redirection de l’application cliente d’autorisation code toohello.
3. application web de Hello doit tooacquire un jeton d’accès pour qu’il peut s’authentifier toohello web API et récupération de la ressource de hello souhaité. Il rend le point de terminaison token un tooAzure de demande d’AD, en fournissant des informations d’identification hello, ID de client et URI d’ID d’application de l’API web. Elle présente tooprove de code d’autorisation hello que hello utilisateur a donné son consentement.
4. Azure AD authentifie l’application hello et retourne un jeton d’accès JWT est utilisé toocall hello web API.
5. Sur HTTPS, application web de hello utilise hello retourné hello de tooadd jeton d’accès JWT chaîne JWT avec une désignation « Support » dans l’en-tête d’autorisation de hello d’API web toohello demande de hello. API web de Hello valide ensuite un jeton JWT hello, et si la validation est réussie, retourne hello souhaitée des ressources.

Dans ce flux « application identity », API web de hello fait confiance à cet utilisateur de hello web application hello authentifié. C’est pour cette raison que ce modèle est appelé « sous-système approuvé ». Hello [diagramme sur cette page](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) décrit comment le code d’autorisation accorder flux fonctionne.

Dans l’acquisition de licence avec restriction token, nous continuons à hello même modèle de sous-système approuvé. Et service de remise de licences hello dans Azure Media Services est la ressource d’API web hello, hello « ressource principal » tooaccess a besoin d’une application web. Où est donc de jeton d’accès hello ?

Nous devons obtenir un jeton d’accès de la part d’Azure AD. Une fois l’authentification utilisateur réussie, le code d’autorisation est renvoyé. code d’autorisation de Hello est ensuite utilisé, ainsi que d’application et les ID de clé de client, tooexchange pour le jeton d’accès. Et jeton d’accès hello pour accéder à une application « pointeur » qui pointe ou représentant le service de remise de licences Azure Media Services.

Nous avons besoin tooregister et que vous configurez hello « pointeur » application dans Azure AD en suivant les étapes de hello ci-dessous :

1. Dans le client de hello Azure AD

   * ajouter une application (ressource) avec l’URL de connexion :

   https://[nom_ressource].azurewebsites.net/ et

   * URL d’ID d’application :

   https://[nom_client_aad].onmicrosoft.com/[nom_ressource]
2. Ajoutez une nouvelle clé pour l’application de ressource hello ;
3. Mettre à jour du fichier manifeste d’application hello afin que la propriété de groupMembershipClaims hello a hello valeur suivante : « groupMembershipClaims » : « Tous »,  
4. Dans l’application Azure AD de hello pointant toohello lecteur web app, dans la section de hello « autorisations tooother applications », ajouter une application de ressource hello qui a été ajoutée à l’étape 1 ci-dessus. Sous « autorisations déléguées », cliquez sur la coche « Accès [nom_ressource] ». Cela autorise hello web application toocreate des jetons d’accès pour accéder à application de ressource hello. Vous devez le faire pour la version locale et déployée de hello web application si vous développez avec l’application web Visual Studio et Azure.

Par conséquent, un jeton JWT hello émis par Azure AD est effectivement jeton d’accès hello pour accéder à cette ressource de « pointeur ».

### <a name="what-about-live-streaming"></a>Qu’en est-il de la diffusion en continu ?
Bonjour ci-dessus, notre discussion a été en mettant l’accent sur les ressources à la demande. Qu’en est-il de la diffusion en continu ?

Hello excellente est que vous pouvez utiliser exactement hello même conception et implémentation de la protection de diffusion en continu dans Azure Media Services, en traitant asset hello associé à un programme comme une « ressource VOD ».

Plus précisément, il est bien connu que toodo diffusion en continu dans Azure Media Services, vous devez toocreate un canal, puis un programme sous un canal de hello. programme de hello toocreate, vous devez toocreate un élément multimédia qui contient une archive de programme de hello en hello. Dans l’ordre tooprovide CENC avec la protection de multi-DRM du contenu dynamique hello, il vous suffit de toodo, est tooapply hello même le programme d’installation/de traitement toohello actif comme si elle était un « asset VOD » avant de démarrer le programme de hello.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>Qu’en est-il des serveurs de licences hors Azure Media Services ?
Souvent, les clients investissent dans une batterie de serveurs qu’ils hébergent dans leur propre centre de données ou chez des fournisseurs de service DRM. Heureusement, Protection du contenu Azure Media Services vous permet de toooperate en mode hybride : contenu hébergé et dynamiquement protégées dans Azure Media Services, alors que les licences DRM sont fournies par les serveurs en dehors d’Azure Media Services. Dans ce cas, il existe des hello suivant des considérations relatives à des modifications :

1. Hello Service d’émission de jeton sécurisé besoins tooissue jetons qui sont acceptables et peuvent être vérifiés par batterie de serveurs de licences hello. Par exemple, les serveurs de licences Widevine hello fournies par Axinom requiert un jeton JWT spécifique qui contient « message droit ». Par conséquent, vous devez toohave une tooissue STS ce jeton Web JSON. les auteurs de Hello est terminé une telle implémentation et vous trouverez des détails de hello Bonjour suivant du document dans [centre de Documentation Azure](https://azure.microsoft.com/documentation/): [tooAzure Media Servicesleslicencesàl’aidedeAxinomtoodeliverWidevine](media-services-axinom-integration.md).
2. Vous n’avez plus besoin service de remise de licences tooconfigure (ContentKeyAuthorizationPolicy) dans Azure Media Services. Vous devez toodo est l’URL d’acquisition de licence de tooprovide hello (pour PlayReady, Widevine et FairPlay) lorsque vous configurez AssetDeliveryPolicy dans Configuration CENC avec multi-DRM.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>Que se passe-t-il si je veux toouse un STS personnalisé ?
Il peut exister plusieurs raisons un client peut choisir toouse un STS personnalisé (Secure Token Service) pour fournir des jetons JWT. parmi lesquelles :

1. Hello fournisseur d’identité (IDP) utilisé par le client de hello ne prend pas en charge le STS. Dans ce cas, un service STS pourrait être une option.
2. client de Hello peut-être un contrôle plus souple ou plus strict dans intégrant STS abonné du client système de facturation. Par exemple, un opérateur MVPD peut offrir plusieurs packages d’abonné OTT comme premium, basic, sports, opérateur de hello etc. pouvez toomatch les revendications de hello dans un jeton avec le package de l’abonné afin que seul le contenu dans le package approprié de hello est rendue disponible. Dans ce cas, un STS personnalisé fournit hello nécessaire flexibilité et contrôle.

Deux modifications doivent toobe effectuée lors de l’utilisation d’un STS personnalisé :

1. Lorsque vous configurez le service de remise de licences d’un composant, vous devez la clé de sécurité hello toospecify utilisé pour la vérification par le STS personnalisé hello (plus de détails ci-dessous) au lieu de la clé actuelle de hello d’Azure Active Directory.
2. Lorsqu’un jeton JTW est généré, une clé de sécurité est spécifiée au lieu de la clé privée de hello du certificat hello X509 actuelle dans Azure Active Directory.

Il existe deux types de clés de sécurité :

1. Clé symétrique : hello même clé est utilisée pour générer et vérifier un jeton Web JSON ;
2. Clé asymétrique : une paire de clés publique-privée dans un X509 certificat est utilisé avec une clé privée pour chiffrer/génération d’un JWT hello et jeton de clé publique pour la vérification de jeton de hello.

#### <a name="tech-note"></a>Note technique
Si vous utilisez .NET Framework / C# comme plateforme de développement, hello X509 certificat utilisé pour la clé de sécurité asymétrique doit avoir au moins 2048 longueur de clé. Il s’agit d’une spécification de classe de hello System.IdentityModel.Tokens.X509AsymmetricSecurityKey dans .NET Framework. Dans le cas contraire, hello l’exception suivante est levée :

IDX10630 : hello 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' pour la signature ne peut pas être inférieure à '2048' bits.

## <a name="hello-completed-system-and-test"></a>test et du système de hello terminée
Nous vous guide dans quelques scénarios dans le système de bout en bout hello terminée afin que les lecteurs peuvent avoir une « image » du comportement de hello basic avant d’obtenir un compte de connexion.

Hello application web de lecteur et sa connexion se trouvent [ici](https://openidconnectweb.azurewebsites.net/).

Si vous avez besoin est « non intégré » le scénario : ressources vidéo hébergé dans Azure Media Services sont soit non protégé, les DRM protégé mais sans l’authentification des jetons (émettre un toowhoever licence demandant), vous pouvez le tester sans connexion (en basculant tooHTTP si votre vidéo en continu est effectuée via HTTP).

Si vous avez besoin est scénario intégrée de bout en bout : ressources vidéo est sous protection DRM dynamique dans Azure Media Services, avec le jeton d’authentification et jeton Web JSON généré par Azure AD, vous devez toologin.

### <a name="user-login"></a>Connexion utilisateur
Commande tootest hello bout en bout DRM système intégré, vous devez toohave un « compte » créé ou ajouté.

Quel compte ?

Même si Azure avait initialement autorisé l’accès aux utilisateurs de compte Microsoft uniquement, il autorise désormais l’accès aux utilisateurs des deux systèmes. Cela a été effectuée en faisant confiance de propriétés Azure toutes les hello Azure AD pour l’authentification, ayant Azure AD d’authentification des utilisateurs professionnels et en créant une relation de fédération où Azure AD approuve le système d’identité hello Microsoft compte consommateur tooauthenticate particuliers. Par conséquent, Azure AD est tooauthenticate en mesure des comptes de Microsoft « invités », ainsi que les comptes Azure AD « natifs ».

Étant donné que Azure AD approuve le domaine de compte Microsoft (MSA), vous pouvez ajouter des comptes à partir des hello suivant toohello de domaines personnalisé Azure AD de client et utilisent hello compte toologin :

| **Nom de domaine** | **Domaine** |
| --- | --- |
| **Domaine client Azure AD personnalisé** |somename.onmicrosoft.com |
| **Domaine d’entreprise** |microsoft.com |
| **Domaine de compte Microsoft (MSA)** |outlook.com, live.com, hotmail.com |

Vous pouvez contacter un des auteurs de hello toohave un compte créé ou ajoutés pour vous.

Vous trouverez ci-dessous des captures d’écran de hello de pages de connexion différents utilisés par les différents comptes de domaine.

**Compte de domaine de client personnalisé Azure AD**: dans ce cas, vous voyez la page de connexion personnalisée hello du domaine du client hello personnalisé Azure AD.

![compte de domaine client Azure personnalisé](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Compte de domaine Microsoft avec carte à puce**: dans ce cas vous consultez la page de connexion hello personnalisé par Microsoft d’entreprise informatique à l’aide de l’authentification à deux facteurs.

![compte de domaine client Azure personnalisé](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Compte Microsoft (MSA)**: dans ce cas, vous voyez la page de connexion de hello de Account Microsoft pour les consommateurs.

![compte de domaine client Azure personnalisé](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Utilisation de Encrypted Media Extensions pour PlayReady
Sur un navigateur modern avec chiffrés Media Extensions (EME) pour la prise en charge, tels que navigateur Internet Explorer 11 sur Windows 8.1 et suivantes et Microsoft Edge sur Windows 10, PlayReady sera de PlayReady hello DRM sous-jacent pour EME.

![Utilisation d’EME pour PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

la zone de lecteur sombre Hello est dû fait toohello que la protection PlayReady empêche un d’effectuer la capture d’écran de la vidéo protégé.

Hello d’écran suivante montre plug-ins du lecteur hello et prise en charge MSE/EME.

![Utilisation d’EME pour PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

EME dans Microsoft Edge et IE 11 sur Windows 10 permet d’appeler [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) sur les appareils Windows 10 compatibles. PlayReady SL3000 déverrouille flux hello de contenu premium améliorées (4 Ko, en-tête, etc.) et les nouveaux modèles de diffusion de contenu (fenêtre anticipée de contenu amélioré).

Se concentrer sur des appareils Windows hello : PlayReady est hello uniquement DRM dans HW hello disponible sur les appareils Windows (PlayReady SL3000). Un service de diffusion en continu peut utiliser PlayReady via EME ou via une application UWP, et offrir ainsi une meilleure qualité vidéo à l'aide de PlayReady SL3000 par rapport à un autre DRM. En règle générale, 2K contenu flux au sein de Chrome ou Firefox, et 4 K contenu via Microsoft Edge/IE11 ou une application UWP sur hello même appareil (en fonction des paramètres de service et l’implémentation).

#### <a name="using-eme-for-widevine"></a>Utilisation d’EME pour Widevine
Sur un navigateur modern avec EME/Widevine prise en charge, telles que Chrome 41 + sur Windows 10, Windows 8.1, Mac OSX Yosemite et Chrome sur Android 4.4.4, Google Widevine est hello DRM derrière EME.

![Utilisation d’EME pour Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Notez que Widevine n’empêche pas d’effectuer une capture d’écran de la vidéo protégée.

![Utilisation d’EME pour Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Utilisateurs sans intitulé
Si un utilisateur n’est pas membre du groupe « Utilisateurs intitulée », utilisateur de hello ne sera pas toopass en mesure de « droit vérification » et service de licence de multi-DRM hello refusera licence demandée de hello tooissue comme indiqué ci-dessous. Bonjour description détaillée est « acquisition de licence a échoué », qui est conçu.

![Utilisateurs non autorisés](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Exécution d’un Service d’émission de jeton sécurisé personnalisé
Pour le scénario hello personnalisé sécuriser Service d’émission de jeton en cours d’exécution, un jeton JWT hello est émis par un STS personnalisé de hello à l’aide de la clé symétrique ou asymétrique.

cas de Hello d’à l’aide de la clé symétrique (à l’aide de Chrome) :

![Exécution de STS personnalisé](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

Hello cas d’utilisation d’une clé asymétrique via un X509 de certificat (à l’aide du navigateur moderne de Microsoft).

![Exécution de STS personnalisé](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

Dans les deux hello au-dessus de cas, reste de l’authentification utilisateur même : hello via Azure AD. Hello seule différence est que les jetons JWT sont émis par STS personnalisé de hello au lieu d’Azure AD. Bien entendu, lorsque vous configurez la protection CENC dynamique, restriction hello du service de remise de licences spécifie type hello de jeton JWT, clé symétrique ou asymétrique.

## <a name="summary"></a>Résumé
Dans ce document, nous avons abordé les sujets des DRM natives multiples, et un contrôle d’authentification des jetons : sa conception et son implémentation à l’aide d’Azure, d’Azure Media Services et d’Azure Media Player.

* Un modèle de référence est présenté qui contient tous les composants nécessaires hello dans un sous-système DRM/CENC ;
* Une implémentation de référence sur Azure, Azure Media Services et Azure Media Player.
* Certaines rubriques directement impliqués dans hello conception et implémentation sont également décrites.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
