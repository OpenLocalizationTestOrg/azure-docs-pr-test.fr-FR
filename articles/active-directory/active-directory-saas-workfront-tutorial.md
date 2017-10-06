---
title: "Didacticiel : Intégration d’Azure Active Directory avec Workfront | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: e7249b9ec769f19cf5aa7d44ff6f58705df4020a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="eaeee-103">Didacticiel : Intégration d’Azure Active Directory avec Workfront</span><span class="sxs-lookup"><span data-stu-id="eaeee-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="eaeee-104">Dans ce didacticiel, vous apprendrez comment toointegrate Workfront avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eaeee-104">In this tutorial, you learn how toointegrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eaeee-105">Intégration Workfront à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="eaeee-105">Integrating Workfront with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eaeee-106">Vous pouvez contrôler dans Azure AD qui a accès tooWorkfront</span><span class="sxs-lookup"><span data-stu-id="eaeee-106">You can control in Azure AD who has access tooWorkfront</span></span>
- <span data-ttu-id="eaeee-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkfront (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-107">You can enable your users tooautomatically get signed-on tooWorkfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eaeee-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="eaeee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eaeee-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eaeee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eaeee-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eaeee-110">Prerequisites</span></span>

<span data-ttu-id="eaeee-111">tooconfigure intégration d’Azure AD avec Workfront, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eaeee-111">tooconfigure Azure AD integration with Workfront, you need hello following items:</span></span>

- <span data-ttu-id="eaeee-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eaeee-113">Un abonnement Workfront pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="eaeee-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eaeee-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="eaeee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eaeee-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="eaeee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eaeee-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eaeee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eaeee-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eaeee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eaeee-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="eaeee-118">Scenario description</span></span>
<span data-ttu-id="eaeee-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="eaeee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eaeee-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="eaeee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eaeee-121">Ajout de Workfront à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eaeee-121">Adding Workfront from hello gallery</span></span>
2. <span data-ttu-id="eaeee-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-hello-gallery"></a><span data-ttu-id="eaeee-123">Ajout de Workfront à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eaeee-123">Adding Workfront from hello gallery</span></span>
<span data-ttu-id="eaeee-124">intégration de hello tooconfigure de Workfront dans Azure AD, vous devez tooadd Workfront à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="eaeee-124">tooconfigure hello integration of Workfront into Azure AD, you need tooadd Workfront from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eaeee-125">**tooadd Workfront à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eaeee-125">**tooadd Workfront from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeee-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="eaeee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eaeee-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eaeee-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="eaeee-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eaeee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="eaeee-133">Dans la zone de recherche de hello, tapez **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-133">In hello search box, type **Workfront**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="eaeee-135">Dans le volet de résultats hello, sélectionnez **Workfront**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eaeee-135">In hello results panel, select **Workfront**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eaeee-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eaeee-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workfront, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="eaeee-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eaeee-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Workfront est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaeee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workfront is tooa user in Azure AD.</span></span> <span data-ttu-id="eaeee-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Workfront doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="eaeee-140">In other words, a link relationship between an Azure AD user and hello related user in Workfront needs toobe established.</span></span>

<span data-ttu-id="eaeee-141">Dans Workfront, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="eaeee-141">In Workfront, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eaeee-142">tooconfigure et test Azure AD l’authentification unique avec Workfront, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="eaeee-142">tooconfigure and test Azure AD single sign-on with Workfront, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eaeee-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="eaeee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eaeee-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eaeee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eaeee-145">**[Création d’un utilisateur de test Workfront](#creating-a-workfront-test-user)**  -toohave un équivalent de Britta Simon dans Workfront est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eaeee-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - toohave a counterpart of Britta Simon in Workfront that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eaeee-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eaeee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eaeee-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="eaeee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eaeee-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eaeee-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Workfront.</span><span class="sxs-lookup"><span data-stu-id="eaeee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="eaeee-150">**tooconfigure Azure AD single sign-on avec Workfront, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eaeee-150">**tooconfigure Azure AD single sign-on with Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeee-151">Bonjour portail Azure, sur hello **Workfront** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-151">In hello Azure portal, on hello **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="eaeee-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eaeee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="eaeee-155">Sur hello **Workfront domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eaeee-155">On hello **Workfront Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="eaeee-157">a.</span><span class="sxs-lookup"><span data-stu-id="eaeee-157">a.</span></span> <span data-ttu-id="eaeee-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="eaeee-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="eaeee-159">b.</span><span class="sxs-lookup"><span data-stu-id="eaeee-159">b.</span></span> <span data-ttu-id="eaeee-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="eaeee-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eaeee-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="eaeee-161">These values are not real.</span></span> <span data-ttu-id="eaeee-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="eaeee-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eaeee-163">Contact [équipe de support Client de Workfront](https://www.workfront.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="eaeee-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="eaeee-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eaeee-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="eaeee-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="eaeee-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eaeee-168">Sur hello **Workfront Configuration** , cliquez sur **Workfront de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="eaeee-168">On hello **Workfront Configuration** section, click **Configure Workfront** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eaeee-169">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="eaeee-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="eaeee-171">Site d’entreprise Workfront tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="eaeee-171">Sign-on tooyour Workfront company site as administrator.</span></span>

