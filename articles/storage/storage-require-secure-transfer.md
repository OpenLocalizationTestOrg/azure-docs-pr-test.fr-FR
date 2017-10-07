---
title: "aaaRequire un transfert sécurisé dans le stockage Azure | Documents Microsoft"
description: "En savoir plus sur la fonctionnalité de « Requièrent un transfert sécurisé » hello pour le stockage Azure et comment tooenable il."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Exiger un transfert sécurisé

option de Hello » un transfert sécurisé requis » améliore la sécurité de hello de votre compte de stockage en autorisant uniquement les demandes de compte de stockage toohello à partir des connexions sécurisées. Par exemple, lors de l’appel tooaccess de l’API REST de votre compte de stockage, vous devez vous connecter à l’aide de HTTPS. Toutes les requêtes utilisant HTTP sont rejetées lorsque l’option Transfert sécurisé requis est activée.

Lorsque vous utilisez le service de fichiers Azure hello, toute connexion sans chiffrement échoue lorsque « Sécuriser le transfert requis » est activée. Cela inclut des scénarios à l’aide de SMB 2.1, SMB 3.0 sans chiffrement et certaines versions de hello client Linux SMB. 

Par défaut, l’option de hello » un transfert sécurisé requis » est désactivée.

> [!NOTE]
> Étant donné que le stockage Azure ne prend pas en charge HTTPS pour les noms de domaine personnalisés, cette option n’est pas appliquée lorsque vous utilisez un nom de domaine personnalisé.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Activer « Transfert sécurisé requis » Bonjour portail Azure

Vous pouvez activer hello » un transfert sécurisé requis » à la fois paramètre lorsque vous créez un compte de stockage dans hello [portail Azure](https://portal.azure.com)et pour les comptes de stockage existant.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Exiger un transfert sécurisé lorsque vous créez un compte de stockage

1. Ouvrez hello **créer le compte de stockage** panneau Bonjour portail Azure.
1. Sous **Transfert sécurisé requis**, sélectionnez **Activé**.

  ![capture d’écran](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Exiger un transfert sécurisé pour un compte de stockage existant

1. Sélectionnez un compte de stockage existant dans hello portail Azure.
1. Sélectionnez **Configuration** sous **paramètres** dans le panneau de menu de compte de stockage hello.
1. Sous **Transfert sécurisé requis**, sélectionnez **Activé**.

  ![capture d’écran](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Activer le paramètre « Transfert sécurisé requis » par programmation

nom du paramètre Hello est _supportsHttpsTrafficOnly_ dans les propriétés de compte de stockage. Vous pouvez activer « Transfert sécurisé requis » avec l’API REST, des outils ou des bibliothèques :

* **API REST** (Version : 2016-12-01) : [package de version](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (Version : 4.1.0) : [package de version](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (Version : 2.0.11) : [package de version](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (Version : 1.1.0) : [package de version](https://www.npmjs.com/package/azure-arm-storage/)
* **SDK .NET** (Version : 6.3.0) : [package de version](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **SDK Python** (Version : 1.1.0) : [package de version](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **SDK Ruby** (Version : 0.11.0) : [package de version](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Activer le paramètre « Transfert sécurisé requis » avec l’API REST

toosimplify test avec l’API REST, vous pouvez utiliser [ArmClient](https://github.com/projectkudu/ARMClient) toocall à partir de la ligne de commande.

 Vous pouvez utiliser sous le paramètre de hello toocheck de ligne de commande avec hello API REST :

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

Dans la réponse de hello, vous pouvez trouver _supportsHttpsTrafficOnly_ paramètre. Exemple :

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

Vous pouvez utiliser sous le paramètre de hello tooenable de ligne de commande avec hello API REST :

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Exemple de code Input.json :
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Étapes suivantes
Le stockage Azure fournit un ensemble complet des fonctionnalités de sécurité, qui ensemble permettent aux développeurs de toobuild des applications sécurisées. Pour plus d’informations, visitez hello [Guide de sécurité de stockage](storage-security-guide.md).
