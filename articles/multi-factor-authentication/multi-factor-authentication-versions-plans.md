---
title: "versions de l’authentification Multifacteur aaaAzure et la consommation des plans | Documents Microsoft"
description: "Informations sur le client de l’authentification multifacteur hello et les différentes méthodes de hello et les versions disponibles. Détails sur chaque plan de consommation"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Comment tooget Azure multi-Factor Authentication

Lorsqu’il s’agit tooprotecting vos comptes, vérification en deux étapes doit être standard dans votre organisation. Cette fonctionnalité est particulièrement importante pour les comptes administratifs qui ont des privilèges élevés tooresources d’accès. Pour cette raison, Microsoft propose tooOffice de fonctionnalités de vérification en deux étapes de base 365 et les administrateurs Azure. Si vous souhaitez que les fonctionnalités de hello tooupgrade pour vos administrateurs, ou étendez le reste de toohello vérification en deux étapes de vos utilisateurs, vous pouvez acheter Azure multi-Factor Authentication. 

Cet article traite des explique la différence hello entre les versions hello proposé tooadministrators et hello version Azure MFA complète et spécifie quelles fonctionnalités sont disponibles dans chaque. Si vous êtes prêt toodeploy hello Azure MFA offre complète, hello des options de mise en œuvre ultérieure sections couvre et comment Microsoft calcule la consommation.

