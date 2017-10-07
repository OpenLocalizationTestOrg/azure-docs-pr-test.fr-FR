---
title: "aaaChoose une solution d’identité hybride Azure | Documents Microsoft"
description: "Obtenir une compréhension de base des solutions d’identité hybride disponible hello et des recommandations pour vous toomake hello meilleure identité gouvernance décision pour votre organisation."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Solutions d'identité hybride Microsoft
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) solutions d’identité hybride vous permettent d’objets d’annuaire local toosynchronize avec Azure AD pendant encore la gestion de vos utilisateurs locaux. Bonjour première décision toomake lors de la planification toosynchronize que local Windows Server Active Directory avec Azure AD est que vous souhaitez toouse synchronisé identité ou l’identité fédérée. Identités synchronisées et éventuellement des hachages de mot de passe, permettent à vos utilisateurs toouse hello même tooaccess de mot de passe locaux et cloud en ressources de l’organisation. Pour des spécifications de scénario plus avancées, telles que single-sign-on (SSO) ou de l’authentification Multifacteur localement, vous devez les identités toofederate toodeploy les Services de fédération Active Directory (AD FS). 

Plusieurs options sont disponibles pour la configuration d’identités hybrides. Cet article fournit toohelp informations que vous choisissez hello une meilleure pour votre organisation en fonction de la facilité de déploiement et la gestion des identités et des accès spécifique a besoin. Lorsque vous devez décider quel modèle d’identité meilleures le mieux aux besoins de votre organisation, vous devez également toothink sur le temps, l’infrastructure existante, la complexité et coût. Ces facteurs sont différents pour chaque organisation et peuvent changer au fil du temps. Toutefois, si vos besoins changent, vous devez également le modèle identité tooa hello flexibilité tooswitch.

