---
title: "aaaRed Infrastructure de mise à jour du fonctionnement (RHUI) | Documents Microsoft"
description: "Découvrez l’infrastructure RHUI (Red Hat Update Infrastructure) pour les instances Red Hat Enterprise Linux à la demande dans Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Infrastructure RHUI (Red Hat Update Infrastructure) pour machines virtuelles Red Hat Enterprise Linux à la demande dans Azure
Machines virtuelles créées à partir de hello sur demande Red Hat Enterprise Linux (RHEL) images disponibles dans Azure Marketplace sont inscrits tooaccess hello Red Hat mise à jour Infrastructure (RHUI) est déployé dans Azure.  les instances RHEL de demande Hello ont référentiel d’yum régionaux accès tooa et tooreceive en mesure des mises à jour incrémentielles.

liste des référentiels yum Hello, qui est gérée par RHUI, est configurée dans votre instance RHEL lors de la configuration. Vous n’avez pas besoin toodo aucune configuration supplémentaire - exécuter `yum update` une fois votre instance RHEL dernières mises à jour tooget prêt hello.

> [!NOTE]
> En septembre 2016, nous avons déployé une mise à jour RHUI d’Azure et en janvier 2017, nous avons commencé l’arrêt en plusieurs phases de hello plus anciens RHUI d’Azure. Si vous avez utilisé les images RHEL hello (ou leurs instantanés) à partir de septembre 2016 ou version ultérieure - probablement aucune action n’est requise. Si, toutefois, vous devez les anciens instantanés/VMs, leur configuration doit toobe mis à jour pour un accès ininterrompu toohello RHUI d’Azure.
> 

## <a name="rhui-azure-infrastructure-update"></a>Mise à jour de l’infrastructure RHUI Azure
Depuis septembre 2016, Azure propose un nouvel ensemble de serveurs d’infrastructure de mise à jour de Red Hat (RHUI). Ces serveurs sont déployés avec [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) de sorte qu’un simple point de terminaison (rhui-1.micrsoft.com) peut être utilisé par n’importe quelle machine virtuelle, quelle que soit la région. Hello nouvelles images de RHEL paiement à l’utilisation (retenues à la source) dans les nouveaux serveurs Azure RHUI de point toohello hello Azure Marketplace (versions datées de septembre 2016 ou version ultérieures) et ne nécessitent pas d’action supplémentaire.

