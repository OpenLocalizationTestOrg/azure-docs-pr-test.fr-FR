---
title: "Didacticiel : Intégration d’Azure Active Directory dans M-Files | Documentation Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et des millions de fichiers."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="17342-103">Didacticiel : Intégration d’Azure AD à M-Files</span><span class="sxs-lookup"><span data-stu-id="17342-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="17342-104">Dans ce didacticiel, vous apprendrez comment toointegrate millions de fichiers avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17342-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17342-105">Intégration des millions de fichiers avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="17342-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17342-106">Vous pouvez contrôler dans Azure AD qui a accès aux fichiers tooM</span><span class="sxs-lookup"><span data-stu-id="17342-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="17342-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooM-fichiers (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17342-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="17342-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17342-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17342-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17342-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="17342-110">Prerequisites</span></span>

<span data-ttu-id="17342-111">tooconfigure intégration d’Azure AD avec des millions de fichiers, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="17342-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="17342-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17342-113">Un abonnement à M-Files pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="17342-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17342-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="17342-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17342-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="17342-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17342-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="17342-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17342-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17342-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17342-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="17342-118">Scenario description</span></span>
<span data-ttu-id="17342-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="17342-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17342-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="17342-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17342-121">Ajout des millions de fichiers à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="17342-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="17342-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="17342-123">Ajout des millions de fichiers à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="17342-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="17342-124">tooconfigure hello intégration des millions de fichiers dans Azure AD, vous devez tooadd millions de fichiers à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="17342-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17342-125">**tooadd millions de fichiers à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17342-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17342-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="17342-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17342-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="17342-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17342-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="17342-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="17342-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="17342-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="17342-133">Dans la zone de recherche de hello, tapez **millions de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="17342-133">In hello search box, type **M-Files**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="17342-135">Dans le volet de résultats hello, sélectionnez **millions de fichiers**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="17342-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17342-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17342-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec M-Files avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="17342-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17342-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les fichiers de M est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17342-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="17342-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les fichiers de M hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="17342-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="17342-141">Dans les fichiers-M, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="17342-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="17342-142">tooconfigure et test Azure AD l’authentification unique avec des millions de fichiers, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="17342-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17342-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="17342-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17342-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17342-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17342-145">**[Création d’un utilisateur de test de millions de fichiers](#creating-a-m-files-test-user)**  -toohave un équivalent de Britta Simon dans des millions de fichiers qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="17342-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17342-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="17342-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17342-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="17342-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17342-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17342-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de millions de fichiers.</span><span class="sxs-lookup"><span data-stu-id="17342-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="17342-150">**tooconfigure Azure AD authentification unique avec des millions de fichiers, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17342-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="17342-151">Bonjour portail Azure, sur hello **millions de fichiers** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="17342-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="17342-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="17342-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="17342-155">Sur hello **domaine des millions de fichiers et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="17342-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="17342-157">a.</span><span class="sxs-lookup"><span data-stu-id="17342-157">a.</span></span> <span data-ttu-id="17342-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="17342-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="17342-159">b.</span><span class="sxs-lookup"><span data-stu-id="17342-159">b.</span></span> <span data-ttu-id="17342-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="17342-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17342-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="17342-161">These values are not real.</span></span> <span data-ttu-id="17342-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="17342-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="17342-163">Contact [équipe de support Client de millions de fichiers](mailto:support@m-files.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="17342-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="17342-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="17342-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="17342-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="17342-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17342-168">tooget l’authentification unique configurée pour votre application, contactez [équipe de support des millions de fichiers](mailto:support@m-files.com) et les fournir hello téléchargé les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="17342-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="17342-169">Suivez les instructions hello si vous souhaitez tooconfigure SSO pour vous, application de bureau M de fichier.</span><span class="sxs-lookup"><span data-stu-id="17342-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="17342-170">Aucune étape supplémentaire est requise si vous souhaitez uniquement tooconfigure l’authentification unique pour la version web de millions de fichiers.</span><span class="sxs-lookup"><span data-stu-id="17342-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="17342-171">Suivez hello suivant étapes tooconfigure hello M-fichier application de bureau tooenable SSO avec AD Azure.</span><span class="sxs-lookup"><span data-stu-id="17342-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="17342-172">toodownload millions de fichiers, accédez trop[millions de fichiers téléchargement](https://www.m-files.com/en/download-latest-version) page.</span><span class="sxs-lookup"><span data-stu-id="17342-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="17342-173">Ouvrez hello **paramètres du bureau millions de fichiers** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="17342-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="17342-174">Cliquez ensuite sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="17342-174">Then, click **Add**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="17342-176">Sur hello **propriétés de connexion de coffre Document** fenêtre, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="17342-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="17342-178">Sous type de serveur de section de hello, hello valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="17342-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="17342-179">a.</span><span class="sxs-lookup"><span data-stu-id="17342-179">a.</span></span> <span data-ttu-id="17342-180">Pour **Nom**, saisissez `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="17342-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="17342-181">b.</span><span class="sxs-lookup"><span data-stu-id="17342-181">b.</span></span> <span data-ttu-id="17342-182">Pour **Numéro de port**, saisissez **4466**.</span><span class="sxs-lookup"><span data-stu-id="17342-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="17342-183">c.</span><span class="sxs-lookup"><span data-stu-id="17342-183">c.</span></span> <span data-ttu-id="17342-184">Pour **Protocole**, sélectionnez **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="17342-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="17342-185">d.</span><span class="sxs-lookup"><span data-stu-id="17342-185">d.</span></span> <span data-ttu-id="17342-186">Bonjour **authentification** champ, sélectionnez **utilisateur Windows spécifique**.</span><span class="sxs-lookup"><span data-stu-id="17342-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="17342-187">Ensuite, une page de signature s’affiche.</span><span class="sxs-lookup"><span data-stu-id="17342-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="17342-188">Entrez vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17342-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="17342-189">e.</span><span class="sxs-lookup"><span data-stu-id="17342-189">e.</span></span> <span data-ttu-id="17342-190">Pourquoi **coffre sur serveur**, sélectionnez hello coffre correspondant sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="17342-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="17342-191">f.</span><span class="sxs-lookup"><span data-stu-id="17342-191">f.</span></span> <span data-ttu-id="17342-192">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="17342-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="17342-193">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="17342-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17342-194">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="17342-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17342-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17342-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17342-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="17342-197">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="17342-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="17342-199">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17342-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17342-200">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="17342-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17342-202">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="17342-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17342-204">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="17342-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17342-206">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="17342-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17342-208">a.</span><span class="sxs-lookup"><span data-stu-id="17342-208">a.</span></span> <span data-ttu-id="17342-209">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17342-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17342-210">b.</span><span class="sxs-lookup"><span data-stu-id="17342-210">b.</span></span> <span data-ttu-id="17342-211">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17342-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17342-212">c.</span><span class="sxs-lookup"><span data-stu-id="17342-212">c.</span></span> <span data-ttu-id="17342-213">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="17342-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17342-214">d.</span><span class="sxs-lookup"><span data-stu-id="17342-214">d.</span></span> <span data-ttu-id="17342-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="17342-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="17342-216">Création d’un utilisateur de test M-Files</span><span class="sxs-lookup"><span data-stu-id="17342-216">Creating a M-Files test user</span></span>

<span data-ttu-id="17342-217">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans les fichiers de M.</span><span class="sxs-lookup"><span data-stu-id="17342-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="17342-218">Travailler avec [équipe de support des millions de fichiers](mailto:support@m-files.com) utilisateurs hello tooadd hello millions de fichiers.</span><span class="sxs-lookup"><span data-stu-id="17342-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17342-219">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17342-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17342-220">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès aux fichiers tooM.</span><span class="sxs-lookup"><span data-stu-id="17342-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="17342-222">**tooassign Britta Simon tooM-Files, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17342-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="17342-223">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="17342-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="17342-225">Dans la liste des applications hello, sélectionnez **millions de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="17342-225">In hello applications list, select **M-Files**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="17342-227">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="17342-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="17342-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="17342-229">Click **Add** button.</span></span> <span data-ttu-id="17342-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="17342-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="17342-232">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="17342-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17342-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="17342-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17342-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="17342-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17342-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="17342-235">Testing single sign-on</span></span>

<span data-ttu-id="17342-236">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="17342-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="17342-237">Lorsque vous cliquez sur hello millions de fichiers vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour millions de fichiers application.</span><span class="sxs-lookup"><span data-stu-id="17342-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17342-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="17342-238">Additional resources</span></span>

* [<span data-ttu-id="17342-239">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17342-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17342-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="17342-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

