---
title: "Didacticiel : intégration d’Azure Active Directory à IQNavigator VMS | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et IQNavigator VMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="9ff23-103">Didacticiel : intégration d’Azure Active Directory à IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="9ff23-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="9ff23-104">Dans ce didacticiel, vous apprendrez comment toointegrate VMS IQNavigator avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ff23-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ff23-105">Intégration IQNavigator VMS à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9ff23-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9ff23-106">Vous pouvez contrôler dans Azure AD qui a accès tooIQNavigator machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9ff23-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="9ff23-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIQNavigator machines virtuelles (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ff23-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9ff23-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9ff23-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ff23-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ff23-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9ff23-110">Prerequisites</span></span>

<span data-ttu-id="9ff23-111">tooconfigure intégration d’Azure AD avec IQNavigator VMS, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9ff23-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="9ff23-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ff23-113">Un abonnement IQNavigator VMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9ff23-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ff23-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9ff23-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ff23-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9ff23-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ff23-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9ff23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ff23-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ff23-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ff23-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9ff23-118">Scenario description</span></span>
<span data-ttu-id="9ff23-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9ff23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ff23-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9ff23-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ff23-121">Ajout de IQNavigator VMS à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9ff23-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="9ff23-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="9ff23-123">Ajout de IQNavigator VMS à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9ff23-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="9ff23-124">intégration de hello tooconfigure de IQNavigator VMS dans Azure AD, vous devez tooadd IQNavigator VMS à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9ff23-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9ff23-125">**tooadd VMS IQNavigator à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9ff23-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ff23-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9ff23-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ff23-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9ff23-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9ff23-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9ff23-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9ff23-133">Dans la zone de recherche de hello, tapez **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="9ff23-135">Dans le volet de résultats hello, sélectionnez **IQNavigator VMS**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9ff23-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ff23-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ff23-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD à IQNavigator VMS basé sur un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9ff23-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ff23-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello IQNavigator VMS est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ff23-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="9ff23-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans IQNavigator VMS doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9ff23-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="9ff23-141">Dans IQNavigator VMS, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9ff23-142">tooconfigure et test Azure AD l’authentification unique avec IQNavigator VMS, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9ff23-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9ff23-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9ff23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9ff23-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ff23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ff23-145">**[Création d’un utilisateur de test IQNavigator VMS](#creating-a-iqnavigator-vms-test-user)**  -toohave un équivalent de Britta Simon dans VMS IQNavigator qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9ff23-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ff23-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9ff23-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ff23-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9ff23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ff23-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ff23-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="9ff23-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="9ff23-150">**tooconfigure Azure AD single sign-on avec IQNavigator VMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9ff23-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ff23-151">Bonjour portail Azure, sur hello **IQNavigator VMS** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9ff23-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9ff23-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="9ff23-155">Sur hello **URL et le domaine des ordinateurs virtuels IQNavigator** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9ff23-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="9ff23-157">a.</span><span class="sxs-lookup"><span data-stu-id="9ff23-157">a.</span></span> <span data-ttu-id="9ff23-158">Bonjour **identificateur** zone de texte, tapez l’URL hello :`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="9ff23-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="9ff23-159">b.</span><span class="sxs-lookup"><span data-stu-id="9ff23-159">b.</span></span> <span data-ttu-id="9ff23-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="9ff23-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="9ff23-161">Vérifiez **afficher les paramètres d’URL avancés**, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="9ff23-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="9ff23-163">Bonjour **état de relais** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="9ff23-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ff23-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9ff23-164">These values are not real.</span></span> <span data-ttu-id="9ff23-165">Mettre à jour ces valeurs avec l’état réel de relais et les URL de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="9ff23-166">Contact [équipe de support Client de machines virtuelles IQNavigator](https://www.beeline.com/iqn-product-support/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="9ff23-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="9ff23-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9ff23-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ff23-169">toogenerate hello **métadonnées** url, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9ff23-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="9ff23-170">a.</span><span class="sxs-lookup"><span data-stu-id="9ff23-170">a.</span></span> <span data-ttu-id="9ff23-171">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-171">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="9ff23-173">b.</span><span class="sxs-lookup"><span data-stu-id="9ff23-173">b.</span></span> <span data-ttu-id="9ff23-174">Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9ff23-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="9ff23-176">c.</span><span class="sxs-lookup"><span data-stu-id="9ff23-176">c.</span></span> <span data-ttu-id="9ff23-177">Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="9ff23-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="9ff23-179">d.</span><span class="sxs-lookup"><span data-stu-id="9ff23-179">d.</span></span> <span data-ttu-id="9ff23-180">Maintenant accédez toohello page de propriétés de **IQNavigator VMS** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="9ff23-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="9ff23-182">e.</span><span class="sxs-lookup"><span data-stu-id="9ff23-182">e.</span></span> <span data-ttu-id="9ff23-183">Générer hello **URL de métadonnées** hello suivant le modèle à l’aide de :`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="9ff23-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="9ff23-184">D’application IQNavigator attendre la valeur de l’identificateur hello utilisateur unique dans la revendication d’identificateur de nom hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="9ff23-185">Client peut mapper la valeur correcte de hello pour une revendication d’identificateur de nom hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="9ff23-186">Dans ce cas, nous avons mappé utilisateur de hello. UserPrincipalName fins de démonstration hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="9ff23-187">Mais, en fonction des paramètres de l’organisation de tooyour, vous devez mapper valeur correcte de hello pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="9ff23-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="9ff23-189">Sur hello **Configuration des machines virtuelles IQNavigator** , cliquez sur **configurer des machines virtuelles IQNavigator** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9ff23-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9ff23-190">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="9ff23-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="9ff23-192">tooconfigure l’authentification unique sur **IQNavigator VMS** côté, vous devez toosend hello **URL de métadonnées**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop [Équipe de support IQNavigator VMS](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="9ff23-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="9ff23-193">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="9ff23-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9ff23-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="9ff23-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9ff23-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9ff23-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ff23-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ff23-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ff23-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9ff23-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9ff23-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9ff23-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ff23-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="9ff23-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ff23-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ff23-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ff23-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9ff23-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ff23-209">a.</span><span class="sxs-lookup"><span data-stu-id="9ff23-209">a.</span></span> <span data-ttu-id="9ff23-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ff23-211">b.</span><span class="sxs-lookup"><span data-stu-id="9ff23-211">b.</span></span> <span data-ttu-id="9ff23-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9ff23-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ff23-213">c.</span><span class="sxs-lookup"><span data-stu-id="9ff23-213">c.</span></span> <span data-ttu-id="9ff23-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9ff23-215">d.</span><span class="sxs-lookup"><span data-stu-id="9ff23-215">d.</span></span> <span data-ttu-id="9ff23-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="9ff23-217">Création d’un utilisateur de test IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="9ff23-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="9ff23-218">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="9ff23-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="9ff23-219">Travailler avec [équipe de support IQNavigator VMS](https://www.beeline.com/iqn-product-support/) utilisateurs hello tooadd hello compte de IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="9ff23-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9ff23-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ff23-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9ff23-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIQNavigator machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9ff23-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9ff23-223">**tooassign Britta Simon tooIQNavigator machines virtuelles, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9ff23-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ff23-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9ff23-226">Dans la liste des applications hello, sélectionnez **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="9ff23-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9ff23-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-230">Click **Add** button.</span></span> <span data-ttu-id="9ff23-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9ff23-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="9ff23-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9ff23-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ff23-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9ff23-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ff23-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9ff23-236">Testing single sign-on</span></span>

<span data-ttu-id="9ff23-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9ff23-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9ff23-238">Lorsque vous cliquez sur hello vignette IQNavigator VMS Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="9ff23-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="9ff23-239">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9ff23-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ff23-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9ff23-240">Additional resources</span></span>

* [<span data-ttu-id="9ff23-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ff23-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ff23-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9ff23-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

