---
title: "Azure AD Connect : Authentification unique transparente - Démarrage rapide | Microsoft Docs"
description: "Cet article décrit comment tooget démarrer avec Azure Active Directory transparente l’authentification unique."
services: active-directory
keywords: "Qu’est-ce qu’Azure AD Connect, Installation d’Active Directory, Composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Authentification unique transparente Azure Active Directory - Démarrage rapide

## <a name="how-toodeploy-seamless-sso"></a>Comment toodeploy l’authentification unique transparente

Azure Active Directory transparente Single Sign-On (Azure AD transparente l’authentification unique) connecte automatiquement les utilisateurs lorsqu’ils sont sur leur réseau d’entreprise connecté tooyour de postes de travail. Il fournit à vos utilisateurs un accès facile tooyour les applications cloud sans avoir besoin de tous les composants de site supplémentaires.

>[!IMPORTANT]
>fonctionnalité d’authentification unique transparente Hello est actuellement en version préliminaire.

toodeploy l’authentification unique transparente, vous devez toofollow comme suit :

## <a name="step-1-check-prerequisites"></a>Étape 1 : Vérifier les prérequis

Vérifiez que hello suivant les conditions préalables sont réunies :

1. Configurez votre serveur Azure AD Connect : si vous utilisez l’[authentification directe](active-directory-aadconnect-pass-through-authentication.md) comme méthode de connexion, aucune action supplémentaire n’est nécessaire. Si vous utilisez la [synchronisation de hachage de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) comme méthode de connexion, et s’il existe un pare-feu entre Azure AD Connect et Azure AD, vérifiez les points suivants :
- Vous utilisez la version 1.1.484.0 ou une version ultérieure d’Azure AD Connect.
- Azure AD Connect peut communiquer avec les URL `*.msappproxy.net` et sur le port 443. Cette condition préalable est applicable uniquement lorsque vous activez la fonctionnalité de hello, pas pour les connexions utilisateur réelle.
- Azure AD Connect peut rendre toohello de connexions IP directe [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653). Là encore, cette condition préalable est applicable uniquement lorsque vous activez la fonctionnalité de hello.
2. Vous avez besoin des informations d’identification d’administrateur de domaine pour chaque forêt Active Directory que vous synchronisez tooAzure AD (à l’aide d’Azure AD Connect) et pour les utilisateurs dont vous souhaitez tooenable l’authentification unique transparente.

## <a name="step-2-enable-hello-feature"></a>Étape 2 : Activer la fonctionnalité de hello

L’authentification unique transparente peut être activée à l’aide d’[Azure AD Connect](active-directory-aadconnect.md).

Si vous effectuez une nouvelle installation d’Azure AD Connect, choisissez hello [chemin d’installation personnalisé](active-directory-aadconnect-get-started-custom.md). Dans la page « Connexion d’utilisateur » hello, activez l’option de « Activer l’authentification unique » de hello.

![Azure AD Connect - Connexion utilisateur](./media/active-directory-aadconnect-sso/sso8.png)

Si vous disposez déjà d’une installation Azure AD Connect, choisissez Modifier la connexion utilisateur et cliquez sur Suivant. Vérifiez ensuite l’option « Activer l’authentification unique » de hello.

