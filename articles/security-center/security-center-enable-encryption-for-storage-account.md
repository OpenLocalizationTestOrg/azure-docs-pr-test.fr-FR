---
title: "chiffrement aaaEnable pour le compte de stockage dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandations du centre de sécurité Azure ** activer le chiffrement pour Azure Storage compte **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Activation du chiffrement pour le compte de stockage Azure dans Azure Security Center | Microsoft Docs
Azure Security Center peut vous recommander d’activer le chiffrement du service Azure Storage pour les données au repos.

Chiffrement de Service de stockage (SSE) fonctionne par chiffrement des données de hello lorsqu’elle est écrite tooAzure stockage et le déchiffrement des données hello avant la récupération.  SSE n’est actuellement disponible uniquement pour hello service Blob Azure et peut être utilisé pour les objets BLOB de blocs, objets BLOB de pages et ajoute des objets BLOB.  toolearn, voir [chiffrement de Service de stockage pour les données au repos](../storage/common/storage-service-encryption.md).


> [!Note]
> Après l’activation du chiffrement, seules les nouvelles données sont chiffrées. Tous les objets blob existants dans votre compte de stockage restent non chiffrés. tooencrypt des objets BLOB, consultez hello [FAQ de chiffrement de Service de stockage](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

SSE est uniquement pris en charge sur les comptes de stockage Resource Manager. Les comptes de stockage classiques ne sont actuellement pas pris en charge. hello toounderstand classique et les modèles de déploiement du Gestionnaire de ressources, consultez [modèles de déploiement Azure](../azure-classic-rm.md).

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Ce document n'est pas un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **activer le chiffrement pour le compte de stockage Azure**.
   ![Activer le chiffrement pour le compte Azure Storage][1]
2. Hello **activer le chiffrement de stockage** panneau s’ouvre. Ce panneau répertorie les comptes de stockage Azure hello où le chiffrement de stockage est désactivé. Dans cet exemple, sélectionnons **storageacct1**.
   ![Activer le chiffrement du stockage][2]
3. Hello **chiffrement** panneau pour **storageacct1** s’ouvre. Sélectionnez **Enabled**.
   ![Panneau Chiffrement][3]
4. Sélectionnez **Enregistrer**.

Vous avez activé le chiffrement de stockage pour **storageacct1**.


## <a name="see-also"></a>Voir aussi
Ce document vous a montré comment tooimplement hello centre de sécurité recommandation « activer le chiffrement pour le compte de stockage Azure. » toolearn en savoir plus sur le chiffrement de Service de stockage Azure, voir hello :

* [Azure Storage Service Encryption pour les données au repos](../storage/common/storage-service-encryption.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) -en savoir comment les stratégies de sécurité tooconfigure pour vos abonnements Azure et les groupes de ressources.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) -en savoir comment toomonitor hello d’intégrité de vos ressources Azure.
* [Gestion et répond toosecurity alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) -en savoir comment les alertes toosecurity toomanage et y répondre.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) -Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
