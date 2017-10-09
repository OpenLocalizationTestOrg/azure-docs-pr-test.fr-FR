---
title: guide de protocole de connexions hybrides de relais aaaAzure | Documents Microsoft
description: Guide du protocole de connexions hybrides Azure Relay.
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Protocole de connexions hybrides Azure Relay
Relais Azure est un des piliers de fonctionnalité clé hello de plateforme du Bus des services Azure hello. Hello nouvelle *connexions hybrides* de relais est une évolution sécurisée, protocole ouvert basée sur HTTP et le protocole WebSocket. Elle remplace l’ancienne hello, également nommé *BizTalk Services* fonctionnalité qui a été fondée sur un protocole propriétaire. intégration de Hello des connexions hybrides dans les Services d’application Azure continue toofunction comme-est.

Les connexions hybrides permettent d’établir une communication de flux binaire bidirectionnel entre deux applications en réseau, durant laquelle une des deux, voire les deux, peuvent se trouver derrière un NAT ou un pare-feu. Cet article décrit les interactions du côté client hello avec relais de connexions hybrides hello pour connecter des clients dans l’écouteur et rôles d’expéditeur et comment écouteurs acceptent de nouvelles connexions.

## Modèle d’interaction
relais de connexions hybrides Hello connecte deux parties en fournissant un point de rendezvous Bonjour Azure cloud qui les deux parties peuvent détecter et connecter toofrom du point de vue de son propre réseau. Ce point rendezvous est appelé « Connexion hybride » dans cette section et autres documentations, Bonjour API et Bonjour portail Azure. Hello connexions hybrides point de terminaison de service est appelé tooas hello « service » pour le reste de hello de cet article. modèle d’interaction Hello utilise nomenclature hello établie par de nombreuses autres API de mise en réseau.

Il existe un écouteur qui vous indique tout d’abord les connexions entrantes toohandle de préparation et par la suite les accepte lorsqu’ils arrivent. Sur hello autre côté, il existe un connexion client qui se connecte à l’écouteur hello, attendu que toobe connexion accepté pour l’établissement d’un chemin d’accès de la communication bidirectionnelle.
« Connexion », « Écouter » et « Accepter » sont hello même termes vous trouvez dans la plupart des API de socket.

N’importe quel modèle de communication relayée a des connexions sortantes vers un point de terminaison de service, qui confère un « écouteur » de hello également un « client » en cours d’utilisation de langage commun et peuvent également provoquer des autres surcharges de la terminologie des parties. Nous avons donc d’utiliser pour les connexions hybrides une terminologie précise Hello est comme suit :

programmes Hello des deux côtés d’une connexion sont appelés « clients », car elles sont service toohello de clients. Hello client qui attend et accepte les connexions est le « écouteur », ou est dite toobe dans hello « écouteur un rôle. » client Hello qui démarre une nouvelle connexion vers un écouteur via le service de hello est appelée hello « expéditeur », ou dans le rôle « expéditeur ».

### Interactions de l’écouteur
écouteur de Hello a quatre interactions avec le service de hello ; tous les détails de câble sont décrits plus loin dans cet article dans la section de référence hello.

#### Écouter
service de toohello readiness tooindicate qu’un écouteur est prêt tooaccept connexions, il crée une connexion WebSocket sortante. la négociation de connexion Hello exécute nom hello d’une connexion hybride configuré sur l’espace de noms de relais hello et un jeton de sécurité qui confère hello « Écoute » à droite sous ce nom.
Lorsque hello WebSocket est acceptée par le service de hello, hello inscription est terminée et hello établie web que WebSocket est persistante en tant que hello « canal de contrôle » pour l’activation de toutes les interactions résultantes. service de Hello permet des too25 des écouteurs simultanés sur une connexion hybride. S’il existe plusieurs écouteurs actifs, les connexions entrantes sont réparties entre tous selon un ordre aléatoire ; la répartition équitable n’est pas garantie.

#### Acceptation
Lorsqu’un expéditeur ouvre une nouvelle connexion sur le service de hello, service de hello choisit et notifie un des écouteurs de hello active sur hello connexion hybride. Cette notification est envoyée toohello écouteur sur canal de contrôle ouverte hello en tant qu’un message JSON contenant URL hello du point de terminaison WebSocket hello hello écouteur doit se connecter toofor hello connexion acceptée.

