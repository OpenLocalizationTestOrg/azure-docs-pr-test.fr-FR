---
title: "aaaConfigure serveur Azure MFA pour la haute disponibilité | Documents Microsoft"
description: "Déployez plusieurs instances du serveur Azure Multi-Factor Authentication dans les configurations qui fournissent une haute disponibilité."
services: multi-factor-authentication
keywords: Azure MFA,
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Configurer un serveur Azure Multi-Factor Authentication pour la haute disponibilité

tooachieve haute disponibilité avec votre déploiement d’Azure MFA de serveur, vous devez toodeploy plusieurs serveurs d’authentification Multifacteur. Cette section fournit des informations sur une conception d’équilibrage de la charge de tooachieve votre cible de haute disponibilité dans votre déploiement Azure MFS Server.

## <a name="mfa-server-overview"></a>Vue d’ensemble du serveur MFA

Hello architecture de service de serveur de l’authentification Multifacteur Azure comprend plusieurs composants comme indiqué dans hello suivant schéma :

 ![Architecture du serveur MFA](./media/mfa-server-high-availability/mfa-ha-architecture.png)

Un serveur de l’authentification Multifacteur est un serveur Windows qui dispose d’un logiciel hello Azure multi-Factor Authentication. instance de serveur MFA Hello doit être activé par hello Service de l’authentification Multifacteur dans Azure toofunction. Plusieurs serveurs MFA peuvent être installés localement.

Hello premier serveur de l’authentification Multifacteur est installé est hello serveur maître de l’authentification Multifacteur lors de l’activation par hello du Service Azure MFA par défaut. serveur de l’authentification Multifacteur maître Hello possède une copie accessible en écriture de base de données PhoneFactor.pfdata hello. Les installations ultérieures d’instances de serveur MFA sont appelées instances subordonnées. instances subordonnées de l’authentification Multifacteur Hello ont une copie en lecture seule de la base de données PhoneFactor.pfdata hello. Les serveurs MFA répliquent les informations par appel de procédure distante (RPC). Tous les serveurs de l’authentification Multifacteur doit collectivement être joints à un domaine ou des informations tooreplicate autonome.

Maître de l’authentification Multifacteur et esclave serveurs MFA communiquent avec hello Service de l’authentification Multifacteur lors de l’authentification à deux facteurs est requise. Par exemple, lorsqu’un utilisateur tente de toogain accès tooan application qui nécessite l’authentification à deux facteurs, hello utilisateur sera tout d’abord être authentifié par un fournisseur d’identité, telles que Active Directory (AD).

Après une authentification réussie avec Active Directory, hello MFA Server communique avec hello Service d’authentification Multifacteur. Hello serveur MFA attend une notification de hello Service MFA tooallow ou refuser l’application de toohello accès hello utilisateur.

Si le serveur maître de l’authentification Multifacteur hello est mis hors connexion, les authentifications peuvent encore être traitées, mais les opérations qui nécessitent la base de données de l’authentification Multifacteur modifications toohello ne peut pas être traitées. (Exemples : hello Ajout d’utilisateurs libre-service les modifications de code confidentiel et modifiez les informations de l’utilisateur)

## <a name="deployment"></a>Déploiement

Envisagez de hello suivant les points importants pour l’équilibrage de charge serveur Azure MFA et ses composants associés.

* **À l’aide de la haute disponibilité RADIUS standard tooachieve**. Si vous utilisez des serveurs Azure MFA en tant que serveurs RADIUS, vous pouvez potentiellement configurer un seul serveur MFA en tant que cible d’authentification RADIUS principale et les autres serveurs Azure MFA en tant que cibles d’authentification secondaires. Toutefois, cette disponibilité tooachieve de méthode ne peut pas être pratique car vous devez attendre un toooccur période de délai d’attente en cas d’échec de l’authentification sur la cible de l’authentification principale hello avant que vous pouvez être authentifié par rapport à l’authentification secondaire hello cible. Il est plus efficace tooload solde hello le trafic RADIUS entre un client RADIUS hello et serveurs RADIUS de hello (dans ce cas, les serveurs de l’authentification Multifacteur Azure hello agissant en tant que serveurs RADIUS) afin que vous pouvez configurer des clients RADIUS de hello avec elles peuvent pointer vers une URL unique.
* **Toomanually devez promouvoir des instances subordonnées de l’authentification Multifacteur**. Si le serveur de l’authentification Multifacteur Azure hello maître est mis hors connexion, hello Azure MFA serveurs secondaires continuent tooprocess les demandes de l’authentification Multifacteur. Toutefois, jusqu'à ce qu’un serveur maître de l’authentification Multifacteur est disponible, administrateurs ne peuvent pas ajouter des utilisateurs ou modifier les paramètres d’authentification Multifacteur, et les utilisateurs ne peuvent pas modifier les à l’aide du portail de l’utilisateur hello. Promotion d’un rôle de maître de l’authentification Multifacteur esclave toohello est toujours un processus manuel.
* **Possibilité de séparation des composants**. Hello Azure MFA Server comprend plusieurs composants qui peuvent être installés sur hello la même instance de Windows Server ou sur différentes instances. Ces composants incluent hello portail de l’utilisateur, Service Web d’application Mobile et l’adaptateur ADFS hello (agent). Cette séparation rend possible toouse Bonjour Proxy d’Application Web toopublish Bonjour portail de l’utilisateur et le serveur Web Mobile application du réseau de périmètre hello. Une telle configuration ajoute toohello sécurité globale de votre conception, comme indiqué dans hello suivant schéma. Hello MFA portail de l’utilisateur et le serveur Web Mobile application peuvent être déployés dans des configurations d’équilibrage de la charge de haute disponibilité.

   ![Serveur MFA avec un réseau de périmètre](./media/mfa-server-high-availability/mfasecurity.png)

