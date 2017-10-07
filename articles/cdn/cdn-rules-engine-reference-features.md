---
title: "fonctionnalités du moteur de règles aaaAzure CDN | Documents Microsoft"
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
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Fonctionnalités du moteur de règles Azure CDN
Cette rubrique répertorie une description détaillée des fonctionnalités disponibles de hello réseau de distribution contenu (CDN) pour Azure [moteur de règles](cdn-rules-engine.md).

Hello de troisième partie d’une règle est la fonctionnalité de hello. Une fonctionnalité définit le type de hello d’action qui sera appliqué le type de toohello de requête identifié par un ensemble de conditions de correspondance.

## <a name="access"></a>Access

Ces fonctionnalités sont conçues toocontrol accès toocontent.


Nom | Objectif
-----|--------
Refuser l’accès | Détermine si toutes les requêtes sont rejetées avec une réponse 403 Interdit.
Authentification de jeton | Détermine si l’authentification basée sur le jeton sera appliqué tooa demande.
Code de refus d’authentification de jeton | Détermine le type hello de réponse qui sera renvoyé tooa utilisateur lorsqu’une demande est refusée en raison de l’authentification basée sur les tooToken.
Ignorer la casse de l’URL pour l’authentification de jeton | Détermine si les comparaisons d’URL effectuées par l’authentification basée sur les jetons respectent la casse.
Paramètre d’authentification de jeton | Détermine si le paramètre de chaîne de requête de l’authentification basée sur le jeton hello doit être renommé.

### <a name="deny-access"></a>Refuser l’accès
**Objectif** : détermine si toutes les requêtes sont rejetées avec une réponse 403 Interdit.

Valeur | Résultat
------|-------
Activé| Provoque la toutes les demandes qui répondent à hello correspondant critères toobe est rejetée avec réponse 403 Interdit.
Désactivé| Restaure le comportement par défaut de hello. comportement par défaut de Hello est tooallow hello server toodetermine hello type d’origine de la réponse qui sera renvoyé.

**Comportement par défaut** : Désactivé

> [!TIP]
   > Une utilisation possible de cette fonctionnalité est tooassociate avec un en-tête de demande correspond à la condition tooblock accès tooHTTP points d’accès qui utilisent le contenu tooyour inclus des liens.

### <a name="token-auth"></a>Authentification de jeton
**Objectif :** détermine si l’authentification basée sur le jeton sera appliqué tooa demande.

Si l’authentification basée sur le jeton est activée, seules les demandes qui fournissent un jeton chiffré et de satisfaire les exigences toohello spécifiés par ce jeton seront respectés.

clé de chiffrement Hello qui est les valeurs de jeton tooencrypt et de déchiffrement utilisés est déterminé par la clé primaire et les options de la clé de sauvegarde sur la page du jeton d’authentification. N’oubliez pas que les clés de chiffrement sont spécifiques de la plateforme.

Valeur | Résultat
------|---------
Activé | Protège hello demandé contenu avec l’authentification basée sur le jeton. Seules les demandes des clients qui fournissent un jeton valide et répondent aux exigences seront respectées. Les transactions FTP sont exclues de l’authentification basée sur les jetons.
Désactivé| Restaure le comportement par défaut de hello. Hello le comportement par défaut est tooallow votre toodetermine de configuration de l’authentification basée sur le jeton si une demande sera sécurisée.

**Comportement par défaut** : Désactivé.

###<a name="token-auth-denial-code"></a>Code de refus d’authentification de jeton
**Objectif :** détermine le type de hello de réponse qui sera renvoyé tooa utilisateur lorsqu’une demande est refusée en raison de l’authentification basée sur les tooToken.

codes de réponse disponible Hello sont répertoriées ci-dessous.

Code de la réponse|Nom de la réponse|Description
----------------|-----------|--------
301|Déplacé de façon permanente|Ce code d’état redirige les utilisateurs non autorisés toohello URL est spécifiée dans l’en-tête Location.
302|Trouvé|Ce code d’état redirige les utilisateurs non autorisés toohello URL est spécifiée dans l’en-tête Location. Ce code d’état est hello méthode standard de l’exécution d’une redirection.
307|Redirection temporaire|Ce code d’état redirige les utilisateurs non autorisés toohello URL est spécifiée dans l’en-tête Location.
401|Non autorisé|Combinaison de ce code d’état avec l’en-tête WWW-Authenticate de réponse vous permet de tooprompt un utilisateur pour l’authentification.
403|Interdit|Il s’agit de hello standard 403 Interdit message d’état qu’un utilisateur non autorisé s’affiche lorsque la tentative de tooaccess du contenu protégé.
404|Fichier introuvable|Ce code d’état indique que le client de hello HTTP a été en mesure de toocommunicate avec le serveur de hello, mais hello demandé de contenu n’a pas été trouvé.

#### <a name="url-redirection"></a>Redirection d’URL

Cette fonctionnalité prend en charge la redirection des URL URL défini par l’utilisateur le tooa lorsqu’il est configuré tooreturn un code d’état 3xx. Cette URL définie par l’utilisateur peut être spécifiée en effectuant hello comme suit :

1. Sélectionnez un code de réponse 3xx pour la fonctionnalité de Code de jeton d’authentification refus hello.
2. Sélectionnez « Location » à partir de l’option de nom de l’en-tête facultatif.
3. Définir l’URL de toohello souhaité option valeur de l’en-tête facultatif.

Si une URL n’est pas définie pour un code d’état 3xx, puis hello page de réponse standard pour un code d’état 3xx sera retourné toohello utilisateur.

La redirection des URL est uniquement applicable pour les codes de réponse 3xx.

L’option de valeur d’en-tête facultative prend en charge les caractères alphanumériques, les guillemets et les espaces.

#### <a name="authentication"></a>Authentification

Cette fonctionnalité prend en charge l’en-tête de tooinclude le WWW-Authenticate hello capacité lors de la réponse tooan de demande non autorisée pour le contenu protégé par l’authentification basée sur le jeton. Si l’en-tête WWW-Authenticate a été défini trop « basique » dans votre configuration, utilisateur non autorisé de hello sera invité à entrer des informations d’identification du compte.

Hello au-dessus de configuration peut être obtenue en effectuant hello comme suit :

1. Sélectionnez « 401 » en tant que code de réponse hello pour la fonctionnalité de Code de jeton d’authentification refus hello.
2. Sélectionnez « WWW-Authenticate » à partir de l’option de nom de l’en-tête facultatif.
3. Définir l’option de valeur de l’en-tête facultatif trop « base ».

L’en-tête WWW-Authenticate est uniquement applicable pour les codes de réponse 401.

### <a name="token-auth-ignore-url-case"></a>Ignorer la casse de l’URL pour l’authentification de jeton
**Objectif :** détermine si les comparaisons d’URL effectuées par l’authentification basée sur les jetons respectent la casse.

paramètres Hello affectés par cette fonctionnalité sont :

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Les valeurs autorisées sont :

Valeur|Résultat
---|----
Activé|Provoque le notre serveur edge tooignore cas lors de la comparaison des URL pour les paramètres de l’authentification basée sur le jeton.
Désactivé|Restaure le comportement par défaut de hello. Il est par défaut Hello pour les comparaisons d’URL pour toobe du jeton d’authentification qui respecte la casse.

**Comportement par défaut** : Désactivé.
 
### <a name="token-auth-parameter"></a>Paramètre d’authentification de jeton
**Objectif :** détermine si le paramètre de chaîne de requête de l’authentification basée sur le jeton hello doit être renommé.

Informations essentielles :

- L’option valeur définit le nom du paramètre chaîne requête hello via lequel un jeton peut être spécifié.
- Impossible de définir l’option valeur trop « ec_token ».
- Assurez-vous que ce nom hello défini dans l’option valeur uniquement 
- uniquement des caractères d’URL valides.

Valeur|Résultat
----|----
Activé|L’option valeur définit le nom du paramètre chaîne requête hello via lequel les jetons doivent être définis.
Désactivé|Un jeton peut être spécifié comme un paramètre de chaîne de requête non défini dans l’URL de demande hello.

**Comportement par défaut** : Désactivé. Un jeton peut être spécifié comme un paramètre de chaîne de requête non défini dans l’URL de demande hello.

## <a name="caching"></a>Mise en cache

Ces fonctionnalités sont conçue toocustomize quand et comment le contenu est mis en cache.

