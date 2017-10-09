---
title: "aaaLearn sur hello dernières versions de système d’exploitation invité Azure | Documents Microsoft"
description: "Bonjour les dernières informations de version et de compatibilité du Kit de développement logiciel pour le système d’exploitation invité de Azure Cloud Services."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Versions du SE invité et matrice de compatibilité du Kit de développement logiciel (SDK) Azure
Vous fournit des informations récentes sur hello que libère le dernier système d’exploitation invité de Azure pour Services de cloud computing. Ces informations vous permettent de planifier votre mise à niveau avant la désactivation d’un SE invité. Si vous configurez votre toouse rôles *automatique* mises à jour de système d’exploitation invité comme décrit dans [paramètres de mise à jour du système d’exploitation Azure invité][Azure Guest OS Update Settings], il n’est pas indispensable que vous lisez cette page.

> [!IMPORTANT]
> Cette page s’applique tooCloud Services rôles web et de travail, qui s’exécutent sur un système d’exploitation invité. Il effectue **s’appliquent pas** tooIaaS Machines virtuelles.
>
>


> [!NOTE]
> Flux RSS de Hello a été récemment déconseillée. Surveillez les mises à jour sur un nouveau flux bientôt disponible !
>
>

Savez pas quel hello est de système d’exploitation invité ou hello comment le système d’exploitation invité libère travail ? Lisez [cette](#how-it-works) section.

## <a name="news-updates"></a>Nouvelles mises à jour

###### <a name="august-24-2017"></a>**24 août 2017**
Publication du SE invité août.

###### <a name="august-3-2017"></a>**3 août 2017**
Publication du SE invité juillet.

###### <a name="july-19-2017"></a>**19 juillet 2017**
Début du déploiement du SE invité de juillet le 19 juillet et publication projetée le 8 août.

###### <a name="july-7-2017"></a>**7 juillet 2017**
Publication du SE invité juin.

###### <a name="june-16-2017"></a>**16 juin 2017**
Début du déploiement du SE invité de juin le 16 juin et publication projetée le 11 juillet.

###### <a name="june-5-2017"></a>**5 juin 2017**
Publication du SE invité mai.

###### <a name="may-17-2017"></a>**17 mai 2017**
En raison du bogue de sécurité tooa, nous allons désactiver hello suivant 2016 de décembre et janvier 2017 versions du système d’exploitation qui n’ont pas hello [corriger] à partir du portail de hello : WA-invité-OS-5.4_201612-01, WA-invité-OS-4.39_201612-01, WA-invité-système d’exploitation-3.46_ 201612-01, WA-GUEST-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**12 mai 2017**
Début du déploiement du SE invité de mai le 12 mai et publication projetée le 13 juin.

###### <a name="april-18-2017"></a>**18 avril 2017**
Début du déploiement du SE invité d’avril le 18 avril et publication projetée le 9 mai.

###### <a name="april-10-2017"></a>**10 avril 2017**
Le déploiement du SE invité de mars a commencé le 14 mars 2017 et s’est achevé le 10 avril 2017.

###### <a name="january-10-2017"></a>**10 janvier 2017**
Hello du système d’exploitation invité de janvier contient des correctifs qui affectent uniquement la famille de systèmes d’exploitation 2 (Windows Server 2008 R2). Nous avons publié par conséquent uniquement l’image hello 2 de famille du système d’exploitation (WA-GUEST-OS-2.59_201701-01) pour ce mois. Pour toutes les familles du système d’exploitation, hello décembre du système d’exploitation (201612 - 01) reste hello plus récentes.


## <a name="releases"></a>Publications
## <a name="family-5-releases"></a>Publications de famille 5
**Windows Server 2016**

.NET Framework est installé : 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> Les dates avec un * sont toochange de sujet.
>
> Hello mot de passe RDP 5 de famille du système d’exploitation doit être d’au moins 10 caractères.
>

| Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |24 août 2017 |Post 5.12 |TBD |
| WA-GUEST-OS-5.9_201707-01 |3 août 2017 |Post 5.11 |TBD |
| WA-GUEST-OS-5.8_201706-01 |7 juillet 2017 |Post 5.10 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |5 juin 2017 |24 août 2017 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |9 mai 2017 |3 août 2017 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |10 avril 2017 |7 juillet 2017 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |10 janvier 2017 |5 juin 2017|TBD |
|~~WA-GUEST-OS-5.3_201611-01~~ |14 décembre 2016 |9 mai 2017 |TBD |
|~~WA-GUEST-OS-5.2_201610-02~~ |1er novembre 2016 |10 avril 2017 |TBD |

## <a name="family-4-releases"></a>Publications de famille 4
**Windows Server 2012 R2**

Prend en charge .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Les dates avec un * sont toochange d’objet
>
>

| Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |24 août 2017 |Post 4.47 |TBD |
| WA-GUEST-OS-4.44_201707-01 |3 août 2017 |Post 4.46 |TBD |
| WA-GUEST-OS-4.43_201706-01 |7 juillet 2017 |Post 4.45 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |5 juin 2017 |24 août 2017 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |9 mai 2017 |3 août 2017 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |10 avril 2017 |7 juillet 2017 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |10 janvier 2017 |5 juin 2017 |TBD |
|~~WA-GUEST-OS-4.38_201611-01~~ |14 décembre 2016 |9 mai 2017 |TBD |
|~~WA-GUEST-OS-4.37_201610-02~~ |16 novembre 2016 |10 avril 2017 |TBD |
|~~WA-GUEST-OS-4.36_201609-01~~ |13 octobre 2016 |14 janvier 2017 |TBD |
|~~WA-GUEST-OS-4.35_201608-01~~ |13 septembre 2016 |16 décembre 2016 |TBD |
|~~WA-GUEST-OS-4.34_201607-01~~ |8 août 2016 |13 novembre 2016 |TBD |


## <a name="family-3-releases"></a>Publications de famille 3
**Windows Server 2012**

Prend en charge .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Les dates avec un * sont toochange d’objet
>
>

| Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |24 août 2017 |Post 3.54 |TBD |
| WA-GUEST-OS-3.51_201707-01 |3 août 2017 |Post 3.53 |TBD |
| WA-GUEST-OS-3.50_201706-01 |7 juillet 2017 |Post 3.52 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |5 juin 2017 |24 août 2017 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |9 mai 2017 |3 août 2017 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |10 avril 2017 |7 juillet 2017 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |10 janvier 2017 |5 juin 2017 |TBD |
|~~WA-GUEST-OS-3.45_201611-01~~ |14 décembre 2016 |9 mai 2017 |TBD |
|~~WA-GUEST-OS-3.44_201610-02~~ |16 novembre 2016 |1 mai 2017 |TBD |
|~~WA-GUEST-OS-3.43_201609-01~~ |13 octobre 2016 |14 janvier 2017 |TBD |
|~~WA-GUEST-OS-3.42_201608-01~~ |13 septembre 2016 |16 décembre 2016 |TBD |
|~~WA-GUEST-OS-3.41_201607-01~~ |8 août 2016 |13 novembre 2016 |TBD |


## <a name="family-2-releases"></a>Publications de famille 2
**Windows Server 2008 R2 SP1**

Prend en charge .NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Les dates avec un * sont toochange d’objet
>
>

| Chaîne de configuration | Date de lancement | Date de désactivation | Date d’expiration |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |24 août 2017 |Post 2.67 |TBD |
| WA-GUEST-OS-2.64_201707-01 |3 août 2017 |Post 2.66 |TBD |
| WA-GUEST-OS-2.63_201706-01 |7 juillet 2017 |Post 2.65 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |5 juin 2017 |24 août 2017 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |9 mai 2017 |3 août 2017 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |10 avril 2017 |7 juillet 2017 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |10 janvier 2017 |5 juin 2017 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |10 janvier 2017 |9 mai 2017|TBD |
|~~WA-GUEST-OS-2.57_201611-01~~ |14 décembre 2016 |10 avril 2017 |TBD |
|~~WA-GUEST-OS-2.56_201610-02~~ |16 novembre 2016 |10 février 2017 |TBD |
|~~WA-GUEST-OS-2.55_201609-01~~ |13 octobre 2016 |14 janvier 2017 |TBD |
|~~WA-GUEST-OS-2.54_201608-01~~ |13 septembre 2016 |16 décembre 2016 |TBD |
|~~WA-GUEST-OS-2.53_201607-01~~ |8 août 2016 |13 novembre 2016 |TBD |



## <a name="msrc-patch-updates"></a>Mises à jour correctives MSRC
Hello liste des correctifs qui sont inclus dans chaque version de système d’exploitation invité mensuelle est disponible [ici][patches].

## <a name="sdk-support"></a>Prise en charge des Kits de développement logiciel (SDK)
Bien que hello [stratégie de retrait pour hello Azure SDK] [ retire policy sdk] indique que seules les versions ci-dessus 2.2 sont pris en charge, spécifique des familles de système d’exploitation invité vous autorisent toouse les versions antérieures. Vous devez toujours utiliser hello plus tard pris en charge le Kit de développement logiciel.

| Famille de SE invité | Versions du Kit de développement logiciel (SDK) compatibles |
| --- | --- |
| 5 |Versions 2.9.5.1 et ultérieures |
| 4 |Versions 2.1 et ultérieures |
| 3 |Versions 1.8 et ultérieures |
| 2 |Versions 1.3 et ultérieures |
| 1 |Versions 1.0 et ultérieures |

## <a name="guest-os-release-information"></a>Informations de publication du SE invité
Il existe trois dates importantes tooGuest du système d’exploitation libère : **release** date, **désactivé** date, et **expiration** date. Un système d’exploitation invité est considéré comme étant disponible lorsqu’il est dans le portail de hello et peut être sélectionné comme cible de hello du système d’exploitation invité. Lorsqu’un système d’exploitation invité atteint hello **désactivé** date, il est supprimé de Azure. Toutefois, tous les services cloud qui ciblent ce SE invité continuent de fonctionner normalement.

fenêtre Hello entre hello **désactivé** date et hello **expiration** date vous fournit une transition tooeasily de mémoire tampon à partir d’un tooone de système d’exploitation invité plus récente. Si vous utilisez *automatique* en tant que votre système d’exploitation invité, vous serez toujours sur la version la plus récente hello et vous n’avez pas tooworry à son expiration.

Hello lorsque **expiration** passe, n’importe quel Service Cloud toujours à l’aide de ce système d’exploitation invité est arrêté, supprimé ou forcé tooupgrade de date. Vous pouvez en savoir plus sur la stratégie de retrait hello [ici][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Informations sur les versions des familles de SE invité
familles de système d’exploitation invité Hello sont basées sur les versions publiées de Microsoft Windows Server. Hello du système d’exploitation invité est système d’exploitation sous-jacent hello qui exécute Azure Cloud Services. Chaque SE invité possède un numéro de famille, de version et de publication.

* **Guest OS family**  
  Version du système d’exploitation Windows Server sur laquelle est basé un SE invité. Par exemple, la *famille 3* est basée sur Windows Server 2012.
* **Version de SE invité**  
  Tooa spécifique famille de système d’exploitation invité de l’image plus pertinentes [MSRC Microsoft Security Response Center ()] [ msrc] correctifs qui sont disponibles dans la version de système d’exploitation invité nouveau hello date hello est généré. Il est possible que les correctifs ne soient pas tous inclus.

    Les numéros commencent à 0 et augmentent de 1 chaque fois qu’un nouvel ensemble de mises à jour est ajouté. Les zéros à droite sont uniquement affichés s’ils sont importants. Autrement dit, la version 2.10 est une version différente, bien plus récente, que la version 2.1.
* **Publication de SE invité**  
  Nouvelle publication d’une version de SE invité. Une nouvelle publication est produite si Microsoft détecte des problèmes pendant les tests nécessitant des modifications. Hello dernière build publiée remplace toujours précédent libère, public ou non. Hello portail Azure autorise uniquement les utilisateurs toopick hello dernière version pour une version donnée. Les déploiements en cours d’exécution sur une version précédente ne sont généralement pas automatiquement mis à niveau en fonction de la gravité hello de bogue de hello.

Dans l’exemple hello ci-dessous, 2 est la famille de hello, 12 est la version de hello et « rel2 » est mise en production hello.

**Publication du SE invité** - 2.12 rel2

**Chaîne de configuration pour cette publication** - WA-GUEST-OS-2.12_201208-02

chaîne de configuration Hello pour un système d’exploitation invité possède ces mêmes informations intégrées, ainsi qu’une date indiquant les correctifs MSRC ont été analysés pour cette version. Dans cet exemple, les correctifs MSRC produits pour Windows Server 2008 R2 des tooand jusqu’en août 2012 ont été analysés pour l’inclure. Seuls les correctifs logiciels qui s’appliquent spécifiquement version toothat de Windows Server sont inclus. Par exemple, si un correctif MSRC s’applique tooMicrosoft Office, il sera pas inclus, car ce produit n’est pas partie de l’image de base Windows Server hello.

## <a name="guest-os-system-update-process"></a>Processus de mise à jour du SE invité
Cette page contient des informations sur les prochaines publications de SE invités. Les clients ont communiqué qu’ils veulent tooknow lorsqu’une version se produit parce que leurs rôles de service cloud redémarrent si elles sont définies à une mise à jour trop « automatique ». Les versions de système d’exploitation invité se produisent généralement au moins cinq (5) jours après la mise à jour se produit sur hello deuxième mardi de chaque mois jour hello MSRC. Les nouvelles versions incluent tous les hello correctifs appropriés de MSRC pour chaque famille de système d’exploitation invité.

Microsoft Azure publie constamment des mises à jour. Hello du système d’exploitation invité n'est qu’une telle mise à jour dans le pipeline de hello. Une version peut être affectée par de nombreux facteurs trop nombreuses toolist ici. En outre, Azure s’exécute sur des centaines de milliers d’ordinateurs. Cela signifie qu’il est impossible toogive une date exacte et une heure lorsque redémarrage de vos rôles. Nous avons travaillez sur un plan toolimit ou moment où ils interviennent.

Lorsqu’une nouvelle version de système d’exploitation invité est publiée de hello, il peut prendre un temps toofully se propage sur Azure. Comme les services sont mis à jour toohello nouveau système d’exploitation invité, ils sont redémarré en respectant des domaines de mise à jour. Mises à jour « Automatique » services ensemble toouse seront obtiennent une build en premier. Après la mise à jour de hello, vous verrez nouvelle version de système d’exploitation invité hello répertoriée pour votre service Bonjour portail Azure. De nouvelles publications peuvent se produire pendant cette période. Certaines versions peuvent être déployées sur de longues périodes et les redémarrages de mise à niveau automatique peut ne pas survenir pour plusieurs semaines après la date de sortie officielle hello. Une fois qu’un système d’exploitation invité est disponible, vous pouvez choisir explicitement cette version à partir du portail de hello ou dans votre fichier de configuration.

Pour une grande partie des informations précieuses sur les redémarrages et les pointeurs toomore informations techniques de mises à jour du système d’exploitation hôte et de l’invité, consultez hello du blog MSDN intitulé post [rôle Instance redémarre en raison des mises à niveau de tooOS] [ restarts].

Si vous mettre à jour manuellement votre système d’exploitation invité, consultez hello [stratégie de retrait de système d’exploitation invité] [ retirepolicy] pour plus d’informations.

## <a name="guest-os-supportability-and-retirement-policy"></a>Prise en charge et stratégie de suppression du SE invité
stratégie de prise en charge et de retrait du système d’exploitation invité de Hello est expliquée [ici][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[corriger]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
