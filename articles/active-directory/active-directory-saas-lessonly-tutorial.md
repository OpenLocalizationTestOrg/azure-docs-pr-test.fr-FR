---
title: "Didacticiel : Intégration d’Azure Active Directory à Lesson.ly | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="e888e-103">Didacticiel : Intégration d’Azure Active Directory à Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="e888e-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="e888e-104">Dans ce didacticiel, vous apprendrez comment toointegrate Lesson.ly avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e888e-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e888e-105">Intégration Lesson.ly à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e888e-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e888e-106">Vous pouvez contrôler dans Azure AD qui a accès tooLesson.ly</span><span class="sxs-lookup"><span data-stu-id="e888e-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="e888e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLesson.ly (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e888e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e888e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e888e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e888e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e888e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e888e-110">Prerequisites</span></span>

<span data-ttu-id="e888e-111">tooconfigure intégration d’Azure AD avec Lesson.ly, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e888e-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="e888e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e888e-113">Un abonnement Lesson.ly pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e888e-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e888e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e888e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e888e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e888e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e888e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e888e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e888e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e888e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e888e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e888e-118">Scenario description</span></span>
<span data-ttu-id="e888e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e888e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e888e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e888e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e888e-121">Ajout de Lesson.ly à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e888e-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="e888e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="e888e-123">Ajout de Lesson.ly à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e888e-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="e888e-124">intégration de hello tooconfigure de Lesson.ly dans Azure AD, vous devez tooadd Lesson.ly à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e888e-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e888e-125">**tooadd Lesson.ly à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e888e-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e888e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e888e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e888e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e888e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e888e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e888e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e888e-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e888e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e888e-133">Dans la zone de recherche de hello, tapez **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="e888e-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="e888e-135">Dans le volet de résultats hello, sélectionnez **Lesson.ly**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e888e-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e888e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e888e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lesson.ly, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e888e-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e888e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Lesson.ly est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e888e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="e888e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Lesson.ly doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e888e-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="e888e-141">Dans Lesson.ly, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e888e-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e888e-142">tooconfigure et test Azure AD l’authentification unique avec Lesson.ly, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e888e-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e888e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e888e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e888e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e888e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e888e-145">**[Création d’un utilisateur de test Lesson.ly](#creating-a-lessonly-test-user)**  -toohave un équivalent de Britta Simon dans Lesson.ly est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e888e-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e888e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e888e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e888e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e888e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e888e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e888e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="e888e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="e888e-150">**tooconfigure Azure AD single sign-on avec Lesson.ly, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e888e-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="e888e-151">Bonjour portail Azure, sur hello **Lesson.ly** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e888e-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e888e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e888e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="e888e-155">Sur hello **Lesson.ly domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e888e-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="e888e-157">a.</span><span class="sxs-lookup"><span data-stu-id="e888e-157">a.</span></span> <span data-ttu-id="e888e-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="e888e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="e888e-159">Lors de la référence d’un type générique nom qui **companyname** doit toobe remplacé par le nom réel.</span><span class="sxs-lookup"><span data-stu-id="e888e-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="e888e-160">b.</span><span class="sxs-lookup"><span data-stu-id="e888e-160">b.</span></span> <span data-ttu-id="e888e-161">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="e888e-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="e888e-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e888e-162">These values are not real.</span></span> <span data-ttu-id="e888e-163">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="e888e-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e888e-164">Contact [équipe de support Client de Lesson.ly](mailto:dev@lessonly.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e888e-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="e888e-165">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e888e-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="e888e-167">Hello Lesson.ly application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton SAML** configuration.hello suivant capture d’écran montre un exemple de Cette barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="e888e-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="e888e-169">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans hello précédant l’image et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e888e-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="e888e-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="e888e-170">Attribute Name</span></span>   | <span data-ttu-id="e888e-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="e888e-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="e888e-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="e888e-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="e888e-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e888e-173">user.givenname</span></span> |
    | <span data-ttu-id="e888e-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="e888e-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="e888e-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="e888e-175">user.surname</span></span> |
    | <span data-ttu-id="e888e-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="e888e-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="e888e-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="e888e-177">user.mail</span></span> |

    <span data-ttu-id="e888e-178">a.</span><span class="sxs-lookup"><span data-stu-id="e888e-178">a.</span></span> <span data-ttu-id="e888e-179">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e888e-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e888e-182">b.</span><span class="sxs-lookup"><span data-stu-id="e888e-182">b.</span></span> <span data-ttu-id="e888e-183">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="e888e-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e888e-184">c.</span><span class="sxs-lookup"><span data-stu-id="e888e-184">c.</span></span> <span data-ttu-id="e888e-185">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="e888e-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e888e-186">d.</span><span class="sxs-lookup"><span data-stu-id="e888e-186">d.</span></span> <span data-ttu-id="e888e-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e888e-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="e888e-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e888e-188">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e888e-190">Sur hello **Lesson.ly Configuration** , cliquez sur **Lesson.ly de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e888e-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e888e-191">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e888e-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="e888e-193">tooconfigure l’authentification unique sur **Lesson.ly** côté, vous devez hello toosend téléchargé **Certificate(Base64)** et **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="e888e-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="e888e-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e888e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e888e-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e888e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e888e-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e888e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e888e-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e888e-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e888e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e888e-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e888e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e888e-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e888e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e888e-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e888e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e888e-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e888e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e888e-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e888e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e888e-209">a.</span><span class="sxs-lookup"><span data-stu-id="e888e-209">a.</span></span> <span data-ttu-id="e888e-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e888e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e888e-211">b.</span><span class="sxs-lookup"><span data-stu-id="e888e-211">b.</span></span> <span data-ttu-id="e888e-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e888e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e888e-213">c.</span><span class="sxs-lookup"><span data-stu-id="e888e-213">c.</span></span> <span data-ttu-id="e888e-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e888e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e888e-215">d.</span><span class="sxs-lookup"><span data-stu-id="e888e-215">d.</span></span> <span data-ttu-id="e888e-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e888e-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="e888e-217">Création d’un utilisateur de test Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="e888e-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="e888e-218">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="e888e-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="e888e-219">Lesson.ly. prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="e888e-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e888e-220">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="e888e-220">There is no action item for you in this section.</span></span> <span data-ttu-id="e888e-221">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Lesson.ly s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="e888e-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="e888e-222">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="e888e-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e888e-223">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e888e-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e888e-224">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLesson.ly.</span><span class="sxs-lookup"><span data-stu-id="e888e-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e888e-226">**tooassign Britta Simon tooLesson.ly, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e888e-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="e888e-227">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e888e-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e888e-229">Dans la liste des applications hello, sélectionnez **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="e888e-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="e888e-231">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e888e-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e888e-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e888e-233">Click **Add** button.</span></span> <span data-ttu-id="e888e-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e888e-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e888e-236">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e888e-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e888e-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e888e-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e888e-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e888e-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e888e-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e888e-239">Testing single sign-on</span></span>

<span data-ttu-id="e888e-240">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e888e-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e888e-241">Lorsque vous cliquez sur mosaïque Lesson.ly hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Lesson.ly application.</span><span class="sxs-lookup"><span data-stu-id="e888e-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e888e-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e888e-242">Additional resources</span></span>

* [<span data-ttu-id="e888e-243">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e888e-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e888e-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e888e-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

