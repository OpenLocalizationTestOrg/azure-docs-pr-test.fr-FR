---
title: "Didacticiel : Intégration d’Azure Active Directory à 123ContactForm | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="5c266-103">Didacticiel : Intégration d’Azure Active Directory à 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="5c266-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="5c266-104">Dans ce didacticiel, vous apprendrez comment 123ContactForm toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c266-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c266-105">Intégration 123ContactForm à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5c266-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c266-106">Vous pouvez contrôler dans Azure AD qui a accès too123ContactForm</span><span class="sxs-lookup"><span data-stu-id="5c266-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="5c266-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté too123ContactForm (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c266-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5c266-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c266-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c266-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c266-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5c266-110">Prerequisites</span></span>

<span data-ttu-id="5c266-111">tooconfigure intégration d’Azure AD avec 123ContactForm, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5c266-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="5c266-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c266-113">Un abonnement 123ContactForm pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5c266-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c266-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5c266-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c266-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5c266-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c266-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5c266-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c266-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c266-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c266-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5c266-118">Scenario description</span></span>
<span data-ttu-id="5c266-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5c266-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c266-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5c266-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c266-121">Ajout de 123ContactForm à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5c266-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="5c266-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="5c266-123">Ajout de 123ContactForm à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5c266-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="5c266-124">intégration de hello tooconfigure de 123ContactForm dans Azure AD, vous devez 123ContactForm tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5c266-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c266-125">**123ContactForm tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c266-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c266-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5c266-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c266-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5c266-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c266-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c266-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5c266-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5c266-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5c266-133">Dans la zone de recherche de hello, tapez **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="5c266-133">In hello search box, type **123ContactForm**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="5c266-135">Dans le volet de résultats hello, sélectionnez **123ContactForm**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5c266-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c266-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c266-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec 123ContactForm pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5c266-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c266-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans 123ContactForm est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c266-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="5c266-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans 123ContactForm doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5c266-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="5c266-141">Dans 123ContactForm, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5c266-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5c266-142">tooconfigure et test Azure AD l’authentification unique avec 123ContactForm, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5c266-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c266-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5c266-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c266-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c266-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c266-145">**[Création d’un utilisateur de test 123ContactForm](#creating-a-123contactform-test-user)**  -toohave un homologue de Britta Simon dans 123ContactForm est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5c266-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c266-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c266-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c266-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5c266-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c266-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c266-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="5c266-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="5c266-150">**tooconfigure Azure AD single sign-on avec 123ContactForm, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c266-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c266-151">Bonjour portail Azure, sur hello **123ContactForm** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5c266-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5c266-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c266-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="5c266-155">Sur hello **123ContactForm domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c266-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="5c266-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c266-157">a.</span></span> <span data-ttu-id="5c266-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="5c266-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="5c266-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c266-159">b.</span></span> <span data-ttu-id="5c266-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="5c266-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="5c266-161">Si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c266-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="5c266-163">a.</span><span class="sxs-lookup"><span data-stu-id="5c266-163">a.</span></span> <span data-ttu-id="5c266-164">Cliquez sur hello **afficher les paramètres d’URL avancés** option</span><span class="sxs-lookup"><span data-stu-id="5c266-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="5c266-165">b.</span><span class="sxs-lookup"><span data-stu-id="5c266-165">b.</span></span> <span data-ttu-id="5c266-166">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="5c266-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c266-167">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5c266-167">These values are not real.</span></span> <span data-ttu-id="5c266-168">Vous devez tooupdate ces valeur réelle URL et identificateur qui est expliquée plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="5c266-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="5c266-169">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5c266-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="5c266-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5c266-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5c266-173">tooconfigure l’authentification unique sur **123ContactForm** côté, accédez trop[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c266-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="5c266-175">a.</span><span class="sxs-lookup"><span data-stu-id="5c266-175">a.</span></span> <span data-ttu-id="5c266-176">Bonjour **messagerie** zone de texte, par courrier électronique de type hello de hello, utilisateur ex :</span><span class="sxs-lookup"><span data-stu-id="5c266-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="5c266-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="5c266-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="5c266-178">b.</span><span class="sxs-lookup"><span data-stu-id="5c266-178">b.</span></span> <span data-ttu-id="5c266-179">Cliquez sur **télécharger** et parcourir hello fichier XML de Metadata, que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c266-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="5c266-180">c.</span><span class="sxs-lookup"><span data-stu-id="5c266-180">c.</span></span> <span data-ttu-id="5c266-181">Cliquez sur **Envoyer le formulaire**.</span><span class="sxs-lookup"><span data-stu-id="5c266-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="5c266-182">Sur hello **Microsoft Azure AD l’authentification unique sur - Configurer les paramètres application** effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c266-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="5c266-184">a.</span><span class="sxs-lookup"><span data-stu-id="5c266-184">a.</span></span> <span data-ttu-id="5c266-185">Si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, hello de copie **identificateur** pour votre instance de valeur et le coller dans **identificateur** zone de texte dans **123ContactForm domaine et les URL** section sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c266-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="5c266-186">b.</span><span class="sxs-lookup"><span data-stu-id="5c266-186">b.</span></span> <span data-ttu-id="5c266-187">Si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, hello de copie **URL de réponse** pour votre instance de valeur et le coller dans **URL de réponse** zone de texte dans **123ContactForm domaine et les URL** section sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c266-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="5c266-188">c.</span><span class="sxs-lookup"><span data-stu-id="5c266-188">c.</span></span> <span data-ttu-id="5c266-189">Si vous le souhaitez application hello tooconfigure **mode initiée par SP**, hello de copie **URL de connexion** pour votre instance de valeur et le coller dans **URL de connexion** zone de texte dans **123ContactForm domaine et les URL** section sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c266-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="5c266-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5c266-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c266-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5c266-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c266-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c266-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c266-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c266-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5c266-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5c266-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c266-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c266-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5c266-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c266-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5c266-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c266-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5c266-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c266-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c266-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c266-205">a.</span><span class="sxs-lookup"><span data-stu-id="5c266-205">a.</span></span> <span data-ttu-id="5c266-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c266-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c266-207">b.</span><span class="sxs-lookup"><span data-stu-id="5c266-207">b.</span></span> <span data-ttu-id="5c266-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c266-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c266-209">c.</span><span class="sxs-lookup"><span data-stu-id="5c266-209">c.</span></span> <span data-ttu-id="5c266-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5c266-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c266-211">d.</span><span class="sxs-lookup"><span data-stu-id="5c266-211">d.</span></span> <span data-ttu-id="5c266-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c266-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="5c266-213">Création d’un utilisateur de test 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="5c266-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="5c266-214">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5c266-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c266-215">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c266-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c266-216">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès too123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="5c266-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5c266-218">**tooassign Britta Simon too123ContactForm, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c266-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c266-219">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c266-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5c266-221">Dans la liste des applications hello, sélectionnez **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="5c266-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="5c266-223">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c266-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5c266-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c266-225">Click **Add** button.</span></span> <span data-ttu-id="5c266-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c266-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5c266-228">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5c266-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c266-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c266-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c266-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c266-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c266-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5c266-231">Testing single sign-on</span></span>

<span data-ttu-id="5c266-232">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5c266-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c266-233">Lorsque vous cliquez sur mosaïque 123ContactForm hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour 123ContactForm application.</span><span class="sxs-lookup"><span data-stu-id="5c266-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="5c266-234">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c266-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c266-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5c266-235">Additional resources</span></span>

* [<span data-ttu-id="5c266-236">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c266-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c266-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5c266-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

