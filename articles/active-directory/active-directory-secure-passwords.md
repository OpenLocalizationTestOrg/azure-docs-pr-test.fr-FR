---
title: "aaaAzure AD à plusieurs niveaux de sécurité de mot de passe | Documents Microsoft"
description: "Explique comment Azure AD impose des mots de passe forts et protège les mots de passe des utilisateurs contre les cybercriminels,"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="da919-103">Une approche multiniveau tooAzure AD mot de passe de sécurité</span><span class="sxs-lookup"><span data-stu-id="da919-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="da919-104">Cet article décrit quelques meilleures pratiques que vous pouvez suivre en tant qu’utilisateur ou un administrateur tooprotect des Account Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da919-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="da919-105">Azure AD les administrateurs peuvent réinitialiser les mots de passe utilisateur à l’aide des instructions de hello dans l’article de hello [hello réinitialisation mot de passe pour un utilisateur dans Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="da919-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="da919-106">Les utilisateurs peuvent réinitialiser leur mot de passe à l’aide des instructions de hello dans l’article de hello [aide j’ai oublié mon mot de passe Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="da919-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="da919-107">Conditions requises pour les mots de passe</span><span class="sxs-lookup"><span data-stu-id="da919-107">Password requirements</span></span>

<span data-ttu-id="da919-108">Azure AD incorpore hello suivant des mots de passe approches toosecuring communs :</span><span class="sxs-lookup"><span data-stu-id="da919-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="da919-109">Exigences en termes de longueur du mot de passe</span><span class="sxs-lookup"><span data-stu-id="da919-109">Password length requirements</span></span>
* <span data-ttu-id="da919-110">Exigences en termes de « complexité » du mot de passe</span><span class="sxs-lookup"><span data-stu-id="da919-110">Password complexity requirements</span></span>
* <span data-ttu-id="da919-111">Expiration du mot de passe périodique et régulière</span><span class="sxs-lookup"><span data-stu-id="da919-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="da919-112">Pour plus d’informations sur le mot de passe réinitialisé dans Azure Active Directory, consultez la rubrique de hello [AD Azure mot de passe libre-service réinitialiser pour hello professionnel de l’informatique](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="da919-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="da919-113">Protections de mot de passe Azure AD</span><span class="sxs-lookup"><span data-stu-id="da919-113">Azure AD password protections</span></span>

<span data-ttu-id="da919-114">Azure AD et hello système de comptes Microsoft utiliser éprouvées approches tooensure sécurisée la protection des mots de passe utilisateur et administrateur, notamment :</span><span class="sxs-lookup"><span data-stu-id="da919-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="da919-115">Mots de passe interdits dynamiquement</span><span class="sxs-lookup"><span data-stu-id="da919-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="da919-116">Verrouillage de mot de passe intelligent</span><span class="sxs-lookup"><span data-stu-id="da919-116">Smart Password Lockout</span></span>

<span data-ttu-id="da919-117">Pour plus d’informations sur la gestion de mot de passe en fonction de recherche actuelle, consultez le livre blanc de hello [des conseils de mot de passe](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="da919-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="da919-118">Mots de passe interdits dynamiquement</span><span class="sxs-lookup"><span data-stu-id="da919-118">Dynamically banned passwords</span></span>

<span data-ttu-id="da919-119">Azure AD et les comptes Microsoft assurent la protection des mots de passe en interdisant dynamiquement tous les mots de passe utilisés couramment.</span><span class="sxs-lookup"><span data-stu-id="da919-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="da919-120">équipe de Protection d’identité ID Azure Hello analyse régulièrement des listes de mot de passe interdit, empêchant les utilisateurs de sélectionner des mots de passe couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="da919-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="da919-121">Ce service est disponible tooAzure AD et les clients du Service de compte Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="da919-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="da919-122">Lorsque vous créez des mots de passe, il est important pour les administrateurs tooencourage utilisateurs toochoose mot de passe des expressions qui incluent une combinaison unique de lettres, des chiffres, des caractères ou des mots.</span><span class="sxs-lookup"><span data-stu-id="da919-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="da919-123">Cette approche permet des mots de passe utilisateur toomake toobe presque impossible compromis, mais il est plus facile pour les utilisateurs tooremember.</span><span class="sxs-lookup"><span data-stu-id="da919-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="da919-124">Violations de mot de passe</span><span class="sxs-lookup"><span data-stu-id="da919-124">Password breaches</span></span>

<span data-ttu-id="da919-125">Microsoft s’emploie toujours toostay une étape avant cybercrime.</span><span class="sxs-lookup"><span data-stu-id="da919-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="da919-126">équipe de Azure AD Identity Protection Hello analyse en permanence les mots de passe qui sont couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="da919-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="da919-127">Cybercrime également utiliser similaire stratégies tooinform leurs attaques, telles que la génération un [table d’arc-en-ciel](https://en.wikipedia.org/wiki/Rainbow_table) pour le décodage des hachages de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="da919-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="da919-128">Microsoft analyse en permanence [violations de données](https://www.privacyrights.org/data-breaches) toomaintain une liste de mises à jour dynamiquement interdit mot de passe, ce qui garantit que les mots de passe vulnérables sont interdites avant qu’ils deviennent une véritable menace tooAzure AD clients.</span><span class="sxs-lookup"><span data-stu-id="da919-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="da919-129">Pour plus d’informations sur nos efforts de sécurité actuelle, consultez hello [rapport de sécurité Microsoft](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="da919-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="da919-130">Verrouillage de mot de passe intelligent</span><span class="sxs-lookup"><span data-stu-id="da919-130">Smart Password Lockout</span></span>

<span data-ttu-id="da919-131">Lorsque Azure AD détecte un potentiel toohack lors de la tentative de cyber pénales dans un mot de passe, nous verrouiller le compte d’utilisateur de hello avec Active le verrouillage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="da919-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="da919-132">Azure AD est conçu risque de hello toodetermine associé aux sessions de connexion spécifique.</span><span class="sxs-lookup"><span data-stu-id="da919-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="da919-133">Ensuite, à l’aide de données de sécurité plus récentes de hello, nous appliquons toostop les menaces de verrouillage sémantique.</span><span class="sxs-lookup"><span data-stu-id="da919-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="da919-134">Si un utilisateur est verrouillé en dehors d’Azure AD, leur écran ressemble toohello similaire qui suit :</span><span class="sxs-lookup"><span data-stu-id="da919-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Accès verrouillé au compte Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="da919-136">Pour les autres comptes Microsoft, leur écran ressemble toohello similaire qui suit :</span><span class="sxs-lookup"><span data-stu-id="da919-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Accès verrouillé au compte Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="da919-138">Pour plus d’informations sur le mot de passe réinitialisé dans Azure Active Directory, consultez la rubrique de hello [AD Azure mot de passe libre-service réinitialiser pour hello professionnel de l’informatique](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="da919-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="da919-139">Si vous êtes un administrateur Azure AD, vous souhaiterez peut-être toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid dont vos utilisateurs créer des mots de passe traditionnels complètement.</span><span class="sxs-lookup"><span data-stu-id="da919-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="da919-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da919-140">Next steps</span></span>

* [<span data-ttu-id="da919-141">Comment tooupdate votre mot de passe</span><span class="sxs-lookup"><span data-stu-id="da919-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="da919-142">Notions de base Hello de gestion des identités de Azure</span><span class="sxs-lookup"><span data-stu-id="da919-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="da919-143">Rapport sur l’activité de réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="da919-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


