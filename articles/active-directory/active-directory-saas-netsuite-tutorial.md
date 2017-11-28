---
title: "Didacticiel : Intégration d’Azure Active Directory à Netsuite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="fda32-103">Didacticiel : Intégration d’Azure Active Directory à Netsuite</span><span class="sxs-lookup"><span data-stu-id="fda32-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="fda32-104">Dans ce didacticiel, vous apprendrez comment toointegrate Netsuite avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fda32-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fda32-105">Intégration de Netsuite à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fda32-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fda32-106">Vous pouvez contrôler dans Azure AD qui a accès tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="fda32-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="fda32-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNetsuite (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fda32-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="fda32-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fda32-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fda32-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fda32-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fda32-110">Prerequisites</span></span>

<span data-ttu-id="fda32-111">tooconfigure intégration d’Azure AD à Netsuite, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fda32-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="fda32-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fda32-113">Un abonnement Netsuite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fda32-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fda32-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fda32-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fda32-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="fda32-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fda32-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fda32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fda32-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fda32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fda32-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fda32-118">Scenario description</span></span>
<span data-ttu-id="fda32-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fda32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fda32-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="fda32-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fda32-121">Ajout de Netsuite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fda32-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="fda32-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="fda32-123">Ajout de Netsuite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="fda32-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="fda32-124">intégration de hello tooconfigure de Netsuite dans Azure AD, vous devez tooadd Netsuite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fda32-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fda32-125">**tooadd Netsuite à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fda32-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fda32-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="fda32-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fda32-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fda32-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fda32-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fda32-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fda32-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="fda32-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fda32-133">Dans la zone de recherche de hello, tapez **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="fda32-133">In hello search box, type **Netsuite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="fda32-135">Dans le volet de résultats hello, sélectionnez **Netsuite**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fda32-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fda32-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fda32-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Netsuite sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fda32-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fda32-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Netsuite est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fda32-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="fda32-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Netsuite doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="fda32-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="fda32-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Netsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="fda32-142">tooconfigure et test Azure AD l’authentification unique avec Netsuite, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="fda32-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fda32-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fda32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fda32-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fda32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fda32-145">**[Création d’un utilisateur de test Netsuite](#creating-a-netsuite-test-user)**  -toohave un équivalent de Britta Simon dans Netsuite est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fda32-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fda32-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fda32-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fda32-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="fda32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fda32-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fda32-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Netsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="fda32-150">**tooconfigure Azure AD single sign-on avec Netsuite, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fda32-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="fda32-151">Bonjour portail Azure, sur hello **Netsuite** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fda32-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fda32-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fda32-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="fda32-155">Sur hello **Netsuite domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fda32-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="fda32-157">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle : `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="fda32-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fda32-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="fda32-158">This value is not real value.</span></span> <span data-ttu-id="fda32-159">Valeur de hello de mise à jour avec hello URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="fda32-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="fda32-160">Contact [équipe de support Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="fda32-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="fda32-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fda32-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="fda32-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fda32-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fda32-165">Sur hello **Netsuite Configuration** , cliquez sur **Netsuite de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="fda32-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fda32-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="fda32-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="fda32-168">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à votre site d’entreprise Netsuite en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fda32-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="fda32-169">Dans la barre d’outils de hello en hello haut hello, cliquez sur **le programme d’installation**, puis cliquez sur **le Gestionnaire d’installation**.</span><span class="sxs-lookup"><span data-stu-id="fda32-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="fda32-171">À partir de hello **les tâches d’installation** liste, sélectionnez **intégration**.</span><span class="sxs-lookup"><span data-stu-id="fda32-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="fda32-173">Bonjour **gérer l’authentification** , cliquez sur **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fda32-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="fda32-175">Sur hello **le programme d’installation SAML** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fda32-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="fda32-176">a.</span><span class="sxs-lookup"><span data-stu-id="fda32-176">a.</span></span> <span data-ttu-id="fda32-177">Hello de copie **SAML Sign-On URL du Service unique** valeur **aide-mémoire** section de **configurer l’authentification** et collez-le dans hello **fournisseur d’identité Page de connexion** champ Netsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="fda32-179">b.</span><span class="sxs-lookup"><span data-stu-id="fda32-179">b.</span></span> <span data-ttu-id="fda32-180">Dans Netsuite, sélectionnez **Méthode d’authentification principale**.</span><span class="sxs-lookup"><span data-stu-id="fda32-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="fda32-181">c.</span><span class="sxs-lookup"><span data-stu-id="fda32-181">c.</span></span> <span data-ttu-id="fda32-182">Pour le champ hello **métadonnées du fournisseur d’identité SAMLV2**, sélectionnez **télécharger un fichier de métadonnées IDP**.</span><span class="sxs-lookup"><span data-stu-id="fda32-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="fda32-183">Puis cliquez sur **Parcourir** fichier de métadonnées hello tooupload que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fda32-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="fda32-185">d.</span><span class="sxs-lookup"><span data-stu-id="fda32-185">d.</span></span> <span data-ttu-id="fda32-186">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="fda32-186">Click **Submit**.</span></span>

12. <span data-ttu-id="fda32-187">Dans Azure AD, activez la case à cocher **Afficher et modifier tous les autres attributs utilisateur**, puis ajoutez un attribut.</span><span class="sxs-lookup"><span data-stu-id="fda32-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="fda32-189">Pourquoi **nom de l’attribut** , tapez dans `account`.</span><span class="sxs-lookup"><span data-stu-id="fda32-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="fda32-190">Pourquoi **valeur d’attribut** , tapez votre ID de compte Netsuite. Cette valeur est constante et la modification à un compte.</span><span class="sxs-lookup"><span data-stu-id="fda32-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="fda32-191">Obtenir des instructions sur la façon de toofind votre ID de compte sont présentés ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fda32-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="fda32-193">a.</span><span class="sxs-lookup"><span data-stu-id="fda32-193">a.</span></span> <span data-ttu-id="fda32-194">Dans Netsuite, cliquez sur **le programme d’installation** à partir du menu de navigation supérieur hello.</span><span class="sxs-lookup"><span data-stu-id="fda32-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="fda32-195">b.</span><span class="sxs-lookup"><span data-stu-id="fda32-195">b.</span></span> <span data-ttu-id="fda32-196">Puis cliquez sur sous hello **les tâches d’installation** section du menu de navigation gauche hello, sélectionnez hello **intégration** section, puis cliquez sur **préférences de Services Web**.</span><span class="sxs-lookup"><span data-stu-id="fda32-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="fda32-197">c.</span><span class="sxs-lookup"><span data-stu-id="fda32-197">c.</span></span> <span data-ttu-id="fda32-198">Copiez votre ID de compte Netsuite et collez-le dans hello **valeur d’attribut** champ dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fda32-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="fda32-200">Avant que les utilisateurs peuvent effectuer l’authentification unique dans Netsuite, ils doivent d’abord être affectés les autorisations appropriées de hello dans Netsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="fda32-201">Suivez les instructions de hello ci-dessous tooassign ces autorisations.</span><span class="sxs-lookup"><span data-stu-id="fda32-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="fda32-202">a.</span><span class="sxs-lookup"><span data-stu-id="fda32-202">a.</span></span> <span data-ttu-id="fda32-203">Dans le menu de navigation supérieur hello, cliquez sur **le programme d’installation**, puis cliquez sur **le Gestionnaire d’installation**.</span><span class="sxs-lookup"><span data-stu-id="fda32-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="fda32-205">b.</span><span class="sxs-lookup"><span data-stu-id="fda32-205">b.</span></span> <span data-ttu-id="fda32-206">Dans le menu de navigation gauche hello, sélectionnez **utilisateurs/rôles**, puis cliquez sur **gérer les rôles**.</span><span class="sxs-lookup"><span data-stu-id="fda32-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="fda32-208">c.</span><span class="sxs-lookup"><span data-stu-id="fda32-208">c.</span></span> <span data-ttu-id="fda32-209">Cliquez sur **Nouveau rôle**.</span><span class="sxs-lookup"><span data-stu-id="fda32-209">Click **New Role**.</span></span>

    <span data-ttu-id="fda32-210">d.</span><span class="sxs-lookup"><span data-stu-id="fda32-210">d.</span></span> <span data-ttu-id="fda32-211">Tapez un **nom** pour votre nouveau rôle, puis sélectionnez hello **unique Sign-On uniquement** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="fda32-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="fda32-213">e.</span><span class="sxs-lookup"><span data-stu-id="fda32-213">e.</span></span> <span data-ttu-id="fda32-214">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fda32-214">Click **Save**.</span></span>

    <span data-ttu-id="fda32-215">f.</span><span class="sxs-lookup"><span data-stu-id="fda32-215">f.</span></span> <span data-ttu-id="fda32-216">Dans le menu hello haut de hello, cliquez sur **autorisations**.</span><span class="sxs-lookup"><span data-stu-id="fda32-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="fda32-217">Cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="fda32-217">Then click **Setup**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="fda32-219">g.</span><span class="sxs-lookup"><span data-stu-id="fda32-219">g.</span></span> <span data-ttu-id="fda32-220">Sélectionnez **Configurer l’authentification unique SAM**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fda32-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="fda32-221">h.</span><span class="sxs-lookup"><span data-stu-id="fda32-221">h.</span></span> <span data-ttu-id="fda32-222">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fda32-222">Click **Save**.</span></span>

    <span data-ttu-id="fda32-223">i.</span><span class="sxs-lookup"><span data-stu-id="fda32-223">i.</span></span> <span data-ttu-id="fda32-224">Dans le menu de navigation supérieur hello, cliquez sur **le programme d’installation**, puis cliquez sur **le Gestionnaire d’installation**.</span><span class="sxs-lookup"><span data-stu-id="fda32-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="fda32-226">j.</span><span class="sxs-lookup"><span data-stu-id="fda32-226">j.</span></span> <span data-ttu-id="fda32-227">Dans le menu de navigation gauche hello, sélectionnez **utilisateurs/rôles**, puis cliquez sur **gérer les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fda32-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="fda32-229">k.</span><span class="sxs-lookup"><span data-stu-id="fda32-229">k.</span></span> <span data-ttu-id="fda32-230">Sélectionnez un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="fda32-230">Select a test user.</span></span> <span data-ttu-id="fda32-231">Puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="fda32-231">Then click **Edit**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="fda32-233">l.</span><span class="sxs-lookup"><span data-stu-id="fda32-233">l.</span></span> <span data-ttu-id="fda32-234">Dans la boîte de dialogue rôles hello, sélectionnez le rôle de hello que vous avez créé et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fda32-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="fda32-236">m.</span><span class="sxs-lookup"><span data-stu-id="fda32-236">m.</span></span> <span data-ttu-id="fda32-237">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fda32-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="fda32-238">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="fda32-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fda32-239">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="fda32-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fda32-240">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fda32-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fda32-241">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="fda32-242">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="fda32-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fda32-244">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fda32-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fda32-245">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="fda32-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="fda32-247">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fda32-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fda32-249">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fda32-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fda32-251">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fda32-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fda32-253">a.</span><span class="sxs-lookup"><span data-stu-id="fda32-253">a.</span></span> <span data-ttu-id="fda32-254">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fda32-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fda32-255">b.</span><span class="sxs-lookup"><span data-stu-id="fda32-255">b.</span></span> <span data-ttu-id="fda32-256">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fda32-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fda32-257">c.</span><span class="sxs-lookup"><span data-stu-id="fda32-257">c.</span></span> <span data-ttu-id="fda32-258">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fda32-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fda32-259">d.</span><span class="sxs-lookup"><span data-stu-id="fda32-259">d.</span></span> <span data-ttu-id="fda32-260">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fda32-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="fda32-261">Création d’un utilisateur de test Netsuite</span><span class="sxs-lookup"><span data-stu-id="fda32-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="fda32-262">Dans cette section, un utilisateur nommé Britta Simon est créé dans Netsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="fda32-263">Netsuite prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="fda32-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="fda32-264">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="fda32-264">There is no action item for you in this section.</span></span> <span data-ttu-id="fda32-265">Si un utilisateur n’existe pas déjà dans Netsuite, un nouveau est créé lorsque vous essayez de tooaccess Netsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fda32-266">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fda32-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fda32-267">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="fda32-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fda32-269">**tooassign Britta Simon tooNetsuite, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fda32-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="fda32-270">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fda32-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fda32-272">Dans la liste des applications hello, sélectionnez **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="fda32-272">In hello applications list, select **Netsuite**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="fda32-274">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fda32-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fda32-276">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fda32-276">Click **Add** button.</span></span> <span data-ttu-id="fda32-277">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fda32-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fda32-279">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="fda32-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fda32-280">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fda32-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fda32-281">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fda32-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fda32-282">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fda32-282">Testing single sign-on</span></span>

<span data-ttu-id="fda32-283">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="fda32-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fda32-284">tootest votre seule paramètres d’authentification, ouvrez hello volet d’accès au [https://myapps.microsoft.com](https://myapps.microsoft.com/), connectez-vous à un compte de test hello, puis cliquez sur **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="fda32-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fda32-285">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fda32-285">Additional resources</span></span>

* [<span data-ttu-id="fda32-286">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fda32-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fda32-287">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fda32-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fda32-288">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="fda32-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

