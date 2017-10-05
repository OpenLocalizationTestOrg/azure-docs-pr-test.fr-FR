---
title: Configurer des applications SaaS pour B2B Collaboration dans Azure Active Directory | Microsoft Docs
description: Code et exemples PowerShell pour Azure Active Directory B2B Collaboration
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="a9f49-103">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="a9f49-104">Azure Active Directory (Azure AD) B2B Collaboration fonctionne avec la plupart des applications qui s’intègrent à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9f49-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="a9f49-105">Dans cette section, nous vous fournissons des instructions sur la configuration de certaines applications SAP populaires à utiliser avec Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="a9f49-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="a9f49-106">Avant d’examiner les instructions propres aux applications, voici quelques règles générales :</span><span class="sxs-lookup"><span data-stu-id="a9f49-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="a9f49-107">Pour la plupart des applications, le paramétrage utilisateur doit être effectué manuellement.</span><span class="sxs-lookup"><span data-stu-id="a9f49-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="a9f49-108">Autrement dit, les utilisateurs doivent également être créés manuellement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a9f49-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="a9f49-109">Pour les applications qui prennent en charge la configuration automatique, par exemple Dropbox, des invitations distinctes sont créées à partir des applications.</span><span class="sxs-lookup"><span data-stu-id="a9f49-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="a9f49-110">Les utilisateurs doivent accepter chaque invitation.</span><span class="sxs-lookup"><span data-stu-id="a9f49-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="a9f49-111">Dans les attributs d’utilisateur, pour atténuer les problèmes liés aux disques de profil utilisateur altérés dans les utilisateurs invités, définissez toujours **Identificateur d’utilisateur** sur **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="a9f49-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="a9f49-112">Dropbox Business</span></span>

