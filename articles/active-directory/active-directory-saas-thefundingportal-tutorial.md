---
title: "Didacticiel : Intégration d’Azure Active Directory avec hello financement de portail | Documents Microsoft"
description: "Découvrez comment tooconfigure sur l’authentification unique entre Azure Active Directory et hello financement de portail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="0fa47-103">Didacticiel : Intégration d’Azure Active Directory avec hello financement de portail</span><span class="sxs-lookup"><span data-stu-id="0fa47-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="0fa47-104">Dans ce didacticiel, vous découvrez comment toointegrate hello financement de portail avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fa47-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fa47-105">Intégration hello financement portail avec Azure AD fournit hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0fa47-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0fa47-106">Vous pouvez contrôler dans Azure AD qui a accès toohello financement portail</span><span class="sxs-lookup"><span data-stu-id="0fa47-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="0fa47-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté toohello portail financement (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fa47-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0fa47-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0fa47-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fa47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa47-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0fa47-110">Prerequisites</span></span>

<span data-ttu-id="0fa47-111">intégration de tooconfigure Azure AD à hello Portal de financement, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0fa47-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="0fa47-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fa47-113">Abonnement un Bonjour financement de portail l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0fa47-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fa47-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0fa47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fa47-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="0fa47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fa47-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0fa47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fa47-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fa47-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fa47-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0fa47-118">Scenario description</span></span>
<span data-ttu-id="0fa47-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0fa47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fa47-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="0fa47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fa47-121">Ajout de hello portail financement à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0fa47-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="0fa47-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="0fa47-123">Ajout de hello portail financement à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0fa47-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="0fa47-124">intégration de hello tooconfigure Hello financement Portal dans Azure AD, vous devez tooadd hello portail financement à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0fa47-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0fa47-125">**tooadd hello financement de portail à partir de la galerie de hello, procédez de hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fa47-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fa47-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0fa47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fa47-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0fa47-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0fa47-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0fa47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0fa47-133">Dans la zone de recherche de hello, tapez **hello financement de portail**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="0fa47-135">Dans le volet de résultats hello, sélectionnez **hello financement de portail**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0fa47-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fa47-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fa47-138">Dans cette section, vous configurez et testez Azure AD single sign-on avec hello que financement de portail basé sur un utilisateur de test appelé « Brian Simon ».</span><span class="sxs-lookup"><span data-stu-id="0fa47-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0fa47-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello Bonjour financement de portail est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fa47-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="0fa47-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello Bonjour financement de portail doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="0fa47-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="0fa47-141">Dans l’hello Portal de financement, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0fa47-142">tooconfigure et test Azure AD l’authentification unique avec hello Portal de financement, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="0fa47-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0fa47-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0fa47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0fa47-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0fa47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fa47-145">**[Création de l’utilisateur test de hello financement de portail](#creating-the-funding-portal-test-user)**  -toohave de Britta Simon contrepartie Bonjour portail financement qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0fa47-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fa47-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0fa47-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fa47-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="0fa47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fa47-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fa47-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de portail de financement hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="0fa47-150">**tooconfigure Azure AD single sign-on avec hello financement de portail, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fa47-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fa47-151">Bonjour portail Azure, sur hello **hello financement de portail** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0fa47-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0fa47-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="0fa47-155">Sur hello **hello financement de domaine de portail et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fa47-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="0fa47-157">a.</span><span class="sxs-lookup"><span data-stu-id="0fa47-157">a.</span></span> <span data-ttu-id="0fa47-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="0fa47-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="0fa47-159">b.</span><span class="sxs-lookup"><span data-stu-id="0fa47-159">b.</span></span> <span data-ttu-id="0fa47-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="0fa47-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0fa47-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="0fa47-161">These values are not real.</span></span> <span data-ttu-id="0fa47-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="0fa47-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0fa47-163">Contact [hello équipe de support Client de Portal financement](mailto:info@regenteducation.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0fa47-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="0fa47-164">application de portail de financement de Hello attend hello SAML assertions toocontain un attribut nommé « externalId1 ».</span><span class="sxs-lookup"><span data-stu-id="0fa47-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="0fa47-165">valeur de Hello de « externalId1 » doit être un studentID reconnue.</span><span class="sxs-lookup"><span data-stu-id="0fa47-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="0fa47-166">Configurer la revendication hello « externalId1 » pour cette application.</span><span class="sxs-lookup"><span data-stu-id="0fa47-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="0fa47-167">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="0fa47-168">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="0fa47-168">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="0fa47-170">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fa47-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="0fa47-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="0fa47-171">Attribute Name</span></span> | <span data-ttu-id="0fa47-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="0fa47-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="0fa47-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="0fa47-173">externalId1</span></span> | <span data-ttu-id="0fa47-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="0fa47-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="0fa47-175">a.</span><span class="sxs-lookup"><span data-stu-id="0fa47-175">a.</span></span> <span data-ttu-id="0fa47-176">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0fa47-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0fa47-179">b.</span><span class="sxs-lookup"><span data-stu-id="0fa47-179">b.</span></span> <span data-ttu-id="0fa47-180">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="0fa47-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0fa47-181">c.</span><span class="sxs-lookup"><span data-stu-id="0fa47-181">c.</span></span> <span data-ttu-id="0fa47-182">À partir de hello **valeur d’attribut** liste, sélectionnez hello attribut toouse pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="0fa47-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="0fa47-183">Par exemple, si vous avez stocké hello StudentID valeur Bonjour ExtensionAttribute1, puis sélectionnez user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="0fa47-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="0fa47-184">d.</span><span class="sxs-lookup"><span data-stu-id="0fa47-184">d.</span></span> <span data-ttu-id="0fa47-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="0fa47-186">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0fa47-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="0fa47-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0fa47-188">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0fa47-190">tooconfigure l’authentification unique sur **hello financement de portail** côté, vous devez hello toosend téléchargé **Metadata XML** trop[hello équipe de support Portal de financement](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="0fa47-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="0fa47-191">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="0fa47-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0fa47-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="0fa47-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0fa47-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0fa47-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0fa47-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fa47-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fa47-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="0fa47-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0fa47-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fa47-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fa47-199">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0fa47-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fa47-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fa47-203">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fa47-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0fa47-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fa47-207">a.</span><span class="sxs-lookup"><span data-stu-id="0fa47-207">a.</span></span> <span data-ttu-id="0fa47-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fa47-209">b.</span><span class="sxs-lookup"><span data-stu-id="0fa47-209">b.</span></span> <span data-ttu-id="0fa47-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0fa47-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fa47-211">c.</span><span class="sxs-lookup"><span data-stu-id="0fa47-211">c.</span></span> <span data-ttu-id="0fa47-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0fa47-213">d.</span><span class="sxs-lookup"><span data-stu-id="0fa47-213">d.</span></span> <span data-ttu-id="0fa47-214">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="0fa47-215">Création d’utilisateur de test du portail de financement hello</span><span class="sxs-lookup"><span data-stu-id="0fa47-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="0fa47-216">Dans cette section, vous créez un utilisateur appelé Britta Simon Bonjour financement Portal.</span><span class="sxs-lookup"><span data-stu-id="0fa47-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="0fa47-217">Travailler avec [hello équipe de support Portal de financement](mailto:info@regenteducation.com) tooadd hello utilisateur de test et activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0fa47-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0fa47-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fa47-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0fa47-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès toohello financement Portal.</span><span class="sxs-lookup"><span data-stu-id="0fa47-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0fa47-221">**tooassign Britta Simon toohello Portal de financement, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0fa47-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fa47-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0fa47-224">Dans la liste des applications hello, sélectionnez **hello financement de portail**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="0fa47-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0fa47-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-228">Click **Add** button.</span></span> <span data-ttu-id="0fa47-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0fa47-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0fa47-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fa47-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0fa47-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fa47-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0fa47-234">Testing single sign-on</span></span>

<span data-ttu-id="0fa47-235">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="0fa47-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0fa47-236">Lorsque vous cliquez sur mosaïque de financement de portail hello hello Bonjour volet d’accès, vous devez obtenir l’application de portail de financement automatiquement signé sur tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="0fa47-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fa47-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0fa47-237">Additional resources</span></span>

* [<span data-ttu-id="0fa47-238">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fa47-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fa47-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0fa47-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

