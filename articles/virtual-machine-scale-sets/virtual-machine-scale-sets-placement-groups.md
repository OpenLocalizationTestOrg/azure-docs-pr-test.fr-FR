---
title: "aaaWorking avec de grands ensembles d’échelle de Machine virtuelle Azure | Documents Microsoft"
description: "Vous devez tooknow toouse grand machine virtuelle Azure mise à l’échelle de jeux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Utilisation de grands groupes de machines virtuelles identiques
Vous pouvez désormais créer Azure [machines virtuelles identiques](/azure/virtual-machine-scale-sets/) avec une capacité de configuration too1, 000 machines virtuelles. Dans ce document, un _grand machines virtuelles identiques_ est défini comme une échelle définie capable d’évoluer toogreater à 100 machines virtuelles. Cette fonctionnalité est définie par une propriété de groupe identique (_singlePlacementGroup=False_). 

Définit certains aspects d’à grande échelle, tels que les domaines et l’équilibrage de charge comportent différemment tooa un ensemble d’échelle standard. Ce document explique les caractéristiques hello de grands jeux d’et décrit ce que vous avez besoin de tooknow toosuccessfully les utiliser dans vos applications. 

Une approche commune pour le déploiement d’infrastructure cloud à grande échelle est toocreate un ensemble de _mettre à l’échelle des unités_, par exemple, en créant plusieurs machines virtuelles, l’échelle jeux sur plusieurs réseaux virtuels et les comptes de stockage. Cette approche offre plus facile par rapport de gestion toosingle machines virtuelles, et plusieurs unités d’échelle sont utiles pour de nombreuses applications, notamment ceux qui nécessitent d’autres composants empilables comme plusieurs réseaux virtuels et les points de terminaison. Si votre application nécessite un seul cluster volumineux Toutefois, il peut être plus simple toodeploy une seule échelle configurer de too1, 000 machines virtuelles. Des exemples de scénarios incluent des déploiements de Big Data centralisés ou des grilles de calcul nécessitant la gestion simple d’un grand pool de nœuds de travail. Combiné avec un ensemble d’échelle de machine virtuelle [disques de données associés](virtual-machine-scale-sets-attached-disks.md), les jeux à grande échelle permettent toodeploy une infrastructure évolutive comprenant des milliers de cœurs et plusieurs pétaoctets de stockage, comme une seule opération.

## <a name="placement-groups"></a>Groupes de placement 
Ce qui rend une _grand_ échelle définie spécial n’est pas nombre hello d’ordinateurs virtuels, mais nombre hello de _groupes de la sélection élective_ qu’il contient. Un groupe de la sélection élective est un ensemble de disponibilité Azure tooan de construction similaire, avec ses propres domaines d’erreur et les domaines de mise à niveau. Par défaut, un groupe identique se compose d’un seul groupe de placement contenant au maximum 100 machines virtuelles. Si la valeur de propriété appelée par une échelle _singlePlacementGroup_ a la valeur too_false_, hello identiques peuvent être composées de plusieurs groupes de la sélection élective et a une plage de 0 à 1 000 machines virtuelles. Lorsque la valeur par défaut toohello de _true_, un ensemble d’échelle est composé d’un groupe de la sélection élective unique et a une plage de 0 à 100 machines virtuelles.

## <a name="checklist-for-using-large-scale-sets"></a>Liste de contrôle pour l’utilisation de grands groupes identiques
toodecide si votre application peut utiliser efficacement les jeux à grande échelle, tenez compte hello suivant les exigences :

