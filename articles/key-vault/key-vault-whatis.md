---
title: "aaaWhat est le coffre de clés Azure ? | Microsoft Docs"
description: "Azure Key Vault permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud. En utilisant Azure Key Vault, les clients peuvent chiffrer les clés et secrets (tels que les clés d’authentification, les clés de compte de stockage, les clés de chiffrement de données, les fichiers .PFX et les mots de passe) à l’aide de clés protégées par des modules de sécurité matériels (HSM)."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e759df6f-0638-43b1-98ed-30b3913f9b82
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 296fcce03658b96b84afab299b73681bbe8ac9fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-key-vault"></a>Qu’est-ce qu’Azure Key Vault ?
Azure Key Vault est disponible dans la plupart des régions. Pour plus d’informations, consultez hello [page de tarification de coffre de clés](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduction
Azure Key Vault permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud. En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (tels que les clés d’authentification, les clés de compte de stockage, les clés de chiffrement de données, les fichiers PFX et les mots de passe) à l’aide de clés protégées par des modules de sécurité matériels (HSM). Pour une meilleure garantie, vous pouvez importer ou générer des clés HSM. Si vous choisissez cette option, les processus Microsoft toodo vos clés de la norme FIPS 140-2 niveau 2 HSM validés (matériel et microprogramme).  

Coffre de clés rationalise le processus de gestion de clés hello et vous permet de contrôler toomaintain clés d’accès et de chiffrer vos données. Les développeurs peuvent créer des clés pour le développement et de test en quelques minutes et puis migrez en toute transparence les clés de tooproduction. Les administrateurs de sécurité peuvent accorder (et révoquer) tookeys d’autorisation, en fonction des besoins.

Hello utilisation suivant table toobetter comprendre comment le coffre de clés peut toomeet les besoins de hello des développeurs et administrateurs de sécurité.

| Rôle | Définition du problème | Résolu par Azure Key Vault |
| --- | --- | --- |
| Développeur d’une application Azure |« Je veux toowrite une application pour Azure qui utilise des clés de signature et de chiffrement, mais je veux ces toobe clés externes à partir de mon application afin que la solution de hello est adaptée à une application qui est distribuée géographiquement. <br/><br/>Je tiens également à ces toobe clés et les secrets protégés, sans avoir à code de hello toowrite moi-même. Je tiens également ces toobe clés et les secrets facile pour moi toouse à partir de mes applications, avec des performances optimales. » |√ Les clés sont stockées dans un coffre et appelées par un URI, si nécessaire.<br/><br/> √ Les clés sont protégées par Azure, à l’aide d’algorithmes standard, de longueurs de clé et de modules de sécurité matériel (HSM).<br/><br/> √ Clés sont traités dans les modules de sécurité matériels qui résident dans hello même des centres de données Azure en tant qu’applications de hello. Cela fournit une meilleure fiabilité et une latence réduite si les clés de hello résident dans un emplacement distinct, tel que localement. |
| Développeur de logiciels en tant que service (SaaS) |« Je ne veux pas responsabilité de responsabilité ou potentiel hello pour les clés de locataire de mes clients et les clés secrètes. <br/><br/>Je souhaitez hello clients tooown et gérer leurs clés, je peux vous concentrer sur les effectuant que faire mieux, qui est fournissant des fonctionnalités de logiciel core hello. » |√ Les clients peuvent importer leurs propres clés dans Azure et les gérer. Lorsqu’une application SaaS doit tooperform les opérations de chiffrement à l’aide de clés de leurs clients, le coffre de clés effectue ces opérations au nom de l’application hello. application Hello ne voit pas les clés de clients hello. |
| Responsable de la sécurité |« Je veux tooknow nos applications conformes FIPS 140-2 niveau 2 modules de sécurité matériels pour la gestion de clé sécurisée. <br/><br/>Je souhaite toomake que mon organisation se trouve dans le contrôle du cycle de vie de clé hello et que vous pouvez surveiller l’utilisation de la clé. <br/><br/>Et bien que nous utilisons plusieurs services Azure et les ressources, les clés de hello toomanage à partir d’un emplacement unique dans Azure. » |√ Les modules de sécurité matériels sont certifiés FIPS 140-2 de niveau 2.<br/><br/>√ Key Vault a été conçu de manière à ce que Microsoft ne puisse pas afficher ni extraire vos clés.<br/><br/>√ Journalisation de l’utilisation des clés, quasiment en temps réel.<br/><br/>Coffre de hello √ fournit une interface unique, quelle que soit la coffres combien avoir dans Azure, les régions qu’ils prise en charge et les applications qui utilisent les. |

Toute personne disposant d’un abonnement Azure peut créer et utiliser des coffres de clés. Bien que Key Vault procure des avantages aux développeurs et aux administrateurs de sécurité, il peut être implémenté et géré par l’administrateur d’une organisation qui gère les autres services Azure pour cette dernière. Par exemple, cet administrateur serait connectez-vous avec un abonnement Azure, créez un coffre pour l’organisation de hello dans les clés de toostore et ensuite être chargé pour les tâches opérationnelles, telles que :

* créer ou importer une clé ou un secret ;
* supprimer ou effacer une clé ou un secret ;
* Autoriser les utilisateurs ou applications tooaccess hello coffre de clés, afin qu’ils peuvent ensuite gérer ou utiliser ses clés et les clés secrètes
* configurer l’utilisation de la clé (par exemple, signer ou chiffrer) ;
* surveiller l’utilisation de clés.

Cet administrateur est ensuite fournir aux développeurs toocall URI à partir de leurs applications et fournir leur administrateur de sécurité avec les informations de journalisation de l’utilisation de la clé. 

   ![Vue d’ensemble Azure Key Vault][1]

Les développeurs peuvent également gérer les clés hello directement, en utilisant les API. Pour plus d’informations, consultez [hello guide du développeur de coffre de clés](key-vault-developers-guide.md).

## <a name="next-steps"></a>Étapes suivantes
Pour un didacticiel de prise en main d’un administrateur, consultez la page [Prise en main d’Azure Key Vault](key-vault-get-started.md).

Pour plus d’informations sur l’utilisation de la journalisation du coffre de clés, consultez [journalisation d’Azure Key Vault](key-vault-logging.md).

Pour en savoir plus sur l’utilisation des clés et des secrets avec Azure Key Vault, consultez la page [About Keys, Secrets, and Certificates](https://msdn.microsoft.com/library/azure/dn903623\(v=azure.1\).aspx) (À propos des clés, des secrets et des certificats).

<!--Image references-->
[1]: ./media/key-vault-whatis/AzureKeyVault_overview.png
