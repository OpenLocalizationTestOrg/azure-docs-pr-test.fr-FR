---
title: aaaTroubleshooting hybride Azure Active Directory joint des appareils Windows 10 et Windows Server 2016 | Documents Microsoft
description: "Résolution des problèmes des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Résolution des problèmes des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory 

Cette rubrique est applicable toohello suivant des clients :

-   Windows 10
-   Windows Server 2016

Pour les autres clients Windows, consultez [Résoudre des problèmes des appareils hybrides de bas niveau joints à Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).

Cette rubrique suppose que vous avez [configuré hybride Azure Active Directory des appareils joints à un](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport les scénarios suivants :

- Accès conditionnel basé sur les appareils

- [Itinérance d’entreprise des paramètres](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello Entreprise](active-directory-azureadjoin-passport-deployment.md)


Ce document fournit des conseils de dépannage sur la façon dont des problèmes potentiels de tooresolve. 


Pour Windows 10 et Windows Server 2016, hybrides Azure Active Directory join prend en charge hello Windows 10 novembre 2015 mise à jour et les versions ultérieures. Nous recommandons à l’aide de la mise à jour anniversaire de hello.

## <a name="step-1-retrieve-hello-join-status"></a>Étape 1 : Récupération de l’état de jointure de hello 

**état de jointure tooretrieve hello :**

1. Invite de commandes ouverte hello en tant qu’administrateur

2. Entrez **dsregcmd /status**



    +----------------------------------------------------------------------+
    | État de l’appareil                                                    | +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined : Aucun ID de périphérique : l’empreinte numérique 5820fbe9-60c8-43b0-bb11-44aee233e4e7 : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : TpmProtected de fournisseur de chiffrement de plateforme Microsoft : Oui KeySignTest : : doit exécuter élevés tootest.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | État utilisateur                                                         | +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>Étape 2 : Évaluer l’état de jointure hello 

Passez en revue les hello suivant des champs et assurez-vous que les valeurs attendues hello :

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

Ce champ indique si l’appareil de hello est joint à Azure AD. Si la valeur hello est **non**, hello tooAzure jointure AD n’est pas encore terminée. 

**Causes possibles :**

- Échec de l’authentification d’ordinateur hello pour une jointure.

- Il existe un proxy HTTP dans l’organisation hello qui ne peut pas être découverts par ordinateur de hello

- ordinateur de Hello ne peut pas atteindre tooauthenticate d’Azure AD ou Azure DRS pour l’inscription

- Hello ordinateur peut-être pas sur le réseau interne de l’organisation hello ou VPN avec la ligne de vue directe tooan contrôleur de domaine Active Directory local.

- Si hello est équipé d’un module de plateforme sécurisée, il peut être dans un état incorrect.

- Il peut y avoir une configuration incorrecte dans les services de hello mentionné dans le document de hello que vous devez à nouveau tooverify. Voici des exemples courants :

    - Votre serveur de fédération n’a pas de points de terminaison WS-Trust activés

    - Votre serveur de fédération n’autorise peut-être pas l’authentification entrante à partir d’ordinateurs de votre réseau à l’aide de l’authentification Windows intégrée.

    - Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

Ce champ indique si l’appareil de hello est joint tooan locale Active Directory ou non. Si la valeur hello est **non**, appareil de hello ne peut pas effectuer une jointure hybrides Azure AD.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

Ce champ indique si l’appareil de hello est inscrit auprès d’Azure AD en tant qu’un appareil personnel (marqué comme *espace de travail joint*). Cette valeur doit être **NON** pour un ordinateur appartenant à un domaine qui est également une jonction hybride Azure AD. Si la valeur hello est **Oui**, un compte professionnel ou scolaire a été ajouté achèvement toohello préalable de jointure de hello hybrides Azure AD. Dans ce cas, le compte de hello est ignoré lorsque vous utilisez la version de mise à jour anniversaire hello de Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES et AzureADPrt : YES
  
Ces champs indiquent si les utilisateurs de hello a été authentifié tooAzure AD lors de la connexion toohello appareil. Si les valeurs hello sont **non**, il peut être dû :

- Clé de stockage incorrecte (STK) dans le TPM associé au périphérique hello lors de l’enregistrement (vérification hello KeySignTest lors de son exécution avec élévation de privilèges).

- ID de connexion de substitution

- Proxy HTTP introuvable

## <a name="next-steps"></a>Étapes suivantes

Pour toute question, consultez hello [Forum aux questions sur la gestion des appareils](device-management-faq.md) 
