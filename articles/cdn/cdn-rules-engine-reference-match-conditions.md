---
title: "conditions de correspondance du moteur des règles aaaAzure CDN | Documents Microsoft"
description: "Documentation de référence sur les fonctionnalités et conditions de correspondance du moteur de règles Azure CDN."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Conditions de correspondance du moteur de règles Azure CDN
Cette rubrique répertorie une description détaillée des hello disponibles aux Conditions de réseau de distribution contenu (CDN) pour Azure [moteur de règles](cdn-rules-engine.md).

Hello de deuxième partie d’une règle est la condition de correspondance hello. Une condition de correspondance identifie des types spécifiques de requêtes pour lesquelles un ensemble de fonctionnalités est exécuté.

Par exemple, il peut être utilisé toofilter demandes pour le contenu à un emplacement particulier, les requêtes générées à partir d’une adresse IP ou un pays particulier, ou par les informations d’en-tête.

## <a name="always"></a>Toujours

Bonjour condition de correspondance toujours est conçue tooapply une valeur par défaut définie de fonctionnalités tooall demandes.

## <a name="device"></a>Appareil

condition de correspondance du périphérique Hello identifie les demandes effectuées à partir d’un appareil mobile en fonction de ses propriétés.  La détection de périphérique mobile est obtenue par le biais de [WURFL](http://wurfl.sourceforge.net/).  Vous trouverez ci-dessous la liste des fonctionnalités WURFL et leurs variables de moteur de règles CDN.

> [!NOTE] 
> variables Hello ci-dessous sont pris en charge dans hello **modifier des en-tête de demande Client** et **modifier un en-tête de réponse Client** fonctionnalités.

Fonctionnalité | Variable | Description | Exemples de valeurs
-----------|----------|-------------|----------------
Nom de la marque | %{wurfl_cap_brand_name} | Chaîne qui indique le nom de marque de hello du périphérique de hello. | Samsung
Système d’exploitation de l’appareil | %{wurfl_cap_device_os} | Chaîne qui indique le système d’exploitation hello sur le périphérique de hello. | IOS
Version du système d’exploitation de l’appareil | %{wurfl_cap_device_os_version} | Chaîne qui indique le numéro de version hello Hello du système d’exploitation installé sur l’appareil de hello. | 1.0.1
Orientation double | %{wurfl_cap_dual_orientation} | Valeur booléenne qui indique si les appareils hello prend en charge la double orientation. | true
DTD HTML par défaut | %{wurfl_cap_html_preferred_dtd} | Chaîne qui indique la définition de type d’appareil mobile hello préféré de document (DTD) pour le contenu HTML. | Aucun<br/>xhtml_basic<br/>html5
Incorporation d’images | %{wurfl_cap_image_inlining} | Valeur booléenne qui indique si les appareils hello prend en charge Base64 les images encodées. | false
Est Android | %{wurfl_vcap_is_android} | Valeur booléenne qui indique si le périphérique de hello utilise hello du système d’exploitation Android. | true
Est IOS | %{wurfl_vcap_is_ios} | Valeur booléenne qui indique si le périphérique de hello utilise iOS. | false
Est une télévision intelligente | %{wurfl_cap_is_smarttv} | Valeur booléenne qui indique si le périphérique de hello est une télévision intelligente. | false
Est un smartphone | %{wurfl_vcap_is_smartphone} | Valeur booléenne qui indique si le périphérique de hello est un smartphone. | true
Est une tablette | %{wurfl_cap_is_tablet} | Valeur booléenne qui indique si le périphérique de hello est un Tablet PC. Il s’agit d’une description indépendante du système d’exploitation. | true
Est un appareil sans fil | %{wurfl_cap_is_wireless_device} | Valeur booléenne qui indique si les appareils hello sont considéré comme un appareil sans fil. | true
Nom marketing | %{wurfl_cap_marketing_name} | Chaîne qui indique le nom du périphérique hello. | BlackBerry 8100 Pearl
Navigateur mobile | %{wurfl_cap_mobile_browser} | Chaîne qui indique le navigateur de hello utilisé toorequest le contenu à partir de l’appareil de hello. | Chrome
Version du navigateur mobile | %{wurfl_cap_mobile_browser_version} | Chaîne qui indique la version de hello du navigateur de hello utilisé toorequest le contenu à partir de l’appareil de hello. | 31
Nom du modèle | %{wurfl_cap_model_name} | Chaîne qui indique le nom du modèle du périphérique hello. | s3
Téléchargement progressif | %{wurfl_cap_progressive_download} | Valeur booléenne qui indique si les appareil hello prend en charge la lecture de l’audio/vidéo hello pendant qu’il est toujours en cours de téléchargement. | true
Date de lancement | %{wurfl_cap_release_date} | Chaîne qui indique l’année de hello et mois sur le hello périphérique a été ajouté de base de données de toohello WURFL.<br/><br/>Format : `yyyy_mm` | 2013_december
Hauteur de résolution | %{wurfl_cap_resolution_height} | Entier qui indique la hauteur de l’appareil hello en pixels. | 768
Largeur de résolution | %{wurfl_cap_resolution_width} | Entier qui indique la largeur de l’appareil hello en pixels. | 1 024


## <a name="location"></a>Lieu

Ceux-ci correspondent aux conditions de demandes tooidentify conçus en fonction emplacement du demandeur hello.

Nom | Objectif
-----|--------
Numéro AS | Identifie les requêtes issues d’un réseau particulier.
Pays | Identifie les demandes provenant de hello spécifié pays.


## <a name="origin"></a>Origine

Ceux-ci correspondent aux conditions sont conçus tooidentify demandes tooCDN du point de stockage ou un serveur d’origine client.

Nom | Objectif
-----|--------
Origine CDN | Identifie les requêtes de contenu stocké sur le stockage CDN.
Origine client | Identifie les requêtes de contenu stocké sur le serveur d’origine d’un client spécifique.


## <a name="request"></a>Demande

Ceux-ci correspondent aux conditions de demandes tooidentify conçue selon leurs propriétés.

Nom | Objectif
-----|--------
Adresse IP du client | Identifie les requêtes issues d’une adresse IP particulière.
Paramètre de cookie | Vérifications hello cookies associés à chaque demande de hello spécifié valeur.
Expression régulière de paramètre de cookie | Vérifie les cookies hello associés à chaque demande de hello de l’expression régulière spécifiée.
Cname Edge | Identifie les requêtes qui pointent bord tooa CNAME.
Domaine de référence | Identifie les demandes qui ont été référencés à partir de hello spécifié hostname(s).
Littéral d’en-tête de requête | Identifie les requêtes qui contiennent hello spécifié en-tête ensemble tooa spécifié (s).
Expression régulière d’en-tête de requête | Identifie les requêtes qui contiennent hello spécifié en-tête tooa valeur qui correspond à hello spécifié d’expression régulière.
Caractère générique d’en-tête de requête | Identifie les requêtes qui contiennent hello spécifié en-tête valeur tooa qui correspond au modèle spécifié de hello.
Méthode de requête | Identifie les requêtes par leur méthode HTTP.
Modèle de requête | Identifie les requêtes par leur protocole HTTP.

## <a name="url"></a>URL

Ceux-ci correspondent aux conditions de demandes tooidentify conçus en fonction de leur URL.

Nom | Objectif
-----|--------
Répertoire du chemin d’URL | Identifie les requêtes par leur chemin relatif.
Extension du chemin d’URL | Identifie les requêtes par leur extension de nom de fichier.
Nom de fichier du chemin d’URL | Identifie les requêtes par leur nom de fichier.
Littéral du chemin d’URL | Compare une demande de chemin d’accès relatif toohello valeur spécifiée.
Expression régulière du chemin d’URL | Compare une demande spécifié de chemin d’accès relatif toohello l’expression régulière.
Caractère générique du chemin d’URL | Compare le modèle spécifié de toohello de chemin d’accès relatif d’une requête.
Littéral de requête d’URL | Compare une demande de valeur toohello de chaîne de requête spécifiée.
Paramètre de requête d’URL | Identifie les requêtes qui contiennent la requête spécifiée à hello paramètre de chaîne de valeur tooa qui correspond à un modèle spécifié.
Expression régulière de requête d’URL | Identifie les requêtes qui contiennent la requête spécifiée à hello paramètre de chaîne de valeur tooa qui correspond à une expression régulière spécifiée.
Caractère générique de requête d’URL | Compare hello spécifié (s) par rapport à hello de chaîne de requête.


## <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
* [Référence du moteur de règles](cdn-rules-engine-reference.md)
* [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-conditional-expressions.md)
* [Fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)