>[!IMPORTANT]
>Cet article est destiné à toobe un toohelp guide que vous comprenez hello toobuy de différentes façons Azure multi-Factor Authentication. Pour plus d’informations sur la tarification et facturation spécifiques, vous devez font toujours référence toohello [multi-Factor Authentication, page de tarification](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Versions disponibles d’Azure Multi-Factor Authentication

Hello tableau suivant décrit les différences de hello entre trois versions de l’authentification multifacteur :

| Version | Description |
| --- | --- |
| Authentification multifacteur pour Office 365 |Cette version fonctionne exclusivement avec les applications Office 365 et est gérée à partir du portail de hello Office 365. Les administrateurs peuvent [sécuriser les ressources Office 365 avec la vérification en deux étapes](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Cette version est fournie dans le cadre d’un abonnement à Office 365. |
| Authentification multifacteur pour administrateurs Azure | Les administrateurs généraux des locataires Azure peuvent activer la vérification en deux étapes pour leurs comptes d’administrateurs généraux sans coût supplémentaire.|
| Azure Multi-Factor Authentication | Version liée à un « complet » hello tooas souvent désignée, Azure multi-Factor Authentication qui offre ensemble plus riche de hello de fonctionnalités. Il fournit des options de configuration supplémentaires via hello [portail Azure classic](https://manage.windowsazure.com), des rapports avancés et prise en charge pour une plage de locaux et cloud des applications. L’authentification multifacteur Azure est incluse dans Azure Active Directory Premium (plans P1 et P2) et Enterprise Mobility + Security (plans E3 et E5) et peut être déployé soit [dans le cloud de hello ou sur site](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Comparaison des fonctionnalités suivant les versions
Hello tableau suivant fournit une liste des fonctionnalités hello qui sont disponibles dans hello différentes versions d’Azure multi-Factor Authentication.

> [!NOTE]
> Ce tableau de comparaison décrit les fonctionnalités de hello qui font partie de chaque version de l’authentification multifacteur. Si vous avez hello complète Azure multi-Factor Authentication service, certaines fonctionnalités ne soient pas disponibles selon que vous utilisez [l’authentification Multifacteur dans le cloud de hello ou l’authentification Multifacteur sur site](multi-factor-authentication-get-started.md).


| Fonctionnalité | Authentification multifacteur pour Office 365 | Authentification multifacteur pour administrateurs Azure | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| Protection des comptes Administrateur avec MFA |● |● (Comptes d’administrateurs généraux uniquement) |● |
| Application mobile comme second facteur |● |● |● |
| Appel téléphonique comme second facteur |● |● |● |
| SMS comme second facteur |● |● |● |
| Mots de passe d'application pour les clients qui ne prennent pas en charge MFA |● |● |● |
| Contrôle d’administration sur les méthodes de vérification |● |● |● |
| Mode du code PIN | | |● |
| Alerte de fraude | | |● |
| Rapports MFA | | |● |
| Contournement à usage unique | | |● |
| Messages de bienvenue personnalisés pour les appels téléphoniques | | |● |
| ID d’appelant personnalisé pour les appels téléphoniques | | |● |
| Adresses IP approuvées | | |● |
| Mémoriser MFA pour les appareils fiables |● |● |● |
| SDK MFA | | |● (Requiert un fournisseur Multi-Factor Auth et un abonnement Azure complet) |
| MFA pour les applications locales | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Comment tooget Azure multi-Factor Authentication
Si vous souhaitez que les fonctionnalités complètes de hello offertes par l’authentification multifacteur Azure, il existe plusieurs options :

### <a name="option-1---mfa-licenses"></a>Option 1 : licences MFA

Acheter des licences Azure multi-Factor Authentication et leur affecter des utilisateurs de tooyour dans Azure Active Directory. 

Si vous utilisez cette option, vous devez créer un fournisseur d’authentification multifacteur Azure seulement si vous devez également une vérification en deux étapes de tooprovide pour certains utilisateurs ne disposant pas de licences. Sinon, vous risquez d’être facturé à deux reprises.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Option 2 : licences regroupées qui incluent MFA

Acheter des licences qui incluent l’authentification multifacteur Azure, comme Azure Active Directory Premium (P1 ou P2) ou Enterprise Mobility + Security (E3 ou E5) et de leur affecter des utilisateurs de tooyour dans Azure Active Directory. 

Si vous utilisez cette option, vous devez créer un fournisseur d’authentification multifacteur Azure seulement si vous devez également une vérification en deux étapes de tooprovide pour certains utilisateurs ne disposant pas de licences. Sinon, vous risquez d’être facturé à deux reprises. 

### <a name="option-3---mfa-consumption-based-model"></a>Option 3 : modèle basé sur la consommation MFA

Créez un fournisseur Azure Multi-Factor Authentication dans un abonnement Azure. Les fournisseurs Azure MFA sont des ressources Azure qui sont facturées sur votre Accord Entreprise, votre engagement monétaire Azure ou votre carte de crédit comme toutes les autres ressources Azure. Ces fournisseurs ne peuvent être créés que dans les abonnements Azure complets, et non dans les abonnements Azure pour lesquels une limite de dépense de 0 $ est définie. Des abonnements limités sont créés lorsque vous activez des licences, comme dans les options 1 et 2. 

Quand vous utilisez un fournisseur Azure Multi-Factor Authentication, vous avez le choix entre deux modèles d’utilisation qui sont facturés dans le cadre de votre abonnement Azure :  

1. **Par utilisateur** - pour les entreprises qui le souhaitent vérification en deux étapes de tooenable pour un nombre fixe d’employés qui s’authentifient régulièrement. La facturation par utilisateur est basée sur le nombre de hello d’utilisateurs activés pour l’authentification Multifacteur dans votre locataire Azure AD et/ou de votre serveur Azure MFA. Si les utilisateurs sont activés pour l’authentification Multifacteur dans les deux Azure AD et le serveur Azure MFA et la synchronisation du domaine (Azure AD Connect) est activée, puis nous compter ensemble plus important de hello d’utilisateurs. Si la synchronisation du domaine n’est pas activée, puis nous compter somme hello de tous les utilisateurs activés pour l’authentification Multifacteur dans Azure AD et le serveur Azure MFA. La facturation est système de Commerce toohello au prorata et signalée quotidienne. 

  > [!NOTE]
  > Exemple de facturation 1 : 5 000 utilisateurs sont activés pour MFA à la date du jour. Hello système de l’authentification Multifacteur divise ce nombre par 31 et 161.29 utilisateurs de rapports pour ce jour. Demain vous activez 15 davantage d’utilisateurs, afin de 161.77 aux utilisateurs des rapports hello système de l’authentification Multifacteur pour ce jour. En fin de hello de hello cycle de facturation, hello nombre d’utilisateurs facturés sur votre abonnement Azure ajoute des tooaround 5 000. 
  >
  > Exemple de facturation 2 : vous disposez d’un mélange d’utilisateurs dont les licences et les utilisateurs sans afin que vous ayez un toomake de fournisseur d’authentification Multifacteur Azure par utilisateur différence de hello. Il existe 4 500 licences Enterprise Mobility + Security sur votre client, mais 5 000 utilisateurs sont activés pour MFA. Votre abonnement Azure est facturé pour 500 utilisateurs, calculé au prorata et indiqué quotidiennement sous la forme de 16,13 utilisateurs. 

2. **Par authentification** - pour les entreprises qui le souhaitent vérification en deux étapes de tooenable pour un grand groupe d’utilisateurs qui s’authentifient rarement. Facturation est basée sur le nombre de hello de demandes de vérification en deux étapes reçus par hello du service cloud Azure MFA, que ces vérifications réussissent ou sont refusées. Cette facturation apparaît dans votre instruction d’utilisation d’Azure dans les packs de 10 authentifications et est signalée toohello Commerce système quotidienne. 

  > [!NOTE]
  > Exemple de facturation 3 : aujourd'hui, hello du service Azure MFA a reçu des demandes de vérification 3,105 en deux étapes. Votre abonnement Azure est facturé pour 310,5 packs d’authentification. 

Il est important toonote peut avoir des licences Azure MFA, mais de toujours obtenir facturé pour la configuration basée sur la consommation. Si vous configurez un fournisseur Azure MFA par authentification, vous êtes facturé pour toutes les demandes de vérification en deux étapes, y compris pour celles qui ont été effectuées par les utilisateurs disposant de licences. Si vous configurez un fournisseur d’authentification Multifacteur Azure par utilisateur sur un domaine qui n’est pas lié tooyour locataire Azure AD, vous êtes facturé par utilisateur activé même si vos utilisateurs disposent de licences sur Azure AD. 

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur la tarification, consultez la [tarification d’Azure MFA](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Choisissez si toodeploy Azure MFA [dans hello ou local](multi-factor-authentication-get-started.md)
