---
title: "Didacticiel : Intégration d’Azure Active Directory avec FilesAnywhere | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="43fb8-103">Didacticiel : Intégration d’Azure Active Directory à FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="43fb8-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="43fb8-104">Dans ce didacticiel, vous apprendrez comment toointegrate FilesAnywhere avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43fb8-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43fb8-105">Intégration FilesAnywhere à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="43fb8-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="43fb8-106">Vous pouvez contrôler dans Azure AD qui a accès tooFilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="43fb8-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="43fb8-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFilesAnywhere (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43fb8-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="43fb8-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="43fb8-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43fb8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43fb8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="43fb8-110">Prerequisites</span></span>

<span data-ttu-id="43fb8-111">tooconfigure intégration d’Azure AD avec FilesAnywhere, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="43fb8-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="43fb8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43fb8-113">Un abonnement FilesAnywhere pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="43fb8-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="43fb8-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="43fb8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="43fb8-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="43fb8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43fb8-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="43fb8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="43fb8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43fb8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="43fb8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="43fb8-118">Scenario description</span></span>
<span data-ttu-id="43fb8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="43fb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43fb8-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="43fb8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43fb8-121">Ajout de FilesAnywhere à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="43fb8-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="43fb8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="43fb8-123">Ajout de FilesAnywhere à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="43fb8-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="43fb8-124">intégration de hello tooconfigure de FilesAnywhere dans Azure AD, vous devez tooadd FilesAnywhere à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="43fb8-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="43fb8-125">**tooadd FilesAnywhere à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="43fb8-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fb8-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="43fb8-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43fb8-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="43fb8-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="43fb8-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="43fb8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="43fb8-133">Dans la zone de recherche de hello, tapez **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="43fb8-135">Dans le volet de résultats hello, sélectionnez **FilesAnywhere**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="43fb8-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43fb8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43fb8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FilesAnywhere, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="43fb8-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="43fb8-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FilesAnywhere est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43fb8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="43fb8-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FilesAnywhere doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="43fb8-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="43fb8-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="43fb8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="43fb8-142">tooconfigure et test Azure AD l’authentification unique avec FilesAnywhere, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="43fb8-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="43fb8-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="43fb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="43fb8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43fb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43fb8-145">**[Création d’un utilisateur de test FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave de Britta Simon dans FilesAnywhere qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="43fb8-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="43fb8-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="43fb8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="43fb8-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="43fb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43fb8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43fb8-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="43fb8-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="43fb8-150">**tooconfigure Azure AD single sign-on avec FilesAnywhere, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="43fb8-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fb8-151">Dans le portail de gestion Azure hello, sur hello **FilesAnywhere** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="43fb8-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="43fb8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="43fb8-155">Sur hello **FilesAnywhere domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**:</span><span class="sxs-lookup"><span data-stu-id="43fb8-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="43fb8-157">a.</span><span class="sxs-lookup"><span data-stu-id="43fb8-157">a.</span></span> <span data-ttu-id="43fb8-158">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="43fb8-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="43fb8-159">Remarque Cette valeur hello **215** est un **clientid** et est juste un exemple.</span><span class="sxs-lookup"><span data-stu-id="43fb8-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="43fb8-160">Vous devez tooreplace avec la valeur de clientid réel hello.</span><span class="sxs-lookup"><span data-stu-id="43fb8-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="43fb8-161">Sur hello **FilesAnywhere domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="43fb8-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="43fb8-163">a.</span><span class="sxs-lookup"><span data-stu-id="43fb8-163">a.</span></span> <span data-ttu-id="43fb8-164">Cliquez sur hello **afficher les paramètres d’URL avancés** option</span><span class="sxs-lookup"><span data-stu-id="43fb8-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="43fb8-165">b.</span><span class="sxs-lookup"><span data-stu-id="43fb8-165">b.</span></span> <span data-ttu-id="43fb8-166">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="43fb8-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="43fb8-167">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="43fb8-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="43fb8-168">Vous avez tooupdate ces valeurs avec URL hello URL de connexion et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="43fb8-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="43fb8-169">Contact [équipe de support FilesAnywhere](mailto:support@FilesAnywhere.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="43fb8-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="43fb8-170">Application logicielle de FilesAnywhere attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="43fb8-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="43fb8-171">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="43fb8-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="43fb8-172">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="43fb8-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="43fb8-173">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="43fb8-173">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="43fb8-175">Hello lorsque les utilisateurs inscrit avec FilesAnywhere ils obtenir valeur hello **clientid** d’attribut de [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="43fb8-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="43fb8-176">Vous disposez d’attribut de « Id Client » hello tooadd hello unique valeur fournie par FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="43fb8-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="43fb8-177">Tous les attributs présentés ci-dessus sont requis.</span><span class="sxs-lookup"><span data-stu-id="43fb8-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="43fb8-178">Remarque Cette valeur hello **2331** de **clientid** est juste un exemple.</span><span class="sxs-lookup"><span data-stu-id="43fb8-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="43fb8-179">Vous devez la valeur réelle de tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="43fb8-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="43fb8-180">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="43fb8-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="43fb8-181">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="43fb8-181">Attribute Name</span></span> | <span data-ttu-id="43fb8-182">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="43fb8-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="43fb8-183">clientid</span><span class="sxs-lookup"><span data-stu-id="43fb8-183">clientid</span></span> | <span data-ttu-id="43fb8-184">*« uniquevalue »*</span><span class="sxs-lookup"><span data-stu-id="43fb8-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="43fb8-185">a.</span><span class="sxs-lookup"><span data-stu-id="43fb8-185">a.</span></span> <span data-ttu-id="43fb8-186">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="43fb8-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="43fb8-189">b.</span><span class="sxs-lookup"><span data-stu-id="43fb8-189">b.</span></span> <span data-ttu-id="43fb8-190">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="43fb8-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="43fb8-191">c.</span><span class="sxs-lookup"><span data-stu-id="43fb8-191">c.</span></span> <span data-ttu-id="43fb8-192">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="43fb8-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="43fb8-193">d.</span><span class="sxs-lookup"><span data-stu-id="43fb8-193">d.</span></span> <span data-ttu-id="43fb8-194">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-194">Click **Ok**</span></span>

7. <span data-ttu-id="43fb8-195">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="43fb8-195">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="43fb8-197">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="43fb8-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="43fb8-199">Sur hello **FilesAnywhere Configuration** , cliquez sur **FilesAnywhere de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="43fb8-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="43fb8-202">configuration de SSO tooget complète pour votre application à fin FilesAnywhere, contactez [équipe de support FilesAnywhere](mailto:support@FilesAnywhere.com) et fournir les URL d’authentification unique (SSO) et de certificat de signature de jetons SAML de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="43fb8-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43fb8-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="43fb8-204">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43fb8-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="43fb8-206">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="43fb8-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fb8-207">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="43fb8-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43fb8-209">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="43fb8-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43fb8-211">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="43fb8-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43fb8-213">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="43fb8-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43fb8-215">a.</span><span class="sxs-lookup"><span data-stu-id="43fb8-215">a.</span></span> <span data-ttu-id="43fb8-216">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43fb8-217">b.</span><span class="sxs-lookup"><span data-stu-id="43fb8-217">b.</span></span> <span data-ttu-id="43fb8-218">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43fb8-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43fb8-219">c.</span><span class="sxs-lookup"><span data-stu-id="43fb8-219">c.</span></span> <span data-ttu-id="43fb8-220">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="43fb8-221">d.</span><span class="sxs-lookup"><span data-stu-id="43fb8-221">d.</span></span> <span data-ttu-id="43fb8-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="43fb8-223">Création d’un utilisateur de test FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="43fb8-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="43fb8-224">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="43fb8-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="43fb8-225">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="43fb8-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="43fb8-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooFilesAnywhere de son accès.</span><span class="sxs-lookup"><span data-stu-id="43fb8-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="43fb8-228">**tooassign Britta Simon tooFilesAnywhere, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="43fb8-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="43fb8-229">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="43fb8-231">Dans la liste des applications hello, sélectionnez **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="43fb8-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="43fb8-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-235">Click **Add** button.</span></span> <span data-ttu-id="43fb8-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="43fb8-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="43fb8-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="43fb8-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43fb8-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="43fb8-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="43fb8-241">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="43fb8-241">Testing single sign-on</span></span>

<span data-ttu-id="43fb8-242">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="43fb8-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="43fb8-243">Lorsque vous cliquez sur mosaïque FilesAnywhere hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour FilesAnywhere application.</span><span class="sxs-lookup"><span data-stu-id="43fb8-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="43fb8-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="43fb8-244">Additional resources</span></span>

* [<span data-ttu-id="43fb8-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43fb8-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43fb8-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="43fb8-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
