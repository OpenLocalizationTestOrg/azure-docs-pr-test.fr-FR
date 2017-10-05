---
title: "Domaines personnalisés dans le proxy d’application Azure AD | Microsoft Docs"
description: "Gérer les domaines personnalisés dans le proxy d’application Azure AD afin que l’URL de l’application soit identique quel que soit l’emplacement d’où vos utilisateurs y accèdent."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="b98f1-103">Utilisation des domaines personnalisés dans le proxy d'application Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98f1-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="b98f1-104">Lorsque vous publiez une application via le proxy d’application Azure Active Directory, vous créez une URL externe accessible à vos utilisateurs lorsqu’ils travaillent à distance.</span><span class="sxs-lookup"><span data-stu-id="b98f1-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="b98f1-105">Cette URL obtient le domaine par défaut *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="b98f1-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="b98f1-106">Par exemple, si vous avez publié une application nommée Dépenses et si votre locataire s’appelle Contoso, l’URL externe serait https://dépenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="b98f1-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="b98f1-107">Si vous souhaitez utiliser votre propre nom de domaine, configurez un domaine personnalisé pour votre application.</span><span class="sxs-lookup"><span data-stu-id="b98f1-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="b98f1-108">Nous vous recommandons de définir des domaines personnalisés pour vos applications, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="b98f1-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="b98f1-109">Voici quelques-uns des avantages des domaines personnalisés :</span><span class="sxs-lookup"><span data-stu-id="b98f1-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="b98f1-110">Les utilisateurs accèdent à l’application avec la même URL, qu’ils travaillent à l’intérieur ou à l’extérieur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="b98f1-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="b98f1-111">Si toutes vos applications ont les mêmes URL internes et externes, les liens qui pointent vers une autre application continuent à fonctionner même en dehors du réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="b98f1-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="b98f1-112">Vous contrôlez votre marque et créez les URL que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b98f1-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="b98f1-113">Configuration d’un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="b98f1-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b98f1-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b98f1-114">Prerequisites</span></span>

