---
title: "Didacticiel : Intégration d’Azure Active Directory à Wingspan eTMF | Microsoft Azure"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Wingspan eTMF."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: ed5fda5318a0d3841af8b2db4fb74db550befaea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="65615-103">Didacticiel : Intégration d’Azure Active Directory à Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="65615-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="65615-104">Dans ce didacticiel, vous apprendrez comment eTMF de Wingspan toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65615-104">In this tutorial, you learn how toointegrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65615-105">Intégration Wingspan eTMF à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="65615-105">Integrating Wingspan eTMF with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65615-106">Vous pouvez contrôler dans Azure AD qui a accès tooWingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="65615-106">You can control in Azure AD who has access tooWingspan eTMF</span></span>
- <span data-ttu-id="65615-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWingspan eTMF (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-107">You can enable your users tooautomatically get signed-on tooWingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65615-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="65615-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65615-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65615-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65615-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="65615-110">Prerequisites</span></span>

<span data-ttu-id="65615-111">intégration d’Azure AD avec Wingspan eTMF de tooconfigure, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="65615-111">tooconfigure Azure AD integration with Wingspan eTMF, you need hello following items:</span></span>

- <span data-ttu-id="65615-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65615-113">Un abonnement Wingspan eTMF pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="65615-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65615-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="65615-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65615-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="65615-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65615-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="65615-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65615-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65615-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65615-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="65615-118">Scenario description</span></span>
<span data-ttu-id="65615-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="65615-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65615-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="65615-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65615-121">Ajout de Wingspan eTMF à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="65615-121">Adding Wingspan eTMF from hello gallery</span></span>
2. <span data-ttu-id="65615-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-hello-gallery"></a><span data-ttu-id="65615-123">Ajout de Wingspan eTMF à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="65615-123">Adding Wingspan eTMF from hello gallery</span></span>
<span data-ttu-id="65615-124">intégration de hello tooconfigure de Wingspan eTMF dans Azure AD, vous devez eTMF de Wingspan tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="65615-124">tooconfigure hello integration of Wingspan eTMF into Azure AD, you need tooadd Wingspan eTMF from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65615-125">**eTMF de Wingspan tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65615-125">**tooadd Wingspan eTMF from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65615-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="65615-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65615-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="65615-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65615-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="65615-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="65615-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="65615-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="65615-133">Dans la zone de recherche de hello, tapez **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="65615-133">In hello search box, type **Wingspan eTMF**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="65615-135">Dans le volet de résultats hello, sélectionnez **Wingspan eTMF**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="65615-135">In hello results panel, select **Wingspan eTMF**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65615-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65615-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec Wingspan eTMF, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="65615-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65615-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Wingspan eTMF est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65615-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wingspan eTMF is tooa user in Azure AD.</span></span> <span data-ttu-id="65615-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Wingspan eTMF doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="65615-140">In other words, a link relationship between an Azure AD user and hello related user in Wingspan eTMF needs toobe established.</span></span>

