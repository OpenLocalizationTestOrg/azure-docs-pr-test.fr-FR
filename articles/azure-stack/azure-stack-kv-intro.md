---
title: "Présentation d’Azure Stack Key Vault | Microsoft Docs"
description: "Découvrez comment Azure Stack Key Vault gère les clés et les secrets"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: dc8b5cb299da74c88aa5ae82636dc345ddd45a2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a>Introduction à Key Vault dans Azure Stack

## <a name="before-you-start"></a>Avant de commencer
Cet article part des principes suivants :

* Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés.  
* Les utilisateurs doivent [s’abonner à une offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service Key Vault.  
* [PowerShell est configuré pour une utilisation avec Azure Stack](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a>Principes fondamentaux de Key Vault
Key Vault dans Azure Stack permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud. En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (comme les clés d’authentification, les clés des comptes de stockage, les clés de chiffrement de données, les fichiers .pfx et les mots de passe).

Key Vault rationalise le processus de gestion de clés et vous permet de garder le contrôle des clés qui accèdent à vos données et les chiffrent. Les développeurs peuvent créer des clés pour le développement et le test en quelques minutes, puis les migrer en toute transparence en clés de production. Les administrateurs de sécurité peuvent accorder (et annuler) les autorisations sur les clés, si nécessaire.

Toute personne disposant d’un abonnement Azure Stack peut créer et utiliser des coffres de clés. Bien que le coffre de clés avantages aux développeurs et administrateurs de sécurité, peut être implémenté et géré par l’administrateur du cloud qui gère les autres services Azure pile pour une organisation. Par exemple, l’administrateur du cloud pouvez vous connecter avec un abonnement Azure pile, créez un coffre pour l’organisation dans lequel stocker les clés, puis être responsable de ces tâches opérationnelles :

* créer ou importer une clé ou un secret ;
* supprimer ou effacer une clé ou un secret ;
* autoriser des utilisateurs ou des applications à accéder au coffre de clés, afin qu’ils puissent gérer ou utiliser ses clés et ses clés secrètes ;
* configurer l’utilisation de la clé (par exemple, signer ou chiffrer) ;

L’administrateur du cloud peut ensuite fournir aux développeurs des URI à appeler à partir de leurs applications et fournir un administrateur de sécurité avec les informations de journalisation de l’utilisation de la clé.

Les développeurs peuvent également gérer les clés directement à l’aide d’API. Pour plus d’informations, consultez le guide du développeur Key Vault.

## <a name="scenarios"></a>Scénarios
Le tableau suivant décrit certains des scénarios où Key Vault peut permettre de répondre aux besoins des développeurs et des administrateurs de sécurité :

### <a name="developer-for-an-azure-stack-application"></a>Développeur d’une application Azure Stack
**Problème** : Je veux écrire une application pour Azure Stack qui utilise des clés pour la signature et le chiffrement, mais je veux que ces clés soient externes à mon application, afin que la solution soit adaptée à une application répartie au niveau géographique.

**Solution** : Les clés sont stockées dans un coffre et appelées par un URI quand c’est nécessaire.

### <a name="developer-for-software-as-a-service-saas"></a>Développeur de logiciels SaaS (Software as a service)
**Problème** : Je ne veux pas prendre la responsabilité des clés et des secrets pour mes clients.

**Solution :** Les clients peuvent importer leurs propres clés dans Azure Stack et les gérer. Je veux que les clients détiennent et gèrent leurs clés, pour pouvoir me concentrer sur ce que je fais le mieux, c’est-à-dire fournir les principales fonctionnalités du logiciel.

### <a name="chief-security-officer-cso"></a>Responsable de la sécurité
**Problème** : Je veux être sûr que mon organisation contrôle le cycle de vie des clés et puisse surveiller leur utilisation.

**Solution :** Key Vault a été conçu de façon que Microsoft ne puisse pas voir ni extraire vos clés.  Quand une application doit effectuer des opérations de chiffrement en utilisant des clés des clients, Key Vault le fait à la place de l’application. L’application ne voit pas les clés des clients.  Même si nous utilisons plusieurs services et ressources Azure Stack, je veux gérer les clés à partir d’un seul emplacement dans Azure. Le coffre fournit une interface unique, indépendamment du nombre de coffres dont vous disposez dans Azure Stack, des régions qui sont prises en charge et des applications qui les utilisent.

## <a name="next-steps"></a>Étapes suivantes

* [Gérer Key Vault dans Azure Stack en utilisant le portail](azure-stack-kv-manage-portal.md)  
* [Gérer Key Vault dans Azure Stack en utilisant PowerShell](azure-stack-kv-manage-powershell.md)
