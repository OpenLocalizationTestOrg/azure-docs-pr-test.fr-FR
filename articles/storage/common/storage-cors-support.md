---
title: prise en charge du partage (CORS) aaaCross-Origin Resource | Documents Microsoft
description: "Découvrez comment tooenable CORS prennent en charge pour hello Services de stockage Microsoft Azure."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Prise en charge de partage de ressources Cross-Origin (CORS) pour hello Services de stockage Azure
Depuis la version 2013-08-15, les services de stockage Azure hello prend en charge de partage de ressources Cross-Origin (CORS) pour les services Blob, Table, file d’attente et de fichier hello. CORS est une fonctionnalité HTTP qui permet à une application web en cours d’exécution ressources de tooaccess sous un domaine dans un autre domaine. Navigateurs Web implémentent une restriction de sécurité appelée [stratégie de même origine](http://www.w3.org/Security/wiki/Same_Origin_Policy) qui empêche une page web d’appeler des API dans un autre domaine. CORS constitue un un domaine de manière sécurisée tooallow (domaine d’origine hello) toocall API dans un autre domaine. Consultez hello [spécification CORS](http://www.w3.org/TR/cors/) pour plus d’informations sur CORS.

Vous pouvez définir les règles CORS individuellement pour chacun des hello services de stockage, en appelant [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [définir les propriétés de Service de file d’attente](https://msdn.microsoft.com/library/hh452232.aspx), et [Set Table Service Properties](https://msdn.microsoft.com/library/hh452240.aspx). Une fois que vous définissez les règles CORS hello pour le service de hello, une demande authentifiée effectuée au service de hello à partir d’un autre domaine sera évaluée toodetermine si elle est autorisée selon les règles de toohello que vous avez spécifié.

> [!NOTE]
> Notez que CORS n'est pas un mécanisme d'authentification. Toute demande adressée à une ressource de stockage lorsque CORS est activé doit avoir une signature d'authentification appropriée ou doit être exécutée sur une ressource publique.
> 
> 

## <a name="understanding-cors-requests"></a>Présentation des demandes CORS
Une demande CORS d'un domaine d'origine peut comprendre deux demandes distinctes :

* Une demande préliminaire, qui interroge hello CORS imposées par le service de hello. demande préliminaire de Hello est requis, sauf si la méthode de demande hello est un [méthode simple](http://www.w3.org/TR/cors/), ce qui signifie GET, HEAD ou POST.
* demande réelle de Hello, effectuée par rapport à la ressource de hello souhaité.

### <a name="preflight-request"></a>Demande préliminaire
requêtes de demande préliminaire Hello hello restrictions CORS qui ont été établies pour le service de stockage hello par propriétaire du compte hello. navigateur Hello (ou tout autre agent utilisateur) envoie une demande OPTIONS qui inclut les en-têtes de demande hello, domaine de méthode et d’origine. service de stockage Hello évalue opération hello conçue selon un ensemble préconfiguré de règles CORS qui spécifient les domaines d’origine, de méthodes de demande et en-têtes de demande peuvent être spécifiés dans une demande réelle sur une ressource de stockage.

Si les règles CORS sont activées pour le service de hello et il existe une règle CORS qui correspond à la demande préliminaire de hello, hello service répond avec le code d’état 200 (OK) et inclut les en-têtes de contrôle d’accès hello requis dans la réponse de hello.

Si CORS n’est pas activée pour le service de hello ou aucune règle CORS correspond à la demande préliminaire de hello, service de hello répond avec le code d’état 403 (interdit).

Si la demande OPTIONS ne contient pas de hello hello en-têtes CORS requis (hello d’origine et les en-têtes Access-Control-Request-Method), service de hello répond avec le code d’état 400 (demande incorrecte).

Notez qu’une demande préliminaire est évaluée par rapport à service hello (Blob, file d’attente et Table) et non sur hello la ressource demandée. propriétaire du compte Hello doit avoir activé des CORS dans le cadre des propriétés de service de compte hello dans l’ordre pour hello demande toosucceed.

### <a name="actual-request"></a>Demande réelle
Une fois la demande préliminaire de hello est accepté et hello réponse est renvoyée, hello navigateur distribue demande réelle de hello par rapport à la ressource de stockage hello. navigateur de Hello refuse la demande réelle de hello immédiatement si hello demande préliminaire est rejetée.

demande réelle de Hello est traité comme une demande normale dans le service de stockage hello. présence de Hello d’en-tête d’origine hello indique que la demande de hello est une demande CORS et hello vérifie hello CORS règles de correspondance. Si une correspondance est trouvée, les en-têtes de hello de contrôle d’accès sont ajoutés toohello réponse et envoyé arrière toohello client. Si une correspondance est introuvable, les en-têtes Access-Control CORS hello ne sont pas retournés.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>L’activation de CORS pour les services de stockage Azure hello
Les règles CORS sont définies au niveau de service hello, donc vous devez tooenable ou désactivez les CORS pour chaque service (Blob, file d’attente et Table) séparément. Par défaut, CORS est désactivé pour tous les services. tooenable CORS, vous avez besoin de propriétés de service appropriée de hello tooset à l’aide de la version 2013-08-15 ou version ultérieure et ajouter des propriétés du service toohello de règles CORS. Pour plus d’informations sur la façon tooenable ou désactiver les CORS pour un service et comment tooset CORS règles, veuillez consultez trop[Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [définir les propriétés de Service de file d’attente](https://msdn.microsoft.com/library/hh452232.aspx), et [définir une Table Propriétés du service](https://msdn.microsoft.com/library/hh452240.aspx).

Voici un exemple de règle CORS spécifiée via une opération Set Service Properties :

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Chaque élément inclus dans la règle de hello CORS est décrit ci-dessous :

* **AllowedOrigins**: domaines d’origine hello autorisés toomake une demande de stockage de hello service via CORS. domaine d’origine Hello est hello à partir de quels hello provient la demande. Notez que les origine hello doivent être une correspondance qui respecte la casse exacte avec origine hello que durée de vie hello utilisateur envoie toohello service. Vous pouvez également utiliser le caractère générique de hello ' *' tooallow toutes les demandes de toomake domaines origin via CORS. Dans l’exemple hello ci-dessus, hello domaines [http://www.contoso.com](http://www.contoso.com) et [http://www.fabrikam.com](http://www.fabrikam.com) peut effectuer des demandes aux services hello à l’aide de CORS.
* **AllowedMethods**: méthodes de hello (verbes de requête HTTP) que le domaine d’origine hello peut utiliser pour une demande CORS. Dans l’exemple hello ci-dessus, seules les demandes PUT et GET sont autorisées.
* **AllowedHeaders**: en-têtes de demande hello ce domaine d’origine hello peut spécifier à la demande CORS hello. Dans l’exemple hello ci-dessus, tous les en-têtes de métadonnées commençant par x-ms-meta-data, x-ms-meta-cible et x-ms-meta-abc sont autorisées. Notez que caractère générique de hello ' *' indique que les en-têtes commençant par hello spécifié est autorisé.
* **ExposedHeaders**: hello des en-têtes de réponse qui peuvent être envoyés dans la demande de hello réponse toohello CORS et exposés par l’émetteur de la demande hello navigateur toohello. Dans l’exemple hello situé au-dessus, hello est demandé tooexpose les en-têtes commençant par x-ms-meta.
* **MaxAgeInSeconds**: hello durée maximale pendant qu’un navigateur doit mettre en cache les demande OPTIONS préliminaire hello.

Hello services de stockage Azure prennent en charge les en-têtes avec préfixe en spécifiant pour les deux hello **AllowedHeaders** et **ExposedHeaders** éléments. tooallow une catégorie d’en-têtes, vous pouvez spécifier une catégorie de toothat préfixe commun. Par exemple, le fait de spécifier *x-ms-meta** comme en-tête préfixé crée une règle qui établit une correspondance avec tous les en-têtes commençant par x-ms-meta.

Hello limites suivantes s’appliquent les règles tooCORS :

* Vous pouvez spécifier des toofive règles CORS par service de stockage (Blob, Table et file d’attente).
* taille maximale de Hello de tous les paramètres de règles CORS sur la demande de hello, à l’exception des balises XML, ne doit pas dépasser 2 Ko.
* la longueur d’un en-tête autorisé, en-tête exposé ou origine autorisée Hello ne doit pas dépasser 256 caractères.
* Les en-têtes autorisés et les en-têtes exposés peuvent être :
  * En-têtes littéraux, où nom précis d’en-tête de hello est spécifié, tel que **x-ms-meta-processed**. Un maximum de 64 en-têtes littéraux peut être spécifié à la demande de hello.
  * En-têtes préfixés, où un préfixe de hello en-tête est spécifié, tel que **x-ms-meta-data***. En spécifiant un préfixe de cette façon autorise ou expose les en-têtes qui commençant par le préfixe de hello. Un maximum de deux en-têtes avec préfixe peut être spécifié à la demande de hello.
* Hello des méthodes (ou verbes HTTP) spécifiés dans hello **AllowedMethods** élément doit respecter les méthodes toohello pris en charge par les API de service de stockage Azure. Les méthodes prises en charge sont DELETE, GET, HEAD, MERGE, POST, OPTIONS et PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Présentation de la logique d'évaluation des règles CORS
Lorsqu’un service de stockage reçoit une demande préliminaire ou réelle, il évalue cette demande, selon les règles CORS hello que vous avez établi pour le service de hello via l’opération Set Service Properties appropriée hello. Les règles CORS sont évaluées dans l’ordre de hello dans lequel ils ont été définis dans le corps de la demande hello Hello opération Set Service Properties.

Les règles CORS sont évaluées comme suit :

1. Tout d’abord, le domaine d’origine hello de demande de hello est comparée aux domaines hello répertoriés pour hello **AllowedOrigins** élément. Si le domaine d’origine hello est inclus dans la liste de hello, ou tous les domaines sont autorisés avec le caractère générique de hello ' *', puis évaluation des règles continue. Si le domaine d’origine hello n’est pas inclus, la demande de hello échoue.
2. Ensuite, méthode hello (ou un verbe HTTP) de demande de hello est vérifié par rapport aux méthodes hello répertoriés dans hello **AllowedMethods** élément. Si la méthode hello est inclus dans la liste de hello, évaluation des règles continue ; Si ce n’est pas le cas, puis demande de hello échoue.
3. Si la demande de hello correspond à une règle dans son domaine d’origine et sa méthode, cette règle est sélectionnée tooprocess hello demande et aucune autre règle n’est évaluées. Avant hello demande réussisse, toutefois, des en-têtes spécifiés dans la demande hello sont vérifiées par rapport aux en-têtes hello répertoriés dans hello **AllowedHeaders** élément. Si les en-têtes de hello envoyés ne correspondent pas hello en-têtes autorisé, la demande de hello échoue.

Étant donné que les règles de hello sont traitées dans l’ordre de hello qu’ils sont présents dans le corps de la demande hello, les meilleures pratiques recommandent de spécifier règles les plus restrictives hello avec respectent tooorigins tout d’abord dans la liste hello, afin que ceux-ci sont évalués en premier. Spécifier des règles qui sont moins restrictives – par exemple, un tooallow règle toutes les origines – à fin hello de liste de hello.

### <a name="example--cors-rules-evaluation"></a>Exemple : évaluation de règles CORS
Hello suivant montre un corps de demande partiel pour une opération tooset CORS de règles pour les services de stockage hello. Consultez [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [définir les propriétés de Service de file d’attente](https://msdn.microsoft.com/library/hh452232.aspx), et [Set Table Service Properties](https://msdn.microsoft.com/library/hh452240.aspx) pour plus d’informations sur la construction de demande de hello.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Ensuite, prenez en compte les hello suivant des demandes CORS :

| Demande |  |  | Réponse |  |
| --- | --- | --- | --- | --- |
| **Méthode** |**Origine** |**En-têtes de requête** |**Correspondance de règle** |**Résultat** |
| **PUT** |http://www.contoso.com |x-ms-blob-content-type |Première règle |Succès |
| **GET** |http://www.contoso.com |x-ms-blob-content-type |Deuxième règle |Succès |
| **GET** |http://www.contoso.com |x-ms-client-request-id |Deuxième règle |Échec |

Hello première demande correspond à première règle de hello : domaine d’origine hello correspond à hello autorisé origines, méthode hello correspond à hello autorisé des méthodes et en-tête de hello correspond à hello autorisée des en-têtes – et sorte qu’elle réussit.

demande de deuxième Hello ne correspond pas à première règle de hello car méthode hello ne correspond pas hello autorisé de méthodes. Il est le cas, cependant, correspondant à seconde hello, en cas de succès.

Hello troisième demande correspond à hello deuxième règle de son domaine d’origine et la méthode, donc aucune autre règle n’est évaluées. Toutefois, hello *en-tête x-ms-client-request-id* , mais n’est pas autorisée par la deuxième règle de hello, de demande de hello échoue, bien que la sémantique de la règle de tiers hello hello lui aurait permis toosucceed hello.

> [!NOTE]
> Bien que cet exemple montre une règle moins restrictive avant une plus restrictive, en général recommandé hello est tout d’abord les règles les plus restrictives toolist hello.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Comprendre comment l’en-tête Vary de hello est défini
Hello *Vary* en-tête est un en-tête HTTP/1.1 standard composé d’un ensemble de champs d’en-tête de demande qui indiquent l’agent utilisateur ou du navigateur hello sur les critères de hello qui ont été sélectionnés par hello server tooprocess hello demande. Hello *Vary* en-tête est principalement utilisé pour la mise en cache par les serveurs proxy, les navigateurs et CDN qui toodetermine l’utiliser la réponse de hello doit être mis en cache. Pour plus d’informations, consultez Spécification hello hello [en-tête Vary](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Lorsque le navigateur de hello ou un autre agent utilisateur met en cache la réponse hello à partir d’une demande CORS, le domaine d’origine hello est mis en cache en tant que hello autorisé d’origine. Lorsqu’un second problèmes de domaine hello même demande pour une ressource de stockage pendant que le cache de hello est actif, l’agent utilisateur de hello récupère le domaine d’origine mis en cache hello. domaine de second Hello ne correspond pas à domaine mis en cache de hello, demande de hello échoue lorsqu’elle réussit dans le cas contraire. Dans certains cas, le stockage Azure affecte en-tête Vary de hello trop**origine** tooinstruct hello utilisateur toosend hello ultérieures CORS demande toohello service de l’agent lorsque hello demande hello diffère de domaine mis en cache d’origine.

Le stockage Azure définit hello *Vary* en-tête trop**origine** pour les demandes GET/HEAD réelles Bonjour suivant cas :

* Si la demande hello origine correspond exactement à hello autorisés origine défini par une règle CORS. toobe une correspondance exacte, règle CORS hello ne peut pas inclure un caractère générique ' * ' caractères.
* Il n’est pas règle correspondante hello demande d’origine, mais CORS sont activées pour le service de stockage hello.

Dans les cas de hello où une demande GET/HEAD correspond à une règle CORS qui autorise toutes les origines, réponse de hello indique que toutes les origines sont autorisées et cache de l’agent utilisateur hello autorise les demandes suivantes à partir de n’importe quel domaine d’origine pendant que le cache de hello est actif.

Notez que pour les demandes à l’aide de méthodes autres que GET/HEAD, services de stockage hello ne définit pas en-tête Vary de hello, étant donné que les méthodes de toothese réponses ne sont pas mises en cache par les agents utilisateurs.

Hello tableau suivant indique comment le stockage Azure répondra tooGET/HEAD demandes en fonction de hello précédemment mentionné cas :

| Demande | Paramètre de compte et résultat de l'évaluation de la règle |  |  | Réponse |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **En-tête d’origine présent dans la demande** |**Règle(s) CORS spécifiée(s) pour ce service** |**Règle de correspondance existante qui autorise toutes les origines(*)** |**Règle de correspondance existante pour la correspondance exacte d’origine** |**Réponse inclut tooOrigin de jeu d’en-tête Vary** |**La réponse inclut l’en-tête Access-Control-Allowed-Origin : «*  »** |**La réponse inclut l’en-têteAccess-Control-Exposed-Headers** |
| Non |Non |Non |Non |Non |Non |Non |
| Non |Oui |Non |Non |Oui |Non |Non |
| Non |Oui |Oui |Non |Non |Oui |Oui |
| Oui |Non |Non |Non |Non |Non |Non |
| Oui |Oui |Non |Oui |Oui |Non |Oui |
| Oui |Oui |Non |Non |Oui |Non |Non |
| Oui |Oui |Oui |Non |Non |Oui |Oui |

## <a name="billing-for-cors-requests"></a>Facturation des demandes CORS
Les demandes préliminaires ayant réussi sont facturées si vous avez activé des CORS pour un des services de stockage hello pour votre compte (en appelant [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [définir les propriétés de Service de file d’attente](https://msdn.microsoft.com/library/hh452232.aspx), ou [ Définir les propriétés de Service de Table](https://msdn.microsoft.com/library/hh452240.aspx)). frais de toominimize, envisagez de définir le hello **MaxAgeInSeconds** élément dans votre CORS règles tooa grande valeur permettant de hello agent utilisateur met en cache les demande hello.

Les demandes préliminaires infructueuses ne seront pas facturés.

## <a name="next-steps"></a>Étapes suivantes
[Définition des propriétés du service Blob](https://msdn.microsoft.com/library/hh452235.aspx)

[Définition des propriétés du service de File d’attente](https://msdn.microsoft.com/library/hh452232.aspx)

[Définition des propriétés du service de Table](https://msdn.microsoft.com/library/hh452240.aspx)

[Spécification du Partage des ressources cross-origin (W3C)](http://www.w3.org/TR/cors/)

