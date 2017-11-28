---
title: "Didacticiel : Intégration d’Azure Active Directory à Rally Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="29d6a-103">Didacticiel : Intégration d’Azure Active Directory à Rally Software</span><span class="sxs-lookup"><span data-stu-id="29d6a-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="29d6a-104">Dans ce didacticiel, vous apprendrez comment toointegrate Rally de logiciel avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29d6a-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29d6a-105">Intégration Rally Software à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="29d6a-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="29d6a-106">Vous pouvez contrôler dans Azure AD qui a accès tooRally logiciel.</span><span class="sxs-lookup"><span data-stu-id="29d6a-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="29d6a-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRally logiciels (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29d6a-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="29d6a-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29d6a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="29d6a-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29d6a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29d6a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="29d6a-110">Prerequisites</span></span>

<span data-ttu-id="29d6a-111">tooconfigure intégration d’Azure AD à Rally Software, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29d6a-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="29d6a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29d6a-113">Un abonnement Rally Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="29d6a-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29d6a-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="29d6a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29d6a-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="29d6a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29d6a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29d6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29d6a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29d6a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29d6a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="29d6a-118">Scenario description</span></span>
<span data-ttu-id="29d6a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="29d6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29d6a-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="29d6a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29d6a-121">Ajout de Rally Software à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29d6a-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="29d6a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="29d6a-123">Ajout de Rally Software à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29d6a-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="29d6a-124">tooconfigure hello intégration de Rally Software dans Azure AD, vous devez tooadd Rally Software à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="29d6a-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29d6a-125">**tooadd Rally le logiciel à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d6a-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d6a-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="29d6a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="29d6a-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="29d6a-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="29d6a-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="29d6a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="29d6a-133">Dans la zone de recherche de hello, tapez **Rally Software**, sélectionnez **Rally Software** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="29d6a-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Rally Software dans la liste des résultats hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29d6a-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d6a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="29d6a-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Rally Software à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="29d6a-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29d6a-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Rally Software est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29d6a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="29d6a-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Rally Software doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="29d6a-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="29d6a-139">Dans Rally Software, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="29d6a-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="29d6a-140">tooconfigure et test Azure AD l’authentification unique avec Rally Software, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="29d6a-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29d6a-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="29d6a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29d6a-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29d6a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29d6a-143">**[Créer un utilisateur de test Rally Software](#create-a-rally-software-test-user)**  -toohave un équivalent de Britta Simon dans Rally Software qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29d6a-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="29d6a-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29d6a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29d6a-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="29d6a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29d6a-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d6a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29d6a-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Rally Software.</span><span class="sxs-lookup"><span data-stu-id="29d6a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="29d6a-148">**tooconfigure Azure AD single sign-on avec Rally Software, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d6a-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d6a-149">Bonjour portail Azure, sur hello **Rally Software** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="29d6a-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29d6a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="29d6a-153">Sur hello **URL et le domaine de logiciel Rally** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d6a-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="29d6a-155">a.</span><span class="sxs-lookup"><span data-stu-id="29d6a-155">a.</span></span> <span data-ttu-id="29d6a-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="29d6a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="29d6a-157">b.</span><span class="sxs-lookup"><span data-stu-id="29d6a-157">b.</span></span> <span data-ttu-id="29d6a-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="29d6a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29d6a-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="29d6a-159">These values are not real.</span></span> <span data-ttu-id="29d6a-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="29d6a-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="29d6a-161">Contact [équipe de support Client de logiciel Rally](https://help.rallydev.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="29d6a-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="29d6a-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="29d6a-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="29d6a-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="29d6a-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29d6a-166">Sur hello **Rally la Configuration logicielle** , cliquez sur **configurer Rally Software** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="29d6a-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="29d6a-167">Hello de copie **URL de déconnexion et l’ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="29d6a-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuration de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="29d6a-169">Connectez-vous à tooyour **Rally Software** client.</span><span class="sxs-lookup"><span data-stu-id="29d6a-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="29d6a-170">Dans la barre d’outils de hello en haut de hello, cliquez sur **le programme d’installation**, puis sélectionnez **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="29d6a-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span><span class="sxs-lookup"><span data-stu-id="29d6a-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="29d6a-172">Cliquez sur hello **Action** bouton.</span><span class="sxs-lookup"><span data-stu-id="29d6a-172">Click hello **Action** button.</span></span> <span data-ttu-id="29d6a-173">Sélectionnez **modifier un abonnement** à hello haut à droite de la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="29d6a-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="29d6a-174">Sur hello **abonnement** page de boîte de dialogue, effectuer hello comme suit, puis cliquez sur **Enregistrer & fermer**:</span><span class="sxs-lookup"><span data-stu-id="29d6a-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="29d6a-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="29d6a-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="29d6a-176">a.</span><span class="sxs-lookup"><span data-stu-id="29d6a-176">a.</span></span> <span data-ttu-id="29d6a-177">Sélectionnez **Rally or SSO authentication** dans la liste déroulante Authentication.</span><span class="sxs-lookup"><span data-stu-id="29d6a-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="29d6a-178">b.</span><span class="sxs-lookup"><span data-stu-id="29d6a-178">b.</span></span> <span data-ttu-id="29d6a-179">Bonjour **URL du fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29d6a-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="29d6a-180">c.</span><span class="sxs-lookup"><span data-stu-id="29d6a-180">c.</span></span> <span data-ttu-id="29d6a-181">Bonjour **déconnexion de SSO** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29d6a-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="29d6a-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="29d6a-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="29d6a-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="29d6a-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="29d6a-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29d6a-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29d6a-185">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d6a-185">Create an Azure AD test user</span></span>

<span data-ttu-id="29d6a-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="29d6a-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="29d6a-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d6a-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d6a-189">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="29d6a-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29d6a-191">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29d6a-193">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="29d6a-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29d6a-195">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d6a-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29d6a-197">a.</span><span class="sxs-lookup"><span data-stu-id="29d6a-197">a.</span></span> <span data-ttu-id="29d6a-198">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29d6a-199">b.</span><span class="sxs-lookup"><span data-stu-id="29d6a-199">b.</span></span> <span data-ttu-id="29d6a-200">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29d6a-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="29d6a-201">c.</span><span class="sxs-lookup"><span data-stu-id="29d6a-201">c.</span></span> <span data-ttu-id="29d6a-202">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="29d6a-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="29d6a-203">d.</span><span class="sxs-lookup"><span data-stu-id="29d6a-203">d.</span></span> <span data-ttu-id="29d6a-204">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="29d6a-205">Créer un utilisateur de test Rally Software</span><span class="sxs-lookup"><span data-stu-id="29d6a-205">Create a Rally Software test user</span></span>

<span data-ttu-id="29d6a-206">Pour Azure AD les utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application Rally Software à l’aide de leur nom d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29d6a-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="29d6a-207">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d6a-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d6a-208">Ouvrez une session dans tooyour client Rally Software.</span><span class="sxs-lookup"><span data-stu-id="29d6a-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="29d6a-209">Accédez trop**le programme d’installation \> utilisateurs**, puis cliquez sur **+ ajouter un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="29d6a-210">![Utilisateurs](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="29d6a-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="29d6a-211">Nom de hello dans la zone de texte hello nouvel utilisateur, puis tapez **ajouter avec des détails**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="29d6a-212">Bonjour **Create User** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d6a-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="29d6a-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="29d6a-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="29d6a-214">a.</span><span class="sxs-lookup"><span data-stu-id="29d6a-214">a.</span></span> <span data-ttu-id="29d6a-215">Bonjour **nom d’utilisateur** zone de texte, nom d’utilisateur comme hello du type **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="29d6a-216">b.</span><span class="sxs-lookup"><span data-stu-id="29d6a-216">b.</span></span> <span data-ttu-id="29d6a-217">Dans **adresse de messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="29d6a-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="29d6a-218">c.</span><span class="sxs-lookup"><span data-stu-id="29d6a-218">c.</span></span> <span data-ttu-id="29d6a-219">Dans **prénom** texte, entrez le nom d’utilisateur comme hello **Brian**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="29d6a-220">d.</span><span class="sxs-lookup"><span data-stu-id="29d6a-220">d.</span></span> <span data-ttu-id="29d6a-221">Dans **nom** texte, entrez le nom d’utilisateur comme hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="29d6a-222">e.</span><span class="sxs-lookup"><span data-stu-id="29d6a-222">e.</span></span> <span data-ttu-id="29d6a-223">Cliquez sur **Enregistrer et fermer**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="29d6a-224">Vous pouvez utiliser n’importe quel autre Rally Software utilisateur compte outil de création ou API fournie par Rally Software tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29d6a-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="29d6a-225">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d6a-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="29d6a-226">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRally logiciel.</span><span class="sxs-lookup"><span data-stu-id="29d6a-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="29d6a-228">**tooassign Britta Simon tooRally logiciel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d6a-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d6a-229">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="29d6a-231">Dans la liste des applications hello, sélectionnez **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-231">In hello applications list, select **Rally Software**.</span></span>

    ![lien de Rally Software Hello dans la liste des Applications hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="29d6a-233">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="29d6a-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-235">Click **Add** button.</span></span> <span data-ttu-id="29d6a-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="29d6a-238">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="29d6a-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="29d6a-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29d6a-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="29d6a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29d6a-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29d6a-241">Test single sign-on</span></span>

<span data-ttu-id="29d6a-242">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29d6a-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="29d6a-243">Lorsque vous cliquez sur mosaïque Rally Software hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Rally Software.</span><span class="sxs-lookup"><span data-stu-id="29d6a-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29d6a-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="29d6a-244">Additional resources</span></span>

* [<span data-ttu-id="29d6a-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29d6a-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29d6a-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="29d6a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

