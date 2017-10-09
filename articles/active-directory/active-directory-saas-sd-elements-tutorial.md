---
title: "Didacticiel : Intégration d’Azure Active Directory à SD Elements | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les éléments de SD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="f3165-103">Didacticiel : Intégration d’Azure Active Directory à SD Elements</span><span class="sxs-lookup"><span data-stu-id="f3165-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="f3165-104">Dans ce didacticiel, vous apprendrez comment toointegrate éléments SD avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3165-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3165-105">Intégrer des éléments de SD avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f3165-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f3165-106">Vous pouvez contrôler dans Azure AD qui a accès tooSD éléments</span><span class="sxs-lookup"><span data-stu-id="f3165-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="f3165-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSD éléments (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3165-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f3165-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f3165-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3165-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3165-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f3165-110">Prerequisites</span></span>

<span data-ttu-id="f3165-111">tooconfigure intégration d’Azure AD avec des éléments de SD, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f3165-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="f3165-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3165-113">Un abonnement SD Elements pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f3165-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3165-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f3165-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3165-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f3165-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3165-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f3165-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3165-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3165-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3165-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f3165-118">Scenario description</span></span>
<span data-ttu-id="f3165-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f3165-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3165-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f3165-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3165-121">Ajout d’éléments à partir de la galerie de hello SD</span><span class="sxs-lookup"><span data-stu-id="f3165-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="f3165-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="f3165-123">Ajout d’éléments à partir de la galerie de hello SD</span><span class="sxs-lookup"><span data-stu-id="f3165-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="f3165-124">tooconfigure hello intégration d’éléments de SD dans Azure AD, vous devez tooadd SD éléments à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f3165-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f3165-125">**tooadd éléments SD à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f3165-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3165-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f3165-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3165-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f3165-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f3165-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f3165-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f3165-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f3165-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f3165-133">Dans la zone de recherche de hello, tapez **SD éléments**.</span><span class="sxs-lookup"><span data-stu-id="f3165-133">In hello search box, type **SD Elements**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="f3165-135">Dans le volet de résultats hello, sélectionnez **SD éléments**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f3165-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3165-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3165-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SD Elements sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f3165-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3165-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les éléments SD est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3165-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="f3165-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les éléments SD hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f3165-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="f3165-141">Dans les éléments SD, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f3165-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f3165-142">tooconfigure et test Azure AD l’authentification unique avec des éléments de SD, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f3165-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f3165-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f3165-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f3165-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3165-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3165-145">**[Création d’un utilisateur de test SD éléments](#creating-a-sd-elements-test-user)**  -toohave un équivalent de Britta Simon dans les éléments de SD qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f3165-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3165-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f3165-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3165-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f3165-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3165-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3165-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SD éléments.</span><span class="sxs-lookup"><span data-stu-id="f3165-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="f3165-150">**tooconfigure Azure AD authentification unique avec les éléments SD, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f3165-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3165-151">Bonjour portail Azure, sur hello **SD éléments** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f3165-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f3165-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f3165-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="f3165-155">Sur hello **URL et le domaine d’éléments SD** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3165-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="f3165-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3165-157">a.</span></span> <span data-ttu-id="f3165-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="f3165-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="f3165-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3165-159">b.</span></span> <span data-ttu-id="f3165-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="f3165-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3165-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f3165-161">These values are not real.</span></span> <span data-ttu-id="f3165-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="f3165-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f3165-163">Contact [équipe de support technique SD éléments](mailto:support@sdelements.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f3165-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="f3165-164">Application des éléments de SD attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="f3165-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f3165-165">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="f3165-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="f3165-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Attribut utilisateur »** onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f3165-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="f3165-167">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="f3165-167">hello following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="f3165-169">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3165-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="f3165-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="f3165-170">Attribute Name</span></span> | <span data-ttu-id="f3165-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="f3165-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f3165-172">email</span><span class="sxs-lookup"><span data-stu-id="f3165-172">email</span></span> |<span data-ttu-id="f3165-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="f3165-173">user.mail</span></span> |
    | <span data-ttu-id="f3165-174">firstname</span><span class="sxs-lookup"><span data-stu-id="f3165-174">firstname</span></span> |<span data-ttu-id="f3165-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f3165-175">user.givenname</span></span> |
    | <span data-ttu-id="f3165-176">lastname</span><span class="sxs-lookup"><span data-stu-id="f3165-176">lastname</span></span> |<span data-ttu-id="f3165-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="f3165-177">user.surname</span></span> |

    <span data-ttu-id="f3165-178">a.</span><span class="sxs-lookup"><span data-stu-id="f3165-178">a.</span></span> <span data-ttu-id="f3165-179">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f3165-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="f3165-182">b.</span><span class="sxs-lookup"><span data-stu-id="f3165-182">b.</span></span> <span data-ttu-id="f3165-183">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="f3165-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="f3165-184">c.</span><span class="sxs-lookup"><span data-stu-id="f3165-184">c.</span></span> <span data-ttu-id="f3165-185">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="f3165-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="f3165-186">d.</span><span class="sxs-lookup"><span data-stu-id="f3165-186">d.</span></span> <span data-ttu-id="f3165-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3165-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="f3165-188">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f3165-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="f3165-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f3165-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f3165-192">Sur hello **Configuration des éléments SD** , cliquez sur **configurer les éléments SD** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f3165-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f3165-193">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f3165-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="f3165-195">tooget l’authentification unique activée, contactez votre [équipe de support technique SD éléments](mailto:support@sdelements.com) et leur fournir un fichier de certificat téléchargé hello.</span><span class="sxs-lookup"><span data-stu-id="f3165-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="f3165-196">Dans une autre fenêtre de navigateur, client de SD éléments tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f3165-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="f3165-197">Dans le menu hello haut de hello, cliquez sur **système**, puis **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f3165-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="f3165-199">Sur hello **paramètres d’authentification unique** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3165-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="f3165-201">a.</span><span class="sxs-lookup"><span data-stu-id="f3165-201">a.</span></span> <span data-ttu-id="f3165-202">Pour **SSO Type**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f3165-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="f3165-203">b.</span><span class="sxs-lookup"><span data-stu-id="f3165-203">b.</span></span> <span data-ttu-id="f3165-204">Bonjour **Entity ID fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f3165-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="f3165-205">c.</span><span class="sxs-lookup"><span data-stu-id="f3165-205">c.</span></span> <span data-ttu-id="f3165-206">Bonjour **Service fournisseur d’identité unique Sign-On** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f3165-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="f3165-207">d.</span><span class="sxs-lookup"><span data-stu-id="f3165-207">d.</span></span> <span data-ttu-id="f3165-208">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f3165-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f3165-209">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f3165-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f3165-210">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f3165-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f3165-211">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3165-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3165-212">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3165-213">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f3165-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f3165-215">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f3165-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3165-216">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f3165-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3165-218">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f3165-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3165-220">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f3165-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3165-222">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3165-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3165-224">a.</span><span class="sxs-lookup"><span data-stu-id="f3165-224">a.</span></span> <span data-ttu-id="f3165-225">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3165-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3165-226">b.</span><span class="sxs-lookup"><span data-stu-id="f3165-226">b.</span></span> <span data-ttu-id="f3165-227">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f3165-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3165-228">c.</span><span class="sxs-lookup"><span data-stu-id="f3165-228">c.</span></span> <span data-ttu-id="f3165-229">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f3165-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f3165-230">d.</span><span class="sxs-lookup"><span data-stu-id="f3165-230">d.</span></span> <span data-ttu-id="f3165-231">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f3165-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="f3165-232">Création d'un utilisateur de test SD Elements</span><span class="sxs-lookup"><span data-stu-id="f3165-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="f3165-233">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans les éléments SD.</span><span class="sxs-lookup"><span data-stu-id="f3165-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="f3165-234">Dans les cas de hello d’éléments de SD, la création d’éléments de SD utilisateurs est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="f3165-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="f3165-235">**toocreate Britta Simon SD éléments effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f3165-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3165-236">Dans une fenêtre de navigateur web, site d’entreprise SD éléments tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f3165-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="f3165-237">Dans le menu hello haut de hello, cliquez sur **gestion des utilisateurs**, puis **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f3165-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![Création d'un utilisateur de test SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="f3165-239">Cliquez sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="f3165-239">Click **Add New User**.</span></span>
   
    ![Création d'un utilisateur de test SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="f3165-241">Sur hello **ajouter un nouvel utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3165-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![Création d'un utilisateur de test SD Elements](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="f3165-243">a.</span><span class="sxs-lookup"><span data-stu-id="f3165-243">a.</span></span> <span data-ttu-id="f3165-244">Bonjour **messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f3165-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="f3165-245">b.</span><span class="sxs-lookup"><span data-stu-id="f3165-245">b.</span></span> <span data-ttu-id="f3165-246">Bonjour **prénom** zone de texte, entrez hello premier nom d’utilisateur comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="f3165-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="f3165-247">c.</span><span class="sxs-lookup"><span data-stu-id="f3165-247">c.</span></span> <span data-ttu-id="f3165-248">Bonjour **nom** zone de texte, entrez le nom d’utilisateur comme hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f3165-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="f3165-249">d.</span><span class="sxs-lookup"><span data-stu-id="f3165-249">d.</span></span> <span data-ttu-id="f3165-250">Pour **Role**, sélectionnez **User**.</span><span class="sxs-lookup"><span data-stu-id="f3165-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="f3165-251">e.</span><span class="sxs-lookup"><span data-stu-id="f3165-251">e.</span></span> <span data-ttu-id="f3165-252">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="f3165-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f3165-253">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3165-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f3165-254">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès à des éléments de tooSD.</span><span class="sxs-lookup"><span data-stu-id="f3165-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f3165-256">**tooassign Britta Simon tooSD éléments, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f3165-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3165-257">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f3165-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f3165-259">Dans la liste des applications hello, sélectionnez **SD éléments**.</span><span class="sxs-lookup"><span data-stu-id="f3165-259">In hello applications list, select **SD Elements**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="f3165-261">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f3165-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f3165-263">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f3165-263">Click **Add** button.</span></span> <span data-ttu-id="f3165-264">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f3165-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f3165-266">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f3165-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f3165-267">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f3165-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3165-268">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f3165-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3165-269">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f3165-269">Testing single sign-on</span></span>

<span data-ttu-id="f3165-270">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f3165-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="f3165-271">Lorsque vous cliquez sur hello SD éléments vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application des éléments de SD.</span><span class="sxs-lookup"><span data-stu-id="f3165-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3165-272">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f3165-272">Additional resources</span></span>

* [<span data-ttu-id="f3165-273">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3165-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3165-274">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f3165-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

