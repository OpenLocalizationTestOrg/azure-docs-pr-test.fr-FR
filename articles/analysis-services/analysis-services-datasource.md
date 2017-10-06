---
title: "sources d’aaaData prises en charge dans Azure Analysis Services | Documents Microsoft"
description: "Décrit les sources de données prises en charge pour les modèles de données dans Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Sources de données prises en charge dans Azure Analysis Services
Serveurs Analysis Services Windows Azure prend en charge la connexion toodata sources dans le cloud de hello et localement dans votre organisation. Sources de données prises en charge supplémentaires sont ajoutées en tout temps hello. Vérifiez ces données régulièrement. 

Hello les sources de données suivantes est actuellement prises en charge :

| Cloud  |
|---|
| Stockage Blob Azure*  |
| Base de données SQL Azure  |
| Azure Data Warehouse |


| Local  |   |   |   |
|---|---|---|---|
| Base de données Access  | Dossier* | Oracle Database  | Base de données Teradata |
| Active Directory*  | Document JSON*  | Base de données PostgreSQL*  |Table XML* |
| Analysis Services  | Lignes issues d’un fichier binaire*  | SAP HANA*  |
| Système de plateforme d’analyse  | MySQL Database  | SAP Business Warehouse*  | |
| Dynamics CRM*  | Flux OData*  | SharePoint*  |
| Classeur Excel  | Requête ODBC  | Base de données SQL  |
| Exchange*  | OLE DB  | Base de données Sybase  |

\* Modèles Tabular 1400 uniquement. 

> [!IMPORTANT]
> Connexion de données local tooon sources requièrent un [passerelle de données locale](analysis-services-gateway.md) installé sur un ordinateur dans votre environnement.

## <a name="data-providers"></a>Fournisseurs de données

Modèles de données dans Azure Analysis Services peuvent nécessiter des différents fournisseurs de données lors de la connexion des sources de données toocertain. Dans certains cas, les modèles tabulaires connexion toodata à l’aide des fournisseurs natifs tels que SQL Server Native Client (SQLNCLI11) peuvent retourner une erreur.

Pour les modèles de données qui connectent des données de cloud tooa source comme base de données SQL Azure, si vous utilisez des fournisseurs natifs que SQLOLEDB, vous pouvez voir le message d’erreur : **« fournisseur hello 'SQLNCLI11.1' n’est pas inscrit ».** Ou, si vous avez un DirectQuery modèle de connexion des sources de données tooon local, si vous utilisez des fournisseurs natifs vous pouvez voir le message d’erreur : **« erreur de création du jeu de lignes OLE DB. Syntaxe incorrecte à proximité de 'LIMITE' »**.

Hello suivant des fournisseurs de source de données est pris en charge en mémoire ou DirectQuery des modèles de données lors de la connexion toodata sources dans le cloud de hello ou locale :

### <a name="cloud"></a>Cloud
| **Source de données** | **En mémoire** | **DirectQuery** |
|  --- | --- | --- |
| Azure SQL Data Warehouse |Fournisseur de données .NET Framework pour SQL Server |Fournisseur de données .NET Framework pour SQL Server |
| Azure SQL Database |Fournisseur de données .NET Framework pour SQL Server |Fournisseur de données .NET Framework pour SQL Server | |

### <a name="on-premises-via-gateway"></a>Local (via une passerelle)
|**Source de données** | **En mémoire** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |Fournisseur de données .NET Framework pour SQL Server |
| SQL Server |Fournisseur Microsoft OLE DB pour SQL Server |Fournisseur de données .NET Framework pour SQL Server | |
| SQL Server |Fournisseur de données .NET Framework pour SQL Server |Fournisseur de données .NET Framework pour SQL Server | |
| Oracle |Fournisseur Microsoft OLE DB pour Oracle |Fournisseur de données Oracle pour .NET | |
| Oracle |Fournisseur de données Oracle pour .NET |Fournisseur de données Oracle pour .NET | |
| Teradata |Fournisseur OLE DB pour Teradata |Fournisseur de données Teradata pour .NET | |
| Teradata |Fournisseur de données Teradata pour .NET |Fournisseur de données Teradata pour .NET | |
| Système de plateforme d’analyse |Fournisseur de données .NET Framework pour SQL Server |Fournisseur de données .NET Framework pour SQL Server | |

> [!NOTE]
> Vérifiez que des fournisseurs 64 bits sont installés lors de l’utilisation d’une passerelle locale.
> 
> 

Lorsque vous migrez une tooAzure de modèle tabulaire SQL Server Analysis Services locaux Analysis Services, il peut être fournisseur de hello toochange nécessaire.

**toospecify un fournisseur de source de données**

1. Dans SSDT > **Explorateur de modèles tabulaires** > **Sources de données**, cliquez sur une connexion de source de données, puis cliquez sur **Modifier la source de données**.
2. Dans **modifier la connexion**, cliquez sur **avancé** fenêtre de propriétés tooopen hello avance.
3. Dans **Set avancé Properties** > **fournisseurs**, puis sélectionnez hello fournisseur approprié.

## <a name="impersonation"></a>Emprunt d’identité
Dans certains cas, il peut être nécessaire toospecify un compte d’emprunt d’identité différent. Le compte d’emprunt d’identité peut être spécifié dans SSDT ou SSMS.

Pour les sources de données locales :

* Si vous utilisez l’authentification SQL, l’emprunt d’identité doit être le compte de service.
* Si vous utilisez l’authentification Windows, définissez l’utilisateur/le mot de passe Windows. Pour SQL Server, l’authentification Windows avec un compte d’emprunt d’identité spécifique est pris en charge pour les modèles de données en mémoire uniquement.

Pour les sources de données cloud :

* Si vous utilisez l’authentification SQL, l’emprunt d’identité doit être le compte de service.

## <a name="next-steps"></a>Étapes suivantes
Si vous avez des sources de données locales, être vraiment tooinstall hello [passerelle locale](analysis-services-gateway.md).   
toolearn savoir plus sur la gestion de votre serveur dans SSDT ou SSMS, consultez [gérer votre serveur](analysis-services-manage.md).

