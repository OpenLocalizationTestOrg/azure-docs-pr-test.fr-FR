---
title: "aaaAzure l’authentification basée sur certificat Active Directory - prise en main | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification basée sur certificat dans votre environnement"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Bien démarrer avec l’authentification par certificat dans Azure Active Directory

L’authentification basée sur certificat vous permet de toobe authentifié par Azure Active Directory avec un certificat client sur un appareil Windows, Android ou iOS lors de la connexion de votre compte en ligne Exchange pour : 

- Des applications mobiles Office, telles que Microsoft Outlook et Microsoft Word ;   

- Des clients Exchange ActiveSync (EAS). 

La configuration de cette fonctionnalité évite hello besoin tooenter un nom d’utilisateur et mot de passe dans certaines applications de Microsoft Office sur votre appareil mobile et de messagerie. 

Cette rubrique :

- Fournit des hello tooconfigure les étapes et utiliser l’authentification basée sur certificat pour les utilisateurs de clients dans Office 365 entreprise, entreprise, éducation et plans du gouvernement des États-Unis. Cette fonctionnalité est disponible en version préliminaire dans les plans Office 365 China, US Government Defense et US Government Federal. 

- Suppose que vous avez déjà une [infrastructure de clé publique (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) et [AD FS](connect/active-directory-aadconnectfed-whatis.md) configurés.    


## <a name="requirements"></a>Configuration requise

l’authentification basée sur certificat tooconfigure, suivants de hello doivent être remplies :  

- L’authentification basée sur les certificats est uniquement prise en charge dans les environnements fédérés pour les applications de navigateur ou les clients natifs qui utilisent l’authentification moderne (ADAL). une exception de Hello est Exchange Active Sync (EAS) pour EXO qui peut être utilisé pour les comptes à la fois, fédérés et gérés. 

- autorité de certification racine Hello et toutes les autorités de certification intermédiaires doivent être configurées dans Azure Active Directory.  

- Chaque autorité de certification doit avoir une liste de révocation de certificat (CRL) qui peut être référencée via une URL accessible sur Internet.  

- Vous devez disposer d’au moins une autorité de certification configurée dans Azure Active Directory. Vous trouverez les étapes associées Bonjour [configurer des autorités de certification hello](#step-2-configure-the-certificate-authorities) section.  

- Pour les clients Exchange ActiveSync, certificat de client hello doit avoir hello routable messagerie d’un utilisateur d’adresses dans Exchange en ligne dans un nom Principal de hello ou hello valeur RFC822 nom du champ de l’autre nom hello. Azure Active Directory mappe l’attribut hello RFC822 value toohello adresse Proxy dans le répertoire de hello.  

- Votre appareil client doit avoir accès tooat au moins un certificat qui émet des certificats de client.  

- Un certificat client pour l’authentification du client doit avoir été émis tooyour client.  




## <a name="step-1-select-your-device-platform"></a>Étape 1 : Sélectionner la plateforme de votre appareil

Dans un premier temps, pour la plate-forme de périphérique hello que vous intéressent, vous tooreview hello éléments suivants sont nécessaires :

- prise en charge des applications mobiles Hello Office 
- besoins spécifiques d’implémentation de Hello  

Hello liées aux informations existent pour hello suivant des plateformes d’appareils :

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Étape 2 : Configurer les autorités de certification hello 

tooconfigure vos autorités de certification dans Azure Active Directory, pour chaque autorité de certification, téléchargement hello suivant : 

* Hello partie publique du certificat de hello, dans *.cer* format 
* Hello Internet faisant face à des URL où hello listes de révocation de certificats (CRL) résident

schéma Hello pour une autorité de certification se présente comme suit : 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Pour la configuration de hello, vous pouvez utiliser hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Démarrez Windows PowerShell avec les privilèges administrateur. 
2. Installer le module de hello Azure AD. Vous devez tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ou une version ultérieure.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

Une première étape de configuration, vous devez tooestablish une connexion avec votre client. Dès qu’un client de tooyour connexion existe, vous pouvez examiner, ajouter, supprimer et modifier des autorités de certification hello approuvé qui sont définies dans votre annuaire. 

### <a name="connect"></a>Connecter

tooestablish une connexion avec votre client, utilisez hello [organisation de se connecter](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) applet de commande :

    Connect-AzureAD 


### <a name="retrieve"></a>Récupération 

les autorités de certification tooretrieve hello approuvé qui sont définies dans votre annuaire, utilisez hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Ajouter

toocreate une autorité de certification approuvée, utilisez hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande et ensemble hello **crlDistributionPoint** attribut la valeur correcte de tooa : 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Supprimer

tooremove une autorité de certification approuvée, utilisez hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande :
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modifier

toomodify une autorité de certification approuvée, utilisez hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande :

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Étape 3 : Configurer la révocation

toorevoke un certificat client, Azure Active Directory extrait le certificat hello téléchargés en tant que partie des informations d’autorité de certificat de la liste de révocation (CRL) à partir de l’URL de hello et met en cache. Hello publier dernier horodatage (**Date d’effet** propriété) Bonjour CRL sert tooensure hello CRL est toujours valide. Hello CRL est régulièrement référencé toorevoke accès toocertificates qui font partie de la liste de hello.

Si une révocation plus instantanée est requise (par exemple, si un utilisateur perd un appareil), le jeton d’autorisation de hello d’utilisateur de hello peut être invalidée. tooinvalidate Bonjour d’autorisation jeton, définissez Bonjour **StsRefreshTokenValidFrom** pour cet utilisateur particulier à l’aide de Windows PowerShell. Vous devez mettre à jour hello **StsRefreshTokenValidFrom** champ pour chaque utilisateur que vous souhaitez accéder toorevoke pour.

tooensure que la révocation de hello persiste, vous devez définir hello **Date d’effet** de date de tooa hello CRL après la valeur hello définie par **StsRefreshTokenValidFrom** et assurez-vous que le certificat hello en question se trouve dans Hello CRL.

Hello suivant étapes plan hello processus pour la mise à jour et invalider le jeton d’autorisation hello en définissant un hello **StsRefreshTokenValidFrom** champ. 

**révocation de tooconfigure :** 

1. Se connecter avec le service d’administration d’informations d’identification toohello MSOL : 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Récupérer hello StsRefreshTokensValidFrom valeur actuelle pour un utilisateur : 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Configurer une nouvelle valeur StsRefreshTokensValidFrom pour l’horodatage actuel de hello utilisateur toohello égal : 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

date de Hello que vous définissez doit être Bonjour futures. Si la date de hello n’est pas hello future, hello **StsRefreshTokensValidFrom** propriété n’est pas définie. Si la date hello est hello future, **StsRefreshTokensValidFrom** a la valeur toohello heure actuelle (pas les dates de hello indiqué par la commande de Set-MsolUser). 


## <a name="step-4-test-your-configuration"></a>Étape 4 : Tester votre configuration

### <a name="testing-your-certificate"></a>Test de votre certificat

Comme un premier test de configuration, vous devez essayer trop toosign dans[Outlook Web Access](https://outlook.office365.com) ou [SharePoint Online](https://microsoft.sharepoint.com) à l’aide de votre **navigateur de l’appareil sur**.

Si votre connexion est réussie, vous savez que :

- certificat de l’utilisateur Hello a été approvisionné tooyour test appareil
- AD FS est correctement configuré  


### <a name="testing-office-mobile-applications"></a>Test des applications Office mobiles

**authentification basée sur certificat tootest sur votre application Office mobile :** 

1. Sur votre appareil de test, installez une application Office mobile (par exemple, OneDrive).
3. Lancez l’application hello. 
4. Entrez votre nom d’utilisateur, puis sélectionnez hello utilisateur certificat toouse. 

Vous devez être connecté. 

### <a name="testing-exchange-activesync-client-applications"></a>Test des applications clientes Exchange ActiveSync

tooaccess Exchange ActiveSync (EAS) via l’authentification basée sur certificat, un profil EAS contenant le certificat de client hello doit être disponible toohello application. 

Hello profil EAS doit contenir hello informations suivantes :

- Hello toobe de certificat d’utilisateur utilisé pour l’authentification 

- point de terminaison Hello EAS (par exemple, outlook.office365.com)

Un profil EAS sont configurables et placé sur l’appareil hello grâce à l’utilisation de hello de gestion des appareils mobiles (MDM) telle qu’Intune ou en plaçant manuellement les certificats de hello Bonjour profil EAS sur les appareils hello.  

### <a name="testing-eas-client-applications-on-android"></a>Test des applications clientes EAS sur Android

**authentification du certificat tootest :**  

1. Configuration d’un profil EAS dans l’application hello qui satisfait aux exigences de hello ci-dessus.  
2. Ouvrez l’application hello et vérifier la synchronisation de la messagerie. 

