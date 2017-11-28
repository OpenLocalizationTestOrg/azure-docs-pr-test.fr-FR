---
title: "aaaMicrosoft États d’utilisateur Azure multi-Factor Authentication"
description: "En savoir plus sur l’état utilisateur dans Azure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a><span data-ttu-id="86209-103">La vérification en deux étapes de toorequire pour un utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="86209-103">How toorequire two-step verification for a user or group</span></span>

<span data-ttu-id="86209-104">Il existe deux approches pour exiger une vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="86209-104">There are two approaches for requiring two-step verification.</span></span> <span data-ttu-id="86209-105">Hello première option est tooenable chaque utilisateur pour Azure multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="86209-105">hello first option is tooenable each individual user for Azure Multi-Factor Authentication (MFA).</span></span> <span data-ttu-id="86209-106">Lorsque les utilisateurs sont activées individuellement, ils effectuent toujours la vérification en deux étapes (à quelques exceptions près, comme lorsqu’ils se connectent à partir d’adresses IP autorisées si hello mémorisés fonctionnalité de périphériques est mis sous tension).</span><span class="sxs-lookup"><span data-stu-id="86209-106">When users are enabled individually, they always perform two-step verification (with some exceptions, like when they sign in from trusted IP addresses or if hello remembered devices feature is turned on).</span></span> <span data-ttu-id="86209-107">deuxième option de Hello est tooset une stratégie d’accès conditionnel qui requiert une vérification en deux étapes sous certaines conditions.</span><span class="sxs-lookup"><span data-stu-id="86209-107">hello second option is tooset up a conditional access policy that requires two-step verification under certain conditions.</span></span>

>[!TIP] 
><span data-ttu-id="86209-108">Choisissez une de ces méthodes toorequire en deux étapes la vérification, pas les deux.</span><span class="sxs-lookup"><span data-stu-id="86209-108">Choose one of these methods toorequire two-step verification, not both.</span></span> <span data-ttu-id="86209-109">L’activation d’un utilisateur pour l’authentification multifacteur Azure remplace toutes les stratégies d’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="86209-109">Enabling a user for Azure MFA overrides any conditional access policies.</span></span>

## <a name="which-option-is-right-for-you"></a><span data-ttu-id="86209-110">Choisir l’option qui vous convient</span><span class="sxs-lookup"><span data-stu-id="86209-110">Which option is right for you</span></span>

<span data-ttu-id="86209-111">**L’activation de l’authentification Multifacteur Azure en modifiant des États utilisateur** est l’approche traditionnelle de hello pour exiger une vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="86209-111">**Enabling Azure MFA by changing user states** is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="86209-112">Elle fonctionne pour les deux Azure MFA dans le cloud de hello et le serveur Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="86209-112">It works for both Azure MFA in hello cloud and Azure MFA Server.</span></span> <span data-ttu-id="86209-113">Tous les utilisateurs de hello que vous activez ont hello même expérience, qui est une vérification en deux étapes tooperform chaque fois qu’ils se connectent.</span><span class="sxs-lookup"><span data-stu-id="86209-113">All hello users that you enable have hello same experience, which is tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="86209-114">L’activation d’un utilisateur remplace toutes les stratégies d’accès conditionnel appliquées à cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86209-114">Enabling a user overrides any conditional access policies that may affect that user.</span></span> 

