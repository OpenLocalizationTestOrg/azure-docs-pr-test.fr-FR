---
title: aaaAdd tooan de surveillance et de diagnostics machine virtuelle Azure | Documents Microsoft
description: "Utilisez un toocreate de modèle Azure resource manager une machine virtuelle Windows avec l’extension Azure diagnostics."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Utiliser la surveillance et les diagnostics avec une machine virtuelle Windows et des modèles Azure Resource Manager
Hello Extension des Diagnostics Azure fournit de surveillance de hello et fonctionnalités des diagnostics sur un Windows basée sur machine virtuelle Azure. Vous pouvez activer ces fonctionnalités sur l’ordinateur virtuel de hello en incluant l’extension de hello en tant que partie du modèle de gestionnaire de Ressources azure hello. Pour plus d’informations sur l’ajout d’une extension dans un modèle de machine virtuelle, consultez [Création de modèles Azure Resource Manager avec des extensions de machine virtuelle](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) . Cet article décrit comment vous pouvez ajouter le modèle d’ordinateur virtuel windows hello Azure Diagnostics extension tooa.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Ajouter une définition de ressource de hello Azure Diagnostics extension toohello machine virtuelle
extension de diagnostics tooenable hello sur une Machine virtuelle Windows vous avez besoin d’une extension de hello tooadd comme une ressource de machine virtuelle dans hello modèle de gestionnaire de ressources.

Pour un gestionnaire de ressources simple basée sur Machine virtuelle ajouter hello extension configuration toohello *ressources* tableau hello Machine virtuelle : 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Une autre convention commune est ajouter la configuration de l’extension hello au nœud de ressources hello racine du modèle hello au lieu de définir sous le nœud de ressources de l’ordinateur virtuel hello. Avec cette approche vous avez tooexplicitly spécifier une relation hiérarchique entre les extension hello et ordinateur virtuel de hello avec hello *nom* et *type* valeurs. Par exemple : 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

Hello extension est toujours associée hello virtual machine, vous pouvez directement définir directement sous le nœud de la ressource d’ordinateur virtuel de hello ou définir au niveau de base hello et utiliser hello tooassociate d’une convention d’affectation de noms hiérarchique avec hello virtuel ordinateur.

Pour les extensions de machines virtuelles identiques hello configuration est spécifiée dans hello *extensionProfile* propriété Hello *VirtualMachineProfile*.

Hello *publisher* propriété avec la valeur hello **Microsoft.Azure.Diagnostics** et hello *type* propriété avec la valeur hello **IaaSDiagnostics** identifier extension des Diagnostics Windows Azure hello.

Hello valeur Hello *nom* propriété peut avoir l’extension de toohello toorefer utilisés dans le groupe de ressources hello. Paramètre spécifiquement trop**Microsoft.Insights.VMDiagnosticsSettings** Active toobe facilement identifié par hello garantissant portail Azure hello analyse graphiques qui s’affichent correctement dans hello portail Azure.

Hello *typeHandlerVersion* spécifie la version de hello d’extension de hello vous aimeriez toouse. Paramètre *autoUpgradeMinorVersion* version mineure trop**true** permet de s’assurer que vous obtenez hello dernière version mineure du extension hello qui est disponible. Il est fortement recommandé de toujours définir *autoUpgradeMinorVersion* tooalways être **true** afin que vous obtenez toujours toouse hello plus récente disponible extension diagnostics avec toutes les nouvelles fonctionnalités de hello et le bogue correctifs. 

