---
title: "vérification de l’étape d’aaaTwo et AD FS - l’authentification Multifacteur Azure | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget main d’Azure MFA et AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Prise en main d’Azure Multi-Factor Authentication et des services de fédération Active Directory (AD FS)
<center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Si votre organisation a fédéré votre Active Directory local avec Azure Active Directory à l’aide d’AD FS, vous disposez de deux options pour l’utilisation d’Azure Multi-Factor Authentication.

* Sécuriser les ressources de cloud à l’aide de l’authentification multifacteur Azure ou des services de fédération Active Directory (AD FS)
* Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication

Hello tableau suivant résume l’expérience de vérification hello entre la sécurisation des ressources avec Azure multi-Factor Authentication et AD FS

| Processus de vérification : applications basées sur le navigateur | Processus de vérification : applications hors navigateur |
|:--- |:--- |:--- |
| Sécurisation des ressources Azure AD à l'aide d’Azure Multi-Factor Authentication |<li>première étape de vérification Hello est effectuée en local avec AD FS.</li> <li>deuxième étape de Hello est une méthode par téléphone effectuée à l’aide de l’authentification cloud.</li> |
| Sécurisation des ressources Azure AD à l'aide des services ADFS |<li>première étape de vérification Hello est effectuée en local avec AD FS.</li><li>Hello deuxième étape est effectué localement en répondant à hello revendication.</li> |

Mises en garde relatives aux mots de passe d'application pour les utilisateurs fédérés :

* Les mots de passe d’applications sont vérifiés à l’aide de l’authentification cloud et contournent donc la fédération. La fédération n’est utilisée activement que lorsque vous configurez un mot de passe d’application.
* Les paramètres de contrôle d’accès client locaux ne sont pas honorés par les mots de passe d’application.
* Vous perdez la fonctionnalité de journalisation-authentification locale pour les mots de passe d’application.
* La désactivation/suppression de compte peut prendre des heures de toothree pour la synchronisation d’annuaire, retardant la désactivation/suppression de mots de passe d’application dans l’identité de cloud hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la configuration de l’authentification multifacteur Azure ou de hello serveur Azure multi-Factor Authentication avec AD FS, consultez hello suivant des articles :

* [Sécuriser les ressources cloud à l’aide d’Azure Multi-Factor Authentication et AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec Windows Server 2012 R2 AD FS](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
