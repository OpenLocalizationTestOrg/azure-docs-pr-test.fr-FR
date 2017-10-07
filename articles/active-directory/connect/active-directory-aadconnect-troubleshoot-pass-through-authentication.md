---
title: "Azure AD Connect : résolution des problèmes d’authentification directe | Microsoft Docs"
description: "Cet article décrit comment tootroubleshoot l’authentification Azure Active Directory (Azure AD) pass-through."
services: active-directory
keywords: "Résolution des problèmes d’authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
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
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Résolution des problèmes d’authentification directe Azure Active Directory

Cet article fournit des informations sur les problèmes courants liés à l’authentification directe Azure AD.

>[!IMPORTANT]
>Si vous êtes confronté à des problèmes utilisateur de connexion avec authentification directe, n’hello de désactiver ou désinstaller des Agents de l’authentification directe sans avoir un toofall de compte d’administrateur général cloud uniquement sur. Découvrez comment [ajouter un compte d’administrateur général de type cloud uniquement](../active-directory-users-create-azure-portal.md). Cette étape est essentielle pour éviter que votre locataire ne soit verrouillé.

## <a name="general-issues"></a>Problèmes d’ordre général

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Vérifiez l’état de la fonctionnalité de hello et d’Agents de l’authentification

Vérifiez que cette fonctionnalité d’authentification directe hello est toujours **activé** sur votre client et hello d’état des Agents de l’authentification montre **Active**et non pas **inactif**. Vous pouvez vérifier l’état à passer de toohello **Azure AD Connect** panneau sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com/).

![Centre d’administration Azure Active Directory - panneau Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centre d’administration Azure Active Directory - panneau Authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Message d’erreur lors de la connexion utilisateur

Si l’utilisateur hello est toosign impossible dans à l’aide de l’authentification directe, ils peuvent consultez hello suivant les erreurs rencontrées par les utilisateurs sur l’écran de connexion hello Azure AD : 

|Error|Description|Résolution :
| --- | --- | ---
|AADSTS80001|Impossible de tooconnect tooActive Active|Assurez-vous que les serveurs de l’agent sont membres de la forêt de hello même AD en tant qu’utilisateurs hello dont les mots de passe doivent toobe validé et qu’ils sont en mesure de tooconnect tooActive active.  
|AADSTS8002|Un délai d’attente s’est produite lors de la connexion tooActive Active|Vérifiez tooensure que Active Directory est disponible et répond toorequests des agents de hello.
|AADSTS80004|nom d’utilisateur Hello passé toohello agent n’est pas valide|Vérifiez que hello utilisateur essaye de toosign avec le nom d’utilisateur hello.
|AADSTS80005|La validation a rencontré une WebException imprévisible|Erreur temporaire. Réessayez la demande de hello. S’il continue toofail, contactez le support Microsoft.
|AADSTS80007|Une erreur s’est produite lors de la communication avec Active Directory|Vérifiez les journaux d’agent hello pour plus d’informations et vérifier qu’Active Directory fonctionne comme prévu.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Raisons d’échec de connexion sur le centre d’administration Active Directory de Azure hello

Commencez le dépannage des problèmes de connexion de l’utilisateur en examinant hello [rapport d’activité de connexion](../active-directory-reporting-activity-sign-ins.md) sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com/).

![Centre d’administration Azure Active Directory - rapport de connexions](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Accédez trop**Azure Active Directory** -> **connexions** sur hello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com/) sur l’activité de connexion d’un utilisateur spécifique. Recherchez hello **CODE d’erreur de connexion** champ. Mapper la valeur hello de cette raison de l’échec tooa champ et de résolution à l’aide de hello tableau suivant :

