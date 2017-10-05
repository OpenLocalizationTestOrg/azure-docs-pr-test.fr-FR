---
title: "Vérification en deux étapes et AD FS : Azure MFA | Microsoft Docs"
description: "Ceci est la page d'Azure Multi-Factor Authentication qui explique la prise en main d’Azure MFA et des services AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="da1cf-103">Prise en main d’Azure Multi-Factor Authentication et des services de fédération Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="da1cf-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="da1cf-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="da1cf-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="da1cf-105">Si votre organisation a fédéré votre Active Directory local avec Azure Active Directory à l’aide d’AD FS, vous disposez de deux options pour l’utilisation d’Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="da1cf-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="da1cf-106">Sécuriser les ressources de cloud à l’aide de l’authentification multifacteur Azure ou des services de fédération Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="da1cf-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="da1cf-107">Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="da1cf-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="da1cf-108">Le tableau suivant résume le processus de vérification avec la sécurisation des ressources à l’aide d’Azure Multi-Factor Authentication et AD FS</span><span class="sxs-lookup"><span data-stu-id="da1cf-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="da1cf-109">Processus de vérification : applications basées sur le navigateur</span><span class="sxs-lookup"><span data-stu-id="da1cf-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="da1cf-110">Processus de vérification : applications hors navigateur</span><span class="sxs-lookup"><span data-stu-id="da1cf-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="da1cf-111">Sécurisation des ressources Azure AD à l'aide d’Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="da1cf-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="da1cf-112">La première étape de vérification est effectuée en local à l’aide d’AD FS.</span><span class="sxs-lookup"><span data-stu-id="da1cf-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="da1cf-113">La seconde étape est une méthode par téléphone effectuée à l’aide de l’authentification cloud.</span><span class="sxs-lookup"><span data-stu-id="da1cf-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="da1cf-114">Sécurisation des ressources Azure AD à l'aide des services ADFS</span><span class="sxs-lookup"><span data-stu-id="da1cf-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="da1cf-115">La première étape de vérification est effectuée en local à l’aide d’AD FS.</span><span class="sxs-lookup"><span data-stu-id="da1cf-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="da1cf-116">La seconde étape est effectuée localement en répondant à la demande.</span><span class="sxs-lookup"><span data-stu-id="da1cf-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="da1cf-117">Mises en garde relatives aux mots de passe d'application pour les utilisateurs fédérés :</span><span class="sxs-lookup"><span data-stu-id="da1cf-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="da1cf-118">Les mots de passe d’applications sont vérifiés à l’aide de l’authentification cloud et contournent donc la fédération.</span><span class="sxs-lookup"><span data-stu-id="da1cf-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="da1cf-119">La fédération n’est utilisée activement que lorsque vous configurez un mot de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="da1cf-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="da1cf-120">Les paramètres de contrôle d’accès client locaux ne sont pas honorés par les mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="da1cf-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="da1cf-121">Vous perdez la fonctionnalité de journalisation-authentification locale pour les mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="da1cf-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="da1cf-122">La désactivation/suppression de compte peut mettre jusqu’à 3 heures pour synchroniser les répertoires, ce qui peut retarder la désactivation/suppression des mots de passe d’application dans l’identité de cloud.</span><span class="sxs-lookup"><span data-stu-id="da1cf-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da1cf-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da1cf-123">Next steps</span></span>
<span data-ttu-id="da1cf-124">Pour plus d’informations sur la configuration d’Azure Multi-Factor Authentication ou du serveur Azure Multi-Factor Authentication avec AD FS, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="da1cf-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="da1cf-125">Sécuriser les ressources cloud à l’aide d’Azure Multi-Factor Authentication et AD FS</span><span class="sxs-lookup"><span data-stu-id="da1cf-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="da1cf-126">Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="da1cf-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="da1cf-127">Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="da1cf-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
