---
title: "Sécurité des mots de passe à niveaux dans Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="ab3f1-103">Une approche à plusieurs niveaux de la sécurité des mots de passe dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab3f1-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="ab3f1-104">Cet article décrit les meilleures pratiques que vous pouvez suivre en tant qu’utilisateur ou administrateur pour protéger vos comptes Azure Active Directory (Azure AD) ou votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="ab3f1-105">Les administrateurs Azure AD peuvent réinitialiser les mots de passe utilisateur à l’aide des instructions de l’article [Réinitialiser le mot de passe d’un utilisateur dans Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ab3f1-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="ab3f1-106">Les utilisateurs peuvent réinitialiser leur propre mot de passe à l’aide des instructions de l’article [J’ai oublié mon mot de passe Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="ab3f1-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="ab3f1-107">Conditions requises pour les mots de passe</span><span class="sxs-lookup"><span data-stu-id="ab3f1-107">Password requirements</span></span>

<span data-ttu-id="ab3f1-108">Azure AD intègre les approches courantes suivantes à la sécurisation des mots de passe :</span><span class="sxs-lookup"><span data-stu-id="ab3f1-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="ab3f1-109">Exigences en termes de longueur du mot de passe</span><span class="sxs-lookup"><span data-stu-id="ab3f1-109">Password length requirements</span></span>
* <span data-ttu-id="ab3f1-110">Exigences en termes de « complexité » du mot de passe</span><span class="sxs-lookup"><span data-stu-id="ab3f1-110">Password complexity requirements</span></span>
* <span data-ttu-id="ab3f1-111">Expiration du mot de passe périodique et régulière</span><span class="sxs-lookup"><span data-stu-id="ab3f1-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="ab3f1-112">Pour plus d’informations sur la réinitialisation de mot de passe dans Azure Active Directory, consultez la rubrique [Réinitialisation de mot de passe en libre service pour Azure Ad pour les professionnels en informatique](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="ab3f1-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="ab3f1-113">Protections de mot de passe Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab3f1-113">Azure AD password protections</span></span>

<span data-ttu-id="ab3f1-114">Azure AD et le système de comptes Microsoft utilisent des approches validées par le secteur pour assurer la protection sécurisée des mots de passe administrateur et utilisateur, dont :</span><span class="sxs-lookup"><span data-stu-id="ab3f1-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="ab3f1-115">Mots de passe interdits dynamiquement</span><span class="sxs-lookup"><span data-stu-id="ab3f1-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="ab3f1-116">Verrouillage de mot de passe intelligent</span><span class="sxs-lookup"><span data-stu-id="ab3f1-116">Smart Password Lockout</span></span>

<span data-ttu-id="ab3f1-117">Pour plus d’informations sur la gestion des mots de passe en fonction de la recherche en cours, consultez le livre blanc [Password Guidance](http://aka.ms/passwordguidance) (Conseils en matière de mots de passe).</span><span class="sxs-lookup"><span data-stu-id="ab3f1-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="ab3f1-118">Mots de passe interdits dynamiquement</span><span class="sxs-lookup"><span data-stu-id="ab3f1-118">Dynamically banned passwords</span></span>

<span data-ttu-id="ab3f1-119">Azure AD et les comptes Microsoft assurent la protection des mots de passe en interdisant dynamiquement tous les mots de passe utilisés couramment.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="ab3f1-120">L’équipe Azure AD Identity Protection analyse régulièrement les listes de mots de passe interdits, empêchant ainsi les utilisateurs de choisir des mots de passe utilisés couramment.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="ab3f1-121">Ce service est disponible pour les clients Azure AD et du service de comptes Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="ab3f1-122">Lorsque vous créez des mots de passe, il est important que les administrateurs encouragent les utilisateurs à choisir des phrases de mot de passe qui incluent une combinaison unique de lettres, de chiffres et de caractères ou de mots.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="ab3f1-123">Cette approche contribue à rendre les mots de passe utilisateur quasiment impossibles à compromettre, mais plus faciles à mémoriser pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="ab3f1-124">Violations de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ab3f1-124">Password breaches</span></span>

<span data-ttu-id="ab3f1-125">Microsoft cherche toujours à garder une longueur d’avance sur les cybercriminels.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="ab3f1-126">L’équipe Azure AD Identity Protection analyse en permanence les mots de passe couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="ab3f1-127">Les cybercriminels utilisent également des stratégies similaires pour créer leurs attaques ; ils peuvent, par exemple, créer une [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) pour craquer les codes de hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="ab3f1-128">Microsoft analyse sans cesse les [violations de données](https://www.privacyrights.org/data-breaches) pour maintenir à jour une liste des mots de passe interdits dynamiquement, qui garantit que les mots de passe vulnérables sont interdits avant de devenir une véritable menace pour les clients Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="ab3f1-129">Pour plus d’informations sur nos travaux en matière de sécurité actuels, consultez le [Rapport de renseignement sur la sécurité (SIR) de Microsoft](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab3f1-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="ab3f1-130">Verrouillage de mot de passe intelligent</span><span class="sxs-lookup"><span data-stu-id="ab3f1-130">Smart Password Lockout</span></span>

<span data-ttu-id="ab3f1-131">Quand Azure AD détecte qu’un potentiel cybercriminel tente de pirater un mot de passe utilisateur, nous verrouillons le compte utilisateur avec le verrouillage de mot de passe intelligent.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="ab3f1-132">Azure AD est conçu pour déterminer les risques associés à des sessions de connexion spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="ab3f1-133">Ensuite, à l’aide des données de sécurité les plus récentes, nous appliquons une sémantique de verrouillage pour arrêter les cybermenaces.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="ab3f1-134">Si l’accès d’un utilisateur à son compte Azure AD est verrouillé, l’écran sera semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ab3f1-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Accès verrouillé au compte Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="ab3f1-136">Pour les autres comptes Microsoft, l’utilisateur verra ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ab3f1-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Accès verrouillé au compte Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="ab3f1-138">Pour plus d’informations sur la réinitialisation de mot de passe dans Azure Active Directory, consultez la rubrique [Réinitialisation de mot de passe en libre service pour Azure Ad pour les professionnels en informatique](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="ab3f1-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="ab3f1-139">Si vous êtes administrateur Azure AD, vous souhaiterez peut-être utiliser [Windows Hello](https://www.microsoft.com/windows/windows-hello) pour éviter que vos utilisateurs créent des mots de passe classiques.</span><span class="sxs-lookup"><span data-stu-id="ab3f1-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="ab3f1-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab3f1-140">Next steps</span></span>

* [<span data-ttu-id="ab3f1-141">Comment mettre à jour votre mot de passe</span><span class="sxs-lookup"><span data-stu-id="ab3f1-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="ab3f1-142">Principes de base de la gestion des identités Azure</span><span class="sxs-lookup"><span data-stu-id="ab3f1-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="ab3f1-143">Rapport sur l’activité de réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="ab3f1-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


