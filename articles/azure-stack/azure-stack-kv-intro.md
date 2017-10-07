---
title: "Présentation de coffre de clés de pile aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a>Introduction tooKey coffre dans la pile de Azure

## <a name="before-you-start"></a>Avant de commencer
Cet article suppose hello qui suit :

* Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés hello.  
* Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.  
* [PowerShell est configuré pour une utilisation avec Azure Stack](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a>Principes fondamentaux de Key Vault
Key Vault dans Azure Stack permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud. En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (comme les clés d’authentification, les clés des comptes de stockage, les clés de chiffrement de données, les fichiers .pfx et les mots de passe).

Coffre de clés rationalise le processus de gestion de clés hello et vous permet de contrôler toomaintain clés d’accès et de chiffrer vos données. Les développeurs peuvent créer des clés pour le développement et de test en quelques minutes et puis migrez en toute transparence les clés de tooproduction. Les administrateurs de sécurité peuvent accorder (et révoquer) tookeys d’autorisation, en fonction des besoins.

Toute personne disposant d’un abonnement Azure Stack peut créer et utiliser des coffres de clés. Bien que le coffre de clés avantages aux développeurs et administrateurs de sécurité, peut être implémenté et géré par l’administrateur du cloud hello qui gère les autres services Azure pile pour une organisation. Par exemple, administrateur du cloud hello peut se connecter avec un abonnement Azure pile, créer un archivage de l’organisation de hello dans les clés de toostore, puis être responsable de ces tâches opérationnelles :

* créer ou importer une clé ou un secret ;
* supprimer ou effacer une clé ou un secret ;
* Autoriser les utilisateurs ou applications tooaccess hello coffre de clés, afin qu’ils peuvent ensuite gérer ou utiliser ses clés et les clés secrètes
* configurer l’utilisation de la clé (par exemple, signer ou chiffrer) ;

administrateur du cloud Hello peut ensuite fournir aux développeurs toocall URI à partir de leurs applications et fournir un administrateur de sécurité avec les informations de journalisation de l’utilisation de la clé.

Les développeurs peuvent également gérer les clés hello directement, en utilisant les API. Pour plus d’informations, consultez le guide du développeur hello coffre de clés.

## <a name="scenarios"></a>Scénarios
Hello tableau suivant décrit certains des scénarios hello où le coffre de clés peuvent aider à répondre aux besoins de hello de développeurs et administrateurs de sécurité :

### <a name="developer-for-an-azure-stack-application"></a>Développeur d’une application Azure Stack
**Problème**: je veux toowrite une application pour la pile de Azure qui utilise des clés de signature et de chiffrement, mais je veux ces toobe externe à partir de mon application afin que la solution de hello est adaptée à une application qui est distribuée géographiquement.

**Solution** : Les clés sont stockées dans un coffre et appelées par un URI quand c’est nécessaire.

### <a name="developer-for-software-as-a-service-saas"></a>Développeur de logiciels SaaS (Software as a service)
**Problème :** je ne souhaite pas responsabilité de responsabilité ou potentiel hello pour les clés et les secrets de mon client.

**Solution :** Les clients peuvent importer leurs propres clés dans Azure Stack et les gérer. Je souhaite tooown des clients et que vous gérer leurs clés, je peux vous concentrer sur les effectuant que faire mieux, qui est fournissant des fonctionnalités de logiciel hello core.

### <a name="chief-security-officer-cso"></a>Responsable de la sécurité
**Problème :** je souhaite toomake que mon organisation se trouve dans le contrôle du cycle de vie de clé hello et que vous pouvez surveiller l’utilisation de la clé.

**Solution :** Key Vault a été conçu de façon que Microsoft ne puisse pas voir ni extraire vos clés.  Lorsqu’une application doit tooperform les opérations de chiffrement à l’aide de clés de clients, le coffre de clés procède au nom de l’application hello. application Hello ne voit pas les clés de clients hello.  Bien que nous utilisons plusieurs services de la pile d’Azure et les ressources, je veux clés de hello toomanage à partir d’un emplacement unique dans la pile de Azure. coffre de Hello fournit une interface unique, quelle que soit la coffres combien vous avez dans la pile d’Azure, les régions de leur prise en charge et les applications qui utilisent les.

## <a name="next-steps"></a>Étapes suivantes

* [Gérer le coffre de clés dans la pile d’Azure à l’aide du portail de hello](azure-stack-kv-manage-portal.md)  
* [Gérer Key Vault dans Azure Stack en utilisant PowerShell](azure-stack-kv-manage-powershell.md)
