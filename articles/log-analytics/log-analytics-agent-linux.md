---
title: "aaaConnect votre tooOperations d’ordinateurs Linux Management Suite (OMS) | Documents Microsoft"
description: "Cet article décrit comment tooconnect des ordinateurs Linux hébergés dans Azure, autres cloud ou tooOMS local à l’aide de hello Agent OMS pour Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Se connecter à votre tooOperations les ordinateurs Linux Management Suite (OMS) 

Avec Microsoft Operations Management Suite (OMS), vous pouvez collecter et agir sur les données générées à partir d’ordinateurs Linux et de solutions de conteneur telles que Docker, résidant dans votre centre de données local en tant que serveurs physiques ou virtuels, de machines virtuelles dans un service hébergé dans le cloud comme Amazon Web Services (AWS), ou de Microsoft Azure. Vous pouvez également utiliser des solutions de gestion disponibles dans OMS telles que le suivi des modifications, les modifications de configuration tooidentify, et gestion de la mise à jour toomanage logicielles mises à jour tooproactively gérer hello du cycle de vie de vos machines virtuelles Linux. 

Hello Agent OMS pour Linux communique sortant avec hello service OMS via le port TCP 443, et si les ordinateur hello connecte toocommunicate de serveur de pare-feu ou proxy tooa sur hello Internet, passez en revue [agent hello de configuration pour une utilisation avec un proxy HTTP serveur ou la passerelle d’OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand quelle configuration change devez toobe appliqué.  Si vous analysez un ordinateur hello avec System Center 2016 - Operations Manager ou Operations Manager 2012 R2, il peut être multirésident avec les données de toocollect du service OMS hello et service de transfert toohello et toujours être surveillée par Operations Manager.  Les ordinateurs Linux analysés par un groupe d’administration Operations Manager intégré à OMS ne reçoivent pas de configuration pour les sources de données et collecté avant les données via le groupe d’administration hello.  l’agent de Hello OMS ne peut pas être toomore tooreport configuré à un espace de travail.  

Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs sur votre toohello de tooconnect réseau Internet, l’agent de hello peut être configuré tooconnect toohello OMS passerelle tooreceive les informations de configuration et envoyer les données collectées en fonction de la solution hello qu'avoir activé. Pour plus d’informations sur comment tooconfigure votre toocommunicate OMS Linux Agent via un service OMS toohello de passerelle d’OMS, consultez [connecter tooOMS d’ordinateurs à l’aide de hello OMS passerelle](log-analytics-oms-gateway.md).  

Hello diagramme suivant décrit les connexions hello entre les ordinateurs gérés par agent Linux de hello et OMS, y compris les ports et la direction de hello.

![diagramme de communication directe entre l’agent et OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Conditions requises pour le système
Avant de commencer, passez en revue hello suivant tooverify détails préalables hello.

### <a name="supported-linux-operating-systems"></a>Systèmes d’exploitation Linux pris en charge
Hello suivant les distributions Linux est officiellement prises en charge.  Toutefois, hello Agent OMS pour Linux peut également s’exécuter sur les autres distributions non répertoriées.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 et 7 (x86/x64)
* Oracle Linux 5, 6 et 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 et 7 (x86/x64)
* Debian GNU/Linux 6, 7 et 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 et 12 (x86/x64)

### <a name="network"></a>Réseau
informations de Hello ci-dessous proxy hello de liste et les informations de configuration de pare-feu requises pour hello toocommunicate de l’agent Linux avec OMS. Le trafic est sortant à partir de votre service OMS toohello réseau. 

|Ressource de l'agent| Ports |  
|------|---------|  
|*.ods.opinsights.azure.com | Port 443|   
|*.oms.opinsights.azure.com | Port 443|   
|*.blob.core.windows.net/ | Port 443|   
|*.azure-automation.net | Port 443|  

### <a name="package-requirements"></a>Packages requis

 **Package requis**   | **Description**   | **Version minimum**
--------------------- | --------------------- | -------------------
Glibc | Bibliothèque C de GNU   | 2.5-12 
Openssl | Bibliothèques OpenSSL | 0.9.8e ou 1.0
Curl | Client web cURL | 7.15.5
Python-ctypes | | 
PAM | Pluggable Authentication Modules | 

> [!NOTE]
>  Rsyslog ou syslog-ng est des messages syslog toocollect requis. démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog. toocollect les données syslog de cette version de ces distributions, hello rsyslog doit être installé et configuré tooreplace sysklog, le démon 

l’agent de Hello comprend plusieurs packages. fichier de la version Hello contient hello suivant des packages, disponibles en cours d’exécution offre groupée du noyau hello avec `--extract`:

**Package** | **Version** | **Description**
----------- | ----------- | --------------
omsagent | 1.4.0 | Hello Operations Management Suite Agent pour Linux
omsconfig | 1.1.1 | Agent de configuration pour hello Agent OMS
omi | 1.2.0 | Open Management Infrastructure (OMI) - Serveur CIM léger
scx | 1.6.3 | Fournisseurs CIM OMI pour les mesures de performances des systèmes d’exploitation
apache-cimprov | 1.0.1 | Fournisseur de surveillance des performances d’Apache HTTP Server pour OMI. Installé si Apache HTTP Server est détecté.
mysql-cimprov | 1.0.1 | Fournisseur de surveillance des performances de MySQL Server pour OMI. Installé si MySQL/MariaDB Server est détecté.
docker-cimprov | 1.0.0 | Fournisseur de Docker pour OMI. Installé si Docker est détecté.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibilité avec System Center Operations Manager
Hello Agent OMS pour Linux partage des fichiers binaires avec l’agent de System Center Operations Manager hello. Si vous installez hello Agent OMS pour Linux sur un système actuellement géré par Operations Manager, il hello packages OMI et SCX sur une version plus récente de hello ordinateur tooa. Dans cette version, de hello OMS et de System Center 2016 - agents d’Operations Manager/Operations Manager 2012 R2 pour Linux sont compatibles. 

> [!NOTE]
> System Center 2012 SP1 et les versions antérieures sont actuellement pas compatibles ni prises en charge par hello Agent OMS pour Linux.<br>
> Si hello Agent OMS pour Linux est installé tooa ordinateur qui n’est pas actuellement analysé par Operations Manager et que vous souhaitez puis toomonitor hello équipé d’Operations Manager, vous devez modifier hello [configuration OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) préalable ordinateur de hello toodiscovering. **Cette étape est *pas* nécessaire si l’agent Operations Manager de hello est installé avant hello Agent OMS pour Linux.**

### <a name="system-configuration-changes"></a>Modifications de configuration système
Après avoir installé hello Agent OMS pour les packages Linux, hello les modifications de système de configuration supplémentaires suivantes sont appliquées. Ces artefacts sont supprimés lors de la désinstallation du package omsagent hello.

* Un utilisateur sans privilège nommé `omsagent` est créé. Il s’agit de hello compte hello omsagent démon l’exécution.
* Un fichier « include » de sudoers est créé à l’emplacement /etc/sudoers.d/omsagent. Ce qui autorise omsagent toorestart hello syslog et omsagent démons. Si les directives « include » de sudo ne sont pas pris en charge dans la version installée de hello de sudo, ces entrées sont écrites trop/etc/programmes sudo.
* configuration de syslog Hello est modifié tooforward un sous-ensemble de l’agent de toohello d’événements. Pour plus d’informations, consultez hello **collecte des données de configuration de** section ci-dessous

### <a name="upgrade-from-a-previous-release"></a>Mettre à niveau à partir d’une version antérieure
La mise à niveau à partir de versions antérieures à 1.0.0-47 est prise en charge dans cette version. Exécution d’installation hello avec hello `--upgrade` commande met à niveau tous les composants de la version la plus récente toohello agent hello.

## <a name="installing-hello-agent"></a>Installation de l’agent hello

Cette section décrit comment tooinstall hello Agent OMS pour Linux à l’aide d’un bunndle, qui contient les Debian et RPM packages pour chacun des composants de l’agent hello.  Il peut être installé directement ou extrait des packages individuels tooretrieve hello.  

Tout d’abord vous avez besoin de votre ID d’espace de travail OMS et la clé, ce qui se trouve en basculant toohello [portail classique OMS](https://mms.microsoft.com).  Sur hello **vue d’ensemble** page, à partir de la sélection de menu du haut hello **paramètres**, puis accédez trop**Sources\Linux serveurs**.  Vous consultez hello valeur toohello droite **ID de l’espace de travail** et **clé primaire**.  Copiez-collez ces deux valeurs dans votre éditeur favori.    

1. Hello téléchargement dernières [Agent OMS pour Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) ou [Agent OMS pour Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) à partir de GitHub.  
2. Transfert de hello bundle approprié (x86 ou x64) tooyour ordinateur Linux à l’aide de scp/sftp.
3. Regroupement de hello installation à l’aide de hello `--install` ou `--upgrade` argument. 

    > [!NOTE]
    > Si des packages existants sont installés comme lorsque hello System Center Operations Manager agent pour Linux est déjà installé, utilisez hello `--upgrade` argument. tooconnect tooOperations Management Suite pendant l’installation, fournissez hello `-w <WorkspaceID>` et `-s <Shared Key>` paramètres.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall et s’intégrer directement
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>package de l’agent hello tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall et espace de travail tooa intégré dans le Cloud de US Government
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Configuration d’agent hello pour une utilisation avec un serveur proxy HTTP ou d’une passerelle d’OMS
Hello Agent OMS pour Linux prend en charge la communication via un serveur proxy HTTP ou HTTPS ou le service de passerelle de OMS toohello OMS.  L’authentification anonyme et l’authentification de base (nom d’utilisateur/mot de passe) sont prises en charge.  

### <a name="proxy-configuration"></a>Configuration du proxy
valeur de configuration de proxy Hello a hello selon la syntaxe :

`[protocol://][user:password@]proxyhost[:port]`

Propriété|Description
-|-
Protocole|http ou https
user|Nom d’utilisateur facultatif pour l’authentification du proxy
password|Mot de passe facultatif pour l’authentification du proxy
proxyhost|Adresse ou le nom de domaine complet de hello proxy server/OMS passerelle
port|Numéro de port facultatif pour hello proxy server/OMS passerelle

Par exemple : `http://user01:password@proxy01.contoso.com:8080`

serveur de proxy Hello peut être spécifié lors de l’installation ou en modifiant le fichier de configuration proxy.conf hello après l’installation.   

### <a name="specify-proxy-configuration-during-installation"></a>Spécifier la configuration du serveur proxy lors de l’installation
Hello `-p` ou `--proxy` argument pour l’installation du bundle omsagent installation hello spécifie toouse de configuration de proxy hello. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Définir la configuration du proxy hello dans un fichier
configuration du proxy Hello peut être définie dans les fichiers hello `/etc/opt/microsoft/omsagent/proxy.conf` et `/etc/opt/microsoft/omsagent/conf/proxy.conf `. les fichiers Hello peuvent être créées ou modifiées directement, mais leurs autorisations doivent être utilisateur d’omiuser hello toogrant mis à jour en lecture sur les fichiers de hello. Par exemple :
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Suppression de la configuration proxy hello
tooremove une configuration de proxy précédemment défini et rétablir la connectivité de toodirect, supprimez le fichier de proxy.conf hello :
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Intégration avec Operations Management Suite
Si un ID de l’espace de travail et une clé n’ont pas été fournies pendant l’installation du bundle hello, l’agent de hello doit être inscrit par la suite avec Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Intégration à l’aide de la ligne de commande hello
Exécuter la commande omsadmin.sh de hello fournissant l’id d’espace de travail hello et la clé pour votre espace de travail. Cette commande doit être exécutée en tant que root (avec élévation des droits sudo) :
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Intégration à l’aide d’un fichier
1.  Créer le fichier de hello `/etc/omsagent-onboard.conf`. fichier de Hello doit être accessible en lecture et en écriture pour la racine.
`sudo vi /etc/omsagent-onboard.conf`
2.  Insérez hello lignes dans le fichier de hello avec votre ID d’espace de travail et la clé partagée suivantes :

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Exécutez hello suivant tooOMS tooOnboard de commande :`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  fichier de Hello est supprimé sur la réussite de l’intégration.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Activer hello Agent OMS pour Linux tooreport tooSystem Center Operations Manager
Effectuer hello suivant les étapes tooconfigure hello Agent OMS pour le groupe d’administration Linux tooreport tooa System Center Operations Manager.  

1. Modifier le fichier de hello`/etc/opt/omi/conf/omiserver.conf`
2. Vérifiez que hello ligne commençant par **httpsport =** définit le port 1270 hello. Par exemple : `httpsport=1270`
3. Redémarrez le serveur OMI de hello :`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Journaux de l’agent
Hello journaux des hello Agent OMS pour Linux se trouvent à : `/var/opt/microsoft/omsagent/<workspace id>/log/` hello journaux pour le programme omsconfig (configuration de l’agent) de hello se trouve à : `/var/opt/microsoft/omsconfig/log/` les journaux des composants OMI et SCX hello (qui fournissent les données de métriques de performances), consultez :`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Configuration de rotation des journaux##
configuration de faire pivoter des journaux Hello pour omsagent peut se trouve à :`/etc/logrotate.d/omsagent-<workspace id>`

Hello par défaut sont les suivantes : 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Désinstallation de hello Agent OMS pour Linux
Hello packages d’agent peuvent être désinstallés par fichier .sh du bundle hello en cours d’exécution avec hello `--purge` argument, ce qui supprime complètement l’agent de hello et sa configuration à partir de l’ordinateur de hello.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Problème : Les tooconnect impossible via proxy tooOMS

#### <a name="probable-causes"></a>Causes probables
* proxy Hello spécifié lors de l’intégration est incorrect
* points de terminaison de Service Hello OMS ne sont pas whitelistested dans votre centre de données 

#### <a name="resolutions"></a>Résolutions
1. Reonboard toohello Service OMS avec hello Agent OMS pour Linux à l’aide de hello suivant de commande avec l’option de hello `-v` activé. Ainsi, la sortie des commentaires de l’agent de hello qui se connectent via hello proxy toohello Service OMS. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Passez en revue la section de hello [agent hello de configuration pour une utilisation avec un proxy HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify que vous avez correctement configuré hello toocommunicate agent via un serveur proxy.    
* Vérifiez que hello suivant les points de terminaison de Service OMS sont autorisés :

    |Ressource de l'agent| Ports |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Port 443|   
    |*.oms.opinsights.azure.com | Port 443|   
    |ods.systemcenteradvisor.com | Port 443|   
    |*.blob.core.windows.net/ | Port 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Problème : Vous recevez une erreur 403 lors de la tentative de tooonboard

#### <a name="probable-causes"></a>Causes probables
* La date et l’heure sont incorrectes sur le serveur Linux 
* L’ID et la clé d’espace de travail utilisés sont incorrects

#### <a name="resolution"></a>Résolution :

1. Vérifie hello sur votre serveur Linux avec la date de commande hello. Si l’heure de hello est + et-15 minutes à partir de l’heure actuelle, l’intégration échoue. toocorrect cette mise à jour hello date et/ou le fuseau horaire de votre serveur Linux. 
2. Vérifiez que vous avez installé hello dernière version de hello Agent OMS pour Linux.  version la plus récente Hello vous avertit désormais si décalage horaire est entraînent l’échec de l’intégration de hello.
3. Reonboard à l’aide de correct ID et la clé d’espace de travail suivant les instructions d’installation hello plus haut dans cette rubrique.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Problème : Vous voyez une erreur 500 et 404 dans le fichier journal de hello juste après l’intégration
Il s’agit d’un problème connu qui se produit lors du premier chargement de données Linux dans un espace de travail OMS. Cela n’affecte pas les données envoyées ni l’expérience du service.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Problème : Vous ne voyez pas toutes les données dans le portail OMS de hello

#### <a name="probable-causes"></a>Causes probables

- Échec de l’intégration toohello Service OMS
- Connexion toohello Service OMS est bloquée.
- Les données de l’Agent OMS pour Linux sont sauvegardées

#### <a name="resolutions"></a>Résolutions
1. Vérifiez si l’intégration hello Service OMS a réussi en vérifiant si hello existence des fichiers suivants :`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard à l’aide de hello `omsadmin.sh` obtenir des instructions de ligne de commande
3. Si vous utilisez un proxy, consultez étapes de résolution toohello proxy fournis précédemment.
4. Dans certains cas, lorsque hello Agent OMS pour Linux ne peuvent pas communiquer avec hello Service OMS, les données sur l’agent de hello sont taille de mémoire tampon saturée toohello en file d’attente, qui est de 50 Mo. Hello Agent OMS pour Linux doit être redémarré en exécutant hello de commande suivante : `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Ce problème est résolu dans l’agent version 1.1.0-28 et versions ultérieures.
> 