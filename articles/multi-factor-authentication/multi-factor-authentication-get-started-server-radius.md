---
title: "aaaRADIUS l’authentification et le serveur Azure MFA | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui va vous aider à déployer l’authentification RADIUS et serveur Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Intégration de l'authentification RADIUS avec le serveur Azure Multi-Factor Authentication
Utilisez la section de l’authentification RADIUS hello du serveur Azure MFA tooenable et configurer l’authentification RADIUS. RADIUS est une norme de protocole tooaccept les demandes d’authentification et tooprocess ces demandes. Hello serveur Azure multi-Factor Authentication agit comme un serveur RADIUS. Insérer entre votre client RADIUS (un équipement VPN) et votre cible d’authentification, ce qui pourrait être Active Directory (AD), un annuaire LDAP ou un autre tooadd de serveur RADIUS Azure multi-Factor Authentication. Pour Azure multi-Factor Authentication (MFA) toofunction, vous devez configurer hello serveur Azure MFA afin qu’il puisse communiquer avec les serveurs client hello et cible d’authentification hello. Hello serveur Azure MFA accepte les requêtes à partir d’un client RADIUS, valide les informations d’identification par rapport à la cible d’authentification hello, ajoute Azure multi-Factor Authentication et envoie une réponse au client RADIUS toohello précédent. demande d’authentification Hello réussit uniquement si l’authentification principale de hello et hello Azure multi-Factor Authentication réussissent.

> [!NOTE]
> Hello serveur MFA prend uniquement en charge PAP (protocole d’authentification de mot de passe) et MSCHAPv2 (Microsoft Challenge Handshake Authentication Protocol) RADIUS protocoles lorsqu’il agit comme un serveur RADIUS.  D’autres protocoles, tels que EAP protocole (extensible authentication protocol), utilisable lorsque le serveur MFA hello agit comme un serveur RADIUS tooanother proxy RADIUS qui prend en charge ce protocole.
>
> Dans cette configuration, des jetons SMS et OATH unidirectionnels ne fonctionnent pas car hello serveur MFA ne peut pas initier une réponse correcte de demande d’accès RADIUS à l’aide d’autres protocoles.

![Authentification RADIUS](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Ajouter un client RADIUS
authentification RADIUS tooconfigure, installation hello serveur Azure multi-Factor Authentication sur un serveur Windows. Si vous avez un environnement Active Directory, serveur de hello doit être domaine toohello jointes à l’intérieur du réseau de hello. Utilisez hello suivant hello tooconfigure de procédure serveur Azure multi-Factor Authentication :

1. Bonjour serveur Azure multi-Factor Authentication, cliquez sur l’icône de l’authentification RADIUS hello dans le menu de gauche hello.
2. Vérifiez hello **activer l’authentification RADIUS** case à cocher.
3. Sous l’onglet de Clients hello, modifiez hello d’authentification et les ports de gestion si hello service Azure MFA RADIUS doit toolisten pour les demandes RADIUS sur des ports non standard.
4. Cliquez sur **Add**.
5. Entrez l’adresse IP de hello de hello équipement ou du serveur qui s’authentifieront toohello serveur Azure multi-Factor Authentication, un nom d’application (facultatif) et un secret partagé.

  nom de l’application Hello apparaît dans les rapports d’Azure multi-Factor Authentication et peut être affichée dans les messages d’authentification SMS ou application Mobile.

  Hello partagé secrète besoins toobe hello identique sur les deux hello du serveur Azure multi-Factor Authentication et équipement ou du serveur.

6. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et authentification toomulti-facteur de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de la vérification en deux étapes, laissez la zone de hello désactivée.
7. Vérifiez hello **activer les jeton OATH secours** zone Si vous souhaitez que les codes d’accès OATH toouse à partir d’applications de vérification mobile comme un appel téléphonique hors-bande toohello de secours, SMS, ou notification push.
8. Cliquez sur **OK**.

Répétez les étapes 4 à 8 tooadd autant de clients RADIUS supplémentaires que nécessaire.

## <a name="configure-your-radius-client"></a>Configurer votre client RADIUS

1. Cliquez sur hello **cible** onglet.
2. Si hello serveur Azure MFA est installé sur un serveur appartenant à un domaine dans un environnement Active Directory, sélectionnez le domaine Windows.
3. Si les utilisateurs doivent être authentifiés par rapport à un répertoire LDAP, sélectionnez la **liaison LDAP**.

  toouse une liaison LDAP, cliquez sur icône d’intégration d’annuaire hello et modifier la configuration LDAP hello sur l’onglet Paramètres de hello afin que hello Server peut lier tooyour active. Vous trouverez des instructions pour configurer LDAP Bonjour [guide de configuration de serveur Proxy LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Si les utilisateurs doivent être authentifiés par rapport à un autre serveur RADIUS, sélectionnez ce serveur RADIUS.
5. Cliquez sur **ajouter** tooconfigure hello toowhich hello serveur Azure MFA sera proxy messages hello du serveur RADIUS des demandes.
6. Dans la boîte de dialogue Ajouter un serveur RADIUS hello, entrez hello adresse IP de serveur RADIUS de hello et un secret partagé.

  Hello partagé secrète besoins toobe hello identique sur les deux hello du serveur Azure multi-Factor Authentication et le serveur RADIUS. Modifier le port d’authentification hello et le port de gestion si des ports différents sont utilisés par le serveur RADIUS de hello.

7. Cliquez sur **OK**.
8. Ajouter hello serveur Azure MFA comme un client RADIUS dans hello autre serveur RADIUS afin qu’il puisse traiter les demandes d’accès provenance tooit hello serveur Azure MFA. Utilisez hello partagée secret configuré Bonjour serveur Azure multi-Factor Authentication.

Répétez ces étapes tooadd davantage de serveurs RADIUS et configurer l’ordre de hello quels Bonjour Azure MFA Server doit les appeler à hello **monter** et **Descendre** boutons.

Configuration du serveur Azure multi-Factor Authentication hello est terminée. Hello serveur écoute sur les ports hello configuré pour les demandes d’accès RADIUS à partir de clients de hello configuré.   

## <a name="radius-client-configuration"></a>Configuration du client RADIUS
tooconfigure hello client RADIUS, suivez les indications de hello :

* Configurer votre tooauthenticate équipement ou du serveur via l’adresse IP toohello Azure multi-Factor d’authentification du serveur RADIUS, qui agira en tant que serveur RADIUS de hello.
* Utilisez hello partagée secret a été configuré précédemment.
* Configurer hello RADIUS délai too30-60 (secondes) pour qu’il y a temps toovalidate hello de l’utilisateur, effectuer une vérification en deux étapes, réception de la réponse et demande d’accès RADIUS toohello de répondre.
