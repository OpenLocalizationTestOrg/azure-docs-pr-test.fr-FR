---
title: "problèmes d’Azure Data Factory aaaTroubleshoot"
description: "Découvrez comment tootroubleshoot problèmes à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Résolution des problèmes liés à Data Factory
Cet article propose des conseils pour la résolution des problèmes d'utilisation d'Azure Data Factory. Cet article ne répertorie pas tous les problèmes possibles hello lors de l’utilisation du service de hello, mais elle traite de certains problèmes et les conseils de dépannage générales.   

## <a name="troubleshooting-tips"></a>Conseils de dépannage
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Erreur : l’abonnement de hello n’est pas inscrit toouse, espace de noms 'Microsoft.DataFactory'
Si vous recevez cette erreur, fournisseur de ressources Azure Data Factory hello n’a pas été inscrit sur votre ordinateur. Hello suivant :

1. Lancez Azure PowerShell.
2. Ouvrez une session dans tooyour compte Azure à l’aide de hello commande suivante.

    ```powershell
    Login-AzureRmAccount
    ```
3. Exécutez hello suivant le fournisseur de commandes tooregister hello Azure Data Factory.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Problème : erreur non autorisée lors de l’exécution d’une applet de commande Data Factory
Vous utilisez probablement pas le droit de hello compte Azure ou d’abonnement avec hello Azure PowerShell. Utilisez hello suivant d’applets de commande tooselect hello droite toouse de compte et votre abonnement Azure avec hello Azure PowerShell.

1. Connexion AzureRmAccount - hello utiliser l’ID d’utilisateur et mot de passe
2. Get-AzureRmSubscription - afficher tous les hello d’abonnements pour le compte de hello.
3. Sélectionnez-AzureRmSubscription &lt;nom de l’abonnement&gt; -sélectionnez l’abonnement hello. Utilisez hello identique à celui vous utilisez toocreate une fabrique de données sur hello portail Azure.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Problème : Ne parviennent pas toolaunch le programme d’installation Express du passerelle de gestion des données à partir du portail Azure
le programme d’installation Express de Hello pour hello passerelle de gestion des données requiert Internet Explorer ou un navigateur web compatible de Microsoft ClickOnce. Si le programme d’installation Express de hello échoue toostart, effectuez l’une des suivantes de hello :

* Utilisez Internet Explorer ou un navigateur web compatible Microsoft ClickOnce.

    Si vous utilisez Chrome, accédez toohello [Boutique Chrome](https://chrome.google.com/webstore/), recherche avec « ClickOnce » (mot clé), choisissez une des extensions de ClickOnce hello et installez-le.

    Hello même pour Firefox (complément installation). Cliquez sur le bouton de Menu Ouvrir dans la barre d’outils de hello (trois lignes horizontales dans l’angle supérieur droit de hello) sur les modules complémentaires, recherche avec « ClickOnce » (mot clé), choisissez une des extensions de ClickOnce hello et installez-le.
* Hello d’utilisation **le programme d’installation manuelle** lien affiché sur hello même panneau dans le portail de hello. Vous utilisez ce fichier d’installation toodownload approche et l’exécutez manuellement. Une fois l’installation de hello réussie, vous voyez la boîte de dialogue de Configuration de gestion des données à l’aide de la passerelle hello. Hello de copie **clé** à partir de l’écran de portail hello et utilisez dans hello configuration manager toomanually inscrire la passerelle de hello auprès du service de hello.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Problème : Ne parviennent pas tooconnect tooon local SQL Server
Lancez **Gestionnaire de Configuration de passerelle de gestion de données** hello ordinateur passerelle et utiliser hello **dépannage** onglet tootest hello connexion tooSQL Server à partir de l’ordinateur de passerelle hello. Consultez [Résolution des problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour obtenir des conseils sur la résolution des problèmes de connexion/passerelle.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Problème : l’état des tranches d’entrée est En attente depuis longtemps
les tranches Hello pourrait être **attente** état en raison des raisons de toovarious. Une des raisons courantes de hello est que hello **externe** propriété n’est pas définie trop**true**. Tout jeu de données est l’étendue de produits hello en dehors d’Azure Data Factory doit être marquée avec **externe** propriété. Cette propriété indique que les données hello pas sauvegardés par les pipelines au sein de la fabrique de données hello et externes. tranches de données Hello sont marqués comme **prêt** une fois que les données de salutation ne sont disponibles dans le store respectif de hello.

Consultez hello exemple pour l’utilisation de hello Hello suivant **externe** propriété. Vous pouvez éventuellement spécifier **externalData*** lorsque vous définissez tootrue externe.

Consultez l’article [Jeux de données](data-factory-create-datasets.md) pour plus d’informations sur cette propriété.

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve hello erreur, ajoutez hello **externe** propriété et hello facultatif **externalData** section Définition JSON de toohello de table d’entrée de hello et recréer la table de hello.

### <a name="problem-hybrid-copy-operation-fails"></a>Problème : échec de l’opération de copie hybride
Consultez [résoudre les problèmes de passerelle](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) pour stocker les problèmes tootroubleshoot avec la copie vers/à partir de des données locales à l’aide des étapes hello passerelle de gestion des données.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Problème : échec de l’approvisionnement HDInsight à la demande
Lorsque vous utilisez un service lié de type HDInsightOnDemand, vous devez toospecify un linkedServiceName qui pointe tooan stockage d’objets Blob Azure. Service de fabrique de données utilise ce stockage toostore journaux et les fichiers de prise en charge pour votre cluster HDInsight de la demande.  Parfois, l’approvisionnement d’un cluster de HDInsight à la demande échoue avec hello l’erreur suivante :

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Cette erreur indique généralement que hello hello du compte de stockage spécifié dans hello linkedServiceName se trouve pas dans hello Datacenter même emplacement où l’approvisionnement HDInsight hello qui se passe. Exemple : Si votre fabrique de données est dans l’ouest des États-Unis et hello stockage Azure est est des États-Unis, hello à la demande de configuration échoue dans l’ouest des États-Unis.

En outre, il existe une seconde propriété JSON additionalLinkedServiceNames avec laquelle les comptes de stockage supplémentaires peuvent être spécifiés dans HDInsight à la demande. Ces comptes de stockage supplémentaire doivent être Bonjour même emplacement que le cluster HDInsight de hello, ou si elle échoue avec hello même message d’erreur.

### <a name="problem-custom-net-activity-fails"></a>Problème : échec de l’activité .NET personnalisée
Consultez la page [Déboguer un pipeline avec une activité personnalisée](data-factory-use-custom-activities.md#troubleshoot-failures) pour obtenir des instructions détaillées.

## <a name="use-azure-portal-tootroubleshoot"></a>Utilisez tootroubleshoot portail Azure
### <a name="using-portal-blades"></a>Utilisation des panneaux du portail
Consultez la page [Surveiller le pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) pour obtenir la procédure.

### <a name="using-monitor-and-manage-app"></a>Utilisation de l’application Surveillance et gestion
Consultez [Surveiller et gérer les pipelines Data Factory à l’aide de l’application Surveillance et gestion](data-factory-monitor-manage-app.md) pour plus d’informations.

## <a name="use-azure-powershell-tootroubleshoot"></a>Utiliser Azure PowerShell tootroubleshoot
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Utiliser Azure PowerShell tootroubleshoot une erreur
Consultez la page [Surveiller les pipelines Data Factory à l’aide d’Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) pour plus d’informations.

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
