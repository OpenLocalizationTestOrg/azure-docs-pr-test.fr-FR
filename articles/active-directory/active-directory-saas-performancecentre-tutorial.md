---
title: "Didacticiel : Intégration d’Azure Active Directory à PerformanceCentre | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="36810-103">Didacticiel : Intégration d’Azure Active Directory à PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="36810-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="36810-104">Dans ce didacticiel, vous apprendrez comment toointegrate PerformanceCentre avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36810-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36810-105">Intégration PerformanceCentre à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="36810-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="36810-106">Vous pouvez contrôler dans Azure AD qui a accès tooPerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="36810-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="36810-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPerformanceCentre (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36810-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="36810-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="36810-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36810-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36810-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="36810-110">Prerequisites</span></span>

<span data-ttu-id="36810-111">tooconfigure intégration d’Azure AD avec PerformanceCentre, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="36810-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="36810-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36810-113">Un abonnement PerformanceCentre pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="36810-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36810-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="36810-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36810-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="36810-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36810-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="36810-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36810-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36810-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36810-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="36810-118">Scenario description</span></span>
<span data-ttu-id="36810-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="36810-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36810-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="36810-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36810-121">Ajout de PerformanceCentre à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="36810-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="36810-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="36810-123">Ajout de PerformanceCentre à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="36810-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="36810-124">intégration de hello tooconfigure de PerformanceCentre dans Azure AD, vous devez tooadd PerformanceCentre à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="36810-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="36810-125">**tooadd PerformanceCentre à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36810-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="36810-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="36810-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36810-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="36810-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="36810-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="36810-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="36810-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="36810-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="36810-133">Dans la zone de recherche de hello, tapez **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="36810-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="36810-135">Dans le volet de résultats hello, sélectionnez **PerformanceCentre**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="36810-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36810-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36810-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec PerformanceCentre au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="36810-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36810-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PerformanceCentre est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36810-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="36810-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PerformanceCentre doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="36810-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="36810-141">Dans PerformanceCentre, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="36810-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="36810-142">tooconfigure et test Azure AD l’authentification unique avec PerformanceCentre, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="36810-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="36810-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="36810-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="36810-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36810-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36810-145">**[Création d’un utilisateur de test PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave un équivalent de Britta Simon dans PerformanceCentre est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="36810-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="36810-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="36810-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36810-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="36810-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36810-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36810-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="36810-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="36810-150">**tooconfigure Azure AD single sign-on avec PerformanceCentre, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36810-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="36810-151">Bonjour portail Azure, sur hello **PerformanceCentre** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="36810-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="36810-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="36810-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="36810-155">Sur hello **PerformanceCentre domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="36810-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="36810-157">a.</span><span class="sxs-lookup"><span data-stu-id="36810-157">a.</span></span> <span data-ttu-id="36810-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="36810-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="36810-159">b.</span><span class="sxs-lookup"><span data-stu-id="36810-159">b.</span></span> <span data-ttu-id="36810-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="36810-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36810-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="36810-161">These values are not real.</span></span> <span data-ttu-id="36810-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="36810-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="36810-163">Contact [équipe de support Client de PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="36810-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="36810-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="36810-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="36810-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="36810-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36810-168">Sur hello **PerformanceCentre Configuration** , cliquez sur **PerformanceCentre de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="36810-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="36810-169">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="36810-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="36810-171">Authentification tooyour **PerformanceCentre** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="36810-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="36810-172">Dans l’onglet hello sur le côté gauche de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="36810-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Authentification unique Azure AD][10]

9. <span data-ttu-id="36810-174">Dans l’onglet hello sur le côté gauche de hello, cliquez sur **divers**, puis cliquez sur **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="36810-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Authentification unique Azure AD][11]

10. <span data-ttu-id="36810-176">Pour **Protocol**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="36810-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Authentification unique Azure AD][12]

11. <span data-ttu-id="36810-178">Ouvrez votre fichier de métadonnées téléchargé dans le bloc-notes, copier le contenu hello, collez-le dans hello **métadonnées du fournisseur d’identité** zone de texte, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="36810-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Authentification unique Azure AD][13]

12. <span data-ttu-id="36810-180">Vérifiez que les valeurs hello pour hello **URL de Base d’entité** et **URL ID d’entité** sont corrects.</span><span class="sxs-lookup"><span data-stu-id="36810-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Authentification unique Azure AD][14]

> [!TIP]
> <span data-ttu-id="36810-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="36810-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="36810-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="36810-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="36810-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36810-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36810-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="36810-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="36810-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="36810-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36810-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="36810-189">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="36810-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36810-191">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="36810-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36810-193">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="36810-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36810-195">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="36810-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36810-197">a.</span><span class="sxs-lookup"><span data-stu-id="36810-197">a.</span></span> <span data-ttu-id="36810-198">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36810-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36810-199">b.</span><span class="sxs-lookup"><span data-stu-id="36810-199">b.</span></span> <span data-ttu-id="36810-200">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="36810-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36810-201">c.</span><span class="sxs-lookup"><span data-stu-id="36810-201">c.</span></span> <span data-ttu-id="36810-202">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="36810-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="36810-203">d.</span><span class="sxs-lookup"><span data-stu-id="36810-203">d.</span></span> <span data-ttu-id="36810-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="36810-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="36810-205">Création d’un utilisateur de test PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="36810-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="36810-206">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="36810-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="36810-207">**toocreate un utilisateur appelé Britta Simon dans PerformanceCentre, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36810-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="36810-208">Se connecter tooyour PerformanceCentre site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="36810-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="36810-209">Dans le menu hello hello gauche, cliquez sur **Interrelate**, puis cliquez sur **créer un Participant**.</span><span class="sxs-lookup"><span data-stu-id="36810-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Create User][400]

3. <span data-ttu-id="36810-211">Sur hello **interagissent - créer Participant** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="36810-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Create User][401]
    
    <span data-ttu-id="36810-213">a.</span><span class="sxs-lookup"><span data-stu-id="36810-213">a.</span></span> <span data-ttu-id="36810-214">Attributs de Britta Simon hello de type est requis dans les zones de texte.</span><span class="sxs-lookup"><span data-stu-id="36810-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="36810-215">Nom d’utilisateur de Brian attribut de PerformanceCentre doit être hello identique hello du nom d’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36810-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="36810-216">b.</span><span class="sxs-lookup"><span data-stu-id="36810-216">b.</span></span> <span data-ttu-id="36810-217">Sélectionnez **Client Administrator** pour **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="36810-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="36810-218">c.</span><span class="sxs-lookup"><span data-stu-id="36810-218">c.</span></span> <span data-ttu-id="36810-219">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="36810-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="36810-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="36810-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="36810-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="36810-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="36810-223">**tooassign Britta Simon tooPerformanceCentre, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="36810-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="36810-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="36810-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="36810-226">Dans la liste des applications hello, sélectionnez **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="36810-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="36810-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="36810-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="36810-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="36810-230">Click **Add** button.</span></span> <span data-ttu-id="36810-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="36810-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="36810-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="36810-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="36810-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="36810-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36810-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="36810-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36810-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="36810-236">Testing single sign-on</span></span>

<span data-ttu-id="36810-237">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="36810-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="36810-238">Lorsque vous cliquez sur mosaïque PerformanceCentre hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour PerformanceCentre application.</span><span class="sxs-lookup"><span data-stu-id="36810-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36810-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="36810-239">Additional resources</span></span>

* [<span data-ttu-id="36810-240">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36810-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36810-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="36810-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

