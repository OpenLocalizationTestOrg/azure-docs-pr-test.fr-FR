---
title: "Comment configurer une machine virtuelle Azure activée par MSI à l’aide d’un Kit de développement logiciel (SDK) Azure"
description: "Instructions détaillées sur la configuration et l’utilisation de l’identité du service administré (MSI, Managed Service Identity) sur une machine virtuelle Azure, à l’aide d’un Kit de développement logiciel (SDK) Azure."
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
ms.date: 09/28/2017
ms.author: bryanla
ms.openlocfilehash: d5fb9decd1417a51c85f23d6b178c8a86cf292bd
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="configure-a-vm-managed-service-identity-msi-using-an-azure-sdk"></a>Configurer l’identité du service administré (MSI) d’une machine virtuelle à l’aide d’un Kit de développement logiciel (SDK) Azure

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]

La MSI fournit des services Azure avec une identité gérée automatiquement dans Azure Active Directory. Vous pouvez utiliser cette identité pour vous authentifier sur n’importe quel service prenant en charge l’authentification Azure AD, sans avoir d’informations d’identification dans votre code. 

Dans cet article, vous allez découvrir comment activer et supprimer la MSI d’une machine virtuelle Azure à l’aide d’un Kit de développement logiciel (SDK) Azure.

## <a name="prerequisites"></a>Composants requis

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

## <a name="azure-sdks-with-msi-support"></a>Kits de développement logiciel (SDK) Azure avec prise en charge de MSI 

Azure prend en charge plusieurs plates-formes de programmation via une série de [Kits de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads). Plusieurs d’entre elles ont été mises à jour pour prendre en charge les MSI, et donnent des exemples illustrant leur utilisation. Cette liste a été mise à jour, suite à l’ajout d’une prise en charge supplémentaire :

| Foundation | Exemple |
| --- | ------ | 
| .NET   | [Gérer une ressource à partir d’une machine virtuelle avec le paramètre MSI activé](https://azure.microsoft.com/resources/samples/aad-dotnet-manage-resources-from-vm-with-msi/) |
| Java   | [Gérer le stockage à partir d’une machine virtuelle avec le paramètre MSI activé](https://azure.microsoft.com/resources/samples/compute-java-manage-resources-from-vm-with-msi-in-aad-group/)|
| Node.js| [Créer une machine virtuelle avec le paramètre MSI activé](https://azure.microsoft.com/resources/samples/compute-node-msi-vm/) |
| Python | [Créer une machine virtuelle avec le paramètre MSI activé](https://azure.microsoft.com/resources/samples/compute-python-msi-vm/) |
| Ruby   | [Créer une machine virtuelle Azure avec une MSI](https://azure.microsoft.com/resources/samples/compute-ruby-msi-vm/) |

## <a name="next-steps"></a>Étapes suivantes

- Consultez les articles connexes répertoriés sous la section relative à la configuration de MSI pour une machine virtuelle Azure pour savoir comment utiliser les modèles de portail Azure, PowerShell, CLI et des ressources.

Utilisez la section Commentaires suivante pour donner votre avis et nous aider à affiner et à mettre en forme notre contenu.
