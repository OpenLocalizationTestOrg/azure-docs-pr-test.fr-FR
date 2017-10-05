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
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="618de-103">Activer la synchronisation du mot de passe pour Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="618de-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="618de-104">Dans les tâches précédentes, vous avez activé Azure Active Directory Domain Services pour votre locataire Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="618de-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="618de-105">Dans la tâche suivante, vous allez activer la synchronisation des hachages d’informations d’identification requis pour l’authentification NT LAN Manager (NTLM) et Kerberos avec Services de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="618de-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="618de-106">Une fois la synchronisation des informations d’identification configurée, les utilisateurs peuvent se connecter au domaine managé à l’aide de leurs informations d’identification d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="618de-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="618de-107">Les étapes nécessaires sont différentes pour les comptes d’utilisateurs uniquement dans le cloud par rapport aux comptes d’utilisateurs qui sont synchronisés à partir de votre répertoire local à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="618de-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="618de-108">Si votre locataire Azure AD utilise une combinaison d’utilisateurs dans le cloud uniquement et d’utilisateurs provenant de votre répertoire Active Directory local, vous devez effectuer ces deux étapes.</span><span class="sxs-lookup"><span data-stu-id="618de-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="618de-109">**Comptes d’utilisateurs uniquement dans le cloud** : [synchroniser les mots de passe des comptes d’utilisateurs uniquement dans le cloud avec votre domaine géré](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="618de-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="618de-110">**Comptes d’utilisateurs locaux** : [synchroniser les mots de passe des comptes d’utilisateurs synchronisés à partir de votre répertoire Active Directory local avec votre domaine géré](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="618de-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="618de-111">Tâche 5 : activer la synchronisation de mot de passe avec votre domaine géré pour les comptes d’utilisateurs uniquement dans le cloud</span><span class="sxs-lookup"><span data-stu-id="618de-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="618de-112">Pour authentifier les utilisateurs sur le domaine managé, Azure AD DS exige que les hachages d’informations d’identification présentent un format adapté à l’authentification NTLM et Kerberos.</span><span class="sxs-lookup"><span data-stu-id="618de-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="618de-113">Azure AD ne génère pas et ne stocke pas les hachages d’informations d’identification dans le format requis pour l’authentification NTLM ou Kerberos, à moins que vous n’activiez Azure Active Directory Domain Services pour votre locataire.</span><span class="sxs-lookup"><span data-stu-id="618de-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="618de-114">Pour des raisons évidentes de sécurité, Azure AD ne stocke pas non plus d’informations de mot de passe dans un format en texte clair.</span><span class="sxs-lookup"><span data-stu-id="618de-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="618de-115">Par conséquent, Azure AD n’a pas la capacité de générer automatiquement ces hachages d’informations d’identification NTLM ou Kerberos en fonction des informations d’identification existantes des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="618de-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="618de-116">Si votre organisation utilise des comptes d’utilisateurs dans le cloud uniquement, les utilisateurs ayant besoin Azure Active Directory Domain Services doivent modifier leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="618de-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="618de-117">Un compte d’utilisateur uniquement dans le cloud est un compte qui a été créé dans votre répertoire Azure AD à l’aide du portail Azure ou d’applets de commande PowerShell Azure AD.</span><span class="sxs-lookup"><span data-stu-id="618de-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="618de-118">Ces comptes d’utilisateurs ne sont pas synchronisés à partir d’un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="618de-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="618de-119">Le processus de modification du mot de passe entraîne la génération, dans Azure AD, des hachages d’informations d’identification requis par Azure AD DS pour l’authentification Kerberos et NTLM.</span><span class="sxs-lookup"><span data-stu-id="618de-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="618de-120">Vous pouvez faire expirer les mots de passe de tous les utilisateurs du locataire qui doivent recourir à Azure AD DS, ou demander à ces utilisateurs de modifier leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="618de-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="618de-121">Activer la génération du hachage des informations d’identification NTLM et Kerberos pour un compte d’utilisateur dans le cloud uniquement</span><span class="sxs-lookup"><span data-stu-id="618de-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="618de-122">Voici les instructions que vous devez fournir aux utilisateurs pour qu’ils puissent modifier leur mot de passe :</span><span class="sxs-lookup"><span data-stu-id="618de-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="618de-123">Accédez à la [page du volet d’accès Azure AD](http://myapps.microsoft.com) de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="618de-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Ouvrez le panneau d’accès Azure AD](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="618de-125">Dans l’angle supérieur droit, cliquez sur votre nom, puis sélectionnez **Profil** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="618de-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Sélectionner un profil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="618de-127">Sur la page **profil**, cliquez sur **Modifier le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="618de-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Cliquez sur « Modifier le mot de passe »](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="618de-129">Si l’option **Modifier le mot de passe** ne s’affiche pas sur la fenêtre du volet d’accès, vérifiez que votre organisation a configuré la [gestion des mots de passe dans Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="618de-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="618de-130">Sur la page **Modifier le mot de passe**, saisissez votre ancien mot de passe, puis tapez un nouveau mot de passe et confirmez-le.</span><span class="sxs-lookup"><span data-stu-id="618de-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Créer un réseau virtuel pour les services de domaine Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="618de-132">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="618de-132">Click **submit**.</span></span>

<span data-ttu-id="618de-133">Quelques minutes après cette modification, le nouveau mot de passe est utilisable Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="618de-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="618de-134">Après 20 minutes environ (en général), vous pouvez vous connecter aux ordinateurs joints au domaine managé à l’aide du nouveau mot de passe.</span><span class="sxs-lookup"><span data-stu-id="618de-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="618de-135">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="618de-135">Related Content</span></span>
* [<span data-ttu-id="618de-136">Comment mettre à jour votre mot de passe</span><span class="sxs-lookup"><span data-stu-id="618de-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="618de-137">Prise en main de la gestion de mot de passe dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="618de-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="618de-138">Activer la synchronisation de mot de passe dans Azure Active Directory Domain Services pour un locataire Azure AD synchronisé</span><span class="sxs-lookup"><span data-stu-id="618de-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="618de-139">Administrer un domaine managé par Azure Active Directory Domain Services </span><span class="sxs-lookup"><span data-stu-id="618de-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="618de-140">Joindre une machine virtuelle Windows à un domaine managé par Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="618de-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="618de-141">Joindre une machine virtuelle Red Hat Enterprise Linux à un domaine managé par Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="618de-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
