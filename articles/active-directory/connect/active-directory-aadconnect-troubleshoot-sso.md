---
title: "Azure AD Connect : Résoudre les problèmes d’authentification unique transparente | Microsoft Docs"
description: "Cette rubrique décrit comment tootroubleshoot Azure Active Directory transparente Single Sign-On (Azure AD transparente l’authentification unique)."
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Résoudre les problèmes d’authentification unique transparente Azure Active Directory

Cet article fournit des informations sur les problèmes courants liés à l’authentification unique transparente Azure AD.

## <a name="known-issues"></a>Problèmes connus

- Si vous synchronisez 30 forêts AD ou plus, vous ne pouvez pas activer l’authentification unique transparente à l’aide d’Azure AD Connect. Pour résoudre ce problème, vous pouvez [activer manuellement](#manual-reset-of-azure-ad-seamless-sso) fonctionnalité hello sur votre client.
- Ajout AD Azure service URL (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello « zone sites de confiance » au lieu de la zone de « intranet Local » hello **empêche les utilisateurs de l’ouverture de session**.
- L’authentification unique transparente ne fonctionne pas en mode Navigation privée sur Firefox et Edge. Il en va de même sur Internet Explorer lorsque le mode Protégé amélioré est activé.

>[!IMPORTANT]
>Nous avons récemment restaurée prise en charge de bord tooinvestigate problèmes signalés par le client.

## <a name="check-status-of-hello-feature"></a>Vérifiez l’état de la fonctionnalité de hello

Vérifiez que cette fonctionnalité de l’authentification unique transparente hello est toujours **activé** sur votre client. Vous pouvez vérifier l’état à passer de toohello **Azure AD Connect** panneau sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com/).

![Centre d’administration Azure Active Directory - panneau Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Raisons d’échec de connexion sur le centre d’administration Active Directory de Azure hello

Un toostart bon point de résolution des problèmes de connexion utilisateur avec l’authentification unique transparente est toolook à hello [rapport d’activité de connexion](../active-directory-reporting-activity-sign-ins.md) sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com/).

![Centre d’administration Azure Active Directory - rapport de connexions](./media/active-directory-aadconnect-sso/sso9.png)

Accédez trop**Azure Active Directory** -> **connexions** sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com/) sur l’activité de connexion d’un utilisateur spécifique. Recherchez hello **CODE d’erreur de connexion** champ. Mapper la valeur hello de cette raison de l’échec tooa champ et de résolution à l’aide de hello tableau suivant :

