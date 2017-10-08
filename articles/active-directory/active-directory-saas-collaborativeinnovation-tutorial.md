---
title: "Didacticiel : intégration d’Azure Active Directory à Collaborative Innovation | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de collaboration de l’Innovation."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="f5aae-103">Didacticiel : intégration d’Azure Active Directory à Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="f5aae-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="f5aae-104">Dans ce didacticiel, vous apprendrez comment toointegrate Innovation collaboration avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5aae-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5aae-105">Intégration Innovation collaboration avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f5aae-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f5aae-106">Vous pouvez contrôler dans Azure AD qui a accès tooCollaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="f5aae-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="f5aae-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCollaborative Innovation (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5aae-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f5aae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f5aae-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5aae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5aae-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f5aae-110">Prerequisites</span></span>

<span data-ttu-id="f5aae-111">tooconfigure intégration d’Azure AD avec l’Innovation collaboration, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f5aae-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="f5aae-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5aae-113">Un abonnement Collaborative Innovation pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f5aae-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5aae-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f5aae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5aae-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f5aae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5aae-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f5aae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5aae-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5aae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5aae-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f5aae-118">Scenario description</span></span>
<span data-ttu-id="f5aae-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f5aae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5aae-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f5aae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5aae-121">Ajout d’Innovation de collaboration à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f5aae-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="f5aae-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="f5aae-123">Ajout d’Innovation de collaboration à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f5aae-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="f5aae-124">tooconfigure hello intégration de collaboration Innovation dans Azure AD, vous devez tooadd Innovation collaboration à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f5aae-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f5aae-125">**tooadd Innovation collaboration à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5aae-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5aae-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f5aae-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5aae-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f5aae-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f5aae-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f5aae-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f5aae-133">Dans la zone de recherche de hello, tapez **Innovation collaboration**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="f5aae-135">Dans le volet de résultats hello, sélectionnez **Innovation collaboration**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f5aae-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5aae-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5aae-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Collaborative Innovation avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f5aae-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f5aae-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Innovation collaboration est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5aae-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="f5aae-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur en matière d’Innovation collaboration hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f5aae-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="f5aae-141">Collaboration de l’innovation en affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="f5aae-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f5aae-142">tooconfigure et test Azure AD l’authentification unique avec l’Innovation collaboration, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f5aae-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f5aae-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f5aae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f5aae-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5aae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5aae-145">**[Création d’un utilisateur de test de l’Innovation collaboration](#creating-a-collaborative-innovation-test-user)**  -toohave un équivalent de Britta Simon innovation collaboratif qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f5aae-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5aae-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f5aae-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5aae-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f5aae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5aae-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5aae-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="f5aae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="f5aae-150">**tooconfigure Azure AD authentification unique avec la collaboration d’Innovation, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5aae-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5aae-151">Bonjour portail Azure, sur hello **Innovation collaboration** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f5aae-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f5aae-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="f5aae-155">Sur hello **URL et domaine de l’Innovation collaboration** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5aae-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="f5aae-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5aae-157">a.</span></span> <span data-ttu-id="f5aae-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="f5aae-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="f5aae-159">b.</span><span class="sxs-lookup"><span data-stu-id="f5aae-159">b.</span></span> <span data-ttu-id="f5aae-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="f5aae-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f5aae-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f5aae-161">These values are not real.</span></span> <span data-ttu-id="f5aae-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="f5aae-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5aae-163">Contact [équipe de support Client de collaboration Innovation](https://www.unilever.com/contact/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f5aae-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="f5aae-164">Application Innovation collaborative attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="f5aae-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f5aae-165">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="f5aae-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="f5aae-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="f5aae-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f5aae-167">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="f5aae-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="f5aae-169">Cliquez sur **afficher et modifier tous les autres attributs utilisateur** case à cocher Bonjour **attributs utilisateur** tooexpand hello attributs de section.</span><span class="sxs-lookup"><span data-stu-id="f5aae-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="f5aae-170">Effectuer hello comme suit sur chaque hello affichée les attributs-</span><span class="sxs-lookup"><span data-stu-id="f5aae-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="f5aae-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="f5aae-171">Attribute Name</span></span> | <span data-ttu-id="f5aae-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="f5aae-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="f5aae-173">givenname</span><span class="sxs-lookup"><span data-stu-id="f5aae-173">givenname</span></span> | <span data-ttu-id="f5aae-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f5aae-174">user.givenname</span></span> |
    | <span data-ttu-id="f5aae-175">surname</span><span class="sxs-lookup"><span data-stu-id="f5aae-175">surname</span></span> | <span data-ttu-id="f5aae-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="f5aae-176">user.surname</span></span> |
    | <span data-ttu-id="f5aae-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="f5aae-177">emailaddress</span></span> | <span data-ttu-id="f5aae-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f5aae-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="f5aae-179">name</span><span class="sxs-lookup"><span data-stu-id="f5aae-179">name</span></span> | <span data-ttu-id="f5aae-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f5aae-180">user.userprincipalname</span></span> |

    <span data-ttu-id="f5aae-181">a.</span><span class="sxs-lookup"><span data-stu-id="f5aae-181">a.</span></span> <span data-ttu-id="f5aae-182">Cliquez sur hello de hello attribut tooopen **modifier l’attribut** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f5aae-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="f5aae-184">b.</span><span class="sxs-lookup"><span data-stu-id="f5aae-184">b.</span></span> <span data-ttu-id="f5aae-185">Supprimer la valeur d’URL de hello de hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="f5aae-186">c.</span><span class="sxs-lookup"><span data-stu-id="f5aae-186">c.</span></span> <span data-ttu-id="f5aae-187">Cliquez sur **Ok** paramètre hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="f5aae-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="f5aae-188">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f5aae-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="f5aae-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f5aae-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f5aae-192">tooconfigure l’authentification unique sur **Innovation collaboration** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support de collaboration Innovation](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f5aae-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="f5aae-193">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="f5aae-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f5aae-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f5aae-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f5aae-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f5aae-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f5aae-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5aae-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5aae-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5aae-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f5aae-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f5aae-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5aae-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5aae-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f5aae-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5aae-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5aae-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f5aae-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5aae-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5aae-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5aae-209">a.</span><span class="sxs-lookup"><span data-stu-id="f5aae-209">a.</span></span> <span data-ttu-id="f5aae-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5aae-211">b.</span><span class="sxs-lookup"><span data-stu-id="f5aae-211">b.</span></span> <span data-ttu-id="f5aae-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f5aae-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5aae-213">c.</span><span class="sxs-lookup"><span data-stu-id="f5aae-213">c.</span></span> <span data-ttu-id="f5aae-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f5aae-215">d.</span><span class="sxs-lookup"><span data-stu-id="f5aae-215">d.</span></span> <span data-ttu-id="f5aae-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="f5aae-217">Création d’un utilisateur de test Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="f5aae-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="f5aae-218">tooenable Azure AD les utilisateurs toolog dans tooCollaborative Innovation, vous devez les configurer en collaboration Innovation.</span><span class="sxs-lookup"><span data-stu-id="f5aae-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="f5aae-219">En cas de cette application mise en service est automatique prend en charge de l’application hello juste-à-temps l’approvisionnement des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f5aae-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="f5aae-220">Il n’est donc aucune tooperform nécessaire ici toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="f5aae-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f5aae-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5aae-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f5aae-222">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCollaborative l’Innovation.</span><span class="sxs-lookup"><span data-stu-id="f5aae-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f5aae-224">**tooassign Britta Simon tooCollaborative Innovation, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5aae-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="f5aae-225">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f5aae-227">Dans la liste des applications hello, sélectionnez **Innovation collaboration**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="f5aae-229">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f5aae-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-231">Click **Add** button.</span></span> <span data-ttu-id="f5aae-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f5aae-234">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f5aae-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f5aae-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5aae-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f5aae-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5aae-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f5aae-237">Testing single sign-on</span></span>

<span data-ttu-id="f5aae-238">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f5aae-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f5aae-239">Lorsque vous cliquez sur mosaïque de collaboration Innovation hello Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application de collaboration Innovation.</span><span class="sxs-lookup"><span data-stu-id="f5aae-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="f5aae-240">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5aae-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f5aae-241">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f5aae-241">Additional resources</span></span>

* [<span data-ttu-id="f5aae-242">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5aae-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5aae-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f5aae-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

