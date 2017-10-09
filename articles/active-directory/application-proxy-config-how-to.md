---
title: "aaaHow tooconfigure une application de Proxy d’Application | Documents Microsoft"
description: "Découvrez comment toocreate une configuration d’une application Proxy d’APplication en quelques étapes simples"
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="b6d70-103">Comment tooconfigure une application de Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="b6d70-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="b6d70-104">Cet article vous a-t-il toounderstand tooconfigure une application de Proxy d’Application dans Azure AD tooexpose votre toohello d’applications sur site de cloud.</span><span class="sxs-lookup"><span data-stu-id="b6d70-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="b6d70-105">Documents recommandés</span><span class="sxs-lookup"><span data-stu-id="b6d70-105">Recommended documents</span></span> 

<span data-ttu-id="b6d70-106">toolearn sur les configurations initiales hello et la création d’une application de Proxy d’Application via hello portail d’administration, suivez hello [publier des applications à l’aide du Proxy d’Application Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b6d70-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="b6d70-107">Pour plus d’informations sur la configuration des connecteurs, consultez [activer le Proxy d’Application Bonjour Azure portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="b6d70-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="b6d70-108">Pour plus d’informations sur le chargement des certificats et l’utilisation des domaines personnalisés, consultez [Utilisation des domaines personnalisés dans le proxy d’application Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="b6d70-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="b6d70-109">Créer des URL de hello de paramètre d’Application hello</span><span class="sxs-lookup"><span data-stu-id="b6d70-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="b6d70-110">Si vous suivez les étapes hello Bonjour [publier des applications à l’aide du Proxy d’Application Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation et sont une erreur de création d’application hello, consultez les détails de l’erreur hello pour plus d’informations et des suggestions pour application hello toofix.</span><span class="sxs-lookup"><span data-stu-id="b6d70-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="b6d70-111">La plupart des messages d’erreur incluent la suggestion d’un correctif.</span><span class="sxs-lookup"><span data-stu-id="b6d70-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="b6d70-112">les erreurs courantes tooavoid, vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="b6d70-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="b6d70-113">Vous êtes un administrateur disposant d’autorisations toocreate une application de Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="b6d70-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="b6d70-114">une URL interne Hello est unique</span><span class="sxs-lookup"><span data-stu-id="b6d70-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="b6d70-115">URL externe de Hello est unique</span><span class="sxs-lookup"><span data-stu-id="b6d70-115">hello external URL is unique</span></span>

-   <span data-ttu-id="b6d70-116">Hello commencent URL http ou https et se terminer par un « / »</span><span class="sxs-lookup"><span data-stu-id="b6d70-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="b6d70-117">URL de Hello doit être un nom de domaine, et non une adresse IP</span><span class="sxs-lookup"><span data-stu-id="b6d70-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="b6d70-118">message d’erreur Hello doit afficher dans le coin supérieur droit de hello lorsque vous créez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b6d70-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="b6d70-119">Vous pouvez également sélectionner les messages d’erreur hello notification icône toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b6d70-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Invite de notification](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="b6d70-121">Configurer des connecteurs/groupes de connecteurs</span><span class="sxs-lookup"><span data-stu-id="b6d70-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="b6d70-122">Si vous avez des difficultés à configurer votre application en raison de l’avertissement concernant les connecteurs hello et groupes de connecteurs, consultez les instructions sur l’activation du Proxy d’Application pour plus d’informations sur la façon des connecteurs toodownload.</span><span class="sxs-lookup"><span data-stu-id="b6d70-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="b6d70-123">Si vous souhaitez toolearn plus d’informations sur les connecteurs, consultez hello [documentation de connecteurs](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="b6d70-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="b6d70-124">Si vos connecteurs sont inactives, cela signifie qu’ils sont le service de hello tooreach impossible.</span><span class="sxs-lookup"><span data-stu-id="b6d70-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="b6d70-125">Il s’agit souvent, car tous les ports hello requis ne sont pas ouverts.</span><span class="sxs-lookup"><span data-stu-id="b6d70-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="b6d70-126">toosee une liste des ports requis, consultez la section de conditions préalables de hello Hello l’activation de la documentation de Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="b6d70-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="b6d70-127">Charger des certificats pour des domaines personnalisés</span><span class="sxs-lookup"><span data-stu-id="b6d70-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="b6d70-128">Domaines personnalisés vous permettent de domaine de hello toospecify de votre URL externes.</span><span class="sxs-lookup"><span data-stu-id="b6d70-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="b6d70-129">toouse des domaines personnalisés, vous avez besoin tooupload hello certificat pour ce domaine.</span><span class="sxs-lookup"><span data-stu-id="b6d70-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="b6d70-130">Pour plus d’informations sur l’utilisation des domaines et des certificats personnalisés, consultez [Utilisation des domaines personnalisés dans le proxy d’application Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="b6d70-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="b6d70-131">Si vous rencontrez des problèmes de téléchargement de votre certificat, recherchez les messages d’erreur de hello dans portail hello pour plus d’informations sur un problème avec le certificat de hello hello.</span><span class="sxs-lookup"><span data-stu-id="b6d70-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="b6d70-132">Voici les problèmes courants liés aux certificats :</span><span class="sxs-lookup"><span data-stu-id="b6d70-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="b6d70-133">Expiration du certificat</span><span class="sxs-lookup"><span data-stu-id="b6d70-133">Expired certificate</span></span>

-   <span data-ttu-id="b6d70-134">Certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="b6d70-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="b6d70-135">Certificat ne contient pas de clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="b6d70-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="b6d70-136">affichage messages d’erreur Hello dans hello coin supérieur droit lorsque vous essaierez de certificat de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="b6d70-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="b6d70-137">Vous pouvez également sélectionner les messages d’erreur hello notification icône toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b6d70-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Invite de notification](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="b6d70-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6d70-139">Next steps</span></span>
[<span data-ttu-id="b6d70-140">Publier des applications avec le Proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6d70-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
