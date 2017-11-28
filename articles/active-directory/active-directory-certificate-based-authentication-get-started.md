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
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="32b13-103">Bien démarrer avec l’authentification par certificat dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32b13-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="32b13-104">L’authentification basée sur certificat vous permet de toobe authentifié par Azure Active Directory avec un certificat client sur un appareil Windows, Android ou iOS lors de la connexion de votre compte en ligne Exchange pour :</span><span class="sxs-lookup"><span data-stu-id="32b13-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="32b13-105">Des applications mobiles Office, telles que Microsoft Outlook et Microsoft Word ;</span><span class="sxs-lookup"><span data-stu-id="32b13-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="32b13-106">Des clients Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="32b13-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="32b13-107">La configuration de cette fonctionnalité évite hello besoin tooenter un nom d’utilisateur et mot de passe dans certaines applications de Microsoft Office sur votre appareil mobile et de messagerie.</span><span class="sxs-lookup"><span data-stu-id="32b13-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="32b13-108">Cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="32b13-108">This topic:</span></span>

- <span data-ttu-id="32b13-109">Fournit des hello tooconfigure les étapes et utiliser l’authentification basée sur certificat pour les utilisateurs de clients dans Office 365 entreprise, entreprise, éducation et plans du gouvernement des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="32b13-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="32b13-110">Cette fonctionnalité est disponible en version préliminaire dans les plans Office 365 China, US Government Defense et US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="32b13-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="32b13-111">Suppose que vous avez déjà une [infrastructure de clé publique (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) et [AD FS](connect/active-directory-aadconnectfed-whatis.md) configurés.</span><span class="sxs-lookup"><span data-stu-id="32b13-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="32b13-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="32b13-112">Requirements</span></span>

<span data-ttu-id="32b13-113">l’authentification basée sur certificat tooconfigure, suivants de hello doivent être remplies :</span><span class="sxs-lookup"><span data-stu-id="32b13-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="32b13-114">L’authentification basée sur les certificats est uniquement prise en charge dans les environnements fédérés pour les applications de navigateur ou les clients natifs qui utilisent l’authentification moderne (ADAL).</span><span class="sxs-lookup"><span data-stu-id="32b13-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="32b13-115">une exception de Hello est Exchange Active Sync (EAS) pour EXO qui peut être utilisé pour les comptes à la fois, fédérés et gérés.</span><span class="sxs-lookup"><span data-stu-id="32b13-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="32b13-116">autorité de certification racine Hello et toutes les autorités de certification intermédiaires doivent être configurées dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32b13-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="32b13-117">Chaque autorité de certification doit avoir une liste de révocation de certificat (CRL) qui peut être référencée via une URL accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="32b13-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="32b13-118">Vous devez disposer d’au moins une autorité de certification configurée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32b13-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="32b13-119">Vous trouverez les étapes associées Bonjour [configurer des autorités de certification hello](#step-2-configure-the-certificate-authorities) section.</span><span class="sxs-lookup"><span data-stu-id="32b13-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="32b13-120">Pour les clients Exchange ActiveSync, certificat de client hello doit avoir hello routable messagerie d’un utilisateur d’adresses dans Exchange en ligne dans un nom Principal de hello ou hello valeur RFC822 nom du champ de l’autre nom hello.</span><span class="sxs-lookup"><span data-stu-id="32b13-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="32b13-121">Azure Active Directory mappe l’attribut hello RFC822 value toohello adresse Proxy dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="32b13-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="32b13-122">Votre appareil client doit avoir accès tooat au moins un certificat qui émet des certificats de client.</span><span class="sxs-lookup"><span data-stu-id="32b13-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="32b13-123">Un certificat client pour l’authentification du client doit avoir été émis tooyour client.</span><span class="sxs-lookup"><span data-stu-id="32b13-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="32b13-124">Étape 1 : Sélectionner la plateforme de votre appareil</span><span class="sxs-lookup"><span data-stu-id="32b13-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="32b13-125">Dans un premier temps, pour la plate-forme de périphérique hello que vous intéressent, vous tooreview hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="32b13-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="32b13-126">prise en charge des applications mobiles Hello Office</span><span class="sxs-lookup"><span data-stu-id="32b13-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="32b13-127">besoins spécifiques d’implémentation de Hello</span><span class="sxs-lookup"><span data-stu-id="32b13-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="32b13-128">Hello liées aux informations existent pour hello suivant des plateformes d’appareils :</span><span class="sxs-lookup"><span data-stu-id="32b13-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="32b13-129">Android</span><span class="sxs-lookup"><span data-stu-id="32b13-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="32b13-130">iOS</span><span class="sxs-lookup"><span data-stu-id="32b13-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="32b13-131">Étape 2 : Configurer les autorités de certification hello</span><span class="sxs-lookup"><span data-stu-id="32b13-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="32b13-132">tooconfigure vos autorités de certification dans Azure Active Directory, pour chaque autorité de certification, téléchargement hello suivant :</span><span class="sxs-lookup"><span data-stu-id="32b13-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="32b13-133">Hello partie publique du certificat de hello, dans *.cer* format</span><span class="sxs-lookup"><span data-stu-id="32b13-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="32b13-134">Hello Internet faisant face à des URL où hello listes de révocation de certificats (CRL) résident</span><span class="sxs-lookup"><span data-stu-id="32b13-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="32b13-135">schéma Hello pour une autorité de certification se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="32b13-135">hello schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="32b13-136">Pour la configuration de hello, vous pouvez utiliser hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="32b13-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="32b13-137">Démarrez Windows PowerShell avec les privilèges administrateur.</span><span class="sxs-lookup"><span data-stu-id="32b13-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="32b13-138">Installer le module de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32b13-138">Install hello Azure AD module.</span></span> <span data-ttu-id="32b13-139">Vous devez tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="32b13-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="32b13-140">Une première étape de configuration, vous devez tooestablish une connexion avec votre client.</span><span class="sxs-lookup"><span data-stu-id="32b13-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="32b13-141">Dès qu’un client de tooyour connexion existe, vous pouvez examiner, ajouter, supprimer et modifier des autorités de certification hello approuvé qui sont définies dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="32b13-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="32b13-142">Connecter</span><span class="sxs-lookup"><span data-stu-id="32b13-142">Connect</span></span>

<span data-ttu-id="32b13-143">tooestablish une connexion avec votre client, utilisez hello [organisation de se connecter](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="32b13-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="32b13-144">Récupération</span><span class="sxs-lookup"><span data-stu-id="32b13-144">Retrieve</span></span> 

<span data-ttu-id="32b13-145">les autorités de certification tooretrieve hello approuvé qui sont définies dans votre annuaire, utilisez hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="32b13-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="32b13-146">Ajouter</span><span class="sxs-lookup"><span data-stu-id="32b13-146">Add</span></span>

<span data-ttu-id="32b13-147">toocreate une autorité de certification approuvée, utilisez hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande et ensemble hello **crlDistributionPoint** attribut la valeur correcte de tooa :</span><span class="sxs-lookup"><span data-stu-id="32b13-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="32b13-148">Supprimer</span><span class="sxs-lookup"><span data-stu-id="32b13-148">Remove</span></span>

<span data-ttu-id="32b13-149">tooremove une autorité de certification approuvée, utilisez hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="32b13-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="32b13-150">Modifier</span><span class="sxs-lookup"><span data-stu-id="32b13-150">Modfiy</span></span>

<span data-ttu-id="32b13-151">toomodify une autorité de certification approuvée, utilisez hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="32b13-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="32b13-152">Étape 3 : Configurer la révocation</span><span class="sxs-lookup"><span data-stu-id="32b13-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="32b13-153">toorevoke un certificat client, Azure Active Directory extrait le certificat hello téléchargés en tant que partie des informations d’autorité de certificat de la liste de révocation (CRL) à partir de l’URL de hello et met en cache.</span><span class="sxs-lookup"><span data-stu-id="32b13-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="32b13-154">Hello publier dernier horodatage (**Date d’effet** propriété) Bonjour CRL sert tooensure hello CRL est toujours valide.</span><span class="sxs-lookup"><span data-stu-id="32b13-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="32b13-155">Hello CRL est régulièrement référencé toorevoke accès toocertificates qui font partie de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="32b13-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="32b13-156">Si une révocation plus instantanée est requise (par exemple, si un utilisateur perd un appareil), le jeton d’autorisation de hello d’utilisateur de hello peut être invalidée.</span><span class="sxs-lookup"><span data-stu-id="32b13-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="32b13-157">tooinvalidate Bonjour d’autorisation jeton, définissez Bonjour **StsRefreshTokenValidFrom** pour cet utilisateur particulier à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32b13-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="32b13-158">Vous devez mettre à jour hello **StsRefreshTokenValidFrom** champ pour chaque utilisateur que vous souhaitez accéder toorevoke pour.</span><span class="sxs-lookup"><span data-stu-id="32b13-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="32b13-159">tooensure que la révocation de hello persiste, vous devez définir hello **Date d’effet** de date de tooa hello CRL après la valeur hello définie par **StsRefreshTokenValidFrom** et assurez-vous que le certificat hello en question se trouve dans Hello CRL.</span><span class="sxs-lookup"><span data-stu-id="32b13-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="32b13-160">Hello suivant étapes plan hello processus pour la mise à jour et invalider le jeton d’autorisation hello en définissant un hello **StsRefreshTokenValidFrom** champ.</span><span class="sxs-lookup"><span data-stu-id="32b13-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="32b13-161">**révocation de tooconfigure :**</span><span class="sxs-lookup"><span data-stu-id="32b13-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="32b13-162">Se connecter avec le service d’administration d’informations d’identification toohello MSOL :</span><span class="sxs-lookup"><span data-stu-id="32b13-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="32b13-163">Récupérer hello StsRefreshTokensValidFrom valeur actuelle pour un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="32b13-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="32b13-164">Configurer une nouvelle valeur StsRefreshTokensValidFrom pour l’horodatage actuel de hello utilisateur toohello égal :</span><span class="sxs-lookup"><span data-stu-id="32b13-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="32b13-165">date de Hello que vous définissez doit être Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="32b13-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="32b13-166">Si la date de hello n’est pas hello future, hello **StsRefreshTokensValidFrom** propriété n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="32b13-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="32b13-167">Si la date hello est hello future, **StsRefreshTokensValidFrom** a la valeur toohello heure actuelle (pas les dates de hello indiqué par la commande de Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="32b13-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="32b13-168">Étape 4 : Tester votre configuration</span><span class="sxs-lookup"><span data-stu-id="32b13-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="32b13-169">Test de votre certificat</span><span class="sxs-lookup"><span data-stu-id="32b13-169">Testing your certificate</span></span>

<span data-ttu-id="32b13-170">Comme un premier test de configuration, vous devez essayer trop toosign dans[Outlook Web Access](https://outlook.office365.com) ou [SharePoint Online](https://microsoft.sharepoint.com) à l’aide de votre **navigateur de l’appareil sur**.</span><span class="sxs-lookup"><span data-stu-id="32b13-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="32b13-171">Si votre connexion est réussie, vous savez que :</span><span class="sxs-lookup"><span data-stu-id="32b13-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="32b13-172">certificat de l’utilisateur Hello a été approvisionné tooyour test appareil</span><span class="sxs-lookup"><span data-stu-id="32b13-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="32b13-173">AD FS est correctement configuré</span><span class="sxs-lookup"><span data-stu-id="32b13-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="32b13-174">Test des applications Office mobiles</span><span class="sxs-lookup"><span data-stu-id="32b13-174">Testing Office mobile applications</span></span>

<span data-ttu-id="32b13-175">**authentification basée sur certificat tootest sur votre application Office mobile :**</span><span class="sxs-lookup"><span data-stu-id="32b13-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="32b13-176">Sur votre appareil de test, installez une application Office mobile (par exemple, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="32b13-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="32b13-177">Lancez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="32b13-177">Launch hello application.</span></span> 
4. <span data-ttu-id="32b13-178">Entrez votre nom d’utilisateur, puis sélectionnez hello utilisateur certificat toouse.</span><span class="sxs-lookup"><span data-stu-id="32b13-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="32b13-179">Vous devez être connecté.</span><span class="sxs-lookup"><span data-stu-id="32b13-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="32b13-180">Test des applications clientes Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="32b13-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="32b13-181">tooaccess Exchange ActiveSync (EAS) via l’authentification basée sur certificat, un profil EAS contenant le certificat de client hello doit être disponible toohello application.</span><span class="sxs-lookup"><span data-stu-id="32b13-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="32b13-182">Hello profil EAS doit contenir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="32b13-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="32b13-183">Hello toobe de certificat d’utilisateur utilisé pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="32b13-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="32b13-184">point de terminaison Hello EAS (par exemple, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="32b13-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="32b13-185">Un profil EAS sont configurables et placé sur l’appareil hello grâce à l’utilisation de hello de gestion des appareils mobiles (MDM) telle qu’Intune ou en plaçant manuellement les certificats de hello Bonjour profil EAS sur les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="32b13-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="32b13-186">Test des applications clientes EAS sur Android</span><span class="sxs-lookup"><span data-stu-id="32b13-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="32b13-187">**authentification du certificat tootest :**</span><span class="sxs-lookup"><span data-stu-id="32b13-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="32b13-188">Configuration d’un profil EAS dans l’application hello qui satisfait aux exigences de hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="32b13-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="32b13-189">Ouvrez l’application hello et vérifier la synchronisation de la messagerie.</span><span class="sxs-lookup"><span data-stu-id="32b13-189">Open hello application, and verify that mail is synchronizing.</span></span> 