URL de Hello peut et doit être utilisé directement par l’écouteur hello sans aucun travail supplémentaire.
informations de Hello encodé sont uniquement valide pendant une courte période de temps, essentiellement pour aussi longtemps que l’expéditeur de hello sont toowait prêt pour hello connexion toobe établie de bout en bout, mais les 30 secondes au maximum tooa. Hello URL peut uniquement être utilisée pour la tentative d’une connexion réussie. Dès que hello WebSocket connexion avec rendezvous de hello QU'URL est établie, toutes les activités supplémentaires sur cette WebSocket est relayée entre et expéditeur toohello, sans intervention ni interprétation par le service de hello.

#### Renouveler
jeton de sécurité Hello qui doit être utilisés tooregister hello écouteur et maintenir que le canal de contrôle peut expirer pendant que hello écouteur est actif. expiration du jeton Hello n’affecte pas les connexions en cours, mais il cause toobe de canal de contrôle hello supprimé par le service hello à ou peu après le moment hello d’expiration. opération de « renouveler » Hello est un message JSON hello écouteur peut envoyer des jeton de hello tooreplace associé au canal de contrôle hello, afin que hello canal de contrôle peut être conservée pendant de longues périodes.

#### Ping
Si le canal de contrôle hello reste inactif pendant une longue période, intermédiaires sur la façon de hello, comme le chargement équilibrages ou NAT peut supprimer connexion TCP de hello. opération de « ping » Hello évite dont les en envoyant une petite quantité de données sur le canal hello qui rappelle tous les membres de l’itinéraire de réseau hello cette connexion hello toobe actif, et il sert également un test « dynamique » pour le port d’écoute hello. Si la commande ping de hello échoue, canal de contrôle hello doit être considérée comme inutilisable et écouteur de hello doit se reconnecter.

### Interaction de l’expéditeur
expéditeur de Hello a uniquement une interaction avec le service de hello : il se connecte.

#### Connecter
opération de « se connecter » Hello ouvre un WebSocket sur service hello, en fournissant hello nom Hello connexion hybride (le cas échéant, mais requise par défaut) un jeton de sécurité donnant l’autorisation « Send » dans la chaîne de requête hello. service de Hello interagit ensuite avec l’écouteur hello Bonjour façon décrit précédemment, et écouteur de hello crée une connexion rendezvous qui est jointe à cette WebSocket. Une fois hello WebSocket a été accepté, tous les autres interactions sur ce WebSocket sont avec un écouteur connecté.

### Résumé de l’interaction
résultat de Hello de ce modèle d’interaction est que le client expéditeur hello proviennent de la négociation avec un WebSocket « propre », qui est connecté tooa écouteur et qui a besoin d’aucune autres PRÉAMBULES ou la préparation. Ce modèle permet de pratiquement n’importe quel existant WebSocket client implémentation tooreadily tirer parti de hello service de connexions hybrides, vous devez fournir une URL correctement construit dans leur couche du client WebSocket.

Hello rendezvous connexion WebSocket qui hello écouteur obtient via l’interaction d’acceptation est également nette et peut être transmise tooany implémentation serveur WebSocket existante avec une abstraction supplémentaire minimale qui fait la distinction entre « accepter » opérations sur les écouteurs de réseau local et les connexions hybrides à distance de leur infrastructure opérations « acceptent ».

## Référence sur le protocole

Cette section décrit en détail de hello d’interactions de protocole hello décrites précédemment.

Toutes les connexions de WebSocket sont effectuées sur le port 443 mis à niveau à partir de HTTPS 1.1, qui est couramment abstrait par les API et les infrastructures de WebSocket. Cette description ne tient pas compte de l’implémentation et ne suggère aucune infrastructure en particulier.

### Protocole de l’écouteur
protocole de l’écouteur Hello se compose de deux mouvements de connexion et les trois opérations de message.

#### Connexion du canal de contrôle de l’écouteur
canal de contrôle Hello est ouvert avec la création d’une connexion WebSocket à :

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Hello `namespace-address` est le nom de domaine complet de hello d’espace de noms Azure relais hello que hôtes hello connexion hybride, en général du formulaire de hello `{myname}.servicebus.windows.net`.

options de paramètre de chaîne de requête Hello sont les suivantes.