* **Mot de passe à usage unique (OTP) par SMS (également appelé SMS unidirectionnels) nécessite l’utilisation de hello de sessions rémanentes si le trafic est équilibrée**. SMS unidirectionnelle est une option d’authentification qui provoque les utilisateurs de hello serveur MFA toosend hello un message texte contenant un secret à usage unique. utilisateur de Hello entre les hello secret à usage unique dans un Bonjour toocomplete de fenêtre d’invite stimulation d’authentification Multifacteur. Si vous chargez le solde de serveurs de l’authentification Multifacteur Azure, hello même serveur qui a traité la demande d’authentification initiale hello doit être hello serveur qui reçoit le message de salutation OTP à partir de l’utilisateur de hello ; Si un autre serveur de l’authentification Multifacteur reçoit hello réponse du secret à usage unique, la demande d’authentification hello échoue. Pour plus d’informations, consultez [un mot de passe via SMS ajouté tooAzure serveur MFA](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **Équilibrage de la charge des déploiements de hello portail de l’utilisateur et de Service Web d’application Mobile nécessitent des sessions rémanentes**. Si vous êtes l’équilibrage de charge hello du portail de l’utilisateur l’authentification Multifacteur et hello Service Web d’application Mobile, chaque session doit toostay sur hello même serveur.

## <a name="high-availability-deployment"></a>Déploiement de la haute disponibilité

Hello diagramme suivant illustre une implémentation d’équilibrage de la charge à haute disponibilité complète de l’authentification Multifacteur Azure et de ses composants, ainsi que d’ADFS pour référence.

 ![Implémentation de la haute disponibilité du serveur Azure MFA](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Notez hello éléments pour la zone de hello en conséquence numéroté de hello précédant diagramme suivants.

1. Hello deux serveurs de l’authentification Multifacteur Azure (MFA1 et MFA2) sont à charge équilibrée (mfaapp.contoso.com) de charge et sont toouse configuré un port statique (4443) tooreplicate hello PhoneFactor.pfdata base de données. Hello SDK du Service Web est installé sur chacun des hello MFA tooenable communication entre les serveurs sur le port TCP 443 avec des serveurs ADFS hello. serveurs de l’authentification Multifacteur Hello sont déployés dans une configuration d’équilibrage de la charge sans état. Toutefois, si vous souhaitiez toouse OTP par SMS, vous devez utiliser l’équilibrage de charge avec état.
   ![Serveur Azure MFA - Haute disponibilité du serveur d’applications](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > Étant donné que RPC utilise des ports dynamiques, il est déconseillé pare-feu tooopen plage toohello de ports dynamiques RPC peut utiliser. Si vous avez un pare-feu **entre** vos serveurs d’applications de l’authentification Multifacteur, vous devez configurer hello serveur MFA toocommunicate sur un port statique hello le trafic de réplication entre les serveurs esclave et maître et ouvrir ce port sur votre pare-feu. Vous pouvez forcer les ports statiques hello en créant une valeur de Registre DWORD sur ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` appelée ```Pfsvc_ncan_ip_tcp_port``` et la définition de valeur de hello tooan port statique disponible. Toujours les connexions sont initiées par le maître de toohello serveurs MFA hello esclave, port statique de hello est requis uniquement sur les principales hello, mais étant donné que vous pouvez promouvoir un maître de hello toobe subordonnée à tout moment, vous devez définir les ports statiques hello sur tous les serveurs d’authentification Multifacteur.

2. les serveurs de l’application utilisateur/MFA du portail Mobile Hello deux (l’authentification Multifacteur-UP-MAS1 et l’authentification Multifacteur-UP-MAS2) sont à charge équilibrée dans un **avec état** configuration (mfa.contoso.com). Rappelez-vous que les sessions persistantes sont requis pour l’équilibrage de charge hello portail utilisateur de l’authentification Multifacteur et du Service d’applications mobiles.
   ![Serveur Azure MFA - Haute disponibilité du portail utilisateur et du service d’applications mobiles](./media/mfa-server-high-availability/mfaportal.png)
3. batterie de serveurs ADFS Hello est l’équilibrage de charge et publié toohello Internet via l’équilibrage de la charge des serveurs proxy ADFS dans un réseau de périmètre hello. Chaque serveur ADFS utilise hello ADFS agent toocommunicate avec hello les serveurs de l’authentification Multifacteur Azure à l’aide d’une URL avec équilibrage de charge unique (mfaapp.contoso.com) sur le port TCP 443.

## <a name="next-steps"></a>Étapes suivantes

* [Installer et configurer un serveur Azure MFA](multi-factor-authentication-get-started-server.md)
