---
title: "aaaProblem configuration fédérée l’authentification unique pour une application non-galerie | Documents Microsoft"
description: "Résoudre certains des problèmes courants de hello que vous pouvez rencontrer lors de la configuration d’application SAML personnalisée tooyour d’authentification unique fédérée qui n’est pas répertoriée dans hello Galerie d’applications Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9fffd-103">Problème de configuration de l’authentification unique fédérée pour une application non issue de la galerie</span><span class="sxs-lookup"><span data-stu-id="9fffd-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9fffd-104">Si vous rencontrez un problème lors de la configuration d’une application,</span><span class="sxs-lookup"><span data-stu-id="9fffd-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="9fffd-105">Vérifiez que vous avez suivi toutes les étapes de hello dans l’article de hello [configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="9fffd-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="9fffd-106">Impossible d’ajouter une autre instance de l’application hello</span><span class="sxs-lookup"><span data-stu-id="9fffd-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="9fffd-107">tooadd une deuxième instance d’une application, vous devez toobe en mesure de :</span><span class="sxs-lookup"><span data-stu-id="9fffd-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="9fffd-108">Configurer un identificateur unique pour la deuxième instance de hello.</span><span class="sxs-lookup"><span data-stu-id="9fffd-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="9fffd-109">Vous ne serez pas hello tooconfigure en mesure de même identificateur utilisé pour première instance de hello.</span><span class="sxs-lookup"><span data-stu-id="9fffd-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="9fffd-110">Configurer un certificat différent que hello celui utilisé pour la première instance de hello.</span><span class="sxs-lookup"><span data-stu-id="9fffd-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="9fffd-111">Si hello application ne prend en charge des hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9fffd-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="9fffd-112">Ensuite, vous ne serez pas en mesure de tooconfigure une deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="9fffd-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="9fffd-113">Où définir le format de hello EntityID (identifiant d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="9fffd-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="9fffd-114">Vous ne sont pas être en mesure de tooselect hello au format EntityID (identifiant d’utilisateur) que Azure AD envoie toohello application dans la réponse de hello après l’authentification des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9fffd-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="9fffd-115">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="9fffd-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="9fffd-116">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) section hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="9fffd-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="9fffd-117">Où obtenir les métadonnées de l’application hello ou un certificat auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="9fffd-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="9fffd-118">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9fffd-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="9fffd-119">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="9fffd-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9fffd-120">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="9fffd-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9fffd-121">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="9fffd-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9fffd-122">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9fffd-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9fffd-123">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="9fffd-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="9fffd-124">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="9fffd-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="9fffd-125">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9fffd-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9fffd-126">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="9fffd-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9fffd-127">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="9fffd-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9fffd-128">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="9fffd-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="9fffd-129">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="9fffd-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="9fffd-130">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="9fffd-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="9fffd-131">Ne connaissez pas comment toocustomize SAML revendications envoyé tooan application</span><span class="sxs-lookup"><span data-stu-id="9fffd-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="9fffd-132">toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9fffd-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fffd-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fffd-133">Next steps</span></span>
[<span data-ttu-id="9fffd-134">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fffd-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
