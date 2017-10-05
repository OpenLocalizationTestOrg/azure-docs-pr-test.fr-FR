---
title: "Sécuriser les services principaux à l’aide d’une authentification de certificat client dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment sécuriser des services principaux à l'aide d'une authentification par certificat client dans la Gestion des API Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="11c78-103">Comment sécuriser les services principaux à l'aide d'une authentification par certificat client dans la Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="11c78-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="11c78-104">La Gestion des API permet de sécuriser l'accès au service principal d'une API en utilisant des certificats client.</span><span class="sxs-lookup"><span data-stu-id="11c78-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="11c78-105">Ce guide explique comment gérer les certificats dans le portail des éditeurs de l’API et comment configurer une API pour utiliser un certificat et accéder à son service principal.</span><span class="sxs-lookup"><span data-stu-id="11c78-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="11c78-106">Pour en savoir plus sur la gestion des certificats à l’aide de l’API REST de gestion des API, consultez [Entité de certificat API REST de gestion des API Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="11c78-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="11c78-107"><a name="prerequisites"> </a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="11c78-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="11c78-108">Ce guide explique comment configurer votre instance de service de gestion des API afin d'utiliser l'authentification par certificat pour accéder au service principal d'une API.</span><span class="sxs-lookup"><span data-stu-id="11c78-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="11c78-109">Avant de suivre la procédure présentée dans cette rubrique, vous devez configurer votre service principal pour l’authentification avec certificat client ([pour configurer l’authentification avec certificat dans Sites Web Azure, consultez cet article ][to configure certificate authentication in Azure WebSites refer to this article]) et avoir accès au certificat et au mot de passe associés afin de les charger dans le portail de publication de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="11c78-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="11c78-110"><a name="step1"> </a>Chargement d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="11c78-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="11c78-111">Pour commencer, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="11c78-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="11c78-112">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="11c78-112">This takes you to the API Management publisher portal.</span></span>

![Portail des éditeurs d’API][api-management-management-console]

> <span data-ttu-id="11c78-114">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="11c78-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="11c78-115">Cliquez sur **Sécurité** dans le menu **Gestion des API** de gauche, puis sur **Certificats clients**.</span><span class="sxs-lookup"><span data-stu-id="11c78-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Certificats clients][api-management-security-client-certificates]

<span data-ttu-id="11c78-117">Pour charger un nouveau certificat, cliquez sur **Charger un certificat**.</span><span class="sxs-lookup"><span data-stu-id="11c78-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Charger un certificat][api-management-upload-certificate]

<span data-ttu-id="11c78-119">Accédez à votre certificat, puis entrez le mot de passe pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="11c78-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="11c78-120">Le certificat doit être au format **.pfx** .</span><span class="sxs-lookup"><span data-stu-id="11c78-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="11c78-121">Les certificats auto-signés sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="11c78-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Charger un certificat][api-management-upload-certificate-form]

<span data-ttu-id="11c78-123">Cliquez sur **Charger** pour charger le certificat.</span><span class="sxs-lookup"><span data-stu-id="11c78-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="11c78-124">Le mot de passe du certificat est validé à ce moment.</span><span class="sxs-lookup"><span data-stu-id="11c78-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="11c78-125">S'il est incorrect, un message d'erreur s'affiche.</span><span class="sxs-lookup"><span data-stu-id="11c78-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificat chargé][api-management-certificate-uploaded]

<span data-ttu-id="11c78-127">Lorsque le certificat est chargé, il s'affiche dans l'onglet **Certificats clients** .</span><span class="sxs-lookup"><span data-stu-id="11c78-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="11c78-128">Si vous avez plusieurs certificats, faites une note indiquant les quatre derniers caractères de l’empreinte numérique, qui sont utilisés pour sélectionner le certificat lors de la configuration d’une API pour l’utilisation de certificats, tel qu’indiqué dans la section suivante [Configuration d’une API afin d’utiliser un certificat pour l’authentification de passerelle][Configure an API to use a client certificate for gateway authentication].</span><span class="sxs-lookup"><span data-stu-id="11c78-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="11c78-129">Pour désactiver la validation des chaînes de certificat lorsque vous utilisez, par exemple, un certificat auto-signé, suivez les étapes décrites dans cet [élément](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) de FAQ.</span><span class="sxs-lookup"><span data-stu-id="11c78-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="11c78-130"><a name="step1a"> </a>Suppression d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="11c78-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="11c78-131">Pour supprimer un certificat, cliquez sur **Supprimer** à côté du certificat en question.</span><span class="sxs-lookup"><span data-stu-id="11c78-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Suppression d'un certificat][api-management-certificate-delete]

<span data-ttu-id="11c78-133">Cliquez sur **Oui, le supprimer** pour confirmer la suppression.</span><span class="sxs-lookup"><span data-stu-id="11c78-133">Click **Yes, delete it** to confirm.</span></span>

![Confirmation de suppression][api-management-confirm-delete]

<span data-ttu-id="11c78-135">Si le certificat est en cours d'utilisation par une API, un écran d'avertissement s'affiche.</span><span class="sxs-lookup"><span data-stu-id="11c78-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="11c78-136">Pour supprimer le certificat, vous devez d'abord le supprimer de toutes les API configurées pour l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="11c78-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Confirmation de suppression][api-management-confirm-delete-policy]

## <span data-ttu-id="11c78-138"><a name="step2"> </a>Configuration d'une API afin d'utiliser un certificat pour l'authentification de passerelle</span><span class="sxs-lookup"><span data-stu-id="11c78-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="11c78-139">Cliquez sur **API** dans le menu **Gestion des API** de gauche, cliquez sur le nom de l’API désirée, puis cliquez sur l’onglet **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="11c78-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![Sécurité API][api-management-api-security]

<span data-ttu-id="11c78-141">Sélectionnez **Certificats client** dans la liste déroulante **Avec informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="11c78-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Certificats clients][api-management-mutual-certificates]

<span data-ttu-id="11c78-143">Sélectionnez le certificat désiré dans la liste déroulante **Certificat client** .</span><span class="sxs-lookup"><span data-stu-id="11c78-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="11c78-144">Si plusieurs certificats s'affichent, vous pouvez consulter le sujet ou les quatre derniers caractères de l'empreinte numérique (notés dans la section précédente) afin d'identifier le certificat correct.</span><span class="sxs-lookup"><span data-stu-id="11c78-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Sélection de certificat][api-management-select-certificate]

<span data-ttu-id="11c78-146">Cliquez sur **Enregistrer** pour enregistrer la modification de configuration de l'API.</span><span class="sxs-lookup"><span data-stu-id="11c78-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="11c78-147">Cette modification s'applique immédiatement, et les appels d'opérations de cette API utiliseront désormais ce certificat pour s'authentifier sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="11c78-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Enregistrement des modifications d'API][api-management-save-api]

> <span data-ttu-id="11c78-149">Lorsqu’un certificat est spécifié pour l’authentification passerelle d’un service principal d’une API, il est intégré à la stratégie de cette API et peut être affiché dans l’éditeur de stratégies.</span><span class="sxs-lookup"><span data-stu-id="11c78-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Stratégie de certificat][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="11c78-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11c78-151">Next steps</span></span>
<span data-ttu-id="11c78-152">Pour plus d'informations sur les autres méthodes de sécurisation de votre service principal, telles que l’authentification HTTP de base ou partagée, regardez la vidéo suivante</span><span class="sxs-lookup"><span data-stu-id="11c78-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