8. <span data-ttu-id="eaeee-172">Accédez trop**l’authentification unique sur la Configuration**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-172">Go too**Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="eaeee-173">Sur hello **Single Sign-On** boîte de dialogue, effectuer hello comme suit</span><span class="sxs-lookup"><span data-stu-id="eaeee-173">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
    
    ![Configurer l’authentification unique][23]
   
    <span data-ttu-id="eaeee-175">a.</span><span class="sxs-lookup"><span data-stu-id="eaeee-175">a.</span></span> <span data-ttu-id="eaeee-176">Comme **Type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="eaeee-177">b.</span><span class="sxs-lookup"><span data-stu-id="eaeee-177">b.</span></span> <span data-ttu-id="eaeee-178">Sélectionnez **///ID fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="eaeee-179">c.</span><span class="sxs-lookup"><span data-stu-id="eaeee-179">c.</span></span> <span data-ttu-id="eaeee-180">Hello de coller **SAML Sign-On URL du Service unique** dans hello **URL du portail de compte de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="eaeee-180">Paste hello **SAML Single Sign-On Service URL** into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="eaeee-181">d.</span><span class="sxs-lookup"><span data-stu-id="eaeee-181">d.</span></span> <span data-ttu-id="eaeee-182">Coller **URL de Service de déconnexion unique** dans hello **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="eaeee-182">Paste **Single Sign-Out Service URL** into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="eaeee-183">e.</span><span class="sxs-lookup"><span data-stu-id="eaeee-183">e.</span></span> <span data-ttu-id="eaeee-184">Coller **URL de modification du mot de passe** dans hello **URL de modification du mot de passe** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="eaeee-184">Paste **Change Password URL** into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="eaeee-185">f.</span><span class="sxs-lookup"><span data-stu-id="eaeee-185">f.</span></span> <span data-ttu-id="eaeee-186">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="eaeee-187">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="eaeee-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eaeee-188">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="eaeee-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eaeee-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eaeee-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eaeee-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="eaeee-191">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="eaeee-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="eaeee-193">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eaeee-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeee-194">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="eaeee-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eaeee-196">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eaeee-198">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="eaeee-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eaeee-200">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eaeee-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eaeee-202">a.</span><span class="sxs-lookup"><span data-stu-id="eaeee-202">a.</span></span> <span data-ttu-id="eaeee-203">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eaeee-204">b.</span><span class="sxs-lookup"><span data-stu-id="eaeee-204">b.</span></span> <span data-ttu-id="eaeee-205">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eaeee-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eaeee-206">c.</span><span class="sxs-lookup"><span data-stu-id="eaeee-206">c.</span></span> <span data-ttu-id="eaeee-207">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eaeee-208">d.</span><span class="sxs-lookup"><span data-stu-id="eaeee-208">d.</span></span> <span data-ttu-id="eaeee-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="eaeee-210">Création d’un utilisateur de test Workfront</span><span class="sxs-lookup"><span data-stu-id="eaeee-210">Creating a Workfront test user</span></span>

<span data-ttu-id="eaeee-211">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Workfront.</span><span class="sxs-lookup"><span data-stu-id="eaeee-211">hello objective of this section is toocreate a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="eaeee-212">**toocreate un utilisateur appelé Britta Simon dans Workfront, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eaeee-212">**toocreate a user called Britta Simon in Workfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeee-213">Se connecter tooyour Workfront site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="eaeee-213">Sign on tooyour Workfront company site as administrator.</span></span>
2. <span data-ttu-id="eaeee-214">Dans le menu hello haut de hello, cliquez sur **personnes**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-214">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="eaeee-215">Cliquez sur **New Person**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="eaeee-216">Dans la boîte de dialogue nouvelle personne hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eaeee-216">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Créer un utilisateur de test Workfront][21] 
   
    <span data-ttu-id="eaeee-218">a.</span><span class="sxs-lookup"><span data-stu-id="eaeee-218">a.</span></span> <span data-ttu-id="eaeee-219">Bonjour **prénom** zone de texte, tapez « Brian ».</span><span class="sxs-lookup"><span data-stu-id="eaeee-219">In hello **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="eaeee-220">b.</span><span class="sxs-lookup"><span data-stu-id="eaeee-220">b.</span></span> <span data-ttu-id="eaeee-221">Bonjour **nom** zone de texte, tapez « Simon ».</span><span class="sxs-lookup"><span data-stu-id="eaeee-221">In hello **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="eaeee-222">c.</span><span class="sxs-lookup"><span data-stu-id="eaeee-222">c.</span></span> <span data-ttu-id="eaeee-223">Bonjour **adresse de messagerie** zone de texte, tapez l’adresse de messagerie Britta Simon dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eaeee-223">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="eaeee-224">d.</span><span class="sxs-lookup"><span data-stu-id="eaeee-224">d.</span></span> <span data-ttu-id="eaeee-225">Cliquez sur **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-225">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eaeee-226">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaeee-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eaeee-227">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWorkfront.</span><span class="sxs-lookup"><span data-stu-id="eaeee-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkfront.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="eaeee-229">**tooassign Britta Simon tooWorkfront, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eaeee-229">**tooassign Britta Simon tooWorkfront, perform hello following steps:**</span></span>

1. <span data-ttu-id="eaeee-230">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="eaeee-232">Dans la liste des applications hello, sélectionnez **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-232">In hello applications list, select **Workfront**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="eaeee-234">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="eaeee-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-236">Click **Add** button.</span></span> <span data-ttu-id="eaeee-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="eaeee-239">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="eaeee-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eaeee-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eaeee-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eaeee-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eaeee-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eaeee-242">Testing single sign-on</span></span>

<span data-ttu-id="eaeee-243">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="eaeee-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eaeee-244">Lorsque vous cliquez sur mosaïque Workfront hello hello volet d’accès, vous devez obtenir la page de connexion de l’application de Workfront.</span><span class="sxs-lookup"><span data-stu-id="eaeee-244">When you click hello Workfront tile in hello Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="eaeee-245">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eaeee-245">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eaeee-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eaeee-246">Additional resources</span></span>

* [<span data-ttu-id="eaeee-247">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eaeee-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eaeee-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="eaeee-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

