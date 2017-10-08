---
title: "aaaAzure l’authentification basée sur certificat Active Directory sur Android | Documents Microsoft"
description: "En savoir plus sur les scénarios de hello pris en charge et les exigences de hello pour la configuration de l’authentification basée sur certificat dans les solutions avec les appareils Android"
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
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="60325-103">Authentification par certificat Azure Active Directory sur Android</span><span class="sxs-lookup"><span data-stu-id="60325-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="60325-104">Authentification par certificat (Services) vous permet de toobe authentifié par Azure Active Directory avec un certificat client sur un appareil Windows, Android ou iOS lors de la connexion de votre compte en ligne Exchange pour :</span><span class="sxs-lookup"><span data-stu-id="60325-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="60325-105">Des applications mobiles Office, telles que Microsoft Outlook et Microsoft Word ;</span><span class="sxs-lookup"><span data-stu-id="60325-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="60325-106">Des clients Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="60325-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="60325-107">La configuration de cette fonctionnalité évite hello besoin tooenter un nom d’utilisateur et mot de passe dans certaines applications de Microsoft Office sur votre appareil mobile et de messagerie.</span><span class="sxs-lookup"><span data-stu-id="60325-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="60325-108">Cette rubrique vous fournit des exigences de hello et les scénarios de hello pris en charge pour la configuration des services sur un appareil iOS(Android) pour les utilisateurs de clients dans Office 365 entreprise, entreprise, éducation, du gouvernement, Chine, et plans de l’Allemagne.</span><span class="sxs-lookup"><span data-stu-id="60325-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="60325-109">Cette fonctionnalité est disponible en version préliminaire dans les plans Office 365 US Government Defense et US Government Federal.</span><span class="sxs-lookup"><span data-stu-id="60325-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="60325-110">Prise en charge des applications mobiles Office</span><span class="sxs-lookup"><span data-stu-id="60325-110">Office mobile applications support</span></span>
| <span data-ttu-id="60325-111">Applications</span><span class="sxs-lookup"><span data-stu-id="60325-111">Apps</span></span> | <span data-ttu-id="60325-112">Support</span><span class="sxs-lookup"><span data-stu-id="60325-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="60325-113">Application Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="60325-113">Azure Information Protection app</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="60325-115">Microsoft Teams</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="60325-117">OneNote</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="60325-119">OneDrive</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="60325-121">Outlook</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-123">Applications mobiles Power BI</span><span class="sxs-lookup"><span data-stu-id="60325-123">Power BI mobile apps</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-125">Skype Entreprise</span><span class="sxs-lookup"><span data-stu-id="60325-125">Skype for Business</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="60325-127">Word / Excel / PowerPoint</span></span> |![Vérification][1] |
| <span data-ttu-id="60325-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="60325-129">Yammer</span></span> |![Vérification][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="60325-131">Conditions requises pour la mise en œuvre</span><span class="sxs-lookup"><span data-stu-id="60325-131">Implementation requirements</span></span>

<span data-ttu-id="60325-132">Hello version du système d’exploitation de périphérique doit être Android 5.0 (Lollipop) et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="60325-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="60325-133">Un serveur de fédération doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="60325-133">A federation server must be configured.</span></span>  

<span data-ttu-id="60325-134">Pour Azure Active Directory toorevoke un certificat client, jeton d’ADFS hello doit avoir hello suivant revendications :</span><span class="sxs-lookup"><span data-stu-id="60325-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="60325-135">(hello le numéro de série du certificat de client hello)</span><span class="sxs-lookup"><span data-stu-id="60325-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="60325-136">(chaîne hello pour émetteur hello du certificat de client hello)</span><span class="sxs-lookup"><span data-stu-id="60325-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="60325-137">Azure Active Directory ajoute ces revendications toohello actualiser le jeton si elles sont disponibles dans le jeton d’ADFS hello (ou tout autre jeton SAML).</span><span class="sxs-lookup"><span data-stu-id="60325-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="60325-138">Lorsque le jeton d’actualisation hello doit toobe validé, ces informations sont utilisées toocheck hello révocation.</span><span class="sxs-lookup"><span data-stu-id="60325-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="60325-139">Comme meilleure pratique, mettez à jour les pages d’erreurs hello ADFS avec des instructions sur la façon de tooget un certificat utilisateur.</span><span class="sxs-lookup"><span data-stu-id="60325-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="60325-140">Pour plus d’informations, consultez [personnalisation des Pages de hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="60325-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="60325-141">Certaines applications Office (avec l’authentification moderne activée) envoyer '*prompt = connexion*' tooAzure AD dans sa demande.</span><span class="sxs-lookup"><span data-stu-id="60325-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="60325-142">Par défaut, Azure AD convertit ce dans hello demande tooADFS trop '*wauth = usernamepassworduri*» (demande d’authentification ADFS toodo U/P) et «*wfresh = 0*» (demande d’état de l’authentification AD FS tooignore et effectuez une nouvelle authentification) .</span><span class="sxs-lookup"><span data-stu-id="60325-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="60325-143">Si vous souhaitez que l’authentification basée sur certificat tooenable pour ces applications, vous devez toomodify hello Azure AD par défaut.</span><span class="sxs-lookup"><span data-stu-id="60325-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="60325-144">Simplement ensemble hello '*PromptLoginBehavior*' dans les paramètres de votre domaine fédéré trop '*désactivé*'.</span><span class="sxs-lookup"><span data-stu-id="60325-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="60325-145">Vous pouvez utiliser hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform de l’applet de commande cette tâche :</span><span class="sxs-lookup"><span data-stu-id="60325-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="60325-146">Prise en charge des clients Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="60325-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="60325-147">Certaines applications Exchange ActiveSync sur Android 5.0 (Lollipop) ou version ultérieure sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="60325-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="60325-148">toodetermine si votre application de messagerie ne prend pas en charge cette fonctionnalité, contactez le développeur de votre application.</span><span class="sxs-lookup"><span data-stu-id="60325-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="60325-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60325-149">Next steps</span></span>

<span data-ttu-id="60325-150">Si vous souhaitez que l’authentification par certificat tooconfigure dans votre environnement, consultez [prise en main l’authentification basée sur le certificat sur Android](active-directory-certificate-based-authentication-get-started.md) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="60325-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