| Paramètre | Requis | Description |
| --- | --- | --- |
| `sb-hc-action` |Oui |Pourquoi de rôle d’écouteur hello paramètre doit être **sb-hc-action = écoute** |
| `{path}` |Oui |chemin d’espace de noms encodé en URL Hello Hello préconfiguré connexion hybride tooregister cet écouteur sur. Cette expression est ajoutée toohello fixée `$hc/` partie chemin d’accès. |
| `sb-hc-token` |Oui\* |Hello écouteur doit fournir un valide, encodé en URL, Service Bus partagé jeton d’accès pour l’espace de noms hello ou la connexion hybride qui confère hello **écouter** droite. |
| `sb-hc-id` |Non |Cet ID facultatif fourni par le client permet un suivi de diagnostic de bout en bout. |

Si la connexion WebSocket de hello échoue en raison de chemin d’accès de la connexion hybride toohello ne pas en cours d’inscription, ou un jeton non valide ou manquant ou une autre erreur, des commentaires d’erreur hello sont fournie à l’aide du modèle de commentaires d’état HTTP 1.1 hello régulière. La description d’état contient un ID de suivi d’erreur qui peut être communiqué au personnel de support Azure :

| Code | Error | Description |
| --- | --- | --- |
| 404 |Introuvable |chemin d’accès de la connexion hybride Hello n’est pas valide ou l’URL de base hello est incorrect. |
| 401 |Non autorisé |jeton de sécurité Hello est manquant ou incorrect ou non valide. |
| 403 |Interdit |jeton de sécurité Hello n’est pas valide pour ce chemin d’accès pour cette action. |
| 500 |Erreur interne |Suite à un problème dans le service hello. |

Si hello connexion WebSocket est intentionnellement arrêté par le service de hello après que qu’il a été initialement configuré, raison hello pour cette opération est communiqué à l’aide d’un code d’erreur de protocole WebSocket approprié, ainsi que d’un message d’erreur qui inclut également un suivi ID. service de Hello arrêtera pas le canal de contrôle sans rencontrer une condition d’erreur. Les arrêts normaux sont contrôlés par le client.

| État du SW | Description |
| --- | --- |
| 1001 |chemin d’accès de la connexion hybride Hello a été supprimé ou désactivé. |
| 1008 |jeton de sécurité Hello a expiré, par conséquent, la stratégie d’autorisation de hello est violée. |
| 1011 |Suite à un problème dans le service hello. |

### Négociation d’acceptation
Hello « accepter » est envoyé par l’écouteur de toohello service hello sur le canal de contrôle précédemment établie en tant qu’un message JSON dans un bloc de texte WebSocket. Il n’existe aucun message de réponse à toothis.

message de salutation contient un objet JSON nommé « accepter », qui définit les propriétés suivantes pour l’instant de hello :

* **adresse** : hello toobe de chaîne URL utilisée pour établir hello WebSocket toothe service tooaccept une connexion entrante.
* **ID** – hello un identificateur unique pour cette connexion. Si l’ID de hello a été fourni par le client expéditeur du hello, il s’agit de la valeur de l’expéditeur fournie hello, sinon il s’agit d’une valeur générée par le système.
* **connectHeaders** – tous les en-têtes HTTP qui ont été fournis de point de terminaison de relais toohello par expéditeur hello, qui inclut également hello protocole s-WebSocket et les en-têtes Sec-WebSocket-Extensions.

#### Message d’acceptation

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Hello adresse URL fournie Bonjour message JSON est utilisé par l’écouteur de hello pour établir hello WebSocket pour accepter ou rejeter le socket de l’expéditeur hello.

#### Acceptation du socket de hello
tooaccept, port d’écoute hello établit une adresse toohello fourni de connexion WebSocket.

Si hello « Accepter » message transporte une `Sec-WebSocket-Protocol` en-tête, il est prévu à cet écouteur hello accepte uniquement hello WebSocket si elle prend en charge ce protocole. En outre, il définit les en-tête hello comme hello que WebSocket est établie.

Hello valable toohello `Sec-WebSocket-Extensions` en-tête. Si l’infrastructure de hello prend en charge une extension, il doit définir réponse de côté serveur hello en-tête toohello Hello requis `Sec-WebSocket-Extensions` protocole de transfert pour l’extension de hello.

