---
title: "Téléchargement d’un certificat de gestion API Azure | Microsoft Docs"
description: "Découvrez comment charger le certificat d’API de gestion pour le portail Azure Classic."
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
ms.openlocfilehash: 9dc438e927acd9aef38f06807fabf3dda9b021c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="57712-103">Téléchargement d’un certificat de gestion API dans Azure Management</span><span class="sxs-lookup"><span data-stu-id="57712-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="57712-104">Les certificats de gestion vous permettent de vous authentifier dans le modèle de déploiement classique fourni par Azure.</span><span class="sxs-lookup"><span data-stu-id="57712-104">Management certificates allow you to authenticate with the classic deployment model provided by Azure.</span></span> <span data-ttu-id="57712-105">De nombreux programmes et outils (tels que Visual Studio ou le Kit de développement logiciel (SDK) Azure) utilisent ces certificats pour automatiser la configuration et le déploiement de divers services Azure.</span><span class="sxs-lookup"><span data-stu-id="57712-105">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="57712-106">Soyez prudent !</span><span class="sxs-lookup"><span data-stu-id="57712-106">Be careful!</span></span> <span data-ttu-id="57712-107">Ces types de certificat permettent à toute personne qui s’authentifie par leur biais de gérer l’abonnement auquel ils sont associés.</span><span class="sxs-lookup"><span data-stu-id="57712-107">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="57712-108">Si vous souhaitez plus d’informations sur les certificats Azure (y compris sur la création d’un certificat auto-signé), consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="57712-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="57712-109">Vous pouvez également utiliser [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) pour authentifier le code client à des fins d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="57712-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="57712-110">Charger un certificat de gestion</span><span class="sxs-lookup"><span data-stu-id="57712-110">Upload a management certificate</span></span>
<span data-ttu-id="57712-111">Une fois le certificat de gestion créé (fichier .cer contenant uniquement la clé publique), vous pouvez charger ce dernier sur le portail.</span><span class="sxs-lookup"><span data-stu-id="57712-111">Once you have a management certificate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="57712-112">Quand le certificat est disponible sur le portail, toute personne disposant d’un certificat adéquat (clé privée) peut se connecter par le biais de l’API de gestion et accéder aux ressources de l’abonnement associé.</span><span class="sxs-lookup"><span data-stu-id="57712-112">When the certificate is available in the portal, anyone with a matching certificate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="57712-113">Connectez-vous au [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="57712-113">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="57712-114">Cliquez sur **Autres services** en bas de la liste des services Azure, puis sélectionnez **Abonnements** dans le groupe de services _Général_.</span><span class="sxs-lookup"><span data-stu-id="57712-114">Click **More services** at the bottom Azure service list, then select **Subscriptions** in the _General_ service group.</span></span>

    ![Options Abonnements dans le menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="57712-116">Veillez à bien sélectionner l’abonnement que vous souhaitez associer au certificat.</span><span class="sxs-lookup"><span data-stu-id="57712-116">Make sure to select the correct subscription that you want to associate with the certificate.</span></span>     
4. <span data-ttu-id="57712-117">Après avoir sélectionné l’abonnement approprié, appuyez sur **Certificats de gestion** dans le groupe _Paramètres_.</span><span class="sxs-lookup"><span data-stu-id="57712-117">After you have selected the correct subscription, press **Management certificates** in the _Settings_ group.</span></span>

    ![Paramètres](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="57712-119">Appuyez sur le bouton **Télécharger** .</span><span class="sxs-lookup"><span data-stu-id="57712-119">Press the **Upload** button.</span></span>

    ![charger sur la page des certificats](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="57712-121">Complétez la boîte de dialogue et appuyez sur **Charger**.</span><span class="sxs-lookup"><span data-stu-id="57712-121">Fill out the dialog information and press **Upload**.</span></span>

    ![Paramètres](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="57712-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57712-123">Next steps</span></span>
<span data-ttu-id="57712-124">Un certificat de gestion étant désormais associé à un abonnement, vous pouvez (après avoir installé le certificat correspondant localement) vous connecter par programmation à [l’API REST du modèle de déploiement classique](https://msdn.microsoft.com/library/azure/mt420159.aspx) et automatiser les différentes ressources Azure associées à cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="57712-124">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>
