---
title: "Authentification par certificat Azure Active Directory - Bien démarrer | Microsoft Docs"
description: "Découvrez comment configurer l’authentification par certificat dans votre environnement"
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
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="c2831-103">Bien démarrer avec l’authentification par certificat dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2831-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="c2831-104">L’authentification par certificat vous permet d’être authentifié par Azure Active Directory avec un certificat client sur un appareil Windows, Android ou iOS lors de la connexion de votre compte Exchange Online à :</span><span class="sxs-lookup"><span data-stu-id="c2831-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="c2831-105">Des applications mobiles Office, telles que Microsoft Outlook et Microsoft Word ;</span><span class="sxs-lookup"><span data-stu-id="c2831-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="c2831-106">Des clients Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="c2831-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="c2831-107">La configuration de cette fonctionnalité élimine le besoin d’entrer un nom d’utilisateur et un mot de passe dans certaines applications de messagerie et Microsoft Office sur votre appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="c2831-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="c2831-108">Cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="c2831-108">This topic:</span></span>

- <span data-ttu-id="c2831-109">Vous indique la procédure pour configurer et utiliser l’authentification par certificat pour les utilisateurs de clients dans les plans Office 365 Enterprise, Business et Education et US Government.</span><span class="sxs-lookup"><span data-stu-id="c2831-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="c2831-110">Cette fonctionnalité est disponible en version préliminaire dans les plans Office 365 China, US Government Defense et US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="c2831-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="c2831-111">Suppose que vous avez déjà une [infrastructure de clé publique (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) et [AD FS](connect/active-directory-aadconnectfed-whatis.md) configurés.</span><span class="sxs-lookup"><span data-stu-id="c2831-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="c2831-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="c2831-112">Requirements</span></span>

<span data-ttu-id="c2831-113">Pour configurer l’authentification par certificat, les éléments suivants doivent se vérifier :</span><span class="sxs-lookup"><span data-stu-id="c2831-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="c2831-114">L’authentification basée sur les certificats est uniquement prise en charge dans les environnements fédérés pour les applications de navigateur ou les clients natifs qui utilisent l’authentification moderne (ADAL).</span><span class="sxs-lookup"><span data-stu-id="c2831-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="c2831-115">La seule exception est Exchange Active Sync (EAS) pour EXO qui peut être utilisé à la fois pour les comptes fédérés et les comptes managés.</span><span class="sxs-lookup"><span data-stu-id="c2831-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="c2831-116">L’autorité de certification racine et les autorités de certification intermédiaires doivent être configurées dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2831-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="c2831-117">Chaque autorité de certification doit avoir une liste de révocation de certificat (CRL) qui peut être référencée via une URL accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="c2831-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="c2831-118">Vous devez disposer d’au moins une autorité de certification configurée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2831-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="c2831-119">Vous trouverez les étapes associées dans la section [Configurer les autorités de certification](#step-2-configure-the-certificate-authorities).</span><span class="sxs-lookup"><span data-stu-id="c2831-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="c2831-120">Pour les clients Exchange ActiveSync, le certificat client doit avoir l’adresse de messagerie routable de l’utilisateur dans Exchange Online, dans la valeur Nom du principal ou la valeur Nom RFC822 du champ Autre nom de l’objet.</span><span class="sxs-lookup"><span data-stu-id="c2831-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="c2831-121">Azure Active Directory mappe la valeur RFC822 à l’attribut Adresse proxy dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="c2831-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="c2831-122">Votre appareil client doit avoir accès à au moins une autorité de certification qui émet des certificats clients.</span><span class="sxs-lookup"><span data-stu-id="c2831-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="c2831-123">Un certificat client pour l’authentification du client doit avoir été émis pour votre client.</span><span class="sxs-lookup"><span data-stu-id="c2831-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="c2831-124">Étape 1 : Sélectionner la plateforme de votre appareil</span><span class="sxs-lookup"><span data-stu-id="c2831-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="c2831-125">Dans un premier temps, pour la plateforme d’appareil qui vous intéresse, vous devez passer en revue les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c2831-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="c2831-126">La prise en charge des applications mobiles Office</span><span class="sxs-lookup"><span data-stu-id="c2831-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="c2831-127">Les conditions requises spécifiques pour la mise en œuvre</span><span class="sxs-lookup"><span data-stu-id="c2831-127">The specific implementation requirements</span></span>  

<span data-ttu-id="c2831-128">Les informations connexes existent pour les plateformes d’appareils suivantes :</span><span class="sxs-lookup"><span data-stu-id="c2831-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="c2831-129">Android</span><span class="sxs-lookup"><span data-stu-id="c2831-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="c2831-130">iOS</span><span class="sxs-lookup"><span data-stu-id="c2831-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="c2831-131">Étape 2 : Configurer les autorités de certification</span><span class="sxs-lookup"><span data-stu-id="c2831-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="c2831-132">Pour configurer vos autorités de certification dans Azure Active Directory, pour chaque autorité de certification, vous devez télécharger les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c2831-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="c2831-133">La partie publique du certificat, au format *.cer*</span><span class="sxs-lookup"><span data-stu-id="c2831-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="c2831-134">Les URL accessibles sur Internet où résident les listes de révocation de certificat (CRL)</span><span class="sxs-lookup"><span data-stu-id="c2831-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="c2831-135">Le schéma d’une autorité de certification se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2831-135">The schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="c2831-136">Pour la configuration, vous pouvez utiliser [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) :</span><span class="sxs-lookup"><span data-stu-id="c2831-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="c2831-137">Démarrez Windows PowerShell avec les privilèges administrateur.</span><span class="sxs-lookup"><span data-stu-id="c2831-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="c2831-138">Installez le module Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2831-138">Install the Azure AD module.</span></span> <span data-ttu-id="c2831-139">Vous devez installer la version [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ou une version supérieure.</span><span class="sxs-lookup"><span data-stu-id="c2831-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="c2831-140">Comme première étape de configuration, vous devez établir une connexion avec votre client.</span><span class="sxs-lookup"><span data-stu-id="c2831-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="c2831-141">Dès qu’il existe une connexion à votre client, vous pouvez examiner, ajouter, supprimer et modifier les autorités de certification approuvées qui sont définies dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="c2831-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="c2831-142">Connecter</span><span class="sxs-lookup"><span data-stu-id="c2831-142">Connect</span></span>

<span data-ttu-id="c2831-143">Pour établir une connexion avec votre client, utilisez l’applet de commande [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) :</span><span class="sxs-lookup"><span data-stu-id="c2831-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="c2831-144">Récupération</span><span class="sxs-lookup"><span data-stu-id="c2831-144">Retrieve</span></span> 

<span data-ttu-id="c2831-145">Pour récupérer les autorités de certification approuvées qui sont définies dans votre répertoire, utilisez l’applet de commande [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="c2831-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="c2831-146">Ajouter</span><span class="sxs-lookup"><span data-stu-id="c2831-146">Add</span></span>

<span data-ttu-id="c2831-147">Pour créer une autorité de certification approuvée, utilisez l’applet de commande [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) et définissez l’attribut **crlDistributionPoint** à une valeur correcte :</span><span class="sxs-lookup"><span data-stu-id="c2831-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="c2831-148">Supprimer</span><span class="sxs-lookup"><span data-stu-id="c2831-148">Remove</span></span>

<span data-ttu-id="c2831-149">Pour supprimer une autorité de certification approuvée, utilisez l’applet de commande [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) :</span><span class="sxs-lookup"><span data-stu-id="c2831-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="c2831-150">Modifier</span><span class="sxs-lookup"><span data-stu-id="c2831-150">Modfiy</span></span>

<span data-ttu-id="c2831-151">Pour modifier une autorité de certification approuvée, utilisez l’applet de commande [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) :</span><span class="sxs-lookup"><span data-stu-id="c2831-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="c2831-152">Étape 3 : Configurer la révocation</span><span class="sxs-lookup"><span data-stu-id="c2831-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="c2831-153">Pour révoquer un certificat client, Azure Active Directory extrait la liste de révocation de certificat (CRL) à partir des URL téléchargées dans le cadre des informations sur l’autorité de certification et la met en cache.</span><span class="sxs-lookup"><span data-stu-id="c2831-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="c2831-154">L’horodateur de la dernière publication (propriété**Effective Date** ) dans la liste de révocation de certificat permet de vérifier si la CRL est toujours valide.</span><span class="sxs-lookup"><span data-stu-id="c2831-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="c2831-155">La CRL est référencée périodiquement pour révoquer l’accès à des certificats qui font partie de la liste.</span><span class="sxs-lookup"><span data-stu-id="c2831-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="c2831-156">Si une révocation plus instantanée est requise (par exemple, si un utilisateur perd un appareil), le jeton d’autorisation de l’utilisateur peut être invalidé.</span><span class="sxs-lookup"><span data-stu-id="c2831-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="c2831-157">Pour invalider le jeton d’autorisation, définissez le champ **StsRefreshTokenValidFrom** pour cet utilisateur à l’aide de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2831-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="c2831-158">Vous devez mettre à jour le champ **StsRefreshTokenValidFrom** pour chaque utilisateur pour lequel vous souhaitez révoquer l’accès.</span><span class="sxs-lookup"><span data-stu-id="c2831-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="c2831-159">Pour garantir que la révocation persiste, vous devez définir la propriété **Effective Date** de la CRL sur une date postérieure à la valeur définie par **StsRefreshTokenValidFrom** et vérifiez que le certificat en question est inclus dans la CRL.</span><span class="sxs-lookup"><span data-stu-id="c2831-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="c2831-160">Les étapes suivantes décrivent le processus de mise à jour et d’invalidation du jeton d’autorisation avec la définition du champ **StsRefreshTokenValidFrom** .</span><span class="sxs-lookup"><span data-stu-id="c2831-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="c2831-161">**Pour configurer la révocation :**</span><span class="sxs-lookup"><span data-stu-id="c2831-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="c2831-162">Connectez-vous au service MSOL avec les informations d’identification administrateur :</span><span class="sxs-lookup"><span data-stu-id="c2831-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="c2831-163">Récupérez la valeur StsRefreshTokensValidFrom actuelle pour un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c2831-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="c2831-164">Configurez une nouvelle valeur StsRefreshTokensValidFrom pour l’utilisateur. Elle doit être égale à l’horodateur actuel :</span><span class="sxs-lookup"><span data-stu-id="c2831-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="c2831-165">La date que vous définissez doit être dans le futur.</span><span class="sxs-lookup"><span data-stu-id="c2831-165">The date you set must be in the future.</span></span> <span data-ttu-id="c2831-166">Si la date n’est pas dans le futur, la propriété **StsRefreshTokensValidFrom** n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="c2831-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="c2831-167">Si la date est dans le futur, la propriété **StsRefreshTokensValidFrom** est définie sur l’heure actuelle (et non la date indiquée par la commande Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="c2831-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="c2831-168">Étape 4 : Tester votre configuration</span><span class="sxs-lookup"><span data-stu-id="c2831-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="c2831-169">Test de votre certificat</span><span class="sxs-lookup"><span data-stu-id="c2831-169">Testing your certificate</span></span>

<span data-ttu-id="c2831-170">Comme premier test de configuration, vous devez essayer de vous connecter à [Outlook Web Access](https://outlook.office365.com) ou [SharePoint Online](https://microsoft.sharepoint.com) à l’aide du **navigateur sur l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="c2831-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="c2831-171">Si votre connexion est réussie, vous savez que :</span><span class="sxs-lookup"><span data-stu-id="c2831-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="c2831-172">Le certificat utilisateur a été configuré sur votre appareil de test</span><span class="sxs-lookup"><span data-stu-id="c2831-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="c2831-173">AD FS est correctement configuré</span><span class="sxs-lookup"><span data-stu-id="c2831-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="c2831-174">Test des applications Office mobiles</span><span class="sxs-lookup"><span data-stu-id="c2831-174">Testing Office mobile applications</span></span>

<span data-ttu-id="c2831-175">**Pour tester l’authentification par certificat sur votre application Office mobile :**</span><span class="sxs-lookup"><span data-stu-id="c2831-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="c2831-176">Sur votre appareil de test, installez une application Office mobile (par exemple, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="c2831-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="c2831-177">Lancez l’application.</span><span class="sxs-lookup"><span data-stu-id="c2831-177">Launch the application.</span></span> 
4. <span data-ttu-id="c2831-178">Entrez votre nom d’utilisateur et sélectionnez le certificat utilisateur que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="c2831-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="c2831-179">Vous devez être connecté.</span><span class="sxs-lookup"><span data-stu-id="c2831-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="c2831-180">Test des applications clientes Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="c2831-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="c2831-181">Pour accéder à Exchange ActiveSync (EAS) via l’authentification par certificat, un profil EAS contenant le certificat client doit être disponible pour l’application.</span><span class="sxs-lookup"><span data-stu-id="c2831-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="c2831-182">Le profil EAS doit contenir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c2831-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="c2831-183">Le certificat utilisateur à utiliser pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="c2831-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="c2831-184">Le point de terminaison EAS (par exemple, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="c2831-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="c2831-185">Un profil EAS peut être configuré et placé sur l’appareil via l’utilisation de la gestion des appareils mobiles (MDM), comme Intune, ou en plaçant manuellement le certificat dans le profil EAS sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="c2831-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="c2831-186">Test des applications clientes EAS sur Android</span><span class="sxs-lookup"><span data-stu-id="c2831-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="c2831-187">**Pour tester l’authentification par certificat :**</span><span class="sxs-lookup"><span data-stu-id="c2831-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="c2831-188">Configurez un profil EAS dans l’application qui respecte les spécifications citées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c2831-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="c2831-189">Ouvrez l’application et vérifiez la synchronisation de la messagerie.</span><span class="sxs-lookup"><span data-stu-id="c2831-189">Open the application, and verify that mail is synchronizing.</span></span> 

