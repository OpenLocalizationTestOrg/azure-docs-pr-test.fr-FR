---
title: "rubriques relatives à la mise à niveau des applications d’aaaAdvanced | Documents Microsoft"
description: "Cet article décrit certaines rubriques avancées relatives tooupgrading une application de Service Fabric."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Mise à niveau d’une application Service Fabric : rubriques avancées
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Ajout ou suppression de services pendant la mise à niveau d'une application
Si un nouveau service est ajouté application tooan qui est déjà déployée et publiée une mise à niveau, hello nouveau service est ajouté toohello déployé application.  Une mise à niveau n’affecte pas un des services hello faisant déjà partie d’une application hello. Toutefois, une instance de service hello qui a été ajouté doit être démarrée pour toobe service hello nouvelle active (à l’aide de hello `New-ServiceFabricService` applet de commande).

Des services peuvent également être supprimés d’une application dans le cadre d’une mise à niveau. Toutefois, toutes les instances en cours du service de hello à supprimer doivent être arrêtés avant de poursuivre la mise à niveau hello (à l’aide de hello `Remove-ServiceFabricService` applet de commande).

## <a name="manual-upgrade-mode"></a>Mode de mise à niveau manuelle
> [!NOTE]
> mode manuel de Hello non contrôlée doit être considéré uniquement pour une mise à niveau a échoué ou suspendue. le mode surveillé Hello est hello recommandé en mode de mise à niveau pour les applications de Service Fabric.
>
>

Azure Service Fabric fournit plusieurs modes de mise à niveau des clusters de développement et de production toosupport. Les options de déploiement choisies peuvent être différentes pour différents environnements.

mise à niveau application propagée Hello analysé est hello toouse de mise à niveau plus classique dans l’environnement de production hello. Lors de la mise à niveau de hello stratégie est spécifiée, Service Fabric garantit qu’application hello est saine avant de la mise à niveau hello se poursuit.

 administrateur de l’application Hello peut utiliser manuel hello propagée application en mode de mise à niveau toohave contrôle total sur la progression de mise à niveau hello via hello différents domaines de mise à niveau. Ce mode est utile lorsqu’une stratégie d’évaluation d’intégrité personnalisé ou complexe est nécessaire, ou une mise à niveau non conventionnelle se produit (par exemple, application hello est déjà une perte de données).

Enfin, hello automatisée mise à niveau propagée d’application est utile pour le développement ou de test des environnements tooprovide une itération rapide cycle pendant le développement du service.

## <a name="change-toomanual-upgrade-mode"></a>Changement du mode de mise à niveau toomanual
**Manuel**--arrêt hello application mise à niveau à Bonjour Bonjour actuel UD et modification de niveau tooUnmonitored de mode manuel. administrateur Hello doit toomanually appel **MoveNextApplicationUpgradeDomainAsync** tooproceed avec hello mise à niveau ou d’un déclencheur d’une restauration en lançant une nouvelle mise à niveau. Une fois la mise à niveau hello entrée en mode manuel de hello, elle reste en mode manuel de hello jusqu'à ce qu’une nouvelle mise à niveau est déclenché. Hello **GetApplicationUpgradeProgressAsync** commande retourne l’ensemble fibre optique\_APPLICATION\_mise à niveau\_état\_propagées\_par progression\_en attente.

## <a name="upgrade-with-a-diff-package"></a>Effectuer une mise à niveau avec un package différentiel
Une application Service Fabric peut être mise à niveau via une mise en service avec un package d'application autonome et complet. Une application peut également être mis à niveau à l’aide d’un package de comparaison qui contient les fichiers d’application hello mis à jour uniquement, hello mis à jour le manifeste d’application et les fichiers manifeste de service hello.

Un package d’application complet contient tous les hello fichiers nécessaires toostart et exécuter une application de Service Fabric. Un package diff contient uniquement les fichiers de hello changé entre la dernière disposition de hello et mise à niveau actuel de hello, plus les fichiers manifestes de manifeste de l’application complète hello et service de hello. Toute référence dans le manifeste d’application hello ou service qui ne figure pas dans la disposition de build hello est recherché dans le magasin d’images hello.

Les packages d’application complet sont requis pour hello première installation d’un cluster de toohello d’application. Les mises à jour suivantes peuvent être un package d'application complet ou un package différentiel.

Situations qui se prêtent à l'utilisation d'un package différentiel :

* Un package différentiel est préférable quand vous disposez d’un package d’application volumineux qui référence plusieurs fichiers manifeste de service et/ou plusieurs packages de code, de configuration ou de données.
* Un package de comparaison est préférable lorsque vous disposez d’un système de déploiement qui génère la disposition de build hello directement à partir de votre processus de génération d’application. Dans ce cas, même si le code de hello n’a pas changé, assemblys nouvellement générés obtenir une somme de contrôle différents. À l’aide d’un package d’application complet nécessiterait vous tooupdate hello version sur tous les packages de code. À l’aide d’un package de comparaison, vous fournissez uniquement les fichiers hello modifiés et les fichiers de manifeste de hello dont la version de hello a changé.

Lorsqu’une application est mise à niveau à l’aide de Visual Studio, il se peut que hello diff package est publié automatiquement. toocreate un package diff hello manuellement, le manifeste d’application et hello manifestes doivent être mis à jour, mais uniquement les packages hello modifié doivent figurer dans le package d’application finale hello.

Par exemple, commençons par hello suite de l’application (numéros de version fournies pour faciliter la compréhension) :

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Maintenant, supposons que vous souhaitiez tooupdate uniquement hello package de code de service1 à l’aide d’un package de comparaison à l’aide de PowerShell. À présent, votre application mise à jour a hello suivant la structure de dossiers :

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Dans ce cas, vous mettez à jour too2.0.0 de manifeste application hello et manifeste du service de mise à jour du package de code hello service1 tooreflect hello. dossier Hello pour votre package d’application a hello suivant structure :

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Étapes suivantes
[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.

[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.

Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).

Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).

Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).
