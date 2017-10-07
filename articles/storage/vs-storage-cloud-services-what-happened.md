---
title: "aaaWhat est devenu toomy projet de service cloud ? | Microsoft Docs"
description: "Décrit ce qui se passe dans un projet de services cloud après que connexion tooan compte de stockage Azure à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 65662dde45dd75bca1b57022283f76305f95e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-cloud-services-project-visual-studio-azure-storage-connected-service"></a>Les services de cloud computing s’est produit toomy de projets (Visual Studio Azure Storage connecté service) ?
## <a name="references-added"></a>Références ajoutées
package NuGet de stockage Azure de Hello a été ajouté le projet de Visual Studio tooyour.  
Ce package ajoute hello suivant des références .NET :

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.Configuration**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **System.Data**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Chaîne de connexion pour Azure Storage ajoutée
Éléments ont été créées avec la chaîne de connexion et la clé du compte de stockage hello sélectionné. Les modifications ont été apportées toohello fichiers suivants :

* **ServiceDefinition.csdef**
* **ServiceConfiguration.Cloud.cscfg**
* **ServiceConfiguration.Local.cscfg**

