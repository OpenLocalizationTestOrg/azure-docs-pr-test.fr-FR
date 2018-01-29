---
title: "Utilisation d’une identité du service administré de machine virtuelle Azure avec les kits de développement logiciel Azure"
description: "Exemples de code pour l’utilisation de kits de développement Azure avec une MSI de machine virtuelle Azure."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/01/2017
ms.author: bryanla
ms.openlocfilehash: 6c9bd57080c95e4aad45515a0814471194261286
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2018
---
# <a name="how-to-use-an-azure-vm-managed-service-identity-msi-with-azure-sdks"></a>Utilisation d’une identité du service administré (MSI) de machine virtuelle Azure avec les kits de développement logiciel Azure 

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]  
Cet article fournit une liste d’exemples de kits de développement logiciel, qui illustrent l’utilisation de la prise en charge du MSI par leurs kits de développement logiciel Azure respectifs.

## <a name="prerequisites"></a>Conditions préalables

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

> [!IMPORTANT]
> - Tous les scripts/exemples de code de cet article supposent que le client exécute une machine virtuelle avec le paramètre MSI activé. Utilisez la fonctionnalité « Se connecter » de machine virtuelle dans le portail Azure, pour vous connecter à distance à votre machine virtuelle. Pour plus d’informations sur l’activation de MSI sur une machine virtuelle, consultez [Configurer une identité du service administré (MSI) d’une machine virtuelle à l’aide du portail Azure](msi-qs-configure-portal-windows-vm.md), ou l’un des autres articles (à l’aide de PowerShell, CLI, d’un modèle ou d’un kit de développement logiciel Azure). 

## <a name="sdk-code-samples"></a>Exemples de code de kit de développement logiciel

| Foundation             | Exemple de code |
| --------------- | ----------- |
| .NET            | [Déployer un modèle Azure Resource Manager à partir d’une machine virtuelle Windows à l’aide de Managed Service Identity](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet) |
| .NET Core       | [Appeler les services Azure à partir d’une machine virtuelle Linux à l’aide de Managed Service Identity](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/) |
| Node.js         | [Gérer des ressources à l’aide d’une identité du service administré](https://azure.microsoft.com/resources/samples/resources-node-manage-resources-with-msi/) |
| Python          | [Utiliser une identité du service administré pour s’authentifier simplement depuis l’intérieur d’une machine virtuelle](https://azure.microsoft.com/resources/samples/resource-manager-python-manage-resources-with-msi/) |
| Ruby            | [Gérer des ressources à partir d’une machine virtuelle avec le paramètre MSI activé](https://azure.microsoft.com/resources/samples/resources-ruby-manage-resources-with-msi/) |

## <a name="related-content"></a>Contenu connexe

- Consultez [Kits de développement logiciel Azure](https://azure.microsoft.com/downloads/) pour obtenir la liste complète des ressources des kits de développement Azure, y compris les téléchargements de bibliothèque, la documentation et bien plus encore.
- Pour activer l’identité du service administré sur une machine virtuelle Azure, consultez [Configurer l’identité du service administré (MSI) d’une machine virtuelle via le portail Azure](msi-qs-configure-portal-windows-vm.md).

Utilisez la section Commentaires suivante pour donner votre avis et nous aider à affiner et à mettre en forme notre contenu.








