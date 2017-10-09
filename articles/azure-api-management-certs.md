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
# <a name="upload-an-azure-management-api-management-certificate"></a>Téléchargement d’un certificat de gestion API dans Azure Management
Certificats de gestion permettent de vous tooauthenticate avec le modèle de déploiement classique hello fournie par Azure. Plusieurs des programmes et des outils (tels que Visual Studio ou hello Azure SDK) utilisent ces tooautomate configuration des certificats et le déploiement des services Azure différents. 

> [!WARNING]
> Soyez prudent ! Ces types de certificats autorisent tout le monde qui s’authentifie avec les abonnements de hello toomanage auxquels ils sont associés.
>
>

Si vous souhaitez plus d’informations sur les certificats Azure (y compris sur la création d’un certificat auto-signé), consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Vous pouvez également utiliser [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) code client tooauthenticate fins d’automatisation.

## <a name="upload-a-management-certificate"></a>Charger un certificat de gestion
Une fois que vous avez un certificat de gestion créé, un (fichier .cer avec uniquement une clé publique hello) vous pouvez le télécharger dans le portail de hello. Lorsque le certificat de hello est disponible dans le portail de hello, toute personne disposant d’un certificat correspondant (clé privée) peut se connecter via hello API de gestion et accès hello des ressources pour l’abonnement de hello associé.

1. Connectez-vous à toohello [portail Azure](http://portal.azure.com).
2. Cliquez sur **davantage de services** à la liste des services Azure hello bas, puis sélectionnez **abonnements** Bonjour _général_ groupe de service.

    ![Options Abonnements dans le menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. Assurez-vous que tooselect hello abonnement approprié que vous souhaitez tooassociate avec un certificat de hello.     
4. Une fois que vous avez sélectionné l’abonnement approprié de hello, appuyez sur **certificats de gestion** Bonjour _paramètres_ groupe.

    ![Paramètres](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Hello de presse **télécharger** bouton.

    ![charger sur la page des certificats](./media/azure-api-management-certs/certificates_page.png)
6. Renseignez les informations de boîte de dialogue hello et appuyez sur **télécharger**.

    ![Paramètres](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous disposez d’un certificat de gestion associé à un abonnement, vous pouvez (une fois que vous avez installé hello correspondance de certificat localement) vous connecter par programmation toohello [le modèle de déploiement classique API REST](https://msdn.microsoft.com/library/azure/mt420159.aspx) et automatiser Bonjour différentes ressources Azure sont également associés à cet abonnement.
