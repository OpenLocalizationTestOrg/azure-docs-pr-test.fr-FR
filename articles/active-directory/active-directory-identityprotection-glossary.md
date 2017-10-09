---
title: "aaaAzure Active Directory identité Protection glossaire | Documents Microsoft"
description: "Glossaire d’Azure Active Directory Identity Protection"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité, glossaire"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ff2e96d20e2a3f1df24b78e66be5a0c6807e60a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a>Glossaire d’Azure Active Directory Identity Protection
### <a name="at-risk-user"></a>À risque (utilisateur)
Utilisateur associé à un ou plusieurs événements à risque actifs. 

### <a name="atypical-sign-in-location"></a>Emplacement de connexion atypique
Une sign-in à partir d’un emplacement géographique qui n’est pas typique pour hello spécifique utilisateur, les utilisateurs similaires ou hello locataire.

### <a name="azure-ad-identity-protection"></a>Azure AD Identity Protection
Module de sécurité d’Azure Active Directory offrant une vue consolidée des événements à risque et des vulnérabilités potentielles qui affectent les identités d’une organisation.

### <a name="conditional-access"></a>Accès conditionnel
Une stratégie pour la sécurisation des accès tooresources. Règles d’accès conditionnel sont stockés dans hello Azure Active Directory et sont évaluées par Azure AD avant d’accorder l’accès toohello ressource.  Il existe, par exemple, des règles de restriction d’accès en fonction de l’emplacement de l’utilisateur, de l’intégrité de l’appareil ou de la méthode d’authentification de l’utilisateur.

### <a name="credentials"></a>Informations d'identification
Informations qui incluent l’identification et la preuve d’identification est utilisé toogain accéder aux ressources réseau et toolocal. Les noms d’utilisateur et mots de passe, les cartes à puce et les certificats sont des exemples d’informations d’identification.

### <a name="event"></a>Événement
Enregistrement d’une activité dans Azure Active Directory.

### <a name="false-positive-risk-event"></a>Faux positif (événement à risque)
Statut de l’événement risque définie manuellement par un utilisateur de la Protection d’identité, indiquant que l’événement hello risque a été examiné et a été marqué comme un événement à risque.

### <a name="identity"></a>Identité
Personne ou entité devant faire l’objet d’une vérification au moyen d’une authentification basée sur certains critères, tels qu’un mot de passe ou un certificat.

### <a name="identity-risk-event"></a>Événement de risque d’identité
Événement AAD ayant été marqué comme anormal par le service Identity Protection et qui peut impliquer la corruption d’une identité.

### <a name="ignored-risk-event"></a>Ignoré (événement à risque)
Statut de l’événement risque définie manuellement par un utilisateur de la Protection d’identité, indiquant que l’événement hello risque est fermé sans effectuer une action de mise à jour.

### <a name="impossible-travel-from-atypical-locations"></a>Déplacement impossible à partir d’emplacements inhabituels
Un événement déclenché lorsque deux connexions pour hello même utilisateur sont détectées, où au moins un d’eux est à partir d’un emplacement de connexion inhabituel et où le temps hello entre les connexions hello est plus courte que hello minimale de temps il faudrait toophysically à risque se déplacent entre ces emplacements.  

### <a name="investigation"></a>Investigation
Hello processus de révision des activités de hello, les journaux et autres informations pertinentes relatives tooa risque événement toodecide si les étapes de mise à jour ou d’atténuation sont nécessaires, comprendre si et comment l’identité de hello était compromis et comprendre comment hello identité compromise a été utilisée.

### <a name="leaked-credentials"></a>Informations d’identification divulguées
Un événement déclenché lorsque des informations d’identification utilisateur actuel (nom d’utilisateur et mot de passe) sont détectées à risque validée publiquement dans web foncé de hello par les chercheurs de notre.

### <a name="mitigation"></a>Atténuation
Une action toolimit ou éliminer les capacité de hello d’un appareil ou une personne malveillante tooexploit une identité compromise sans restauration de l’état sans échec tooa hello identité ou l’appareil. Une atténuation ne résout pas les événements précédents risque associés hello identité ou d’appareil.

