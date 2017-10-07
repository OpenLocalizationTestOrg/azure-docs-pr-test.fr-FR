---
title: aaaUpgrade un cluster Azure Service Fabric | Documents Microsoft
description: "Mise à niveau du code de Service Fabric hello et/ou de configuration qui s’exécute à un cluster Service Fabric, notamment en définissant le mode de mise à jour de cluster, la mise à niveau des certificats, ajout de ports d’application, faisant de correctifs de système d’exploitation, et ainsi de suite. Ce que vous attendez lorsque des mises à niveau hello sont effectuées ?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Mettre à niveau un cluster Azure Service Fabric
> [!div class="op_single_selector"]
> * [Cluster Azure](service-fabric-cluster-upgrade.md)
> * [Cluster autonome](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Pour n’importe quel système moderne, la conception des mises à jour est tooachieving clé de succès à long terme de votre produit. Un cluster Azure Service Fabric est une ressource que vous possédez mais qui est en partie gérée par Microsoft. Cet article décrit ce qui est géré automatiquement et ce que vous pouvez configurer vous-même.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Contrôle de version de l’ensemble fibre optique hello qui s’exécute sur votre Cluster
Vous pouvez définir votre structure automatique de cluster tooreceive mises à niveau comme elles sont publiées par Microsoft, ou vous pouvez sélectionner une version prise en charge l’infrastructure souhaité dans votre toobe de cluster.

Pour ce faire, la configuration de cluster « upgrademode doit être » paramètre hello sur le portail de hello ou à l’aide du Gestionnaire de ressources au moment de la création de hello ou version ultérieure sur un cluster dynamique 

> [!NOTE]
> Assurez-vous que tookeep votre cluster exécutant une version prise en charge l’infrastructure toujours. Et, lorsque nous annoncer version hello d’une nouvelle version de l’infrastructure de service, version précédente de hello est marquée pour la fin de la prise en charge un minimum de 60 jours à partir de cette date. Hello nouvelles versions de hello sont annoncées [sur le blog de l’équipe service fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/). mise en production Hello est toochoose disponible. 
> 
> 

14 jours expiration toohello préalable de mise en production hello votre cluster est en cours d’exécution, un événement de contrôle d’intégrité est généré qui place de votre cluster dans un état d’avertissement. cluster de Hello reste dans un état d’avertissement jusqu'à ce que vous mettez à niveau la version de l’infrastructure de prise en charge tooa.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Paramètre de mode de mise à niveau hello via le portail
Lorsque vous créez un cluster de hello, vous pouvez définir hello cluster tooautomatic ou manuelle.

![Create_Manualmode][Create_Manualmode]

Vous pouvez définir hello cluster tooautomatic ou manuelle sur un cluster dynamique, à l’aide de hello gérer l’expérience. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>La mise à niveau tooa une nouvelle version sur un cluster qui est défini en mode de tooManual via le portail.
tooupgrade tooa nouvelle version, vous devez toodo est sélectionnez la version hello disponible à partir de la liste déroulante de hello et enregistrez. mise à niveau de Fabric Hello obtient lancé automatiquement. Hello stratégies d’intégrité de cluster (il s’agit d’une combinaison de l’intégrité de nœud et de contrôle d’intégrité hello tous hello applications s’exécutant dans un cluster de hello) sont respectés mise à niveau de tooduring hello.

Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée. Défiler ce document de tooread plus sur la façon de tooset ces stratégies d’intégrité personnalisés. 

Une fois que vous avez résolution des problèmes de hello qui a entraîné la restauration hello, vous devez mise à niveau de hello tooinitiate à nouveau, en suivant hello même procédure qu’avant.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Paramètre de mode de mise à niveau hello via un modèle de gestionnaire de ressources
Ajouter hello de définition de ressource « upgrademode doit être » configuration toohello Microsoft.ServiceFabric/clusters et ensemble hello « clusterCodeVersion » tooone Hello pris en charge les versions de l’infrastructure, comme indiqué ci-dessous et ensuite déployer le modèle de hello. les valeurs valides de Hello pour « upgrademode doit être » sont « Manuel » ou « Automatique »

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>La mise à niveau tooa une nouvelle version sur un cluster qui est défini en mode de tooManual via un modèle de gestionnaire de ressources.
Lorsque le cluster de hello est en mode manuel, tooupgrade tooa nouvelle version, modifiez la version prise en charge de tooa hello « clusterCodeVersion » et le déployer. déploiement de modèle de hello Hello plaisir de mise à niveau de Fabric hello obtient lancé automatiquement. Hello stratégies d’intégrité de cluster (il s’agit d’une combinaison de l’intégrité de nœud et de contrôle d’intégrité hello tous hello applications s’exécutant dans un cluster de hello) sont respectés mise à niveau de tooduring hello.

Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée. Défiler ce document de tooread plus sur la façon de tooset ces stratégies d’intégrité personnalisés. 

Une fois que vous avez résolution des problèmes de hello qui a entraîné la restauration hello, vous devez mise à niveau de hello tooinitiate à nouveau, en suivant hello même procédure qu’avant.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Obtenir la liste de toutes les versions disponibles pour tous les environnements dans le cas d’un abonnement donné
Exécutez hello la commande suivante, et vous devez obtenir un toothis similaire de sortie.

Le paramètre « supportExpiryUtc » vous indique lorsqu’une version donnée arrive à expiration ou a expiré. Hello version la plus récente n’a pas une date valide - elle a la valeur « 9999-12-31T23:59:59.9999999 », ce qui signifie simplement que date d’expiration hello n’est pas encore définie.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Comportement de mise à niveau de fabric lorsque le Mode de mise à niveau de cluster de hello est automatique
Microsoft gère la configuration qui s’exécute dans un cluster Azure et le code de l’ensemble fibre optique hello. Nous effectuons des logiciels de toohello automatique de mises à niveau analysées en fonction des besoins. Ces mises à niveau peuvent concerner le code, la configuration ou les deux. toomake sûr que votre application ne subit aucun impact ou un impact minime en raison de mises à niveau toothese, nous effectuer des mises à niveau de la hello Bonjour suivant phases :

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>Phase 1 : Une mise à niveau est effectuée à l'aide de toutes les stratégies d'intégrité du cluster
Pendant cette phase, les mises à niveau hello passer un seul domaine de mise à niveau à la fois, et les applications de hello en cours d’exécution dans un cluster de hello continuent toorun sans interruption de service. Hello stratégies d’intégrité de cluster (il s’agit d’une combinaison de l’intégrité de nœud et de contrôle d’intégrité hello tous hello applications s’exécutant dans un cluster de hello) sont respectés mise à niveau de tooduring hello.

Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée. Puis un message électronique est envoyé propriétaire toohello d’abonnement de hello. messagerie de Hello contient hello informations suivantes :

* Notification que nous avons dû tooroll dans une mise à niveau de cluster.
* Des suggestions d'actions correctives, le cas échéant.
* nombre de Hello de jours (n) jusqu'à ce que nous exécutons la Phase 2.

Nous essayons hello tooexecute que même mettre à niveau plusieurs fois au cas où les mises à niveau a échoué pour des raisons de l’infrastructure. Hello n jours à partir de la messagerie de hello hello date a été envoyée, nous progressons tooPhase 2.

Si les stratégies de contrôle d’intégrité de cluster hello sont remplies, mise à niveau hello est considérée comme réussie et marquée comme terminée. Cela peut se produire pendant la mise à niveau initiale de hello ou des rediffusions de mise à niveau hello dans cette phase. Aucun message électronique de confirmation d'une exécution réussie n'est envoyé. Il s’agit de tooavoid envoi vous trop de courriels--reçoit un message électronique devez être considérée comme un toonormal d’exception. Nous pensons que la plupart des toosucceed de mises à niveau de cluster hello sans affecter la disponibilité de votre application.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>Phase 2 : Une mise à niveau est effectuée à l'aide des stratégies d'intégrité par défaut uniquement
stratégies de contrôle d’intégrité Hello dans cette phase sont définies de telle sorte que nombre de hello d’applications qui ont été intègre au début de hello de mise à niveau hello reste hello même pour hello durée du processus de mise à niveau hello. Dans la Phase 1, mises à niveau de la Phase 2 de hello passer un seul domaine de mise à niveau à la fois, et les applications de hello en cours d’exécution dans un cluster de hello continuent toorun sans interruption de service. stratégies d’intégrité de cluster Hello (une combinaison de l’intégrité de nœud et de contrôle d’intégrité hello que tous hello applications s’exécutant dans un cluster de hello) sont durée de hello adhésive toofor de mise à niveau hello.

Si les stratégies d’intégrité de cluster hello en vigueur ne sont pas remplies, mise à niveau hello est restaurée. Puis un message électronique est envoyé propriétaire toohello d’abonnement de hello. messagerie de Hello contient hello informations suivantes :

* Notification que nous avons dû tooroll dans une mise à niveau de cluster.
* Des suggestions d'actions correctives, le cas échéant.
* nombre de Hello de jours (n) jusqu'à ce que nous exécutons la Phase 3.

Nous essayons hello tooexecute que même mettre à niveau plusieurs fois au cas où les mises à niveau a échoué pour des raisons de l’infrastructure. Un message électronique de rappel est envoyé deux jours avant que le délai de n jours ne soit écoulé. Hello n jours à partir de la messagerie de hello hello date a été envoyée, nous progressons tooPhase 3. des messages électroniques Hello que nous envoyer dans la Phase 2 doivent être prises au sérieux et actions de réparation doivent être effectuées.

Si les stratégies de contrôle d’intégrité de cluster hello sont remplies, mise à niveau hello est considérée comme réussie et marquée comme terminée. Cela peut se produire pendant la mise à niveau initiale de hello ou des rediffusions de mise à niveau hello dans cette phase. Aucun message électronique de confirmation d'une exécution réussie n'est envoyé.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>Phase 3 : Une mise à niveau est effectuée à l'aide de stratégies d'intégrité agressives
Ces stratégies d’intégrité de cette phase sont adressent à la fin de la mise à niveau hello plutôt que d’intégrité de hello des applications de hello. Un nombre très faible de mises à niveau du cluster se termine par cette phase. Si votre cluster obtient toothis phase, il est probable que votre application devient non intègre et/ou de perdre la disponibilité.

Toohello similaire autres deux phases, les mises à niveau de la Phase 3 passer un seul domaine de mise à niveau à la fois.

Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée. Nous essayons hello tooexecute que même mettre à niveau plusieurs fois au cas où les mises à niveau a échoué pour des raisons de l’infrastructure. Après cela, le cluster de hello est épinglé, afin qu’il ne recevra plus les mises à niveau et/ou de prise en charge.

Propriétaire de l’abonnement toohello, ainsi que les actions correctives hello est envoyé à un message avec ces informations. N’importe quel tooget clusters ne devrait pas dans un état où la Phase 3 a échoué.

Si les stratégies de contrôle d’intégrité de cluster hello sont remplies, mise à niveau hello est considérée comme réussie et marquée comme terminée. Cela peut se produire pendant la mise à niveau initiale de hello ou des rediffusions de mise à niveau hello dans cette phase. Aucun message électronique de confirmation d'une exécution réussie n'est envoyé.

## <a name="cluster-configurations-that-you-control"></a>Configurations de cluster que vous contrôlez
En outre cluster hello de toohello capacité tooset mise à niveau en mode, voici les configurations hello que vous pouvez modifier sur un cluster dynamique.

### <a name="certificates"></a>Certificats
Vous pouvez ajouter de nouvelles ou supprimer des certificats pour le cluster de hello et du client via le portail de hello facilement. Consultez trop[ce document pour obtenir des instructions détaillées](service-fabric-cluster-security-update-certs-azure.md)

![Capture d’écran qui affiche les empreintes numériques de certificat Bonjour portail Azure.][CertificateUpgrade]

### <a name="application-ports"></a>Ports d'application
Vous pouvez modifier les ports d’application en modifiant les propriétés de ressource d’équilibrage de charge hello qui sont associées au type de nœud hello. Vous pouvez utiliser le portail de hello, ou vous pouvez utiliser le Gestionnaire de ressources PowerShell directement.

tooopen un nouveau port sur toutes les machines virtuelles dans un type de nœud, hello suivant :

1. Ajouter un nouvel équilibrage de charge approprié toohello sonde.
   
    Si vous avez déployé votre cluster à l’aide du portail de hello, équilibreurs de charge hello sont nommées « LB-nom du groupe de ressources hello-NodeTypename », une pour chaque type de nœud. Étant donné que les noms d’équilibrage de charge de hello sont uniques uniquement dans un groupe de ressources, il est préférable du faire si vous recherchez les sous un groupe de ressources spécifique.
   
    ![Capture d’écran montre l’ajout d’une sonde tooa charger équilibrage dans le portail de hello.][AddingProbes]
2. Ajouter un équilibrage de charge nouvelle règle toohello.
   
    Ajouter un nouveau toohello de règle même équilibreur de charge à l’aide de sonde hello que vous avez créé à l’étape précédente de hello.
   
    ![Ajout d’un équilibreur de charge nouvelle règle tooa dans le portail de hello.][AddingLBRules]

### <a name="placement-properties"></a>Propriétés de positionnement
Pour chacun des types de nœuds hello, vous pouvez ajouter des propriétés de sélection élective personnalisée que vous souhaitez toouse dans vos applications. NodeType est une propriété par défaut que vous pouvez utiliser sans l'ajouter explicitement.

> [!NOTE]
> Pour plus d’informations sur l’utilisation de hello de contraintes de placement, propriétés de nœud, et comment toodefine, référence toohello section « Contraintes de Placement et propriétés du nœud » Bonjour Document du Gestionnaire de ressources du Cluster Service Fabric sur [décrivant de votre Cluster ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Métriques de capacité
Pour chacun des types de nœuds hello, vous pouvez ajouter des métriques de capacité personnalisé que vous souhaitez toouse dans votre charge de tooreport d’applications. Pour plus d’informations sur l’utilisation hello de métriques tooreport charge, consultez la toohello Documents du Gestionnaire de ressources du Cluster Service Fabric [décrivant de votre Cluster](service-fabric-cluster-resource-manager-cluster-description.md) et [métriques et charge](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Paramètres de mise à niveau de la structure : stratégies de contrôle d’intégrité
Vous pouvez spécifier des stratégies de contrôle d’intégrité personnalisées pour la mise à niveau de la structure. Si vous avez défini votre tooAutomatic cluster mises à niveau de l’ensemble fibre optique, ces stratégies obtiennent appliqué toohello Phase 1 de mises à niveau de l’ensemble fibre optique automatique hello.
Si vous avez défini votre cluster de l’ensemble fibre optique manuelle de mises à niveau, puis ces stratégies soient appliqués à chaque fois que vous sélectionnez une nouvelle version de déclenchement tookick de système de hello désactiver la mise à niveau de fabric hello dans votre cluster. Si vous ne substituez pas les stratégies de hello, valeurs par défaut de hello sont utilisées.

Vous pouvez spécifier des stratégies de contrôle d’intégrité personnalisé hello ou passez en revue les paramètres actuels de hello sous le panneau de « mise à niveau de fabric » hello, en sélectionnant la mise à niveau des paramètres avancé de hello. Passez en revue hello suivant image comment. 

![Gérer les stratégies de contrôle d’intégrité personnalisées][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Personnaliser les paramètres de la structure pour votre cluster
Consultez trop[les paramètres de l’infrastructure de cluster l’infrastructure de service](service-fabric-cluster-fabric-settings.md) sur les éléments et comment vous pouvez les personnaliser.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Correctifs de système d’exploitation sur hello machines virtuelles qui composent hello cluster
Consultez trop[correctif Orchestration Application](service-fabric-patch-orchestration-application.md) qui peuvent être déployés sur vos correctifs tooinstall de cluster à partir de Windows Update de façon orchestrée, en conservant les services hello disponibles tout temps hello. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Mises à niveau du système d’exploitation sur hello machines virtuelles qui composent hello cluster
Si vous devez mettre à niveau d’image de système d’exploitation hello sur des machines virtuelles de hello du cluster de hello, vous devez utiliser une machine virtuelle à la fois. Vous êtes responsable de cette mise à niveau, rien n’est actuellement automatisé à ce sujet.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment toocustomize certaines hello [les paramètres de l’infrastructure de cluster l’infrastructure de service](service-fabric-cluster-fabric-settings.md)
* Découvrez comment trop[l’échelle de votre cluster et l’extraction](service-fabric-cluster-scale-up-down.md)
* Découvrez les [mises à niveau de l’application](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
