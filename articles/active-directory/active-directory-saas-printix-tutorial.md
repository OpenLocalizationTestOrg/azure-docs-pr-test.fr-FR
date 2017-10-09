---
title: "Didacticiel : Intégration d’Azure Active Directory à Printix | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="9f028-103">Didacticiel : Intégration d’Azure Active Directory à Printix</span><span class="sxs-lookup"><span data-stu-id="9f028-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="9f028-104">Dans ce didacticiel, vous apprendrez comment toointegrate Printix avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f028-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f028-105">Intégration Printix à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9f028-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f028-106">Vous pouvez contrôler dans Azure AD qui a accès tooPrintix</span><span class="sxs-lookup"><span data-stu-id="9f028-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="9f028-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPrintix (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f028-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9f028-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f028-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f028-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f028-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9f028-110">Prerequisites</span></span>

<span data-ttu-id="9f028-111">tooconfigure intégration d’Azure AD avec Printix, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9f028-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="9f028-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f028-113">Un abonnement Printix pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9f028-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f028-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9f028-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f028-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9f028-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f028-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9f028-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f028-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f028-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f028-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9f028-118">Scenario description</span></span>
<span data-ttu-id="9f028-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9f028-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f028-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9f028-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f028-121">Ajout de Printix à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9f028-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="9f028-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="9f028-123">Ajout de Printix à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9f028-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="9f028-124">intégration de hello tooconfigure de Printix dans Azure AD, vous devez tooadd Printix à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9f028-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f028-125">**tooadd Printix à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f028-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f028-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9f028-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f028-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9f028-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f028-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9f028-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9f028-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9f028-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9f028-133">Dans la zone de recherche de hello, tapez **Printix**.</span><span class="sxs-lookup"><span data-stu-id="9f028-133">In hello search box, type **Printix**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="9f028-135">Dans le volet de résultats hello, sélectionnez **Printix**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f028-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f028-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f028-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Printix avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9f028-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f028-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Printix est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f028-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="9f028-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Printix doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9f028-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="9f028-141">Dans Printix, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="9f028-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f028-142">tooconfigure et test Azure AD l’authentification unique avec Printix, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9f028-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f028-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9f028-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f028-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f028-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f028-145">**[Création d’un utilisateur de test Printix](#creating-a-printix-test-user)**  -toohave un équivalent de Britta Simon dans Printix est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9f028-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f028-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9f028-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f028-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9f028-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f028-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f028-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Printix.</span><span class="sxs-lookup"><span data-stu-id="9f028-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="9f028-150">**tooconfigure Azure AD single sign-on avec Printix, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f028-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f028-151">Bonjour portail Azure, sur hello **Printix** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9f028-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9f028-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9f028-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="9f028-155">Sur hello **Printix domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f028-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="9f028-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="9f028-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f028-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="9f028-158">hello value is not real.</span></span> <span data-ttu-id="9f028-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="9f028-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9f028-160">Contact [équipe de support Client de Printix](mailto:support@printix.net) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="9f028-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="9f028-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9f028-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="9f028-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9f028-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f028-165">Client de Printix tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9f028-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="9f028-166">Dans le menu hello haut de hello, cliquez sur icône hello dans le coin supérieur droit de hello et sélectionnez «**authentification**».</span><span class="sxs-lookup"><span data-stu-id="9f028-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="9f028-168">Sur hello **le programme d’installation** onglet, sélectionnez **365 de Azure/Office activer l’authentification**</span><span class="sxs-lookup"><span data-stu-id="9f028-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="9f028-170">Sur hello **Azure** onglet, zone de texte toohello d’entrée de fédération pour métadonnées URL de «**document de métadonnées de fédération**».</span><span class="sxs-lookup"><span data-stu-id="9f028-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="9f028-171">Attacher le fichier xml de métadonnées hello que vous avez téléchargé à partir d’Azure AD trop[équipe de support Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="9f028-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="9f028-172">Ensuite, ils charger le fichier xml de hello et fournissent une URL de métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="9f028-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="9f028-174">Cliquez sur hello »**Test**«, puis cliquez sur »**OK**« bouton hello test a réussi.</span><span class="sxs-lookup"><span data-stu-id="9f028-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="9f028-175">Page d’Azure Active Directory s’affichera après avoir cliqué sur hello **test** bouton.</span><span class="sxs-lookup"><span data-stu-id="9f028-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="9f028-176">« test de hello a réussi » signifie ici après avoir entré les informations d’identification hello de votre compte de test Azure qu'il s’affiche un message « paramètres testés OK ». Puis cliquez sur hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="9f028-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="9f028-178">Cliquez sur hello **enregistrer** bouton «**authentification**« page.</span><span class="sxs-lookup"><span data-stu-id="9f028-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="9f028-179">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="9f028-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f028-180">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="9f028-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f028-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f028-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f028-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f028-183">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9f028-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9f028-185">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f028-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f028-186">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9f028-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f028-188">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9f028-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f028-190">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9f028-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f028-192">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f028-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f028-194">a.</span><span class="sxs-lookup"><span data-stu-id="9f028-194">a.</span></span> <span data-ttu-id="9f028-195">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f028-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f028-196">b.</span><span class="sxs-lookup"><span data-stu-id="9f028-196">b.</span></span> <span data-ttu-id="9f028-197">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f028-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f028-198">c.</span><span class="sxs-lookup"><span data-stu-id="9f028-198">c.</span></span> <span data-ttu-id="9f028-199">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9f028-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f028-200">d.</span><span class="sxs-lookup"><span data-stu-id="9f028-200">d.</span></span> <span data-ttu-id="9f028-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9f028-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="9f028-202">Création d’un utilisateur de test Printix</span><span class="sxs-lookup"><span data-stu-id="9f028-202">Creating a Printix test user</span></span>

<span data-ttu-id="9f028-203">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Printix.</span><span class="sxs-lookup"><span data-stu-id="9f028-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="9f028-204">Printix prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="9f028-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9f028-205">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9f028-205">There is no action item for you in this section.</span></span> <span data-ttu-id="9f028-206">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess Printix s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="9f028-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="9f028-207">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="9f028-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f028-208">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f028-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f028-209">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPrintix.</span><span class="sxs-lookup"><span data-stu-id="9f028-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9f028-211">**tooassign Britta Simon tooPrintix, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9f028-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f028-212">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9f028-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9f028-214">Dans la liste des applications hello, sélectionnez **Printix**.</span><span class="sxs-lookup"><span data-stu-id="9f028-214">In hello applications list, select **Printix**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="9f028-216">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9f028-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9f028-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9f028-218">Click **Add** button.</span></span> <span data-ttu-id="9f028-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9f028-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9f028-221">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9f028-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f028-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9f028-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f028-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9f028-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f028-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9f028-224">Testing single sign-on</span></span>

<span data-ttu-id="9f028-225">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9f028-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f028-226">Lorsque vous cliquez sur mosaïque Printix hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Printix application.</span><span class="sxs-lookup"><span data-stu-id="9f028-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f028-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9f028-227">Additional resources</span></span>

* [<span data-ttu-id="9f028-228">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f028-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f028-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9f028-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

