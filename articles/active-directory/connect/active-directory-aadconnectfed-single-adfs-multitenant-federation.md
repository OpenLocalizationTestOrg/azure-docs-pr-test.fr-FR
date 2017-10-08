---
title: aaaFederating plusieurs Azure AD avec unique AD FS | Documents Microsoft
description: Dans ce document, vous allez apprendre comment toofederate plusieurs Azure AD avec un seul AD FS.
keywords: "fédérer, ADFS, AD FS, plusieurs locataires, AD FS unique, un seul ADFS, fédération multi-client, adfs à forêts multiples, aad connect, fédération, fédération multi-locataire"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Fédérer plusieurs instances d’Azure AD avec une seule instance d’AD FS

Une même batterie AD FS à haute disponibilité peut fédérer plusieurs forêts si elles entretiennent une relation d’approbation bidirectionnelle. Ces forêts multiples peut ou peut ne pas correspondre toohello même Azure Active Directory. Cet article fournit des instructions sur la fédération tooconfigure entre un déploiement AD FS unique et plusieurs forêts qui toodifferent de synchronisation Azure AD.

![Fédération multi-locataire avec une seule instance d’AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> L’écriture différée sur les appareils et la jonction automatique d’appareils ne sont pas prises en charge dans ce scénario.

> [!NOTE]
> Azure AD Connect ne peut pas être fédération tooconfigure utilisés dans ce scénario Azure AD Connect peut configurer la fédération pour les domaines dans un Azure AD unique.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Étapes de la fédération d’AD FS avec plusieurs instances d’Azure AD

Envisagez de qu'un domaine est contoso.com dans Azure Active Directory contoso.onmicrosoft.com est déjà fédéré avec hello AD FS local installé dans l’environnement de Active Directory local de contoso.com. Fabrikam.com est un domaine dans Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Étape 1 : Établir une relation d’approbation bidirectionnelle
 
Pour AD FS dans contoso.com toobe tooauthenticate en mesure d’utilisateurs du domaine fabrikam.com, une approbation bidirectionnelle est nécessaire entre contoso.com et fabrikam.com. Suivez les indications hello dans ce [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello d’approbation bidirectionnelle.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Étape 2 : Modifier les paramètres de fédération contoso.com 
 
émetteur par défaut est Hello pour un seul domaine fédéré de tooAD FS est « http://ADFSServiceFQDN/adfs/services/trust », par exemple, « http://fs.contoso.com/adfs/services/trust ». Azure Active Directory nécessite un émetteur unique pour chaque domaine fédéré. Étant donné que hello même AD FS va toofederate deux domaines, valeur d’émetteur hello doit toobe modifié afin qu’il soit unique pour chaque domaine QU'AD FS se fédère avec Azure Active Directory. 
 
Sur le serveur de hello AD FS, ouvrez PowerShell Azure AD et effectuer hello comme suit :
 
Se connecter toohello Azure Active Directory qui contient les paramètres fédération hello domaine contoso.com mise à jour Connect-MsolService hello pour contoso.com Update-MsolFederatedDomain - DomainName contoso.com – SupportMultipleDomain
 
L’émetteur dans les paramètres de fédération de domaine hello sera modifié trop « http://contoso.com/adfs/services/trust » et une émission de revendication règle est ajoutée pour hello Azure AD de confiance tooissue hello correct issuerId valeur basée sur un suffixe UPN hello.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Étape 3 : Fédérer fabrikam.com avec AD FS
 
Dans Azure AD powershell session effectuer hello comme suit : se connecter tooAzure Active Directory contenant hello domaine fabrikam.com.

    Connect-MsolService
Convertir toofederated de domaine fabrikam.com gérés hello :

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Hello ci-dessus opération sera fédérer hello domaine fabrikam.com avec hello même AD FS. Vous pouvez vérifier les paramètres de domaine hello à l’aide de Get-MsolDomainFederationSettings pour les deux domaines.

## <a name="next-steps"></a>Étapes suivantes
[Connecter Active Directory à Azure Active Directory](active-directory-aadconnect.md)