### <a name="determine-if-action-is-required"></a>Déterminer si une action est requise
Si vous rencontrez des problèmes de connexion tooAzure RHUI à partir de votre machine virtuelle de Azure RHEL retenues à la source, procédez comme suit
1. Examen de la configuration de machine virtuelle pour le point de terminaison RHUI Azure

    Vérifiez si `/etc/yum.repos.d/rh-cloud.repo` fichier contient également les référence`rhui-[1-3].microsoft.com` dans baseurl de `[rhui-microsoft-azure-rhel*]` section du fichier de hello. Si elle est, vous utilisez hello nouvelle RHUI d’Azure.

    Si pointant tooa emplacement avec hello modèle `mirrorlist.*cds[1-4].cloudapp.net` -mise à jour de la configuration hello est requis.

    Si vous utilisez la nouvelle configuration de hello et toujours pas vous connecter tooAzure RHUI - fichier un cas de prise en charge par Microsoft ou Red Hat.

    > [!NOTE]
    > RHUI tooAzure hébergé d’accès est machines virtuelles de toohello limité dans [plages d’adresses IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Si hello ancien Azure RHUI est toujours disponible lorsque vous effectuez cette vérification et vous souhaitez que la configuration de hello tooautomatically mise à jour, exécutez hello de commande suivante :

    `sudo yum update RHEL6`ou `sudo yum update RHEL7` en fonction de la version de famille RHEL hello.

3. Si vous pouvez connecter n’est plus toohello ancien RHUI d’Azure, suivez hello manuelles décrites dans la section suivante de hello.

4. Assurez-vous que la configuration hello tooupdate hello source image/capture instantanée affectées de machine virtuelle a été configuré à partir de.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Arrêt en plusieurs phases de hello ancien Azure RHUI
Lors de l’arrêt de hello Hello ancien RHUI Azure nous restreindre accéder aux tooit comme suit :

1. Restreindre davantage le tooset d’accès (ACL) des adresses IP qui sont déjà connectés tooit. Effets possibles : Si vous continuez à l’aide de hello ancien Azure RHUI - vos nouvelles machines virtuelles ne peuvent pas être en mesure de tooconnect tooit. RHEL machines virtuelles avec des adresses IP dynamiques séquence d’arrêt/libérer/start reçoive la nouvelle adresse IP et donc également pu échouent tooconnect toohello ancien Azure RHUI

2. Arrêtez les serveurs de distribution du contenu de mise en miroir. Effets possibles : comme nous arrêter CDSes plus vous pouvez voir plus `yum update` la maintenance de temps, les délais d’attente plus jusqu’au hello point lorsque vous pourrez ne plus se connecter toohello ancien RHUI d’Azure.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Hello des adresses IP pour les nouveaux serveurs de diffusion de contenu RHUI hello sont
Si vous utilisez toofurther de configuration réseau restreindre l’accès à partir d’ordinateurs virtuels de RHEL retenues à la source, assurez-vous que hello suivant des adresses IP est autorisée pour `yum update` toowork en fonction de l’environnement hello dans. 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Mise à jour manuelle procédure toouse hello nouveaux Azure RHUI serveurs
Signature de clé publique de téléchargement (via curl) hello

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Vérifiez la clé de hello téléchargé

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Vérifiez la sortie de hello, vérifiez les `keyid` et `user ID packet`:

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

Installer la clé publique de hello

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Télécharger, vérifier et installer le package RPM Client

Télécharger : pour RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

pour RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Vérifier :

```bash
rpm -Kv azureclient.rpm
```

Vérifiez dans la sortie de cette signature de hello package est OK

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Installer hello tr/min

```bash
sudo rpm -U azureclient.rpm
```

À la fin, vérifiez que vous avez accès hello du formulaire Azure RHUI machine virtuelle

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>Script tout-en-un pour l’automatisation hello précédant la tâche
Utilisez hello script suivant en tant que tâche de hello tooautomate nécessaires de mise à jour des serveurs affectés Azure RHUI de nouveau toohello machines virtuelles.

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a>Vue d’ensemble de RHUI
[Infrastructure de mise à jour de Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) propose une solution hautement évolutive toomanage yum référentiel pour les instances de cloud de Red Hat Enterprise Linux qui sont hébergés par les fournisseurs de cloud de certifiés Red Hat. Selon le projet de pâtes hello en amont, RHUI permet aux fournisseurs cloud toolocally miroir hébergée de Red Hat du contenu de référentiel, créer des référentiels personnalisés avec leur propre contenu et rendre ces référentiels disponibles tooa grand groupe d’utilisateurs finaux via un équilibrage de la charge système de livraison de contenu.

## <a name="regions-where-rhui-is-available"></a>Régions où RHUI est disponible
L’infrastructure RHUI est disponible dans toutes les régions où les images RHEL à la demande sont disponibles. Elle comprend actuellement publiques toutes les régions répertoriées sur hello [tableau de bord Azure status](https://azure.microsoft.com/status/) page, les régions Azure du gouvernement et Azure situés en Allemagne. L’accès à l’infrastructure RHUI pour les machines virtuelles mises en service à partir d’images RHEL à la demande est inclus dans leur prix. Disponibilité du cloud régionales et nationales supplémentaire sera mise à jour en disponibilité à la demande RHEL Bonjour futures.

> [!NOTE]
> RHUI tooAzure hébergé d’accès est machines virtuelles de toohello limité dans [plages d’adresses IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Obtenir des mises à jour à partir d’un autre référentiel de mise à jour
Si vous avez besoin de mises à jour tooget à partir d’un référentiel autre mise à jour (au lieu de RHUI hébergés par Azure), vous devez toounregister vos instances de RHUI. Vous devez toore-s’inscrire avec l’infrastructure de mises à jour souhaitée hello (telles que Red Hat Satellite ou Red Hat Customer Portal CDN). Vous aurez besoin d’abonnements Red Hat appropriés pour ces services, et d’une inscription pour l’ [accès cloud Red Hat dans Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI et infrastructure de mise à jour réinscrivez tooyour, procédez comme suit :

1. Modifiez /etc/yum.repos.d/rh-cloud.repo et tous les `enabled=1` trop`enabled=0`. Par exemple :
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Modifiez /etc/yum/pluginconf.d/rhnplugin.conf et `enabled=0` trop`enabled=1`.
3. Inscrivez ensuite à l’infrastructure de votre choix de hello, comme portail des clients Red Hat. Suivez Red Hat guide de solution sur [comment tooregister et s’abonner à un toohello système portail des clients Red Hat](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Accès toohello RHUI de hébergés par Azure est inclus dans le prix d’image hello RHEL paiement à l’utilisation (retenues à la source). Annuler l’inscription d’une machine virtuelle RHEL de retenue à la source à partir de hello RHUI de hébergés par Azure ne convertit pas hello virtual machine dans le type Bring-Your-propre-licence (BYOL) machine virtuelle. Si vous inscrivez hello même machine virtuelle avec une autre source de mises à jour vous pouvez subir des frais doubles : la première fois des frais de logiciels Azure RHEL et hello deuxième fois pour les abonnements de Red Hat. 
> 
> Si vous devez régulièrement toouse une infrastructure de mise à jour autre que RHUI de hébergés par Azure envisagez de créer et déployer vos propres images (BYOL-type), comme décrit dans [créer et télécharger Red Hat-machine virtuelle pour Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) l’article.
> 

## <a name="next-steps"></a>Étapes suivantes
toocreate un ordinateur Red Hat Enterprise Linux virtuel à partir d’image de paiement à l’utilisation de Azure Marketplace et tirer parti de la RHUI de hébergés par Azure accédez trop[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Vous serez en mesure de toouse `yum update` dans votre instance RHEL sans toute configuration supplémentaire.

