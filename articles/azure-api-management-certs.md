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
# <a name="upload-an-azure-management-api-management-certificate"></a>Téléchargement d’un certificat de gestion API dans Azure Management
Les certificats de gestion vous permettent de vous authentifier dans le modèle de déploiement classique fourni par Azure. De nombreux programmes et outils (tels que Visual Studio ou le Kit de développement logiciel (SDK) Azure) utilisent ces certificats pour automatiser la configuration et le déploiement de divers services Azure. 

> [!WARNING]
> Soyez prudent ! Ces types de certificat permettent à toute personne qui s’authentifie par leur biais de gérer l’abonnement auquel ils sont associés.
>
>

Si vous souhaitez plus d’informations sur les certificats Azure (y compris sur la création d’un certificat auto-signé), consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Vous pouvez également utiliser [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) pour authentifier le code client à des fins d’automatisation.

## <a name="upload-a-management-certificate"></a>Charger un certificat de gestion
Une fois le certificat de gestion créé (fichier .cer contenant uniquement la clé publique), vous pouvez charger ce dernier sur le portail. Quand le certificat est disponible sur le portail, toute personne disposant d’un certificat adéquat (clé privée) peut se connecter par le biais de l’API de gestion et accéder aux ressources de l’abonnement associé.

1. Connectez-vous au [portail Azure](http://portal.azure.com).
2. Cliquez sur **Autres services** en bas de la liste des services Azure, puis sélectionnez **Abonnements** dans le groupe de services _Général_.

    ![Options Abonnements dans le menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. Veillez à bien sélectionner l’abonnement que vous souhaitez associer au certificat.     
4. Après avoir sélectionné l’abonnement approprié, appuyez sur **Certificats de gestion** dans le groupe _Paramètres_.

    ![Paramètres](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Appuyez sur le bouton **Télécharger** .

    ![charger sur la page des certificats](./media/azure-api-management-certs/certificates_page.png)
6. Complétez la boîte de dialogue et appuyez sur **Charger**.

    ![Paramètres](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Étapes suivantes
Un certificat de gestion étant désormais associé à un abonnement, vous pouvez (après avoir installé le certificat correspondant localement) vous connecter par programmation à [l’API REST du modèle de déploiement classique](https://msdn.microsoft.com/library/azure/mt420159.aspx) et automatiser les différentes ressources Azure associées à cet abonnement.
