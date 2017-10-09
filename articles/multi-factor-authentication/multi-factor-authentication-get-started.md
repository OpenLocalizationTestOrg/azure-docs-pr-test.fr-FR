---
title: "aaaChoose entre le serveur ou de cloud d’Azure MFA | Documents Microsoft"
description: "Choisissez la solution de sécurité de l’authentification multifacteur hello qui vous convient en demandant, quelles am I la tentative de toosecure et où sont mes utilisateurs situé.  Choisissez ensuite le cloud, le serveur MFA ou AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Choisissez la solution d’authentification multifacteur Azure hello pour vous
Comme il existe plusieurs versions d’Azure multi-Factor Authentication (MFA), nous devons répondre quelques questions toofigure votre version est toouse d’un bon hello.  Ces questions sont les suivantes :

* [Ce que je fais toosecure](#what-am-i-trying-to-secure)
* [Où sont situés les utilisateurs de hello](#where-are-the-users-located)
* [quelles sont les fonctionnalités nécessaires ?](#what-featured-do-i-need)

Hello sections suivantes fournissent des conseils sur la détermination de chacun de ces réponses.

## <a name="what-am-i-trying-toosecure"></a>Ce que je fais toosecure ?
solution de vérification en deux étapes correct toodetermine hello, tout d’abord, nous devons répondre permis de hello de ce que vous toosecure lors de la tentative avec une deuxième méthode d’authentification.  S’agit-il d’une application dans Azure ?  Ou d’un système d’accès à distance ?  En déterminant ce que nous essayons toosecure, nous pouvons répondre hello question où l’authentification multifacteur doit toobe activé.  

| Quelles sont les toosecure lors de la tentative de vous | Authentification Multifacteur dans le cloud de hello | Serveur MFA |
| --- |:---:|:---:|
| Applications Microsoft internes |● |● |
| Applications SaaS dans la galerie d’applications hello |● |  |
| Applications Web publiées via le proxy d’application Azure AD |● |  |
| Applications IIS non publiées via le proxy d'application Azure AD | |● |
| Accès à distance comme VPN, RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Où sont situés les utilisateurs de hello
Ensuite, examinant où se trouvent nos utilisateurs permet de toodetermine hello solution appropriée toouse, que ce soit dans le cloud de hello ou localement à l’aide de hello serveur MFA.

| Emplacement de l'utilisateur | Authentification Multifacteur dans le cloud de hello | Serveur MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD et AD local à l'aide de la fédération avec AD FS |● |● |
| Azure AD et AD local à l'aide de DirSync, Azure AD Sync, Azure Connect AD : aucune synchronisation de mot de passe |● |● |
| Azure AD et AD local à l'aide de DirSync, Azure AD Sync, Azure Connect AD : avec synchronisation de mot de passe |● | |
| Active Directory local | |● |

## <a name="what-features-do-i-need"></a>Quelles sont les fonctionnalités nécessaires ?
Hello tableau suivant compare les fonctionnalités de hello qui sont disponibles avec l’authentification multifacteur dans le cloud de hello et hello serveur multi-Factor Authentication.

| Fonctionnalité | Authentification Multifacteur dans le cloud de hello | Serveur MFA |
| --- |:---:|:---:|
| Notification d'application mobile comme second facteur | ● | ● |
| Code de vérification d'application mobile comme second facteur | ● | ● |
| Appel téléphonique comme second facteur | ● | ● |
| SMS unidirectionnel comme second facteur | ● | ● |
| SMS bidirectionnel comme second facteur | | ● |
| Jetons matériels comme second facteur | | ● |
| Mots de passe d’application pour les clients Office 365 qui ne prennent pas en charge MFA | ● | |
| Contrôle d'administration sur les méthodes d'authentification | ● | ● |
| Mode du code PIN | | ● |
| Alerte de fraude |● | ● |
| Rapports MFA |● | ● |
| Contournement à usage unique | | ● |
| Messages de bienvenue personnalisés pour les appels téléphoniques | ● | ● |
| ID d'appelant personnalisable pour les appels téléphoniques | ● | ● |
| Adresses IP approuvées | ● | ● |
| Mémoriser MFA pour les appareils fiables | ● | |
| Accès conditionnel | ● | ● |
| Cache |  | ● |

## <a name="next-steps"></a>Étapes suivantes

Maintenant que nous avons déterminé si toouse cloud l’authentification multifacteur ou hello serveur MFA localement, nous pouvons démarrer configuration et l’utilisation d’Azure multi-Factor Authentication. **Sélectionnez l’icône hello qui représente votre scénario**

<center>




[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Serveur](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</center>