Nom | Objectif
-----|--------
Paramètres de bande passante | Détermine si les paramètres de limitation de bande passante (c.-à-d., ec_rate et ec_prebuf) sont actifs.
Limitation de bande passante | Limite la bande passante hello pour réponse hello fournie par nos serveurs edge.
Ignorer le cache | Détermine si la demande de hello peut tirer parti de notre technologie de mise en cache.
Traitement d’en-tête de contrôle de cache | Contrôles hello la génération des en-têtes de contrôle du Cache par le serveur de périphérie hello lors de la fonctionnalité de Max-Age externe est active.
Chaîne de requête de clé de cache | Détermine si hello-clé de cache s’inclure ou exclure les paramètres de chaîne de requête associés à une demande.
Réécriture de la clé de cache | Réécrit hello-clé de cache associé à une demande.
Remplissage de cache complet | Détermine ce qui se passe quand une requête génère une absence de cache partielle sur un serveur Edge.
Compresser les types de fichiers | Définit des formats de fichier hello qui doit être compressées sur le serveur hello.
Âge maximal interne par défaut | Détermine l’intervalle de max-age hello par défaut pour la revalidation du cache serveur edge server tooorigin.
Expiration du traitement d’en-tête | Contrôles hello la génération des en-têtes de la date d’expiration par un serveur edge lors de la fonctionnalité de Max-Age externe hello est active.
Âge maximal externe | Détermine l’intervalle de max-age hello revalidation du cache de navigateur tooedge server.
Forcer l’âge maximal interne | Détermine l’intervalle de max-age hello pour la revalidation du cache serveur edge server tooorigin.
Prise en charge H.264 (téléchargement progressif HTTP) | Détermine les types hello de H.264 formats de fichiers qui peuvent être utilisé toostream contenu.
Honorer la requête non-cache | Détermine si les demandes d’un client HTTP non-cache seront transférés toohello serveur d’origine.
Ignorer la requête non-cache d’origine | Détermine si notre CDN ignore certaines directives remises par un serveur d’origine.
Ignorer les plages inacceptables | Détermine la réponse hello qui sera renvoyé tooclients lorsqu’une requête génère un code d’état 416 plage demandée non satisfaisante.
Obsolescence maximale interne | Contrôle la durée pendant laquelle dépassant le délai d’expiration normale hello une ressource mise en cache peut être pris en charge à partir d’un serveur edge lorsque le serveur de périphérie hello est impossible toorevalidate hello asset mises en cache avec le serveur d’origine hello.
Partage de cache partiel | Détermine si une requête peut générer du contenu partiellement mis en cache.
Prévalider le contenu mis en cache | Détermine si du contenu mis en cache peut faire l’objet d’une revalidation anticipée avant l’expiration de sa durée de vie.
Actualiser les fichiers de cache de zéro octet | Détermine la façon dont nos serveurs Edge gèrent la requête d’un client HTTP liée à une ressource de cache de 0 octet.
Définir les codes d’état pouvant être mis en cache | Définit un jeu hello des codes d’état qui peuvent entraîner de contenu mis en cache.
Rendre obsolète la remise de contenu en cas d’erreur | Détermine si expiré contenu mis en cache est envoyée lorsqu’une erreur se produit lors de la revalidation du cache ou hello lors de la récupération a demandé le contenu à partir du serveur d’origine hello client.
Rendre obsolète pendant la revalidation | Améliore les performances en permettant à nos serveurs edge demandeur de toohello client obsolète tooserve lors de la revalidation a lieu.
Commentaire | fonctionnalité de commentaire Hello permet un toobe Remarque ajoutée au sein d’une règle.

###<a name="bandwidth-parameters"></a>Paramètres de bande passante
**Objectif :** détermine si les paramètres de limitation de bande passante (c.-à-d., ec_rate et ec_prebuf) sont actifs.

Les paramètres de limitation de bande passante déterminent si le taux de transfert de données hello pour une demande du client seront tooa limité des taux personnalisé.

