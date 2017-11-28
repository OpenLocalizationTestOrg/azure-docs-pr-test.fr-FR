---
title: "Didacticiel : Intégration d’Azure Active Directory avec eKincare | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="c8c3f-103">Didacticiel : Intégration d’Azure Active Directory avec eKincare</span><span class="sxs-lookup"><span data-stu-id="c8c3f-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="c8c3f-104">Dans ce didacticiel, vous apprendrez comment eKincare toointegrate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8c3f-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8c3f-105">Intégration eKincare à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8c3f-106">Vous pouvez contrôler dans Azure AD qui a accès tooeKincare</span><span class="sxs-lookup"><span data-stu-id="c8c3f-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="c8c3f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooeKincare (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8c3f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c8c3f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c8c3f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8c3f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8c3f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c8c3f-110">Prerequisites</span></span>

<span data-ttu-id="c8c3f-111">tooconfigure intégration d’Azure AD avec eKincare, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="c8c3f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8c3f-113">Un abonnement eKincare pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c8c3f-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8c3f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8c3f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8c3f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8c3f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8c3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8c3f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c8c3f-118">Scenario description</span></span>
<span data-ttu-id="c8c3f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8c3f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8c3f-121">Ajout d’eKincare à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c8c3f-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="c8c3f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="c8c3f-123">Ajout d’eKincare à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c8c3f-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="c8c3f-124">intégration de hello tooconfigure d’eKincare dans Azure AD, vous devez eKincare tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8c3f-125">**eKincare tooadd à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8c3f-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8c3f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8c3f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8c3f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c8c3f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c8c3f-133">Dans la zone de recherche de hello, tapez **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-133">In hello search box, type **eKincare**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="c8c3f-135">Dans le volet de résultats hello, sélectionnez **eKincare**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8c3f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8c3f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec eKincare, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c8c3f-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c8c3f-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans eKincare est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="c8c3f-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans eKincare doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="c8c3f-141">Dans eKincare, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c8c3f-142">tooconfigure et test Azure AD l’authentification unique avec eKincare, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8c3f-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8c3f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8c3f-145">**[Création d’un utilisateur de test eKincare](#creating-a-ekincare-test-user)**  -toohave un homologue de Britta Simon dans eKincare est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8c3f-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8c3f-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8c3f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8c3f-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application eKincare.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="c8c3f-150">**tooconfigure Azure AD single sign-on avec eKincare, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8c3f-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8c3f-151">Bonjour portail Azure, sur hello **eKincare** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c8c3f-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="c8c3f-155">Sur hello **eKincare domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="c8c3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-157">a.</span></span> <span data-ttu-id="c8c3f-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="c8c3f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="c8c3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-159">b.</span></span> <span data-ttu-id="c8c3f-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="c8c3f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8c3f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-161">These values are not real.</span></span> <span data-ttu-id="c8c3f-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c8c3f-163">Contact [équipe de support eKincare](mailto:tech@ekincare.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="c8c3f-164">eKincare application attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c8c3f-165">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="c8c3f-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c8c3f-167">Hello suivant capture d’écran montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="c8c3f-168">Hello nom de la revendication sera toujours **« employeeid »** et la valeur hello dont nous avons mappé toouser.extensionattribute1, qui contient l’employeeid hello d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="c8c3f-169">ex : nom Hello autres deux revendications</span><span class="sxs-lookup"><span data-stu-id="c8c3f-169">hello other two claims' name i.e</span></span> <span data-ttu-id="c8c3f-170">**« organizationid »** et **« NomOrganisation »** sera toujours même et leurs valeurs contiennent respectivement les détails de hello d’organisation hello d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="c8c3f-172">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c8c3f-173">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="c8c3f-173">Attribute Name</span></span> | <span data-ttu-id="c8c3f-174">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="c8c3f-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="c8c3f-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="c8c3f-175">employeeid</span></span> | <span data-ttu-id="c8c3f-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="c8c3f-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="c8c3f-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="c8c3f-177">organizationid</span></span> | <span data-ttu-id="c8c3f-178">*« uniquevalue »*</span><span class="sxs-lookup"><span data-stu-id="c8c3f-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="c8c3f-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="c8c3f-179">organizationname</span></span> | <span data-ttu-id="c8c3f-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="c8c3f-180">*user.companyname*</span></span> |

    <span data-ttu-id="c8c3f-181">a.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-181">a.</span></span> <span data-ttu-id="c8c3f-182">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="c8c3f-185">b.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-185">b.</span></span> <span data-ttu-id="c8c3f-186">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c8c3f-187">c.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-187">c.</span></span> <span data-ttu-id="c8c3f-188">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c8c3f-189">d.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-189">d.</span></span> <span data-ttu-id="c8c3f-190">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-190">Click **Ok**</span></span>

6. <span data-ttu-id="c8c3f-191">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="c8c3f-193">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c8c3f-193">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c8c3f-195">tooconfigure l’authentification unique sur **eKincare** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="c8c3f-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="c8c3f-196">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c8c3f-197">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="c8c3f-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c8c3f-198">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c8c3f-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8c3f-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8c3f-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8c3f-201">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c8c3f-203">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8c3f-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8c3f-204">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8c3f-206">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8c3f-208">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8c3f-210">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8c3f-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8c3f-212">a.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-212">a.</span></span> <span data-ttu-id="c8c3f-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8c3f-214">b.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-214">b.</span></span> <span data-ttu-id="c8c3f-215">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8c3f-216">c.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-216">c.</span></span> <span data-ttu-id="c8c3f-217">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c8c3f-218">d.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-218">d.</span></span> <span data-ttu-id="c8c3f-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="c8c3f-220">Création d’un utilisateur de test eKincare</span><span class="sxs-lookup"><span data-stu-id="c8c3f-220">Creating a eKincare test user</span></span>

<span data-ttu-id="c8c3f-221">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c8c3f-222">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8c3f-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c8c3f-223">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooeKincare.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c8c3f-225">**tooassign Britta Simon tooeKincare, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c8c3f-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8c3f-226">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c8c3f-228">Dans la liste des applications hello, sélectionnez **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-228">In hello applications list, select **eKincare**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="c8c3f-230">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c8c3f-232">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-232">Click **Add** button.</span></span> <span data-ttu-id="c8c3f-233">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c8c3f-235">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8c3f-236">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8c3f-237">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8c3f-238">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c8c3f-238">Testing single sign-on</span></span>

<span data-ttu-id="c8c3f-239">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c8c3f-240">Lorsque vous cliquez sur mosaïque eKincare hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour eKincare application.</span><span class="sxs-lookup"><span data-stu-id="c8c3f-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="c8c3f-241">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello panneau d’accès](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c8c3f-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8c3f-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c8c3f-242">Additional resources</span></span>

* [<span data-ttu-id="c8c3f-243">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8c3f-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8c3f-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c8c3f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

