---
title: 'Azure AD Connect : authentification directe - Forum aux questions | Documents Microsoft'
description: "Elles en sonttrop de réponses aux questions sur l’authentification Azure Active Directory pass-through."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Authentification directe Azure Active Directory : forum aux questions

Dans cet article, nous répondons au forum aux questions sur l’authentification directe d’Azure Active Directory (Azure AD). N’hésitez pas à le consulter régulièrement, du contenu nouveau y est fréquemment ajouté.

>[!IMPORTANT]
>fonctionnalité d’authentification directe Hello est actuellement en version préliminaire.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Quels hello Azure AD méthodes de connexion - authentification directe, synchronisation de hachage de mot de passe et les Services de fédération Active Directory (AD FS) - dois-je choisir ?

Cela dépend de votre environnement local et des exigences de votre organisation. Lisez cet article pour une [comparaison de hello des méthodes de connexion Azure AD différents](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>L’authentification directe est-elle une fonctionnalité gratuite ?

Authentification directe est une fonctionnalité gratuite et vous n’avez pas besoin des éditions payantes d’Azure AD toouse il. Il reste disponible lors de la fonctionnalité de hello rendue publique.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>L’authentification directe est-elle disponible dans [Microsoft Cloud Allemagne](http://www.microsoft.de/cloud-deutschland) et [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/) ?

Non, authentification directe est uniquement disponible dans l’instance d’à l’échelle mondiale hello d’Azure AD.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>[L’accès conditionnel](../active-directory-conditional-access.md) fonctionne-t-il avec l’authentification directe ?

Oui, toutes les fonctionnalités, y compris l’authentification multifacteur Azure, fonctionnent avec l’authentification directe.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Authentification directe prend-il en charge les « Autres ID » comme nom d’utilisateur hello, au lieu de « userPrincipalName » ?

Oui. Prend en charge de l’authentification directe `Alternate ID` comme hello nom d’utilisateur configuré dans Azure AD Connect comme [ici](active-directory-aadconnect-get-started-custom.md). Toutes les applications Office 365 ne prennent pas en charge `Alternate ID`. Consultez la documentation de l’application toohello spécifique pour l’instruction de prise en charge hello.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>Synchronisation du hachage de mot de passe agit comme authentification de secours via tooPass ?

Non, la synchronisation du hachage de mot de passe n’est pas une générique tooPass via l’authentification de secours. Elle agit uniquement comme solution de secours pour les [scénarios que l’authentification directe ne prend pas en charge aujourd'hui](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid utilisateur échecs de connexion, vous devez configurer l’authentification directe pour [haute disponibilité](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>Puis-je installer un [Proxy d’Application Azure AD](../active-directory-application-proxy-get-started.md) connecteur hello même serveur qu’un Agent de l’authentification directe ?

Oui, cette configuration est prise en charge par hello renommé les versions de hello Agent d’authentification pass-through (versions 1.5.193.0 ou version ultérieure).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>De quelles versions d’Azure AD Connect et de quel agent d’authentification directe avez-vous besoin ?

Vous devez utiliser la version 1.1.486.0 ou une version ultérieure pour Azure AD Connect et 1.5.58.0 ou ultérieurement pour hello Agent d’authentification pass-through pour toowork de cette fonctionnalité. Tous les logiciels doivent être installés sur des serveurs avec Windows Server 2012 R2 ou version ultérieure.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>Que se passe-t-il si mon mot de passe a expiré et qu’ils essaient toosign à l’aide de l’authentification directe ?

Si vous avez configuré [l’écriture différée de mot de passe](../active-directory-passwords-update-your-own-password.md) pour un utilisateur spécifique, et si l’utilisateur de hello se connecte à l’aide de l’authentification directe, ils peuvent modifier ou réinitialiser leurs mots de passe. les mots de passe Hello mis à jour Active Directory local tooon comme prévu.

Toutefois, si l’écriture différée de mot de passe n’est pas configurée pour un utilisateur spécifique ou si hello utilisateur ne dispose pas un Azure AD valide licence attribuée, utilisateur de hello ne peut pas mettre à jour son mot de passe dans le cloud de hello. Il ne peut pas mettre à jour son mot de passe même si le mot de passe a expiré. Hello utilisateur voit ce message : « votre organisation ne vous autorise pas tooupdate votre mot de passe sur ce site. Mettre à jour selon la méthode toohello recommandé par votre organisation, ou demandez à votre administrateur si vous avez besoin d’aide. » Hello utilisateur ou un administrateur de hello a tooreset leur mot de passe dans votre annuaire Active Directory local.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>Comment l’authentification directe vous protège-t-elle contre les attaques par recherche exhaustive de mot de passe ?

Pour plus d’informations, consultez [cet article](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>Qu’est-ce que les agents de l’authentification directe communiquent via les ports 80 et 443 ?

- Agents de l’authentification de Hello établissent des requêtes HTTPS sur le port 443 pour toutes les opérations de fonctionnalité.
- Agents d’authentification Hello effectuent des requêtes HTTP sur port 80 toodownload SSL les listes de certificats.

     >[!NOTE]
     >Dans les mises à jour récentes nous hello nombre réduit de ports requis par la fonctionnalité de hello. Si vous disposez des versions antérieures de Azure AD Connect ou hello Agent d’authentification, conserver ces ports ouverts également : 5671, 8080, 9090, 9091, 9350, 9352 et 10100-10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Hello pass-through Authentication Agents peuvent communiquer sur un serveur proxy web sortant ?

Oui. Si WPAD (Web Proxy Auto-Discovery) est activé dans votre environnement local, authentification Agents essayer toolocate automatiquement et utiliser un serveur proxy web sur le réseau de hello.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>Puis-je installer deux ou plusieurs Agents de l’authentification pass-through sur hello même serveur ?

Non, vous ne pouvez installer qu’un seul agent d’authentification directe sur un serveur unique. Si vous souhaitez tooconfigure authentification directe pour la haute disponibilité, suivez les instructions de hello dans ce [article](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) à la place.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>J’utilise déjà Active Directory Federation Services (AD FS) pour la connexion d’Azure AD. Comment basculer il tooPass via l’authentification ?

Si vous avez configuré AD FS en tant que votre méthode de connexion à l’aide d’Assistant de hello Azure AD Connect, modifier la méthode d’authentification de l’utilisateur du hello tooPass-par le biais de l’authentification. Cette modification permet l’authentification directe sur le client de hello et convertit _tous les_ vos domaines fédérés dans des domaines gérés. Toutes les requêtes de connexion suivantes sur votre client sont gérées par l’authentification directe. Actuellement, il est pris en charge impossible dans Azure AD Connect toouse une combinaison d’AD FS et l’authentification directe sur différents domaines.

Si les services AD FS a été configuré en tant que méthode d’authentification hello _en dehors de_ de l’Assistant de connexion hello Azure AD, modifier la méthode d’authentification de l’utilisateur du hello tooPass via l’authentification (à partir de l’option de « Ne configurez pas » hello). Cette modification permet une authentification directe sur le client de hello. Toutefois, tous vos domaines fédérés continuent toouse AD FS pour la connexion. Utiliser PowerShell toomanually convertir certains ou tous ces fédéré domaines tooManaged domaines. Après cela, toutes les requêtes de connexion sur des domaines gérés (_uniquement_) sont gérées par l’authentification directe.

>[!IMPORTANT]
>L’authentification directe ne gère pas la connexion pour les utilisateurs Active Directory dans le cloud uniquement.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>Puis-je utiliser l’authentification directe dans un environnement à plusieurs forêts AD ?

Oui. Les environnements à plusieurs forêts sont pris en charge s’il existe des approbations de forêts entre les forêts AD et si le routage du suffixe de leurs noms est configuré correctement.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>Les agents d’authentification directe fournissent-ils une fonctionnalité d’équilibrage de charge ?

Non, l’installation de plusieurs agents d’authentification directe assure une [haute disponibilité](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), mais pas l’équilibrage de charge. Un ou deux de hello Agents d’authentification peut se terminer la gestion en bloc de hello de demandes de connexion hello.

Demandes de validation de mot de passe qui hello toohandle besoin de l’authentification Agents sont légers. Par conséquent la charge de pointe et moyenne pour la plupart des clients est facilement gérée par deux ou trois agents d’authentification au total.

Nous vous recommandons d’installer des Agents de l’authentification tooyour fermer les contrôleurs de domaine tooimprove connectez-vous latence.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>Puis-je installer hello premier Agent d’authentification directe sur un serveur autre que hello qui s’exécute Azure AD Connect ?

Non, ce scénario n’est _pas_ pris en charge.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>Combien d’agents d’authentification directe dois-je installer ?

Nous vous recommandons :

- d’installer deux ou trois agents d’authentification au total. Cette configuration est suffisante pour la plupart des clients.
- Vous installez tooimprove connectez-vous latence de l’authentification des Agents sur vos contrôleurs de domaine (ou fermer toothem possible).
- Vous assurer que les serveurs (où sont installés les Agents d’authentification) sont ajoutés toohello AD même forêt en tant qu’utilisateurs hello dont les mots de passe doivent toobe validé.

>[!NOTE]
>Il existe une limite système de 12 agents d’authentification par client.

## <a name="how-can-i-disable-pass-through-authentication"></a>Comment désactiver l’authentification directe ?

Réexécutez l’Assistant d’Azure AD Connect hello et modifier la méthode d’authentification de l’utilisateur du hello à partir de la méthode de tooanother authentification directe. Cette modification désactive l’authentification directe sur le client de hello et désinstalle hello Agent d’authentification hello serveur. Vous avez toomanually désinstallation hello Agents d’authentification à partir d’autres serveurs.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>Que se passe-t-il lorsque je désinstalle un agent d’authentification directe ?

Désinstallation d’un Agent de l’authentification directe à partir d’un serveur provoque la toostop acceptant les demandes de connexion. Assurez-vous d’avoir un autre Agent d’authentification en cours d’exécution avant de procéder à cette opération, tooavoid avec rupture utilisateur connectez-vous sur votre client.

## <a name="next-steps"></a>Étapes suivantes
- [**Limitations actuelles**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) : cette fonctionnalité est actuellement en préversion. Découvrez les scénarios pris en charge et ceux qui ne le sont pas.
- [**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : soyez opérationnel avec l’authentification directe Azure AD.
- [**Immersion technique**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.