Hello *paramètres* élément contient des propriétés de configurations pour l’extension hello qui peut être défini et lire à partir de l’extension hello (parfois désignée tooas publique configuration). Hello *xmlcfg* propriété contient la configuration basée sur xml pour les journaux de diagnostics hello, etc. qui seront collectées par l’agent de diagnostics hello les compteurs de performance. Consultez [schéma de Configuration de Diagnostics](https://msdn.microsoft.com/library/azure/dn782207.aspx) pour plus d’informations sur le schéma xml de hello lui-même. Une pratique courante consiste toostore hello réelle de configuration xml comme base64 de variable dans le modèle de gestionnaire de ressources Azure hello et puis concaténer les encoder valeur hello tooset *xmlcfg*. Consultez la section de hello sur [les variables de configuration de diagnostics](#diagnostics-configuration-variables) toounderstand plus en détail comment toostore hello xml dans des variables. Hello *storageAccount* propriété spécifie le nom hello hello stockage compte toowhich des données de diagnostic est transférée. 

Hello propriétés dans *protectedSettings* (parfois désignée tooas privé configuration) peut être définie, mais ne peut pas être lu à la suite en cours de définition. Hello nature en écriture seule de *protectedSettings* permet de stocker des secrets, comme clé de compte de stockage hello où les données de diagnostic hello seront écrit.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Spécification du compte de stockage de diagnostics en tant que paramètres
Hello diagnostics extension json extrait de code ci-dessus suppose que deux paramètres *existingdiagnosticsStorageAccountName* et *existingdiagnosticsStorageResourceGroup* diagnostics de hello toospecify compte de stockage où les données de diagnostic seront stockées. Spécification de compte de stockage de diagnostics hello comme un paramètre rend compte de stockage de diagnostics hello toochange facile entre les différents environnements par exemple, vous souhaiterez peut-être toouse un compte de stockage différents tests de diagnostic pour le test et une autre pour votre déploiement de production.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Il s’agit des meilleures pratiques toospecify un compte de stockage de diagnostics dans un autre groupe de ressources que le groupe de ressources hello pour la machine virtuelle de hello. Un groupe de ressources peut être considéré comme une unité de déploiement avec sa propre durée de vie de toobe, un ordinateur virtuel peut être déployé et redéployé lors des nouvelles mises à jour des configurations il tooit, mais vous souhaiterez peut-être toocontinue le stockage des données de diagnostic hello Bonjour même compte de stockage dans les déploiements d’ordinateurs virtuels. Avoir un compte de stockage hello dans un compte hello stockage de ressources différent Active tooaccept de données à partir de différents déploiements de machine virtuelle rend facile tootroubleshoot problèmes sur hello différentes versions.

> [!NOTE]
> Si vous créez un modèle d’ordinateur virtuel windows à partir de Visual Studio compte de stockage par défaut hello peut être défini toouse hello même compte de stockage où la machine virtuelle de hello disque dur virtuel est téléchargé. Il s’agit de la configuration initiale toosimplify Hello machine virtuelle. Vous devez refactoriser hello modèle toouse un autre compte de stockage qui peut être passé comme un paramètre. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Variables de configuration des diagnostics
Hello diagnostics extension json extrait de code ci-dessus définit un *accountid* toosimplify variable mise en route de la clé de compte de stockage hello pour le stockage de diagnostics hello :   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Hello *xmlcfg* propriété pour l’extension de diagnostics hello est définie à l’aide de plusieurs variables qui sont concaténées. les valeurs Hello de ces variables sont en xml donc toobe échappé correctement lors de la définition des variables de json hello.

la section suivante de Hello décrit xml de configuration de diagnostics hello qui collecte des compteurs de performance au niveau système standard, ainsi que des journaux des événements windows et les journaux d’infrastructure de diagnostics. Il a été échappé et mise en forme correctement afin que hello configuration peut directement être collée dans la section de variables hello de votre modèle. Consultez hello [schéma de Configuration de Diagnostics](https://msdn.microsoft.com/library/azure/dn782207.aspx) pour obtenir un exemple plu lisible hello configuration XML.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

nœud de xml de définition de métriques Hello Bonjour au-dessus de configuration est un élément de configuration importantes car elle définit la façon dont les compteurs de performance hello définis précédemment dans xml hello dans *PerformanceCounter* nœud est agrégé et stockées. 

> [!IMPORTANT]
> Ces mesures lecteur hello alertes Bonjour portail Azure et les graphiques d’analyse.  Hello **métriques** nœud avec hello *resourceID* et **MetricAggregation** doit être inclus dans la configuration des diagnostics hello pour votre machine virtuelle si vous souhaitez toosee hello machine virtuelle données d’analyse Bonjour portail Azure. 
> 
> 

Hello Voici un exemple de code xml de hello pour les définitions de métriques : 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Hello *resourceID* attribut identifie de façon unique machine virtuelle de hello dans votre abonnement. Assurez-vous que subscription() de hello toouse et resourceGroup() fonctions afin que hello modèle met automatiquement à jour ces valeurs basées sur le groupe d’abonnement et de ressources hello que vous effectuez le déploiement.

Si vous créez plusieurs Machines virtuelles dans une boucle, vous devez toopopulate hello *resourceID* valeur avec un toocorrectly de fonction copyIndex() différencier chaque machine virtuelle individuelle. Hello *xmlCfg* valeur peut être mis à jour toosupport cela comme suit :  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Hello valeur MetricAggregation *PT1H* et *PT1M* constitue une agrégation sur une minute et une agrégation sur une heure.

## <a name="wadmetrics-tables-in-storage"></a>Tables WADMetrics dans le stockage
configuration des métriques Hello ci-dessus génère les tables dans votre compte de stockage de diagnostics avec hello suit les conventions d’affectation de noms :

* **WADMetrics** : préfixe standard pour toutes les tables WADMetrics
* **PT1H** ou **PT1M** : signifie que la table hello contient des données agrégées en 1 heure ou 1 minute
* **P10D** : désigne la table de hello contiendra les données de 10 jours à partir de la table de hello démarrage de collecte de données
* **V2S** : constante de chaîne
* **AAAAMMJJ** : date hello à quels hello table démarré la collecte de données

Exemple : *WADMetricsPT1HP10DV2S20151108* contient les données de mesures agrégées pendant une heure et pour une période de 10 jours commençant le 11 novembre 2015    

Chaque table WADMetrics contiendra hello suivant des colonnes :

* **PartitionKey**: hello partitionkey est créée en fonction de hello *resourceID* valeur toouniquely identifier la ressource de machine virtuelle hello. Par exemple : 002Fsubscriptions:<subscriptionID>:002FresourceGroups:002F<ResourceGroupName>:002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : format de hello suit <Descending time tick>:<Performance Counter Name>. Hello décroissant réapprovisionnement graduation est graduations temps max moins de temps hello du début de hello de période de globalisation hello. Par exemple, Si la période d’échantillonnage hello démarré novembre-10-2015 et calcul de UTC puis hello 00:00Hrs serait : DateTime.MaxValue.Ticks - (DateTime(2015,11,10,0,0,0,DateTimeKind.Utc) de nouveau. Graduations). Pour la recherche de clé de ligne hello compteur de performance de hello mémoire octets disponibles telles que : 2519551871999999999__:005CMemory:005CAvailable:0020 octets
* **CounterName** : nom hello hello du compteur de performance. Cela correspond à hello *counterSpecifier* défini dans la configuration xml de hello.
* **Maximale** : hello valeur maximale du compteur de performances hello période hello d’agrégation.
* **Minimum** : hello valeur minimale hello du compteur de performance sur la période de globalisation hello.
* **Total** : somme de hello de toutes les valeurs de compteur de performance hello indiquée sur la période de globalisation hello.
* **Nombre** : nombre total de hello de valeurs signalées pour le compteur de performances hello.
* **Moyenne** : hello valeur moyenne (total/nombre) hello du compteur de performance sur la période de globalisation hello.

## <a name="next-steps"></a>Étapes suivantes
* Pour un exemple de modèle complet d’une machine virtuelle Windows avec l’extension Diagnostics, consultez [201-vm-monitoring-diagnostics-extension](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Déployer le modèle de gestionnaire de ressources hello avec [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [ligne de commande Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* En savoir plus sur la [création de modèles Azure Resource Manager](../../resource-group-authoring-templates.md)

