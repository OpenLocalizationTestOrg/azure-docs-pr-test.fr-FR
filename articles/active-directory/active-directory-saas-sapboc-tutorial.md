---
title: "Didacticiel : Intégration d’Azure Active Directory avec SAP Business Object Cloud | Microsoft Docs)"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP Business objet Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="2d9b1-103">Didacticiel : Intégration d’Azure Active Directory avec SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="2d9b1-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="2d9b1-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAP Cloud d’objet métier avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d9b1-105">Vous obtenez hello avantages suivants lorsque vous intégrez SAP Business objet Cloud avec Azure AD :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="2d9b1-106">Dans Azure AD, vous pouvez contrôler qui a accès tooSAP Cloud d’objet métier.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="2d9b1-107">Vous pouvez signer automatiquement dans votre tooSAP utilisateurs Cloud d’objet métier à l’aide de l’authentification unique et un compte d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="2d9b1-108">Vous pouvez gérer vos comptes dans un emplacement central, hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="2d9b1-109">toolearn savoir plus sur le logiciel en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d9b1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2d9b1-110">Prerequisites</span></span>

<span data-ttu-id="2d9b1-111">tooset d’intégration avec SAP Business objet Cloud d’Azure AD, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="2d9b1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d9b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d9b1-113">SAP Business Object Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2d9b1-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="2d9b1-114">Si vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas les tester dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="2d9b1-115">Recommandations pour le test des étapes de hello dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="2d9b1-116">N’utilisez pas votre environnement de production, à moins que cela ne soit nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="2d9b1-117">Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [obtenir un essai gratuit d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d9b1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2d9b1-118">Scenario description</span></span>
<span data-ttu-id="2d9b1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="2d9b1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d9b1-121">Ajouter des SAP Business objet Cloud à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="2d9b1-122">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="2d9b1-123">Ajouter des SAP Business objet Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2d9b1-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="2d9b1-124">tooset intégration hello de SAP Business objet Cloud avec Azure AD, dans la galerie hello, ajouter la liste de tooyour SAP Business objet Cloud des applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d9b1-125">tooadd SAP Business objet Cloud à partir de la galerie de hello :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="2d9b1-126">Bonjour [portail Azure](https://portal.azure.com)hello du menu de gauche, dans Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="2d9b1-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![page des applications Enterprise Hello][2]
    
3. <span data-ttu-id="2d9b1-130">tooadd une nouvelle application, sélectionnez **nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-130">tooadd a new application, select **New application**.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="2d9b1-132">Dans la zone de recherche de hello, entrez **SAP Business objet Cloud**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![zone de recherche Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="2d9b1-134">Dans le volet de résultats hello, sélectionnez **SAP Business objet Cloud**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![Liste des résultats de SAP Business objet Cloud Bonjour](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2d9b1-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d9b1-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="2d9b1-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Business Object Cloud, grâce à un utilisateur de test appelé *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="2d9b1-138">Pour toowork de l’authentification unique, Azure AD doit utilisateur d’homologue tooknow hello Azure AD dans SAP Business objet Cloud.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="2d9b1-139">Une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP Business objet Cloud doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="2d9b1-140">relation, dans SAP Business objet Cloud, de liens tooestablish hello pour **nom d’utilisateur**, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="2d9b1-141">tooconfigure et test Azure AD l’authentification unique avec le Cloud d’objet SAP Business, hello complète tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="2d9b1-142">[Configurer l’authentification unique Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="2d9b1-143">Définit un toouse utilisateur cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="2d9b1-144">[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="2d9b1-145">Tests AD Azure authentification unique avec l’utilisateur hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="2d9b1-146">[Créer un utilisateur de test pour SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="2d9b1-147">Crée un équivalent de Britta Simon dans SAP Business objet Cloud qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="2d9b1-148">[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="2d9b1-149">Définit les toouse Britta Simon Azure AD l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d9b1-150">[Tester l’authentification unique](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="2d9b1-151">Vérifie que la configuration hello fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="2d9b1-152">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d9b1-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="2d9b1-153">Dans cette section, vous activez Azure AD unique signe sur Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="2d9b1-154">Ensuite, configurez l’authentification unique dans votre application SAP Business objet Cloud.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="2d9b1-155">tooset d’Azure AD single sign-on avec SAP Business objet Cloud :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="2d9b1-156">Bonjour portail Azure, sur hello **SAP Business objet Cloud** page d’intégration d’application, sélectionnez **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Sélectionner l’authentification unique][4]

2. <span data-ttu-id="2d9b1-158">Sur hello **l’authentification unique** page, pour **Mode**, sélectionnez **SAML-authentification**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Sélectionner l’authentification basée sur SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="2d9b1-160">Sous **URL et le domaine de SAP Business objet Cloud**complète hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="2d9b1-161">Bonjour **URL de connexion** , entrez une URL qui pointe hello modèle :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="2d9b1-162">Bonjour **identificateur** , entrez une URL qui pointe hello modèle :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL de la page URL et domaine SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="2d9b1-164">les valeurs Hello dans ces URL sont fins de démonstration uniquement.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="2d9b1-165">Mise à jour des valeurs de hello avec hello réel authentification URL URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="2d9b1-166">tooget hello URL de connexion, contact hello [équipe de support SAP Business objet Cloud Client](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="2d9b1-167">Vous pouvez obtenir l’URL d’identificateur hello en téléchargeant des métadonnées du Cloud d’objet SAP Business hello à partir de la console d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="2d9b1-168">Cela est expliqué plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="2d9b1-169">Sous **le certificat de signature SAML**, sélectionnez **XML des métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="2d9b1-170">Ensuite, enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-170">Then, save hello metadata file on your computer.</span></span>

    ![Sélectionnez XML des métadonnées](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="2d9b1-172">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-172">Select **Save**.</span></span>

    ![Sélectionner Enregistrer](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d9b1-174">Dans une fenêtre de navigateur web, connectez-vous dans un site d’entreprise tooyour SAP Business objet Cloud en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="2d9b1-175">Sélectionnez **Menu** > **Système** > **Administration**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Sélectionner Menu, puis Système et Administration](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="2d9b1-177">Sur hello **sécurité** onglet, sélectionnez hello **modifier** icône (stylet).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Sur l’onglet sécurité de hello, sélectionnez l’icône de modification hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="2d9b1-179">Sélectionnez **Méthode d’authentification unique SAML (SSO)** comme **Méthode d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Sélectionnez SAML Single Sign-On pour la méthode d’authentification hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="2d9b1-181">toodownload hello fournisseur métadonnées de service (étape 1), sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="2d9b1-182">Dans le fichier de métadonnées hello, recherchez et copiez hello **entityID** valeur.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="2d9b1-183">Bonjour Azure portail, sous **URL et le domaine de SAP Business objet Cloud**, collez la valeur de hello Bonjour **identificateur** boîte.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Copiez et collez la valeur entityID de hello](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="2d9b1-185">tooupload hello fournisseur métadonnées de service (étape 2) dans le fichier hello que vous avez téléchargé à partir de hello portail Azure, sous **les métadonnées de télécharger le fournisseur d’identité**, sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Sous Charger les métadonnées du fournisseur d’identité, sélectionnez Charger](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="2d9b1-187">Bonjour **attribut utilisateur** répertorier, attribut d’utilisateur Sélectionnez hello (étape 3) que vous souhaitez toouse pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="2d9b1-188">Cet attribut utilisateur mappe toohello fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="2d9b1-189">tooenter un attribut personnalisé sur la page de l’utilisateur hello, utilisez hello **de mappage SAML personnalisées** option.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="2d9b1-190">Ou bien, vous pouvez sélectionner **messagerie** ou **ID utilisateur** en tant qu’attribut de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="2d9b1-191">Dans notre exemple, nous avons sélectionné **messagerie** , car nous avons mappé la revendication d’identificateur hello utilisateur avec hello **userprincipalname** attribut Bonjour **attributs utilisateur** section Bonjour Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="2d9b1-192">Cela fournit une messagerie de l’utilisateur unique, ce qui est envoyé toohello application SAP Business objet Cloud chaque réponse SAML correcte.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Sélectionner un attribut utilisateur](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="2d9b1-194">compte de hello tooverify avec le fournisseur d’identité (étape 4), hello Bonjour **informations d’identification de connexion (courrier électronique)** , entrez l’adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="2d9b1-195">Ensuite, sélectionnez **Vérifier le compte**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="2d9b1-196">système de Hello ajoute le compte d’utilisateur toohello informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Entrer l’e-mail et sélectionner Vérifier le compte](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="2d9b1-198">Sélectionnez hello **enregistrer** icône.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-198">Select hello **Save** icon.</span></span>

    ![Icône Enregistrer](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="2d9b1-200">Vous pouvez lire une version concise de ces instructions Bonjour [portail Azure](https://portal.azure.com), alors que vous configurez votre application !</span><span class="sxs-lookup"><span data-stu-id="2d9b1-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="2d9b1-201">Après avoir ajouté l’application hello en sélectionnant **Active Directory** > **des Applications d’entreprise**, sélectionnez hello **Single Sign-On** onglet. Vous pouvez accéder à documentation hello incorporé Bonjour **Configuration** section, au bas de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="2d9b1-202">Pour plus d’informations, consultez la page [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2d9b1-203">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d9b1-203">Create an Azure AD test user</span></span>
<span data-ttu-id="2d9b1-204">Dans cette section, vous créez un utilisateur de test nommé Britta Simon Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="2d9b1-205">toocreate un utilisateur test dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="2d9b1-206">Bonjour portail Azure, dans le menu de gauche hello, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d9b1-208">liste de hello toodisplay d’utilisateurs, sélectionnez **utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d9b1-210">tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d9b1-212">Bonjour **utilisateur** boîte de dialogue, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="2d9b1-213">Bonjour **nom** , entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="2d9b1-214">Bonjour **nom d’utilisateur** , entrez l’adresse de messagerie hello de l’utilisateur hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="2d9b1-215">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="2d9b1-216">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-216">Select **Create**.</span></span>

        ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Créer un utilisateur Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="2d9b1-219">Créer un utilisateur de test SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="2d9b1-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="2d9b1-220">Les utilisateurs Active Directory Azure doivent être configurés dans le Cloud d’objet SAP Business pour pouvoir se connecter dans tooSAP Cloud d’objet métier.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="2d9b1-221">Dans SAP Business Object Cloud, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="2d9b1-222">tooprovision un compte d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="2d9b1-223">Se connecter tooyour site SAP Business objet Cloud d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="2d9b1-224">Sélectionnez **Menu** > **Sécurité** > **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="2d9b1-226">Sur hello **utilisateurs** , tooadd nouveau détails d’utilisateur, sélectionnez  **+** .</span><span class="sxs-lookup"><span data-stu-id="2d9b1-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Page Ajouter des utilisateurs](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="2d9b1-228">Ensuite, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="2d9b1-229">Bonjour **ID utilisateur** , entrez le code hello d’utilisateur de hello, tel que **Brian**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="2d9b1-230">Bonjour **prénom** , entrez le nom d’utilisateur de hello, hello comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="2d9b1-231">Bonjour **nom** , entrez le nom d’utilisateur de hello, hello comme **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="2d9b1-232">Bonjour **nom d’affichage** zone, entrez le nom complet de hello d’utilisateur de hello, tel que **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="2d9b1-233">Bonjour **messagerie** zone, entrez les adresse de messagerie hello d’utilisateur de hello, tel que  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2d9b1-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="2d9b1-234">Sur hello **sélectionner des rôles** page, sélectionnez hello le rôle approprié pour l’utilisateur de hello, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Sélectionner un rôle](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="2d9b1-236">Sélectionnez hello **enregistrer** icône.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2d9b1-237">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d9b1-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2d9b1-238">Dans cette section, vous permettre à l’utilisateur hello Britta Simon toouse Azure AD l’authentification unique en accordant hello utilisateur compte accès tooSAP Cloud d’objet métier.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="2d9b1-239">tooassign Britta Simon tooSAP Cloud d’objet métier :</span><span class="sxs-lookup"><span data-stu-id="2d9b1-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="2d9b1-240">Bonjour portail Azure, ouvrez la vue des applications hello et passez toohello vue d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="2d9b1-241">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2d9b1-243">Dans la liste des applications hello, sélectionnez **SAP Business objet Cloud**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="2d9b1-245">Dans le menu de gauche hello, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-245">In hello left menu, select **Users and groups**.</span></span>

    ![Sélectionner Utilisateurs et groupes][202] 

4. <span data-ttu-id="2d9b1-247">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-247">Select **Add**.</span></span> <span data-ttu-id="2d9b1-248">Ensuite, sous hello **ajouter l’affectation** page, sélectionnez **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![page Ajouter une attribution de Hello][203]

5. <span data-ttu-id="2d9b1-250">Sur hello **utilisateurs et groupes** page, dans la liste de hello des utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="2d9b1-251">Sur hello **utilisateurs et groupes** page, sélectionnez **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="2d9b1-252">Sur hello **ajouter l’affectation** page, sélectionnez **affecter**.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2d9b1-254">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2d9b1-254">Test single sign-on</span></span>

<span data-ttu-id="2d9b1-255">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide du volet d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="2d9b1-256">Lorsque vous sélectionnez la vignette de SAP Business objet Cloud hello hello panneau d’accès, vous devez être connecté automatiquement dans tooyour application SAP Business objet Cloud.</span><span class="sxs-lookup"><span data-stu-id="2d9b1-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="2d9b1-257">Pour plus d’informations sur le volet d’accès hello, consultez [volet d’accès toohello Introduction](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d9b1-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d9b1-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2d9b1-258">Additional resources</span></span>

* [<span data-ttu-id="2d9b1-259">Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d9b1-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d9b1-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2d9b1-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

