---
title: "aaaUpload un certificat d’API de gestion Azure | Documents Microsoft"
description: "Découvrez comment tooupload athe API de gestion des certificats pour hello portail classique Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="8300b-103">Téléchargement d’un certificat de gestion API dans Azure Management</span><span class="sxs-lookup"><span data-stu-id="8300b-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="8300b-104">Certificats de gestion permettent de vous tooauthenticate avec le modèle de déploiement classique hello fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="8300b-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="8300b-105">Plusieurs des programmes et des outils (tels que Visual Studio ou hello Azure SDK) utilisent ces tooautomate configuration des certificats et le déploiement des services Azure différents.</span><span class="sxs-lookup"><span data-stu-id="8300b-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="8300b-106">Soyez prudent !</span><span class="sxs-lookup"><span data-stu-id="8300b-106">Be careful!</span></span> <span data-ttu-id="8300b-107">Ces types de certificats autorisent tout le monde qui s’authentifie avec les abonnements de hello toomanage auxquels ils sont associés.</span><span class="sxs-lookup"><span data-stu-id="8300b-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="8300b-108">Si vous souhaitez plus d’informations sur les certificats Azure (y compris sur la création d’un certificat auto-signé), consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="8300b-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="8300b-109">Vous pouvez également utiliser [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) code client tooauthenticate fins d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="8300b-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="8300b-110">Charger un certificat de gestion</span><span class="sxs-lookup"><span data-stu-id="8300b-110">Upload a management certificate</span></span>
<span data-ttu-id="8300b-111">Une fois que vous avez un certificat de gestion créé, un (fichier .cer avec uniquement une clé publique hello) vous pouvez le télécharger dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="8300b-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="8300b-112">Lorsque le certificat de hello est disponible dans le portail de hello, toute personne disposant d’un certificat correspondant (clé privée) peut se connecter via hello API de gestion et accès hello des ressources pour l’abonnement de hello associé.</span><span class="sxs-lookup"><span data-stu-id="8300b-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="8300b-113">Connectez-vous à toohello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8300b-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="8300b-114">Cliquez sur **davantage de services** à la liste des services Azure hello bas, puis sélectionnez **abonnements** Bonjour _général_ groupe de service.</span><span class="sxs-lookup"><span data-stu-id="8300b-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Options Abonnements dans le menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="8300b-116">Assurez-vous que tooselect hello abonnement approprié que vous souhaitez tooassociate avec un certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="8300b-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="8300b-117">Une fois que vous avez sélectionné l’abonnement approprié de hello, appuyez sur **certificats de gestion** Bonjour _paramètres_ groupe.</span><span class="sxs-lookup"><span data-stu-id="8300b-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Paramètres](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="8300b-119">Hello de presse **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="8300b-119">Press hello **Upload** button.</span></span>

    ![charger sur la page des certificats](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="8300b-121">Renseignez les informations de boîte de dialogue hello et appuyez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="8300b-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Paramètres](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="8300b-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8300b-123">Next steps</span></span>
<span data-ttu-id="8300b-124">Maintenant que vous disposez d’un certificat de gestion associé à un abonnement, vous pouvez (une fois que vous avez installé hello correspondance de certificat localement) vous connecter par programmation toohello [le modèle de déploiement classique API REST](https://msdn.microsoft.com/library/azure/mt420159.aspx) et automatiser Bonjour différentes ressources Azure sont également associés à cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="8300b-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
