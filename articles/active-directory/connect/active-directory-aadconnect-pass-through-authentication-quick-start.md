---
title: "Authentification directe Azure AD : Démarrage rapide | Microsoft Docs"
description: "Cet article décrit comment tooget démarrer avec une authentification directe Azure Active Directory (Azure AD)."
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
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Authentification directe Azure Active Directory : Démarrage rapide

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Comment toodeploy authentification Azure AD directe

Azure Active Directory (Azure AD) pass-through Authentication permet à votre toosign utilisateurs tooboth locaux et les applications cloud à l’aide de hello mêmes mots de passe. Elle connecte les utilisateurs en validant leurs mots de passe directement par rapport à votre annuaire Active Directory local.

>[!IMPORTANT]
>L’authentification directe Azure AD est actuellement en préversion. Si vous utilisez cette fonctionnalité via l’aperçu, vous devez vous assurer que vous mettez à niveau les versions préliminaires de hello authentification Agents à l’aide d’instructions hello fournies [ici](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

Vous devez toofollow ces toodeploy instructions authentification directe :

## <a name="step-1-check-prerequisites"></a>Étape 1 : Vérifier les prérequis

Vérifiez que hello suivant les conditions préalables sont réunies :

### <a name="on-hello-azure-active-directory-admin-center"></a>Sur le centre d’administration Active Directory de Azure hello

1. Créez un compte d’administrateur général « cloud uniquement » dans votre locataire Azure AD. De cette manière, vous pouvez gérer configuration hello de votre client doivent vos services locaux échouent ou ne sont plus disponibles. Découvrez comment [ajouter un compte d’administrateur général de type cloud uniquement](../active-directory-users-create-azure-portal.md). Cette étape est tooensure critiques que vous ne soit verrouillé de votre client.
2. Ajouter un ou plusieurs [ou les noms de domaine personnalisé](../active-directory-add-domain.md) tooyour Azure AD client. Vos utilisateurs se connectent à l’aide de l’un de ces noms de domaine.

### <a name="in-your-on-premises-environment"></a>Dans votre environnement local

1. Identifier un serveur exécutant Windows Server 2012 R2 ou version ultérieure sur le toorun Azure AD Connect. Ajouter la forêt toohello même AD du serveur hello en tant qu’utilisateurs hello dont les mots de passe doivent toobe validé.
2. Installer hello [version la plus récente d’Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) sur serveur hello identifié à l’étape précédente. Si vous avez déjà en cours d’exécution Azure AD Connect, assurez-vous que la version hello est 1.1.557.0 ou version ultérieure.
3. Identifier un serveur supplémentaire exécutant Windows Server 2012 R2 ou version ultérieure sur le toorun un autonome Agent d’authentification. version d’Agent d’authentification Hello doit toobe 1.5.193.0 ou version ultérieure. Ce serveur est nécessaire tooensure haute disponibilité des demandes de connexion. Ajouter la forêt toohello même AD du serveur hello en tant qu’utilisateurs hello dont les mots de passe doivent toobe validé.
4. S’il existe un pare-feu entre les serveurs et Azure AD, vous devez hello tooconfigure éléments suivants :
   - Assurez-vous que les Agents de l’authentification peut effectuer **sortant** demande tooAzure AD sur hello suivant des ports :
   
   | Numéro de port | Utilisation |
   | --- | --- |
   | **80** | Téléchargement de la révocation de certificats de listes (CRL) lors de la validation du certificat SSL de hello |
   | **443** | Toutes les communications sortantes avec notre service |
   
   Si votre pare-feu applique les règles selon les utilisateurs toooriginating, ouvrir ces ports pour le trafic à partir des services Windows qui s’exécutent en tant que Service réseau.
   - Si votre pare-feu ou un proxy autorise liste approuvées DNS, les connexions de la liste blanche d’adresses trop**\*. msappproxy.net** et  **\*. servicebus.windows.net**. Dans le cas contraire, autoriser l’accès trop[plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653), qui sont mis à jour chaque semaine.
   - Les Agents d’authentification doivent accéder trop**login.windows.net** et **login.microsoftonline.com** pour l’inscription initiale, ouvrez votre pare-feu pour ces URL ainsi.
   - Validation du certificat, débloquer hello URL suivantes : **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** et  **www.Microsoft.com:80**. Ces URL sont utilisées pour la validation de certificat avec d’autres produits Microsoft : elles seront peut-être déjà débloquées.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Étape 2 : Activer la prise en charge d’Exchange ActiveSync (facultatif)

Suivez ces instructions de tooenable prise en charge Exchange ActiveSync :

1. Utilisez [PowerShell Exchange](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) hello toorun commande suivante :
```
Get-OrganizationConfig | fl per*
```

2. Vérifiez la valeur hello hello `PerTenantSwitchToESTSEnabled` paramètre. Si la valeur hello est **true**, votre client est correctement configuré ; c’est généralement hello cas pour la plupart des clients. Si la valeur hello est **false**, exécutez hello commande suivante :
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Vérifiez que la valeur hello Hello `PerTenantSwitchToESTSEnabled` est maintenant défini trop**true**. Attendre une heure avant mobile toohello prochaine étape.

Si vous rencontrez des problèmes au cours de cette étape, consultez notre [guide de résolution des problèmes](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) pour plus d’informations.

## <a name="step-3-enable-hello-feature"></a>Étape 3 : Activer la fonctionnalité de hello

Vous pouvez activer l’authentification directe par l’intermédiaire d’[Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Authentification directe peut être activée sur les serveur hello Azure AD Connect principal ou intermédiaire. Il est vivement recommandé de l’activer à partir du serveur principal de hello.

Si vous installez Azure AD Connect pour hello première fois, choisissez hello [chemin d’installation personnalisé](active-directory-aadconnect-get-started-custom.md). À hello **connexion d’utilisateur** choisissez **authentification directe** comme hello signe sur la méthode. Opération réussie, un agent de l’authentification directe est installé sur hello même serveur que Azure AD Connect. En outre, la fonctionnalité d’authentification directe hello est activée sur votre client.

![Azure AD Connect - Connexion de l’utilisateur](./media/active-directory-aadconnect-sso/sso3.png)

Si vous avez déjà installé Azure AD Connect (à l’aide de hello [installation express](active-directory-aadconnect-get-started-express.md) ou hello [installation personnalisée](active-directory-aadconnect-get-started-custom.md) chemin d’accès), sélectionnez **modification utilisateur-page de connexion** sur Azure AD Se connecter, puis cliquez sur **suivant**. Puis sélectionnez **authentification directe** comme hello signe sur la méthode. Opération réussie, un agent de l’authentification directe est installé sur hello même serveur que la fonctionnalité de Azure AD Connect et hello est activé sur votre client.

![Azure AD Connect - Modifier la connexion utilisateur](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>L’authentification directe est une fonctionnalité au niveau du locataire. Mise sous tension qu’il a un impact sur Connectez-vous pour les utilisateurs au sein de _tous les_ hello gérés des domaines dans votre client. Si vous passez de tooPass via l’authentification AD FS, nous vous recommandons que vous attendez au moins 12 heures avant l’arrêt de votre infrastructure AD FS, ce délai d’attente est tooensure que les utilisateurs peuvent conserver la connexion tooExchange ActiveSync au cours de transition.

## <a name="step-4-test-hello-feature"></a>Étape 4 : Tester la fonctionnalité de hello

Suivez ces tooverify d’instructions que vous avez activé l’authentification directe correctement :

1. Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec informations d’identification d’administrateur Global de hello pour votre client.
2. Sélectionnez **Azure Active Directory** de navigation de gauche hello.
3. Sélectionnez ensuite **Azure AD Connect**.
4. Vérifiez que hello **authentification directe** fonctionnalité affiche sous la forme **activé**.
5. Sélectionnez **Authentification directe**. Ce panneau répertorie les serveurs de hello où sont installées vos Agents de l’authentification.

![Centre d’administration Azure Active Directory - panneau Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centre d’administration Azure Active Directory - panneau Authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

À ce stade, les utilisateurs de tous les domaines gérés de votre locataire peuvent se connecter à l’aide de l’authentification directe. Toutefois, les utilisateurs de domaines fédérés continuent toosign à l’aide des Services de fédération Active Directory (AD FS) ou un autre fournisseur de fédération que vous avez configuré précédemment. Si vous convertissez un domaine fédéré toomanaged, tous les utilisateurs de ce domaine démarre automatiquement la connexion à l’aide de l’authentification directe. Les utilisateurs de cloud uniquement ne sont pas affectées par la fonctionnalité d’authentification directe hello.

## <a name="step-5-ensure-high-availability"></a>Étape 5 : Garantir une haute disponibilité

Si vous envisagez toodeploy authentification directe dans un environnement de production, vous devez installer un Agent d’authentification autonome. Installez ce deuxième Agent d’authentification sur un serveur _autres_ que hello un en cours d’exécution Azure AD Connect et hello premier Agent d’authentification. Cette installation procure une haute disponibilité des demandes de connexion. Suivez ces instructions de toodeploy un Agent d’authentification autonome :

1. **Télécharger hello dernière version de l’Agent d’authentification de hello (versions 1.5.193.0 ou version ultérieure)**: connectez-vous toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec des droits d’administrateur Global de votre locataire.
2. Sélectionnez **Azure Active Directory** de navigation de gauche hello.
3. Sélectionnez **Azure AD Connect**, puis **Authentification directe**. Sélectionnez **Télécharger l’agent**.
4. Cliquez sur hello **accepter les termes du contrat de & Télécharger** bouton.
5. **Installer version la plus récente de l’Agent d’authentification de hello hello**: hello exécuter exécutable téléchargé Bonjour précédant l’étape. Fournissez les informations d’identification de l’administrateur général de votre locataire lorsque vous y êtes invité.

![Centre d’administration Azure Active Directory - Bouton Télécharger Agent d’authentification](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Centre d’administration Azure Active Directory - Panneau Télécharger l’agent](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>Vous pouvez également télécharger hello Agent d’authentification à partir de [ici](https://aka.ms/getauthagent). Vérifiez que vous passez en revue et acceptez l’Agent d’authentification hello [termes du contrat de Service](https://aka.ms/authagenteula) _avant_ l’installer.

## <a name="next-steps"></a>Étapes suivantes
- [**Limitations actuelles**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) : cette fonctionnalité est actuellement en préversion. Découvrez les scénarios pris en charge et ceux qui ne le sont pas.
- [**Immersion technique**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Forum aux Questions** ](active-directory-aadconnect-pass-through-authentication-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.