### <a name="multi-factor-authentication"></a>Authentification multifacteur
Une méthode d’authentification qui requiert deux ou plusieurs méthodes d’authentification, qui peuvent inclure un élément hello utilisateur a, ce type de certificat ; un utilisateur de hello connaît, telles que les noms d’utilisateur, les mots de passe ou les mots de passe ; attributs physiques, telles qu’une empreinte numérique ; et les attributs personnels, par exemple une signature personnelle.

### <a name="offline-detection"></a>Détection en mode hors connexion
détection de Hello d’anomalies et l’évaluation des risques hello d’un événement tel qu’une tentative de connexion après les faits hello, pour un événement qui a déjà eu lieu.

### <a name="policy-condition"></a>Condition de stratégie
Partie d’une stratégie de sécurité qui définit les entités hello (groupes, les utilisateurs, les applications, des plateformes d’appareils, États des appareils, plages d’adresses IP, types de clients) inclus dans la stratégie de hello ou exclus.

### <a name="policy-rule"></a>Règle de stratégie
partie Hello d’une stratégie de sécurité qui décrit les circonstances hello qui déclencheraient hello stratégie et les actions hello effectuées lors de la stratégie de hello est déclenchée.

### <a name="prevention"></a>Prévention
Une action tooprevent dommages toohello organisation abus par le biais d’un appareil ou l’identité suspects ou connaître toobe compromis. Une action de prévention ne sécurise pas les périphériques de hello ou l’identité et ne résout pas les événements à risque précédente.

### <a name="privileged-user"></a>Privilégié (utilisateur)
Un utilisateur ayant au moment de hello d’un événement à risque, tooone des autorisations admin permanentes ou temporaires ou plus de ressources dans Azure Active Directory, comme un administrateur Global, administrateur de facturation, administrateur de Service, administrateur de l’utilisateur et mot de passe Administrateur. 

### <a name="real-time"></a>Temps réel
Voir « Détection en temps réel ».

### <a name="real-time-detection"></a>Détection en temps réel
la détection d’anomalies Hello et l’évaluation des risques hello d’un événement tel qu’une tentative de connexion avant l’événement de hello sont autorisées à tooproceed.

### <a name="remediated-risk-event"></a>Corrigé (événement à risque)
Statut de l’événement risque définie automatiquement par la Protection d’identité, qui indique que l’événement hello risque a été mis à jour à l’aide des mesures correctives standard hello pour ce type d’événement à risque. Par exemple, lors de la réinitialisation de mot de passe utilisateur hello, de nombreux événements risque indiquant que ce mot de passe hello précédente a été compromise sont automatiquement mis à jour.

### <a name="remediation"></a>Correction
Une action toosecure une identité ou un périphérique qui ont été précédemment ou suspectées toobe compromis. Une action de mise à jour restaure l’état sans échec tooa hello identité ou l’appareil et résout les événements précédents risque associés hello identité ou d’appareil.

### <a name="resolved-risk-event"></a>Résolu (événement à risque)
Un statut de l’événement risque défini manuellement par un utilisateur de la Protection d’identité, qui indique que les utilisateur hello d’effectuer une action de mise à jour appropriée en dehors de la Protection de l’identité, cet événement risque de hello doit être considérée comme fermé.

### <a name="risk-event-status"></a>État d’un événement à risque
Une propriété d’un événement à risque, qui indique si l’événement de hello est active et si fermé, raison hello de fermeture.

### <a name="risk-event-type"></a>Type d’événement à risque
Une catégorie pour hello risque d’événement, indiquant le type de hello d’anomalie qui a provoqué hello événement toobe est considéré comme présentant un risque.

### <a name="risk-level-risk-event"></a>Niveau de risque (événement à risque)
Une indication (haute, moyenne ou faible) de gravité hello d’utilisateurs de la Protection d’identité hello risque événement toohelp établir des priorités hello informerons organisation de tootheir tooreduce hello risque. 

