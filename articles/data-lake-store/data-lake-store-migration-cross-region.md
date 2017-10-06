---
title: "aaaAzure la migration entre régions Data Lake Store | Documents Microsoft"
description: "Découvrez la migration entre les régions pour Azure Data Lake Store."
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Migration Data Lake Store entre les régions

Azure Data Lake Store est disponible dans les régions de nouveau, vous pouvez choisir une migration à usage unique, parti tootake de nouvelle région de hello toodo. Découvrez quels tooconsider lorsque vous planifiez et terminez la migration de hello.

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Pour plus d’informations, consultez [Créer votre compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Data Lake Store dans deux régions différentes**. Pour plus d’informations, consultez [Prise en main d’Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. Pour plus d’informations, consultez [Introduction tooAzure Data Factory](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Considérations relatives à la migration

Identifiez tout d’abord la stratégie de migration hello qui convient le mieux pour votre application qui écrit, lit ou traite les données de Data Lake Store. Lorsque vous choisissez une stratégie, prendre en compte les exigences de disponibilité de votre application et temps d’arrêt hello qui se produit lors d’une migration. Par exemple, votre approche la plus simple peut être toouse hello « courbes d’élévation et MAJ » cloud migration modèle. Dans cette approche, vous suspendez application hello dans votre région existante toutes vos données sont copiées toohello nouvelle zone. Lorsque hello copie est terminée, vous reprenez votre application dans la nouvelle région de hello, puis supprimez les compte Data Lake Store ancien hello. Temps d’arrêt pendant la migration de hello est requis.

tooreduce temps d’arrêt, vous pouvez commencer immédiatement absorber les nouvelles données dans la nouvelle région de hello. Lorsque vous avez les données minimales hello si nécessaires, exécutez votre application dans la nouvelle région de hello. Dans l’arrière-plan de hello, continuer toocopy des données plus anciennes de hello Data Lake Store compte toohello nouveau Data Lake Store compte dans la nouvelle région de hello. À l’aide de cette approche, vous pouvez rendre la nouvelle zone de toohello hello commutateur avec peu de temps mort. Lorsque toutes les données plus anciennes hello a été copié, supprimer l’ancien compte Data Lake Store d’hello.

Autres tooconsider obtenir des informations importantes lorsque vous planifiez votre migration sont les suivantes :

* **Volume de données**. volume Hello de données (en gigaoctets, nombre de hello de fichiers et dossiers et ainsi de suite) affecte le temps de hello et ressources que nécessaires pour la migration de hello.

* **Nom du compte Data Lake Store**. nom du nouveau compte Hello dans la nouvelle région de hello doit être globalement unique. Par exemple, le nom hello de votre ancien compte Data Lake Store dans est des États-Unis 2 peut être contosoeastus2.azuredatalakestore.net. Vous pouvez nommer votre nouveau compte Data Lake Store dans la région Europe du Nord contosonortheu.azuredatalakestore.net.

* **Outils**. Nous vous recommandons d’utiliser hello [activité de copie de fabrique de données Azure](../data-factory/data-factory-azure-datalake-connector.md) toocopy les fichiers de Data Lake Store. Data Factory prend en charge le déplacement de données avec une fiabilité optimale et de hautes performances. Gardez à l’esprit que la fabrique de données copie uniquement arborescence des dossiers hello et le contenu des fichiers de hello. Vous devez toomanually s’appliquent à toutes les listes de contrôle d’accès (ACL) que vous utilisez dans hello ancien compte toohello nouveau compte. Pour plus d’informations, y compris les objectifs de performances pour les scénarios optimistes, consultez hello [guide de paramétrage et de performances de l’activité de copie](../data-factory/data-factory-copy-activity-performance.md). Si vous souhaitez que les données copiées plus rapidement, vous devrez peut-être toouse unités de déplacement de données Cloud supplémentaires. D’autres outils, tels que AdlCopy, ne permettent pas de copier de données entre différentes régions.  

* **Frais liés à la bande passante**. Des [frais liés à la bande passante](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) s’appliquent, car les données sont transférées en dehors d’une région Azure.

* **Listes de contrôle d’accès sur vos données**. Sécuriser vos données dans la nouvelle région de hello en appliquant les dossiers et les listes ACL toofiles. Pour plus d’informations, consultez [Sécurisation des données stockées dans Azure Data Lake Store](data-lake-store-secure-data.md). Nous vous recommandons d’utiliser hello migration tooupdate et ajuster vos ACL. Vous pourriez toouse paramètres tooyour actuel des paramètres similaires. Vous pouvez afficher les listes ACL hello est appliqués tooany fichier à l’aide de hello portail Azure, [applets de commande PowerShell](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), ou les kits de développement logiciel.  

* **Emplacement des services d’analyse**. Pour des performances optimales, vos services analytique, tels qu’Analytique de LAC de données Azure ou Azure HDInsight, doivent être Bonjour même région que vos données.  

## <a name="next-steps"></a>Étapes suivantes
* [Présentation d’Azure Data Lake Store](data-lake-store-overview.md)