> [!TIP]
> Ces solutions sont toutes fournies par [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="synchronized-identity"></a>Identité synchronisée 
Identité synchronisée est toosynchronize de façon la plus simple de hello locales des objets d’annuaire (utilisateurs et groupes) avec Azure AD. 

![Identité hybride synchronisée](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Alors qu’identité synchronisée est méthode plus rapide et facile de hello, vos utilisateurs doivent toujours toomaintain un mot de passe distinct pour les ressources de cloud. tooavoid, vous pouvez également (éventuellement) [synchroniser un hachage des mots de passe utilisateur](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) tooyour Azure AD active. Synchronisation de mot de passe hachages permet aux utilisateurs toolog dans les ressources d’organisation toocloud avec hello même nom d’utilisateur et mot de passe qu’ils utilisent sur site. Azure AD Connect contrôle régulièrement les modifications apportées à votre répertoire local pour le synchroniser dans votre répertoire Azure AD. Si un attribut utilisateur ou un mot de passe est modifié localement dans Active Directory, il est automatiquement mis à jour dans Azure AD. 

La plupart des organisations qui ont uniquement besoin tooenable leur toosign utilisateurs tooOffice 365 applications SaaS et autres ressources Azure basée sur Active Directory, l’option de synchronisation de mot de passe par défaut hello est recommandée. Si cela ne fonctionne pas pour vous, vous devez toodecide entre l’authentification directe et AD FS.

> [!TIP]
> Les mots de passe utilisateur sont stockées dans les locaux Windows Server Active Directory sous forme de hello d’une valeur de hachage qui représente le mot de passe de l’utilisateur réel hello. Une valeur de hachage est un résultat d’une fonction mathématique unidirectionnelle (hello algorithme de hachage). Il n’existe aucun résultat de hello méthode toorevert d’une version de texte brut toohello fonction à sens unique d’un mot de passe. Vous ne pouvez pas utiliser un toosign de hachage de mot de passe dans le réseau local de tooyour. Lorsque vous choisissez des mots de passe toosynchronize, hachages de mot de passe Azure AD Connect extraits à partir de hello Active Directory local et applique la sécurité supplémentaire, le traitement de hachage de mot de passe toohello avant qu’il soit synchronisé tooAzure AD. Synchronisation de mot de passe peut également servir avec mot de passe tooenable d’écriture différée de mot de passe libre-service réinitialiser dans Azure AD. En outre, vous pouvez activer l’authentification unique (SSO) pour les utilisateurs sur les ordinateurs joints à un domaine qui sont connectés toohello réseau d’entreprise. Avec l’authentification unique, les utilisateurs activés suffit tooenter un nom d’utilisateur toosecurely accéder aux ressources de le cloud. 

## <a name="pass-through-authentication"></a>Authentification directe
[L’authentification directe Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) fournit une solution de validation du mot de passe simple pour les services Azure AD à l’aide de votre répertoire Active Directory local. Si les stratégies de sécurité et de conformité pour votre organisation n’autorisent pas l’envoi des mots de passe utilisateurs, même dans un format haché, et vous devez uniquement toosupport bureau SSO pour les appareils joints à un domaine, il est recommandé que vous évaluez à l’aide de l’authentification directe. Authentification directe ne nécessite pas de n’importe quel déploiement Bonjour réseau de périmètre, ce qui simplifie l’infrastructure de déploiement hello lors de la comparaison avec les services AD FS. Lorsque les utilisateurs se connectent à l’aide d’Azure AD, cette méthode d’authentification valide les mots de passe utilisateurs directement à partir d’Active Directory local.

![Authentification directe](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Avec l’authentification directe, il est inutile d’une infrastructure réseau complexe, et vous n’avez pas besoin des mots de passe local toostore dans le cloud de hello. Combiné avec l’authentification unique, l’authentification directe fournit une expérience entièrement intégrée pour se connecter à tooAzure AD ou d’autres services de cloud.

L’authentification directe peut être configurée par le biais d’Azure AD Connect. Elle utilise un agent local simple qui écoute les requêtes de validation du mot de passe. agent de Hello peut être facilement déployé toomultiple machines tooprovide haute disponibilité et l’équilibrage de charge. Étant donné que toutes les communications sortantes ne sont, il n’est pas obligatoire pour hello connecteur toobe est installé dans un réseau de périmètre. configuration requise des ordinateurs serveur Hello pour le connecteur de hello est les suivantes :

- Windows Server 2012 R2 ou version ultérieure
- Joint le domaine tooa de forêt hello par le biais duquel les utilisateurs sont validés.

> [!NOTE]
> L’authentification directe Azure AD est généralement en aperçu et est prise en charge par les clients basés sur le navigateur Web et les clients Office qui prennent en charge l’authentification moderne. Pour les clients qui ne sont pas pris en charge, tels que les anciens clients Office et Exchange ActiveSync (y compris les clients de messagerie native sur les appareils mobiles), il est recommandé toouse hello authentification moderne équivalente. L’authentification moderne permet l’authentification directe mais permet également d’accès conditionnel toobe de stratégies appliquée, telles que l’authentification multifacteur. 

Authentification directe n'est pas actuellement pris en charge à l’aide d’appareils Windows 10 joints tooAzure AD. Toutefois, vous pouvez utiliser la synchronisation du hachage de mot de passe en tant qu’un toosupport de secours automatique Windows 10 et les clients hérités hello mentionné précédemment. Version préliminaire hello, la synchronisation du hachage de mot de passe est activée par défaut lors de l’authentification directe est sélectionnée comme hello-option de connexion dans Azure AD Connect.


## <a name="federated-identity-ad-fs"></a>Identité fédérée (AD FS)
Pour obtenir un meilleur contrôle sur le mode d’accès des utilisateurs à Office 365 et autres services cloud, vous pouvez configurer la synchronisation de répertoires avec authentification unique (SSO) à l’aide de [Active Directory Federation Services (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). Fédération de connexions de vos utilisateurs avec AD FS délégués authentification tooan serveur local qui valide les informations d’identification de l’utilisateur. Dans ce modèle, informations d’identification de Active Directory local ne sont jamais passées tooAzure AD.

![Identité fédérée](./media/choose-hybrid-identity-solution/federated-identity.png)

Également appelée fédération des identités, cette méthode garantit que toutes les authentifications utilisateur sont contrôlé sur site et permet aux administrateurs tooimplement plus rigoureux niveaux de contrôle d’accès. Fédération des identités avec AD FS est l’option de hello plus compliqué et nécessite le déploiement de serveurs supplémentaires dans votre environnement local. Fédération d’identité valide également prise en charge de tooproviding 24 x 7 de votre infrastructure Active Directory et AD FS. Ce niveau élevé de prise en charge est nécessaire, car si l’accès à Internet de votre local, contrôleur de domaine ou serveurs AD FS ne sont pas disponibles, les utilisateurs ne peuvent pas se connecter toocloud services.

> [!TIP]
> Si vous décidez toouse fédération avec Active Directory Federation Services (ADFS), vous pouvez éventuellement définir la synchronisation de mot de passe de sauvegarde en cas d’échec de votre infrastructure AD FS.


## <a name="common-scenarios-and-recommendations"></a>Scénarios et recommandations courants
Voici certains identité hybride commune et scénarios de gestion de l’accès avec les recommandations en tant qu’option d’identité hybride toowhich (ou options) peuvent être appropriées pour chacun.

|J’ai besoin de :|PWS et SSO<sup>1</sup>| PTA et SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Synchroniser le nouvel utilisateur, contact et les comptes de groupe créés automatiquement dans mon cloud toohello de Active Directory local.|![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png) |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Configurer mon client pour des scénarios hybrides Office 365|![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png) |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Activer mon toosign utilisateurs dans et accéder aux services de cloud à l’aide de leur mot de passe local|![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png) |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Implémenter l’authentification unique à l’aide des informations d’identification d’entreprise|![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png) |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Assurez-vous qu'aucun hachages de mot de passe ne sont stockées dans le cloud de hello| |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Activer des solutions d’authentification multifacteur locales| | |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Prendre en charge l’authentification par carte à puce pour mes utilisateurs<sup>4</sup>| | |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|
|Afficher les notifications d’expiration de mot de passe dans hello portail Office et sur le bureau de hello Windows 10| | |![Recommandé](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Synchronisation du mot de passe avec l’authentification unique. 

> <sup>2</sup> Authentification directe et authentification unique. 

> <sup>3</sup> Authentification unique fédérée avec AD FS.

> <sup>4</sup> AD FS peut être intégré à votre tooallow PKI d’entreprise connectez-vous à l’aide de certificats. Ces certificats peuvent être des certificats logiciels déployés via des canaux d’approvisionnement approuvés tels que les certificats de gestion des périphériques mobiles (GPM), d’objet de stratégie de groupe (GPO), de carte à puce (y compris les cartes PIV/CAC) ou Hello for Business (approbation de certificat). Pour plus d’informations sur la prise en charge de l’authentification par carte à puce, consultez [ce  blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Étapes suivantes
[En apprendre davantage dans un environnement de preuve de concept Azure](https://aka.ms/aad-poc)

[Installer Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

[Surveiller la synchronisation des identités hybrides](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

