---
title: "Azure Site Recovery deployment planner pour le déploiement de VMware vers Azure| Microsoft Docs"
description: "Il s’agit du guide de l’utilisateur d’Azure Site Recovery deployment planner."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/04/2017
ms.author: nisoneji
ms.openlocfilehash: 2985ed0b4bf5d9525bc2274d71b703922524f5a8
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2018
---
# <a name="azure-site-recovery-deployment-planner-for-vmware-to-azure"></a>Planificateur de déploiement Azure Site Recovery de VMware vers Azure
Cet article est le guide de l’utilisateur d’Azure Site Recovery Deployment Planner portant sur les déploiements de production de VMware vers Azure.

## <a name="overview"></a>Vue d'ensemble

Avant de commencer à protéger les machines virtuelles VMware à l’aide de Site Recovery, allouez suffisamment de bande passante en fonction de votre taux de modifications des données par jour pour atteindre votre objectif de point de récupération (RPO) souhaité. Assurez-vous de déployer le nombre approprié de serveurs de configuration et de serveurs de processus en local.

Vous devez également créer le type approprié et le nombre de comptes de stockage Azure cibles. Vous créez des comptes de stockage standard ou premium, en tenant compte de la croissance de vos serveurs de production sources en raison d’une utilisation accrue au fil du temps. Vous choisissez le type de stockage par machine virtuelle, en fonction des caractéristiques de charge de travail (par exemple, les opérations de lecture/écriture d’E/S par seconde, ou l’activité des données) et des limites Site Recovery.

Le planificateur de déploiement Azure Site Recovery est un outil de ligne de commande pour les scénarios de récupération d’urgence de Hyper-V vers Azure et de VMware vers Azure. Vous pouvez profiler à distance vos machines virtuelles VMware à l’aide de cet outil (sans conséquences sur la production) pour comprendre les besoins de stockage Azure et de bande passante afin d’assurer la réussite de la réplication et du test de basculement. Vous pouvez exécuter l’outil sans installer les composants Site Recovery locaux. Cependant, pour obtenir des résultats de débit précis, nous vous recommandons d’exécuter l’outil sur un serveur Windows Server répondant à la configuration requise minimale du serveur de configuration Site Recovery que vous devrez finalement déployer dans les premières étapes du déploiement de production.

L’outil fournit les informations suivantes :

**Évaluation de la compatibilité**

* Une évaluation de l’éligibilité de la machine virtuelle en fonction du nombre de disques, de la taille du disque, des E/S par seconde, de l’activité, du type de démarrage (EFI/BIOS) et de la version du système d’exploitation
 
**Besoin de bande passante réseau et évaluation de RPO**

* La bande passante réseau estimée requise pour la réplication différentielle
* Le débit pouvant être obtenu par Site Recovery dans le scénario « local vers Azure »
* Le nombre de machines virtuelles à traiter par lot en fonction de la bande passante estimée pour effectuer une réplication initiale pendant une durée donnée
* RPO qui peut être obtenu pour une bande passante donnée
* Impact sur le RPO souhaité si une bande passante inférieure est configurée.

**Exigences de l’infrastructure Azure**

* Le type de stockage (compte de stockage standard ou premium) pour chaque machine virtuelle
* Le nombre total de comptes de stockage standard et premium à configurer pour la réplication
* Suggestions d’affectation de noms pour les comptes de stockage en fonction des conseils liés au Stockage Azure
* L’emplacement du compte de stockage pour toutes les machines virtuelles
* Le nombre de cœurs Azure à configurer avant le test de basculement ou le basculement sur l’abonnement
* La taille recommandée de machine virtuelle Azure pour chaque machine virtuelle sur site

**Exigences de l’infrastructure locale**
* Le nombre requis de serveurs de configuration et de serveurs de processus à déployer en local

**Estimation du coût de récupération d’urgence vers Azure**
* Estimation du coût total de récupération d’urgence vers Azure : coût de calcul, stockage, réseau et de licence Azure Site Recovery
* Analyse détaillée du coût par machine virtuelle


