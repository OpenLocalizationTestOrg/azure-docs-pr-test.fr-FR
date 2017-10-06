---
title: aaaVirtual des tailles de machine pour les services de cloud computing de Azure | Documents Microsoft
description: "Répertorie les tailles de machine virtuelle différente hello (et ID) pour les rôles web et de travail du service cloud Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Tailles de services cloud
Cette rubrique décrit hello tailles et options disponibles pour les instances de rôle de Service Cloud (rôles web et worker). Il fournit également des toobe de considérations de déploiement lorsque vous planifiez toouse ces ressources. Chaque taille a un identifiant que vous placez dans votre [fichier de définition de service](cloud-services-model-and-package.md#csdef). Prix pour chaque taille sont disponibles sur hello [tarification des Services Cloud](https://azure.microsoft.com/pricing/details/cloud-services/) page.

> [!NOTE]
> toosee connexes des limites d’Azure, consultez [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Tailles pour les instances de rôle web et de travail
Il existe plusieurs toochoose tailles standard à partir de sur Azure. Voici des considérations quant à certaines de ces tailles :

* Machines virtuelles de série D sont conçues toorun les applications qui exigent une puissance de calcul et de performances de disque temporaire. Machines virtuelles de série D fournissent des processeurs plus rapides, un taux de mémoire-cœur plus élevé et un disque SSD (SSD) pour le disque temporaire de hello. Pour plus d’informations, consultez annonce de type hello sur hello Azure blog, [nouvelles tailles de Machine virtuelle de série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Série Dv2, un toohello les fonctionnalités de la série D d’origine, un processeur plus puissant. Hello série Dv2 processeur est d’environ 35 % plus rapide que hello série D à l’UC. Il est basé sur hello dernière génération 2,4 GHz Intel Xeon® E5-2673 v3 (Haswell), processeur et avec hello 2.0 de la technologie Intel Turbo Boost, peuvent atteindre la too3.1 GHz. Hello Dv2 série a hello les mêmes configurations de mémoire et de disque comme hello série D.
* Machines virtuelles de série G offrent hello plus de mémoire et s’exécuter sur les ordinateurs hôtes qui ont des processeurs de la famille Intel Xeon E5 V3.
* machines virtuelles de série de Hello peut être déployé sur différents types de matériel et les processeurs. taille de Hello est limitée, en fonction du matériel hello, les performances du processeur cohérent toooffer pour hello instance, quel que soit le matériel hello sur qu'il est déployé en cours d’exécution. toodetermine hello physique matériel sur lequel cette taille est déployée, requête hello virtuel du matériel à partir de hello Machine virtuelle.
* Hello taille A0 est trop sollicité sur du matériel physique de hello. Pour cette taille spécifique, les autres déploiements de client peuvent affecter les performances de hello de votre charge de travail en cours d’exécution. les performances relatives Hello sont décrite ci-dessous comme base hello attendu, variabilité approximative de sujet tooan de 15 pour cent.

Hello la taille de machine virtuelle de hello affecte la tarification de hello. taille de Hello affecte également la capacité de traitement, de mémoire et de stockage hello de machine virtuelle de hello. Les coûts de stockage sont calculés séparément en fonction des pages utilisées dans le compte de stockage hello. Pour plus d’informations, voir les pages [Tarification - Services cloud](https://azure.microsoft.com/pricing/details/cloud-services/) et [Tarification - Stockage Azure](https://azure.microsoft.com/pricing/details/storage/).

Hello suivant considérations peut-être vous aider à choisir une taille :

* Hello tailles A8-A11 et H-série sont également appelés *instances de calcul intensif*. matériel Hello qui exécute ces tailles est conçu et optimisé pour les calculs intensifs et applications, de modélisation et de simulations de cluster applications gourmandes en réseau, y compris informatique hautes performances (HPC). Hello A8-A11 série utilise Intel Xeon E5-2670 2,6 GHz et hello H-series v3 Intel Xeon E5-2667 @ 3,2 GHz. Pour plus d’informations et pour connaître les éléments à prendre en considération sur l’utilisation de ces tailles, consultez [Tailles de machines virtuelles de calcul haute performance](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Les séries Dv2, D et G sont idéales pour les applications qui exigent des processeurs plus rapides, de meilleures performances de disque local, ou qui ont des exigences de mémoire plus élevées. Elles offrent une combinaison puissante pour de nombreuses applications professionnelles.
* Certains des hôtes physiques hello des centres de données Azure incompatibles avec les grandes tailles de machine virtuelle, telles que A5 à A11. Par conséquent, vous pouvez voir le message d’erreur hello **virtuels n’a pas pu tooconfigure {nom de l’ordinateur}** ou **virtuels n’a pas pu toocreate {nom de l’ordinateur}** lors du redimensionnement d’un nouveau de tooa ordinateur virtuel existant taille ; Création d’un nouvel ordinateur virtuel dans un réseau virtuel créé avant le 16 avril 2013 ; ou l’ajout d’un ordinateur virtuel tooan existant service cloud. Consultez [erreur : « Ordinateur virtuel de tooconfigure échec »](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) sur le forum de support hello pour les solutions de contournement pour chaque scénario de déploiement.
* Votre abonnement peut également limiter hello nombre de cœurs, que vous pouvez déployer dans certaines familles de taille. tooincrease un quota, contactez le Support de Azure.

## <a name="performance-considerations"></a>Considérations relatives aux performances
Nous avons créé concept hello de hello unité de calcul de Azure (ACU) tooprovide un moyen de comparer les performances de calcul (processeur) entre les références (SKU) de Azure et tooidentify qui référence (SKU) est plus probable toosatisfy les performances de vos besoins.  L’unité ACU est actuellement normalisée sur une machine virtuelle de petite taille (Standard_A1) correspondant à 100, et toutes les autres références représentent ensuite approximativement la rapidité avec laquelle la référence en question peut exécuter un test d’évaluation.

> [!IMPORTANT]
> Hello ACU n'est qu’une indication. résultats Hello pour votre charge de travail peuvent varier.
>
>

<br>

| Famille de références | ACU/Cœur |
| --- | --- |
| [Très petite](#a-series) |50 |
| [Petite à très grande](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210 - 250* |
| [G1-5](#g-series) |180 - 240* |
| [H](#h-series) |290 - 300* |

ACUs marqués avec un * utiliser Intel® Turbo technologie tooincrease processeur fréquence et fournir une amélioration des performances. Hello quantité de renforcement de hello peut varier en fonction de la taille de machine virtuelle hello, de charge de travail et d’autres charges de travail en cours d’exécution sur hello même hôte.

## <a name="size-tables"></a>Tableaux des tailles
Hello tableaux suivants indiquent les tailles de hello et ils fournissent des capacités de hello.

* La capacité de stockage est indiquée en unités de Gio ou 1 024^3 octets. Lorsque la comparaison des disques exprimée en Go (1000 ^ 3 octets) toodisks mesurée en Gio (1024 ^ 3) souvenez-vous que les numéros de capacité dans Gio peuvent sembler inférieures. Par exemple, 1 023 Gio = 1 098,4 Go
* Le débit de disque est mesuré en opérations d’entrée/sortie par seconde (IOPS) et Mbits/s où Mbits/s = 10^6 octets par seconde.
* Les disques de données peuvent fonctionner en mode avec ou sans mise en cache. Pour l’opération de disque de données mises en cache, le mode de cache hôte hello est défini trop**ReadOnly** ou **ReadWrite**. Pour l’opération de disque de données non mis en cache, le mode de cache hôte hello est défini trop**aucun**.
* Bande passante réseau maximale est hello agrégées la bande passante maximale allouée et attribuée par le type de machine virtuelle. la bande passante maximale de Hello fournit des conseils pour la sélection de hello droite VM type tooensure une capacité réseau adéquate sont disponible. Lors du déplacement entre faible, modéré, haute et très élevée, le débit de hello augmente en conséquence. Les performances réseau réelles dépendent de nombreux facteurs, notamment les charges du réseau et de l’application, ainsi que les paramètres réseau de l’application.

## <a name="a-series"></a>Série A
| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | Disque dur local : Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Très petite      | 1         | 0,768        | 20                   | 1 / Faible |
| Petite           | 1         | 1,75         | 225                  | 1 / Modérée |
| Moyenne          | 2         | 3,5 Go       | 490                  | 1 / Modérée |
| Grande           | 4         | 7            | 1 000                 | 2 / Élevée |
| Très grande      | 8         | 14           | 2040                 | 4 / Élevée |
| A5              | 2         | 14           | 490                  | 1 / Modérée |
| A6              | 4         | 28           | 1 000                 | 2 / Élevée |
| A7              | 8         | 56           | 2040                 | 4 / Élevée |

## <a name="a-series---compute-intensive-instances"></a>Série A - Instances de calcul intensif
Pour plus d’informations et pour connaître les éléments à prendre en considération sur l’utilisation de ces tailles, consultez [Tailles de machines virtuelles de calcul haute performance](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | Disque dur local : Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8*             |8          | 56           | 1817                 | 2 / Élevée |
| A9*             |16         | 112          | 1817                 | 4 / Très élevée |
| A10             |8          | 56           | 1817                 | 2 / Élevée |
| A11             |16         | 112          | 1817                 | 4 / Très élevée |

\*Compatible RDMA

## <a name="av2-series"></a>Série Av2

| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | SSD local = Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1 / Modérée                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2 / Modérée                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4 / Élevée                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8 / Élevée                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2 / Modérée                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4 / Élevée                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8 / Élevée                     |


## <a name="d-series"></a>Série D
| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | SSD local = Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| D1 standard     | 1         | 3,5          | 50                   | 1 / Modérée |
| D2 standard     | 2         | 7            | 100                  | 2 / Élevée |
| D3 standard     | 4         | 14           | 200                  | 4 / Élevée |
| D4 standard     | 8         | 28           | 400                  | 8 / Élevée |
| D11 standard    | 2         | 14           | 100                  | 2 / Élevée |
| D12 standard    | 4         | 28           | 200                  | 4 / Élevée |
| D13 standard    | 8         | 56           | 400                  | 8 / Élevée |
| D14 standard    | 16        | 112          | 800                  | 8 / Très élevée |

## <a name="dv2-series"></a>Série Dv2
| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | SSD local = Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3,5          | 50                   | 1 / Modérée |
| Standard_D2_v2  | 2         | 7            | 100                  | 2 / Élevée |
| Standard_D3_v2  | 4         | 14           | 200                  | 4 / Élevée |
| Standard_D4_v2  | 8         | 28           | 400                  | 8 / Élevée |
| Standard_D5_v2  | 16        | 56           | 800                  | 8 / Extrêmement élevée |
| Standard_D11_v2 | 2         | 14           | 100                  | 2 / Élevée |
| Standard_D12_v2 | 4         | 28           | 200                  | 4 / Élevée |
| Standard_D13_v2 | 8         | 56           | 400                  | 8 / Élevée |
| Standard_D14_v2 | 16        | 112          | 800                  | 8 / Extrêmement élevée |
| Standard_D15_v2 | 20        | 140          | 1 000                | 8 / Extrêmement élevée |

## <a name="g-series"></a>Série G
| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | SSD local = Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1 / Élevée |
| Standard_G2     | 4         | 56           | 768                  |2 / Élevée |
| Standard_G3     | 8         | 112          | 1 536                |4 / Très élevée |
| Standard_G4     | 16        | 224          | 3 072                |8 / Extrêmement élevée |
| Standard_G5     | 32        | 448          | 6 144                |8 / Extrêmement élevée |

## <a name="h-series"></a>Série H
Machines virtuelles de série H sont hello prochaine génération informatiques hautes performances que machines virtuelles destinées à des besoins de calcul haut de gamme, telles que la modélisation moléculaire et fluides. Ces 8 et 16 noyaux VM reposent sur la technologie de processeur hello Intel Haswell E5-2667 V3 DDR4 mémoire et de stockage SSD local.

De plus toohello substantielle puissance de l’UC, hello H-series propose diverses options de mise en réseau RDMA de latence faible à l’aide de Verification InfiniBand et plusieurs configurations toosupport mémoire intensif calcul besoins en mémoire.

| Taille            | Cœurs d’unité centrale | Mémoire : Gio  | SSD local = Gio       | Cartes réseau (max)/Bande passante réseau |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1 000                 | 8 / Élevée |
| Standard_H16    | 16        | 112          | 2000                 | 8 / Très élevée |
| Standard_H8m    | 8         | 112          | 1 000                 | 8 / Élevée |
| Standard_H16m   | 16        | 224          | 2000                 | 8 / Très élevée |
| Standard_H16r*  | 16        | 112          | 2000                 | 8 / Très élevée |
| Standard_H16mr* | 16        | 224          | 2000                 | 8 / Très élevée |

\*Compatible RDMA

## <a name="configure-sizes-for-cloud-services"></a>Configurer les tailles pour les Cloud Services
Vous pouvez spécifier la taille de Machine virtuelle hello d’une instance de rôle dans le cadre du modèle de service hello décrite par hello [fichier de définition de service](cloud-services-model-and-package.md#csdef). taille Hello du rôle de hello détermine le nombre hello de cœurs du processeur, la capacité de mémoire hello et taille de système de fichiers local hello est allouée tooa instance en cours d’exécution. Choisissez la taille de rôle hello selon la spécification de ressources de votre application.

Voici un exemple de configuration hello rôle taille toobe [Standard_D2](#general-purpose-d) pour une instance de rôle Web :

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Modification de la taille de hello d’un rôle existant

En tant que caractère hello de votre charge de travail change ou les nouvelles tailles de machine virtuelle sont disponibles, vous souhaiterez taille de hello toochange de votre rôle. toodo, vous devez donc modifier la taille de machine virtuelle hello dans votre fichier de définition de service (comme indiqué ci-dessus), réorganiser votre Service Cloud et le déployer. Il n’est pas possible toochange les tailles de machine virtuelle directement à partir de hello portail ou de PowerShell.

>[!TIP]
> Vous souhaiterez toouse différentes tailles de machine virtuelle pour votre rôle dans des environnements différents (par exemple). test ou production). Une façon toodo cela est toocreate plusieurs fichiers de définition (.csdef) de service dans votre projet, puis créer des packages de service par l’environnement de cloud computing différent lors de la génération automatisée à l’aide d’outil de CSPack hello. package de services toolearn en savoir plus sur les éléments d’un cloud de hello et toocreate, voir [Nouveautés cloud de hello services modèle et comment il package ?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Obtenir une liste des tailles
Vous pouvez utiliser PowerShell ou hello API REST tooget une liste de tailles. Hello API REST est documenté [ici](https://msdn.microsoft.com/library/azure/dn469422.aspx). Bonjour de code suivant est une commande PowerShell qui répertorie toutes les tailles de hello actuellement disponibles pour votre Service Cloud.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur l’ [abonnement Azure et les limites, quotas et contraintes des services](../azure-subscription-service-limits.md).
* En savoir plus sur les [Tailles de machines virtuelles de calcul haute performance](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour les charges de travail HPC.
