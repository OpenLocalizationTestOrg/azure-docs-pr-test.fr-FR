---
title: "Didacticiel : Intégration d’Azure Active Directory à Procore SSO | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’authentification unique Procore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="f6fe5-103">Didacticiel : Intégration d’Azure Active Directory à Procore SSO</span><span class="sxs-lookup"><span data-stu-id="f6fe5-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="f6fe5-104">Dans ce didacticiel, vous apprendrez comment toointegrate Procore l’authentification unique avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6fe5-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6fe5-105">Intégration SSO Procore à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6fe5-106">Vous pouvez contrôler dans Azure AD qui a accès tooProcore SSO</span><span class="sxs-lookup"><span data-stu-id="f6fe5-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="f6fe5-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooProcore l’authentification unique (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6fe5-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="f6fe5-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f6fe5-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6fe5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="f6fe5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f6fe5-110">Prerequisites</span></span>

<span data-ttu-id="f6fe5-111">tooconfigure intégration d’Azure AD avec l’authentification unique Procore, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="f6fe5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6fe5-113">Un abonnement Procore SSO pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f6fe5-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6fe5-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6fe5-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6fe5-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f6fe5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6fe5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6fe5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f6fe5-118">Scenario description</span></span>
<span data-ttu-id="f6fe5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6fe5-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6fe5-121">Ajout de l’authentification unique Procore à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f6fe5-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="f6fe5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="f6fe5-123">Ajout de l’authentification unique Procore à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f6fe5-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="f6fe5-124">tooconfigure hello intégration de l’authentification unique Procore dans Azure AD, vous devez tooadd Procore de l’authentification unique à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6fe5-125">**tooadd Procore l’authentification unique à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6fe5-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6fe5-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6fe5-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6fe5-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f6fe5-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f6fe5-133">Dans la zone de recherche de hello, tapez **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-133">In hello search box, type **Procore SSO**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="f6fe5-135">Dans le volet de résultats hello, sélectionnez **SSO Procore**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6fe5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6fe5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Procore SSO avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f6fe5-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6fe5-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SSO Procore est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="f6fe5-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’authentification unique Procore hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="f6fe5-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Procore de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="f6fe5-142">tooconfigure et test Azure AD l’authentification unique avec l’authentification unique Procore, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6fe5-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6fe5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6fe5-145">**[Création d’un utilisateur de test de l’authentification unique Procore](#creating-a-procore-sso-test-user)**  -toohave de Britta Simon dans Procore l’authentification unique qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f6fe5-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6fe5-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6fe5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6fe5-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application SSO Procore.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="f6fe5-150">**tooconfigure Azure AD authentification unique avec l’authentification unique Procore, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6fe5-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6fe5-151">Dans le portail de gestion Azure hello, sur hello **SSO Procore** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f6fe5-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="f6fe5-155">Sur hello **Procore domaine d’authentification unique et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="f6fe5-157">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="f6fe5-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f6fe5-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6fe5-161">Sur hello **Procore Configuration SSO** , cliquez sur **configurer la SSO Procore** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f6fe5-162">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f6fe5-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="f6fe5-164">tooconfigure l’authentification unique sur **Procore SSO** côté, le site de société procore tooyour de connexion en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="f6fe5-165">Dans liste déroulante de boîte à outils hello vers le bas, cliquez sur **Admin** page des paramètres de l’authentification unique tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="f6fe5-167">Hello coller des valeurs dans les zones hello comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-167">Paste hello values in hello boxes as described below-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="f6fe5-169">a.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-169">a.</span></span> <span data-ttu-id="f6fe5-170">Bonjour **émetteur URL d’authentification unique** zone, collez hello ID d’entité SAML copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="f6fe5-171">b.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-171">b.</span></span> <span data-ttu-id="f6fe5-172">Bonjour **SAML cible URL de connexion de** zone, collez hello SAML Sign-On URL du Service unique provenant de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="f6fe5-173">c.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-173">c.</span></span> <span data-ttu-id="f6fe5-174">Ouvrez maintenant hello **Metadata XML** téléchargé au-dessus de hello portail Azure et de la copie du certificat de hello dans la balise hello nommée **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="f6fe5-175">Hello de coller copiées valeur hello **certificat Single Sign On x509** boîte.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="f6fe5-176">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="f6fe5-177">Après ces paramètres, vous avez besoin de toosend hello **nom de domaine** (par exemple **contoso.com**) à laquelle vous vous connectez à toohello Procore [équipe de Support Procore](https://support.procore.com/) et ils seront Activer l’authentification unique fédérée pour ce domaine.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6fe5-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6fe5-179">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f6fe5-181">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6fe5-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6fe5-182">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6fe5-184">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6fe5-186">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6fe5-188">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6fe5-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6fe5-190">a.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-190">a.</span></span> <span data-ttu-id="f6fe5-191">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6fe5-192">b.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-192">b.</span></span> <span data-ttu-id="f6fe5-193">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6fe5-194">c.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-194">c.</span></span> <span data-ttu-id="f6fe5-195">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6fe5-196">d.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-196">d.</span></span> <span data-ttu-id="f6fe5-197">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="f6fe5-198">Création d’un utilisateur de test Procore SSO</span><span class="sxs-lookup"><span data-stu-id="f6fe5-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="f6fe5-199">Veuillez suivre hello ci-dessous les étapes toocreate un utilisateur de test Procore sur son côté.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="f6fe5-200">Connexion tooyour procore site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="f6fe5-201">Dans liste déroulante de boîte à outils hello vers le bas, cliquez sur **répertoire** page de répertoire tooopen hello entreprise.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="f6fe5-203">Cliquez sur **ajouter une personne** formulaire de hello tooopen et entrez exécuter suivantes options -</span><span class="sxs-lookup"><span data-stu-id="f6fe5-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="f6fe5-205">a.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-205">a.</span></span> <span data-ttu-id="f6fe5-206">Bonjour **prénom** zone de texte, nom d’utilisateur de type comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="f6fe5-207">b.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-207">b.</span></span> <span data-ttu-id="f6fe5-208">Bonjour **nom** zone de texte, nom d’utilisateur de type comme **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="f6fe5-209">c.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-209">c.</span></span> <span data-ttu-id="f6fe5-210">Bonjour **adresse de messagerie** adresse de messagerie de l’utilisateur du type de zone de texte, comme  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f6fe5-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="f6fe5-211">d.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-211">d.</span></span> <span data-ttu-id="f6fe5-212">Sélectionnez **Modèle d’autorisation** pour **Appliquer le modèle d’autorisation plus tard**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="f6fe5-213">e.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-213">e.</span></span> <span data-ttu-id="f6fe5-214">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-214">Click **Create**.</span></span>

4. <span data-ttu-id="f6fe5-215">Vérifier et mettre à jour les détails de hello hello ajoutés récemment contact.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-215">Check and update hello details for hello newly added contact.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="f6fe5-217">Cliquez sur **enregistrer et envoyer une invitation** (si une invitation par courrier est requise) ou **enregistrer** (enregistrer directement) d’inscription des utilisateurs toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6fe5-219">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6fe5-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6fe5-220">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooProcore accès SSO.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f6fe5-222">**tooassign Britta Simon tooProcore SSO, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f6fe5-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6fe5-223">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f6fe5-225">Dans la liste des applications hello, sélectionnez **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="f6fe5-227">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f6fe5-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-229">Click **Add** button.</span></span> <span data-ttu-id="f6fe5-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f6fe5-232">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6fe5-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6fe5-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6fe5-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f6fe5-235">Testing single sign-on</span></span>

<span data-ttu-id="f6fe5-236">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f6fe5-237">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="f6fe5-238">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f6fe5-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="f6fe5-239">Lorsque vous cliquez sur mosaïque SSO Procore hello hello volet d’accès, vous devez obtenir l’application de l’authentification unique Procore tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="f6fe5-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6fe5-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f6fe5-240">Additional resources</span></span>

* [<span data-ttu-id="f6fe5-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6fe5-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6fe5-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f6fe5-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