![Azure AD Connect - Modifier la connexion utilisateur](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Poursuivez avec l’Assistant de hello jusqu'à ce que vous obtenez toohello « Activer l’authentification unique » page. Fournir des informations d’identification d’administrateur de domaine pour chaque forêt Active Directory que vous synchronisez tooAzure AD (à l’aide d’Azure AD Connect) et pour les utilisateurs dont vous souhaitez tooenable l’authentification unique transparente. 

Après l’achèvement de l’Assistant de hello, l’authentification unique transparente est activé sur votre client.

>[!NOTE]
> informations d’identification d’administrateur de domaine de Hello ne sont pas stockées dans Azure AD Connect ou dans Azure AD, mais sont uniquement utilisés tooenable hello.

Suivez ces tooverify d’instructions que vous avez activé l’authentification unique transparente correctement :

1. Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec informations d’identification d’administrateur Global de hello pour votre client.
2. Sélectionnez **Azure Active Directory** de navigation de gauche hello.
3. Sélectionnez ensuite **Azure AD Connect**.
4. Vérifiez que hello **transparente Single Sign-On** fonctionnalité affiche sous la forme **activé**.

![Portail Azure - panneau Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Étape 3 : Déployer la fonctionnalité de hello

tooroll les utilisateurs de tooyour fonctionnalité hello, vous devez les paramètres de la zone Intranet des toousers du Azure AD URL (https://autologon.microsoftazuread-sso.com https://aadg.windows.net.nsatc.net) de deux tooadd via la stratégie de groupe dans Active Directory.

>[!NOTE]
> Hello suivant les instructions ne fonctionnent que pour Internet Explorer et Google Chrome sur Windows (si elle porte le même jeu d’URL du site de confiance dans Internet Explorer). Lire la section suivante de hello pour tooset instructions Mozilla Firefox et Google Chrome sur Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Pourquoi devez-vous les paramètres de la zone Intranet toomodify utilisateurs ?

Par défaut, les navigateur hello calcule automatiquement la zone de droite hello (Internet ou Intranet) à partir d’une URL. Par exemple, http://contoso/ est mappé toohello zone Intranet tandis que http://intranet.contoso.com/ est mappé toohello ernet (car hello URL contient un point). Point de terminaison cloud Kerberos pour les tickets tooa - comme hello deux Azure AD URL - ne pas envoyer de navigateurs, sauf si son URL est ajouté explicitement la zone Intranet du navigateur toohello.

### <a name="detailed-steps"></a>Procédure détaillée

1. Ouvrez l’outil de gestion de stratégie de groupe hello.
2. Modifier hello stratégie de groupe qui est appliqué toosome ou tous vos utilisateurs. Dans cet exemple, nous utilisons hello **stratégie de domaine par défaut**.
3. Accédez trop**Page Panel\Security de contrôle utilisateur Configuration ordinateur\Modèles d’administration\Composants Windows\Internet Explorer\Panneau** et sélectionnez **tooZone liste d’attribution de Site**.
![Authentification unique](./media/active-directory-aadconnect-sso/sso6.png)  
4. Activer la stratégie hello, puis entrez hello suivant de valeurs (Azure AD URL où les tickets Kerberos sont transférés) et données (*1* indique la zone Intranet) dans la boîte de dialogue hello.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Si vous voulez toodisallow que certains utilisateurs d’utiliser l’authentification unique transparente - par exemple, si ces utilisateurs se connectent sur les bornes partagées - définir hello précédant les valeurs trop*4*. Cette action ajoute hello Azure AD URL toohello Zone sensibles et Échec de l’authentification unique transparente tout temps hello.

5. Cliquez sur **OK**, puis de nouveau sur **OK**.

![Authentification unique](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Considérations sur le navigateur

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox ne procède pas automatiquement à l’authentification Kerberos. Chaque utilisateur a toomanually ajouter des paramètres de Firefox hello Azure AD URL tootheir à l’aide de hello comme suit :
1. Exécutez Firefox et entrez `about:config` dans la barre d’adresses hello. Ignorez les notifications que vous voyez.
2. Recherchez hello **network.negotiate-auth.trusted-URI** préférence. Cette préférence répertorie les sites de confiance de Firefox pour l’authentification Kerberos.
3. Cliquez avec le bouton droit et sélectionnez Modifier.
4. Entrez « https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net » dans le champ de hello.
5. Cliquez sur « OK » et rouvrez le navigateur de hello.

#### <a name="safari-on-mac-os"></a>Safari sur Mac OS

Vérifiez que cet ordinateur hello en cours d’exécution du système d’exploitation Mac est tooAD jointe. Consultez les instructions sur la façon de toodo qui [ici](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome sur Mac

Pour Google Chrome sur Mac OS et d’autres plateformes non-Windows, consultez trop[cet article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) pour plus d’informations sur la façon dont toowhitelist hello URL Azure AD pour l’authentification intégrée.

À l’aide de la stratégie de groupe Active Directory tiers tooroll extensions hello Azure AD URL tooFirefox et Google Chrome sur les utilisateurs Mac est en dehors de la portée de cet article.

#### <a name="known-limitations"></a>Limites connues

L’authentification unique transparente ne fonctionne pas en mode de navigation privée sur Firefox et Edge. Il ne fonctionne pas sur Internet Explorer si le navigateur de hello s’exécute en mode de Protection d’améliorée.

>[!IMPORTANT]
>Nous avons récemment restaurée prise en charge de bord tooinvestigate problèmes signalés par le client.

## <a name="step-4-test-hello-feature"></a>Étape 4 : Tester la fonctionnalité de hello

fonctionnalité de hello tootest pour un utilisateur spécifique, assurez-vous que _tous les_ hello conditions suivantes est réunies :
  - utilisateur de Hello se connecte sur un appareil d’entreprise.
  - Appareil de Hello a été domaine d’Active Directory (AD) tooyour jointes précédemment.
  - Appareil de Hello possède un contrôleur de domaine (DC), soit sur le réseau hello câblés ou sans fil d’entreprise via une connexion d’accès à distance, notamment les connexions VPN de tooyour connexion directe.
  - Vous avez [transférée de la fonctionnalité de hello](##step-3-roll-out-the-feature) utilisateur toothis à l’aide de la stratégie de groupe.

scénario de hello tootest où les utilisateur hello entre uniquement les nom d’utilisateur hello, mais pas un mot de passe hello :
- Connectez-vous à *https://myapps.microsoft.com/* dans une nouvelle session de navigation privée.

scénario de hello tootest où hello utilisateur ne dispose pas tooenter hello nom d’utilisateur ou hello un mot de passe : 
- Connectez-vous à *https://myapps.microsoft.com/contoso.onmicrosoft.com* dans une nouvelle session de navigation privée. Remplacez « *contoso* » par le nom de votre locataire.
- Ou connectez-vous à *https://myapps.microsoft.com/contoso.com* dans une nouvelle session de navigation privée. Remplacez « *contoso.com* » par un domaine vérifié (pas un domaine fédéré) dans votre locataire.

## <a name="step-5-roll-over-keys"></a>Étape 5 : substituer les clés

À l’étape 2, Azure AD Connect crée des comptes d’ordinateurs (représentant Azure AD) dans toutes les forêts hello AD sur lequel vous avez activé l’authentification unique transparente. Obtenez plus de détails [ici](active-directory-aadconnect-sso-how-it-works.md). Pour améliorer la sécurité, il est recommandé de substituer fréquemment clés de déchiffrement hello Kerberos de ces comptes d’ordinateur.

>[!IMPORTANT]
>Vous n’avez pas besoin toodo cette étape _immédiatement_ après avoir activé la fonctionnalité de hello. Substituer les clés de déchiffrement hello Kerberos au moins tous les 30 jours.

## <a name="next-steps"></a>Étapes suivantes

- [**Immersion technique**](active-directory-aadconnect-sso-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Forum aux Questions** ](active-directory-aadconnect-sso-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-sso.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour le dépôt de nouvelles demandes de fonctionnalités.
