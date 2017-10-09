---
title: "Didacticiel : Intégration d’Azure Active Directory avec Cisco Spark | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="191a1-103">Didacticiel : Intégration d’Azure Active Directory avec Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="191a1-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="191a1-104">Dans ce didacticiel, vous apprendrez comment toointegrate Cisco nouvelles avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="191a1-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="191a1-105">Intégration de Cisco Spark avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="191a1-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="191a1-106">Vous pouvez contrôler dans Azure AD qui a accès tooCisco Spark</span><span class="sxs-lookup"><span data-stu-id="191a1-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="191a1-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCisco Spark (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="191a1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="191a1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="191a1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="191a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="191a1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="191a1-110">Prerequisites</span></span>

<span data-ttu-id="191a1-111">tooconfigure intégration d’Azure AD avec Cisco Spark, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="191a1-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="191a1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="191a1-113">Un abonnement Cisco Spark pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="191a1-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="191a1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="191a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="191a1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="191a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="191a1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="191a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="191a1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="191a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="191a1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="191a1-118">Scenario description</span></span>
<span data-ttu-id="191a1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="191a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="191a1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="191a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="191a1-121">Ajout de Cisco Spark à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="191a1-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="191a1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="191a1-123">Ajout de Cisco Spark à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="191a1-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="191a1-124">tooconfigure hello intégration de Cisco Spark dans Azure AD, vous devez tooadd Cisco Spark à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="191a1-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="191a1-125">**tooadd Spark Cisco à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="191a1-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="191a1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="191a1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="191a1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="191a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="191a1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="191a1-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="191a1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="191a1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="191a1-133">Dans la zone de recherche de hello, tapez **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="191a1-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="191a1-135">Dans le volet de résultats hello, sélectionnez **Cisco Spark**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="191a1-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="191a1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="191a1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cisco Spark sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="191a1-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="191a1-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Cisco Spark est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="191a1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="191a1-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur de Cisco Spark hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="191a1-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="191a1-141">Dans Cisco Spark, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="191a1-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="191a1-142">tooconfigure et test Azure AD l’authentification unique avec Cisco Spark, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="191a1-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="191a1-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="191a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="191a1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="191a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="191a1-145">**[Création d’un utilisateur de test Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave un équivalent de Britta Simon dans Spark Cisco qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="191a1-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="191a1-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="191a1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="191a1-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="191a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="191a1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="191a1-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="191a1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="191a1-150">**tooconfigure Azure AD single sign-on avec Cisco Spark, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="191a1-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="191a1-151">Bonjour portail Azure, sur hello **Cisco Spark** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="191a1-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="191a1-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="191a1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="191a1-155">Sur hello **Cisco Spark domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="191a1-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="191a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="191a1-157">a.</span></span> <span data-ttu-id="191a1-158">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="191a1-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="191a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="191a1-159">b.</span></span> <span data-ttu-id="191a1-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="191a1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="191a1-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="191a1-161">This value is not real.</span></span> <span data-ttu-id="191a1-162">Mettre à jour de cette valeur avec hello identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="191a1-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="191a1-163">Contact [équipe de support Client de Spark Cisco](https://support.ciscospark.com/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="191a1-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="191a1-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="191a1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="191a1-166">Application de Spark Cisco attend des attributs spécifiques du toocontain assertions SAML hello.</span><span class="sxs-lookup"><span data-stu-id="191a1-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="191a1-167">Configurer hello suivant des attributs pour cette application.</span><span class="sxs-lookup"><span data-stu-id="191a1-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="191a1-168">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="191a1-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="191a1-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="191a1-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="191a1-171">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="191a1-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="191a1-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="191a1-172">Attribute Name</span></span>  | <span data-ttu-id="191a1-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="191a1-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="191a1-174">uid</span><span class="sxs-lookup"><span data-stu-id="191a1-174">uid</span></span>    | <span data-ttu-id="191a1-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="191a1-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="191a1-176">a.</span><span class="sxs-lookup"><span data-stu-id="191a1-176">a.</span></span> <span data-ttu-id="191a1-177">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="191a1-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="191a1-180">b.</span><span class="sxs-lookup"><span data-stu-id="191a1-180">b.</span></span> <span data-ttu-id="191a1-181">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="191a1-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="191a1-182">c.</span><span class="sxs-lookup"><span data-stu-id="191a1-182">c.</span></span> <span data-ttu-id="191a1-183">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="191a1-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="191a1-184">d.</span><span class="sxs-lookup"><span data-stu-id="191a1-184">d.</span></span> <span data-ttu-id="191a1-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="191a1-185">Click **Ok**.</span></span>

7. <span data-ttu-id="191a1-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="191a1-186">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="191a1-188">Connectez-vous trop[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) avec vos informations d’identification d’administrateur complet.</span><span class="sxs-lookup"><span data-stu-id="191a1-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="191a1-189">Sélectionnez **paramètres** sous hello **authentification** , cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="191a1-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="191a1-191">Sélectionnez **intégrer un fournisseur d’identité tiers. (Avancé)**  et l’écran suivant de toohello accédez.</span><span class="sxs-lookup"><span data-stu-id="191a1-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="191a1-192">Sur hello **importer les métadonnées Idp** page, soit glisser et supprimer le fichier de métadonnées hello Azure AD sur la page de hello ou utiliser hello fichier navigateur option toolocate et télécharger le fichier de métadonnées hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="191a1-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="191a1-193">Ensuite, sélectionnez **Require certificate signed by a certificate authority in Metadata (more secure)** (Exiger un certificat signé par une autorité de certification dans les métadonnées (plus sûr)), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="191a1-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="191a1-195">Sélectionnez **Test SSO Connection** (Tester la connexion SSO), puis, quand un nouvel onglet de navigateur s’ouvre, et authentifiez-vous auprès d’Azure AD en vous connectant.</span><span class="sxs-lookup"><span data-stu-id="191a1-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="191a1-196">Retourner toohello **Cisco Cloud Collaboration Management** onglet du navigateur. Si le test de hello a réussi, sélectionnez **ce test a réussi. option Activer l’authentification unique** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="191a1-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="191a1-197">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="191a1-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="191a1-198">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="191a1-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="191a1-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="191a1-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="191a1-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="191a1-201">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="191a1-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="191a1-203">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="191a1-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="191a1-204">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="191a1-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="191a1-206">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="191a1-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="191a1-208">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="191a1-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="191a1-210">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="191a1-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="191a1-212">a.</span><span class="sxs-lookup"><span data-stu-id="191a1-212">a.</span></span> <span data-ttu-id="191a1-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="191a1-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="191a1-214">b.</span><span class="sxs-lookup"><span data-stu-id="191a1-214">b.</span></span> <span data-ttu-id="191a1-215">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="191a1-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="191a1-216">c.</span><span class="sxs-lookup"><span data-stu-id="191a1-216">c.</span></span> <span data-ttu-id="191a1-217">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="191a1-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="191a1-218">d.</span><span class="sxs-lookup"><span data-stu-id="191a1-218">d.</span></span> <span data-ttu-id="191a1-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="191a1-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="191a1-220">Création d’un utilisateur de test Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="191a1-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="191a1-221">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="191a1-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="191a1-222">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="191a1-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="191a1-223">Accédez toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) avec vos informations d’identification d’administrateur complet.</span><span class="sxs-lookup"><span data-stu-id="191a1-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="191a1-224">Cliquez sur **Utilisateurs**, puis sur **Gérer les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="191a1-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="191a1-226">Bonjour **gérer les utilisateurs** fenêtre, sélectionnez **manuellement ajouter ou modifier des utilisateurs** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="191a1-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="191a1-227">Sélectionnez **Names and Email address** (Noms et adresse de messagerie).</span><span class="sxs-lookup"><span data-stu-id="191a1-227">Select **Names and Email address**.</span></span> <span data-ttu-id="191a1-228">Renseignez ensuite, zone de texte hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="191a1-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="191a1-230">a.</span><span class="sxs-lookup"><span data-stu-id="191a1-230">a.</span></span> <span data-ttu-id="191a1-231">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="191a1-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="191a1-232">b.</span><span class="sxs-lookup"><span data-stu-id="191a1-232">b.</span></span> <span data-ttu-id="191a1-233">Bonjour **nom** zone de texte, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="191a1-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="191a1-234">c.</span><span class="sxs-lookup"><span data-stu-id="191a1-234">c.</span></span> <span data-ttu-id="191a1-235">Bonjour **adresse de messagerie** zone de texte, type  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="191a1-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="191a1-236">Cliquez sur hello plus se connecter tooadd Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="191a1-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="191a1-237">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="191a1-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="191a1-238">Bonjour **ajouter des Services pour les utilisateurs** fenêtre, cliquez sur **enregistrer** , puis **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="191a1-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="191a1-239">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="191a1-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="191a1-240">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="191a1-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="191a1-242">**tooassign Britta Simon tooCisco Spark, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="191a1-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="191a1-243">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="191a1-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="191a1-245">Dans la liste des applications hello, sélectionnez **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="191a1-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="191a1-247">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="191a1-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="191a1-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="191a1-249">Click **Add** button.</span></span> <span data-ttu-id="191a1-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="191a1-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="191a1-252">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="191a1-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="191a1-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="191a1-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="191a1-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="191a1-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="191a1-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="191a1-255">Testing single sign-on</span></span>

<span data-ttu-id="191a1-256">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="191a1-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="191a1-257">Lorsque vous cliquez sur mosaïque de Cisco Spark hello Bonjour volet d’accès, vous devez obtenir l’application de Cisco Spark automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="191a1-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="191a1-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="191a1-258">Additional resources</span></span>

* [<span data-ttu-id="191a1-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="191a1-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="191a1-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="191a1-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

