---
title: "aaaRDG et le serveur Azure MFA à l’aide de RADIUS | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui va vous aider à déployer la passerelle de bureau à distance (RD) et de serveur Azure multi-Factor Authentication utilisant RADIUS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Passerelle des services Bureau à distance et serveur Multi-Factor Authentication avec RADIUS
Passerelle de bureau à distance (RD) utilise souvent, les utilisateurs tooauthenticate de Services de stratégie réseau (NPS) locaux hello. Cet article décrit comment tooroute RADIUS demande hello passerelle Bureau à distance (via hello du serveur NPS local) toohello serveur multi-Factor Authentication. Hello combinaison de passerelle Bureau à distance et de l’authentification Multifacteur Azure signifie que les utilisateurs peuvent accéder à leur environnement de travail à partir de n’importe quel emplacement lors de l’exécution de l’authentification forte. 

Étant donné que l’authentification Windows pour les services Terminal Server n’est pas prise en charge de Server 2012 R2, utilisez toointegrate RADIUS et de la passerelle Bureau à distance avec le serveur de l’authentification Multifacteur. 

Installez hello serveur Azure multi-Factor Authentication sur un serveur distinct, les proxys hello RADIUS demande sauvegarder toohello NPS sur le serveur de passerelle Bureau à distance de hello. Une fois le serveur NPS aura validé le mot de passe et le nom d’utilisateur hello, elle retourne un toohello réponse serveur multi-Factor. Ensuite, hello serveur MFA effectue hello second facteur d’authentification et retourne une passerelle toohello de résultat.

## <a name="prerequisites"></a>Composants requis