URL de Hello doit être utilisée en tant que-est pour l’établissement de hello accepter socket, mais qui contient les paramètres suivants :

| Paramètre | Requis | Description |
| --- | --- | --- |
| `sb-hc-action` |Oui |Pour accepter un socket, le paramètre hello doit être`sb-hc-action=accept` |
| `{path}` |Oui |(voir hello paragraphe suivant) |
| `sb-hc-id` |Non |Voir la description précédente de **id**. |

`{path}`est le chemin d’accès de hello espace de noms encodé en URL de hello préconfiguré connexion hybride sur le tooregister cet écouteur. Cette expression est ajoutée toothe fixée `$hc/` partie chemin d’accès. 

Hello `path` expression peut être étendue avec un suffixe et une expression de chaîne de requête qui suit le nom enregistré de hello après une barre oblique séparation. Ainsi, hello expéditeur toopass dispatch arguments toohello acceptant écouteur client lorsqu’il n’est pas possible de tooinclude HTTP en-têtes. Hello expectation cet écouteur hello analyse framework partie du chemin d’accès fixe hello et hello le nom enregistré dans le chemin d’accès et rend les reste hello, éventuellement sans argument de chaîne de requête par le préfixe `sb-`, application toohello disponible pour choix entre si tooaccept hello connexion.

Pour plus d’informations, consultez hello après « Expéditeur Protocol » section.

Si une erreur existe, le service de hello peut répondre comme suit :

| Code | Error | Description |
| --- | --- | --- |
| 403 |Interdit |URL de Hello n’est pas valide. |
| 500 |Erreur interne |Suite à un problème dans le service hello |

Une fois la connexion de hello a été établie, hello serveur s’arrête hello WebSocket lorsque l’expéditeur hello WebSocket arrête, ou par hello suivant l’état :

| État du SW | Description |
| --- | --- |
| 1001 |client de l’expéditeur Hello arrête de connexion de hello. |
| 1001 |chemin d’accès de la connexion hybride Hello a été supprimé ou désactivé. |
| 1008 |jeton de sécurité Hello a expiré, par conséquent, la stratégie d’autorisation de hello est violée. |
| 1011 |Suite à un problème dans le service hello. |

#### Rejet de socket de hello
Rejet de socket de hello après que « Accepter » message d’inspection hello requiert une négociation similaire pour que hello code d’état et la description de l’état communique le motif du rejet de hello peut transférer de nouveau toohello expéditeur.

