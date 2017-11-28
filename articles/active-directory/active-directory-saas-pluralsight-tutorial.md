---
title: "Didacticiel : Intégration de Pluralsight à Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="4b583-103">Didacticiel : Intégration de Pluralsight à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b583-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="4b583-104">Dans ce didacticiel, vous apprendrez comment toointegrate Pluralsight avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b583-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b583-105">Intégration de Pluralsight à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4b583-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b583-106">Vous pouvez contrôler dans Azure AD qui a accès tooPluralsight</span><span class="sxs-lookup"><span data-stu-id="4b583-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="4b583-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPluralsight (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b583-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4b583-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b583-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b583-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b583-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4b583-110">Prerequisites</span></span>

<span data-ttu-id="4b583-111">tooconfigure intégration d’Azure AD avec Pluralsight, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4b583-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="4b583-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b583-113">Un abonnement Pluralsight pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4b583-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b583-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4b583-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b583-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4b583-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b583-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4b583-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b583-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b583-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b583-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4b583-118">Scenario description</span></span>
<span data-ttu-id="4b583-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4b583-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b583-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4b583-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b583-121">Ajout de Pluralsight à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4b583-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="4b583-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="4b583-123">Ajout de Pluralsight à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4b583-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="4b583-124">intégration de hello tooconfigure de Pluralsight dans Azure AD, vous devez tooadd Pluralsight à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4b583-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b583-125">**tooadd Pluralsight à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b583-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b583-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4b583-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b583-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4b583-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b583-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4b583-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4b583-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4b583-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4b583-133">Dans la zone de recherche de hello, tapez **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="4b583-133">In hello search box, type **Pluralsight**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="4b583-135">Dans le volet de résultats hello, sélectionnez **Pluralsight**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b583-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b583-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b583-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pluralsight avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4b583-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b583-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Pluralsight est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b583-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="4b583-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Pluralsight doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4b583-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="4b583-141">Dans Pluralsight, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b583-142">tooconfigure et test Azure AD l’authentification unique avec Pluralsight, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4b583-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b583-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4b583-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b583-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b583-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b583-145">**[Création d’un utilisateur de test Pluralsight](#creating-a-pluralsight-test-user)**  -toohave un équivalent de Britta Simon dans Pluralsight est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b583-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b583-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b583-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b583-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4b583-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b583-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b583-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="4b583-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="4b583-150">**tooconfigure Azure AD single sign-on avec Pluralsight, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b583-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b583-151">Bonjour portail Azure, sur hello **Pluralsight** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4b583-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4b583-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b583-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="4b583-155">Sur hello **Pluralsight domaine et les URL** section, hello suivants :</span><span class="sxs-lookup"><span data-stu-id="4b583-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="4b583-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="4b583-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b583-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="4b583-158">This value is not real.</span></span> <span data-ttu-id="4b583-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="4b583-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4b583-160">Contact [équipe de support Client de Pluralsight](mailto:support@pluralsight.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="4b583-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="4b583-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4b583-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="4b583-163">objectif Hello de cette section est tooenable Azure AD single sign-on hello portail Azure et tooconfigure l’authentification unique dans l’application de Pluralsight hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="4b583-164">Hello Pluralsight application attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="4b583-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="4b583-165">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="4b583-165">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="4b583-167">Vous pouvez également ajouter hello **« ID Unique »** attribut avec la valeur appropriée hello comme EmployeeID ou autre chose qui correspond le mieux à votre organisation.</span><span class="sxs-lookup"><span data-stu-id="4b583-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="4b583-168">Notez également qu’il ne s’agit pas d’attribut requis de hello ; Toutefois, vous pouvez l’ajouter trop identifier utilisateur unique de hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="4b583-169">hello tooadd requis **attributs du jeton SAML**, pour chaque ligne de la table hello ci-dessous, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b583-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="4b583-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="4b583-170">Attribute Name</span></span> | <span data-ttu-id="4b583-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="4b583-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="4b583-172">Prénom</span><span class="sxs-lookup"><span data-stu-id="4b583-172">First Name</span></span> |<span data-ttu-id="4b583-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4b583-173">user.givenname</span></span> |
   | <span data-ttu-id="4b583-174">Nom</span><span class="sxs-lookup"><span data-stu-id="4b583-174">Last Name</span></span> |<span data-ttu-id="4b583-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="4b583-175">user.surname</span></span> |
   | <span data-ttu-id="4b583-176">Email</span><span class="sxs-lookup"><span data-stu-id="4b583-176">Email</span></span> |<span data-ttu-id="4b583-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="4b583-177">user.mail</span></span> |
   
   <span data-ttu-id="4b583-178">a.</span><span class="sxs-lookup"><span data-stu-id="4b583-178">a.</span></span> <span data-ttu-id="4b583-179">Cliquez sur **ajouter un attribut utilisateur** tooopen hello **Attribure d’utilisateur Ajouter** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4b583-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="4b583-181">b.</span><span class="sxs-lookup"><span data-stu-id="4b583-181">b.</span></span> <span data-ttu-id="4b583-182">Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="4b583-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="4b583-183">c.</span><span class="sxs-lookup"><span data-stu-id="4b583-183">c.</span></span> <span data-ttu-id="4b583-184">À partir de hello **valeur d’attribut** liste, la valeur de l’attribut select hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="4b583-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="4b583-185">d.</span><span class="sxs-lookup"><span data-stu-id="4b583-185">d.</span></span> <span data-ttu-id="4b583-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b583-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="4b583-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4b583-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4b583-189">tooget l’authentification unique configurée pour votre application, contactez [technologiques Pluralsight](mailTo:professionalservices@pluralsight.com) d’équipe et de fournir le fichier de métadonnées téléchargé hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="4b583-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4b583-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b583-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b583-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b583-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b583-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b583-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4b583-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4b583-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b583-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b583-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4b583-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b583-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4b583-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b583-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b583-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b583-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b583-205">a.</span><span class="sxs-lookup"><span data-stu-id="4b583-205">a.</span></span> <span data-ttu-id="4b583-206">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b583-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b583-207">b.</span><span class="sxs-lookup"><span data-stu-id="4b583-207">b.</span></span> <span data-ttu-id="4b583-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b583-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b583-209">c.</span><span class="sxs-lookup"><span data-stu-id="4b583-209">c.</span></span> <span data-ttu-id="4b583-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4b583-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b583-211">d.</span><span class="sxs-lookup"><span data-stu-id="4b583-211">d.</span></span> <span data-ttu-id="4b583-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b583-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="4b583-213">Création d’un utilisateur de test Pluralsight</span><span class="sxs-lookup"><span data-stu-id="4b583-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="4b583-214">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="4b583-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="4b583-215">Collaborez avec [équipe de support Client de Pluralsight](mailto:support@pluralsight.com) utilisateurs hello tooadd hello Pluralsight compte.</span><span class="sxs-lookup"><span data-stu-id="4b583-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b583-216">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b583-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b583-217">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPluralsight.</span><span class="sxs-lookup"><span data-stu-id="4b583-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4b583-219">**tooassign Britta Simon tooPluralsight, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b583-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b583-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4b583-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4b583-222">Dans la liste des applications hello, sélectionnez **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="4b583-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="4b583-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4b583-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4b583-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4b583-226">Click **Add** button.</span></span> <span data-ttu-id="4b583-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4b583-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4b583-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4b583-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b583-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4b583-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b583-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4b583-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b583-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4b583-232">Testing single sign-on</span></span>

<span data-ttu-id="4b583-233">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4b583-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b583-234">Lorsque vous cliquez sur mosaïque Pluralsight hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Pluralsight application.</span><span class="sxs-lookup"><span data-stu-id="4b583-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="4b583-235">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b583-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b583-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4b583-236">Additional resources</span></span>

* [<span data-ttu-id="4b583-237">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b583-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b583-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4b583-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

