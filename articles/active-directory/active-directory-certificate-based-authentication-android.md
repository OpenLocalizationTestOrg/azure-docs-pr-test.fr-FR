---
title: Authentification par certificat Azure Active Directory sur Android | Microsoft Docs
description: "En savoir plus sur les scénarios pris en charge et la configuration requise pour la configuration de l’authentification par certificat dans les solutions avec les appareils Android"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 8005bfe821fea25539c84efdccf6c49bd5f1f8ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="4d52f-103">Authentification par certificat Azure Active Directory sur Android</span><span class="sxs-lookup"><span data-stu-id="4d52f-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="4d52f-104">L’authentification par certificat (CBA) vous permet d’être authentifié par Azure Active Directory avec un certificat client sur un appareil Windows, Android ou iOS lors de la connexion de votre compte Exchange Online à :</span><span class="sxs-lookup"><span data-stu-id="4d52f-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="4d52f-105">Des applications mobiles Office, telles que Microsoft Outlook et Microsoft Word ;</span><span class="sxs-lookup"><span data-stu-id="4d52f-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="4d52f-106">Des clients Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="4d52f-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="4d52f-107">La configuration de cette fonctionnalité élimine le besoin d’entrer un nom d’utilisateur et un mot de passe dans certaines applications de messagerie et Microsoft Office sur votre appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="4d52f-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="4d52f-108">Cette rubrique vous indique la configuration requise et les scénarios pris en charge pour la configuration de l’authentification par certificat sur un appareil iOS (Android) pour les utilisateurs des locataires des plans Office 365 Enterprise, Business, Education, US Government, Chine et Allemagne.</span><span class="sxs-lookup"><span data-stu-id="4d52f-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="4d52f-109">Cette fonctionnalité est disponible en version préliminaire dans les plans Office 365 US Government Defense et US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="4d52f-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="4d52f-110">Prise en charge des applications mobiles Office</span><span class="sxs-lookup"><span data-stu-id="4d52f-110">Office mobile applications support</span></span>
| <span data-ttu-id="4d52f-111">Applications</span><span class="sxs-lookup"><span data-stu-id="4d52f-111">Apps</span></span> | <span data-ttu-id="4d52f-112">Support</span><span class="sxs-lookup"><span data-stu-id="4d52f-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="4d52f-113">Application Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="4d52f-113">Azure Information Protection app</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4d52f-115">Microsoft Teams</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="4d52f-117">OneNote</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="4d52f-119">OneDrive</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="4d52f-121">Outlook</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-123">Applications mobiles Power BI</span><span class="sxs-lookup"><span data-stu-id="4d52f-123">Power BI mobile apps</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-125">Skype Entreprise</span><span class="sxs-lookup"><span data-stu-id="4d52f-125">Skype for Business</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="4d52f-127">Word / Excel / PowerPoint</span></span> |![Vérification][1] |
| <span data-ttu-id="4d52f-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="4d52f-129">Yammer</span></span> |![Vérification][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="4d52f-131">Conditions requises pour la mise en œuvre</span><span class="sxs-lookup"><span data-stu-id="4d52f-131">Implementation requirements</span></span>

<span data-ttu-id="4d52f-132">La version du système d’exploitation de l’appareil doit être Android 5.0 (Lollipop) ou toute version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4d52f-132">The device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="4d52f-133">Un serveur de fédération doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="4d52f-133">A federation server must be configured.</span></span>  

<span data-ttu-id="4d52f-134">Pour qu’Azure Active Directory révoque un certificat client, le jeton ADFS doit posséder les déclarations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d52f-134">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="4d52f-135">(Le numéro de série du certificat client)</span><span class="sxs-lookup"><span data-stu-id="4d52f-135">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="4d52f-136">(La chaîne de l’émetteur du certificat client)</span><span class="sxs-lookup"><span data-stu-id="4d52f-136">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="4d52f-137">Azure Active Directory ajoute ces déclarations au jeton d’actualisation si elles sont disponibles dans le jeton ADFS (ou n’importe quel autre jeton SAML).</span><span class="sxs-lookup"><span data-stu-id="4d52f-137">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="4d52f-138">Lorsque le jeton d’actualisation doit être validé, ces informations sont utilisées pour vérifier la révocation.</span><span class="sxs-lookup"><span data-stu-id="4d52f-138">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="4d52f-139">La meilleure pratique consiste à mettre à jour les pages d’erreur ADFS avec des instructions sur l’obtention d’un certificat utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4d52f-139">As a best practice, you should update the ADFS error pages with instructions on how to get a user certificate.</span></span>  
<span data-ttu-id="4d52f-140">Pour plus d’informations, consultez [Personnalisation des pages de connexion AD FS](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d52f-140">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="4d52f-141">Certaines applications Office (avec l’authentification moderne activée) envoient « *prompt=login* » à Azure AD dans leur demande.</span><span class="sxs-lookup"><span data-stu-id="4d52f-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="4d52f-142">Par défaut, Azure AD traduit cela dans la demande aux services ADFS en « *wauth=usernamepassworduri* » (demande aux services ADFS d’effectuer l’authentification U/P) et « *wfresh=0* » (demande aux services ADFS d’ignorer l’état d’authentification unique et d’effectuer une nouvelle authentification).</span><span class="sxs-lookup"><span data-stu-id="4d52f-142">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="4d52f-143">Si vous souhaitez activer l’authentification par certificat pour ces applications, vous devez modifier le comportement par défaut d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d52f-143">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="4d52f-144">Définissez simplement « *PromptLoginBehavior* » dans vos paramètres de domaine fédéré sur « *Désactivé* ».</span><span class="sxs-lookup"><span data-stu-id="4d52f-144">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="4d52f-145">Vous pouvez utiliser l’applet de commande [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) pour effectuer cette tâche :</span><span class="sxs-lookup"><span data-stu-id="4d52f-145">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="4d52f-146">Prise en charge des clients Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="4d52f-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="4d52f-147">Certaines applications Exchange ActiveSync sur Android 5.0 (Lollipop) ou version ultérieure sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="4d52f-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="4d52f-148">Pour déterminer si votre application de messagerie prend en charge cette fonctionnalité, contactez le développeur de votre application.</span><span class="sxs-lookup"><span data-stu-id="4d52f-148">To determine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4d52f-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d52f-149">Next steps</span></span>

<span data-ttu-id="4d52f-150">Si vous souhaitez configurer l’authentification par certificat dans votre environnement, consultez [Bien démarrer avec l’authentification par certificat sur Android](active-directory-certificate-based-authentication-get-started.md) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="4d52f-150">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png