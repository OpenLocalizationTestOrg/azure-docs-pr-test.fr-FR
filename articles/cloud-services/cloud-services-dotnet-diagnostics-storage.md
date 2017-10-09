---
title: "aaaStore et afficher les données de Diagnostic dans le stockage Azure | Documents Microsoft"
description: "Obtenir des données de diagnostics Microsoft Azure dans Azure Storage et les afficher"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Stocker et afficher des données de diagnostic dans Azure Storage
Données de diagnostic ne sont pas définitivement stockées, sauf si vous le transférez toohello l’émulateur de stockage Microsoft Azure ou tooAzure stockage. Une fois dans le stockage, elles peuvent être affichées avec un des outils disponibles.

## <a name="specify-a-storage-account"></a>Spécifiez un compte de stockage
Vous spécifiez le compte de stockage hello que vous souhaitez toouse dans le fichier ServiceConfiguration.cscfg de hello. les informations de compte Hello sont définies comme une chaîne de connexion dans un paramètre de configuration. Hello exemple suivant montre hello chaîne de connexion par défaut créé pour un nouveau projet de Service Cloud dans Visual Studio :

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Vous pouvez modifier ces informations de compte de connexion chaîne tooprovide pour un compte de stockage Azure.

Selon le type de données de diagnostic qui sont collectées de hello, Azure Diagnostics utilise le service d’objets Blob hello ou service de Table hello. Hello tableau suivant répertorie les sources de données hello qui sont conservées et leur format.

| Source de données | Format de stockage |
| --- | --- |
| Journaux Azure |Table |
| Journaux IIS 7.0 |Blob |
| Journaux d’infrastructure de diagnostics Azure |Table |
| Journaux de suivi de requête ayant échoué |Blob |
| Journaux d'événements Windows |Table |
| Compteurs de performances |Table |
| Vidages sur incident |Blob |
| Journaux d'erreurs personnalisés |Blob |

## <a name="transfer-diagnostic-data"></a>Transférer les données de diagnostic
Pour le SDK 2.5 et versions ultérieures, les données de diagnostic hello demande tootransfer peuvent se produire via le fichier de configuration hello. Vous pouvez transférer des données de diagnostic à intervalles planifiés, tel que spécifié dans la configuration de hello.

Pour 2.4 du Kit de développement logiciel précédent et vous pouvez demander des données de diagnostic hello tootransfer via le fichier de configuration hello ainsi que par programme. méthode Hello vous permet également de toodo les transferts à la demande.

> [!IMPORTANT]
> Lorsque vous transférez des données de diagnostic tooan compte de stockage Azure, vous encourez des frais pour les ressources de stockage hello par des données de diagnostic.
> 
> 

## <a name="store-diagnostic-data"></a>Stockez les données de diagnostic
Données du journal sont stockées dans le stockage Blob ou de Table avec hello nom :

**Tables**

* **WadLogsTable** - journaux écrits dans le code à l’aide d’écouteur de suivi hello.
* **WADDiagnosticInfrastructureLogsTable** : modifications de configuration et d’analyse de diagnostic.
* **WADDirectoriesTable** – répertoires de contrôle qui analyse le diagnostic hello.  Cela inclut les journaux IIS, les journaux de requêtes ayant échoué et les répertoires personnalisés IIS.  emplacement Hello du fichier journal de blob hello est spécifié dans le champ de conteneur hello et hello nom de hello blob est dans le champ RelativePath de hello.  champ de AbsolutePath Hello indique l’emplacement de hello et le nom du fichier de hello tel qu’il existait sur hello machine virtuelle Azure.
* **WADPerformanceCountersTable** : les compteurs de performance.
* **WADWindowsEventLogsTable** : journaux des événements Windows.

**Objets blob**

* **WAD-control-container** : (uniquement pour les SDK 2.4 et précédente) contient les fichiers de configuration XML hello qui contrôle hello diagnostics Azure.
* **wad-iis-failedreqlogfiles** : contient des informations tirées des journaux de requêtes de IIS ayant échoué.
* **wad-iis-logfiles** : contient des informations sur les journaux IIS.
* **« custom »** – conteneur personnalisé basé sur la configuration des répertoires qui sont contrôlés par le moniteur de diagnostic hello.  nom de Hello de ce conteneur d’objets blob est spécifié dans WADDirectoriesTable.

## <a name="tools-tooview-diagnostic-data"></a>Données de diagnostic Tools tooview
Plusieurs outils sont les données de salutation tooview disponibles une fois qu’il toostorage transféré. Par exemple :

* L’Explorateur de serveurs dans Visual Studio - si vous avez installé hello Windows Azure Tools pour Microsoft Visual Studio, vous pouvez utiliser nœud hello Azure dans l’Explorateur de serveurs tooview données en lecture seule blob et de table à partir de vos comptes de stockage Azure. Vous pouvez afficher des données à partir de votre compte d’émulateur de stockage local et de comptes de stockage que vous avez créés pour Azure. Pour plus d’informations, consultez [Consultation et gestion des ressources de stockage avec l’Explorateur de serveurs](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, OSX et Linux.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) inclut Azure Diagnostics Manager qui vous permet de tooview, télécharger et gérer des données de diagnostic hello collectées par les applications de hello s’exécutant sur Azure.

## <a name="next-steps"></a>Étapes suivantes
[Flux de hello de trace dans une application de Services de Cloud avec Azure Diagnostics](cloud-services-dotnet-diagnostics-trace-flow.md)