### <a name="risk-level-sign-in"></a>Niveau de risque (connexion)
Une indication (haute, moyenne ou faible) de vraisemblance de hello que pour une connexion complémentaire spécifique, une autre personne tente d’identité de l’utilisateur toouse hello.

### <a name="risk-level-user-compromise"></a>Niveau de risque (compromission de l’utilisateur)
Indication (haute, moyenne ou faible) de probabilité hello qu’une identité a été compromise.

### <a name="risk-level-vulnerability"></a>Niveau de risque (vulnérabilité)
Une indication (haute, moyenne ou faible) de gravité hello d’utilisateurs de la Protection d’identité toohelp hello vulnérabilité établir des priorités hello informerons organisation de tootheir tooreduce hello risque.

### <a name="secure-identity"></a>Sécurisé (identité)
Prendre des mesures correctives comme un changement de mot de passe ou d’un ordinateur réinitialisation toorestore un état de tooan une identité potentiellement compromis.

### <a name="security-policy"></a>Stratégie de sécurité
Ensemble de règles et conditions de stratégie. Une stratégie peut être appliquée tooentities tels que les utilisateurs, groupes, applications, appareils, des plateformes d’appareils, États des appareils, plages d’adresses IP et Auth2.0 les types de clients. Lorsqu’une stratégie est activée, elle est évaluée chaque fois qu’une entité incluse dans la stratégie de hello est émise à un jeton pour une ressource.

### <a name="sign-in-v"></a>Se connecter (v)
identité de tooan tooauthenticate dans Azure Active Directory.

### <a name="sign-in-n"></a>Connexion (n)
processus de Hello ou action de l’authentification dans Azure Active Directory et les événements hello qui capture cette opération.

### <a name="sign-in-from-anonymous-ip-address"></a>Connexion à partir d’une adresse IP anonyme
Événement à risque déclenché après une réussite de connexion à partir d’une adresse IP ayant été identifiée comme adresse IP proxy anonyme.

### <a name="sign-in-from-infected-device"></a>Connexion à partir d’un appareil infecté
Un événement à risque déclenché lorsqu’une connexion à provient d’une adresse IP connue toobe utilisé par un ou plusieurs périphériques compromis, qui tentent de toocommunicate avec un serveur robot activement.

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a>Connexion à partir d’une adresse IP affichant une activité suspecte
Événement à risque déclenché après une réussite de connexion à partir d’une adresse IP associée à un grand nombre de tentatives de connexion effectuées pendant une courte période sur plusieurs comptes d’utilisateur.

### <a name="sign-in-from-unfamiliar-location"></a>Connexion à partir d’un emplacement inconnu
Événement à risque déclenché lorsqu’un utilisateur parvient à se connecter depuis un nouvel emplacement (adresse IP, latitude/longitude et ASN).

### <a name="sign-in-risk"></a>Risque à la connexion
Voir « Niveau de risque (connexion) »

### <a name="sign-in-risk-policy"></a>Stratégie en matière de risque à la connexion
Une stratégie d’accès conditionnel qui prend la valeur hello risque tooa spécifique connectez-vous et applique les limitations de risques selon les règles et conditions prédéfinies.

### <a name="user-compromise-risk"></a>Risque de compromission de l’utilisateur
Voir « Niveau de risque (compromission de l’utilisateur) »

### <a name="user-risk"></a>Risque de l’utilisateur
Voir « Niveau de risque (compromission de l’utilisateur) ».

### <a name="user-risk-policy"></a>Stratégie de risque d’utilisateur
Une stratégie d’accès conditionnel qui considère hello connectez-vous et applique les limitations de risques selon les règles et conditions prédéfinies.

### <a name="users-flagged-for-risk"></a>Utilisateurs associés à un indicateur de risque
Utilisateurs associés à des événements à risque actifs ou corrigés

### <a name="vulnerability"></a>Vulnérabilité
Une configuration ou une condition dans Azure Active Directory, qui rend tooexploits sensibles du répertoire hello ou les menaces.

## <a name="see-also"></a>Voir aussi
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