<span data-ttu-id="86209-115">**L’activation de l’authentification multifacteur Azure avec une stratégie d’accès conditionnel** est une approche plus souple pour exiger une vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="86209-115">**Enabling Azure MFA with a conditional access policy** is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="86209-116">Il fonctionne toutefois, pour l’authentification Multifacteur Azure dans le cloud de hello, et l’accès conditionnel est un [payé la fonctionnalité d’Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="86209-116">It only work for Azure MFA in hello cloud, though, and conditional access is a [paid feature of Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span> <span data-ttu-id="86209-117">Vous pouvez créer des stratégies d’accès conditionnel qui s’appliquent toogroups, ainsi que des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="86209-117">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="86209-118">Vous pouvez appliquer davantage de restrictions aux groupes à haut risque par rapport aux groupes à faible risque, ou exiger la vérification en deux étapes uniquement pour les applications cloud à haut risque tout en ignorant celles à faible risque.</span><span class="sxs-lookup"><span data-stu-id="86209-118">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> 

<span data-ttu-id="86209-119">Ces deux options invite tooregister utilisateurs pourquoi de l’authentification multifacteur Azure première fois qu’ils se connectent après que les spécifications hello allumé.</span><span class="sxs-lookup"><span data-stu-id="86209-119">Both of these options prompt users tooregister for Azure Multi-Factor Authentication hello first time that they sign in after hello requirements turn on.</span></span> <span data-ttu-id="86209-120">Les deux options fonctionnent également avec hello configurable [paramètres Azure multi-Factor Authentication](multi-factor-authentication-whats-next.md)</span><span class="sxs-lookup"><span data-stu-id="86209-120">Both options also work with hello configurable [Azure Multi-Factor Authentication settings](multi-factor-authentication-whats-next.md)</span></span>

## <a name="enable-azure-mfa-by-changing-user-status"></a><span data-ttu-id="86209-121">Activer Azure MFA en modifiant l’état de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="86209-121">Enable Azure MFA by changing user status</span></span>

<span data-ttu-id="86209-122">Comptes d’utilisateur dans Azure multi-Factor Authentication ont hello suivant trois états distincts :</span><span class="sxs-lookup"><span data-stu-id="86209-122">User accounts in Azure Multi-Factor Authentication have hello following three distinct states:</span></span>

| <span data-ttu-id="86209-123">État</span><span class="sxs-lookup"><span data-stu-id="86209-123">Status</span></span> | <span data-ttu-id="86209-124">Description</span><span class="sxs-lookup"><span data-stu-id="86209-124">Description</span></span> | <span data-ttu-id="86209-125">Applications affectées (autres que des navigateurs)</span><span class="sxs-lookup"><span data-stu-id="86209-125">Non-browser apps affected</span></span> |
|:---:|:---:|:---:|
| <span data-ttu-id="86209-126">Désactivé</span><span class="sxs-lookup"><span data-stu-id="86209-126">Disabled</span></span> |<span data-ttu-id="86209-127">état par défaut de Hello pour un nouvel utilisateur n'inscrit pas Azure multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="86209-127">hello default state for a new user not enrolled Azure Multi-Factor Authentication (MFA).</span></span> |<span data-ttu-id="86209-128">Non</span><span class="sxs-lookup"><span data-stu-id="86209-128">No</span></span> |
| <span data-ttu-id="86209-129">Activé</span><span class="sxs-lookup"><span data-stu-id="86209-129">Enabled</span></span> |<span data-ttu-id="86209-130">utilisateur de Hello a été inscrit dans Azure MFA, mais n’a pas été inscrit.</span><span class="sxs-lookup"><span data-stu-id="86209-130">hello user has been enrolled in Azure MFA, but has not registered.</span></span> <span data-ttu-id="86209-131">Elles seront demandées tooregister hello leur prochaine dans que connexion.</span><span class="sxs-lookup"><span data-stu-id="86209-131">They will be prompted tooregister hello next time they sign in.</span></span> |<span data-ttu-id="86209-132">Non.</span><span class="sxs-lookup"><span data-stu-id="86209-132">No.</span></span>  <span data-ttu-id="86209-133">Ils continuent toowork jusqu'à ce que le processus d’inscription de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="86209-133">They continue toowork until hello registration process is completed.</span></span> |
| <span data-ttu-id="86209-134">Appliquée</span><span class="sxs-lookup"><span data-stu-id="86209-134">Enforced</span></span> |<span data-ttu-id="86209-135">utilisateur de Hello a été inscrit et terminée le processus d’inscription de hello pour Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="86209-135">hello user has been enrolled and has completed hello registration process for Azure MFA.</span></span> |<span data-ttu-id="86209-136">Oui.</span><span class="sxs-lookup"><span data-stu-id="86209-136">Yes.</span></span>  <span data-ttu-id="86209-137">Les applications requièrent des mots de passe d'application.</span><span class="sxs-lookup"><span data-stu-id="86209-137">Apps require app passwords.</span></span> |

<span data-ttu-id="86209-138">État de l’utilisateur reflète si un administrateur a les inscrit dans Azure MFA, et si elles s’est terminée de processus d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="86209-138">A user's state reflects whether an admin has enrolled them in Azure MFA, and whether they completed hello registration process.</span></span>

<span data-ttu-id="86209-139">Tous les utilisateurs commencent avec l’état *désactivé*.</span><span class="sxs-lookup"><span data-stu-id="86209-139">All users start out *disabled*.</span></span> <span data-ttu-id="86209-140">Lorsque vous inscrivez des utilisateurs dans l’authentification multifacteur Azure, leur état devient *activé*.</span><span class="sxs-lookup"><span data-stu-id="86209-140">When you enroll users in Azure MFA, their state changes *enabled*.</span></span> <span data-ttu-id="86209-141">Lorsque les utilisateurs activés se connectent et terminer le processus d’inscription de hello, leur état change également*appliquée*.</span><span class="sxs-lookup"><span data-stu-id="86209-141">When enabled users sign in and complete hello registration process, their state changes too*enforced*.</span></span>  

### <a name="view-hello-status-for-a-user"></a><span data-ttu-id="86209-142">Afficher l’état hello pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="86209-142">View hello status for a user</span></span>

<span data-ttu-id="86209-143">Hello utilisation suivant étapes tooaccess hello page où vous pouvez afficher et gérer des États utilisateur :</span><span class="sxs-lookup"><span data-stu-id="86209-143">Use hello following steps tooaccess hello page where you can view and manage user states:</span></span>

1. <span data-ttu-id="86209-144">Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="86209-144">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="86209-145">Accédez trop**Azure Active Directory** > **utilisateurs et groupes** > **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="86209-145">Go too**Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="86209-146">Sélectionnez **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="86209-146">Select **Multi-Factor Authentication**.</span></span>
   <span data-ttu-id="86209-147">![Sélectionnez Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span><span class="sxs-lookup"><span data-stu-id="86209-147">![Select Multi-Factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)</span></span>
4. <span data-ttu-id="86209-148">Une nouvelle page qui affiche les États utilisateur hello, s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="86209-148">A new page, which displays hello user states, opens.</span></span>
   <span data-ttu-id="86209-149">![État utilisateur pour l’authentification multifacteur - capture d’écran](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span><span class="sxs-lookup"><span data-stu-id="86209-149">![multi-factor authentication user status - screenshot](./media/multi-factor-authentication-get-started-user-states/userstate1.png)</span></span>

### <a name="change-hello-status-for-a-user"></a><span data-ttu-id="86209-150">Modifier l’état hello pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="86209-150">Change hello status for a user</span></span>

1. <span data-ttu-id="86209-151">Utilisez hello précédant la page users d’étapes tooget toohello l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="86209-151">Use hello preceding steps tooget toohello multi-factor authentication users page.</span></span>
2. <span data-ttu-id="86209-152">Rechercher un utilisateur hello que vous souhaitez tooenable pour Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="86209-152">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="86209-153">Vous devrez peut-être toochange hello vue haut hello.</span><span class="sxs-lookup"><span data-stu-id="86209-153">You may need toochange hello view at hello top.</span></span> 
   <span data-ttu-id="86209-154">![Rechercher un utilisateur - capture d’écran](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="86209-154">![Find user - screenshot](./media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
3. <span data-ttu-id="86209-155">Vérifiez le nom de tootheir suivant hello boîte.</span><span class="sxs-lookup"><span data-stu-id="86209-155">Check hello box next tootheir name.</span></span>
4. <span data-ttu-id="86209-156">Sur la droite, sous étapes rapides de hello, choisissez **activer** ou **désactiver**.</span><span class="sxs-lookup"><span data-stu-id="86209-156">On hello right, under quick steps, choose **Enable** or **Disable**.</span></span>
   <span data-ttu-id="86209-157">![Activer l’utilisateur sélectionné - capture d’écran](./media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="86209-157">![Enable selected user - screenshot](./media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>

   >[!TIP]
   ><span data-ttu-id="86209-158">*Activé* les utilisateurs basculent automatiquement trop*appliquée* quand ils s’inscrivent pour Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="86209-158">*Enabled* users automatically switch too*enforced* when they register for Azure MFA.</span></span> <span data-ttu-id="86209-159">Vous ne devez pas modifier manuellement hello utilisateur état tooenforced.</span><span class="sxs-lookup"><span data-stu-id="86209-159">You shouldn't manually change hello user state tooenforced.</span></span> 

5. <span data-ttu-id="86209-160">Confirmez votre sélection dans la fenêtre contextuelle hello qui s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="86209-160">Confirm your selection in hello pop-up window that opens.</span></span> 

<span data-ttu-id="86209-161">Après avoir activé des utilisateurs, vous devez les en avertir par e-mail.</span><span class="sxs-lookup"><span data-stu-id="86209-161">After you enable users, you should notify them via email.</span></span> <span data-ttu-id="86209-162">Indiquez-leur qu’ils sont demandées tooregister hello leur prochaine dans que connexion.</span><span class="sxs-lookup"><span data-stu-id="86209-162">Tell them that they'll be asked tooregister hello next time they sign in.</span></span> <span data-ttu-id="86209-163">En outre, si votre organisation utilise des applications non-Web qui ne prennent pas en charge l’authentification moderne, ils devez toocreate mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="86209-163">Also, if your organization uses non-browser apps that don't support modern authentication, they'll need toocreate app passwords.</span></span> <span data-ttu-id="86209-164">Vous pouvez également inclure un lien de tooour [guide de l’utilisateur final de l’authentification Multifacteur Azure](./end-user/multi-factor-authentication-end-user.md) toohelp leur prise en main.</span><span class="sxs-lookup"><span data-stu-id="86209-164">You can also include a link tooour [Azure MFA end-user guide](./end-user/multi-factor-authentication-end-user.md) toohelp them get started.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="86209-165">Utiliser PowerShell</span><span class="sxs-lookup"><span data-stu-id="86209-165">Use PowerShell</span></span>
<span data-ttu-id="86209-166">utilisation de l’état de toochange hello utilisateur état [PowerShell Azure AD](/powershell/azure/overview), modifier `$st.State`.</span><span class="sxs-lookup"><span data-stu-id="86209-166">toochange hello user status state using [Azure AD PowerShell](/powershell/azure/overview), change `$st.State`.</span></span> <span data-ttu-id="86209-167">Il existe trois états possibles :</span><span class="sxs-lookup"><span data-stu-id="86209-167">There are three possible states:</span></span>

* <span data-ttu-id="86209-168">Activé</span><span class="sxs-lookup"><span data-stu-id="86209-168">Enabled</span></span>
* <span data-ttu-id="86209-169">Appliquée</span><span class="sxs-lookup"><span data-stu-id="86209-169">Enforced</span></span>
* <span data-ttu-id="86209-170">Désactivé</span><span class="sxs-lookup"><span data-stu-id="86209-170">Disabled</span></span>  

<span data-ttu-id="86209-171">Ne déplacez pas les utilisateurs directement toohello *appliqué* état.</span><span class="sxs-lookup"><span data-stu-id="86209-171">Don't move users directly toohello *Enforced* state.</span></span> <span data-ttu-id="86209-172">Applications sans navigateur cessera de fonctionner, car l’utilisateur de hello n'a pas fait l’objet d’inscription de l’authentification Multifacteur et obtenu une [mot de passe](multi-factor-authentication-whats-next.md#app-passwords).</span><span class="sxs-lookup"><span data-stu-id="86209-172">Non-browser-based apps will stop working because hello user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span></span> 

<span data-ttu-id="86209-173">À l’aide de PowerShell d’est une bonne option lorsque vous avez besoin toobulk permettant aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="86209-173">Using PowerShell is a good option when you need toobulk enabling users.</span></span> <span data-ttu-id="86209-174">Créez un script PowerShell qui effectue une itération sur une liste d’utilisateurs et active ces utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="86209-174">Create a PowerShell script that loops through a list of users and enables them:</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="86209-175">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="86209-175">Here is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a><span data-ttu-id="86209-176">Activer Azure MFA avec une stratégie d’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="86209-176">Enable Azure MFA with a conditional access policy</span></span>

<span data-ttu-id="86209-177">L’accès conditionnel est une fonctionnalité payante d’Azure Active Directory qui offre de nombreuses options de configuration.</span><span class="sxs-lookup"><span data-stu-id="86209-177">Conditional access is a paid feature of Azure Active Directory, with many possible configuration options.</span></span> <span data-ttu-id="86209-178">Ces étapes guident monodirectionnelle toocreate une stratégie.</span><span class="sxs-lookup"><span data-stu-id="86209-178">These steps walk through one way toocreate a policy.</span></span> <span data-ttu-id="86209-179">Pour plus d’informations, consultez [Accès conditionnel dans Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="86209-179">For more information, read about [Conditional Access in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).</span></span>

1. <span data-ttu-id="86209-180">Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="86209-180">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="86209-181">Accédez trop**Azure Active Directory** > **accès conditionnel**.</span><span class="sxs-lookup"><span data-stu-id="86209-181">Go too**Azure Active Directory** > **Conditional access**.</span></span>
3. <span data-ttu-id="86209-182">Sélectionnez **Nouvelle stratégie**.</span><span class="sxs-lookup"><span data-stu-id="86209-182">Select **New policy**.</span></span>
4. <span data-ttu-id="86209-183">Sous **Affectations**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="86209-183">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="86209-184">Hello d’utilisation **Include** et **exclure** onglets toospecify quels utilisateurs et groupes qui est géré par la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="86209-184">Use hello **Include** and **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>
5. <span data-ttu-id="86209-185">Sous **Affectations**, sélectionnez **Applications cloud**.</span><span class="sxs-lookup"><span data-stu-id="86209-185">Under **Assignments**, select **Cloud apps**.</span></span> <span data-ttu-id="86209-186">Choisissez tooinclude **toutes les applications de cloud**.</span><span class="sxs-lookup"><span data-stu-id="86209-186">Choose tooinclude **All cloud apps**.</span></span>
6. <span data-ttu-id="86209-187">Sous **Contrôles d’accès**, sélectionnez **Accorder**.</span><span class="sxs-lookup"><span data-stu-id="86209-187">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="86209-188">Choisissez **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="86209-188">Choose **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="86209-189">Activer **activer la stratégie** trop**sur** , puis sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="86209-189">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="86209-190">Hello autres options dans la stratégie d’accès conditionnel hello permettent toospecify exactement lors de la vérification en deux étapes doit être requise.</span><span class="sxs-lookup"><span data-stu-id="86209-190">hello other options in hello conditional access policy allow you toospecify exactly when two-step verification should be required.</span></span> <span data-ttu-id="86209-191">Par exemple, vous pouvez apporter une stratégie qui stipule : lors de sous-traitants tooaccess notre application d’approvisionnement des réseaux non approuvés sur les appareils qui ne sont pas joints au domaine, nécessitent la vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="86209-191">For example, you could make a policy that states: when contractors try tooaccess our procurement app from untrusted networks on devices that are not domain-joined, require two-step verification.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="86209-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86209-192">Next steps</span></span>

- <span data-ttu-id="86209-193">Obtenir des conseils sur hello [meilleures pratiques pour l’accès conditionnel](../active-directory/active-directory-conditional-access-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="86209-193">Get tips on hello [Best practices for conditional access](../active-directory/active-directory-conditional-access-best-practices.md)</span></span>

- <span data-ttu-id="86209-194">Gérer les paramètres de l’authentification multifacteur pour [vos utilisateurs et leurs appareils](multi-factor-authentication-manage-users-and-devices.md)</span><span class="sxs-lookup"><span data-stu-id="86209-194">Manage Multi-Factor Authentication settings for [your users and their devices](multi-factor-authentication-manage-users-and-devices.md)</span></span>