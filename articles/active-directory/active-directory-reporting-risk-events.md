---
title: "événements à risque aaaAzure Active Directory | Documents Microsoft"
description: "Cette rubrique offre une présentation détaillée des événements à risque."
services: active-directory
keywords: "azure active directory identity protection, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Événements à risque dans Azure Active Directory

Hello grande majorité des prennent des failles de sécurité placer lorsque des personnes malveillantes accèdent environnement tooan d’accès par le vol d’identité d’un utilisateur. Détecter les identités compromises n’est pas chose aisée. Azure Active Directory utilise des algorithmes et des paramètres heuristiques actions suspectes toodetect qui sont des comptes d’utilisateur associés tooyour d’apprentissage adaptatif. Chaque action suspecte détectée est stockée dans un enregistrement appelé *événement à risque*.

À l’heure actuelle, Azure Active Directory détecte six types d’événements à risque :

- [Utilisateurs dont les informations d’identification ont fait l’objet d’une fuite](#leaked-credentials) 
- [Connexions depuis des adresses IP anonymes](#sign-ins-from-anonymous-ip-addresses) 
- [Voyage Impossible tooatypical emplacements](#impossible-travel-to-atypical-locations) 
- [Connexions depuis des emplacements inconnus](#sign-in-from-unfamiliar-locations)
- [Connexions depuis des périphériques infectés](#sign-ins-from-infected-devices) 
- [Connexions depuis des adresses IP avec une activité suspecte](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Événement à risque](./media/active-directory-reporting-risk-events/91.png)

Cette rubrique fournit une présentation détaillée des événements risque sont et comment vous pouvez les utiliser tooprotect vos identités Azure AD.


## <a name="risk-event-types"></a>Type d’événement à risque

propriété de type événement Hello risque est qu'un identificateur pour l’action de suspectes hello un enregistrement d’événement risque a été créé.  
Investissements de Microsoft dans le processus de détection hello entraînent :

- Précision de la détection toohello améliorations des événements existants, risque 
- Nouveaux types d’événements risque qui seront ajoutés dans hello future

### <a name="leaked-credentials"></a>Informations d’identification divulguées

Lorsque cybercriminels compromettent des mots de passe valides des utilisateurs légitimes, personnes mal intentionnées hello souvent partagent ces informations d’identification. Cela est généralement effectuée par leur validation publiquement sur hello sombre web ou coller les sites ou par les commerciaux ou vendre les informations d’identification hello sur le marché noir de hello. informations d’identification révélés Hello Microsoft service acquiert le nom d’utilisateur / mot de passe par l’analyse des sites web publics et foncé et en travaillant avec des paires :

- Des chercheurs
- Les lois en vigueur
- Les équipes de sécurité Microsoft
- D’autres sources approuvées 

Lorsque le service de hello acquiert nom d’utilisateur / paires de mot de passe, elles sont vérifiées par rapport aux informations d’identification valides utilisateurs AAD actuel. Lorsqu’une correspondance est trouvée, cela signifie que le mot de passe d’un utilisateur a été compromis. Un *événement à risque lié à une fuite d’informations d’identification* est alors créé.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Connexions depuis des adresses IP anonymes

Ce type d’événement à risque signale les utilisateurs qui se sont connectés depuis une adresse IP ayant été identifiée comme l’adresse IP d’un proxy anonyme. Ces proxies sont utilisés par des personnes qui veulent toohide son leur adresse IP et peut être utilisé dans un but malveillant.


### <a name="impossible-travel-tooatypical-locations"></a>Voyage Impossible tooatypical emplacements

Ce type d’événement risque identifie deux connexions provenant d’emplacements géographiquement distants, où au moins un des emplacements de hello peut également être inhabituel pour l’utilisateur de hello, fonction comportement antérieur. En outre, le temps de hello entre hello deux connexions est plus courte que durée hello il aurait fallu tootravel d’utilisateur hello de hello premier emplacement toohello deuxième, indiquant qu’un autre utilisateur est à l’aide de hello même informations d’identification. 

Cet algorithme d’apprentissage automatique qui ignore évidente «*faux positifs*» qui contribuent à condition de voyage impossible toohello, tels que les réseaux privés virtuels et des emplacements régulièrement utilisées par d’autres utilisateurs dans l’organisation de hello.  système de Hello a une période d’apprentissage initiale de 14 jours au cours de laquelle elle a appris le comportement d’authentification d’un nouvel utilisateur.

### <a name="sign-in-from-unfamiliar-locations"></a>Connexions depuis des emplacements non connus

Ce type d’événement risque considère au-delà de l’authentification dans les emplacements (IP, la Latitude / Longitude et ASN) toodetermine des emplacements inhabituels / nouveau. système de Hello stocke des informations sur les emplacements précédents utilisé par un utilisateur et prend en compte ces emplacements « familiers ». Hello risque est déclenché lorsque hello la connexion se produit à partir d’un emplacement qui n’est pas déjà dans liste hello des emplacements familiers. système de Hello a une période d’apprentissage initiale de 30 jours, pendant laquelle il ne signale pas d’emplacements en tant qu’emplacements non connus. système de Hello ignore également les connexions à partir d’appareils familières et emplacements géographiquement Fermez tooa l’emplacement de votre choix. 

### <a name="sign-ins-from-infected-devices"></a>Connexions depuis des appareils infectés

Ce type d’événement risque identifie les connexions à partir des appareils infectés par des logiciels malveillants, qui sont connues tooactively à communiquer avec un serveur robot. Cela est déterminé par la corrélation des adresse IP du périphérique de l’utilisateur hello par rapport aux adresses IP qui étaient en contact avec un serveur robot. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Connexions depuis des adresses IP avec des activités suspectes
Ce type d’événement à risque identifie les adresses IP depuis lesquelles un grand nombre de tentatives de connexion ayant échoué ont été constatées, pour plusieurs comptes d’utilisateurs et sur une courte période. Cela correspond à des modèles de trafic d’adresses IP utilisées par les pirates et est un indicateur fort comptes soit déjà ou qui sont sur toobe compromis. Il s’agit d’un algorithme d’apprentissage automatique qui ignore évidente »*des faux positifs*», telles que les adresses IP qui sont régulièrement utilisées par d’autres utilisateurs dans l’organisation de hello.  système de Hello a une période d’apprentissage initiale de 14 jours où elle a appris hello connectez-vous comportement d’un nouvel utilisateur et un nouveau client.


## <a name="detection-type"></a>Type de détection

propriété de type Hello détection est un indicateur (en temps réel ou en mode hors connexion) et intervalle de temps de détection d’un événement à risque hello.  
Actuellement, la plupart des événements à risque sont détectés en mode hors connexion dans une opération de post-traitement après que l’événement à risque hello s’est produite.

Hello tableau suivant répertorie la durée hello qu'il occupe pour un tooshow de type de détection dans un rapport connexe :

| Type de détection | Latence dans la génération des rapports |
| --- | --- |
| Temps réel | too10 5 minutes |
| Hors ligne | too4 2 heures |


Pour les types d’événements risque hello Qu'azure Active Directory détecte, les types de détection hello sont :

| Type d’événement à risque | Type de détection |
| :-- | --- | 
| [Utilisateurs dont les informations d’identification ont fait l’objet d’une fuite](#leaked-credentials) | Hors ligne |
| [Connexions depuis des adresses IP anonymes](#sign-ins-from-anonymous-ip-addresses) | Temps réel |
| [Voyage Impossible tooatypical emplacements](#impossible-travel-to-atypical-locations) | Hors ligne |
| [Connexions depuis des emplacements inconnus](#sign-in-from-unfamiliar-locations) | Temps réel |
| [Connexions depuis des périphériques infectés](#sign-ins-from-infected-devices) | Hors ligne |
| [Connexions depuis des adresses IP avec une activité suspecte](#sign-ins-from-ip-addresses-with-suspicious-activity) | Hors ligne|


## <a name="risk-level"></a>Niveau de risque

propriété du niveau Hello risque d’un événement à risque est un indicateur (haute, moyenne ou faible) pour le niveau de gravité hello et confiance hello d’un événement à risque. Cette propriété vous permet de tooprioritize hello actions nécessaires. 

gravité Hello d’événement à risque hello représente la puissance hello du signal de hello sous la forme d’un PRÉDICTEUR de compromission de l’identité.  
confiance de Hello est un indicateur possibilité hello de faux positifs. 

Par exemple, 

* **Élevé**: probabilité élevée et gravité élevée de l’événement à risque. Ces événements sont des indicateurs fort que hello l’identité d’utilisateur a été compromise, et des comptes d’utilisateur affectés doivent être mis à jour immédiatement.

* **Moyen**: sévérité élevée, mais probabilité moindre de l’événement à risque, ou inversement. Ces événements présentent des risques potentiels et les comptes d’utilisateurs concernés doivent faire l’objet de mesures de correction.

* **Faible**: probabilité faible et gravité limitée de l’événement à risque. Cet événement ne peut pas nécessiter une action immédiate, mais lorsqu’elles sont combinées avec d’autres événements risque, peut fournir une indication fort qui hello identité est compromise.

![Niveau de risque](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Informations d’identification divulguées

Une fuite des informations d’identification des risques événements sont classés comme un **haute**car ils fournissent une indication que le nom d’utilisateur hello et le mot de passe sont disponibles tooan attaquant.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Connexions depuis des adresses IP anonymes

le niveau de risque Hello pour ce type d’événement risque est **support** , car une adresse IP anonyme n’est pas une indication fort d’une compromission d’un compte.  
Nous vous recommandons de contacter hello utilisateur tooverify immédiatement si elles ont été à l’aide des adresses IP anonymes.


### <a name="impossible-travel-tooatypical-locations"></a>Voyage Impossible tooatypical emplacements

Voyage Impossible est généralement un bon indicateur qu’un pirate a été en mesure de toosuccessfully connectez-vous. Toutefois, des faux positifs peuvent se produire lorsqu’un utilisateur est en déplacement à l’aide d’un nouveau périphérique ou un réseau privé virtuel qui n’est généralement pas utilisé par d’autres utilisateurs dans l’organisation de hello. Une autre source de faux positifs, des applications incorrectement passer le serveur d’adresses IP en tant que client IPs, ce qui peut donner l’apparence de hello de connexions ayant lieu à partir du centre de données hello où cette application du serveur principal est hébergé (souvent, ce sont les centres de données Microsoft, qui peut donner d’apparence de hello de connexions en cours à partir de Microsoft appartenant à des adresses IP). À la suite de ces faux positifs, est le niveau de risque hello pour cet événement risque **support**.

> [!TIP]
> Vous pouvez réduire hello de false-positves signalé pour ce type d’événement risque en configurant [emplacements nommés](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Connexions depuis des emplacements non connus

Emplacements non connus peuvent fournir une indication de fort qu’un intrus est en mesure de toouse une identité. De faux positifs peuvent se produire quand un utilisateur est en déplacement, essaie un nouvel appareil ou utilise un nouveau VPN. À la suite de ces faux positifs, est le niveau de risque hello pour ce type d’événement **support**.

### <a name="sign-ins-from-infected-devices"></a>Connexions depuis des appareils infectés

Cet événement à risque identifie les adresses IP, pas les appareils des utilisateurs. Si plusieurs périphériques sont derrière une seule adresse IP et uniquement certaines sont contrôlés par un réseau bot, les connexions à partir d’autres appareils mon déclencheur cet événement inutilement, qui est la raison hello pour cet événement risque de classer en tant que **faible**.  

Nous vous recommandons de vous contactez hello utilisateur et analyser les périphériques de l’utilisateur du hello. Il est également possible que le périphérique personnel d’un utilisateur est infecté, ou comme mentionné précédemment, que quelqu'un d’autre utilisait un appareil infecté d’hello même adresse IP en tant qu’utilisateur de hello. Appareils infectés sont souvent infectés par des logiciels malveillants qui n’ont pas encore été identifiés par un logiciel antivirus et peut également indiquer comme des habitudes d’utilisateur incorrects qui peuvent avoir provoqué toobecome de périphérique hello infecté.

Pour plus d’informations sur les infections de programmes malveillants tooaddress, consultez hello [centre de Protection contre les programmes malveillants](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Connexions depuis des adresses IP avec des activités suspectes

Nous vous conseillons de contacter hello utilisateur tooverify si elles réellement connecté à partir d’une adresse IP qui a été marquée comme suspecte. le niveau de risque Hello pour ce type d’événement est «**support**», car plusieurs périphériques peuvent se trouver derrière hello même adresse IP, alors que seules certaines peuvent être responsables d’activité suspecte hello. 


 
## <a name="next-steps"></a>Étapes suivantes

Événements à risque sont foundation hello pour protéger les identités de votre Azure AD. Azure AD peut détecter actuellement six événements à risque : 


| Type d’événement à risque | Niveau de risque | Type de détection |
| :-- | --- | --- |
| [Utilisateurs dont les informations d’identification ont fait l’objet d’une fuite](#leaked-credentials) | Élevé | Hors ligne |
| [Connexions depuis des adresses IP anonymes](#sign-ins-from-anonymous-ip-addresses) | Moyenne | Temps réel |
| [Voyage Impossible tooatypical emplacements](#impossible-travel-to-atypical-locations) | Moyenne | Hors ligne |
| [Connexions depuis des emplacements inconnus](#sign-in-from-unfamiliar-locations) | Moyenne | Temps réel |
| [Connexions depuis des périphériques infectés](#sign-ins-from-infected-devices) | Faible | Hors ligne |
| [Connexions depuis des adresses IP avec une activité suspecte](#sign-ins-from-ip-addresses-with-suspicious-activity) | Moyenne | Hors ligne|

Où vous trouverez hello événements à risque qui ont été détectés dans votre environnement ?
Il existe deux emplacements dans lesquels vous pouvez passer en revue les événements à risque signalés :

 - **Génération de rapports Azure AD** : les événements à risque font partie des rapports de sécurité d’Azure AD. Pour plus d’informations, consultez hello [les utilisateurs sur les rapports de sécurité risque](active-directory-reporting-security-user-at-risk.md) et hello [rapport de sécurité des connexions risquée](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection** : les événements à risque font également partie des fonctionnalités de génération de rapports [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
    

Lors de la détection hello d’événements à risque déjà représente un aspect important de la protection de vos identités, vous avez également hello option tooeither remédier manuellement ou même d’implémenter des réponses automatisées en configurant des stratégies d’accès conditionnel. Pour plus de détails, consultez [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
 
