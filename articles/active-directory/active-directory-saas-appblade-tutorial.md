---
title: "Didacticiel : Intégration d’Azure Active Directory à AppBlade | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="472da-103">Didacticiel : Intégration d’Azure Active Directory à AppBlade</span><span class="sxs-lookup"><span data-stu-id="472da-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="472da-104">Dans ce didacticiel, vous apprendrez comment toointegrate AppBlade avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="472da-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="472da-105">Intégration AppBlade à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="472da-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="472da-106">Vous pouvez contrôler dans Azure AD qui a accès tooAppBlade</span><span class="sxs-lookup"><span data-stu-id="472da-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="472da-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAppBlade (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="472da-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="472da-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="472da-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="472da-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="472da-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="472da-110">Prerequisites</span></span>

<span data-ttu-id="472da-111">tooconfigure intégration d’Azure AD avec AppBlade, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="472da-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="472da-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="472da-113">Un abonnement AppBlade pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="472da-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="472da-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="472da-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="472da-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="472da-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="472da-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="472da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="472da-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="472da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="472da-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="472da-118">Scenario description</span></span>
<span data-ttu-id="472da-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="472da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="472da-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="472da-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="472da-121">Ajout de AppBlade à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="472da-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="472da-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="472da-123">Ajout de AppBlade à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="472da-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="472da-124">intégration de hello tooconfigure de AppBlade dans Azure AD, vous devez tooadd AppBlade à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="472da-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="472da-125">**tooadd AppBlade à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="472da-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="472da-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="472da-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="472da-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="472da-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="472da-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="472da-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="472da-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="472da-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="472da-133">Dans la zone de recherche de hello, tapez **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="472da-133">In hello search box, type **AppBlade**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="472da-135">Dans le volet de résultats hello, sélectionnez **AppBlade**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="472da-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="472da-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="472da-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec AppBlade au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="472da-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="472da-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans AppBlade est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="472da-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="472da-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans AppBlade doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="472da-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="472da-141">Dans AppBlade, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="472da-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="472da-142">tooconfigure et test Azure AD l’authentification unique avec AppBlade, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="472da-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="472da-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="472da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="472da-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="472da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="472da-145">**[Création d’un utilisateur de test AppBlade](#creating-an-appblade-test-user)**  -toohave un équivalent de Britta Simon dans AppBlade est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="472da-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="472da-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="472da-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="472da-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="472da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="472da-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="472da-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application AppBlade.</span><span class="sxs-lookup"><span data-stu-id="472da-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="472da-150">**tooconfigure Azure AD single sign-on avec AppBlade, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="472da-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="472da-151">Bonjour portail Azure, sur hello **AppBlade** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="472da-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="472da-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="472da-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="472da-155">Sur hello **AppBlade domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="472da-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="472da-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="472da-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="472da-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="472da-158">This value is not real.</span></span> <span data-ttu-id="472da-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="472da-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="472da-160">Contact [équipe de support Client de AppBlade](mailto:support@appblade.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="472da-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="472da-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="472da-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="472da-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="472da-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="472da-165">tooconfigure l’authentification unique sur **AppBlade** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="472da-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="472da-166">En outre, demandez-lui de tooconfigure hello **URL de l’émetteur SSO** comme `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="472da-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="472da-167">Ce paramètre est requis pour toowork de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="472da-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="472da-168">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="472da-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="472da-169">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="472da-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="472da-170">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="472da-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="472da-171">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="472da-172">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="472da-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="472da-174">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="472da-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="472da-175">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="472da-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="472da-177">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="472da-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="472da-179">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="472da-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="472da-181">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="472da-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="472da-183">a.</span><span class="sxs-lookup"><span data-stu-id="472da-183">a.</span></span> <span data-ttu-id="472da-184">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="472da-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="472da-185">b.</span><span class="sxs-lookup"><span data-stu-id="472da-185">b.</span></span> <span data-ttu-id="472da-186">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="472da-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="472da-187">c.</span><span class="sxs-lookup"><span data-stu-id="472da-187">c.</span></span> <span data-ttu-id="472da-188">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="472da-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="472da-189">d.</span><span class="sxs-lookup"><span data-stu-id="472da-189">d.</span></span> <span data-ttu-id="472da-190">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="472da-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="472da-191">Création d’un utilisateur de test AppBlade</span><span class="sxs-lookup"><span data-stu-id="472da-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="472da-192">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans AppBlade.</span><span class="sxs-lookup"><span data-stu-id="472da-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="472da-193">AppBlade prend en charge l'approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="472da-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="472da-194">**Vérifiez que votre nom de domaine a été correctement configuré avec AppBlade pour l’approvisionnement des utilisateurs. Après ce seul hello juste-à-temps utilisateur fonctionne de la configuration.**</span><span class="sxs-lookup"><span data-stu-id="472da-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="472da-195">Si l’utilisateur de hello possède une adresse de messagerie se terminant par domaine hello configuré par AppBlade pour votre compte, puis de l’utilisateur de hello joint automatiquement les compte hello en tant que membre avec le niveau d’autorisation hello que vous spécifiez, ce qui est un des « De base » (un utilisateur de base qui ne peut être installé les applications), « Membre » (un utilisateur peut télécharger les nouvelles versions d’application et gérer des projets), ou « Administrateur » (compte de toohello des privilèges administrateur complet).</span><span class="sxs-lookup"><span data-stu-id="472da-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="472da-196">Normalement un serait choisissez Basic et puis promouvoir les utilisateurs manuellement via une connexion Admin (AppBlade doit tooconfigure une connexion administrateur de courrier électronique à l’avance ou promouvoir un utilisateur pour le compte du client de hello après la connexion).</span><span class="sxs-lookup"><span data-stu-id="472da-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="472da-197">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="472da-197">There is no action item for you in this section.</span></span> <span data-ttu-id="472da-198">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess AppBlade s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="472da-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="472da-199">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="472da-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="472da-200">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="472da-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="472da-201">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAppBlade.</span><span class="sxs-lookup"><span data-stu-id="472da-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="472da-203">**tooassign Britta Simon tooAppBlade, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="472da-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="472da-204">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="472da-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="472da-206">Dans la liste des applications hello, sélectionnez **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="472da-206">In hello applications list, select **AppBlade**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="472da-208">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="472da-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="472da-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="472da-210">Click **Add** button.</span></span> <span data-ttu-id="472da-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="472da-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="472da-213">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="472da-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="472da-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="472da-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="472da-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="472da-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="472da-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="472da-216">Testing single sign-on</span></span>

<span data-ttu-id="472da-217">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="472da-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="472da-218">Lorsque vous cliquez sur mosaïque AppBlade hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour AppBlade application.</span><span class="sxs-lookup"><span data-stu-id="472da-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="472da-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="472da-219">Additional resources</span></span>

* [<span data-ttu-id="472da-220">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="472da-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="472da-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="472da-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