|Code d’erreur de connexion|Raison de l’échec de connexion|Résolution :
| --- | --- | ---
| 81001 | Le ticket Kerberos de l’utilisateur est trop volumineux. | Réduire les appartenances à des groupes de l’utilisateur, puis réessayez.
| 81002 | Ticket Kerberos de l’utilisateur toovalidate impossible. | Consultez la [liste de contrôle pour la résolution des problèmes](#troubleshooting-checklist).
| 81003 | Ticket Kerberos de l’utilisateur toovalidate impossible. | Consultez la [liste de contrôle pour la résolution des problèmes](#troubleshooting-checklist).
| 81004 | Échec de la tentative d’authentification Kerberos. | Consultez la [liste de contrôle pour la résolution des problèmes](#troubleshooting-checklist).
| 81008 | Ticket Kerberos de l’utilisateur toovalidate impossible. | Consultez la [liste de contrôle pour la résolution des problèmes](#troubleshooting-checklist).
| 81009 | « Ticket Kerberos de l’utilisateur toovalidate impossible. | Consultez la [liste de contrôle pour la résolution des problèmes](#troubleshooting-checklist).
| 81010 | Échec de l’authentification unique transparente, car le ticket Kerberos de l’utilisateur hello a expiré ou n’est pas valide. | L’utilisateur doit toosign dans à partir d’un appareil appartenant à un domaine à l’intérieur de votre réseau d’entreprise.
| 81011 | Toofind Impossible d’objet d’utilisateur basé sur les informations de ticket Kerberos de l’utilisateur hello. | Utilisez les informations d’utilisateur Azure AD Connect toosynchronize dans Azure AD.
| 81012 | utilisateur Hello lors de la tentative toosign dans tooAzure AD diffère de l’utilisateur hello connecté à l’appareil de hello. | Connectez-vous à partir d’un autre appareil.
| 81013 | Toofind Impossible d’objet d’utilisateur basé sur les informations de ticket Kerberos de l’utilisateur hello. |Utilisez les informations d’utilisateur Azure AD Connect toosynchronize dans Azure AD. 

## <a name="troubleshooting-checklist"></a>Liste de contrôle pour la résolution des problèmes

Utilisez hello suivant des problèmes de l’authentification unique transparente tootroubleshoot de liste de vérification :

- Vérifiez si la fonctionnalité de l’authentification unique transparente hello est activée dans Azure AD Connect. Si vous ne pouvez pas activer la fonctionnalité hello (par exemple, en raison d’un port de tooa bloqué), assurez-vous que vous disposez de tous les hello [préalables](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) en place.
- Vérifiez si les deux ces Azure AD (https://autologon.microsoftazuread-sso.com et https://aadg.windows.net.nsatc.net) font partie des paramètres de la zone Intranet de l’utilisateur hello.
- Vérifiez que les appareils d’entreprise hello est jointe toohello AD domaine.
- Vérifiez que hello d’utilisateur sur l’appareil toohello à l’aide d’un compte de domaine Active Directory.
- Assurez-vous que le compte de l’utilisateur hello est à partir d’une forêt Active Directory dans lequel l’authentification unique transparente a été défini.
- Vérifiez que hello est connecté sur le réseau d’entreprise de hello.
- Assurez-vous que le temps de l’appareil hello est synchronisée avec hello Active Directory et les contrôleurs de domaine hello et est cinq minutes.
- Liste des tickets Kerberos existants sur l’appareil hello à l’aide de hello **klist** commande à partir d’une invite de commandes. Vérifiez si les tickets émis pour hello `AZUREADSSOACCT` compte d’ordinateur sont présents. En règle générale, la durée de validité des tickets Kerberos des utilisateurs est de 12 heures. Votre instance Active Directory est peut-être paramétrée différemment.
- Purger les tickets Kerberos existants à partir de l’appareil de hello à l’aide de hello **klist purge** de commandes, puis réessayez.
- toodetermine s’il existe des problèmes liés à JavaScript, examinez les journaux de la console hello du navigateur hello (sous « Outils de développement »).
- Hello de révision [contrôleur de domaine consigne](#domain-controller-logs) également.

### <a name="domain-controller-logs"></a>Journaux des contrôleurs de domaine

Si l’audit des succès est activé sur votre contrôleur de domaine, chaque fois qu’un utilisateur se connecte à l’aide de l’authentification unique transparente une entrée de sécurité est enregistrée dans le journal des événements hello. Vous pouvez trouver ces événements de sécurité à l’aide de hello suivant la requête (recherchez l’événement **4769** associé au compte d’ordinateur hello **AzureADSSOAcc$**) :

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Réinitialisation manuelle de la fonctionnalité de hello

Si la résolution des problèmes n’a pas d’aide, vous pouvez réinitialiser manuellement la fonctionnalité de hello sur votre client. Procédez comme suit sur le serveur local de hello où vous exécutez Azure AD Connect :

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>Étape 1 : Importer le module PowerShell de l’authentification unique transparente de hello

1. Tout d’abord, téléchargez et installez hello [Assistant Microsoft Online Services Sign-In](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Puis téléchargez et installez hello [64 bits du module Active Directory de Azure pour Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Accédez toohello `%programfiles%\Microsoft Azure Active Directory Connect` dossier.
4. Module PowerShell de l’authentification unique transparente d’hello importation à l’aide de cette commande : `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Étape 2 : Obtenir la liste de hello des forêts Active Directory sur lequel l’authentification unique transparente a été activée.

1. Exécutez PowerShell en tant qu’administrateur. Dans PowerShell, appelez `New-AzureADSSOAuthenticationContext`. Lorsque vous y êtes invité, fournissez les informations d’identification de l’administrateur général de votre locataire.
2. Appelez `Get-AzureADSSOStatus`. Cette commande fournit que Hello de liste des forêts d’Active Directory (Regardez dans la liste les domaines « hello ») sur lequel cette fonctionnalité a été activée.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Étape 3 : Désactiver l’authentification unique (SSO) transparente pour chaque forêt AD dans laquelle elle a été configurée

1. Appelez `$creds = Get-Credential`. Lorsque vous y êtes invité, entrez informations d’identification d’administrateur de domaine de hello hello destiné à la forêt Active Directory.
2. Appelez `Disable-AzureADSSOForest -OnPremCredentials $creds`. Cette commande supprime hello `AZUREADSSOACCT` compte d’ordinateur à partir de hello localement le contrôleur de domaine pour cette forêt Active Directory spécifique.
3. Répétez hello étapes pour chaque forêt Active Directory que vous avez configuré la fonctionnalité de hello sur précédentes.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Étape 4 : Activer l’authentification unique (SSO) transparente pour chaque forêt AD

1. Appelez `Enable-AzureADSSOForest`. Lorsque vous y êtes invité, entrez informations d’identification d’administrateur de domaine de hello hello destiné à la forêt Active Directory.
2. Répétez hello étapes pour chaque forêt Active Directory que vous voulez tooset fonctionnalité de hello sur précédentes.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Étape 5. Activer la fonctionnalité hello sur votre client

Appelez `Enable-AzureADSSO` et tapez « true » à hello `Enable: ` invite tooturn fonctionnalité hello dans votre client.
