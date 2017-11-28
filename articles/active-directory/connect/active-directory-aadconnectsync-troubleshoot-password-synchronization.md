---
title: synchronisation de mot de passe aaaTroubleshoot avec synchronisation Azure AD Connect | Documents Microsoft
description: "Cet article fournit des informations sur la façon tootroubleshoot les problèmes de synchronisation de mot de passe."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="2ba46-103">Résolution des problèmes de synchronisation de mot de passe avec Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="2ba46-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="2ba46-104">Cette rubrique explique comment tootroubleshoot problèmes avec la synchronisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2ba46-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="2ba46-105">Si les mots de passe ne se synchronisent pas comme prévu, il peut s’agir d’un sous-ensemble d’utilisateurs ou de tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2ba46-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="2ba46-106">Pour Azure Active Directory (Azure AD) connecter le déploiement avec la version 1.1.524.0 ou une version ultérieure, il existe désormais une applet de commande de diagnostic que vous pouvez utiliser des problèmes de synchronisation de mot de passe tootroubleshoot :</span><span class="sxs-lookup"><span data-stu-id="2ba46-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="2ba46-107">Si vous avez un problème dans lequel aucun des mots de passe ne sont synchronisés, consultez toohello [aucun mot de passe n’est synchronisés : résoudre les problèmes à l’aide d’applet de commande hello diagnostic](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span><span class="sxs-lookup"><span data-stu-id="2ba46-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="2ba46-108">Si vous avez un problème avec des objets individuels, consultez toohello [un objet ne synchronise pas les mots de passe : résoudre les problèmes à l’aide d’applet de commande hello diagnostic](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span><span class="sxs-lookup"><span data-stu-id="2ba46-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="2ba46-109">Pour les versions antérieures de déploiement Azure AD Connect :</span><span class="sxs-lookup"><span data-stu-id="2ba46-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="2ba46-110">Si vous avez un problème dans lequel aucun des mots de passe ne sont synchronisés, consultez toohello [aucun mot de passe n’est synchronisés : manuel des étapes de dépannage](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span><span class="sxs-lookup"><span data-stu-id="2ba46-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="2ba46-111">Si vous avez un problème avec des objets individuels, consultez toohello [un objet ne synchronise pas les mots de passe : manuel des étapes de dépannage](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span><span class="sxs-lookup"><span data-stu-id="2ba46-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="2ba46-112">Aucun mot de passe n’est synchronisés : résoudre les problèmes à l’aide d’applet de commande hello diagnostic</span><span class="sxs-lookup"><span data-stu-id="2ba46-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="2ba46-113">Vous pouvez utiliser hello `Invoke-ADSyncDiagnostics` toofigure d’applet de commande out pour lesquelles aucun mot de passe n’est synchronisés.</span><span class="sxs-lookup"><span data-stu-id="2ba46-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="2ba46-114">Hello `Invoke-ADSyncDiagnostics` applet de commande est uniquement disponible pour Azure AD Connect version 1.1.524.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2ba46-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="2ba46-115">Exécutez l’applet de commande hello diagnostics</span><span class="sxs-lookup"><span data-stu-id="2ba46-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="2ba46-116">problèmes tootroubleshoot où aucun mot de passe n’est synchronisés :</span><span class="sxs-lookup"><span data-stu-id="2ba46-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="2ba46-117">Ouvrez une nouvelle session Windows PowerShell sur votre serveur Azure AD Connect avec hello **exécuter en tant qu’administrateur** option.</span><span class="sxs-lookup"><span data-stu-id="2ba46-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="2ba46-118">Exécutez `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="2ba46-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="2ba46-119">Exécutez `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="2ba46-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="2ba46-120">Exécutez `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="2ba46-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="2ba46-121">Comprendre les résultats hello d’applet de commande hello</span><span class="sxs-lookup"><span data-stu-id="2ba46-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="2ba46-122">applet de commande Hello diagnostic exécute hello contrôles :</span><span class="sxs-lookup"><span data-stu-id="2ba46-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="2ba46-123">Valide que hello fonctionnalité de synchronisation de mot de passe est activée pour votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba46-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="2ba46-124">Valide que hello Azure AD Connect serveur n’est pas en mode de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="2ba46-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="2ba46-125">Pour chaque locales existantes connecteur Active Directory (ce qui correspond à la forêt Active Directory existant tooan) :</span><span class="sxs-lookup"><span data-stu-id="2ba46-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="2ba46-126">Valide que hello fonctionnalité de synchronisation de mot de passe est activée.</span><span class="sxs-lookup"><span data-stu-id="2ba46-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="2ba46-127">Les journaux d’événements d’Application de Windows recherche les événements de pulsation de synchronisation de mot de passe Bonjour.</span><span class="sxs-lookup"><span data-stu-id="2ba46-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="2ba46-128">Pour chaque domaine Active Directory sous le connecteur Active Directory hello local :</span><span class="sxs-lookup"><span data-stu-id="2ba46-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="2ba46-129">Valide que hello domaine est accessible à partir du serveur de connexion hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba46-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="2ba46-130">Valide que les comptes de Services de domaine Active Directory (AD DS) hello utilisés par le connecteur Active Directory hello local a hello correct nom d’utilisateur, mot de passe et les autorisations requises pour la synchronisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2ba46-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="2ba46-131">Hello suivant schéma illustre les résultats de hello d’applet de commande hello pour une topologie de Active Directory de domaine unique, sur site :</span><span class="sxs-lookup"><span data-stu-id="2ba46-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Sortie de diagnostic pour la synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="2ba46-133">Hello le reste de cette section décrit des résultats spécifiques qui sont retournées par l’applet de commande hello et les problèmes correspondants.</span><span class="sxs-lookup"><span data-stu-id="2ba46-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="2ba46-134">La fonctionnalité de synchronisation de mot de passe n’est pas activée</span><span class="sxs-lookup"><span data-stu-id="2ba46-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="2ba46-135">Si vous n’avez pas activé la synchronisation de mot de passe à l’aide d’Assistant de hello Azure AD Connect, hello l’erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![La synchronisation de mot de passe n’est pas activée](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="2ba46-137">Le serveur Azure AD Connect est en mode intermédiaire</span><span class="sxs-lookup"><span data-stu-id="2ba46-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="2ba46-138">Si le serveur de Azure AD Connect de hello est en mode de préproduction, synchronisation de mot de passe est temporairement désactivée, et hello erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Le serveur Azure AD Connect est en mode intermédiaire](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="2ba46-140">Aucun événement de pulsation de synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="2ba46-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="2ba46-141">Chaque connecteur Active Directory local a son propre canal de synchronisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2ba46-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="2ba46-142">Lorsque le canal de synchronisation de mot de passe hello est établie et il n’existe pas de n’importe quel toobe de modifications de mot de passe synchronisé, un événement de pulsation (ID d’événement 654) est généré une fois toutes les 30 minutes sous hello journal des événements Windows.</span><span class="sxs-lookup"><span data-stu-id="2ba46-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="2ba46-143">Pour chaque connecteur Active Directory local, hello applet de commande recherche les événements de pulsation correspondants dans hello les trois dernières heures.</span><span class="sxs-lookup"><span data-stu-id="2ba46-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="2ba46-144">Si aucun événement de pulsation n’est trouvée, hello erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Aucun événement de pulsation de synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="2ba46-146">Le compte AD DS n’a pas les autorisations appropriées</span><span class="sxs-lookup"><span data-stu-id="2ba46-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="2ba46-147">Si le compte hello AD DS qui est utilisé par hello local hachages de mot de passe de toosynchronize de connecteur Active Directory n’a pas les autorisations appropriées hello, hello erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Informations d’identification incorrectes](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="2ba46-149">Nom d’utilisateur ou mot de passe du compte AD DS incorrect</span><span class="sxs-lookup"><span data-stu-id="2ba46-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="2ba46-150">Si hello AD DS le compte utilisé par hello hachages de mot de passe local Active Directory connector toosynchronize dispose d’un nom d’utilisateur incorrect ou le mot de passe, hello erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Informations d’identification incorrectes](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="2ba46-152">Un objet ne synchronise pas les mots de passe : résoudre les problèmes à l’aide d’applet de commande hello diagnostic</span><span class="sxs-lookup"><span data-stu-id="2ba46-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="2ba46-153">Vous pouvez utiliser hello `Invoke-ADSyncDiagnostics` toodetermine d’applet de commande pourquoi un objet ne synchronise pas les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="2ba46-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="2ba46-154">Hello `Invoke-ADSyncDiagnostics` applet de commande est uniquement disponible pour Azure AD Connect version 1.1.524.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2ba46-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="2ba46-155">Exécutez l’applet de commande hello diagnostics</span><span class="sxs-lookup"><span data-stu-id="2ba46-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="2ba46-156">problèmes tootroubleshoot où aucun mot de passe n’est synchronisés :</span><span class="sxs-lookup"><span data-stu-id="2ba46-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="2ba46-157">Ouvrez une nouvelle session Windows PowerShell sur votre serveur Azure AD Connect avec hello **exécuter en tant qu’administrateur** option.</span><span class="sxs-lookup"><span data-stu-id="2ba46-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="2ba46-158">Exécutez `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="2ba46-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="2ba46-159">Exécutez `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="2ba46-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="2ba46-160">Exécutez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="2ba46-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="2ba46-161">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ba46-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="2ba46-162">Comprendre les résultats hello d’applet de commande hello</span><span class="sxs-lookup"><span data-stu-id="2ba46-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="2ba46-163">applet de commande Hello diagnostic exécute hello contrôles :</span><span class="sxs-lookup"><span data-stu-id="2ba46-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="2ba46-164">Examine l’état hello d’objet Active Directory de hello dans l’espace de connecteur Active Directory hello métaverse et Azure espace de connecteur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ba46-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="2ba46-165">Vérifie qu’il n’y a des règles de synchronisation avec la synchronisation de mot de passe activée et appliquer l’objet d’Active Directory toohello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="2ba46-166">Tente de tooretrieve et l’affichage des résultats hello hello dernière tentative toosynchronize hello mot de passe pour l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="2ba46-167">Hello suivant schéma illustre les résultats de hello d’applet de commande hello lors de la résolution des problèmes de synchronisation de mot de passe pour un seul objet :</span><span class="sxs-lookup"><span data-stu-id="2ba46-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Sortie de diagnostic pour la synchronisation de mot de passe - objet unique](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="2ba46-169">Hello le reste de cette section décrit des résultats spécifiques retournés par l’applet de commande hello et les problèmes correspondants.</span><span class="sxs-lookup"><span data-stu-id="2ba46-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="2ba46-170">objet d’Active Directory Hello n’est pas exporté tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="2ba46-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="2ba46-171">Synchronisation de mot de passe pour ce compte d’Active Directory local échoue, car il n’existe aucun objet correspondant dans le locataire Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="2ba46-172">Hello, l’erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-172">hello following error is returned:</span></span>

![Objet Azure Active Directory manquant](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="2ba46-174">L’utilisateur a un mot de passe temporaire</span><span class="sxs-lookup"><span data-stu-id="2ba46-174">User has a temporary password</span></span>
<span data-ttu-id="2ba46-175">Actuellement, Azure AD Connect ne prend pas en charge la synchronisation des mots de passe temporaires avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba46-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="2ba46-176">Un mot de passe est considéré comme toobe temporaire si hello **modification de mot de passe à la prochaine ouverture de session** option est définie sur l’utilisateur de Active Directory local hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="2ba46-177">Hello, l’erreur suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="2ba46-177">hello following error is returned:</span></span>

![Le mot de passe temporaire n’est pas exporté](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="2ba46-179">Résultats de la dernière tentative de toosynchronize un mot de passe ne sont pas disponibles</span><span class="sxs-lookup"><span data-stu-id="2ba46-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="2ba46-180">Par défaut, Azure AD Connect stocke les résultats de hello de tentatives de synchronisation de mot de passe pendant sept jours.</span><span class="sxs-lookup"><span data-stu-id="2ba46-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="2ba46-181">Si aucun résultat n’est disponible pour l’objet d’Active Directory hello sélectionné, hello suivant l’avertissement est retourné :</span><span class="sxs-lookup"><span data-stu-id="2ba46-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Sortie de diagnostic pour un seul objet - aucun historique de synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="2ba46-183">Aucun mot de passe n’est synchronisé : étapes de dépannage manuel</span><span class="sxs-lookup"><span data-stu-id="2ba46-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="2ba46-184">Suivez ces toodetermine étapes pour lesquelles aucun mot de passe n’est synchronisés :</span><span class="sxs-lookup"><span data-stu-id="2ba46-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="2ba46-185">Serveur de se connecter hello dans [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="2ba46-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="2ba46-186">Un serveur en mode intermédiaire ne synchronise pas les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="2ba46-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="2ba46-187">Exécutez le script de hello dans hello [obtenir l’état de hello de paramètres de synchronisation de mot de passe](#get-the-status-of-password-sync-settings) section.</span><span class="sxs-lookup"><span data-stu-id="2ba46-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="2ba46-188">Il vous donne une vue d’ensemble de la configuration de la synchronisation de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Sortie de script PowerShell à partir des paramètres de synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="2ba46-190">Si la fonctionnalité de hello n’est pas activée dans Azure AD, ou si l’état de canal de synchronisation hello n’est pas activé, exécuter l’Assistant installation de se connecter hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="2ba46-191">Sélectionnez **Personnaliser les options de synchronisation** et désélectionnez la synchronisation de mot de passe. Cette modification désactive temporairement la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="2ba46-192">Ensuite, réexécutez hello et réactiver la synchronisation de mot de passe. Exécutez le script de hello nouveau tooverify qui hello configuration est correcte.</span><span class="sxs-lookup"><span data-stu-id="2ba46-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="2ba46-193">Recherchez dans le journal des événements hello pour les erreurs.</span><span class="sxs-lookup"><span data-stu-id="2ba46-193">Look in hello event log for errors.</span></span> <span data-ttu-id="2ba46-194">Recherchez hello suivant des événements, qui indiquent un problème :</span><span class="sxs-lookup"><span data-stu-id="2ba46-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="2ba46-195">Source : « Synchronisation d’annuaires » ID : 0, 611, 652, 655 Si vous voyez ces événements, vous avez un problème de connectivité.</span><span class="sxs-lookup"><span data-stu-id="2ba46-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="2ba46-196">message du journal des événements Hello contient des informations de forêt où vous avez un problème.</span><span class="sxs-lookup"><span data-stu-id="2ba46-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="2ba46-197">Pour plus d’informations, consultez [Problème de connectivité](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="2ba46-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="2ba46-198">Si vous ne voyez aucune pulsation ou que rien d’autre n’a fonctionné, exécutez [Déclencher une synchronisation complète de tous les mots de passe](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="2ba46-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="2ba46-199">Exécutez le script de hello qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="2ba46-199">Run hello script only once.</span></span>

6. <span data-ttu-id="2ba46-200">Consultez hello [résoudre les problèmes d’un objet qui ne se synchronise pas les mots de passe](#one-object-is-not-synchronizing-passwords) section.</span><span class="sxs-lookup"><span data-stu-id="2ba46-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="2ba46-201">Problèmes de connectivité</span><span class="sxs-lookup"><span data-stu-id="2ba46-201">Connectivity problems</span></span>

<span data-ttu-id="2ba46-202">Avez-vous une connectivité avec Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="2ba46-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="2ba46-203">Compte de hello ont requis des hachages de mot de passe autorisations tooread hello dans tous les domaines ?</span><span class="sxs-lookup"><span data-stu-id="2ba46-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="2ba46-204">Si vous avez installé de se connecter à l’aide de paramètres Express, hello autorisations doivent déjà être correctes.</span><span class="sxs-lookup"><span data-stu-id="2ba46-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="2ba46-205">Si vous avez utilisé une installation personnalisée, définir des autorisations de hello manuellement en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="2ba46-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="2ba46-206">compte de hello toofind utilisé par le connecteur Active Directory de hello, début **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="2ba46-207">Accédez trop**connecteurs**, puis recherchez forêt Active Directory de hello local vous dépannez.</span><span class="sxs-lookup"><span data-stu-id="2ba46-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="2ba46-208">Sélectionnez hello connecteur, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="2ba46-209">Accédez trop**connecter tooActive Directory forêt**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Compte utilisé par le connecteur Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="2ba46-211">Notez le nom d’utilisateur hello et domaine hello où se trouve le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="2ba46-212">Démarrer **Active Directory Users and Computers**, puis vérifiez que compte hello trouvés précédemment dispose des autorisations de suivi hello définie au niveau racine hello de tous les domaines de votre forêt :</span><span class="sxs-lookup"><span data-stu-id="2ba46-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="2ba46-213">Répliquer les changements d’annuaires</span><span class="sxs-lookup"><span data-stu-id="2ba46-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="2ba46-214">Répliquer les changements d’annuaire Tout</span><span class="sxs-lookup"><span data-stu-id="2ba46-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="2ba46-215">Est des contrôleurs de domaine est accessibles par Azure AD Connect hello ?</span><span class="sxs-lookup"><span data-stu-id="2ba46-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="2ba46-216">Si le serveur de se connecter de hello ne peut pas se connecter à des contrôleurs de domaine tooall, configurez **uniquement utiliser le contrôleur de domaine par défaut**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Contrôleur de domaine utilisé par le connecteur Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="2ba46-218">Revenir en arrière trop**Synchronization Service Manager** et **configurer la Partition de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="2ba46-219">Sélectionnez votre domaine dans **sélectionner les partitions d’annuaire**, sélectionnez hello **utiliser uniquement les contrôleurs de domaine par défaut** case à cocher, puis cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="2ba46-220">Dans la liste hello, entrez les contrôleurs de domaine hello que connexion doit utiliser pour la synchronisation de mot de passe. Hello même liste est utilisée pour importer et exporter également.</span><span class="sxs-lookup"><span data-stu-id="2ba46-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="2ba46-221">Effectuez ces étapes pour tous vos domaines.</span><span class="sxs-lookup"><span data-stu-id="2ba46-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="2ba46-222">Si le script de hello montre qu’il n’y a aucune pulsation, exécutez le script de hello [déclencher une synchronisation complète de tous les mots de passe](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="2ba46-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="2ba46-223">Un objet ne synchronise pas les mots de passe : étapes de dépannage manuel</span><span class="sxs-lookup"><span data-stu-id="2ba46-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="2ba46-224">Vous pouvez facilement résoudre les problèmes de synchronisation de mot de passe en consultant l’état hello d’un objet.</span><span class="sxs-lookup"><span data-stu-id="2ba46-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="2ba46-225">Dans **Active Directory Users and Computers**, recherchez hello utilisateur, puis vérifiez que hello **utilisateur doit changer de mot de passe à la prochaine ouverture de session** case à cocher est désactivée.</span><span class="sxs-lookup"><span data-stu-id="2ba46-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Mots de passe productifs Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="2ba46-227">Si la case à cocher hello est sélectionné, poser toosign d’utilisateur hello dans et modifier le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="2ba46-228">Les mots de passe temporaires ne sont pas synchronisés avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba46-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="2ba46-229">Si le mot de passe hello est correct dans Active Directory, procédez comme utilisateur hello dans le moteur de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="2ba46-230">Par utilisateur hello suivant à partir de tooAzure d’Active Directory sur site Active Directory, vous pouvez voir s’il existe une erreur descriptive sur l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="2ba46-231">a.</span><span class="sxs-lookup"><span data-stu-id="2ba46-231">a.</span></span> <span data-ttu-id="2ba46-232">Démarrer hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="2ba46-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="2ba46-233">b.</span><span class="sxs-lookup"><span data-stu-id="2ba46-233">b.</span></span> <span data-ttu-id="2ba46-234">Cliquez sur **Connecteurs**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-234">Click **Connectors**.</span></span>

    <span data-ttu-id="2ba46-235">c.</span><span class="sxs-lookup"><span data-stu-id="2ba46-235">c.</span></span> <span data-ttu-id="2ba46-236">Sélectionnez hello **connecteur Active Directory** où se trouve hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ba46-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="2ba46-237">d.</span><span class="sxs-lookup"><span data-stu-id="2ba46-237">d.</span></span> <span data-ttu-id="2ba46-238">Sélectionnez **Search Connector Space**(Rechercher l’espace de connecteur).</span><span class="sxs-lookup"><span data-stu-id="2ba46-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="2ba46-239">e.</span><span class="sxs-lookup"><span data-stu-id="2ba46-239">e.</span></span> <span data-ttu-id="2ba46-240">Bonjour **étendue** boîte, sélectionnez **DN ou ancre**, puis entrez le nom unique complet de hello d’utilisateur hello vous dépannez.</span><span class="sxs-lookup"><span data-stu-id="2ba46-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Rechercher un utilisateur dans l’espace de connecteur avec le nom unique](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="2ba46-242">f.</span><span class="sxs-lookup"><span data-stu-id="2ba46-242">f.</span></span> <span data-ttu-id="2ba46-243">Recherchez l’utilisateur hello vous recherchez, puis cliquez sur **propriétés** toosee tous hello d’attributs.</span><span class="sxs-lookup"><span data-stu-id="2ba46-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="2ba46-244">Si l’utilisateur de hello n’est pas dans le résultat de la recherche hello, vérifiez votre [règles de filtrage](active-directory-aadconnectsync-configure-filtering.md) et vérifiez que vous exécutez [appliquer et vérifier les modifications](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) pour tooappear d’utilisateur hello dans se connecter.</span><span class="sxs-lookup"><span data-stu-id="2ba46-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="2ba46-245">g.</span><span class="sxs-lookup"><span data-stu-id="2ba46-245">g.</span></span> <span data-ttu-id="2ba46-246">Cliquez sur la semaine dernière, détails de synchronisation de mot de passe de hello toosee d’objet hello pour hello **journal**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Détails d’un journal d’objet](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="2ba46-248">Si le journal d’objet hello est vide, Azure AD Connect a été le hachage de mot de passe hello tooread impossible à partir d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ba46-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="2ba46-249">Continuez la résolution des problèmes avec [Erreurs de connectivité](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="2ba46-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="2ba46-250">Si vous voyez une valeur autre que **réussite**, consultez la table toohello dans [journal de synchronisation de mot de passe](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="2ba46-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="2ba46-251">h.</span><span class="sxs-lookup"><span data-stu-id="2ba46-251">h.</span></span> <span data-ttu-id="2ba46-252">Sélectionnez hello **lignage** onglet et vérifiez que cette règle de synchronisation au moins un Bonjour **PasswordSync** colonne est **True**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="2ba46-253">Dans la configuration par défaut de hello, nom hello de la règle de synchronisation hello est **dans depuis AD - utilisateur AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informations de lignage sur un utilisateur](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="2ba46-255">i.</span><span class="sxs-lookup"><span data-stu-id="2ba46-255">i.</span></span> <span data-ttu-id="2ba46-256">Cliquez sur **propriétés d’objet métaverse** toodisplay une liste d’attributs de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2ba46-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Informations de métaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="2ba46-258">Vérifiez qu’aucun attribut **cloudFiltered** n’est présent.</span><span class="sxs-lookup"><span data-stu-id="2ba46-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="2ba46-259">Assurez-vous que les attributs de domaine hello (domainFQDN et domainNetBios) ont des valeurs attendues de hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="2ba46-260">j.</span><span class="sxs-lookup"><span data-stu-id="2ba46-260">j.</span></span> <span data-ttu-id="2ba46-261">Cliquez sur hello **connecteurs** onglet. Assurez-vous que les connecteurs tooboth locale Active Directory et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba46-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Informations de métaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="2ba46-263">k.</span><span class="sxs-lookup"><span data-stu-id="2ba46-263">k.</span></span> <span data-ttu-id="2ba46-264">Sélectionnez hello ligne représentant Azure AD, cliquez sur **propriétés**, puis cliquez sur hello **lignage** objet d’espace connecteur onglet hello doit avoir une règle sortante Bonjour **PasswordSync** jeu de colonnes trop**True**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="2ba46-265">Dans la configuration par défaut de hello, nom hello de la règle de synchronisation hello est **hors tooAAD - jointure utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Boîte de dialogue Propriétés de l’objet espace connecteur](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="2ba46-267">Journal de synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="2ba46-267">Password sync log</span></span>
<span data-ttu-id="2ba46-268">colonne d’état Hello peut avoir hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ba46-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="2ba46-269">État</span><span class="sxs-lookup"><span data-stu-id="2ba46-269">Status</span></span> | <span data-ttu-id="2ba46-270">Description</span><span class="sxs-lookup"><span data-stu-id="2ba46-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ba46-271">Succès</span><span class="sxs-lookup"><span data-stu-id="2ba46-271">Success</span></span> |<span data-ttu-id="2ba46-272">Le mot de passe a été correctement synchronisé.</span><span class="sxs-lookup"><span data-stu-id="2ba46-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="2ba46-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="2ba46-273">FilteredByTarget</span></span> |<span data-ttu-id="2ba46-274">Mot de passe est défini trop**utilisateur doit changer de mot de passe à la prochaine ouverture de session**.</span><span class="sxs-lookup"><span data-stu-id="2ba46-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="2ba46-275">Mot de passe n'a pas été synchronisé.</span><span class="sxs-lookup"><span data-stu-id="2ba46-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="2ba46-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="2ba46-276">NoTargetConnection</span></span> |<span data-ttu-id="2ba46-277">Aucun objet de métaverse de hello ou dans l’espace de connecteur hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ba46-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="2ba46-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="2ba46-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="2ba46-279">Aucun objet trouvé dans l’espace de connecteur Active Directory hello localement.</span><span class="sxs-lookup"><span data-stu-id="2ba46-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="2ba46-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="2ba46-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="2ba46-281">objet Hello Bonjour espace du connecteur Azure AD n’a pas été exporté.</span><span class="sxs-lookup"><span data-stu-id="2ba46-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="2ba46-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="2ba46-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="2ba46-283">L'entrée de journal a été créée avant la version 1.0.9125.0 et est affichée dans son état hérité.</span><span class="sxs-lookup"><span data-stu-id="2ba46-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="2ba46-284">Error</span><span class="sxs-lookup"><span data-stu-id="2ba46-284">Error</span></span> |<span data-ttu-id="2ba46-285">Le service a renvoyé une erreur inconnue.</span><span class="sxs-lookup"><span data-stu-id="2ba46-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="2ba46-286">Unknown</span><span class="sxs-lookup"><span data-stu-id="2ba46-286">Unknown</span></span> |<span data-ttu-id="2ba46-287">Une erreur s’est produite lors de la tentative de tooprocess un lot de hachages de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2ba46-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="2ba46-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="2ba46-288">MissingAttribute</span></span> |<span data-ttu-id="2ba46-289">Des attributs spécifiques (par exemple, le hachage Kerberos) requis par Azure AD Domain Services ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="2ba46-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="2ba46-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="2ba46-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="2ba46-291">Des attributs spécifiques (par exemple, le hachage Kerberos) requis par Azure AD Domain Services n’étaient pas disponibles précédemment.</span><span class="sxs-lookup"><span data-stu-id="2ba46-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="2ba46-292">Hachage de mot de passe d’une tentative de tooresynchronize hello utilisateur est établie.</span><span class="sxs-lookup"><span data-stu-id="2ba46-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="2ba46-293">Dépannage de scripts toohelp</span><span class="sxs-lookup"><span data-stu-id="2ba46-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="2ba46-294">Obtenir l’état de hello de paramètres de synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="2ba46-294">Get hello status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="2ba46-295">Déclencher une synchronisation complète de tous les mots de passe</span><span class="sxs-lookup"><span data-stu-id="2ba46-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="2ba46-296">Exécutez ce script une seule fois.</span><span class="sxs-lookup"><span data-stu-id="2ba46-296">Run this script only once.</span></span> <span data-ttu-id="2ba46-297">Si vous devez toorun il plusieurs fois, problème est ailleurs hello.</span><span class="sxs-lookup"><span data-stu-id="2ba46-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="2ba46-298">problème de hello tootroubleshoot, contactez le support technique Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2ba46-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="2ba46-299">Vous pouvez déclencher une synchronisation complète de tous les mots de passe à l’aide de hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="2ba46-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="2ba46-300">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ba46-300">Next steps</span></span>
* [<span data-ttu-id="2ba46-301">Implémentation de la synchronisation de mot de passe avec Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="2ba46-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="2ba46-302">Azure AD Connect Sync : Personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="2ba46-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="2ba46-303">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ba46-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
