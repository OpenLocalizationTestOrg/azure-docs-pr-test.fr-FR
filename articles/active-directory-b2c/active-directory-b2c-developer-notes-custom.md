---
title: "Azure Active Directory B2C : Notes du développeur sur l’utilisation des stratégies personnalisées | Microsoft Docs"
description: "Notes à destination des développeurs pour configurer et maintenir Azure AD B2C avec des stratégies personnalisées"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Notes de version pour la version préliminaire publique de la stratégie personnalisée Azure Active Directory B2C
Hello ensemble de fonctionnalités de stratégie personnalisée est désormais disponible pour évaluation sous la version préliminaire publique de tous les B2C à Active Directory Azure (B2C Active Directory de Azure) clients. Cet ensemble de fonctionnalités est destiné aux développeurs identités avancée création de solutions d’identité hello plus complexes.  

Aujourd'hui, cet ensemble de fonctionnalités nécessite les développeurs tooconfigure hello identité expérience Framework directement via la modification de fichiers XML. Cette méthode de configuration est à la fois puissante et complexe. Les développeurs d’identité à l’aide de hello avancés identité expérience Framework prévoyez tooinvest du temps d’exécution des procédures détaillées et la lecture de documents de référence. 

## <a name="features-included-in-this-public-preview"></a>Fonctionnalités incluses dans cette version préliminaire publique
Avec hello nouvelles fonctionnalités introduites dans la version préliminaire publique de hello, les développeurs peuvent effectuer hello tâches suivantes :<br>

* Créer et charger des parcours utilisateur d’authentification personnalisés à l’aide de stratégies personnalisées. 
   * Décrire des parcours utilisateur étape par étape comme des échanges entre des fournisseurs de revendications. 
   * Définir le branchement conditionnel dans des parcours utilisateur. 
* Intégrer des services compatibles avec l’API REST dans vos parcours utilisateur d’authentification personnalisés.  
* Ajoutez la fédération avec les fournisseurs d’identité qui sont compatibles avec hello OpenIDConnect standard. <br>
* Ajouter la fédération avec les fournisseurs d’identité qui respectent le protocole de toohello SAML 2.0. 

## <a name="terms-of-hello-public-preview"></a>Termes du contrat de l’aperçu public de hello

* Nous vous encourageons toouse hello Nouveautés destinées à des fins d’évaluation uniquement.<br>
* Les nouvelles fonctionnalités ne sont pas destinées à une utilisation dans un environnement de production.<br>
* Contrats de niveau de service (SLA) ne s’appliquent pas toohello nouvelles fonctionnalités. <br>
* Les demandes de support peuvent être déposées via les canaux de support habituels. <br>
* Il n’existe aucune date prévue pour une mise à disposition générale.<br>
* Notre discrétion et pour une raison quelconque, Microsoft peut indicateur et rejeter ou restreindre des scénarios et des trajets utilisateur qui dépassent la portée de hello de hello Azure AD B2C produit charte tooserve comme une plateforme de gestion (CIAM) des identités et des accès client.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>Responsabilités des développeurs de l’ensemble de fonctionnalités de stratégie personnalisée
Configuration de la stratégie manuelle accorde toohello d’accès de niveau inférieur sous-jacent de la plateforme de Azure AD B2C et entraîne la création d’une infrastructure d’approbation unique, entièrement personnalisable hello. Les permutations possibles personnalisés des fournisseurs d’identité, des relations d’approbation, intégration avec les services externes et des flux de travail pas à pas place des demandes supérieurs sur hello avancé les développeurs consomment les.

avantages de toofully à partir de la version préliminaire publique de hello, nous vous suggérons de que les développeurs qui utilisent le jeu de fonctionnalités de stratégie personnalisée hello respectent toohello instructions :
* Vous familiariser avec le langage de configuration hello Hello moteur expérience d’identité et de gestion de clé/secret.
* S’approprier les scénarios et les intégrations personnalisées.
* Effectuer un test de scénario méthodique.
* Suivre les meilleures pratiques de test et de développement de logiciels avec au minimum un environnement de développement et de test et un environnement de production.
* Restez informé des développements à partir des fournisseurs d’identité hello et les services que vous intégrez. Par exemple, l’effectuer le suivi des modifications dans les clés secrètes et du service de toohello de modifications planifiées et non planifiées.
* Configurer la surveillance active et surveiller la réactivité hello des environnements de production.
* Maintenez à jour les adresses de messagerie de contact et restent des messages électroniques du site live équipe réactive toohello Microsoft.
* Agissez en temps voulu toodo conseillée hello, l’équipe Microsoft live-site. 


>[!NOTE]
>Ces fonctionnalités peuvent éventuellement être incluses dans les stratégies intégrées d’Azure AD, ce qui les rend plus accessibles aux développeurs de tooall.

## <a name="next-steps"></a>Étapes suivantes
[Azure Active Directory B2C : bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md).
