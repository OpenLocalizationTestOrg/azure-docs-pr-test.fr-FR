---
title: "codes d’erreur de rapport aaaSign sur l’activité dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "Informations de référence des codes d’erreur des rapports d’activité des connexions."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Codes d’erreur de rapport activité de connexion dans le portail d’Azure Active Directory hello

Informations hello fournies par le rapport de connexions utilisateur hello, trouver tooquestions réponses telles que :

- Qui s’est connecté à l’aide d’Azure Active Directory ?
- À quelles applications l’utilisateur s’est-il connecté ?
- Quelles connexions ont échoué ? Le cas échéant, pourquoi ?

Cette erreur de hello rubrique répertorie les codes et hello descriptions associées. 

## <a name="how-can-i-display-failed-sign-ins"></a>Comment afficher les connexions en échec ? 

Votre première entrée tooall de point de connexion activités données  **[connexions](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  Bonjour **activité** section de **Azure Active**.


![Activité de connexion](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Activité de connexion")


Dans votre rapport de connexions, vous pouvez afficher toutes les connexions en échec en sélectionnant **Échec** pour **État de la connexion**.


![Activité de connexion](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Activité de connexion")

En cliquant sur un élément de liste de hello affiché, ouvre hello **détails de l’activité : connexions** panneau. Cette vue fournit tous les détails de hello Azure Active Directory effectue le suivi sur les connexions, y compris hello **code d’erreur de connexion** et un **raison de l’échec**.

![Activité de connexion](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Activité de connexion")


En tant qu’une autre toousing hello données de connexions hello tooaccess portail Azure, vous pouvez également utiliser hello [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).


Hello section suivante vous offre une vue d’ensemble complète de toutes les erreurs possibles et hello des descriptions liées. 

## <a name="error-codes"></a>Codes d’erreur

| Error| Description |
| --- | --- |
| 50001| principal du service Hello nommé X dans le locataire hello nommé Y est introuvable. Cela peut se produire si l’application hello n’a pas été installée par l’administrateur de hello du client de hello. Ou principal de ressource est introuvable dans le répertoire de hello ou n’est pas valide|
| 50008| Assertion SAML sont manquantes ou mal configurées dans le jeton de hello.|
| 50011| adresse de réponse Hello est manquant, mal configuré ou ne correspondent pas aux adresses de réponse configurés pour l’application hello.|
| 50053| Compte est verrouillé, car l’utilisateur a essayé de toosign dans trop de fois avec un ID d’utilisateur incorrect ou le mot de passe.|
| 50054| Un ancien mot de passe est utilisé pour l’authentification.|
| 50055| Mot de passe non valide, mot de passe arrivé à expiration entré.|
| 50057| Le compte d’utilisateur est désactivé.|
| 50058| Aucune information sur l’identité de l’utilisateur ne se trouve entre fourni les informations d’identification ou d’utilisateur est introuvable dans le client ou une demande de connexion en mode silencieux a été envoyée, mais aucun utilisateur n’est connecté ou Service a été utilisateur de hello tooauthenticate impossible.|
| 50074| Une authentification forte (second facteur) est requise.|
| 50079| Utilisateur doit tooenroll authentification à deux facteurs|
| 50126| Nom d’utilisateur ou mot de passe non valides, ou nom d’utilisateur ou mot de passe locaux non valides.|
| 50131| Utilisation dans différentes erreurs d’accès conditionnel. Périphérique de Windows incorrecte par exemple, demande bloquée en raison de toosuspicious activité, la stratégie d’accès et la stratégie de sécurité décisions d’état.|
| 50133| Session n’est pas valide en raison de tooexpiration ou de modification de mot de passe récente.|
| 50144| Le mot de passe Active Directory de l’utilisateur est arrivé à expiration.|
| 65 001| Application X dépourvu d’autorisation tooaccess application Y ou hello autorisation a été révoquée. Ou hello utilisateur ou un administrateur n’a pas consenti application hello de toouse avec ID X. Send une demande d’autorisation interactive pour cet utilisateur et des ressources. Ou hello utilisateur ou un administrateur a consenti pas d’application de hello toouse avec ID X. Send un tooact administrateur client de tooyour de demande d’autorisation pour le compte d’application de hello : Y pour la ressource : Z.|
| 65005| application Hello requis liste d’accès de ressource ne contient pas les applications pouvant être découverte par ressource de hello ou application cliente de hello a demandé tooresource d’accès qui n’a pas été spécifié dans sa liste d’accès de ressource requise ou de retour incorrect du service de graphique demande ou ressource introuvable.|
| 70001| application Hello nommée X dans le locataire hello nommé Y est introuvable. Cela peut se produire si l’application hello n’a pas été installée par Bonjour administrateur de client de hello ou tooby ayant reçu un consentement n’importe quel utilisateur de client de hello. Vous avez peut-être envoyé votre client de mauvais toohello de demande d’authentification.|
| 80001| Agents d’authentification non disponibles.|
| 80002| La demande de validation du mot de passe de l’Agent d’authentification est arrivée à expiration.|
| 80003| Réponse non valide reçue par l’Agent d’authentification.|
| 80004| Nom d’utilisateur principal (UPN) incorrect utilisé dans la demande de connexion.|
| 80005| Agent d’authentification : une erreur s’est produite.|
| 80007| TooActive de tooconnect Impossible de l’Agent d’authentification Active.|
| 80010| Mot de passe d’authentification Agent toodecrypt impossible.|
| 81001| Le ticket Kerberos de l’utilisateur est trop volumineux.|
| 81002| Ticket Kerberos de l’utilisateur toovalidate impossible.|
| 81003| Ticket Kerberos de l’utilisateur toovalidate impossible.|
| 81004| Échec de l’authentification Kerberos.|
| 81008| Ticket Kerberos de l’utilisateur toovalidate impossible.|
| 81009| Ticket Kerberos de l’utilisateur toovalidate impossible.|
| 81010| Échec de l’authentification unique transparente, car le ticket Kerberos de l’utilisateur hello a expiré ou n’est pas valide.|
| 81011| Toofind Impossible d’objet d’utilisateur basé sur les informations de ticket Kerberos de l’utilisateur hello.|
| 81012| utilisateur Hello lors de la tentative toosign dans tooAzure AD diffère de l’utilisateur hello connecté à l’appareil de hello.|
| 81013| Toofind Impossible d’objet d’utilisateur basé sur les informations de ticket Kerberos de l’utilisateur hello.|
| 90014| Utilisé dans différents cas lorsqu’un champ attendu n’est pas présent dans les informations d’identification hello.|
| 90093| Graphique retourné avec le code d’erreur interdit pour demande de hello.|



## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez hello [-in Rapports d’activité dans le portail d’Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md).