- Un serveur Azure MFA joint à un domaine. Si vous n’en avez déjà installé, suivez les étapes de hello dans [prise en main de hello serveur Azure multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
- Une passerelle Bureau à distance qui s’authentifie avec les services de stratégie réseau.

## <a name="configure-hello-remote-desktop-gateway"></a>Configurer hello passerelle Bureau à distance
Configurer tooan de l’authentification RADIUS hello passerelle Bureau à distance toosend serveur Azure multi-Factor Authentication. 

1. Dans le Gestionnaire de passerelle Bureau à distance, cliquez sur le nom de serveur hello et sélectionnez **propriétés**.
2. Accédez toohello **magasin de stratégies de bureau à distance** onglet et sélectionnez **serveur Central exécutant NPS**. 
3. Ajoutez un ou plusieurs serveurs de l’authentification multifacteur de Azure en tant que serveurs RADIUS en entrant le nom de hello ou adresse IP de chaque serveur. 
4. Créez un secret partagé pour chaque serveur.

## <a name="configure-nps"></a>Configuration NPS
Hello passerelle Bureau à distance utilise NPS toosend hello RADIUS demande tooAzure multi-Factor Authentication. tooconfigure NPS, tout d’abord, vous modifiez les paramètres de délai d’attente hello tooprevent hello passerelle Bureau à distance à partir de l’expiration du délai avant la fin de la vérification de hello en deux étapes. Ensuite, vous mettez à jour des authentifications RADIUS NPS tooreceive à partir de votre serveur de l’authentification Multifacteur. Utilisez hello suivant la procédure tooconfigure NPS :

### <a name="modify-hello-timeout-policy"></a>Modifier la stratégie de délai d’attente hello

1. Dans NPS, ouvrez hello **Clients et serveurs RADIUS** menu Bonjour gauche colonne et sélectionnez **des groupes de serveurs RADIUS distants**. 
2. Sélectionnez hello **groupe de serveur de passerelle TS**. 
3. Accédez toohello **l’équilibrage de charge** onglet. 
4. Modifier les deux hello **nombre de secondes sans réponse avant que la requête est considérée comme supprimée** et hello **nombre de secondes entre les demandes quand le serveur est identifié comme étant indisponible** toobetween 30 et 60 secondes. (Si vous trouvez que ce serveur hello expire toujours lors de l’authentification, vous pouvez revenir ici et augmenter le nombre de hello de secondes.)
5. Accédez toohello **/compte d’authentification** et vérifiez que les ports RADIUS hello spécifié hello de correspondance que hello serveur multi-Factor Authentication est à l’écoute sur les ports.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>Préparer les authentifications de tooreceive NPS à partir de hello serveur MFA

1. Avec le bouton droit **Clients RADIUS** sous Clients RADIUS et serveurs Bonjour gauche colonne et sélectionnez **nouveau**.
2. Ajoutez hello serveur Azure multi-Factor Authentication comme client RADIUS. Choisissez un nom convivial et spécifiez un secret partagé.
3. Ouvrez hello **stratégies** menu Bonjour gauche colonne et sélectionnez **stratégies de demande de connexion**. Vous devez voir une stratégie appelée STRATÉGIE D’AUTORISATION DE PASSERELLE TS créée lors de la configuration de la passerelle RD. Cette stratégie transfère les demandes RADIUS toohello serveur multi-Factor.
4. Cliquez avec le bouton droit sur **STRATÉGIE D’AUTORISATION DE PASSERELLE TS** et sélectionnez **Dupliquer la stratégie**. 
5. Ouvrez toohello de stratégie et accédez de nouveau hello **Conditions** onglet.
6. Ajouter une condition qui correspond au nom convivial du Client avec le nom convivial du hello défini à l’étape 2 pour le client RADIUS du serveur Azure multi-Factor Authentication de hello de hello. 
7. Accédez toohello **paramètres** onglet et sélectionnez **authentification**.
8. Modifier hello fournisseur d’authentification trop**authentifier les demandes sur ce serveur**. Cette stratégie garantit que lorsque le serveur NPS reçoit une demande RADIUS hello serveur Azure MFA, l’authentification de hello se produit localement au lieu d’envoyer une demande RADIUS arrière toohello serveur Azure multi-Factor Authentication, entraînant une condition de boucle. 
9. tooprevent une condition de boucle, assurez-vous qu’une nouvelle stratégie hello est placée au-dessus de stratégie d’origine de hello Bonjour **stratégies de demande de connexion** volet.

## <a name="configure-azure-multi-factor-authentication"></a>Configuration d’Azure Multi-Factor Authentication

Hello serveur Azure multi-Factor Authentication est configuré en tant que proxy RADIUS entre la passerelle Bureau à distance et le serveur NPS.  Il doit être installé sur un serveur appartenant à un domaine qui est distinct du serveur de passerelle Bureau à distance hello. Utilisez hello suivant hello tooconfigure de procédure serveur Azure multi-Factor Authentication.

1. Ouvrez hello serveur Azure multi-Factor Authentication et sélectionnez l’icône de l’authentification RADIUS hello. 
2. Vérifiez hello **activer l’authentification RADIUS** case à cocher.
3. Sous l’onglet de Clients hello, vérifiez les ports hello correspondent à ce qui est configuré dans NPS, puis sélectionnez **ajouter**.
4. Ajouter une adresse IP hello du serveur de passerelle Bureau à distance (facultatif) nom de l’application et un secret partagé. Hello partagé secrètes besoins toobe même hello sur hello serveur Azure multi-Factor Authentication et de passerelle Bureau à distance.
3. Accédez toohello **cible** onglet et sélectionnez hello **ou les serveurs RADIUS** case d’option.
4. Sélectionnez **ajouter** et entrez l’adresse IP de hello, secret partagé et les ports du serveur NPS de hello. Sauf si vous utilisez un serveur NPS central, hello client RADIUS et RADIUS cible sont hello même. secret partagé de Hello doit correspondre à une configuration de hello Bonjour section client RADIUS du serveur NPS de hello.

![Authentification RADIUS](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Étapes suivantes

- Intégrer Azure MFA et les [applications web IIS](multi-factor-authentication-get-started-server-iis.md)

- Obtenir des réponses hello [le Forum aux questions sur Azure multi-Factor Authentication](multi-factor-authentication-faq.md)