>[!IMPORTANT]
>
>Étant donné que l’utilisation est susceptible d’augmenter au fil du temps, tous les calculs de l’outil précédent sont effectués en supposant un facteur de croissance de 30 pour cent de caractéristiques de charge de travail et à l’aide d’une valeur de 95e centile de toutes les mesures profilage (E/S par seconde en lecture/écriture, activité, etc.). Ces deux éléments (facteur de croissance et calcul de centile), sont configurables. Pour en savoir plus sur le facteur de croissance, consultez la section « Considérations relatives au facteur de croissance ». Pour en savoir plus sur la valeur de centile, consultez la section « Valeur de centile utilisée pour le calcul ».
>

## <a name="support-matrix"></a>Matrice de prise en charge

| | **VMware vers Azure** |**Hyper-V vers Azure**|**Azure vers Azure**|**Hyper-V vers un site secondaire**|**VMware vers un site secondaire**
--|--|--|--|--|--
Scénarios pris en charge |Oui|Oui|Non |Oui*|Non 
Version prise en charge | vCenter 6.5, 6.0 ou 5.5| Windows Server 2016, Windows Server 2012 R2 | N/D |Windows Server 2016, Windows Server 2012 R2|N/D
Configuration prise en charge|vCenter, ESXi| Cluster Hyper-V, hôte Hyper-V|N/D|Cluster Hyper-V, hôte Hyper-V|N/D|
Nombre de serveurs pouvant être profilés par instance en cours d’exécution du planificateur de déploiement Azure Site Recovery |Unique (des machines virtuelles appartenant à un vCenter Server ou un serveur ESXi peuvent être profilées à la fois)|Plusieurs (des machines virtuelles sur plusieurs hôtes ou clusters hôtes peuvent être profilées à la fois)| N/D |Plusieurs (des machines virtuelles sur plusieurs hôtes ou clusters hôtes peuvent être profilées à la fois)| N/D

* L’outil s’applique principalement au scénario de récupération d’urgence Hyper-V vers Azure. Pour la récupération d’urgence Hyper-V vers un site secondaire, il permet uniquement de disposer de recommandations côté source telles que la bande passante réseau requise, l’espace de stockage disponible requis sur chacun des serveurs Hyper-V source, et les numéros et définitions de lots de réplication initiale.  Ignorez les recommandations et coûts Azure dans le rapport. De plus, l’opération d’obtention du débit ne s’applique pas au scénario de récupération d’urgence Hyper-V vers un site secondaire.

## <a name="prerequisites"></a>Conditions préalables
L’outil comporte deux phases principales : le profilage et la génération de rapport. En outre, une troisième option permet de calculer le débit uniquement. La configuration requise pour le serveur à partir de laquelle le profilage et la mesure du débit sont initiés est présentée dans le tableau suivant :