<span data-ttu-id="a9f49-113">Pour permettre aux utilisateurs de se connecter à l’aide de leur compte d’organisation, vous devez configurer manuellement Dropbox Business pour utiliser Azure AD comme fournisseur d’identité SAML (Security Assertion Markup Language).</span><span class="sxs-lookup"><span data-stu-id="a9f49-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="a9f49-114">Si Dropbox for Business n’a pas été configuré à cette intention, l’application ne peut pas inviter ni autoriser les utilisateurs à se connecter à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9f49-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="a9f49-115">Pour ajouter l’application Dropbox Business dans Azure AD, sélectionnez **Applications d’entreprise** dans le volet gauche, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![Bouton « Ajouter » dans la page Applications d’entreprise](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="a9f49-117">Dans la fenêtre **Ajouter une application**, entrez **dropbox** dans la zone de recherche, puis sélectionnez **Dropbox Business** dans la liste de résultats.</span><span class="sxs-lookup"><span data-stu-id="a9f49-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Rechercher « dropbox » dans la page Ajouter une application](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="a9f49-119">Dans la page **Authentification unique**, sélectionnez **Authentification unique** dans le volet gauche, puis entrez **user.mail** dans la zone **Identificateur d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="a9f49-120">(Il est défini comme UPN par défaut).</span><span class="sxs-lookup"><span data-stu-id="a9f49-120">(It's set as UPN by default.)</span></span>

  ![Configuration de l’authentification unique pour l’application](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="a9f49-122">Pour télécharger le certificat à utiliser pour la configuration de Dropbox, sélectionnez **Configurer Dropbox**, puis **URL SSO SAML** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a9f49-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Téléchargement du certificat pour la configuration de Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="a9f49-124">Connectez-vous à Dropbox avec l’URL de connexion à partir de la page **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Page de connexion Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="a9f49-126">Dans le menu, sélectionnez **Console d’administration**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-126">On the menu, select **Admin Console**.</span></span>

  ![Lien « Console d’administration » dans le menu Dropbox](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="a9f49-128">Dans la boîte de dialogue **Authentification**, sélectionnez **Plus**, chargez le certificat, puis, dans la zone **URL de connexion**, entrez l’URL SSO SAML.</span><span class="sxs-lookup"><span data-stu-id="a9f49-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![Lien « Plus » dans la boîte de dialogue Authentification réduite](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Lien « URL de connexion » dans la boîte de dialogue Authentification développée](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="a9f49-131">Pour configurer le paramétrage utilisateur automatique dans le portail Azure, sélectionnez **Approvisionnement** dans le volet gauche, puis sélectionnez **Automatique** dans la zone **Mode d’approvisionnement** et **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configuration de l’approvisionnement d’utilisateurs automatique dans le portail Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="a9f49-133">Une fois que les utilisateurs invités ou membres ont été configurés dans l’application Dropbox, ils reçoivent une invitation distincte de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a9f49-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="a9f49-134">Pour utiliser l’authentification unique de Dropbox, les invités doivent accepter l’invitation en cliquant sur un lien qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="a9f49-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="a9f49-135">Box</span><span class="sxs-lookup"><span data-stu-id="a9f49-135">Box</span></span>
<span data-ttu-id="a9f49-136">Vous pouvez autoriser les utilisateurs à authentifier les utilisateurs invités de Box avec leur compte Azure AD à l’aide de la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="a9f49-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="a9f49-137">Dans cette procédure, vous chargez les métadonnées vers Box.com.</span><span class="sxs-lookup"><span data-stu-id="a9f49-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="a9f49-138">Ajoutez l’application Box à partir des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="a9f49-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="a9f49-139">Configurez l’authentification unique dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="a9f49-139">Configure single sign-on in the following order:</span></span>

  ![Configurer l’authentification unique de Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="a9f49-141">a.</span><span class="sxs-lookup"><span data-stu-id="a9f49-141">a.</span></span> <span data-ttu-id="a9f49-142">Dans la zone **URL de connexion**, vérifiez que l’URL de connexion est définie correctement pour Box dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9f49-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="a9f49-143">Cette URL est celle de votre client Box.com.</span><span class="sxs-lookup"><span data-stu-id="a9f49-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="a9f49-144">Elle doit suivre la convention d’affectation de noms *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="a9f49-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="a9f49-145">L’**Identificateur** ne s’applique pas à cette application, mais apparaît toujours comme un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="a9f49-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="a9f49-146">b.</span><span class="sxs-lookup"><span data-stu-id="a9f49-146">b.</span></span> <span data-ttu-id="a9f49-147">Dans la zone **Identificateur d’utilisateur**, entrez **user.mail** (pour l’authentification unique des comptes d’invité).</span><span class="sxs-lookup"><span data-stu-id="a9f49-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="a9f49-148">c.</span><span class="sxs-lookup"><span data-stu-id="a9f49-148">c.</span></span> <span data-ttu-id="a9f49-149">Sous **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="a9f49-150">d.</span><span class="sxs-lookup"><span data-stu-id="a9f49-150">d.</span></span> <span data-ttu-id="a9f49-151">Pour configurer votre client Box.com pour utiliser Azure AD comme fournisseur d’identité, téléchargez le fichier de métadonnées et enregistrez-le sur votre lecteur local.</span><span class="sxs-lookup"><span data-stu-id="a9f49-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="a9f49-152">e.</span><span class="sxs-lookup"><span data-stu-id="a9f49-152">e.</span></span> <span data-ttu-id="a9f49-153">Transférez le fichier de métadonnées à l’équipe de support Box, qui configure l’authentification unique pour vous.</span><span class="sxs-lookup"><span data-stu-id="a9f49-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="a9f49-154">Pour le paramétrage utilisateur automatique d’Azure AD, dans le volet gauche, sélectionnez **Approvisionnement**, puis **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="a9f49-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autoriser Azure AD à se connecter à Box](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="a9f49-156">À l’instar des invités Dropbox, les invités Box doivent utiliser leur invitation reçue de l’application Box.</span><span class="sxs-lookup"><span data-stu-id="a9f49-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9f49-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9f49-157">Next steps</span></span>

<span data-ttu-id="a9f49-158">Consultez les articles suivants sur Azure AD B2B Collaboration :</span><span class="sxs-lookup"><span data-stu-id="a9f49-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a9f49-159">Qu'est-ce que la collaboration B2B d'Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="a9f49-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a9f49-160">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="a9f49-161">Ajout d’un utilisateur B2B Collaboration à un rôle</span><span class="sxs-lookup"><span data-stu-id="a9f49-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="a9f49-162">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="a9f49-163">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="a9f49-164">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9f49-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="a9f49-165">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="a9f49-166">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="a9f49-167">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="a9f49-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="a9f49-168">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="a9f49-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