<span data-ttu-id="65615-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="65615-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="65615-142">tooconfigure et test Azure AD l’authentification unique avec Wingspan eTMF, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="65615-142">tooconfigure and test Azure AD single sign-on with Wingspan eTMF, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65615-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="65615-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65615-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65615-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65615-145">**[Création d’un utilisateur de test eTMF Wingspan](#creating-a-wingspan-etmf-test-user)**  -toohave un homologue de Britta Simon dans eTMF Wingspan qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="65615-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - toohave a counterpart of Britta Simon in Wingspan eTMF that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65615-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="65615-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65615-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="65615-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65615-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65615-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="65615-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="65615-150">**tooconfigure Azure AD single sign-on avec Wingspan eTMF, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65615-150">**tooconfigure Azure AD single sign-on with Wingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="65615-151">Bonjour portail Azure, sur hello **Wingspan eTMF** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="65615-151">In hello Azure portal, on hello **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="65615-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="65615-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="65615-155">Sur hello **Wingspan eTMF domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="65615-155">On hello **Wingspan eTMF Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="65615-157">a.</span><span class="sxs-lookup"><span data-stu-id="65615-157">a.</span></span> <span data-ttu-id="65615-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="65615-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="65615-159">b.</span><span class="sxs-lookup"><span data-stu-id="65615-159">b.</span></span> <span data-ttu-id="65615-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="65615-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="65615-161">c.</span><span class="sxs-lookup"><span data-stu-id="65615-161">c.</span></span> <span data-ttu-id="65615-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="65615-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="65615-163">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="65615-163">These values are not hello real.</span></span> <span data-ttu-id="65615-164">Mettre à jour ces valeurs hello réelle URL de connexion, identificateur et réponse à une URL, y compris le nom du client réel hello et le nom de l’instance.</span><span class="sxs-lookup"><span data-stu-id="65615-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL including hello actual customer name and instance name.</span></span> <span data-ttu-id="65615-165">Contact [équipe de support Client Wingspan eTMF](http://www.wingspan.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="65615-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="65615-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="65615-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="65615-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="65615-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65615-170">tooconfigure l’authentification unique sur **Wingspan eTMF** côté, vous devez hello toosend téléchargé **Metadata XML** trop[prise en charge de Wingspan eTMF](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="65615-170">tooconfigure single sign-on on **Wingspan eTMF** side, you need toosend hello downloaded **Metadata XML** too[Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="65615-171">Ils configurer toohave hello connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="65615-171">They set this up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="65615-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="65615-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65615-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="65615-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65615-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65615-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65615-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="65615-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="65615-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="65615-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65615-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65615-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="65615-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65615-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="65615-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65615-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="65615-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65615-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="65615-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65615-187">a.</span><span class="sxs-lookup"><span data-stu-id="65615-187">a.</span></span> <span data-ttu-id="65615-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65615-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65615-189">b.</span><span class="sxs-lookup"><span data-stu-id="65615-189">b.</span></span> <span data-ttu-id="65615-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65615-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65615-191">c.</span><span class="sxs-lookup"><span data-stu-id="65615-191">c.</span></span> <span data-ttu-id="65615-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="65615-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65615-193">d.</span><span class="sxs-lookup"><span data-stu-id="65615-193">d.</span></span> <span data-ttu-id="65615-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="65615-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="65615-195">Création d’un utilisateur de test de Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="65615-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="65615-196">Dans cette section, vous créez un utilisateur appelé Britta Simon dans Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="65615-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="65615-197">Travailler avec [prise en charge de Wingspan eTMF](http://www.wingspan.com/contact-us/) tooadd les utilisateurs de hello Bonjour application eTMF de Wingspan.</span><span class="sxs-lookup"><span data-stu-id="65615-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) tooadd hello users in hello Wingspan eTMF application.</span></span> <span data-ttu-id="65615-198">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="65615-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65615-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="65615-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65615-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="65615-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWingspan eTMF.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="65615-202">**tooassign Britta Simon tooWingspan eTMF, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="65615-202">**tooassign Britta Simon tooWingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="65615-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="65615-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="65615-205">Dans la liste des applications hello, sélectionnez **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="65615-205">In hello applications list, select **Wingspan eTMF**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="65615-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="65615-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="65615-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="65615-209">Click **Add** button.</span></span> <span data-ttu-id="65615-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="65615-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="65615-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="65615-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65615-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="65615-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65615-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="65615-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65615-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="65615-215">Testing single sign-on</span></span>

<span data-ttu-id="65615-216">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="65615-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="65615-217">Cliquez sur la vignette d’eTMF Wingspan hello Bonjour volet d’accès, vous serez redirigé tooOrganization page d’authentification.</span><span class="sxs-lookup"><span data-stu-id="65615-217">Click hello Wingspan eTMF tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="65615-218">Connexion réussie, vous serez connecté tooyour application eTMF de Wingspan.</span><span class="sxs-lookup"><span data-stu-id="65615-218">After successful login, you will be signed-on tooyour Wingspan eTMF application.</span></span> <span data-ttu-id="65615-219">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="65615-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65615-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="65615-220">Additional resources</span></span>

* [<span data-ttu-id="65615-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65615-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65615-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="65615-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