Valeur|Résultat
--|--
Activé|Permet de nos serveurs edge toohonor de demandes de bande passante.
Désactivé|Provoque des paramètres de limitation de bande passante tooignore nos serveurs edge. Hello demandé contenu sera pris en charge normalement (c'est-à-dire, sans limitation de bande passante).

**Comportement par défaut :** Activé.

###<a name="bandwidth-throttling"></a>Limitation de bande passante
**Objectif :** accélérateurs hello la bande passante pour la réponse de hello fournie par nos serveurs edge.

Les deux options suivantes de hello doivent être défini tooproperly configurer la limitation de bande passante.

Option|Description
--|--
Koctets par seconde|Définissez cette option toohello la bande passante maximale (en Ko par seconde) qui peut-être être utilisés toodeliver hello réponse.
Secondes prebuf|Définissez un nombre de secondes d’attente jusqu'à ce que la limitation de bande passante nos serveurs edge toohello option. Hello cette période de la bande passante illimitée vise tooprevent un lecteur multimédia à partir de la raison d’interruption ou de mise en mémoire tampon des problèmes en raison de la limitation de toobandwidth.

**Comportement par défaut** : Désactivé.

###<a name="bypass-cache"></a>Ignorer le cache
**Objectif :** détermine si la demande de hello peut tirer parti de notre technologie de mise en cache.

Valeur|Résultat
--|--
Activé|Force toutes les demandes toofall, via le serveur d’origine toohello, même si le contenu hello a été précédemment mis en cache sur les serveurs edge.
Désactivé|Provoque des serveurs edge actifs toocache selon la stratégie de cache toohello défini dans ses en-têtes de réponse.

**Comportement par défaut :**

- **HTTP Large :** Désactivé

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Traitement d’en-tête de contrôle de cache
**Objectif :** contrôle la génération de hello des en-têtes de contrôle du Cache par le serveur de périphérie hello lors de la fonction Max-Age externe est active.

Hello tooachieve de façon plus simple est de ce type de configuration tooplace hello Max-Age externes et des fonctionnalités de traitement d’en-tête Cache-Control hello dans hello même instruction.

Valeur|Résultat
--|--
Remplacer|Garantit que hello suivant actions aura lieu :<br/> -Remplace l’en-tête Cache-Control généré par le serveur d’origine hello. <br/>-Ajoute l’en-tête Cache-Control produit par hello réponse de toohello fonctionnalité Max-Age externe.
Transmettre directement|Garantit que l’en-tête Cache-Control produit par la fonctionnalité de Max-Age externe hello n’est jamais ajouté toohello réponse. <br/> Si le serveur d’origine hello génère un en-tête Cache-Control, celui-ci passe par l’utilisateur toohello. <br/> Cause hello réponse en-tête toonot peut contenir un en-tête Cache-Control si le serveur d’origine hello ne produit pas un en-tête Cache-Control, alors cette option.
Ajouter si manquant|Si un en-tête Cache-Control n’a pas été reçu à partir du serveur d’origine hello, cette option ajoute l’en-tête Cache-Control produit par la fonctionnalité de Max-Age externe hello. Cette option est utile pour s’assurer que toutes les ressources recevront un en-tête de contrôle de cache.
Supprimer| Cette option garantit qu’un en-tête Cache-Control n’est pas inclus dans la réponse de l’en-tête hello. Si un en-tête Cache-Control a déjà été attribué, il sera supprimé à partir de la réponse de l’en-tête hello.

**Comportement par défaut :** Remplacer.

###<a name="cache-key-query-string"></a>Chaîne de requête de clé de cache
**Objectif :** détermine si la clé de cache inclut ou exclut les paramètres de chaîne de requête associés à une requête.

Informations essentielles :

- Spécifiez un ou plusieurs noms de paramètre de chaîne de requête. Chaque nom de paramètre doit être délimité par un espace.
- Cette fonctionnalité détermine si les paramètres de chaîne de requête sont inclus ou exclus de la clé de cache hello. Vous trouverez des informations supplémentaires pour chaque option ci-dessous.

Type|Description
--|--
 Inclure|  Indique que chaque paramètre spécifié doit être inclus dans la clé de cache hello. Une clé de cache unique est générée pour chaque requête contenant une valeur unique pour un paramètre de chaîne de requête défini dans cette fonctionnalité. 
 Inclure tout  |Indique qu’une clé de cache unique sera créée pour chaque élément multimédia tooan demande qui inclut une chaîne de requête unique. Ce type de configuration n’est généralement pas recommandé car elle peut entraîner des tooa petit pourcentage de présences dans le cache. Cela augmentera la charge hello sur le serveur d’origine hello, dans la mesure où il aura tooserve plus de requêtes. Cette configuration duplique hello comportement appelé « unique-cache » sur la page mise en cache de la chaîne de requête de mise en cache. 
 Exclure | Indique que seul hello spécifié seront exclus ou des paramètres à partir de la clé de cache hello. Tous les autres paramètres de chaîne de requête sont inclus dans la clé de cache hello. 
 Exclure tous  |Indique que tous les paramètres de chaîne de requête seront exclus de la clé de cache hello. Cette configuration duplique la mise en cache de comportement, appelé « standard-cache » sur la page mise en cache de la chaîne de requête de la valeur par défaut hello. 

alimentation Hello du moteur de règles HTTP vous permet de manière de hello toocustomize dans lesquels la mise en cache de chaîne de requête est implémentée. Par exemple, vous pouvez spécifier que la mise en cache de la chaîne de requête est effectuée uniquement sur certains emplacements ou types de fichiers.

Si vous souhaitez que la chaîne de requête tooduplicate hello comportement appelé « no-cache » sur la page mise en cache de la chaîne de requête de mise en cache, vous devez toocreate une règle qui contient une condition de correspondance générique de requête d’URL et une fonctionnalité de contournement du Cache. Hello condition de correspondance générique de requête URL doit être définie tooan astérisque (*).

#### <a name="sample-scenarios"></a>Exemples de scénarios

Des exemples d’utilisation de cette fonctionnalité spnt fournis ci-dessous. Un exemple de demande et de hello de clé de cache par défaut sont fournies ci-dessous.

- **Exemple de requête :** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&amp;language=EN&amp;userid=01
- **Clé de cache par défaut :** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Inclure

Exemple de configuration :

- **Type :** Inclure
- **Paramètre(s) :** langue

Ce type de configuration génèrent hello suivant cache-clé de paramètre de chaîne de requête :

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Inclure tout

Exemple de configuration :

- **Type :** Inclure tout

Ce type de configuration génèrent hello suivant cache-clé de paramètre de chaîne de requête :

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Exclure

Exemple de configuration :

- **Type :** Exclure
- **Paramètre(s) :**sessionid userid

Ce type de configuration génèrent hello suivant cache-clé de paramètre de chaîne de requête :

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Exclure tous

Exemple de configuration :

- **Type :** Exclure tous

Ce type de configuration génèrent hello suivant cache-clé de paramètre de chaîne de requête :

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Réécriture de la clé de cache
**Objectif :** réécritures hello associé à une demande de clé de cache.

Une clé de cache est hello chemin d’accès relatif qui identifie une ressource à des fins hello de mise en cache. En d’autres termes, nos serveurs recherchera une version mise en cache d’une ressource en fonction du chemin d’accès tooits tel que défini par sa clé de cache.

Configurer cette fonctionnalité en définissant deux hello options suivantes :

Option|Description
--|--
Chemin d’accès d’origine| Définir des types de toohello de chemin d’accès relatif hello de demandes dont clé de cache sera réécrit. Un chemin d’accès relatif peut être défini en sélectionnant un chemin d’accès d’origine de base et en définissant un modèle d’expression régulière.
Nouveau chemin d’accès|Définir le chemin d’accès relatif de hello pour hello nouvelle clé de cache. Un chemin d’accès relatif peut être défini en sélectionnant un chemin d’accès d’origine de base et en définissant un modèle d’expression régulière. Ce chemin d’accès relatif peut être construit dynamiquement à l’aide de hello de variables HTTP
**Comportement par défaut :** clé d’une demande de cache est déterminée par les URI de demande hello.

###<a name="complete-cache-fill"></a>Remplissage de cache complet
**Objectif :** détermine ce qui se passe quand une requête génère une absence de cache partielle sur un serveur Edge.

Une absence dans le cache partiel décrit l’état du cache de hello d’un composant qui n’était pas serveur de périphérie tooan complètement téléchargé. Si un élément multimédia n'est que partiellement mises en cache sur un serveur edge, puis hello demande suivante pour cet élément multimédia est transféré à nouveau serveur d’origine toohello.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Une absence de cache partielle se produit généralement après qu’un utilisateur a abandonné un téléchargement ou pour les ressources qui sont demandées uniquement à l’aide de requêtes de plage HTTP. Cette fonctionnalité est particulièrement utile pour les éléments multimédias volumineux, où les utilisateurs ne permet pas généralement de le télécharger à partir du début toofinish (par exemple, des vidéos). Par conséquent, cette fonctionnalité est activée par défaut sur la plateforme de grandes HTTP hello. Elle est désactivée sur toutes les autres plateformes.

Il est tooleave hello par défaut configuration recommandée de plateforme HTTP volumineux de hello, puisqu’elle sera réduire la charge de hello sur votre serveur d’origine client et augmenter la vitesse de hello auquel vos clients téléchargement votre contenu.

En raison de la manière de toohello dans le cache, les paramètres sont suivies, cette fonctionnalité ne peut pas être associée à hello conditions de correspondance suivantes : bord Cname, demander l’en-tête littéral, demander en-tête génériques, littérale de requête URL et URL de requête génériques.

Valeur|Résultat
--|--
Activé|Restaure le comportement par défaut de hello. comportement par défaut de Hello est tooinitiate pour le serveur edge tooforce hello une extraction en arrière-plan de l’élément multimédia de hello hello serveur d’origine. Après quoi, asset de hello sera dans le cache local du serveur de périphérie hello.
Désactivé|Un serveur edge empêche d’effectuer une récupération en arrière-plan pour un composant de hello. Cela signifie que cette demande suivante hello de cet élément multimédia à partir de cette région entraîne une toorequest de serveur de bord à partir du serveur d’origine hello client.

**Comportement par défaut :** Activé.

###<a name="compress-file-types"></a>Compresser les types de fichiers
**Objectif :** définit des formats de fichier hello qui doit être compressées sur le serveur hello.

Un format de fichier peut être spécifié à l’aide de son type de média Internet (par exemple, Content-Type). Type de média Internet est indépendantes de la plate-forme permet d’utiliser notre format de fichier serveurs tooidentify hello d’une ressource particulière. Vous trouverez ci-dessous une liste des types de média Internet courants.

Type de média Internet|Description
--|--
texte/brut|Fichiers de texte brut
texte/html| Fichiers HTML
texte/css|Cascading Style Sheets (CSS)
application/x-javascript|JavaScript
application/javascript|JavaScript
Informations essentielles :

- Spécifiez plusieurs types de média Internet en délimitant chacun d’entre eux à l’aide d’un seul espace. 
- Cette fonctionnalité compresse uniquement les ressources dont la taille est inférieure à 1 Mo. Les ressources plus volumineuses ne seront pas compressées par nos serveurs.
- Certains types de contenu, tels que des images, des vidéos et des éléments multimédias audio (par exemple, JPG, MP3, MP4, etc.), sont déjà compressés. Une compression supplémentaire sur ces types de ressources ne diminuera pas la taille de fichier de manière significative. Par conséquent, il est recommandé de ne pas activer la compression sur ces types de ressources.
- Les caractères génériques, tels que des astérisques, ne sont pas pris en charge.
- Avant d’ajouter la règle de tooa de cette fonctionnalité, assurez-vous que tooset l’option de Compression désactivé dans la page de Compression pour toowhich de plateforme hello que cette règle sera appliquée.

###<a name="default-internal-max-age"></a>Âge maximal interne par défaut
**Objectif :** intervalle de max-age détermine hello par défaut pour la revalidation du cache serveur edge server tooorigin. En d’autres termes, durée hello écoulées avant que d’un serveur edge vérifie si un élément mis en cache correspond à asset hello stocké sur le serveur d’origine hello.

Informations essentielles :

- Cette action aura lieu uniquement pour les réponses issues d’un serveur d’origine qui n’a pas attribué d’indication d’âge maximal dans l’en-tête de contrôle de cache ou d’expiration.
- Cette action n’aura pas lieu pour les ressources qui ne sont pas considérées comme susceptibles d’être mises en cache.
- Cette action n’affecte pas le nombre de revalidations du cache du serveur de tooedge navigateur. Ces types de nombre de revalidations du sont déterminés par le Cache-Control ou Expires en-têtes envoyés navigateur toohello, ce qui peut être personnalisée avec la fonction Max-Age externe.
- résultats Hello de cette action n’ont pas d’effet observable sur les en-têtes de réponse hello et contenu de hello retourné à partir de serveurs de bord pour votre contenu, mais elle peut avoir une incidence sur la quantité de hello de revalidation du trafic à partir du serveur d’origine tooyour bord serveurs.
- Configurez cette fonctionnalité en :
    - Code d’état en sélectionnant hello pour lequel un max-age interne par défaut peut être appliqué.
    - En spécifiant une valeur entière, puis en sélectionnant hello unité de temps souhaitée (par exemple, secondes, minutes, heures, etc.). Cette valeur définit l’intervalle de max-age interne hello par défaut.

- Unité de temps de paramètre hello trop « Off » affecte un intervalle de max-age interne par défaut de 7 jours pour les demandes qui n’ont pas reçus d’une indication de max-age dans leur Cache-Control ou l’en-tête Expires.
- En raison de la manière de toohello dans le cache, les paramètres sont suivies, cette fonctionnalité ne peut pas être associée à hello conditions de correspondance suivantes : 
    - Edge 
    - Cname
    - Littéral d’en-tête de requête
    - Caractère générique d’en-tête de requête
    - Méthode de requête
    - Littéral de requête d’URL
    - Caractère générique de requête d’URL

**Valeur par défaut :** 7 jours

###<a name="expires-header-treatment"></a>Expiration du traitement d’en-tête
**Objectif :** contrôle la génération de hello des en-têtes de la date d’expiration par un serveur edge lorsque la fonction Max-Age externe est active.

Hello tooachieve de façon plus simple est de ce type de configuration tooplace hello Max-Age externe et fonctionnalités de traitement d’en-tête expire hello dans hello même instruction.

Valeur|Résultat
--|--
Remplacer|Garantit que hello suivant actions aura lieu :<br/>-Remplace l’en-tête Expires généré par le serveur d’origine hello.<br/>-Ajoute l’en-tête Expires produit par la réponse de toohello fonctionnalité hello Max-Age externe.
Transmettre directement|Garantit que l’en-tête Expires produit par la fonctionnalité de Max-Age externe hello n’est jamais ajouté toohello réponse. <br/> Si le serveur d’origine hello génère un en-tête d’expiration, il passe par l’utilisateur final toohello. <br/>Cause hello réponse en-tête toonot peut contenir un en-tête d’expiration si le serveur d’origine hello ne produit pas un en-tête d’expiration, alors cette option.
Ajouter si manquant| Si un en-tête d’expiration n’a pas été reçu à partir du serveur d’origine hello, cette option ajoute l’en-tête Expires produit par la fonctionnalité de Max-Age externe hello. Cette option est utile pour s’assurer que toutes les ressources recevront un en-tête d’expiration.
Supprimer| Garantit qu’un en-tête d’expiration n’est pas inclus dans la réponse de l’en-tête hello. Si un en-tête d’expiration a déjà été attribué, il sera supprimé à partir de la réponse de l’en-tête hello.

**Comportement par défaut :** Remplacer

###<a name="external-max-age"></a>Âge maximal externe
**Objectif :** intervalle de max-age hello détermine de revalidation du cache de navigateur tooedge server. En d’autres termes, une nouvelle version d’une ressource à partir d’un serveur edge peut vérifier durée hello écoulées avant que d’un navigateur.

L’activation de cette fonctionnalité génère Cache-contrôle : max-age et expire en-têtes à partir de nos serveurs edge et envoyez-le toohello HTTP client. Par défaut, ces en-têtes remplace ceux créés par le serveur d’origine hello. Toutefois, le traitement d’en-tête Cache-Control et les fonctionnalités de traitement d’en-tête expiration peuvent être utilisé tooalter ce comportement.

Informations essentielles :

- Cette action n’affecte pas le nombre de revalidations du bord serveur tooorigin serveur du cache. Ces types de nombre de revalidations du sont déterminés par les en-têtes de Cache-contrôle/Expires provenant du serveur d’origine hello et peuvent être personnalisées avec la valeur par défaut interne Max-Age et les fonctionnalités de Force interne Max-Age.
- Configurer cette fonctionnalité en spécifiant une valeur entière et en sélectionnant hello au moment voulu unité (par exemple, secondes, minutes, heures, etc.).
- La valeur négative tooa fonctionnalité provoque notre toosend de serveurs edge un Cache-Control : no-cache et un temps d’expiration est défini dans hello passé avec chaque navigateur toohello de réponse. Bien qu’un client HTTP ne mettra pas en cache de réponse de hello, ce paramètre n’affectera pas réponse nos serveurs edge capacité toocache hello serveur d’origine hello.
- Unité de temps de paramètre hello trop « Off » désactive cette fonctionnalité. Les en-têtes de Cache-contrôle/Expires mis en cache avec la réponse hello du serveur d’origine hello passera via toohello navigateur.

**Comportement par défaut :** Désactivé

###<a name="force-internal-max-age"></a>Forcer l’âge maximal interne
**Objectif :** intervalle de max-age hello détermine de revalidation du cache de bord serveur tooorigin serveur. En d’autres termes, durée hello écoulées avant que d’un serveur edge peut vérifier si un élément mis en cache correspond à asset hello stocké sur le serveur d’origine hello.

Informations essentielles :

- Cette fonctionnalité sera remplacer l’intervalle de max-age hello défini dans le Cache-Control ou Expires les en-têtes générés à partir d’un serveur d’origine.
- Cette fonctionnalité n’affecte pas le nombre de revalidations du cache du serveur de tooedge navigateur. Ces types de nombre de revalidations du sont déterminés par le Cache-Control ou Expires en-têtes envoyés toohello navigateur.
- Cette fonctionnalité n’a pas d’effet observable sur réponse hello remis par un demandeur de toohello serveur edge. Toutefois, il peut avoir une incidence sur la quantité de hello de revalidation du trafic à partir de notre serveur d’origine toohello bord serveurs.
- Configurez cette fonctionnalité en :
    - Code d’état en sélectionnant hello pour lequel un max-age interne est appliqué.
    - En spécifiant une valeur entière et en sélectionnant hello unité de temps souhaitée (par exemple, secondes, minutes, heures, etc.). Cette valeur définit un intervalle de max-age hello la demande.

- Unité de temps de paramètre hello trop « Off » désactive cette fonctionnalité. Un intervalle de max-age interne ne sera pas attribué toorequested actifs. Si l’en-tête d’origine de hello ne contient pas d’instructions de mise en cache, puis les actifs hello sont mises en cache en fonction du paramètre actif de toohello dans la fonctionnalité par défaut interne Max-Age.
- En raison de la manière de toohello dans le cache, les paramètres sont suivies, cette fonctionnalité ne peut pas être associée à hello conditions de correspondance suivantes : 
    - Edge 
    - Cname
    - Littéral d’en-tête de requête
    - Caractère générique d’en-tête de requête
    - Méthode de requête
    - Littéral de requête d’URL
    - Caractère générique de requête d’URL

**Comportement par défaut :** Désactivé

###<a name="h264-support-http-progressive-download"></a>Prise en charge H.264 (téléchargement progressif HTTP)
**Objectif :** détermine les types de hello de H.264 formats de fichiers qui peuvent être utilisé toostream contenu.

Informations essentielles :

- Définissez un ensemble d’extensions de noms de fichier H.264 autorisées séparé par un espace dans l’option Extensions de fichier. L’option d’Extensions de fichier remplace le comportement par défaut de hello. Maintenez la prise en charge de MP4 et F4V en incluant ces extensions de noms de fichier lors de la définition de cette option. 
- Assurez-vous que tooinclude un délai lors de la spécification de chaque extension de nom de fichier (par exemple, .mp4 .f4v).

**Comportement par défaut :** Le téléchargement progressif HTTP prend en charge les formats multimédia MP4 et F4V par défaut.

###<a name="honor-no-cache-request"></a>Honorer la requête non-cache
**Objectif :** détermine si les demandes de cache non d’un client HTTP transférés toohello serveur d’origine.

Une demande non-cache se produit lorsque le client de hello HTTP envoie un Cache-Control : no-cache et/ou pragma : no-en-tête de cache dans une demande HTTP de hello.

Valeur|Résultat
--|--
Activé|Permet de demandes de cache d’un client HTTP non serveur d’origine toobe toohello transféré et serveur d’origine hello retournera les en-têtes de réponse hello et corps hello via le serveur de périphérie hello arrière toohello HTTP client.
Désactivé|Restaure le comportement par défaut de hello. comportement par défaut de Hello est demandes de cache non tooprevent d’être transféré toohello serveur d’origine.

Pour tout le trafic de production, il est vivement recommandé de tooleave cette fonctionnalité dans son état par défaut désactivé. Dans le cas contraire, seront de protéger les serveurs d’origine à partir des utilisateurs finaux qui peuvent déclencher par inadvertance de nombreuses demandes de cache non lors de l’actualisation des pages web ou à partir de hello nombreux lecteurs multimédias classiques sont codées toosend un en-tête no-cache avec chaque demande vidéo. Toutefois, cette fonctionnalité peut être mise en lots de tooapply utile toocertain hors production ou répertoires, les tests dans tooallow commande toobe de nouveau contenu extraite à la demande à partir du serveur d’origine hello.

état du cache Hello qui sera signalé pour une demande qui est autorisée serveur d’origine tooan toobe transféré en raison de la fonctionnalité de toothis est TCP_Client_Refresh_Miss. Le rapport des États de Cache, qui est disponible dans le module de création de rapports de base hello, fournit des informations statistiques à l’état du cache. Cela vous permet de nombre de hello tootrack et pourcentage de demandes de serveur d’origine tooan en raison de la fonctionnalité de toothis sont transférés.

**Comportement par défaut** : Désactivé.

###<a name="ignore-origin-no-cache"></a>Ignorer la requête non-cache d’origine
**Objectif :** détermine si notre CDN ignorera hello suivant les directives pris en charge à partir d’un serveur d’origine :

- Cache-Control: private
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

Informations essentielles :

- Configurer cette fonctionnalité en définissant une liste délimitée par l’espace des codes d’état pour lequel hello ci-dessus directives est ignorée.
- Hello ensemble de codes d’état valides pour cette fonctionnalité sont : 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 et 505.
- Désactiver cette fonctionnalité en lui affectant une valeur vide tooa.
- En raison de la manière de toohello dans le cache, les paramètres sont suivies, cette fonctionnalité ne peut pas être associée à hello conditions de correspondance suivantes : 
    - Edge 
    - Cname
    - Littéral d’en-tête de requête
    - Caractère générique d’en-tête de requête
    - Méthode de requête
    - Littéral de requête d’URL
    - Caractère générique de requête d’URL

**Comportement par défaut :** le comportement par défaut est hello toohonor au-dessus de directives.

###<a name="ignore-unsatisfiable-ranges"></a>Ignorer les plages inacceptables 
**Objectif :** détermine la réponse hello qui sera renvoyé tooclients lorsqu’une requête génère un code d’état 416 plage demandée non satisfaisante.

Par défaut, ce code d’état est retourné lorsque hello spécifié demande de plage d’octets ne peut pas être satisfaite par un serveur edge et un champ d’en-tête de demande If-Range n’a pas été spécifié.

Valeur|Résultat
-|-
Activé|Empêche nos serveurs bord à partir de la demande de plage d’octets non valide-tooan répond avec un code d’état 416 plage demandée non satisfaisante. À la place nos serveurs fournira asset demandée de hello et retourner une réponse 200 OK au client de hello.
Désactivé|Restaure le comportement par défaut de hello. comportement par défaut de Hello est toohonor le code d’état 416 plage demandée non satisfaisante.

**Comportement par défaut** : Désactivé.

###<a name="internal-max-stale"></a>Obsolescence maximale interne
**Objectif :** contrôle la durée pendant laquelle hello normal d’expiration temps une ressource mise en cache peut être pris en charge à partir d’un serveur edge lorsque le serveur de périphérie hello est impossible toorevalidate hello mis en cache actif avec le serveur d’origine hello.

Normalement, lors de l’expiration du délai de max-age d’un élément multimédia, serveur de périphérie hello enverra un serveur d’origine revalidation demande toohello. Hello serveur d’origine puis répondra avec l’option un 304 pas modifié pour permettre à serveur de périphérie hello un nouveau bail sur les ressources mises en cache hello, soit avec 200 OK pour fournir un serveur de périphérie hello avec une version mise à jour de ressource mise en cache de hello.

Si serveur de périphérie hello est impossible tooestablish une connexion avec le serveur d’origine hello lors de la revalidation de ce type, cette fonctionnalité périmée Max interne contrôle si et pour la durée pendant laquelle hello serveur edge peut continuer asset de tooserve hello désormais périmée.

Notez que cet intervalle de temps démarre lorsque max-age l’élément multimédia hello arrive à expiration, pas cas hello revalidation a échoué. Par conséquent, période de hello maximale pendant laquelle une ressource peut être traitée sans revalidation réussie est Montant hello de temps spécifié par la combinaison de hello de max-age plus périmée max. Par exemple, si une ressource a été mis en cache à 9 h 00, avec une durée max. de 30 minutes et périmée une maximum de 15 minutes, puis essayez de la revalidation a échoué à 9:44 entraînerait un utilisateur final réception hello obsolètes mis en cache actif, pendant une tentative de revalidation a échoué à 9:46 entraînerait réception d’une passerelle 504 l’utilisateur final Hello.

Toute valeur configurée pour cette fonctionnalité est remplacée par le Cache-contrôle : doit-revalider ou Cache-contrôle : proxy-revalider les en-têtes reçus à partir du serveur d’origine hello. Si un de ces en-têtes est reçu à partir du serveur d’origine hello lors de la mise en cache initialement un élément multimédia, serveur de périphérie hello ne servira pas une ressource mise en cache obsolète. Dans ce cas, si serveur edge de hello est toorevalidate impossible à l’origine de hello lors de l’intervalle de l’élément multimédia hello max-age a expiré, puis hello bord serveur retournera une passerelle 504.

Informations essentielles :

- Configurez cette fonctionnalité en :
    - Code d’état en sélectionnant hello pour lequel une max-obsolète est appliquée.
    - En spécifiant une valeur entière, puis en sélectionnant hello unité de temps souhaitée (par exemple, secondes, minutes, heures, etc.). Cette valeur définit hello interne max périmée qui est appliquée.

- Unité de temps de paramètre hello trop « Off » désactive cette fonctionnalité. Une ressource mise en cache ne sera pas traitée au-delà de son délai d’expiration normal.
- En raison de la manière de toohello dans le cache, les paramètres sont suivies, cette fonctionnalité ne peut pas être associée à hello conditions de correspondance suivantes : 
    - Edge 
    - Cname
    - Littéral d’en-tête de requête
    - Caractère générique d’en-tête de requête
    - Méthode de requête
    - Littéral de requête d’URL
    - Caractère générique de requête d’URL

**Comportement par défaut :** 2 minutes

###<a name="partial-cache-sharing"></a>Partage de cache partiel
**Objectif :** détermine si une requête peut générer du contenu partiellement mis en cache.

Ce cache partiels peut être puis de nouvelles demandes de toofulfill utilisé pour ce contenu jusqu'à ce que hello demandé est entièrement placé.

Valeur|Résultat
-|-
Activé|Les requêtes peuvent générer du contenu partiellement mis en cache.
Désactivé|Demandes peuvent uniquement générer un entièrement mis en cache la version de hello demandée de contenu.

**Comportement par défaut** : Désactivé.

###<a name="prevalidate-cached-content"></a>Prévalider le contenu mis en cache
**Objectif :** détermine si du contenu mis en cache peut faire l’objet d’une revalidation anticipée avant l’expiration de sa durée de vie.

Définir la durée hello expiration toohello préalable hello demandé TTL du contenu au cours de laquelle il sera éligible pour la revalidation anticipée.

Informations essentielles :

- En sélectionnant « Off » en tant qu’unité de temps hello de requiert sur place de revalidation tootake après l’expiration de la durée de vie du contenu hello mis en cache. Le temps ne doit pas être spécifié, et sera ignoré.

**Comportement par défaut :** Désactivé. Revalidation peut uniquement avoir lieu après hello la durée de vie du contenu mis en cache a expiré.

###<a name="refresh-zero-byte-cache-files"></a>Actualiser les fichiers de cache de zéro octet
**Objectif :** détermine la façon dont nos serveurs Edge gèrent la requête d’un client HTTP liée à une ressource de cache de 0 octet.

Les valeurs autorisées sont :

Valeur|Résultat
--|--
Activé|Provoque le bord serveur toore-extraction hello élément multimédia à partir du serveur d’origine hello.
Désactivé|Restaure le comportement par défaut de hello. comportement par défaut de Hello est tooserve des ressources de cache valide à la demande.
Cette fonctionnalité n’est pas requise pour la mise en cache correcte et la distribution de contenu, mais peut être utile comme solution de contournement. Par exemple, les générateurs de contenu dynamiques sur les serveurs d’origine peuvent entraîner par inadvertance des réponses de 0 octet envoyés toohello les serveurs de périphérie. Ces types de réponses sont généralement mis en cache par nos serveurs Edge. Si vous savez qu’une réponse de 0 octet n’est jamais une réponse valide 

Pour ce type de contenu, puis cette fonctionnalité peut empêcher ces types d’éléments multimédias servies tooyour clients.

**Comportement par défaut** : Désactivé.

###<a name="set-cacheable-status-codes"></a>Définir les codes d’état pouvant être mis en cache
**Objectif :** définit ensemble hello des codes d’état qui peuvent entraîner de contenu mis en cache.

Par défaut, la mise en cache est uniquement activée pour les réponses 200 OK.

Définir un ensemble délimitées hello souhaitée des codes d’état.

Informations essentielles :

- Activez également la fonctionnalité Ignorer la requête non-cache d’origine. Si cette fonctionnalité n’est pas activée, les réponses non 200 OK ne peuvent pas être mises en cache.
- Hello ensemble de codes d’état valides pour cette fonctionnalité sont : 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 et 505.
- Cette fonctionnalité ne peut pas être utilisé toodisable mise en cache pour les réponses qui génèrent un code d’état OK 200.

**Comportement par défaut :** la mise en cache est activée uniquement pour les réponses qui génèrent un code d’état 200 OK.
###<a name="stale-content-delivery-on-error"></a>Rendre obsolète la remise de contenu en cas d’erreur
**Objectif :** 

Détermine si expiré contenu mis en cache est envoyée lorsqu’une erreur se produit lors de la revalidation du cache ou hello lors de la récupération a demandé le contenu à partir du serveur d’origine hello client.

Valeur|Résultat
-|-
Activé|Contenu obsolète sera pris en charge toohello demandeur lorsqu’une erreur se produit pendant un serveur d’origine tooan connexion.
Désactivé|Erreur du serveur d’origine Hello est transféré toohello demandeur.

**Comportement par défaut :** Désactivé

###<a name="stale-while-revalidate"></a>Rendre obsolète pendant la revalidation
**Objectif :** améliore les performances en permettant à nos serveurs edge tooserve toohello contenu obsolète demandeur lors de la revalidation a lieu.

Informations essentielles :

- comportement de Hello de cette fonctionnalité varie en fonction unité de temps sélectionnée toohello.
    - **Unité de temps :** spécifier une période de temps et sélectionnez une unité (par exemple, secondes, Minutes, heures, etc.) tooallow obsolètes contenu livraisons. Ce type d’installation permet hello CDN tooextend hello de durée pendant laquelle elle peut fournir le contenu avant de demander une validation selon la formule suivante de toohello :**TTL** + **temps obsolètes alors que revalider** 
    - **OFF :** sélectionner « Off » revalidation toorequire avant une demande de contenu obsolète peut être pris en charge.
        - Ne spécifiez pas de durée, car elle est inapplicable et sera ignorée.

**Comportement par défaut :** Désactivé. Revalidation doit intervenir avant que hello demandé de contenu peut être pris en charge.

###<a name="comment"></a>Commentaire
**Objectif :** permet un toobe Remarque ajoutée au sein d’une règle.

Une utilisation de cette fonctionnalité est tooprovide plus d’informations sur l’usage général de hello d’une règle ou pourquoi un particulier correspond à la condition ou une fonctionnalité a été ajoutée toohello règle.

Informations essentielles :

- Vous pouvez spécifier un maximum de 150 caractères.
- Assurez-vous que tooonly utilisez des caractères alphanumériques.
- Cette fonctionnalité n’affecte pas le comportement de hello de règle de hello. Il sert simplement de tooprovide une zone où vous pouvez fournir des informations pour référence ultérieure, ou qui peut-être aider lors du dépannage de la règle de hello.
 
## <a name="headers"></a>headers

Ces fonctionnalités sont conçue tooadd, modifier ou supprimer des en-têtes de hello demande ou réponse.

Nom | Objectif
-----|--------
En-tête de réponse Age | Détermine si un en-tête de réponse âge est inclus dans la réponse hello envoyé toohello demandeur.
En-têtes de réponse de cache de débogage | Détermine si une réponse peut inclure des en-tête de réponse X-EC-Debug hello qui fournit des informations sur la stratégie de cache hello pour un composant requis de hello.
Modifier l’en-tête de requête client | Remplace, complète ou supprime un en-tête dans une requête.
Modifier l’en-tête de réponse client | Remplace, complète ou supprime un en-tête dans une réponse.
Définir un en-tête personnalisé d’adresse IP client | Permet de toobe toohello ajouté demande adresse hello du client qui demande hello comme un en-tête de requête personnalisée.

###<a name="age-response-header"></a>En-tête de réponse Age
**Objectif**: détermine si un en-tête de réponse âge est inclus dans hello réponse envoyée toohello demandeur.
Valeur|Résultat
--|--
Activé | en-tête de réponse d’âge Hello figurera dans la réponse hello envoyé toohello demandeur.
Désactivé | en-tête de réponse d’âge Hello est exclu de la réponse hello envoyé toohello demandeur.

**Comportement par défaut :** Désactivé.

###<a name="debug-cache-response-headers"></a>En-têtes de réponse de cache de débogage
**Objectif :** détermine si une réponse peut inclure l’en-tête de réponse X-EC-Debug qui fournit des informations sur la stratégie de cache hello pour un composant requis de hello.

Déboguer la réponse du cache en-têtes seront incluses dans la réponse de hello lorsque les deux éléments suivants de hello sont vraies :

- Hello fonctionnalité des en-têtes de réponse du Cache de débogage a été activée sur la demande souhaitée de hello.
- Hello ci-dessus demande définit ensemble hello debug du cache d’en-têtes de réponse qui seront inclus dans la réponse de hello.

Déboguer la réponse du cache en-têtes peuvent être demandées en insérant hello suivant l’en-tête et hello directives souhaités dans la demande hello :

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**Exemple :**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Valeur|Résultat
-|-
Activé|Les requêtes des en-têtes de réponse de cache de débogage renvoient une réponse qui inclut l’en-tête X-EC-Debug.
Désactivé|L’en-tête de réponse X-EC-Debug est exclu de la réponse de hello.

**Comportement par défaut** : Désactivé.

###<a name="modify-client-response-header"></a>Modifier l’en-tête de réponse client
**Objectif :** chaque requête contient un ensemble d’[en-têtes de requête]() qui le décrivent. Cette fonctionnalité peut soit :

- Ajouter ou remplacer la valeur hello affecté l’en-tête de demande tooa. Si l’en-tête de demande spécifié hello n’existe pas, cette fonctionnalité sera ajoutez-la toohello demande.
- Supprimer un en-tête de demande de requête de hello.

Les demandes qui sont transférés de serveur d’origine tooan reflète hello apportées par cette fonctionnalité.

Un des hello suit les actions peut être effectué sur un en-tête de demande :

Option|Description|Exemple
-|-|-
Append|Hello spécifié la valeur sera ajoutée toend de valeur d’en-tête de demande existante hello.|**Valeur d’en-tête de requête (Client) :**Value1 <br/> **Valeur d’en-tête de requête (moteur de règles HTTP) :** Value2 <br/>**Nouvelle valeur d’en-tête de requête :** Value1Value2
Remplacer|demande Hello valeur d’en-tête seront toohello de l’ensemble spécifié de valeur.|**Valeur d’en-tête de requête (Client) :**Value1 <br/>**Valeur d’en-tête de requête (moteur de règles HTTP) :** Value2 <br/>**Nouvelle valeur d’en-tête de requête :** Value2 <br/>
Supprimer|Supprime l’en-tête de demande spécifié hello.|**Valeur d’en-tête de requête (Client) :**Value1 <br/> **Modifier la configuration de l’en-tête de demande Client :** Delete hello en-tête de la demande en question. <br/>**Résultat :** hello spécifié d’en-tête de demande n’est pas transférée toohello serveur d’origine.

Informations essentielles :

- Assurez-vous que valeur hello spécifiée dans l’option de nom est une correspondance exacte pour l’en-tête de demande souhaitée hello.
- Cas n’est pas pris en compte à des fins de hello d’identification d’un en-tête. Par exemple, tous hello suivant des variations du nom d’en-tête Cache-Control peuvent être utilisé tooidentify il :
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Assurez-vous que tooonly utiliser des caractères alphanumériques, des tirets ou des traits de soulignement lorsque vous spécifiez un nom d’en-tête.
- Suppression d’un en-tête de l’empêcher d’être transféré tooan serveur d’origine par nos serveurs edge.
- Hello en-têtes suivants sont réservés et ne peut pas être modifiées par cette fonctionnalité :
    - forwarded
    - host
    - via
    - Avertissement
    - x-forwarded-for
    - Tous les noms d’en-tête commençant par « x-ec » sont réservés.

###<a name="modify-client-response-header"></a>Modifier l’en-tête de réponse client
Chaque réponse contient un ensemble d’[en-têtes de réponse]() qui la décrivent. Cette fonctionnalité peut soit :

- Ajouter ou remplacer la valeur hello affecté l’en-tête de réponse tooa. Si l’en-tête de demande spécifié hello n’existe pas, cette fonctionnalité sera ajoutez-la toohello réponse.
- Supprimer un en-tête de réponse à partir de la réponse de hello.

Par défaut, les valeurs d’en-tête de réponse sont définies par un serveur d’origine et par nos serveurs Edge.

Un des hello suit les actions peut être effectué sur un en-tête de réponse :

Option|Description|Exemple
-|-|-
Append|Hello spécifié la valeur sera ajoutée toend de valeur d’en-tête de demande existante hello.|**Valeur d’en-tête de réponse (Client) :**Value1 <br/> **Valeur d’en-tête de réponse (moteur de règles HTTP) :** Value2 <br/>**Nouvelle valeur d’en-tête de réponse :** Value1Value2
Remplacer|demande Hello valeur d’en-tête seront toohello de l’ensemble spécifié de valeur.|**Valeur d’en-tête de réponse (Client) :**Value1 <br/>**Valeur d’en-tête de réponse (moteur de règles HTTP) :** Value2 <br/>**Nouvelle valeur d’en-tête de réponse :** Value2 <br/>
Supprimer|Supprime l’en-tête de demande spécifié hello.|**Valeur d’en-tête de requête (Client) :**Value1 <br/> **Modifier la configuration de l’en-tête de demande Client :** en-tête de réponse Delete hello en question. <br/>**Résultat :** hello spécifié d’en-tête de réponse n’est pas transféré toohello demandeur.

Informations essentielles :

- Assurez-vous que valeur hello spécifiée dans l’option de nom est une correspondance exacte pour l’en-tête de réponse souhaitée hello. 
- Cas n’est pas pris en compte à des fins de hello d’identification d’un en-tête. Par exemple, tous hello suivant des variations du nom d’en-tête Cache-Control peuvent être utilisé tooidentify il :
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Suppression d’un en-tête de l’empêcher d’être transféré toohello demandeur.
- Hello en-têtes suivants sont réservés et ne peut pas être modifiées par cette fonctionnalité :
    - accept-encoding
    - age
    - connection
    - content-encoding
    - content-length
    - content-range
    - date
    - Serveur
    - trailer
    - transfer-encoding
    - mettre à niveau
    - vary
    - via
    - Avertissement
    - Tous les noms d’en-tête commençant par « x-ec » sont réservés.

###<a name="set-client-ip-custom-header"></a>Définir un en-tête personnalisé d’adresse IP client
**Objectif :** ajoute un en-tête personnalisé qui identifie le client demande hello par demande de toohello d’adresse IP.

L’option de nom de l’en-tête définit le nom hello hello personnalisé des en-têtes de demande où adresse IP du client hello sera stocké.

Cette fonctionnalité permet à un client toofind de serveur d’origine des adresses IP du client via un en-tête de requête personnalisée. Si la demande de hello est pris en charge à partir du cache, serveur d’origine hello pas informé de l’adresse IP du client hello. Par conséquent, il est recommandé que cette fonctionnalité soit utilisée avec ADN ou les ressources qui ne sont pas mises en cache.

Assurez-vous que ce nom d’en-tête spécifié hello ne correspond pas à hello suivants :

- Noms d’en-tête de requête standard. Vous trouverez une liste de noms d’en-tête standard dans [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Noms d’en-tête réservés :
    - forwarded-for
    - host
    - vary
    - via
    - Avertissement
    - x-forwarded-for
    - Tous les noms d’en-tête commençant par « x-ec » sont réservés.
 
## <a name="logs"></a>Journaux

Ces fonctionnalités sont des données de hello toocustomize conçue stockées dans les fichiers de journal brut.

Nom | Objectif
-----|--------
Champ de fichier journal personnalisé 1 | Détermine le format de hello et contenu hello qui sera assigné toohello personnalisé champ du journal dans un fichier journal brut.
Journaliser la chaîne de requête | Détermine si une chaîne de requête est stockée avec l’URL de hello dans les journaux d’accès.

###<a name="custom-log-field-1"></a>Champ de fichier journal personnalisé 1
**Objectif :** détermine le format de hello et contenu hello qui sera assigné toohello personnalisé champ du journal dans un fichier journal brut.

objectif principal de Hello derrière ce champ personnalisé est tooallow toodetermine les valeurs d’en-tête de demande et de réponse seront stockées dans vos fichiers journaux.

Par défaut, le champ de journal personnalisée hello est appelé « x-ec_custom-1 ». Toutefois, le nom hello de ce champ peut être personnalisée depuis la [page des paramètres de journal brut]().

Hello mise en forme que vous devez utiliser des en-têtes de demande et de réponse toospecify est définie ci-dessous.

Type d’en-tête|Format|Exemples
-|-|-
En-tête de requête|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
En-tête de réponse|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

Informations essentielles :

- Un champ de fichier journal personnalisé peut contenir n’importe quelle combinaison de champs d’en-tête et de texte brut.
- Les caractères valides pour ce champ sont les suivantes de hello : alphanumériques (par exemple, 0-9, a-z et A-Z), des tirets, deux-points, points-virgules, apostrophes, des virgules, des points, des traits de soulignement, signes égal, entre parenthèses, crochets et des espaces. Hello symbole de pourcentage et des accolades sont uniquement autorisées lorsque utilisé toospecify un champ d’en-tête.
- orthographe Hello pour chaque champ d’en-tête spécifié doit correspondre au nom d’en-tête de demande/réponse souhaitée de hello.
- Si vous souhaitez que toospecify plusieurs en-têtes, il est recommandé d’utiliser un séparateur tooindicate chaque en-tête. Par exemple, vous pouvez utiliser une abréviation pour chaque en-tête. Un exemple de syntaxe est fourni ci-dessous.
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**Valeur par défaut :** -

###<a name="log-query-string"></a>Journaliser la chaîne de requête
**Objectif :** détermine si une chaîne de requête est stockée avec l’URL de hello dans les journaux d’accès.

Valeur|Résultat
-|-
Activé|Permet le stockage hello des chaînes de requête lors de l’enregistrement des URL dans un journal d’accès. Si une URL ne contient pas de chaîne de requête, cette option n’aura pas d’effet.
Désactivé|Restaure le comportement par défaut de hello. comportement par défaut de Hello est tooignore les chaînes de requête lors de l’enregistrement des URL dans un journal d’accès.

**Comportement par défaut** : Désactivé.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Origine

Ces fonctionnalités sont conçue toocontrol comment hello CDN communique avec un serveur d’origine.

Nom | Objectif
-----|--------
Nombre maximal de requêtes toujours actives | Définit le nombre maximal de hello de requêtes pour une connexion persistante avant sa fermeture.
En-têtes spéciaux de proxy | Définit le jeu hello CDN spécifiques des en-têtes de demande qui est transféré à partir d’un serveur d’origine edge server tooan.


###<a name="maximum-keep-alive-requests"></a>Nombre maximal de requêtes toujours actives
**Objectif :** définit le nombre maximal de hello de requêtes pour une connexion persistante avant sa fermeture.

La définition hello le nombre maximal de valeur inférieure de demandes tooa est fortement déconseillée et peut entraîner une dégradation des performances.

Informations essentielles :

- Spécifiez cette valeur sous forme d’entier.
- Hello spécifié n’incluent pas des virgules ou des périodes de valeur.

**Valeur par défaut :** 10 000 requêtes

###<a name="proxy-special-headers"></a>En-têtes spéciaux de proxy
**Objectif :** définit ensemble hello de [les en-têtes de demande spécifique CDN]() qui est transféré à partir d’un serveur d’origine edge server tooan.

Informations essentielles :

- Chaque en-tête de demande CDN spécifiques défini dans cette fonctionnalité sera transféré tooan serveur d’origine.
- Un en-tête de demande spécifique CDN empêcher le transfert tooan serveur d’origine en le supprimant de la liste.

**Comportement par défaut :** tous les [les en-têtes de demande spécifique CDN]() sera transféré toohello serveur d’origine.

## <a name="specialty"></a>Spécialité

Ces fonctionnalités sont des fonctionnalités avancées que seuls les utilisateurs expérimentés doivent utiliser.

Nom | Objectif
-----|--------
Méthodes HTTP pouvant être mises en cache | Détermine le jeu hello des méthodes HTTP supplémentaires qui peuvent être mis en cache sur le réseau.
Taille de corps de requête pouvant être mise en cache | Définit le seuil de hello pour déterminer si une réponse de la publication peut être mis en cache.

###<a name="cacheable-http-methods"></a>Méthodes HTTP pouvant être mises en cache
**Objectif :** hello détermine de méthodes HTTP supplémentaires qui peuvent être mis en cache sur notre réseau.

Informations essentielles :

- Cette fonction suppose que les réponses GET soient toujours mises en cache. Par conséquent, hello méthode HTTP GET ne doit pas être inclus lors de la définition de cette fonctionnalité.
- Cette fonctionnalité prend uniquement en charge la méthode POST HTTP de hello. Activez la mise en cache de réponse POST en définissant cette fonctionnalité sur : POST 
- Par défaut, seules les requêtes dont le corps est inférieur à 14 Ko seront mises en cache. Utilisez la fonction de la taille du corps de demande pouvant être pour définir la taille du corps de demande maximale hello.

**Comportement par défaut :** seules les réponses GET sont mises en cache.

###<a name="cacheable-request-body-size"></a>Taille de corps de requête pouvant être mise en cache

**Objectif :** seuil de hello définit pour déterminer si une réponse de la publication peut être mis en cache.

Ce seuil est déterminé par la définition d’une taille de corps de requête maximale. Les requêtes qui contiennent un corps de requête plus large ne sont pas mises en cache.

Informations essentielles :

- Cette fonctionnalité n’est applicable que lorsque les réponses POST peuvent prétendre à la mise en cache. Hello pouvant être fonctionnalité de méthodes HTTP permet d’activer la mise en cache de demande POST.
- corps de la demande Hello est pris en considération pour :
    - les valeurs x-www-form-urlencoded
    - Garantir une clé de cache unique
- La définition d’une taille de corps de requête maximale peut affecter les performances de diffusion de données.
    - **Valeur recommandée :** 14 Ko
    - **Valeur minimale :** 1 Ko

**Comportement par défaut :** 14 ko
 
## <a name="url"></a>URL

Ces fonctionnalités permettent une toobe demande redirigée ou réécrit tooa autre URL.

Nom | Objectif
-----|--------
Suivre les redirections | Détermine si les demandes peuvent être nom d’hôte toohello redirigé défini dans l’en-tête d’emplacement hello retourné par un serveur d’origine client.
Redirection d'URL | Redirige les demandes via l’en-tête d’emplacement hello.
Réécriture d’URL  | Réécrit l’URL de demande hello.

###<a name="follow-redirects"></a>Suivre les redirections
**Objectif :** détermine si les demandes peuvent être nom d’hôte toohello redirigé défini dans l’en-tête d’emplacement retourné par un serveur d’origine client.

Informations essentielles :

- Demandes ne peuvent être redirigé tooedge CNAME correspondant toohello même plateforme.

Valeur|Résultat
-|-
Activé|Les requêtes peuvent être redirigées.
Désactivé|Les requêtes ne seront pas redirigées.

**Comportement par défaut** : Désactivé.
###<a name="url-redirect"></a>Redirection d'URL
**Objectif :** redirige les requêtes via l’en-tête Location.

configuration de Hello de cette fonctionnalité requiert la configuration de hello options suivantes :

Option|Description
-|-
Code|Sélectionnez le code de réponse hello qui sera renvoyé toohello demandeur.
Source et modèle| Ces paramètres définissent un modèle d’URI de demande qui identifie le type de hello de demandes qui peuvent être redirigé. Seules les demandes dont l’URL est conforme aux deux hello suivant des critères s’affichera : <br/> <br/> **Source :** (ou point d’accès au contenu) Sélectionnez un chemin d’accès relatif qui identifie un serveur d’origine. Il s’agit section de « /XXXX/ » hello et votre nom de point de terminaison. <br/> **Source (modèle) :** Un modèle qui identifie les requêtes via un chemin d’accès relatif doit être défini. Ce modèle d’expression régulière doit définir un chemin d’accès qui commence directement après que hello sélectionné précédemment point d’accès au contenu (voir ci-dessus). <br/> -Vérifiez que les critères d’URI de demande hello (c'est-à-dire Source & modèle) défini ci-dessus ne sont en conflit avec les conditions de correspondance définies pour cette fonctionnalité. <br/> -Veillez à que toospecify un modèle. À l’aide d’une valeur vide en tant que modèle de hello correspondra uniquement dossier racine toohello des demandes du serveur d’origine sélectionné hello (par exemple, http://cdn.mydomain.com/).
Destination| Définir l’URL de hello hello toowhich au-dessus de demandes est redirigée. <br/> Construisez dynamiquement cette URL à l’aide des éléments suivants : <br/> - Un modèle d’expression régulière <br/>- Des variables HTTP <br/> Remplacer les valeurs hello capturées dans le modèle de source de hello dans le modèle de destination hello à l’aide de $ _n_  où  _n_  identifie une valeur par la commande hello dans lequel il a été capturé. Par exemple, $1 représente hello première valeur capturée dans le modèle de source de hello, tandis que $2 représente la valeur de seconde hello. <br/> 
Il est vivement recommandé de toouse une URL absolue. Utilisez Hello d’une URL relative peut rediriger le chemin d’accès au CDN URL tooan non valide.

**Exemple de scénario**

Dans cet exemple, nous allons vous montrer comment tooredirect un bord URL CNAME qui résout toothis base URL du CDN : http://marketing.azureedge.net/brochures

Qualification des demandes sera redirigé toothis arête CNAME URL : http://cdn.mydomain.com/resources

Cette redirection d’URL peut être obtenue via hello configuration suivante :![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Points essentiels :**

- fonctionnalité de redirection d’URL de Hello définit hello URL seront redirigés de la requête. Par conséquent, aucune condition de correspondance supplémentaire n’est requise. Bien que la condition de correspondance hello a été définie en tant que « Toujours », ne demande que toohello point « brochures « dossier sur l’origine de client hello « marketing » sera redirigé. 
- Toutes les demandes correspondants sera bord toohello redirigé que CNAME URL définie dans l’option de Destination. 
    - Exemple de scénario n°1 : 
        - Exemple de requête (URL CDN) : http://marketing.azureedge.net/brochures/widgets.pdf 
        - URL de requête (après redirection) : http://cdn.mydomain.com/resources/widgets.pdf  
    - Exemple de scénario n°2 : 
        - Exemple de requête (URL CNAME Edge) : http://marketing.mydomain.com/brochures/widgets.pdf 
        - URL de requête (après redirection) : http://cdn.mydomain.com/resources/widgets.pdf  Exemple de scénario
    - Exemple de scénario n°3 : 
        - Exemple de requête (URL CNAME Edge) : http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - URL de requête (après redirection) : http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- variable de demande de schéma (% {schéma}) Hello a été utilisé dans l’option de Destination. Cela garantit que le schéma de cette demande hello reste inchangé après la redirection.
- les segments d’URL Hello qui ont été capturés à partir de la demande de hello sont toohello ajouté une nouvelle URL via « $1. »
 
###<a name="url-rewrite"></a>Réécriture d’URL
**Objectif :** réécrit l’URL de demande hello.

Informations essentielles :

- configuration de Hello de cette fonctionnalité requiert la configuration de hello options suivantes :

Option|Description
-|-
 Source et modèle | Ces paramètres définissent un modèle d’URI de demande qui identifie le type de hello de demandes qui peuvent être réécrites. Seules les demandes dont l’URL est conforme aux deux hello suivant des critères seront réécrites : <br/>     - **Source (ou point d’accès au contenu) :** sélectionnez un chemin d’accès relatif qui identifie un serveur d’origine. Il s’agit section de « /XXXX/ » hello et votre nom de point de terminaison. <br/> - **Source (modèle) :** un modèle qui identifie les requêtes via un chemin d’accès relatif doit être défini. Ce modèle d’expression régulière doit définir un chemin d’accès qui commence directement après que hello sélectionné précédemment point d’accès au contenu (voir ci-dessus). <br/> Vérifiez que hello demande URI critères (par exemple, modèle de & Source) définis ci-dessus ne sont en conflit avec une des conditions de correspondance hello définies pour cette fonctionnalité. Assurez-vous que toospecify un modèle. À l’aide d’une valeur vide en tant que modèle de hello correspondra uniquement dossier racine toohello des demandes du serveur d’origine sélectionné hello (par exemple, http://cdn.mydomain.com/). 
 Destination  |Définir l’URL relative de hello copiera hello toowhich au-dessus de demandes par : <br/>    1. Sélectionnant un point d’accès au contenu qui identifie un serveur d’origine. <br/>    2. Définissant un chemin d’accès relatif à l’aide des éléments suivants : <br/>        - Un modèle d’expression régulière <br/>        - Des variables HTTP <br/> <br/> Remplacer les valeurs hello capturées dans le modèle de source de hello dans le modèle de destination hello à l’aide de $ _n_  où  _n_  identifie une valeur par la commande hello dans lequel il a été capturé. Par exemple, $1 représente hello première valeur capturée dans le modèle de source de hello, tandis que $2 représente la valeur de seconde hello. 
 Cette fonctionnalité permet à nos serveurs edge toorewrite hello URL sans effectuer une redirection traditionnelle. Cela signifie que demandeur hello recevra hello même réponse de code comme si l’URL de hello réécrite avait été demandée.

**Exemple de scénario nº 1**

Dans cet exemple, nous allons vous montrer comment tooredirect un bord URL CNAME qui résout toothis base URL du CDN : http://marketing.azureedge.net/brochures/

Qualification des demandes sera redirigé toothis arête CNAME URL : http://MyOrigin.azureedge.net/resources/

Cette redirection d’URL peut être obtenue via hello configuration suivante :![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Exemple de scénario nº 2**

Dans cet exemple, nous allons vous montrer comment tooredirect un bord CNAME URL à partir de toolowercase en majuscules à l’aide d’expressions régulières.

Cette redirection d’URL peut être obtenue via hello configuration suivante :![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Points essentiels :**

- fonctionnalité de réécriture d’URL Hello définit hello URL seront réécrites de la requête. Par conséquent, aucune condition de correspondance supplémentaire n’est requise. Bien que la condition de correspondance hello a été définie en tant que « Toujours », ne demande que toohello point « brochures » copiera dossier sur l’origine de client hello « marketing ».

- les segments d’URL Hello qui ont été capturés à partir de la demande de hello sont toohello ajouté une nouvelle URL via « $1. »



###<a name="compatibility"></a>Compatibilité

Cette fonctionnalité inclut correspondant aux critères qui doivent être remplies avant de pouvoir être appliquées tooa demande. Dans la définition de commande tooprevent des critères de correspondance en conflit, cette fonctionnalité est incompatible avec hello conditions de correspondance suivantes :

- Numéro AS
- Origine CDN
- Adresse IP du client
- Origine client
- Modèle de requête
- Répertoire du chemin d’URL
- Extension du chemin d’URL
- Nom de fichier du chemin d’URL
- Littéral du chemin d’URL
- Expression régulière du chemin d’URL
- Caractère générique du chemin d’URL
- Littéral de requête d’URL
- Paramètre de requête d’URL
- Expression régulière de requête d’URL
- Caractère générique de requête d’URL


## <a name="next-steps"></a>Étapes suivantes
* [Référence du moteur de règles](cdn-rules-engine-reference.md)
* [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-conditional-expressions.md)
* [Conditions de correspondance du moteur de règles](cdn-rules-engine-reference-match-conditions.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
