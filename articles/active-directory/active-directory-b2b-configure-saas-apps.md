---
title: les applications SaaS aaaConfigure pour une collaboration B2B dans Azure Active Directory | Documents Microsoft
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="c90be-103">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="c90be-104">Azure Active Directory (Azure AD) B2B Collaboration fonctionne avec la plupart des applications qui s’intègrent à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c90be-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="c90be-105">Dans cette section, nous vous fournissons des instructions sur la configuration de certaines applications SAP populaires à utiliser avec Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="c90be-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="c90be-106">Avant d’examiner les instructions propres aux applications, voici quelques règles générales :</span><span class="sxs-lookup"><span data-stu-id="c90be-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="c90be-107">Pour la plupart des applications de hello, programme d’installation de l’utilisateur a besoin de toohappen manuellement.</span><span class="sxs-lookup"><span data-stu-id="c90be-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="c90be-108">Autrement dit, les utilisateurs doivent être créés manuellement dans l’application hello également.</span><span class="sxs-lookup"><span data-stu-id="c90be-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="c90be-109">Pour les applications qui prennent en charge le programme d’installation automatique, telles que l’échange, invitations distinctes sont créées à partir d’applications de hello.</span><span class="sxs-lookup"><span data-stu-id="c90be-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="c90be-110">Les utilisateurs doit être tooaccept que chaque invitation.</span><span class="sxs-lookup"><span data-stu-id="c90be-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="c90be-111">Dans les attributs utilisateur hello, toomitigate les problèmes avec le disque de profil utilisateur altéré (UPD) dans les utilisateurs invités, toujours la valeur **identificateur de l’utilisateur** trop**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="c90be-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="c90be-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="c90be-112">Dropbox Business</span></span>