- Les grands groupes identiques requièrent Azure Managed Disks. Les groupes identiques qui ne sont pas créés avec Managed Disks nécessitent plusieurs comptes de stockage (un toutes les 20 machines virtuelles). Les jeux à grande échelle sont toowork conçue exclusivement avec tooreduce de disques gérés des limites de votre stockage surcharge de gestion et tooavoid hello des risques de l’exécution dans un abonnement pour les comptes de stockage. Si vous n’utilisez pas de disques gérés, votre jeu de mise à l’échelle est limitée too100 VMs.
- Définit l’échelle créé à partir d’images Azure Marketplace peut évoluer too1, 000 machines virtuelles.
- Définit l’échelle créé à partir d’images personnalisées (images de machine virtuelle vous créez et chargez vous-même) capable d’évoluer actuellement too100 VMs.
- Couche 4 équilibrage de charge avec hello équilibrage de charge Azure n'est pas encore prises en charge l’échelle composé de plusieurs groupes de la sélection élective. Si vous avez besoin hello toouse équilibrage de charge Azure que l’échelle de hello que jeu est toouse configuré un groupe de la sélection élective unique, qui est par défaut hello.
- Couche 7 équilibrage de charge avec hello passerelle d’Application Azure est prise en charge pour tous les jeux de mise à l’échelle.
- Un ensemble d’échelle est défini avec un seul sous-réseau - Assurez-vous que votre sous-réseau dispose d’un espace d’adressage suffisant pour toutes les machines virtuelles de hello vous avez besoin. Par défaut, une échelle définie overprovisions (crée des machines virtuelles supplémentaires au moment du déploiement ou de la montée en puissance parallèle, ce qui vous n’êtes pas facturé pour) tooimprove déploiement fiabilité et les performances. Autoriser une adresse espace 20 % supérieur au nombre de hello d’ordinateurs virtuels que vous envisagez de tooscale à.
- Si vous envisagez de toodeploy de machines virtuelles, les limites des quotas core calcul peut-être toobe augmenté.
- Les domaines d’erreur et de mise à niveau sont cohérents uniquement au sein d’un groupe de placement. Cette architecture ne change pas hello globale d’une échelle de haute disponibilité, comme les machines virtuelles sont réparties uniformément sur un matériel physique distinct, mais c’est le cas signifie que si vous avez besoin de tooguarantee sont de deux machines virtuelles sur un matériel différent, assurez-vous qu’ils sont dans une autre erreur domaines de hello même groupe de sélection élective. ID du groupe de domaine et la sélection élective erreur sont affichés dans hello _affichage de l’instance_ d’une échelle de jeu de machine virtuelle. Vous pouvez afficher la vue d’instance hello d’un ensemble d’échelle de machine virtuelle Bonjour [Explorateur de ressources Azure](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Création d’un grand groupe identique
Lorsque vous créez une échelle définie dans hello portail Azure, vous pouvez autoriser son groupes de la sélection élective tooscale toomultiple en définissant un hello _limite tooa unique de groupe positionnement_ too_False_ option Bonjour _notions de base_ panneau. Avec cette too_False_ ensemble option, vous pouvez spécifier une _le nombre d’instances_ la valeur de configuration too1, 000.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

Vous pouvez créer une à grande échelle de la machine virtuelle à l’aide de hello [CLI d’Azure](https://github.com/Azure/azure-cli) _az mise créer_ commande. Cette commande définit les valeurs par défaut intelligents comme taille de sous-réseau en fonction de hello _-nombre d’instances_ argument :

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Notez que hello _mise créer_ commande par défaut de certaines valeurs de configuration si vous ne spécifiez pas les. options disponibles toosee hello que vous pouvez remplacer, essayez :
```bash
az vmss create --help
```

Si vous créez une grande échelle définie par la composition d’un modèle Azure Resource Manager, assurez-vous que le modèle de hello crée un jeu de mise à l’échelle basé sur des disques gérés Azure. Vous pouvez définir hello _singlePlacementGroup_ too_false_ propriété Bonjour _propriétés_ section Hello _Microsoft.Compute/virtualMAchineScaleSets_ ressource. Hello fragment JSON suivant illustre début hello d’un modèle de jeu de mise à l’échelle, y compris la capacité de machine virtuelle hello 1 000 et hello _« singlePlacementGroup » : false_ paramètre :
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Pour obtenir un exemple complet de grande échelle définir le modèle, consultez trop[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Conversion d’une échelle existante définie toospan plusieurs groupes de la sélection élective
toomake une échelle de machine virtuelle existante définie capable d’évoluer toomore à 100 machines virtuelles, vous devez toochange hello _singplePlacementGroup_ too_false_ de propriété dans l’échelle de hello définir le modèle. Vous pouvez tester la modification de cette propriété avec hello [Explorateur de ressources Azure](https://resources.azure.com/). Rechercher un ensemble existant de l’échelle, sélectionnez _modifier_ et modifiez hello _singlePlacementGroup_ propriété. Si vous ne voyez pas cette propriété, vous pouvez consulter à l’échelle de hello définie avec une version antérieure de hello Microsoft.Compute API.

>[!NOTE] 
Vous pouvez modifier une échelle définie à partir d’un emplacement unique groupe uniquement (comportement par défaut de hello) tooa prise en charge de plusieurs groupes de la sélection élective de prise en charge, mais vous ne pouvez pas convertir hello inverse. Par conséquent Assurez-vous que vous comprenez les propriétés de hello de jeux à grande échelle avant la conversion. Vérifiez en particulier, que vous n’avez pas besoin de couche 4 équilibrage de charge avec hello équilibrage de charge Azure.


