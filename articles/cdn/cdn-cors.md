---
title: aaaUsing CDN Azure avec CORS | Documents Microsoft
description: "Découvrez comment toouse hello toowith de réseau de distribution contenu (CDN) Azure de partage de ressources Cross-Origin (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Utilisation d’Azure CDN avec CORS
## <a name="what-is-cors"></a>Présentation de CORS
CORS (cross-Origin Resource Sharing) est une fonctionnalité HTTP qui permet à une application web en cours d’exécution ressources de tooaccess sous un domaine dans un autre domaine. Dans le risque de hello ordre tooreduce d’attaques de script entre sites, tous les navigateurs web modernes implémentent une restriction de sécurité appelée [stratégie de même origine](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Celle-ci empêche une page web d’appeler des API dans un autre domaine.  CORS constitue un toocall de (domaine d’origine hello) une origine de tooallow sûre API dans une autre origine.

## <a name="how-it-works"></a>Fonctionnement
Il existe deux types de demandes CORS : les *demandes simples* et *les demandes complexes*.

### <a name="for-simple-requests"></a>Pour les demandes simples :

1. navigateur de Hello envoie hello CORS demande supplémentaire **origine** en-tête de demande HTTP. valeur Hello de cet en-tête est origine hello qui a traité la page parente hello, qui est défini en tant que combinaison de hello de *protocole,* *domaine,* et *port.*  Lorsqu’une page à partir de https://www.contoso.com essaie de données d’un utilisateur à l’origine de fabrikam.com hello tooaccess, hello suivant l’en-tête de la requête sera donc envoyé toofabrikam.com :

   `Origin: https://www.contoso.com`

2. serveur de Hello peut répondre par hello suivants :

   * Un en-tête **Access-Control-Allow-Origin** indiquant le site d’origine autorisé. Par exemple :

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Une erreur HTTP de code tels que 403 si les serveur hello n’autorise pas de demande de cross-origin hello après avoir vérifié l’en-tête d’origine hello

   * Un en-tête **Access-Control-Allow-Origin** avec un caractère générique qui autorise toutes les origines :

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Pour les demandes complexes :

Une requête complexe est une demande CORS où le navigateur de hello est requis toosend un *demande préliminaire* (autrement dit, une sonde préliminaire) avant d’envoyer la demande CORS réelle de hello. Hello demande préliminaire demande autorisation de serveur hello si demande CORS d’origine de hello peut continuer et est un `OPTIONS` demande toohello même URL.

> [!TIP]
> Pour plus d’informations sur les flux CORS et pièges les plus courants, afficher hello [Guide tooCORS pour l’API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Scénarios avec caractère générique ou à origine unique
CORS sur Azure CDN fonctionnent automatiquement sans aucune configuration supplémentaire lorsque hello **Access-Control-Allow-Origin** en-tête a la valeur toowildcard (*) ou une origine unique.  Hello CDN mettra en cache les première réponse de hello et les demandes ultérieures utiliseront hello même en-tête.

Si les demandes ont déjà été apportées à tooCORS préalable du CDN toohello qui est définie sur hello votre origine, vous devez toopurge contenu sur votre hello tooreload contenu de point de terminaison avec hello **Access-Control-Allow-Origin** en-tête.

## <a name="multiple-origin-scenarios"></a>Scénarios avec plusieurs origines
Si vous devez tooallow une liste spécifique de toobe origines autorisée pour le service CORS, les choses deviennent un peu plus compliquées. problème de Hello se produit quand hello CDN met en cache hello **Access-Control-Allow-Origin** en-tête d’origine CORS de la première hello.  Une origine CORS différente lorsqu’une demande ultérieure, hello CDN servira hello mis en cache **Access-Control-Allow-Origin** en-tête qui ne correspondre pas.  Il existe plusieurs façons toocorrect cela.

### <a name="azure-cdn-premium-from-verizon"></a>CDN Azure Premium fourni par Verizon
Hello la meilleure façon tooenable il s’agit de toouse **Azure CDN Premium de Verizon**, qui expose certaines fonctionnalités avancées. 

Vous devez trop[créer une règle](cdn-rules-engine.md) toocheck hello **origine** en-tête de demande de hello.  S’il s’agit d’une origine valide, votre règle définit hello **Access-Control-Allow-Origin** en-tête avec origine hello fournie dans la demande de hello.  Si les origine hello spécifié dans hello **origine** en-tête n’est pas autorisé, votre règle doit omettre hello **Access-Control-Allow-Origin** en-tête, ce qui entraîne la demande de hello navigateur tooreject hello. 

Il existe deux façons toodo cela avec le moteur de règles hello.  Dans les deux cas, hello **Access-Control-Allow-Origin** en-tête à partir du serveur d’origine du fichier hello est complètement ignoré, moteur de règles du CDN hello gère hello autorisé origines CORS.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Une expression régulière avec toutes les origines valides
Dans ce cas, vous allez créer une expression régulière qui inclut toutes les origines de hello souhaité tooallow : 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> **CDN Azure fourni par Verizon** utilise [PCRE (Perl Compatible Regular Expressions)](http://pcre.org/) comme moteur pour les expressions régulières.  Vous pouvez utiliser un outil tel que [101 d’Expressions régulières](https://regex101.com/) toovalidate votre expression régulière.  Notez que hello « / » de caractères est valide dans les expressions régulières et n’a pas besoin de toobe d’échappement, toutefois, ce caractère d’échappement est considérée comme une meilleure pratique et n’est attendue par certains programmes de validation d’expression régulière.
> 
> 

Si l’expression régulière de hello correspond à, votre règle remplacera hello **Access-Control-Allow-Origin** en-tête (le cas échéant) à partir de l’origine hello avec origine hello qui a envoyé la demande de hello.  Vous pouvez également ajouter des en-têtes CORS, comme **Access-Control-Allow-Methods**.

![Exemple de règles avec expression régulière](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Règle d’en-tête de demande pour chaque origine
Au lieu d’expressions régulières, vous pouvez créer un distinct pour chaque origine de la règle vous souhaitez tooallow à l’aide de hello **génériques d’en-tête de demande** [correspondent à condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Comme avec la méthode d’expression régulière hello, hello moteur de règles définit uniquement les en-têtes CORS hello. 

![Exemple de règles sans expression régulière](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> Dans l’exemple hello ci-dessus, hello utilisation du caractère générique de hello * indique au moteur de règles de hello toomatch HTTP et HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Azure CDN Standard
Sur les profils d’Azure CDN Standard, hello tooallow mécanisme pour plusieurs origines sans utiliser de hello d’origine des caractères génériques hello est toouse [mise en cache de la chaîne de requête](cdn-query-string.md).  Vous devez tooenable paramètre de chaîne de requête pour le point de terminaison CDN hello et puis utilisez une chaîne de requête unique pour les demandes à partir de chaque domaine autorisé. Cette opération entraîne hello CDN mise en cache d’un objet distinct pour chaque chaîne de requête unique. Cette approche n’est pas idéale, toutefois, il entraînera des copies de hello même fichier mis en cache sur hello CDN.  

