---
title: aaaView consommation adresse IP publique dans la pile de Azure | Documents Microsoft
description: "Les administrateurs peuvent afficher la consommation hello d’adresses IP publiques dans une région"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 0f77be49-eafe-4886-8c58-a17061e8120f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/18/2017
ms.author: scottnap
ms.openlocfilehash: 771c011d133a030218b011cf94bbb8055f8996ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-public-ip-address-consumption-in-azure-stack"></a>Afficher la consommation d’adresses IP publiques dans Azure Stack
Comme administrateur du cloud, vous pouvez afficher le nombre hello d’adresses IP publiques qui ont été alloués tootenants, nombre de hello d’adresses IP publiques qui sont toujours disponibles pour l’allocation et le pourcentage de hello d’adresses IP publiques qui ont été alloués dans cette emplacement.

Hello **d’utilisation des pools d’adresses IP publiques** vignette affiche le nombre total de hello d’adresses IP publiques qui ont été consommés sur tous les pools d’adresses IP publiques sur l’infrastructure hello, si ils ont été utilisés pour le client IaaS VM instances, l’ensemble fibre optique services d’infrastructure, ou les ressources d’adresse IP publiques qui ont été créées explicitement par les locataires.

Hello l’objectif de cette vignette sont administrateurs de Azure pile toogive une idée de hello nombre total d’adresses IP publiques qui ont été consommés dans cet emplacement. Cela leur permet de déterminer si cette ressource est insuffisante.

Sur hello **fournisseurs de ressources**, **réseau** panneau, hello **des adresses IP publiques** élément de menu sous **ressources du client** répertorie uniquement les les adresses IP publiques qui ont été *explicitement créées par les locataires*. Par conséquent, hello nombre de **utilisé** des adresses IP publiques sur hello **d’utilisation des pools d’adresses IP publiques** vignette est toujours différente de (supérieur à) hello nombre sur hello **des adresses IP publiques** vignette sous **ressources du client**.

## <a name="view-hello-public-ip-address-usage-information"></a>Afficher les informations d’utilisation d’adresse publiques IP hello
tooview hello nombre total d’adresses IP publiques qui ont été consommés dans la région de hello :

1. Dans le portail d’administration hello pile d’Azure, cliquez sur **davantage de services**, sous **ressources administratives**, cliquez sur **fournisseurs de ressources**.
2. À partir de la liste des hello **fournisseurs de ressources**, sélectionnez **réseau**.
3. Hello **réseau** panneau affiche hello **d’utilisation des pools d’adresses IP publiques** vignette Bonjour **vue d’ensemble** section.

![Panneau Fournisseur de ressources réseau](media/azure-stack-viewing-public-ip-address-consumption/image01.png)

Gardez à l’esprit que hello **utilisé** nombre représente le nombre de hello d’adresses IP publiques à partir de tous les publics pools d’adresses IP à cet emplacement qui sont affectés. Hello **libre** nombre représente hello nombre d’adresses IP publiques à partir de tous les pools d’adresses IP publiques qui n’ont pas été attribuées et qui sont toujours disponibles. Hello **% utilisées** nombre représente le nombre hello d’utilisé ou adresses attribuées en tant que pourcentage du nombre total de hello d’adresses IP publiques dans tous les pools d’adresses IP publiques dans cet emplacement.

## <a name="view-hello-public-ip-addresses-that-were-created-by-tenant-subscriptions"></a>Vue hello adresses IP publiques qui ont été créés par abonnements du locataire
toosee une liste d’adresses IP publiques qui ont été créées explicitement par abonnements du locataire dans une région spécifique, cliquez sur **des adresses IP publiques** sous **ressources du client**.

![Adresses IP publiques de locataire](media/azure-stack-viewing-public-ip-address-consumption/image02.png)

Vous pouvez remarquer que certaines adresses IP publiques qui ont été alloués dynamiquement s’affichent dans la liste de hello mais n’ont pas une adresse associée encore. Il s’agit, car la ressource d’adresse hello a encore été créé dans le fournisseur de ressources réseau, mais pas dans hello contrôleur de réseau.

Hello contrôleur de réseau n’attribue pas une ressource d’adresse toothis jusqu'à ce qu’il est effectivement lié tooan interface, une carte d’interface réseau (NIC), un équilibreur de charge ou une passerelle de réseau virtuel. Lors de l’adresse IP publique de hello est lié tooan interface, hello contrôleur de réseau alloue une tooit d’adresse IP, et il apparaît dans hello **adresse** champ.

## <a name="view-hello-public-ip-address-information-summary-table"></a>Vue hello publique informations récapitulative table d’adresses IP
Il existe un nombre de différents cas dans lesquels les adresses IP publiques sont affectés qui déterminent si l’adresse de hello figure dans une liste ou un autre.

| **Cas d’affectation d’adresses IP publiques** | **Apparaît dans le récapitulatif d’utilisation** | **Apparaît dans la liste d’adresses IP publiques du locataire** |
| --- | --- | --- |
| Adresse IP publique de dynamique non encore assignés tooan carte réseau ou un équilibrage (temporaire) |Non |Oui |
| Dynamique adresse IP publique affectée tooan carte réseau ou un équilibrage. |Oui |Oui |
| Adresse IP publique statique affecté tooa locataire équilibreur de charge ou de la carte réseau. |Oui |Oui |
| Statique publique IP adresse affectée tooa fabric infrastructure service point de terminaison. |Oui |Non |
| Adresse IP publique implicitement créé pour les instances de IaaS VM et utilisée pour NAT de trafic sortant sur le réseau virtuel de hello. Ceux-ci sont créés coulisses hello chaque fois qu’un client crée une instance de machine virtuelle afin que les machines virtuelles peuvent envoyer des informations toohello Internet. |Oui |Non |

## <a name="next-steps"></a>Étapes suivantes
[Gérer les comptes de stockage dans Azure Stack](azure-stack-manage-storage-accounts.md)