|Code d’erreur de connexion|Raison de l’échec de connexion|Résolution :
| --- | --- | ---
| 50144 | Le mot de passe Active Directory de l’utilisateur est arrivé à expiration. | Réinitialiser le mot de passe de l’utilisateur hello dans votre annuaire Active Directory local.
| 80001 | Agents d’authentification non disponibles. | Installez l’agent d’authentification, puis procédez à son inscription.
| 80002 | La demande de validation du mot de passe de l’Agent d’authentification est arrivée à expiration. | Vérifiez si votre annuaire Active Directory est accessible à partir de l’Agent d’authentification de hello.
| 80003 | Réponse non valide reçue par l’Agent d’authentification. | Si le problème de hello est constamment reproductible entre plusieurs utilisateurs, vérifiez votre configuration Active Directory.
| 80004 | Nom d’utilisateur principal (UPN) incorrect utilisé dans la demande de connexion. | Demandez à toosign d’utilisateur hello avec le nom d’utilisateur correct de hello.
| 80005 | Agent d’authentification : une erreur s’est produite. | Erreur temporaire. Réessayez ultérieurement.
| 80007 | TooActive de tooconnect Impossible de l’Agent d’authentification Active. | Vérifiez si votre annuaire Active Directory est accessible à partir de l’Agent d’authentification de hello.
| 80010 | Mot de passe d’authentification Agent toodecrypt impossible. | Si le problème de hello est constamment reproductible, installer et inscrire un nouvel Agent de l’authentification. Et désinstaller hello en cours. 
| 80011 | Clé de déchiffrement de l’authentification Agent tooretrieve impossible. | Si le problème de hello est constamment reproductible, installer et inscrire un nouvel Agent de l’authentification. Et désinstaller hello en cours.

## <a name="authentication-agent-installation-issues"></a>Problèmes d’installation de l’agent d’authentification

### <a name="an-unexpected-error-occurred"></a>Une erreur inattendue s’est produite

