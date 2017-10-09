---
title: aaaEndorsed des distributions de Linux | Documents Microsoft
description: "Découvrez les distributions Linux approuvées sur Azure, notamment des instructions pour Ubuntu, CentOS, Oracle et SUSE."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux sur les distributions approuvées par Azure
Partenaires pour fournir des images de Linux Bonjour Azure Marketplace. Nous travaillons avec diverses tooadd de communautés Linux davantage versions toohello visé liste. Bonjour pendant ce temps, pour les distributions qui ne sont pas disponibles à partir de hello Marketplace, vous pouvez toujours mettre votre propre Linux en suivant les instructions de hello sur [création et téléchargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Distributions et versions prises en charge
Hello tableau suivant répertorie les distributions de Linux hello et les versions prises en charge sur Azure. Consultez trop[de l’image de prise en charge de Linux dans Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) pour plus d’informations.

pilotes de Services d’intégration Linux (LIS) Hello pour Hyper-V et Azure sont des modules de noyau que Microsoft participe directement toohello en amont noyau de Linux.  Certains pilotes LIS sont intégrées à noyau de la distribution hello par défaut. D’anciennes distributions basées sur Red Hat Enterprise (RHEL)/CentOS sont disponibles sous la forme de téléchargements séparés à partir de la page [Linux Integration Services Version 4.1 pour Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Consultez [configuration requise du noyau Linux](create-upload-generic.md#linux-kernel-requirements) pour plus d’informations sur les pilotes LIS hello.

Hello Linux Agent Azure est déjà préinstallé sur les images Azure Marketplace hello et est généralement disponible à partir d’un référentiel de packages de distribution hello. Le code source est disponible sur [GitHub](https://github.com/azure/walinuxagent).

| Distribution | Version | Pilotes | Agent |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+, 7.0+ |CentOS 6.3 : [téléchargement LIS](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4+ : dans le noyau |Paquet : dans le [référentiel](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) sous « WALinuxAgent » <br/>Code source : [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |Dans le noyau |Code source : [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+, 8.2+ |Dans le noyau |Package : dans le référentiel sous « waagent »  <br/>Code source : [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |Dans le noyau |Package : dans le référentiel sous « WALinuxAgent »  <br/>Code source : [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+, 7.1+ |Dans le noyau |Package : dans le référentiel sous « WALinuxAgent »  <br/>Code source : [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES pour SAP<br>11 SP4<br>12 SP1+|Dans le noyau |Package :<p> pour 11 dans le référentiel [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools)<br>pour 12 inclus dans le module « Cloud public » sous « python-azure-agent »<br/>Code source : [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |Dans le noyau |Package: dans le référentiel [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) sous « python-azure-agent » <br/>Code source : [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |Dans le noyau |Package : dans le référentiel sous « WALinuxAgent »  <br/>Code source : [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Partenaires

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

À partir du site Web de CoreOS hello :

*CoreOS est conçu pour la sécurité, la cohérence et la fiabilité. Au lieu de l’installation des packages via yum ou apt, CoreOS utilise Linux conteneurs toomanage vos services à un niveau supérieur d’abstraction. Un code de service unique et l’ensemble des dépendances sont déployés au sein d’un conteneur pouvant être exécuté sur une ou plusieurs machines CoreOS.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ est un consultant indépendant et des services qui est spécialisé dans le développement de hello et l’implémentation de solutions professionnelles à l’aide de logiciels gratuits. En tant de leader spécialiste de l’Open Source, Credativ a acquis une reconnaissance internationale et de nombreux services informatiques font appel à ses services. En collaboration avec Microsoft, Credativ actuellement prépare images Debian correspondantes pour Debian 8 (Jessica) et Debian avant le 7 (Wheezy). Les deux images sont spécialement conçus pour toorun sur Azure et peuvent être facilement gérés via la plateforme de hello. Credativ prendront également en charge la mise à jour des images de Debian hello pour Azure via ses centres de Support Open Source et la maintenance à long terme de hello.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Stratégie d’Oracle est toooffer une large gamme de solutions pour les clouds privés et publics. stratégie de Hello offre aux clients de choix et la flexibilité dans comment ils déploient des logiciels Oracle dans des clouds d’Oracle et autres clouds. Partenariat d’Oracle avec Microsoft permet au logiciel d’Oracle de toodeploy clients dans des clouds privés et publics de Microsoft en toute confiance hello de certification et de prise en charge à partir d’Oracle.  L'engagement et l'investissement d'Oracle vis-à-vis des solutions de cloud public et privé Oracle sont intacts.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/Strategic-Alliance/Microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Hello premier fournisseur du world de solutions en open source, Red Hat permet plus de 90 % du classement de Fortune 500 relever les défis de l’entreprise, aligner leur informatique et stratégies d’entreprise et se préparer à l’avenir hello de technologie. Red Hat y parvient en proposant des solutions sécurisées grâce à un modèle commercial ouvert et à un modèle d’abonnement abordable et prévisible.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server sur Azure est une plateforme éprouvée qui offre une fiabilité et un niveau de sécurité supérieurs pour le cloud computing. Plate-forme de Linux de SUSE polyvalente s’intègre parfaitement avec Azure cloud services toodeliver un environnement cloud facilement gérables. Avec les applications certifiées 9,200 plus de plus de 1 800 éditeurs de logiciels indépendants pour SUSE Linux Enterprise Server, SUSE garantit que les charges de travail en cours d’exécution pris en charge dans le centre de données hello peuvent être déployés en toute confiance sur Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

L’ingénierie de Canonical et le mode de gouvernance de la communauté Open Source sont les éléments moteurs de la réussite d’Ubuntu dans les environnements client, serveur et cloud, y compris les services cloud personnels à destination du grand public. Vision de canoniques d’une plateforme unifiée, disponible sous Ubuntu, à partir du téléphone toocloud, fournit une gamme d’interfaces cohérents de hello phone, une tablette, TV et bureau. Cette vision rend Ubuntu hello premier choix pour diverses institutions décideurs de toohello de fournisseurs de cloud public de l’électronique du consommateur et un favori entre spécialistes individuels.

Les développeurs et les centres d’ingénierie Bonjour, canoniques est positionnée de manière unique toopartner avec le matériel, les fournisseurs de contenu et les logiciels aux développeurs toobring Ubuntu solutions toomarket pour les PC, serveurs et périphériques de poche.
