---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP NetWeaver | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 69008734864e1e258a0c2ec872e51aa331491fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="15441-103">Didacticiel : Intégration d’Azure Active Directory à SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="15441-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="15441-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAP NetWeaver avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15441-104">In this tutorial, you learn how toointegrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15441-105">Intégration de SAP NetWeaver avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="15441-105">Integrating SAP NetWeaver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="15441-106">Vous pouvez contrôler dans Azure AD qui a accès tooSAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="15441-106">You can control in Azure AD who has access tooSAP NetWeaver</span></span>
- <span data-ttu-id="15441-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP NetWeaver (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-107">You can enable your users tooautomatically get signed-on tooSAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="15441-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="15441-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="15441-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15441-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="15441-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15441-110">Prerequisites</span></span>

<span data-ttu-id="15441-111">tooconfigure intégration d’Azure AD avec SAP NetWeaver, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="15441-111">tooconfigure Azure AD integration with SAP NetWeaver, you need hello following items:</span></span>

- <span data-ttu-id="15441-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15441-113">Un abonnement SAP NetWeaver pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="15441-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15441-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="15441-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15441-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="15441-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15441-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="15441-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15441-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15441-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15441-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="15441-118">Scenario description</span></span>
<span data-ttu-id="15441-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="15441-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15441-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="15441-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15441-121">Ajout de SAP NetWeaver à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="15441-121">Adding SAP NetWeaver from hello gallery</span></span>
2. <span data-ttu-id="15441-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-hello-gallery"></a><span data-ttu-id="15441-123">Ajout de SAP NetWeaver à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="15441-123">Adding SAP NetWeaver from hello gallery</span></span>
<span data-ttu-id="15441-124">tooconfigure hello intégration de SAP NetWeaver dans Azure AD, vous devez tooadd SAP NetWeaver à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="15441-124">tooconfigure hello integration of SAP NetWeaver into Azure AD, you need tooadd SAP NetWeaver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="15441-125">**tooadd SAP NetWeaver à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="15441-125">**tooadd SAP NetWeaver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="15441-126">Bonjour  **[Azure Portal](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="15441-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="15441-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="15441-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="15441-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="15441-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="15441-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="15441-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="15441-133">Dans la zone de recherche de hello, tapez **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="15441-133">In hello search box, type **SAP NetWeaver**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="15441-135">Dans le volet de résultats hello, sélectionnez **SAP NetWeaver**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="15441-135">In hello results panel, select **SAP NetWeaver**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="15441-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="15441-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP NetWeaver à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="15441-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="15441-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAP NetWeaver est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15441-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP NetWeaver is tooa user in Azure AD.</span></span> <span data-ttu-id="15441-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP NetWeaver doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="15441-140">In other words, a link relationship between an Azure AD user and hello related user in SAP NetWeaver needs toobe established.</span></span>

<span data-ttu-id="15441-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="15441-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="15441-142">tooconfigure et test Azure AD l’authentification unique sur SAP NetWeaver, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="15441-142">tooconfigure and test Azure AD single sign-on with SAP NetWeaver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="15441-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="15441-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="15441-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15441-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="15441-145">**[Création d’un utilisateur de test SAP NetWeaver](#creating-an-sap-netweaver-test-user)**  -toohave un équivalent de Britta Simon dans SAP NetWeaver qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15441-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - toohave a counterpart of Britta Simon in SAP NetWeaver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="15441-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="15441-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="15441-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="15441-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="15441-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="15441-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="15441-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="15441-150">**tooconfigure Azure AD l’authentification unique sur SAP NetWeaver, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="15441-150">**tooconfigure Azure AD single sign-on with SAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="15441-151">Bonjour portail Azure, sur hello **SAP NetWeaver** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="15441-151">In hello Azure portal, on hello **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="15441-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="15441-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="15441-155">Sur hello **SAP NetWeaver domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15441-155">On hello **SAP NetWeaver Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="15441-157">a.</span><span class="sxs-lookup"><span data-stu-id="15441-157">a.</span></span> <span data-ttu-id="15441-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="15441-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="15441-159">b.</span><span class="sxs-lookup"><span data-stu-id="15441-159">b.</span></span> <span data-ttu-id="15441-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="15441-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="15441-161">c.</span><span class="sxs-lookup"><span data-stu-id="15441-161">c.</span></span> <span data-ttu-id="15441-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="15441-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="15441-163">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="15441-163">These values are not hello real.</span></span> <span data-ttu-id="15441-164">Mettre à jour les valeurs de hello réel identificateur et les URL de réponse et les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="15441-164">Update these values with hello actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="15441-165">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="15441-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="15441-166">Contact [équipe de support SAP NetWeaver Client](https://www.sap.com/support.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="15441-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) tooget these values.</span></span> 

4. <span data-ttu-id="15441-167">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="15441-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="15441-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="15441-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="15441-171">Sur hello **SAP NetWeaver Configuration** , cliquez sur **configurer SAP NetWeaver** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="15441-171">On hello **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="15441-172">Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="15441-172">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="15441-174">tooconfigure l’authentification unique sur **SAP NetWeaver** côté, vous devez hello toosend téléchargé **Metadata XML** et **ID d’entité SAML** trop[prise en charge de SAP NetWeaver ](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="15441-174">tooconfigure single sign-on on **SAP NetWeaver** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="15441-175">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="15441-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="15441-176">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="15441-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="15441-177">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="15441-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="15441-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="15441-179">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="15441-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="15441-181">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="15441-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="15441-182">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="15441-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="15441-184">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="15441-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="15441-186">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="15441-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="15441-188">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15441-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15441-190">a.</span><span class="sxs-lookup"><span data-stu-id="15441-190">a.</span></span> <span data-ttu-id="15441-191">Bonjour **nom** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="15441-191">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="15441-192">b.</span><span class="sxs-lookup"><span data-stu-id="15441-192">b.</span></span> <span data-ttu-id="15441-193">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15441-193">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="15441-194">c.</span><span class="sxs-lookup"><span data-stu-id="15441-194">c.</span></span> <span data-ttu-id="15441-195">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="15441-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="15441-196">d.</span><span class="sxs-lookup"><span data-stu-id="15441-196">d.</span></span> <span data-ttu-id="15441-197">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="15441-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="15441-198">Création d’un utilisateur de test de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="15441-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="15441-199">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="15441-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="15441-200">Travailler avec votre [prise en charge de SAP NetWeaver](https://www.sap.com/support.html) tooadd les utilisateurs de hello dans la plateforme de SAP NetWeaver hello.</span><span class="sxs-lookup"><span data-stu-id="15441-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) tooadd hello users in hello SAP NetWeaver platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="15441-201">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="15441-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="15441-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="15441-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP NetWeaver.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="15441-204">**tooassign Britta Simon tooSAP NetWeaver, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="15441-204">**tooassign Britta Simon tooSAP NetWeaver, perform hello following steps:**</span></span>

1. <span data-ttu-id="15441-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="15441-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="15441-207">Dans la liste des applications hello, sélectionnez **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="15441-207">In hello applications list, select **SAP NetWeaver**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="15441-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="15441-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="15441-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="15441-211">Click **Add** button.</span></span> <span data-ttu-id="15441-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="15441-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="15441-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="15441-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="15441-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="15441-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="15441-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="15441-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="15441-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="15441-217">Testing single sign-on</span></span>

<span data-ttu-id="15441-218">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="15441-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="15441-219">Lorsque vous cliquez sur mosaïque de SAP NetWeaver hello Bonjour volet d’accès, vous devez obtenir tooyour automatiquement signé sur SAP NetWeaver application.</span><span class="sxs-lookup"><span data-stu-id="15441-219">When you click hello SAP NetWeaver tile in hello Access Panel, you should get automatically signed-on tooyour SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15441-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="15441-220">Additional resources</span></span>

* [<span data-ttu-id="15441-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15441-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="15441-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="15441-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