choix de conception protocole Hello ici est toouse un protocole de transfert WebSocket (c'est-à-dire tooend conçu dans un état d’erreur définie) afin que les implémentations de l’écouteur client peuvent continuer toorely sur un client WebSocket et n’avez pas besoin utiliser un fichier extra, sans système d’exploitation client HTTP.

socket de hello tooreject, client de hello prend hello adresse URI à partir du message « accepter » de type hello et ajoute deux tooit de paramètres de chaîne de requête, comme suit :

| Paramètre | Requis | Description |
| --- | --- | --- |
| statusCode |Oui |Code d’état HTTP numérique. |
| statusDescription |Oui |Humaine lisible raison du refus de hello. |

Hello QU'URI résultant est ensuite utilisé tooestablish une connexion WebSocket.

En cas de réussite, cette liaison échoue intentionnellement avec un code d’erreur HTTP 410, car aucun WebSocket n’a été établi. Si une erreur survient, hello suivant des codes décrire les erreur hello :

| Code | Error | Description |
| --- | --- | --- |
| 403 |Interdit |URL de Hello n’est pas valide. |
| 500 |Erreur interne |Suite à un problème dans le service hello. |

### Renouvellement du jeton de l’écouteur
Lorsque le jeton d’écouteur hello concerne tooexpire, il peut le remplacer par l’envoi d’un service de toohello message texte frame via le canal de contrôle hello établie. Le message contient un objet JSON appelé `renewToken`, qui définit hello suivant de propriété pour l’instant :

* **jeton** – un jeton d’accès au Service Bus partagé valide, encodé en URL, pour l’espace de noms ou de la connexion hybride qui confère hello **écouter** droite.

#### Message renewToken

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Si la validation du jeton hello échoue, l’accès est refusé et service de cloud computing hello ferme le canal de contrôle hello WebSocket avec une erreur. Sinon, il n’y a aucune réponse.

| État du SW | Description |
| --- | --- |
| 1008 |jeton de sécurité Hello a expiré, par conséquent, la stratégie d’autorisation de hello est violée. |

## Protocole de l’expéditeur
protocole de l’expéditeur Hello consiste toohello identiques efficacement qu'un écouteur est établi.
objectif de Hello est plus grande transparence de bout en bout hello WebSocket. adresse Hello pour se connecter hello toois que même que pour l’écouteur de hello, mais hello « action » est différente et le jeton a besoin d’une autorisation différente :

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Hello *adresse de l’espace de noms* est le nom de domaine complet de hello d’espace de noms Azure relais hello que hôtes hello connexion hybride, en général du formulaire de hello `{myname}.servicebus.windows.net`.

demande de Hello peut contenir arbitraires en-têtes HTTP supplémentaires, y compris ceux de définies par l’application. Tous les fourni le port d’écoute en-têtes flux toohello et se trouvent sur hello `connectHeader` objet Hello **accepter** message de contrôle.

options de paramètre de chaîne de requête Hello sont les suivantes :

| Paramètre | Requis ? | Description |
| --- | --- | --- |
| `sb-hc-action` |Oui |Pour le rôle d’expéditeur hello, paramètre hello doit être `action=connect`. |
| `{path}` |Oui |(voir hello paragraphe suivant) |
| `sb-hc-token` |Oui\* |Hello écouteur doit fournir un valide, encodé en URL, Service Bus partagé jeton d’accès pour l’espace de noms hello ou la connexion hybride qui confère hello **envoyer** droite. |
| `sb-hc-id` |Non |Un ID facultatif qui permet le suivi de diagnostic de bout en bout et devient disponible toohello écouteur pendant hello accepter la négociation. |

Hello `{path}` est le chemin d’accès de hello espace de noms encodé en URL de hello préconfiguré connexion hybride sur le tooregister cet écouteur. Hello `path` expression peut être étendue avec un suffixe et un toocommunicate d’expression de chaîne de requête supplémentaire. Si hello connexion hybride est enregistré sous le chemin d’accès hello `hyco`, hello `path` expression peut être `hyco/suffix?param=value&...` suivis par des paramètres de chaîne de requête hello définis ici. Ainsi, l’expression complète peut être celle-ci :

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Hello `path` expression est transmise via un écouteur de toohello dans l’adresse hello URI contenu dans le message de contrôle « accepter » hello.

En cas de hello connexion WebSocket en raison de chemin d’accès de la connexion hybride toohello ne pas en cours d’inscription, un jeton non valide ou manquant ou une autre erreur, des commentaires d’erreur hello sont fournie à l’aide du modèle de commentaires d’état HTTP 1.1 hello régulière. La description d’état contient un ID de suivi d’erreur qui peut être communiqué au personnel de support Azure :

| Code | Error | Description |
| --- | --- | --- |
| 404 |Introuvable |chemin d’accès de la connexion hybride Hello n’est pas valide ou l’URL de base hello est incorrect. |
| 401 |Non autorisé |jeton de sécurité Hello est manquant ou incorrect ou non valide. |
| 403 |Interdit |jeton de sécurité Hello n’est pas valide pour ce chemin d’accès et pour cette action. |
| 500 |Erreur interne |Suite à un problème dans le service hello. |

Si hello connexion WebSocket est intentionnellement arrêté par le service hello après qu’il a été initialement configuré, raison hello pour cela, est communiqué à l’aide d’un code d’erreur de protocole WebSocket approprié, ainsi que d’un message d’erreur inclut également un ID de suivi.

| État du SW | Description |
| --- | --- |
| 1 000 |écouteur de Hello arrêter de socket de hello. |
| 1001 |chemin d’accès de la connexion hybride Hello a été supprimé ou désactivé. |
| 1008 |jeton de sécurité Hello a expiré, par conséquent, la stratégie d’autorisation de hello est violée. |
| 1011 |Suite à un problème dans le service hello. |

## Étapes suivantes
* [FAQ sur Azure Relay](relay-faq.md)
* [Créer un espace de noms](relay-create-namespace-portal.md)
* [Prise en main de .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Prise en main de Node](relay-hybrid-connections-node-get-started.md)