| Configuration requise du serveur | DESCRIPTION|
|---|---|
|Profilage et mesure du débit| <ul><li>Système d’exploitation : Microsoft Windows Server 2016 ou Microsoft Windows Server 2012 R2<br>(dans l’idéal, correspondant au moins aux [recommandations de taille pour le serveur de configuration](https://aka.ms/asr-v2a-on-prem-components))</li><li>Configuration de la machine : 8 processeurs virtuels, 16 Go de RAM, disque dur de 300 Go</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Microsoft Visual C++ Redistributable pour Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>Accès Internet à Azure à partir de ce serveur</li><li>Compte Azure Storage</li><li>Accès administrateur sur le serveur</li><li>Au minimum 100 Go d’espace disque disponible (en supposant que 1 000 machines virtuelles avec une moyenne de trois disques chacune, profilage pour 30 jours)</li><li>Les paramètres de niveau de statistiques de VMware vCenter doivent être définis sur le niveau 2 ou un niveau supérieur</li><li>Autoriser le port 443 : le planificateur de déploiement ASR se sert de ce port pour se connecter au serveur vCenter/à l’hôte ESXi</ul></ul>|
| Génération de rapport | Un PC Windows ou serveur Windows Server doté de Microsoft Excel 2013 ou version ultérieure |
| Autorisations utilisateur | Autorisation de lecture seule pour le compte d’utilisateur utilisé pour accéder au serveur VMware vCenter/à l’hôte VMware vSphere ESXi lors du profilage |

> [!NOTE]
>
>L’outil peut profiler uniquement des machines virtuelles avec des disques de machines virtuelles et des disques RDM. Il ne peut pas profiler les machines virtuelles équipées de disques iSCSI ou NFS. Site Recovery prend en charge les disques iSCSI et NFS pour les serveurs VMware, mais comme l’outil Deployment Planner ne se trouve pas dans l’invité et n’effectue le profilage qu’à l’aide des compteurs de performance vCenter, il n’a pas de visibilité sur ces types de disque.
>

## <a name="download-and-extract-the-deployment-planner-tool"></a>Télécharger et extraire l’outil de planification du déploiement
1. Téléchargez la dernière version [d’Azure Site Recovery deployment planner](https://aka.ms/asr-deployment-planner).  
L’outil se présente dans un dossier .zip. Sa version actuelle ne prend en charge que le scénario VMware vers Azure.

2. Copiez le dossier .zip sur le serveur Windows à partir duquel vous voulez exécuter l’outil.  
Vous pouvez exécuter l’outil à partir de Windows Server 2012 R2 si le serveur a accès au réseau pour se connecter au serveur vCenter/à l’hôte vSphere ESXi qui contient les machines virtuelles à profiler. Toutefois, nous vous recommandons d’exécuter l’outil sur un serveur dont la configuration matérielle répond aux [indications de dimensionnement pour les serveurs de configuration](https://aka.ms/asr-v2a-on-prem-components). Si vous avez déjà déployé les composants Site Recovery en local, exécutez l’outil à partir du serveur de configuration.

 Nous vous recommandons d’adopter la même configuration matérielle que le serveur de configuration (qui dispose d’un serveur de processus intégré) sur le serveur sur lequel vous exécutez l’outil. Cette configuration garantit que le débit atteint rapporté par l’outil corresponde au débit que Site Recovery peut atteindre lors de la réplication. Le calcul du débit dépend de la bande passante réseau disponible sur le serveur et de la configuration matérielle (processeur, stockage, etc.) du serveur. Si vous exécutez l’outil à partir de n’importe quel autre serveur, le débit est calculé à partir de ce serveur vers Microsoft Azure. En outre, étant donné que la configuration matérielle du serveur peut différer de celle du serveur de configuration, le débit atteint rapporté par l’outil peut être inexact.

3. Extrayez le dossier .zip.  
Le dossier contient plusieurs fichiers et sous-dossiers. Le fichier exécutable s’appelle ASRDeploymentPlanner.exe dans le dossier parent.

    Exemple :  
    Copiez le fichier .zip sur le lecteur E:\ et extrayez-le.
   E:\ASR Deployment Planner_v2.1zip

    E:\ASR Deployment Planner_v2.1\ASRDeploymentPlanner.exe

### <a name="updating-to-the-latest-version-of-deployment-planner"></a>Mise à jour vers la dernière version du planificateur de déploiement
Si vous disposez d’une version précédente du planificateur de déploiement, effectuez l’une des actions suivantes :
 * Si la dernière version ne contient pas de correctif de profilage, et que le profilage est déjà en cours sur votre version actuelle de la planification, passez au profilage.
 * Si la dernière version contient un correctif de profilage, nous vous recommandons d’arrêter le profilage sur votre version actuelle et de redémarrer le profilage avec la nouvelle version.


 >[!NOTE]
 >
 >Lorsque vous démarrez le profilage avec la nouvelle version, transmettez le même chemin de répertoire de sortie de sorte que l’outil ajoute les données de profil sur les fichiers existants. Un ensemble complet de données profilées est utilisé pour générer le rapport. Si vous transmettez un répertoire de sortie différent, des fichiers sont créés et les anciennes données profilées ne sont pas utilisées pour générer les rapports.
 >
 >Chaque nouveau deployment planner est une mise à jour cumulative du fichier .zip. Vous n’avez pas besoin de copier les fichiers les plus récents dans le dossier précédent. Vous pouvez créer un dossier et l’utiliser.


## <a name="version-history"></a>Historique des versions
La dernière version de l’outil Planificateur de déploiement ASR est 2.1.
Reportez-vous à la page [Historique des versions du planificateur de déploiement](https://social.technet.microsoft.com/wiki/contents/articles/51049.asr-deployment-planner-version-history.aspx) pour voir les correctifs ajoutés à chaque mise à jour.

## <a name="next-steps"></a>étapes suivantes
* [Exécutez le planificateur de déploiement](site-recovery-vmware-deployment-planner-run.md).
