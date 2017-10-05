---
title: "Problème de configuration de l’authentification unique fédérée pour une application non issue de la galerie | Microsoft Docs"
description: "Découvrez comment résoudre certains problèmes courants que vous pouvez rencontrer lors de la configuration de l’authentification unique fédérée sur votre application SAML personnalisée non répertoriée dans la galerie d’applications Azure AD"
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
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="8ff50-103">Problème de configuration de l’authentification unique fédérée pour une application non issue de la galerie</span><span class="sxs-lookup"><span data-stu-id="8ff50-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="8ff50-104">Si vous rencontrez un problème lors de la configuration d’une application,</span><span class="sxs-lookup"><span data-stu-id="8ff50-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="8ff50-105">vérifiez que vous avez suivi toutes les étapes de l’article [Configuration de l’authentification unique pour les applications ne faisant pas partie de la galerie d’applications Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps).</span><span class="sxs-lookup"><span data-stu-id="8ff50-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="8ff50-106">Impossible d’ajouter une autre instance de l’application</span><span class="sxs-lookup"><span data-stu-id="8ff50-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="8ff50-107">Pour ajouter une deuxième instance d’une application, vous devez être en mesure de :</span><span class="sxs-lookup"><span data-stu-id="8ff50-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="8ff50-108">Configurer un identificateur unique pour la deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="8ff50-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="8ff50-109">Vous ne pourrez pas configurer le même identificateur que celui utilisé pour la première instance.</span><span class="sxs-lookup"><span data-stu-id="8ff50-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="8ff50-110">Configurer un certificat différent de celui utilisé pour la première instance.</span><span class="sxs-lookup"><span data-stu-id="8ff50-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="8ff50-111">Si l’application ne prend en charge aucune de ces configurations,</span><span class="sxs-lookup"><span data-stu-id="8ff50-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="8ff50-112">vous ne pourrez pas configurer une deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="8ff50-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="8ff50-113">Où définir le format d’EntityID (identificateur d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="8ff50-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="8ff50-114">Vous ne pouvez pas sélectionner le format d’EntityID (identificateur d’utilisateur) qu’Azure AD envoie à l’application dans la réponse après l’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8ff50-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="8ff50-115">Azure AD sélectionne le format de l’attribut NameID (identificateur d’utilisateur) en fonction de la valeur sélectionnée ou du format demandé par l’application dans la demande d’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="8ff50-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="8ff50-116">Pour plus d’informations, consultez l’article [Protocole SAML d’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) dans la section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="8ff50-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="8ff50-117">Comment obtenir le certificat ou les métadonnées de l’application à partir d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ff50-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="8ff50-118">Pour télécharger le certificat ou les métadonnées de l’application à partir d’Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ff50-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="8ff50-119">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="8ff50-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="8ff50-120">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="8ff50-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="8ff50-121">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ff50-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="8ff50-122">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ff50-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="8ff50-123">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="8ff50-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="8ff50-124">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="8ff50-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="8ff50-125">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8ff50-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="8ff50-126">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="8ff50-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="8ff50-127">Accédez à la section **Certificat de signature SAML**, puis cliquez sur la valeur de colonne **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="8ff50-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="8ff50-128">En fonction de ce que l’application nécessite pour configurer l’authentification unique, vous voyez soit l’option de téléchargement des métadonnées XML, soit le certificat.</span><span class="sxs-lookup"><span data-stu-id="8ff50-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="8ff50-129">Azure AD ne fournit pas d’URL permettant d’obtenir les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="8ff50-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="8ff50-130">Les métadonnées peuvent uniquement être récupérées sous forme de fichier XML.</span><span class="sxs-lookup"><span data-stu-id="8ff50-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="8ff50-131">Vous ne savez pas comment personnaliser les revendications SAML envoyées à une application</span><span class="sxs-lookup"><span data-stu-id="8ff50-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="8ff50-132">Pour savoir comment personnaliser les revendications d’attribut SAML envoyées à votre application, consultez [Claims mapping in Azure Active Directory (public preview)](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) (Mappage de revendications dans Azure Active Directory [préversion]) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8ff50-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ff50-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ff50-133">Next steps</span></span>
[<span data-ttu-id="8ff50-134">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ff50-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
