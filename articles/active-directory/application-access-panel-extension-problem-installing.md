---
title: "aaaProblem installer l’extension volet navigateur d’accès application hello | Documents Microsoft"
description: "Comment les erreurs courantes toofix rencontré lors de l’installation d’extension du navigateur hello accès Panneau de configuration"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Problème d’installation de l’extension de navigateur hello application accès Panneau de configuration

Hello volet d’accès est un portail web qui permet à un utilisateur qui dispose d’une entreprise ou école administrateur de compte dans Azure Active Directory (Azure AD) tooview et lancer les applications cloud qui hello Azure AD lui a accordé l’accès à. Un utilisateur disposant des éditions d’Azure AD permet également de groupes en libre-service et les fonctionnalités de gestion d’application via hello panneau d’accès. Hello volet d’accès est séparé hello portail Azure et ne requiert pas d’utilisateurs toohave un abonnement Azure.

toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello. Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Configuration requise du navigateur de réunion hello panneau d’accès

Hello volet d’accès nécessite un navigateur qui prend en charge JavaScript et a activé les CSS. toouse mot de passe-session unique (SSO) Bonjour hello extension du volet d’accès, volet d’accès doit être installé dans le navigateur de l’utilisateur hello. Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.

Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :

-   Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure

-   Edge sur Windows 10 Édition anniversaire ou version ultérieure 

-   Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou ultérieur

-   Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou ultérieur, et sur Mac OS X 10.6 ou ultérieur

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Comment tooinstall hello extension du navigateur de panneau d’accès

tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.

2.  Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.

3.  Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.

4.  En fonction de votre navigateur vous être lien de téléchargement toohello dirigée. **Ajouter** navigateur de tooyour extension hello.

5.  Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.

6.  Une fois l’extension installée, **redémarrez** votre session de navigateur.

7.  Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe

Vous pouvez également télécharger l’extension de hello pour Chrome et le bord à partir de liens directs de hello ci-dessous :

-   [Extension du volet d’accès pour Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extension du volet d’accès pour Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configuration d’une stratégie de groupe pour Internet Explorer

Vous pouvez configurer une stratégie de groupe qui vous tooremotely installer une extension volet d’accès hello pour Internet Explorer sur les ordinateurs de vos utilisateurs.

conditions préalables de Hello sont les suivantes :

-   Vous avez configuré [les Services de domaine Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), et vous avez joint le domaine de tooyour ordinateurs de vos utilisateurs.

-   Vous devez avoir hello hello « Modifier les paramètres » autorisation tooedit objet de stratégie de groupe (GPO). Par défaut, les membres de hello les groupes de sécurité suivants ont cette autorisation : les administrateurs de domaine, les administrateurs d’entreprise et les propriétaires créateurs de la stratégie de groupe. [En savoir plus](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Suivez le didacticiel de hello [comment tooDeploy hello Extension volet d’accès pour Internet Explorer à l’aide de la stratégie de groupe](active-directory-saas-ie-group-policy.md) pour obtenir des instructions étape par étape comment tooconfigure hello de stratégie de groupe et déployez-le toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Résoudre les problèmes de hello volet d’accès dans Internet Explorer

Suivez hello [dépannage hello Extension volet d’accès pour Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide pour l’accès d’un outil de diagnostic et des instructions étape par étape sur la configuration de l’extension de hello pour Internet Explorer.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Si ces étapes de dépannage ne résolvent pas le problème de hello

Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :

-   ID d’erreur de corrélation

-   UPN (adresse e-mail de l’utilisateur)

-   ID de locataire

-   Type de navigateur

-   Fuseau horaire et heure/période à laquelle l’erreur se produit

-   Traces Fiddler

## <a name="next-steps"></a>Étapes suivantes
[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
