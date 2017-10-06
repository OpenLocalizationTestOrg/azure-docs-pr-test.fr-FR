---
title: "Azure Active Directory Domain Services : activer la synchronisation de mot de passe | Microsoft Docs"
description: Prise en main des services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="149e9-103">Activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="149e9-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="149e9-104">Dans les tâches précédentes, vous avez activé Azure Active Directory Domain Services pour votre locataire Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="149e9-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="149e9-105">la tâche suivante Hello est synchronisation tooenable des hachages d’informations d’identification requises pour tooAzure de l’authentification NT LAN Manager (NTLM) et Kerberos, les Services de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="149e9-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="149e9-106">Une fois que vous avez configuré la synchronisation des informations d’identification, les utilisateurs peuvent se connecter dans toohello le domaine géré avec leurs informations d’identification d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="149e9-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="149e9-107">Hello différentes étapes sont différents pour les comptes d’utilisateur utilisateur cloud uniquement les comptes Visual Studio qui sont synchronisés à partir de votre annuaire local à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="149e9-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="149e9-108">Si votre client Azure AD a une combinaison de cloud uniquement les utilisateurs et les utilisateurs de votre service Active Directory, vous devez tooperform les deux étapes.</span><span class="sxs-lookup"><span data-stu-id="149e9-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="149e9-109">**Comptes d’utilisateur uniquement dans le cloud**: [synchroniser les mots de passe pour le domaine géré de tooyour des comptes d’utilisateurs uniquement dans le cloud](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="149e9-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="149e9-110">**Comptes d’utilisateur locaux**: [synchroniser les mots de passe des comptes d’utilisateur synchronisés à partir de votre site AD tooyour gérés domaine](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="149e9-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="149e9-111">Tâche 5 : activer le mot de passe tooyour managé domaine de synchronisation des comptes d’utilisateur uniquement dans le cloud</span><span class="sxs-lookup"><span data-stu-id="149e9-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="149e9-112">utilisateurs tooauthenticate sur hello managée domaine, Azure Active Directory Domain Services a besoin des informations d’identification hachages dans un format qui convient pour l’authentification NTLM et Kerberos.</span><span class="sxs-lookup"><span data-stu-id="149e9-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="149e9-113">Azure AD ne pas générer et stocker les hachages d’informations d’identification au format hello qui est requis pour l’authentification NTLM ou Kerberos, jusqu'à ce que vous activez Azure Active Directory Domain Services pour votre client.</span><span class="sxs-lookup"><span data-stu-id="149e9-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="149e9-114">Pour des raisons évidentes de sécurité, Azure AD ne stocke pas non plus d’informations de mot de passe dans un format en texte clair.</span><span class="sxs-lookup"><span data-stu-id="149e9-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="149e9-115">Par conséquent, Azure AD n’a pas un moyen tooautomatically générer ces hachages d’informations d’identification NTLM ou Kerberos selon les informations d’identification existantes des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="149e9-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="149e9-116">Si votre organisation a des comptes d’utilisateur uniquement dans le cloud, les utilisateurs qui ont besoin de Services de domaine Active Directory toouse Azure doivent changer leurs mots de passe.</span><span class="sxs-lookup"><span data-stu-id="149e9-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="149e9-117">Un compte d’utilisateur uniquement dans le cloud est un compte qui a été créé dans votre annuaire Azure AD à l’aide de hello portail Azure ou applets de commande PowerShell Azure AD.</span><span class="sxs-lookup"><span data-stu-id="149e9-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="149e9-118">Ces comptes d’utilisateurs ne sont pas synchronisés à partir d’un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="149e9-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="149e9-119">Ce processus de modification de mot de passe entraîne des informations d’identification hello hachages qui sont requis par Azure Active Directory Domain Services pour toobe de l’authentification Kerberos et NTLM générée dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="149e9-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="149e9-120">Vous pouvez soit faire expirer les mots de passe hello pour tous les utilisateurs de hello client qui ont besoin de Services de domaine Active Directory toouse Azure ou leur demander de toochange leurs mots de passe.</span><span class="sxs-lookup"><span data-stu-id="149e9-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="149e9-121">Activer la génération du hachage des informations d’identification NTLM et Kerberos pour un compte d’utilisateur dans le cloud uniquement</span><span class="sxs-lookup"><span data-stu-id="149e9-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="149e9-122">Voici les instructions hello que nécessaires tooprovide utilisateurs, afin qu’ils peuvent modifier leurs mots de passe :</span><span class="sxs-lookup"><span data-stu-id="149e9-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="149e9-123">Accédez toohello [panneau d’accès Azure AD](http://myapps.microsoft.com) page de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="149e9-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Lancer le panneau d’accès Azure AD hello](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="149e9-125">Dans hello coin supérieur droit, cliquez sur votre nom, puis sélectionnez **profil** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="149e9-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Sélectionner un profil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="149e9-127">Sur hello **profil** page, cliquez sur **Change password**.</span><span class="sxs-lookup"><span data-stu-id="149e9-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Cliquez sur « Modifier le mot de passe »](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="149e9-129">Si hello **Change password** option n’est pas affichée dans la fenêtre du panneau d’accès hello, assurez-vous que votre organisation a configuré [gestion des mots de passe dans Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="149e9-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="149e9-130">Sur hello **modifier le mot de passe** page, tapez votre mot de passe (ancien), tapez un nouveau mot de passe, puis confirmez-le.</span><span class="sxs-lookup"><span data-stu-id="149e9-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Créer un réseau virtuel pour les services de domaine Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="149e9-132">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="149e9-132">Click **submit**.</span></span>

<span data-ttu-id="149e9-133">Quelques minutes après avoir modifié votre mot de passe, le nouveau mot de passe hello est utilisable dans Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="149e9-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="149e9-134">Après quelques minutes (en général, environ 20 minutes), vous pouvez vous connecter toocomputers qui appartiennent à un domaine géré de toohello jointes à l’aide du mot de passe hello qui vient d’être modifié.</span><span class="sxs-lookup"><span data-stu-id="149e9-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="149e9-135">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="149e9-135">Related Content</span></span>
* [<span data-ttu-id="149e9-136">Comment tooupdate votre mot de passe</span><span class="sxs-lookup"><span data-stu-id="149e9-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="149e9-137">Prise en main de la gestion de mot de passe dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="149e9-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="149e9-138">Activer la synchronisation de mot de passe du locataire tooAzure Active Directory Domain Services pour un Azure AD synchronisé</span><span class="sxs-lookup"><span data-stu-id="149e9-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="149e9-139">Administrer un domaine managé par Azure Active Directory Domain Services </span><span class="sxs-lookup"><span data-stu-id="149e9-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="149e9-140">Joindre un domaine géré par Azure Active Directory Domain Services de tooan de machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="149e9-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="149e9-141">Joindre un domaine géré par les Services de domaine Active Directory de Azure de tooan de machine virtuelle Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="149e9-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