<span data-ttu-id="b98f1-115">Avant de configurer un domaine personnalisé, assurez-vous d’avoir rempli les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="b98f1-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="b98f1-116">La [vérification du domaine ajouté à Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b98f1-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="b98f1-117">Un certificat personnalisé pour le domaine, sous la forme de fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="b98f1-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="b98f1-118">Une application locale [publiée via le Proxy d’application](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b98f1-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="b98f1-119">Configurer votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="b98f1-119">Configure your custom domain</span></span>

<span data-ttu-id="b98f1-120">Lorsque vous avez rempli ces trois conditions, procédez comme suit pour configurer votre domaine personnalisé :</span><span class="sxs-lookup"><span data-stu-id="b98f1-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="b98f1-121">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b98f1-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b98f1-122">Accédez à **Azure Active Directory** > **Applications d’entreprise** > **Toutes les applications** et sélectionnez l’application que vous souhaitez gérer.</span><span class="sxs-lookup"><span data-stu-id="b98f1-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="b98f1-123">Sélectionnez **Proxy d’application**.</span><span class="sxs-lookup"><span data-stu-id="b98f1-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="b98f1-124">Dans le champ URL externe, utilisez la liste déroulante pour sélectionner votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b98f1-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="b98f1-125">Si vous ne voyez pas votre domaine dans la liste, il n’a pas encore été vérifié.</span><span class="sxs-lookup"><span data-stu-id="b98f1-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="b98f1-126">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b98f1-126">Select **Save**</span></span>
5. <span data-ttu-id="b98f1-127">Le champ **certificat** qui a été désactivé est maintenant activé.</span><span class="sxs-lookup"><span data-stu-id="b98f1-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="b98f1-128">Sélectionnez ce champ.</span><span class="sxs-lookup"><span data-stu-id="b98f1-128">Select this field.</span></span> 

   ![Cliquez pour télécharger un certificat.](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="b98f1-130">Si vous avez déjà téléchargé un certificat pour ce domaine, le champ Certificat affiche les informations de certificat.</span><span class="sxs-lookup"><span data-stu-id="b98f1-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="b98f1-131">Télécharger le certificat PFX et entrez le mot de passe du certificat.</span><span class="sxs-lookup"><span data-stu-id="b98f1-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="b98f1-132">Cliquez sur **Enregistrer** pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b98f1-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="b98f1-133">Ajoutez un [enregistrement DNS](../dns/dns-operations-recordsets-portal.md) qui redirige la nouvelle URL externe vers le domaine msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="b98f1-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="b98f1-134">Télécharger uniquement un certificat par un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b98f1-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="b98f1-135">Quand vous avez téléchargé un certificat, vous pouvez choisir le domaine personnalisé lorsque vous publiez une nouvelle application, sans effectuer une configuration supplémentaire à l’exception de l’enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="b98f1-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="b98f1-136">Gérer des certificats</span><span class="sxs-lookup"><span data-stu-id="b98f1-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="b98f1-137">Format de certificat</span><span class="sxs-lookup"><span data-stu-id="b98f1-137">Certificate format</span></span>
<span data-ttu-id="b98f1-138">Il n’existe aucune restriction sur les méthodes de signature de certificat.</span><span class="sxs-lookup"><span data-stu-id="b98f1-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="b98f1-139">Chiffrement à courbe elliptique (ECC), autre nom de l’objet (SAN) et d’autres types de certificat courants sont tous pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b98f1-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="b98f1-140">Vous pouvez utiliser un certificat avec caractère générique tant que ce dernier correspond à l’URL externe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="b98f1-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="b98f1-141">Vous pouvez également utiliser des certificats auto-signés.</span><span class="sxs-lookup"><span data-stu-id="b98f1-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="b98f1-142">Si vous utilisez une autorité de certification privée, le point de distribution de la liste de révocation de certificats du certificat doit être public.</span><span class="sxs-lookup"><span data-stu-id="b98f1-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="b98f1-143">Modification de domaine</span><span class="sxs-lookup"><span data-stu-id="b98f1-143">Changing the domain</span></span>
<span data-ttu-id="b98f1-144">Tous les domaines vérifiés s’affichent dans la liste déroulante de l’URL externe pour votre application.</span><span class="sxs-lookup"><span data-stu-id="b98f1-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="b98f1-145">Pour modifier le domaine, mettez simplement ce champ à jour pour l’application.</span><span class="sxs-lookup"><span data-stu-id="b98f1-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="b98f1-146">Si le domaine n’est pas dans la liste, [ajoutez-le en tant que domaine vérifié](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b98f1-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="b98f1-147">Si vous sélectionnez un domaine dont le certificat n’est pas encore associé, suivez les étapes 5 à 7 pour ajouter le certificat.</span><span class="sxs-lookup"><span data-stu-id="b98f1-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="b98f1-148">Ensuite, assurez-vous que vous mettez à jour l’enregistrement DNS pour la redirection à partir de la nouvelle URL externe.</span><span class="sxs-lookup"><span data-stu-id="b98f1-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="b98f1-149">Gestion des certificats</span><span class="sxs-lookup"><span data-stu-id="b98f1-149">Certificate management</span></span>
<span data-ttu-id="b98f1-150">Vous pouvez utiliser le même certificat pour plusieurs applications, sauf si celles-ci partagent un hôte externe.</span><span class="sxs-lookup"><span data-stu-id="b98f1-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="b98f1-151">Lorsqu’un certificat expire, vous obtenez un avertissement vous demandant de télécharger un autre certificat via le portail.</span><span class="sxs-lookup"><span data-stu-id="b98f1-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="b98f1-152">Si le certificat est révoqué, vos utilisateurs pourraient recevoir un avertissement de sécurité lors de l’accès à l’application.</span><span class="sxs-lookup"><span data-stu-id="b98f1-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="b98f1-153">Nous n’effectuons pas de vérification pour déterminer si les certificats sont révoqués.</span><span class="sxs-lookup"><span data-stu-id="b98f1-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="b98f1-154">Pour mettre à jour le certificat pour une application donnée, accédez à l’application et suivez les étapes 5 à 7 pour la configuration des domaines personnalisés dans les applications publiées et servant à télécharger un nouveau certificat.</span><span class="sxs-lookup"><span data-stu-id="b98f1-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="b98f1-155">Si l’ancien certificat n’est pas utilisé par d’autres applications, il est automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="b98f1-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="b98f1-156">La gestion des certificats s’effectue actuellement via les pages d’applications individuelles. Vous devez donc gérer les certificats dans le contexte des applications pertinentes.</span><span class="sxs-lookup"><span data-stu-id="b98f1-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b98f1-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b98f1-157">Next steps</span></span>
* <span data-ttu-id="b98f1-158">[Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md) pour vos applications publiées avec l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b98f1-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="b98f1-159">[Activer l’accès conditionnel](active-directory-application-proxy-conditional-access.md) à vos applications publiées.</span><span class="sxs-lookup"><span data-stu-id="b98f1-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="b98f1-160">Ajout de votre propre nom de domaine à Azure AD</span><span class="sxs-lookup"><span data-stu-id="b98f1-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


