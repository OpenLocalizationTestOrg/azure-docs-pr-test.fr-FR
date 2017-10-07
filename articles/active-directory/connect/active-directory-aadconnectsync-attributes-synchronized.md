---
title: "Attributs synchronisés par Azure AD Connect | Microsoft Docs"
description: "Listes hello attributs synchronisés tooAzure Active Directory."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Synchronisation Azure AD Connect : attributs synchronisés tooAzure Active Directory
Cette rubrique répertorie les attributs de hello sont synchronisées par synchronisation Azure AD Connect.  
les attributs Hello sont regroupés par hello liée application Azure AD.

## <a name="attributes-toosynchronize"></a>Attributs toosynchronize
Une question courante est *quels sont hello d’attributs minimal toosynchronize*. par défaut de Hello et l’approche recommandée est d’attributs par défaut de hello tookeep pour une liste d’adresses globale complète (liste d’adresses globale) peut être construit dans hello cloud et tooget toutes les fonctionnalités dans les charges de travail Office 365. Dans certains cas, il existe certains attributs que votre organisation ne souhaite pas que toohello synchronisé cloud, car ces attributs contiennent sensibles ou données (informations d’identification personnelle) de PII, comme dans cet exemple :  
![mauvais attributs](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

Dans ce cas, démarrez avec une liste hello d’attributs dans cette rubrique et identifier les attributs qui contient des données sensibles ou informations d’identification personnelle et ne peut pas être synchronisés. Ensuite, désélectionnez ces attributs lors de l’installation à l’aide de [l’application Azure AD et du filtrage des attributs](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Lors de la désélection des attributs, vous devez être prudent et uniquement désélectionnez ces toosynchronize absolument pas possible d’attributs. Désélectionner d’autres attributs peut avoir un impact négatif sur les fonctionnalités.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Nom de l'attribut | Utilisateur | Commentaire |
| --- |:---:| --- |
| accountEnabled |X |Détermine si un compte est activé. |
| cn |X | |
| displayName |X | |
| objectSID |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| pwdLastSet |X |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| sourceAnchor |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| usageLocation |X |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |

## <a name="exchange-online"></a>Exchange Online
| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| assistant |X |X | | |
| altRecipient |X | | |Nécessite Azure AD Connect 1.1.552.0 ou version ultérieure. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| société |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimileTelephoneNumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| info |X |X |X |Cet attribut n'est actuellement pas utilisé pour les groupes. |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickName |X |X |X | |
| mangedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Disponible dans Azure AD Connect version 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Cet attribut n'est actuellement pas utilisé par Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Cet attribut n'est actuellement pas utilisé par Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Cet attribut n'est actuellement pas utilisé par Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Cet attribut n'est actuellement pas utilisé par Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Cet attribut n'est actuellement pas utilisé par Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSenderHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg-IsOrganizational | | |X | |
| objectSID |X | |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Dérivé de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailPhoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| société |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimileTelephoneNumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| info |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickName |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Dérivé de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailPhoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| url |X |X | | |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X | | |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| société |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimileTelephoneNumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickName |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| securityEnabled | | |X |Dérivé de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailPhoto |X |X | | |
| title |X |X | | |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X | | |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| cn |X | |X |Nom commun ou alias. Plus souvent hello préfixe valeur [mail]. |
| displayName |X |X |X |Chaîne qui représente le nom de hello souvent affiché comme nom convivial de hello (prénom nom). |
| mail |X |X |X |Adresse de messagerie complète. |
| member | | |X | |
| objectSID |X | |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| proxyAddresses |X |X |X |propriété mécanique. Utilisé par Azure AD. Contient toutes les adresses de messagerie secondaires pour l’utilisateur de hello. |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. |
| securityEnabled | | |X |Dérivé de groupType. |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X | | |Ce nom UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |

## <a name="intune"></a>Intune
| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| c |X |X | | |
| cn |X | |X | |
| description |X |X |X | |
| displayName |X |X |X | |
| mail |X |X |X | |
| mailNickName |X |X |X | |
| member | | |X | |
| objectSID |X | |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| securityEnabled | | |X |Dérivé de groupType |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X | | |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| société |X |X | | |
| countryCode |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimileTelephoneNumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| securityEnabled | | |X |Dérivé de groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| title |X |X | | |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X | | |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |

## <a name="3rd-party-applications"></a>Applications tierces
Ce groupe est un ensemble d’attributs utilisé comme hello attributs minimales requis pour une charge de travail générique ou une application. Il peut être utilisé pour des charges de travail non répertoriées dans une section ou pour une application hors applications Microsoft. Il est utilisé explicitement à la suite hello :

* Yammer (seul l’utilisateur est consommé)
* [Scénarios de collaboration transorganisationnelle B2B (Business-to-Business) hybride proposés par des ressources comme SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Ce groupe est un ensemble d’attributs qui peuvent être utilisés si Windows Azure AD hello n’est pas utilisé toosupport Office 365, Dynamics ou Intune. Il comporte un petit ensemble d’attributs de base.

| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Détermine si un compte est activé. |
| cn |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickName |X |X |X | |
| member | | |X | |
| objectSID |X | | |propriété mécanique. Identificateur de l’utilisateur AD utilisé synchronisation toomaintain entre Azure AD et Active Directory. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |propriété mécanique. Tooknow utilisé lorsque tooinvalidate déjà les jetons émis. Utilisé par la synchronisation de mot de passe et par la fédération. |
| sn |X |X | | |
| sourceAnchor |X |X |X |propriété mécanique. Relation de toomaintain identificateur immuable entre les services AD DS et Azure AD. |
| usageLocation |X | | |propriété mécanique. pays de l’utilisateur Hello. Utilisé pour l’attribution de licence. |
| userPrincipalName |X | | |UPN est hello les ID de connexion pour l’utilisateur de hello. Hello plus souvent identique à la valeur [mail]. |

## <a name="windows-10"></a>Windows 10
Un computer(device) appartenant au domaine de Windows 10 synchronise certains tooAzure d’attributs Active Directory. Pour plus d’informations sur les scénarios de hello, consultez [connecter tooAzure de périphériques joints au domaine Active Directory pour Windows 10 rencontre](../active-directory-azureadjoin-devices-group-policy.md). Ces attributs sont toujours synchronisés et Windows 10 n'apparaît pas comme une application que vous pouvez désélectionner. Un ordinateur joint au domaine de Windows 10 est identifié par ayant hello attribut userCertificate est remplie.

| Nom de l'attribut | Appareil | Commentaire |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |Valeur codée en dur pour les ordinateurs appartenant au domaine. |
| displayName |X | |
| ms-DS-CreatorSID |X |Également appelé registeredOwnerReference. |
| objectGUID |X |Également appelé deviceID. |
| objectSID |X |Également appelé onPremisesSecurityIdentifier. |
| operatingSystem |X |Également appelé deviceOSType. |
| operatingSystemVersion |X |Également appelé deviceOSVersion. |
| userCertificate |X | |

Ces attributs pour **utilisateur** sont en outre toohello autres applications que vous avez sélectionné.  

| Nom de l'attribut | Utilisateur | Commentaire |
| --- |:---:| --- |
| domainFQDN |X |Également appelé dnsDomainName. Par exemple, contoso.com. |
| domainNetBios |X |Également appelé netBiosName. Par exemple, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Écriture différée d’Exchange hybride
Ces attributs sont réécrits à partir d’Azure AD tooon site Active Directory lorsque vous sélectionnez tooenable **Exchange hybride**. Selon votre version d’Exchange, il est possible que moins d’attributs soient synchronisés.

| Nom de l'attribut | Utilisateur | Contact | Groupe | Commentaire |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Dérivé de cloudAnchor dans Azure AD. Cet attribut est une nouveauté dans Exchange 2016 et Windows Server 2016 AD. |
| msExchArchiveStatus |X | | |Archive en ligne : Active les clients tooarchive de la messagerie. |
| msExchBlockedSendersHash |X | | |Filtrage : écrit en différé le filtrage local, les données sécurisées en ligne et les données des expéditeurs bloqués provenant des clients. |
| msExchSafeRecipientsHash |X | | |Filtrage : écrit en différé le filtrage local, les données sécurisées en ligne et les données des expéditeurs bloqués provenant des clients. |
| msExchSafeSenderHash |X | | |Filtrage : écrit en différé le filtrage local, les données sécurisées en ligne et les données des expéditeurs bloqués provenant des clients. |
| msExchUCVoiceMailSettings |X | | |Activer la messagerie unifiée (MU) - messagerie vocale en ligne : utilisée par Microsoft Lync Server intégration tooindicate tooLync serveur local que l’utilisateur hello a vocal dans les services en ligne. |
| msExchUserHoldPolicies |X | | |Gel : Active toodetermine de services de cloud qui sont sous litiges contenir des utilisateurs. |
| proxyAddresses |X |X |X |Hello x500 uniquement l’adresse à partir d’Exchange Online est insérée. |
| publicDelegates |X | | |Permet qu'une toobe de boîte aux lettres Exchange Online accordé toousers de droits SendOnBehalfTo avec boîte aux lettres de Exchange sur site. Nécessite Azure AD Connect 1.1.552.0 ou version ultérieure. |

## <a name="exchange-mail-public-folder"></a>Dossier public de messagerie Exchange
Ces attributs sont synchronisés à partir de tooAzure d’Active Directory sur site Active Directory lorsque vous sélectionnez tooenable **dossier Public de messagerie Exchange**.

| Nom de l'attribut | Dossier public | Commentaire |
| --- | :---:| --- |
| displayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Écriture différée des appareils
Les objets d’appareil sont créés dans Active Directory. Ces objets peuvent être périphériques joints tooAzure AD ou les ordinateurs Windows 10 joints au domaine.

| Nom de l'attribut | Appareil | Commentaire |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| dn |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Uniquement avec le schéma AD de Windows Server 2016 |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Remarques
* Lorsqu’en utilisant un autre ID, hello local attribut userPrincipalName est synchronisé avec onPremisesUserPrincipalName d’attribut hello Azure AD. Hello d’attribut d’un autre ID, de messagerie par exemple, est synchronisé avec hello Azure AD attribut userPrincipalName.
* Dans les listes de hello ci-dessus, hello le type d’objet **utilisateur** s’applique également de type d’objet toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
