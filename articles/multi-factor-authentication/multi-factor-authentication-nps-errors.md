---
title: "codes d’erreur aaaTroubleshoot hello extension d’Azure MFA NPS | Documents Microsoft"
description: "Obtenir de l’aide de résolution des problèmes de hello extension du serveur NPS pour Azure multi-Factor Authentication avec des solutions spécifiques pour les messages d’erreur courants"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Résoudre les messages d’erreur de hello extension du serveur NPS pour Azure multi-Factor Authentication

Si vous rencontrez des erreurs avec hello extension du serveur NPS pour Azure multi-Factor Authentication, utilisez cette tooreach article une résolution plus rapide. 

## <a name="troubleshooting-steps-for-common-errors"></a>Étapes de résolution des erreurs courantes

| Code d'erreur | Étapes de dépannage |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Contactez le support technique](#contact-microsoft-support)et indiquez la liste hello des étapes pour collecter les journaux. Fournir autant d’informations que possible sur ce qui est arrivé avant l’erreur hello, y compris l’id de client et nom d’utilisateur principal (UPN). |
| **CLIENT_CERT_INSTALL_ERROR** | Il peut y avoir un problème avec le mode certificat hello du client a été installé ou associé à votre client. Suivez les instructions de hello dans [dépannage hello extension de MFA NPS](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate les problèmes de certificat client. |
| **ESTS_TOKEN_ERROR** | Suivez les instructions de hello dans [dépannage hello extension de MFA NPS](multi-factor-authentication-nps-extension.md#troubleshooting) des problèmes de jeton de certificat de client tooinvestigate et la bibliothèque ADAL. |
| **HTTPS_COMMUNICATION_ERROR** | serveur NPS de Hello est réponses tooreceive impossible à partir d’Azure MFA. Vérifiez que votre pare-feu est ouvert bidirectionnel pour tooand le trafic à partir de https://adnotifications.windowsazure.com |
| **HTTP_CONNECT_ERROR** | Sur serveur hello qui exécute l’extension de serveur NPS hello, vérifiez que vous pouvez atteindre https://adnotifications.windowsazure.com et https://login.microsoftonline.com/. Si ces sites ne se chargent pas, résolvez les problèmes de connectivité sur ce serveur. |
| **REGISTRY_CONFIG_ERROR** | Une clé est manquante dans le Registre de hello pour application hello, qui peut être car hello [script PowerShell](multi-factor-authentication-nps-extension.md#install-the-nps-extension) n’a pas été exécuté après l’installation. message d’erreur Hello doit inclure la clé manquante de hello. Vérifiez que vous disposez de clé hello sous HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa. |
| **REQUEST_FORMAT_ERROR** <br> Attribut userName\Identifier Radius obligatoire manquant dans la demande Radius. Vérifiez que le serveur NPS reçoit les demandes RADIUS. | Cette erreur indique généralement un problème d’installation. Hello, extension de serveur NPS doit être installé dans les serveurs NPS qui peuvent recevoir des demandes RADIUS. Les serveurs NPS installés en tant que dépendances de services comme RDG et RRAS ne reçoivent pas les demandes RADIUS. Extension de NPS ne fonctionne pas lors de l’installation sur ces installations et des erreurs, car il ne peut pas lire les détails de hello à partir de la demande d’authentification hello. |
| **REQUEST_MISSING_CODE** | Assurez-vous que protocole de chiffrement de mot de passe hello entre hello NPS et NAS prend en charge la méthode d’authentification secondaire hello que vous utilisez. **PAP** prend en charge toutes les méthodes d’authentification hello d’Azure MFA dans le cloud de hello : appel téléphonique, message texte à sens unique, notification d’application mobile et code de vérification des applications mobiles. **CHAPv2** et **EAP** prennent en charge l’appel téléphonique et la notification d’application mobile. |
| **USERNAME_CANONICALIZATION_ERROR** | Vérifiez que les utilisateur hello est présent dans votre instance d’Active Directory local, et ce Service NPS hello a active de hello tooaccess autorisations. Si vous utilisez des approbations inter-forêts, [contactez le support technique](#contact-microsoft-support) pour plus d’informations. |


   

### <a name="alternate-login-id-errors"></a>Erreurs d’ID de connexion de substitution

| Code d'erreur | Message d’erreur | Étapes de dépannage |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Erreur : échec de la recherche userObjectSid | Vérifiez que l’utilisateur hello existe dans votre instance d’Active Directory local. Si vous utilisez des approbations inter-forêts, [contactez le support technique](#contact-microsoft-support) pour plus d’informations. |
| **ALTERNATE_LOGIN_ID_ERROR** | Erreur : échec de la recherche d’un ID de connexion de substitution | Vérifiez que LDAP_ALTERNATE_LOGINID_ATTRIBUTE est tooa [attribut Active Directory valide](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> Si LDAP_FORCE_GLOBAL_CATALOG a la valeur tooTrue ou LDAP_LOOKUP_FORESTS est configuré avec une valeur non vide, vérifiez que vous avez configuré un catalogue Global et attribut AlternateLoginId hello est ajouté tooit. <br><br> Si LDAP_LOOKUP_FORESTS est configuré avec une valeur non vide, vérifiez que la valeur de hello est correct. S’il existe plus d’un nom de la forêt, les noms de hello doivent être séparés par des points-virgules, pas d’espaces. <br><br> Si ces étapes ne résout le problème de hello, [contactez le support technique](#contact-microsoft-support) pour plus d’informations. |
| **ALTERNATE_LOGIN_ID_ERROR** | Erreur : La valeur relative à l’ID de connexion de substitution est vide | Vérifiez le qu'attribut AlternateLoginId hello est configuré pour l’utilisateur de hello. |


## <a name="errors-your-users-may-encounter"></a>Erreurs que vos utilisateurs pourraient rencontrer

| Code d'erreur | Message d’erreur | Étapes de dépannage |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Client de l’appelant n’a pas accès aux autorisations toodo l’authentification de hello utilisateur | Vérifiez si hello domaine du locataire et hello hello nom d’utilisateur principal (UPN) sont hello identiques. Par exemple, assurez-vous que user@contoso.com tente de client de Contoso tooauthenticate toohello. Hello UPN représente un utilisateur valide pour le client hello dans Azure. |
| **AuthenticationMethodNotConfigured** | Hello spécifié la méthode d’authentification n’était pas configurée pour les utilisateur hello | Avoir utilisateur de hello ajouter ou vérifier leurs méthodes de vérification selon les instructions de toohello de [gérer vos paramètres de vérification en deux étapes](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | La méthode d’authentification spécifiée n’est pas prise en charge. | Effectuez la collecte de tous les journaux incluant cette erreur et [contactez le support technique](#contact-microsoft-support). Lorsque vous contactez le support technique, fournir un nom d’utilisateur hello et une méthode de vérification secondaire hello déclenché hello erreur. |
| **BecAccessDenied** | Appel de MSODS Bec retourné accès refusé, probablement hello username n’est pas défini dans le locataire de hello | utilisateur de Hello est présent dans Active Directory local, mais n’est pas synchronisé dans Azure AD par AD Connect. Ou bien, utilisateur de hello est manquant pour le client de hello. Ajouter hello utilisateur tooAzure AD et demandez-lui d’ajouter leurs méthodes de vérification selon les instructions toohello dans [gérer vos paramètres de vérification en deux étapes](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** ou **StrongAuthenticationServiceInvalidParameter** | numéro de téléphone Hello est dans un format non reconnaissable | Utilisateur de hello être corriger leurs numéros de téléphone de vérification. |
| **InvalidSession** | Hello spécifié de session n’est pas valide ou a expiré | session de Hello a pris plus de trois minutes toocomplete. Vérifiez que l’utilisateur hello est saisie de code de vérification hello ou répond toohello notification d’application, dans les trois minutes d’initier la demande d’authentification hello. Si cela ne résout des problème de hello, vérifiez qu’il n’y a aucune latence réseau entre le client, serveur NAS, serveur NPS et point de terminaison de l’authentification Multifacteur Azure hello.  |
| **NoDefaultAuthenticationMethodIsConfigured** | Aucune méthode d’authentification par défaut a été configuré pour l’utilisateur de hello | Avoir utilisateur de hello ajouter ou vérifier leurs méthodes de vérification selon les instructions de toohello de [gérer vos paramètres de vérification en deux étapes](./end-user/multi-factor-authentication-end-user-manage-settings.md). Vérifiez que l’utilisateur hello a choisi une méthode d’authentification par défaut et configuré de cette méthode pour leur compte. |
| **OathCodePinIncorrect** | Code et PIN saisis erronés. | Cette erreur n’est pas attendue dans hello extension du serveur NPS. Si l’utilisateur la rencontre, [contactez le support technique](#contact-microsoft-support) pour obtenir de l’aide. |
| **ProofDataNotFound** | Données de preuve n’a pas été configurées pour hello spécifié méthode d’authentification. | Avoir utilisateur de hello essayez une autre méthode de vérification, ou ajouter une nouvelle méthodes de vérification selon les instructions de toohello de [gérer vos paramètres de vérification en deux étapes](./end-user/multi-factor-authentication-end-user-manage-settings.md). Si l’utilisateur de hello continue toosee cette erreur après avoir confirmé que leur méthode de vérification est correctement configuré, [contactez le support technique](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Code et PIN saisis erronés. (OneWaySMS) | Cette erreur n’est pas attendue dans hello extension du serveur NPS. Si l’utilisateur la rencontre, [contactez le support technique](#contact-microsoft-support) pour obtenir de l’aide. |
| **TenantIsBlocked** | Locataire bloqué | [Contactez le support technique](#contact-microsoft-support) avec l’ID de répertoire à partir de la page des propriétés hello AD Azure hello portail Azure. |
| **UserNotFound** | utilisateur Hello est introuvable. | client de Hello n’est plus visible comme actif dans Azure AD. Vérifiez que votre abonnement est actif et que vous avez hello requis tout d’abord les applications de tiers. Assurez-vous également locataire hello dans l’objet du certificat hello est comme prévu et cert de hello est toujours valide et inscrite sous principal du service hello. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Messages qui ne sont pas des erreurs que vos utilisateurs peuvent rencontrer

Il peut arriver que vos utilisateurs reçoivent des messages de Multi-Factor Authentication en cas d’échec de leur demande d’authentification. Ceux-ci ne sont pas des erreurs dans le produit hello de configuration, mais sont des avertissements intentionnelles expliquant la raison pour laquelle une demande d’authentification a été refusée.

| Code d'erreur | Message d’erreur | Étapes recommandées | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Code saisi erroné\Code OATH incorrect | Ce n’est pas une erreur, l’utilisateur a entré un code erroné. | utilisateur de Hello entré un code erroné hello. Demandez-lui de réessayer en demandant un nouveau code ou en se reconnectant. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Limite maximale autorisée de tentatives de saisie de code atteinte | utilisateur de Hello Échec de la demande de vérification hello trop souvent. En fonction de vos paramètres, ils peuvent doivent toobe débloqué par un administrateur maintenant.  |
| **SMSAuthFailedWrongCodeEntered** | Code saisi erroné/Mot de passe SMS à usage unique incorrect | utilisateur de Hello entré un code erroné hello. Demandez-lui de réessayer en demandant un nouveau code ou en se reconnectant. |

## <a name="errors-that-require-support"></a>Erreurs qui nécessitent un support

Si vous rencontrez l’une de ces erreurs, nous vous recommandons de [contacter le support technique](#contact-microsoft-support) pour un diagnostic. Il n’existe pas d’étapes standard à suivre pour résoudre ces erreurs. Lorsque vous contactez le support, être vraiment tooinclude en tant que la quantité d’informations que possible sur les étapes de hello qui ont conduit tooan erreur et les informations de votre locataire.

| Code d'erreur | Message d’erreur |
| ---------- | ------------- |
| **InvalidParameter** | Request ne doit pas être null |
| **InvalidParameter** | ObjectId ne doit pas être null ou vide pour ReplicationScope : {0} |
| **InvalidParameter** | longueur de CompanyName de Hello \{0} \ est supérieure à {{1} de la longueur maximale autorisée de hello |
| **InvalidParameter** | UserPrincipalName ne doit pas être null ou vide |
| **InvalidParameter** | Hello fourni que tenantid n’est pas au format correct |
| **InvalidParameter** | SessionId ne doit pas être null ou vide |
| **InvalidParameter** | Résolution impossible des ProofData de la demande ou de Msods. Hello ProofData est inconnu |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Étapes suivantes

### <a name="troubleshoot-user-accounts"></a>Résoudre les problèmes relatifs aux comptes utilisateur

Si vos utilisateurs ont [des difficultés avec la vérification en deux étapes](./end-user/multi-factor-authentication-end-user-troubleshoot.md), aidez-les à diagnostiquer eux-mêmes les problèmes. 

### <a name="contact-microsoft-support"></a>Contact Microsoft support

Si vous avez besoin d’une assistance supplémentaire, contactez un professionnel du support via le [Support du serveur Azure Multi-Factor Authentication](https://support.microsoft.com/oas/default.aspx?prid=14947). Lorsque vous nous contactez, veillez à inclure autant d’informations que possible concernant votre problème. Vous pouvez fournir des informations incluent page hello où vous l’avez vu l’erreur de hello, hello erreur spécifique du code, ID de session spécifique hello hello ID d’utilisateur de hello qui a vu l’erreur de hello et les journaux de débogage.

toocollect des journaux de débogage pour les diagnostics de prise en charge, utilisez hello comme suit : 

1. Ouvrez une invite de commandes administrateur et exécutez les commandes suivantes :

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Reproduire le problème de hello

3. Arrêter le suivi de hello avec ces commandes :

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Code postal contenu hello du dossier C:\NPS hello et attacher des cas de support de toohello fichier hello compressé.


