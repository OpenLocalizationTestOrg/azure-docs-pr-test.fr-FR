---
title: ordinateurs joints au aaaTroubleshooting hello-inscription automatique de domaine Azure AD pour Windows 10 et Windows Server 2016 | Documents Microsoft
description: "Résolution des problèmes d’inscription automatique hello de domaine Azure AD les ordinateurs joints pour Windows 10 et Windows Server 2016."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016

Cette rubrique est applicable toohello suivant des clients :

-   Windows 10
-   Windows Server 2016

Pour d’autres clients de Windows, consultez [résolution des problèmes d’enregistrement automatique du domaine joint tooAzure d’ordinateurs Active Directory pour les clients de bas niveau Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

Cette rubrique suppose que vous avez configuré l’inscription automatique des appareils joints au domaine comme expliqué dans décrites dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-device-registration-get-started.md) hello toosupport les scénarios suivants :

- [Accès conditionnel basé sur les appareils](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Itinérance d’entreprise des paramètres](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello Entreprise](active-directory-azureadjoin-passport-deployment.md)


Ce document fournit des conseils de dépannage sur la façon dont des problèmes potentiels de tooresolve. 

Hello l’inscription est pris en charge dans les Windows hello mise à jour 10 novembre 2015 et versions ultérieures.  
Nous vous recommandons d’utiliser hello mise à jour anniversaire pour activer les scénarios de hello ci-dessus.

## <a name="step-1-retrieve-hello-registration-status"></a>Étape 1 : Récupération de l’état de l’inscription de hello 

**état de l’inscription de hello tooretrieve :**

1. Ouvrez l’invite de commandes hello en tant qu’administrateur.

2. Entrez **dsregcmd /status**



    +----------------------------------------------------------------------+
    | État de l’appareil                                                    | +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined : Aucun ID de périphérique : l’empreinte numérique 5820fbe9-60c8-43b0-bb11-44aee233e4e7 : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : TpmProtected de fournisseur de chiffrement de plateforme Microsoft : Oui KeySignTest : : doit exécuter élevés tootest.
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | État utilisateur                                                         | +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>Étape 2 : Évaluer l’état de l’inscription de hello 

Passez en revue les hello suivant des champs et assurez-vous que les valeurs attendues hello :

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

Ce champ indique si l’appareil de hello est inscrit auprès d’Azure AD. Si la valeur de hello est affichée comme « Non », l’enregistrement n’est pas terminée. 

**Causes possibles :**

- Échec de l’authentification d’ordinateur hello pour l’inscription.

- Il existe un proxy HTTP dans l’organisation hello qui ne peut pas être découverts par ordinateur de hello

- ordinateur de Hello ne peut pas accéder à Azure AD pour l’authentification ou le service DRS Azure pour l’inscription

- Hello ordinateur peut-être pas sur le réseau interne de l’organisation hello ou VPN avec la ligne de vue directe tooan contrôleur de domaine Active Directory local.

- Si hello est équipé d’un module de plateforme sécurisée, il peut être dans un état incorrect.

- Il peut y avoir une configuration incorrecte dans les services mentionné dans le document de hello que vous devez à nouveau tooverify. Voici des exemples courants :

    - Votre serveur de fédération n’a pas de points de terminaison WS-Trust activés

    - Votre serveur de fédération n’autorise peut-être pas l’authentification entrante à partir d’ordinateurs de votre réseau à l’aide de l’authentification Windows intégrée.

    - Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

Ce champ indique si hello est tooan jointes locale Active Directory ou pas. Si la valeur de hello est affichée en tant que **non**, appareil de hello ne peut pas l’enregistrement automatique avec Azure AD. Vérifiez d’abord que toohello de jointures hello appareil local Active Directory avant il peut s’inscrire auprès d’Azure AD. Si vous cherchez à l’attachement hello ordinateur tooAzure AD directement, accédez tooLearn sur les fonctionnalités d’Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

Ce champ indique si l’appareil de hello est inscrit auprès d’Azure AD, mais comme un appareil personnel (marqué comme « Espace de travail joint »). Si cette valeur doit être 'Non' pour un ordinateur joint à un domaine enregistré auprès d’Azure AD, toutefois s’il apparaît en tant qu’Oui, cela signifie qu’un compte professionnel ou scolaire était enregistrement de fin ordinateur ajouté toohello préalable. Dans ce cas les compte hello seront ignorée si vous utilisez la version de mise à jour anniversaire hello de Windows 10 (1607 lorsque exécutant la commande WinVer de hello hello fenêtre « Exécuter » ou une fenêtre d’invite de commandes).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES et AzureADPrt : YES
  
Ces champs indiquent que l’utilisateur hello a été authentifié tooAzure AD lors de l’ouverture de session toohello appareil. Si elles affichent 'NO' hello Voici les causes possibles :

- Clé de stockage incorrecte (STK) dans le TPM associé au périphérique hello lors de l’enregistrement (vérification hello KeySignTest lors de son exécution avec élévation de privilèges).

- ID de connexion de substitution

- Proxy HTTP introuvable

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez hello [Forum aux questions sur l’inscription automatique](active-directory-device-registration-faq.md) 
