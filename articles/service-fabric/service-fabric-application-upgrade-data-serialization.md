---
title: "Mise à niveau d’une application : sérialisation des données | Microsoft Docs"
description: "Meilleures pratiques pour la sérialisation de données et son impact sur le déploiement des mises à niveau d'applications."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Impact de la sérialisation des données sur la mise à niveau d’une application
Dans un [application mise à niveau propagée](service-fabric-application-upgrade.md), mise à niveau hello est appliqué tooa sous-ensemble de nœuds, un seul domaine de mise à niveau à la fois. Pendant ce processus, certains domaines de mise à niveau se trouvent sur une version plus récente de hello de votre application, et certains domaines de mise à niveau sont hello ancienne version de votre application. Lors du déploiement hello, hello nouvelle version de votre application doit être en mesure de tooread hello ancienne version de vos données et hello ancienne version de votre application doit être en mesure de tooread hello nouvelle version de vos données. Si le format de données hello n’est pas mise à niveau vers l’avant et vers l’arrière compatible, hello peuvent échouer ou pire, de données peut être perdue ou corrompue. Cet article explique ce qui constitue le format de données et détaille les méthodes recommandées pour que les données offrent une compatibilité ascendante et descendante.

## <a name="what-makes-up-your-data-format"></a>Qu'est-ce qui constitue le format de données ?
Dans Azure Service Fabric, les données hello sont persistant et répliquées provient de vos classes c#. Pour les applications qui utilisent [Collections fiable](service-fabric-reliable-services-reliable-collections.md), que les données sont des objets de hello dans les files d’attente et les dictionnaires fiable hello. Pour les applications qui utilisent [Reliable Actors](service-fabric-reliable-actors-introduction.md), c'est-à-dire les hello sauvegarde l’état d’acteur de hello. Ces classes c# doivent être sérialisables toobe persistant et répliqué. Par conséquent, format de données hello est défini par les champs de hello et les propriétés qui sont sérialisées, ainsi que la manière dont elles sont sérialisées. Par exemple, dans un `IReliableDictionary<int, MyClass>` les données de salutation sont sérialisée `int` et sérialisée `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Modifications du code résultant dans une modification du format de données
Format de données hello est déterminée par les classes c#, classes toohello de modifications peuvent entraîner une modification de format de données. Soyez prudent tooensure une mise à niveau propagée peut gérer les données de salutation du format. Exemples d'opérations pouvant entraîner une modification du format de données :

* Ajout ou suppression de champs ou de propriétés
* Modification du nom d'un champ ou d'une propriété
* Modification des types de champs ou propriétés hello
* Modification du nom de classe hello ou espace de noms

### <a name="data-contract-as-hello-default-serializer"></a>Contrat de données comme hello sérialiseur par défaut
sérialiseur de Hello est généralement responsable de la lecture des données de hello, qui la désérialise dans la version actuelle de hello, même si les données de salutation sont dans une version antérieure ou *plus récente* version. Hello sérialiseur par défaut est hello [sérialiseur de contrat de données](https://msdn.microsoft.com/library/ms733127.aspx), qui a des règles de versioning bien défini. Fiable les Collections permettent toobe de sérialiseur hello remplacée, mais Reliable Actors actuellement pas. sérialiseur de données Hello joue un rôle important dans l’activation des mises à niveau propagées. sérialiseur de contrat de données Hello est sérialiseur hello que nous recommandons pour les applications de Service Fabric.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Comment le format de données hello affecte une mise à niveau propagée
Pendant une mise à niveau propagée, il existe deux principaux scénarios où le sérialiseur de hello peut rencontrer une ancienne ou *plus récente* version de vos données :

1. Une fois un nœud est mis à niveau et démarre sauvegarder, sérialiseur de nouveau hello chargera les données de hello qui a été toodisk persistant par une ancienne version de hello.
2. Au cours de la mise à niveau propagée de hello, cluster de hello contient un mélange de versions anciennes et nouvelles de hello de votre code. Étant donné que les réplicas peuvent être placés dans différents domaines de mise à niveau et réplicas envoient des données tooeach autres, hello nouveau ou ancien version de vos données peut-être être rencontrée par version de nouveau ou ancien hello de votre sérialiseur.

> [!NOTE]
> Hello « nouvelle version » et « version ancienne » ici font référence version toohello de votre code qui est en cours d’exécution. Hello « nouveau sérialiseur » fait référence à code de sérialiseur toohello qui s’exécute dans la nouvelle version de hello de votre application. Hello « de nouvelles données » fait référence classe c# toohello sérialisé de hello nouvelle version de votre application.
> 
> 

Hello deux versions du code et de format de données doit être vers l’avant et vers l’arrière compatible. Si elles ne sont pas compatibles, hello mise à niveau propagée peut échouer ou les données peuvent être perdues. Hello mise à niveau propagée peut échouer, car le code de hello ou un sérialiseur peut-être lever des exceptions ou une erreur quand il rencontre hello autre version. Données peuvent être perdues si, par exemple, une nouvelle propriété a été ajoutée mais sérialiseur ancien de hello ignore pendant la désérialisation.

Contrat de données est hello solution afin de garantir que vos données sont compatibles recommandée. Il possède des règles de gestion de version bien définies pour l'ajout, la suppression et la modification de champs. Il est également prise en charge de traitement avec des champs inconnus, se connecter à un processus de sérialisation et désérialisation hello et de gestion d’héritage de classe. Pour plus d'informations, consultez la page [Utilisation du contrat de données](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Étapes suivantes
[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.

[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.

Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).

Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).

Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application ](service-fabric-application-upgrade-troubleshooting.md).

