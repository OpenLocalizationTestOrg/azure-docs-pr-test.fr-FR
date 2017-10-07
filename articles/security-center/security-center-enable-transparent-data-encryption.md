---
title: "aaaEnable chiffrement Transparent des données dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer Transparent de données chiffrement **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Activation de Transparent Data Encryption dans Azure Security Center
Azure Security Center vous recommande d’activer TDE (Transparent Data Encryption) sur les bases de données SQL si ce n’est déjà fait. Chiffrement transparent des données protègent vos données et vous aide à répondre aux exigences de conformité en chiffrant votre base de données, les sauvegardes associées et les fichiers journaux des transactions au repos, sans nécessiter de modifications tooyour application. Voir toolearn [chiffrement Transparent des données avec Azure SQL Database](https://msdn.microsoft.com/library/dn948096).

Cette recommandation s’applique toohello service SQL Azure uniquement. n’inclut pas SQL en cours d’exécution sur vos ordinateurs virtuels.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **activer Transparent Data Encryption**.
   ![Activer Transparent Data Encryption][1]
2. Cette opération ouvre hello **activer le chiffrement Transparent des données sur les bases de données SQL** panneau. Sélectionnez un tooenable de base de données SQL chiffrement transparent des données.
   ![Sélectionnez la base de données SQL tooenable chiffrement transparent des données sur][2]
3. Sur hello **chiffrement Transparent des données** panneau, sélectionnez **ON** sous le chiffrement des données et sélectionnez **enregistrer** dans le ruban supérieur de hello du Panneau de hello.
   ![Activer le chiffrement transparent des données][3]

   Une fois que le chiffrement transparent des données sont activée sur hello sélectionné base de données SQL, hello **état du chiffrement** modifiera trop**Encrypted**.    

   ![État du chiffrement][4]

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment tooimplement hello recommandation du centre de sécurité « Activer Transparent Data Encryption ». toolearn en savoir plus sur SQL TDE, voir hello :

* [Transparent Data Encryption avec Azure SQL Database](https://msdn.microsoft.com/library/dn948096)
* [Prise en main du chiffrement transparent des données (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