<span data-ttu-id="c90be-113">tooenable les toosign les utilisateurs à l’aide de leur compte d’organisation, vous devez configurer manuellement échange Business toouse Azure AD comme fournisseur d’identité Security Assertion Markup Language (SAML).</span><span class="sxs-lookup"><span data-stu-id="c90be-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="c90be-114">Si l’entreprise de l’échange n’a pas été configuré toodo par conséquent, il ne peut pas demander ou autorisent toosign les utilisateurs à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c90be-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="c90be-115">application d’entreprise de l’échange hello tooadd dans Azure AD, sélectionnez **des applications d’entreprise** dans hello du volet gauche, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c90be-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![bouton « Ajouter » de Hello sur la page des applications Enterprise hello](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="c90be-117">Bonjour **ajouter une application** fenêtre, entrez **dropbox** dans hello de zone de recherche, puis sélectionnez **Dropbox for Business** dans la liste des résultats hello.</span><span class="sxs-lookup"><span data-stu-id="c90be-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Recherchez « échange » sur hello ajouter une page d’application](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="c90be-119">Sur hello **l’authentification unique** page, sélectionnez **l’authentification unique** dans hello du volet gauche, puis entrez **user.mail** Bonjour **identificateur de l’utilisateur** zone.</span><span class="sxs-lookup"><span data-stu-id="c90be-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="c90be-120">(Il est défini comme UPN par défaut).</span><span class="sxs-lookup"><span data-stu-id="c90be-120">(It's set as UPN by default.)</span></span>

  ![Configuration de l’authentification unique pour l’application hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="c90be-122">toodownload hello certificat toouse pour la configuration de l’échange, sélectionnez **configurer un échange**, puis sélectionnez **SAML Service URL d’authentification unique** dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="c90be-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Téléchargement du certificat hello pour la configuration de l’échange](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="c90be-124">Connexion tooDropbox avec hello authentification URL à partir de hello **l’authentification unique** page.</span><span class="sxs-lookup"><span data-stu-id="c90be-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![page de Hello signe dans l’échange](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="c90be-126">Dans le menu de hello, sélectionnez **Console d’administration**.</span><span class="sxs-lookup"><span data-stu-id="c90be-126">On hello menu, select **Admin Console**.</span></span>

  ![lien « Console d’administration » Hello menu de Dropbox de hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="c90be-128">Bonjour **authentification** boîte de dialogue, sélectionnez **plus**, télécharger hello certificat puis, dans hello **URL de connexion** , entrez l’URL de hello SAML l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c90be-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Hello le lien « Plus » dans la boîte de dialogue d’authentification hello réduit](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hello « URL de connexion » Bonjour développé la boîte de dialogue d’authentification](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="c90be-131">le programme d’installation automatique de l’utilisateur de tooconfigure Bonjour portail Azure, sélectionnez **Provisioning** dans le volet gauche de hello, sélectionnez **automatique** Bonjour **Mode d’approvisionnement** zone, puis sélectionnez **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="c90be-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configuration de l’approvisionnement automatique d’un utilisateur Bonjour portail Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="c90be-133">Une fois que les utilisateurs invités ou les membres ont été configurées dans l’application d’échange hello, ils reçoivent une invitation distincte à partir de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="c90be-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="c90be-134">toouse de l’authentification unique de l’échange, invités doivent accepter d’invitation hello en cliquant sur un lien.</span><span class="sxs-lookup"><span data-stu-id="c90be-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="c90be-135">Box</span><span class="sxs-lookup"><span data-stu-id="c90be-135">Box</span></span>
<span data-ttu-id="c90be-136">Vous pouvez activer les utilisateurs invités boîte du utilisateurs tooauthenticate avec leur compte Azure AD à l’aide de fédération qui est basée sur hello protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="c90be-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="c90be-137">Dans cette procédure, vous téléchargez tooBox.com de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="c90be-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="c90be-138">Ajouter l’application hello Box à partir d’applications d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="c90be-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="c90be-139">Configurer l’authentification unique sur Bonjour suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="c90be-139">Configure single sign-on in hello following order:</span></span>

  ![Configurer l’authentification unique de Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="c90be-141">a.</span><span class="sxs-lookup"><span data-stu-id="c90be-141">a.</span></span> <span data-ttu-id="c90be-142">Bonjour **URL de connexion** zone, assurez-vous que les URL de connexion hello est définie correctement pour la zone Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c90be-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="c90be-143">Cette URL est hello de votre locataire Box.com.</span><span class="sxs-lookup"><span data-stu-id="c90be-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="c90be-144">Elle doit suivre la convention d’affectation de noms de hello *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="c90be-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="c90be-145">Hello **identificateur** ne s’applique pas toothis application, mais il apparaît toujours comme un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c90be-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="c90be-146">b.</span><span class="sxs-lookup"><span data-stu-id="c90be-146">b.</span></span> <span data-ttu-id="c90be-147">Bonjour **identificateur de l’utilisateur** , entrez **user.mail** (pour l’authentification unique pour les comptes invité).</span><span class="sxs-lookup"><span data-stu-id="c90be-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="c90be-148">c.</span><span class="sxs-lookup"><span data-stu-id="c90be-148">c.</span></span> <span data-ttu-id="c90be-149">Sous **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="c90be-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="c90be-150">d.</span><span class="sxs-lookup"><span data-stu-id="c90be-150">d.</span></span> <span data-ttu-id="c90be-151">toobegin la configuration de votre toouse de locataire Box.com Azure AD comme fournisseur d’identité, téléchargez le fichier de métadonnées hello et enregistrez-le tooyour le disque local.</span><span class="sxs-lookup"><span data-stu-id="c90be-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="c90be-152">e.</span><span class="sxs-lookup"><span data-stu-id="c90be-152">e.</span></span> <span data-ttu-id="c90be-153">Transférer hello métadonnées fichier toohello zone équipe de support technique, qui permet de configurer l’authentification unique pour vous.</span><span class="sxs-lookup"><span data-stu-id="c90be-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="c90be-154">Pour l’installation automatique d’un utilisateur Azure AD, dans le volet gauche de hello, sélectionnez **Provisioning**, puis sélectionnez **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="c90be-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autoriser Azure AD tooconnect tooBox](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="c90be-156">Comme invités de l’échange, invités de la zone doivent échanger leur invitation à partir de l’application hello Box.</span><span class="sxs-lookup"><span data-stu-id="c90be-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c90be-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c90be-157">Next steps</span></span>

<span data-ttu-id="c90be-158">Consultez hello suivant des articles sur Azure AD B2B collaboration :</span><span class="sxs-lookup"><span data-stu-id="c90be-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c90be-159">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="c90be-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c90be-160">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c90be-161">Ajout d’un rôle tooa B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c90be-162">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c90be-163">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c90be-164">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="c90be-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c90be-165">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c90be-166">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c90be-167">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="c90be-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c90be-168">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="c90be-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
