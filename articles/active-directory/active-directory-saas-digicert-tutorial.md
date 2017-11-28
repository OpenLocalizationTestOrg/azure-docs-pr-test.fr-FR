---
title: "Didacticiel : Intégration d’Azure Active Directory à DigiCert | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="7e01d-103">Didacticiel : Intégration d’Azure Active Directory à DigiCert</span><span class="sxs-lookup"><span data-stu-id="7e01d-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="7e01d-104">Dans ce didacticiel, vous apprendrez comment toointegrate DigiCert avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e01d-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e01d-105">Intégration DigiCert à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7e01d-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e01d-106">Vous pouvez contrôler dans Azure AD qui a accès tooDigiCert</span><span class="sxs-lookup"><span data-stu-id="7e01d-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="7e01d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDigiCert (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e01d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7e01d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e01d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e01d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e01d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7e01d-110">Prerequisites</span></span>

<span data-ttu-id="7e01d-111">tooconfigure intégration d’Azure AD avec DigiCert, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7e01d-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="7e01d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e01d-113">Un abonnement DigiCert pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7e01d-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e01d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7e01d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e01d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="7e01d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e01d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7e01d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e01d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e01d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e01d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7e01d-118">Scenario description</span></span>
<span data-ttu-id="7e01d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7e01d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e01d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="7e01d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e01d-121">Ajout de DigiCert à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7e01d-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="7e01d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="7e01d-123">Ajout de DigiCert à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="7e01d-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="7e01d-124">tooconfigure hello intégration de DigiCert dans Azure AD, vous devez tooadd DigiCert à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7e01d-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e01d-125">**tooadd DigiCert à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7e01d-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e01d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7e01d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e01d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e01d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7e01d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7e01d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7e01d-133">Dans la zone de recherche de hello, tapez **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-133">In hello search box, type **DigiCert**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="7e01d-135">Dans le volet de résultats hello, sélectionnez **DigiCert**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7e01d-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e01d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e01d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec DigiCert à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7e01d-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e01d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello DigiCert est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e01d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="7e01d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans DigiCert doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="7e01d-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="7e01d-141">Dans DigiCert, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="7e01d-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e01d-142">tooconfigure et test Azure AD l’authentification unique avec DigiCert, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="7e01d-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e01d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7e01d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e01d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e01d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e01d-145">**[Création d’un utilisateur de test DigiCert](#creating-a-digicert-test-user)**  -toohave un équivalent de Britta Simon dans DigiCert est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7e01d-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e01d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7e01d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e01d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="7e01d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e01d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e01d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7e01d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="7e01d-150">**tooconfigure Azure AD single sign-on avec DigiCert, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7e01d-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e01d-151">Bonjour portail Azure, sur hello **DigiCert** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7e01d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7e01d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="7e01d-155">Sur hello **DigiCert domaine et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="7e01d-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="7e01d-157">DigiCert application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="7e01d-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="7e01d-158">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="7e01d-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="7e01d-159">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="7e01d-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7e01d-160">Hello suivant capture d’écran montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="7e01d-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="7e01d-162">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e01d-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="7e01d-163">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="7e01d-163">Attribute Name</span></span> | <span data-ttu-id="7e01d-164">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="7e01d-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7e01d-165">société</span><span class="sxs-lookup"><span data-stu-id="7e01d-165">company</span></span> | <span data-ttu-id="7e01d-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="7e01d-166">< companycode ></span></span> |
    | <span data-ttu-id="7e01d-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="7e01d-167">digicertrole</span></span> | <span data-ttu-id="7e01d-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="7e01d-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="7e01d-169">Hello valeur **société** attribut n’est pas réel.</span><span class="sxs-lookup"><span data-stu-id="7e01d-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="7e01d-170">Mettez à jour cette valeur avec le code de la société réel.</span><span class="sxs-lookup"><span data-stu-id="7e01d-170">Update this value with actual company code.</span></span> <span data-ttu-id="7e01d-171">valeur hello tooget **société** attribut contact [équipe de support DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="7e01d-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="7e01d-172">a.</span><span class="sxs-lookup"><span data-stu-id="7e01d-172">a.</span></span> <span data-ttu-id="7e01d-173">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7e01d-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7e01d-176">b.</span><span class="sxs-lookup"><span data-stu-id="7e01d-176">b.</span></span> <span data-ttu-id="7e01d-177">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7e01d-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7e01d-178">c.</span><span class="sxs-lookup"><span data-stu-id="7e01d-178">c.</span></span> <span data-ttu-id="7e01d-179">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7e01d-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7e01d-180">d.</span><span class="sxs-lookup"><span data-stu-id="7e01d-180">d.</span></span> <span data-ttu-id="7e01d-181">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="7e01d-182">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7e01d-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="7e01d-184">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7e01d-184">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7e01d-186">tooconfigure l’authentification unique sur **DigiCert** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="7e01d-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="7e01d-187">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="7e01d-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7e01d-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="7e01d-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e01d-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="7e01d-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e01d-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e01d-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e01d-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e01d-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="7e01d-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7e01d-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7e01d-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e01d-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="7e01d-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e01d-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e01d-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="7e01d-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e01d-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e01d-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e01d-203">a.</span><span class="sxs-lookup"><span data-stu-id="7e01d-203">a.</span></span> <span data-ttu-id="7e01d-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e01d-205">b.</span><span class="sxs-lookup"><span data-stu-id="7e01d-205">b.</span></span> <span data-ttu-id="7e01d-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e01d-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e01d-207">c.</span><span class="sxs-lookup"><span data-stu-id="7e01d-207">c.</span></span> <span data-ttu-id="7e01d-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7e01d-209">d.</span><span class="sxs-lookup"><span data-stu-id="7e01d-209">d.</span></span> <span data-ttu-id="7e01d-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="7e01d-211">Création d’un utilisateur de test DigiCert</span><span class="sxs-lookup"><span data-stu-id="7e01d-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="7e01d-212">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7e01d-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="7e01d-213">Collaborez avec [équipe de support DigiCert](mailto:support@digicert.com) utilisateurs hello tooadd DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7e01d-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7e01d-214">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e01d-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7e01d-215">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDigiCert.</span><span class="sxs-lookup"><span data-stu-id="7e01d-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7e01d-217">**tooassign Britta Simon tooDigiCert, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7e01d-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e01d-218">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7e01d-220">Dans la liste des applications hello, sélectionnez **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-220">In hello applications list, select **DigiCert**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="7e01d-222">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7e01d-224">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-224">Click **Add** button.</span></span> <span data-ttu-id="7e01d-225">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7e01d-227">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7e01d-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e01d-228">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e01d-229">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7e01d-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e01d-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7e01d-230">Testing single sign-on</span></span>

<span data-ttu-id="7e01d-231">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="7e01d-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e01d-232">Lorsque vous cliquez sur mosaïque DigiCert hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour DeigiCert application.</span><span class="sxs-lookup"><span data-stu-id="7e01d-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="7e01d-233">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e01d-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e01d-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7e01d-234">Additional resources</span></span>

* [<span data-ttu-id="7e01d-235">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e01d-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e01d-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7e01d-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

