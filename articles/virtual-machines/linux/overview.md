---
title: aaaOverview de machines virtuelles de Linux dans Azure | Documents Microsoft
description: "Décrit les services de calcul, de stockage et de mise en réseau Azure à l’aide de machines virtuelles Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure et Linux
Microsoft Azure propose une gamme croissante de services cloud publics intégrés, comprenant des analyses, des machines virtuelles, des bases de données, des services mobiles, la mise en réseau, le stockage et le web.&mdash;En d’autres termes, il s’agit de la méthode idéale pour héberger vos solutions.  Microsoft Azure offre une plateforme informatique évolutive qui vous permet de payer tooonly ce que vous utilisez, lorsque vous le souhaitez, sans avoir tooinvest dans le matériel sur site.  Azure est prêt tooscale vos solutions haut et à l’échelle de toowhatever vous avez besoin de besoins de hello tooservice de vos clients.

Si vous êtes familiarisé avec hello diverses fonctionnalités de Amazon AWS, vous pouvez examiner hello vs Azure AWS [document de définition de mappage](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Régions
Ressources Microsoft Azure sont réparties sur plusieurs régions géographiques monde hello.  Une « région » représente plusieurs centres de données au sein d’une seule zone géographique.  Nous avons 34 régions sont généralement disponibles monde hello avec un autres régions 4 annoncé. Étant donné que nous allons continuer tooexpand notre couverture global - nous mettons en place qu'une liste de mises à jour existante et récemment annoncé régions.

* [Régions Azure](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Disponibilité
Nous avons annoncé qu'une machine début seule instance virtuelle industrie contrat SLA de 99,9 % fourni que vous déployez hello machine virtuelle avec le stockage de tous les disques premium.  Dans l’ordre pour votre tooqualify de déploiement pour notre standard 99,95 % contrat de niveau de Service de machine virtuelle, vous devez toujours toodeploy deux ou plusieurs machines virtuelles sont en cours d’exécution votre charge de travail à l’intérieur d’un ensemble de disponibilité. Ainsi, vos machines virtuelles sont réparties sur plusieurs domaines d’erreur dans nos centres de données et déployées sur des hôtes ayant des fenêtres de maintenance distinctes. Hello complète [contrat SLA Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) explique hello garantie de disponibilité de Azure dans sa globalité.

## <a name="managed-disks"></a>Managed Disks

Des poignées de stockage Azure compte création et la gestion en arrière-plan de hello pour vous et permet de s’assurer que vous n’avez pas tooworry sur les limites d’extensibilité hello hello du compte de stockage de disques gérés par. Vous spécifiez simplement taille du disque hello et niveau de performance hello (Standard ou Premium) et Azure crée et gère les disques de hello pour vous. Même lorsque vous ajoutez des disques ou évoluer hello machine virtuelle, vous n’avez tooworry sur le stockage hello utilisé. Si vous créez de nouvelles machines virtuelles, [utiliser hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou hello toocreate portail Azure machines virtuelles avec des disques gérés du système d’exploitation et des données. Si vous avez des machines virtuelles avec des disques non managés, vous pouvez [convertir votre toobe de machines virtuelles sauvegardée avec disques gérés](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Vous pouvez également gérer vos images personnalisées dans un compte de stockage par région Azure et les utiliser toocreate des centaines d’ordinateurs virtuels dans hello même abonnement. Pour plus d’informations sur les disques gérés, consultez hello [vue d’ensemble de disques gérés](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Machines virtuelles et instances Azure
Microsoft Azure prend en charge un certain nombre de distributions Linux populaires fournies et gérées par plusieurs partenaires.  Vous trouverez des distributions telles que Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD et bien plus encore Bonjour Azure Marketplace. Nous activement travailler avec tooadd de communautés Linux différentes versions encore plus toohello [Azure approuvée Distros de Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) liste.

Si votre distributeur Linux préféré de choix n’est pas actuellement présent dans la galerie de hello, vous pouvez « apportez votre propre Linux » VM par [création et téléchargement d’un VHD Linux dans Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Machines virtuelles vous permettent de toodeploy une large gamme de solutions informatiques d’une manière agile. Vous pouvez déployer pratiquement toute charge de travail et tout langage sur presque n’importe quel système d’exploitation : Windows, Linux ou un système personnalisé créé à partir de l’un de nos nombreux partenaires. Vous ne trouvez toujours pas ce que vous cherchez ?  Ne vous inquiétez pas, vous pouvez également ajouter vos propres images en local.

## <a name="vm-sizes"></a>Tailles de machine virtuelle
Lorsque vous déployez une machine virtuelle dans Azure, vous allez tooselect une taille de machine virtuelle au sein de notre série de tailles qui est la charge de travail tooyour approprié. taille de Hello affecte également hello capacité de stockage de l’ordinateur virtuel de hello, la mémoire et la puissance de traitement. Vous êtes facturé selon la quantité hello Hello de temps machine virtuelle est en cours d’exécution et la consommation ses ressources allouées. La liste complète des [tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Voici quelques conseils de base pour la sélection d’une taille de machine virtuelle parmi nos séries (A, D, DS, G et GS).
* Les machines virtuelles de série A sont des machines virtuelles d’entrée de gamme offrant un bon rapport qualité/prix et qui conviennent pour des charges de travail légères et des scénarios de développement/test. Elles sont largement disponibles dans toutes les régions et peuvent se connecter et utiliser tous les ordinateurs disponibles toovirtual de ressources standard.
* Les tailles de série A (A8 - A11) sont des configurations spéciales de calcul intensif adaptées aux applications de cluster informatique à hautes performances.
* Machines virtuelles de série D sont conçues toorun les applications qui exigent une puissance de calcul et de performances de disque temporaire. Machines virtuelles de série D fournissent des processeurs plus rapides, un taux de mémoire-cœur plus élevé et un disque SSD (SSD) pour le disque temporaire de hello.
* Série Dv2, est la version la plus récente hello de notre série D, doté d’un processeur plus puissant. Hello série Dv2 processeur est d’environ 35 % plus rapide que hello série D à l’UC. Il est basé sur hello dernière génération 2,4 GHz Intel Xeon® E5-2673 v3 (Haskell), processeur et avec hello 2.0 de la technologie Intel Turbo Boost, peuvent atteindre la too3.2 GHz. Hello Dv2 série a hello les mêmes configurations de mémoire et de disque comme hello série D.
* Machines virtuelles de série G offrent hello plus de mémoire et s’exécuter sur les ordinateurs hôtes qui ont des processeurs de la famille Intel Xeon E5 V3.

Remarque : La série DS et les machines virtuelles de série GS ont accès tooPremium stockage - notre SSD sauvegardé stockage hautes performances et à faible latence pour les charges de travail intensives d’e/s. Le stockage Premium est disponible dans certaines régions. Pour plus d'informations, consultez les rubriques :

* [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure.](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automatisation
tooachieve une culture DevOps appropriée, toute infrastructure doit être le code.  Lorsque tous les hello infrastructure vie dans le code, il peut être facilement recréées (Phoenix serveurs).  Azure fonctionne avec tous les automation principales hello pour les outils comme Ansible, Chef, SaltStack et Puppet.  Azure propose également ses propres outils pour l’automatisation :

* [Modèles Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure déploie la prise en charge de [cloud-init](http://cloud-init.io/) sur la plupart des distributions Linux qui le prennent en charge.  Actuellement, les machines virtuelles Ubuntu de Canonical sont déployées avec cloud-init activé par défaut.  Fedora prennent en charge le cloud-init, toutefois hello Azure, CentOS et Red chapeaux RHEL images maintenus par RedHat n’ont pas de cloud-init est installé.  toouse init cloud sur une système d’exploitation de la famille RedHat, vous devez créer une image personnalisée avec le cloud-init est installé.

* [À l’aide de cloud-init sur les machines virtuelles Linux Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Quotas
Chaque abonnement Azure a des limites de quota par défaut en place qui pourrait avoir un impact sur déploiement hello d’un grand nombre d’ordinateurs virtuels pour votre projet. limite actuelle de Hello par abonnement est 20 ordinateurs virtuels par région.  Les limites de quota peuvent être augmentées rapidement et facilement en soumettant un ticket de support demandant leur hausse.  Pour plus d’informations sur les limites de quota :

* [Limites du service d’abonnement Azure](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Partenaires
Microsoft travaille en étroite collaboration avec nos partenaires, les images de hello tooensure disponibles sont mis à jour et optimisés pour une exécution Azure.  Pour plus d’informations sur nos partenaires, consultez leurs pages sur la place de marché ci-dessous.

* Linux sur Azure : [Distributions approuvées](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE : [Place de marché Azure - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Redhat - [Place de marché Azure - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical - [Place de marché Azure - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Place de marché Azure - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Place de marché Azure - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [Place de marché Azure - CoreOS (Stable)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Place de marché Azure - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Bitnami Library pour Azure](https://azure.bitnami.com/)
* Mesosphere - [Place de marché Azure - Mesosphere DC/OS sur Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Place de marché Azure - Azure Container Service avec Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Place de marché Azure - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Bien démarrer avec Linux sur Azure
toobegin à l’aide d’Azure, vous avez besoin d’un compte Azure, hello CLI d’Azure installé et une paire de clés publiques et privées de SSH.

### <a name="sign-up-for-an-account"></a>Inscrivez-vous pour obtenir un compte
Hello première étape à l’aide de hello Azure Cloud est toosign pour un compte Azure.  Accédez toohello [inscription à Azure](https://azure.microsoft.com/pricing/free-trial/) page tooget a démarré.

### <a name="install-hello-cli"></a>Installer hello CLI
Avec votre nouveau compte Azure, vous pouvez commencer immédiatement à l’aide de hello portail Azure, qui est un panneau de l’administration basée sur le web.  toomanage hello Azure Cloud via hello de ligne de commande, vous installez hello `azure-cli`.  Installer hello [Azure CLI 2.0](/cli/azure/install-azure-cli) sur votre station de travail Mac ou Linux.

### <a name="create-an-ssh-key-pair"></a>Création d’une paire de clés SSH
Maintenant, vous avez un compte Azure, hello Azure portail web et hello CLI d’Azure.  étape suivante de Hello est toocreate une paire de clés SSH est tooSSH utilisé dans Linux sans utiliser un mot de passe.  [Créer des clés SSH sur Mac et Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable les connexions sans mot de passe et une meilleure sécurité.

### <a name="create-a-vm-using-hello-cli"></a>Créer une machine virtuelle à l’aide de hello CLI
Création d’un VM Linux à l’aide de hello CLI est un toodeploy rapidement une machine virtuelle sans quitter hello terminal dans que vous travaillez.  Tout ce dont vous pouvez spécifier sur le portail web hello est disponible via un commutateur ou un indicateur de ligne de commande.  

* [Créer une VM Linux à l’aide de hello CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Créer une machine virtuelle dans le portail de hello
Créer une VM Linux dans le portail web Azure de hello est un moyen tooeasily point puis cliquez sur hello déploiement tooa de tooget différentes options.  Au lieu d’utiliser des commutateurs ou des indicateurs de ligne de commande, vous êtes en mesure de tooview une mise en page web intéressant de différentes options et paramètres.  Tous les éléments disponibles via une interface de ligne hello est également disponible dans le portail de hello.

* [Créer une VM Linux à l’aide de hello portail](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Connexion avec SSH sans mot de passe
Hello machine virtuelle est en cours d’exécution sur Azure et vous êtes prêt toolog dans.  À l’aide de toolog les mots de passe dans via une connexion SSH est non sécurisé et beaucoup de temps.  À l’aide de clés SSH est hello plus sûre et également toologin moyen le plus rapide de hello.  Lorsque vous créez Linux VM via le portail de hello ou hello CLI, vous avez deux possibilités d’authentification.  Si vous choisissez un mot de passe pour SSH, Azure configure les connexions de tooallow hello machine virtuelle via les mots de passe.  Si vous avez choisi toouse une clé publique SSH, Azure configure hello VM tooonly autoriser les connexions via le protocole SSH clés et désactive les connexions de mot de passe. toosecure votre VM Linux par uniquement ce qui permet des connexions à des clés SSH, utilisez hello option clée publique SSH lors de la création d’ordinateurs virtuels dans le portail de hello ou l’interface CLI de hello.

## <a name="related-azure-components"></a>Composants Azure connexes
## <a name="storage"></a>Storage
* [Introduction tooMicrosoft stockage Azure](../../storage/common/storage-introduction.md)
* [Ajouter un tooa disque VM Linux à l’aide d’azure hello-cli](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tooattach données de disque tooa Linux VM Bonjour portail Azure](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Mise en réseau
* [Présentation du réseau virtuel.](../../virtual-network/virtual-networks-overview.md)
* [Adresses IP dans Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Ouverture des ports tooa Linux VM dans Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Créer un nom de domaine complet dans hello portail Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Conteneurs
* [Machines virtuelles et conteneurs dans Azure](containers.md)
* [Présentation d’Azure Container Service](../../container-service/container-service-intro.md)
* [Déploiement d’un cluster Azure Container Service](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Étapes suivantes
Vous avez maintenant une vue d’ensemble de Linux sur Azure.  étape suivante de Hello est toodive dans et créer quelques machines virtuelles !

* [Explorez notre liste croissante d’exemples de scripts pour les tâches courantes via AzureCLI](cli-samples.md)