[Collecter les journaux de l’agent](#collecting-pass-through-authentication-agent-logs) de serveur de hello et contactez le Support Microsoft avec votre problème.

## <a name="authentication-agent-registration-issues"></a>Problèmes d’inscription de l’agent d’authentification

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>L’inscription de hello Agent d’authentification a échoué en raison de tooblocked ports

Vérifiez ce serveur hello sur quel hello Agent d’authentification a été installé peut communiquer avec notre service URL et les ports répertoriés [ici](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>L’enregistrement de hello Agent d’authentification a échoué en raison des erreurs d’autorisation tootoken ou compte

Veillez à utiliser un compte d’administrateur général cloud pour toutes les opérations d’installation et d’inscription Azure AD Connect ou d’agent d’authentification autonome. Il existe un problème connu avec les comptes d’authentification Multifacteur activée un administrateur Global ; désactiver l’authentification Multifacteur temporairement (seules les opérations toocomplete hello) comme solution de contournement.

### <a name="an-unexpected-error-occurred"></a>Une erreur inattendue s’est produite

[Collecter les journaux de l’agent](#collecting-pass-through-authentication-agent-logs) de serveur de hello et contactez le Support Microsoft avec votre problème.

## <a name="authentication-agent-uninstallation-issues"></a>Problèmes de désinstallation de l’agent d’authentification

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Message d’avertissement lors de la désinstallation d’Azure AD Connect

Si vous avez pass-through activé l’authentification sur votre client et que vous essayez toouninstall Azure AD Connect, il montre vous hello message d’avertissement suivant : « les utilisateurs ne sera pas en mesure de toosign tooAzure AD sauf si vous avez d’autres agents de l’authentification directe installé sur d’autres serveurs. »

Assurez-vous que votre installation est [haute disponible](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) avant de désinstaller tooavoid Azure AD Connect avec rupture de connexion d’utilisateur.

## <a name="issues-with-enabling-hello-feature"></a>Problèmes liés à l’activation de fonctionnalité de hello

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Échec de l’activation de fonctionnalité de hello, car il n’y a aucun agent d’authentification disponibles

Vous devez toohave au moins un active l’Agent d’authentification tooenable authentification directe sur votre client. Vous pouvez installer un agent d’authentification en installant Azure AD Connect ou un agent d’authentification autonome.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>L’activation de fonctionnalité de hello a échoué en raison des ports de tooblocked

Vérifiez ce serveur hello sur lequel est installé Azure AD Connect peut communiquer avec notre service URL et les ports répertoriés [ici](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>L’activation de fonctionnalité de hello a échoué en raison des erreurs d’autorisation tootoken ou compte

Assurez-vous que vous utilisez un compte d’administrateur général uniquement dans le cloud lorsque vous activez la fonctionnalité de hello. Il existe un problème connu avec l’authentification multifacteur (MFA)-activé les comptes d’administrateur Global ; désactiver l’authentification Multifacteur temporairement (uniquement une opération toocomplete hello) comme solution de contournement.

## <a name="exchange-activesync-configuration-issues"></a>Problèmes de configuration Exchange ActiveSync

Voici les problèmes courants de hello lorsque vous configurez la prise en charge Exchange ActiveSync pour l’authentification directe.

### <a name="exchange-powershell-issue"></a>Problème lié à Exchange PowerShell

Si vous voyez hello »**un paramètre ne peut pas être trouvé qui correspond au nom de paramètre 'PerTenantSwitchToESTSEnabled'\.**» erreur lorsque vous exécutez hello `Set-OrganizationConfig` Exchange PowerShell command, contactez le Support Microsoft.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync ne fonctionne ne pas

configuration de Hello en vigueur une fois tootake - hello laps de temps dépend de votre environnement. Si la situation de hello persiste pendant un certain temps, contactez le Support Microsoft.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Collecte des journaux des agents d’authentification directe

En fonction de type hello du problème que vous avez peut-être, vous devez toolook dans des emplacements différents pour les journaux de l’Agent d’authentification pass-through.

### <a name="authentication-agent-event-logs"></a>Journaux des événements des agents d’authentification

Les erreurs liés toohello Agent d’authentification, ouvrez hello application Observateur d’événements sur le serveur de hello et vérifiez sous **d’Application et de Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Pour l’analytique détaillées, activer le journal de « Session » hello. N’exécutez pas hello Agent d’authentification avec ce journal activé pendant les opérations normales ; Utilisez cette option uniquement pour le dépannage. contenu du journal Hello est visibles uniquement après la désactivation du journal de hello à nouveau.

### <a name="detailed-trace-logs"></a>Journaux de suivi détaillés

tootroubleshoot utilisateur échecs de connexion, recherchez les journaux de trace au **%programdata%\Microsoft\Azure AD Agent\Trace de l’authentification de connexion\\**. Ces journaux incluent les raisons pour lesquelles un utilisateur spécifique Échec de la connexion à l’aide de la fonctionnalité d’authentification directe hello. Ces erreurs sont également des raisons d’échec de connexion mappé toohello illustrés hello précédent [table](#sign-in-failure-reasons-on-the-Azure-portal). Vous trouverez ci-dessous un exemple d’entrée de journal :

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

Vous pouvez obtenir la description détaillée de l’erreur hello ('1328 « Bonjour précédent exemple) en ouvrant hello invite de commandes et en cours d’exécution hello commande suivante (Remarque : remplacez '1328' avec le numéro de l’erreur hello que vous voyez dans vos journaux) :

`Net helpmsg 1328`

![Authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Journaux des contrôleurs de domaine

Si l’enregistrement d’audit est activé, vous pouvez trouver des informations supplémentaires dans les journaux de sécurité hello de vos contrôleurs de domaine. Un moyen simple tooquery demandes de connexion envoyées par les Agents de l’authentification directe est la suivante :

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Compteurs Analyseur de performances

Une autre façon toomonitor Agents d’authentification est compteurs de performances spécifiques tootrack sur chaque serveur sur lequel est installé hello Agent d’authentification. Hello utilisation suivant compteurs globaux (**les authentifications # PTA**, **#PTA échecs d’authentification** et **les authentifications réussies #PTA**) et les compteurs d’erreurs (**Erreurs d’authentification # PTA**) :

![Compteurs Analyseur de performances de l’authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>L’authentification directe assure la haute disponibilité à l’aide de plusieurs agents d’authentification, et _non_ de l’équilibrage de charge. Selon votre configuration, les agents d’authentification ne reçoivent _pas_ tous le _même_ nombre exact de demandes. Il est possible qu’un agent d’authentification spécifique ne reçoive aucun trafic du tout.
