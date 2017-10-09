---
title: "vérification de l’étape d’aaaTwo et AD FS - l’authentification Multifacteur Azure | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget main d’Azure MFA et AD FS."
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
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="316b3-103">Prise en main d’Azure Multi-Factor Authentication et des services de fédération Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="316b3-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="316b3-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="316b3-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="316b3-105">Si votre organisation a fédéré votre Active Directory local avec Azure Active Directory à l’aide d’AD FS, vous disposez de deux options pour l’utilisation d’Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="316b3-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="316b3-106">Sécuriser les ressources de cloud à l’aide de l’authentification multifacteur Azure ou des services de fédération Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="316b3-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="316b3-107">Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="316b3-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="316b3-108">Hello tableau suivant résume l’expérience de vérification hello entre la sécurisation des ressources avec Azure multi-Factor Authentication et AD FS</span><span class="sxs-lookup"><span data-stu-id="316b3-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="316b3-109">Processus de vérification : applications basées sur le navigateur</span><span class="sxs-lookup"><span data-stu-id="316b3-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="316b3-110">Processus de vérification : applications hors navigateur</span><span class="sxs-lookup"><span data-stu-id="316b3-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="316b3-111">Sécurisation des ressources Azure AD à l'aide d’Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="316b3-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="316b3-112">première étape de vérification Hello est effectuée en local avec AD FS.</span><span class="sxs-lookup"><span data-stu-id="316b3-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="316b3-113">deuxième étape de Hello est une méthode par téléphone effectuée à l’aide de l’authentification cloud.</span><span class="sxs-lookup"><span data-stu-id="316b3-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="316b3-114">Sécurisation des ressources Azure AD à l'aide des services ADFS</span><span class="sxs-lookup"><span data-stu-id="316b3-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="316b3-115">première étape de vérification Hello est effectuée en local avec AD FS.</span><span class="sxs-lookup"><span data-stu-id="316b3-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="316b3-116">Hello deuxième étape est effectué localement en répondant à hello revendication.</span><span class="sxs-lookup"><span data-stu-id="316b3-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="316b3-117">Mises en garde relatives aux mots de passe d'application pour les utilisateurs fédérés :</span><span class="sxs-lookup"><span data-stu-id="316b3-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="316b3-118">Les mots de passe d’applications sont vérifiés à l’aide de l’authentification cloud et contournent donc la fédération.</span><span class="sxs-lookup"><span data-stu-id="316b3-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="316b3-119">La fédération n’est utilisée activement que lorsque vous configurez un mot de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="316b3-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="316b3-120">Les paramètres de contrôle d’accès client locaux ne sont pas honorés par les mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="316b3-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="316b3-121">Vous perdez la fonctionnalité de journalisation-authentification locale pour les mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="316b3-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="316b3-122">La désactivation/suppression de compte peut prendre des heures de toothree pour la synchronisation d’annuaire, retardant la désactivation/suppression de mots de passe d’application dans l’identité de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="316b3-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="316b3-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="316b3-123">Next steps</span></span>
<span data-ttu-id="316b3-124">Pour plus d’informations sur la configuration de l’authentification multifacteur Azure ou de hello serveur Azure multi-Factor Authentication avec AD FS, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="316b3-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="316b3-125">Sécuriser les ressources cloud à l’aide d’Azure Multi-Factor Authentication et AD FS</span><span class="sxs-lookup"><span data-stu-id="316b3-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="316b3-126">Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="316b3-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="316b3-127">Sécuriser les ressources de cloud et locales à l'aide du serveur Azure Multi-Factor Authentication avec AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="316b3-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
