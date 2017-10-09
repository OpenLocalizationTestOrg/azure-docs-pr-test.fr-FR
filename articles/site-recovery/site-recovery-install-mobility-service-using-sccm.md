---
title: "installation du Service mobilité pour Azure Site Recovery à l’aide des outils de déploiement de logiciels d’aaaAutomate | Documents Microsoft"
description: "Cet article vous aide à automatiser l’installation du service Mobilité à l’aide d’outils de déploiement de logiciels tels que System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>Automatisation de l’installation du service Mobilité à l’aide d’outils de déploiement de logiciels

>[!IMPORTANT]
Ce document part du principe que vous utilisez la version **9.9.4510.1** ou ultérieure.

Cet article fournit un exemple de la façon dont vous pouvez utiliser System Center Configuration Manager toodeploy hello Service de mobilité d’Azure Site Recovery dans votre centre de données. À l’aide d’un outil de déploiement de logiciel tel que le Gestionnaire de Configuration a hello suivant avantages :
* Planification du déploiement (nouvelles installations et mises à niveau) pendant votre fenêtre de maintenance planifiée pour les mises à jour logicielles
* Mise à l’échelle toohundreds de déploiement de serveurs simultanément


> [!NOTE]
> Cet article utilise l’activité de déploiement de System Center Configuration Manager 2012 R2 toodemonstrate hello. Vous pouvez également automatiser l’installation du service Mobilité à l’aide [d’Azure Automation et de la Configuration de l’état souhaité](site-recovery-automate-mobility-service-install.md).

## <a name="prerequisites"></a>Conditions préalables
1. Un outil de déploiement de logiciels tel que Configuration Manager qui est déjà déployé dans votre environnement.
  Créez deux [regroupements de périphériques](https://technet.microsoft.com/library/gg682169.aspx), un pour tous les **serveurs Windows**et l’autre pour toutes les **des serveurs Linux**, que vous souhaitez tooprotect à l’aide de récupération de Site.
3. Un serveur de configuration qui est déjà inscrit auprès Site Recovery.
4. Un réseau sécurisé partage de fichiers (partage Server Message Block) qui sont accessibles par le serveur de Configuration Manager hello.

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Déploiement du service Mobilité sur des ordinateurs exécutant Windows
> [!NOTE]
> Cet article suppose qu’adresse hello hello du serveur de configuration est 192.168.3.121, et que ce partage de fichiers réseau sécurisé hello est \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Étape 1 : Préparation du déploiement
1. Créez un dossier sur un partage de réseau hello et nommez-le **MobSvcWindows**.
2. Connectez-vous au serveur de configuration tooyour et ouvrez une invite de commandes d’administration.
3. Exécutez hello suivant de commandes toogenerate un fichier de mot de passe :

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Hello de copie **MobSvc.passphrase** fichier hello **MobSvcWindows** dossier sur votre partage réseau.
5. Parcourir le référentiel du programme d’installation toohello sur le serveur de configuration hello en exécutant hello de commande suivante :

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Hello de copie  **Microsoft ASR\_UA\_*version*\_Windows\_GA\_*date* \_ Release.exe** toohello **MobSvcWindows** dossier sur votre partage réseau.
7. Copier hello suivant de code et l’enregistrer en tant que **install.bat** dans hello **MobSvcWindows** dossier.

   > [!NOTE]
   > Remplacez les espaces réservés de hello [CSIP] dans ce script avec des valeurs réelles de hello d’adresse IP de hello de votre serveur de configuration.

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a>Étape 2 : Création d’un package

1. Se connecter dans la console Configuration Manager tooyour.
2. Parcourir trop**bibliothèque de logiciels** > **gestion des applications** > **Packages**.
3. Cliquez avec le bouton droit sur **Packages** et sélectionnez **Créer un package**.
4. Fournir des valeurs pour la version, la description, fabricant, langue et nom de hello.
5. Sélectionnez hello **ce package contient des fichiers sources** case à cocher.
6. Cliquez sur **Parcourir**et sélectionnez hello partage de réseau où se trouve le programme d’installation de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. Sur hello **type de programme hello choisir que vous souhaitez toocreate** page, sélectionnez **programme Standard**, puis cliquez sur **suivant**.

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Sur hello **spécifier des informations sur ce programme standard** page, fournissez hello suivant des entrées, puis cliquez sur **suivant**. (hello autres entrées peuvent utiliser leurs valeurs par défaut.)

  | **Nom du paramètre** | **Valeur** |
  |--|--|
  | Nom | Installer le service Mobilité de Microsoft Azure (Windows) |
  | Ligne de commande | install.bat |
  | Le programme peut s’exécuter | Qu’un utilisateur ait ouvert une session ou non |

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. Sur la page suivante de hello, sélectionnez les systèmes d’exploitation cible hello. Le service Mobilité ne peut être installé que sur Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2.

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. Assistant de hello toocomplete, cliquez sur **suivant** à deux reprises.


> [!NOTE]
> script de Hello prend en charge les nouvelles installations d’agents de Service mobilité et met à jour tooagents qui sont déjà installés.

### <a name="step-3-deploy-hello-package"></a>Étape 3 : Déployer le package de hello
1. Dans la console Configuration Manager hello, avec le bouton droit de votre package, puis sélectionnez **distribuer du contenu**.
  ![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Sélectionnez hello  **[les points de distribution](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  sur toowhich les packages hello doivent être copiés.
3. Assistant hello terminée. package de Hello puis le démarrage de la réplication toohello spécifié de points de distribution.
4. Une fois que la distribution de package hello est terminée, cliquez sur le package de hello, puis sélectionnez **déployer**.
  ![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Sélectionnez le regroupement de périphériques Windows Server hello que vous avez créé dans la section conditions préalables de hello en tant que regroupement cible de hello pour le déploiement.

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. Sur hello **spécifier la destination de contenu hello** page, sélectionnez votre **les Points de Distribution**.
7. Sur hello **toocontrol de paramètres de spécifier comment ce logiciel est déployé** , vérifiez que hello vise **requis**.

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Sur hello **spécifier la planification pour ce déploiement hello** , spécifiez une planification. Pour plus d’informations, consultez [Planification de packages](https://technet.microsoft.com/library/gg682178.aspx).
9. Sur hello **les Points de Distribution** page, configurez les propriétés de hello selon les besoins de toohello de votre centre de données. Puis terminer hello.

> [!TIP]
> tooavoid inutile a redémarré, planifier l’installation package hello pendant votre fenêtre de maintenance mensuelle ou d’une fenêtre de mises à jour logicielles.

Vous pouvez surveiller la progression du déploiement hello en utilisant la console de Configuration Manager hello. Accédez trop**analyse** > **déploiements** > *[nom de votre package]*.

  ![Déploiements de toomonitor option de capture d’écran de Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Déploiement du service Mobilité sur des ordinateurs exécutant Linux
> [!NOTE]
> Cet article suppose qu’adresse hello hello du serveur de configuration est 192.168.3.121, et que ce partage de fichiers réseau sécurisé hello est \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Étape 1 : Préparation du déploiement
1. Créez un dossier sur un partage de réseau hello et nommez-le en tant que **MobSvcLinux**.
2. Connectez-vous au serveur de configuration tooyour et ouvrez une invite de commandes d’administration.
3. Exécutez hello suivant de commandes toogenerate un fichier de mot de passe :

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Hello de copie **MobSvc.passphrase** fichier hello **MobSvcLinux** dossier sur votre partage réseau.
5. Parcourir le référentiel du programme d’installation toohello sur le serveur de configuration hello en exécutant la commande hello :

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Suit hello de copie des fichiers toohello **MobSvcLinux** dossier sur votre partage réseau :
   * Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz
   * Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz
   * Microsoft-ASR\_UA\*OL6-64\*release.tar.gz
   * Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz


7. Copier hello suivant de code et l’enregistrer en tant que **install_linux.sh** dans hello **MobSvcLinux** dossier.
   > [!NOTE]
   > Remplacez les espaces réservés de hello [CSIP] dans ce script avec des valeurs réelles de hello d’adresse IP de hello de votre serveur de configuration.

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a>Étape 2 : Création d’un package

1. Se connecter dans la console Configuration Manager tooyour.
2. Parcourir trop**bibliothèque de logiciels** > **gestion des applications** > **Packages**.
3. Cliquez avec le bouton droit sur **Packages** et sélectionnez **Créer un package**.
4. Fournir des valeurs pour la version, la description, fabricant, langue et nom de hello.
5. Sélectionnez hello **ce package contient des fichiers sources** case à cocher.
6. Cliquez sur **Parcourir**et sélectionnez hello partage de réseau où se trouve le programme d’installation de hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. Sur hello **type de programme hello choisir que vous souhaitez toocreate** page, sélectionnez **programme Standard**, puis cliquez sur **suivant**.

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Sur hello **spécifier des informations sur ce programme standard** page, fournissez hello suivant des entrées, puis cliquez sur **suivant**. (hello autres entrées peuvent utiliser leurs valeurs par défaut.)

    | **Nom du paramètre** | **Valeur** |
  |--|--|
  | Nom | Installer le service Mobilité de Microsoft Azure (Linux) |
  | Ligne de commande | ./install_linux.sh |
  | Le programme peut s’exécuter | Qu’un utilisateur ait ouvert une session ou non |

  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. Sur la page suivante de hello, sélectionnez **ce programme peut s’exécuter sur n’importe quelle plateforme**.
  ![Capture d’écran de l’assistant Création d’un package et d’un programme](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. Assistant de hello toocomplete, cliquez sur **suivant** à deux reprises.

> [!NOTE]
> script de Hello prend en charge les nouvelles installations d’agents de Service mobilité et met à jour tooagents qui sont déjà installés.

### <a name="step-3-deploy-hello-package"></a>Étape 3 : Déployer le package de hello
1. Dans la console Configuration Manager hello, avec le bouton droit de votre package, puis sélectionnez **distribuer du contenu**.
  ![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Sélectionnez hello  **[les points de distribution](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  sur toowhich les packages hello doivent être copiés.
3. Assistant hello terminée. package de Hello puis le démarrage de la réplication toohello spécifié de points de distribution.
4. Une fois que la distribution de package hello est terminée, cliquez sur le package de hello, puis sélectionnez **déployer**.
  ![Capture d’écran de la console Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Sélectionnez hello regroupement de périphériques serveur Linux vous avez créé dans la section conditions préalables de hello en tant que regroupement cible de hello pour le déploiement.

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. Sur hello **spécifier la destination de contenu hello** page, sélectionnez votre **les Points de Distribution**.
7. Sur hello **toocontrol de paramètres de spécifier comment ce logiciel est déployé** , vérifiez que hello vise **requis**.

  ![Capture d’écran de l’assistant Déploiement du logiciel](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Sur hello **spécifier la planification pour ce déploiement hello** , spécifiez une planification. Pour plus d’informations, consultez [Planification de packages](https://technet.microsoft.com/library/gg682178.aspx).
9. Sur hello **les Points de Distribution** page, configurez les propriétés de hello selon les besoins de toohello de votre centre de données. Puis terminer hello.

Service mobilité est installé sur hello regroupement de périphériques serveur Linux, selon la planification toohello que vous avez configuré.

## <a name="other-methods-tooinstall-mobility-service"></a>Autres méthodes de tooinstall Service mobilité
Voici d’autres options pour l’installation du service Mobilité :
* [Installation manuelle à l’aide de l’interface utilisateur graphique](http://aka.ms/mobsvcmanualinstall)
* [Installation manuelle à l’aide de la ligne de commande](http://aka.ms/mobsvcmanualinstallcli)
* [Installation Push à l’aide du serveur de configuration](http://aka.ms/pushinstall)
* [Installation automatisée à l’aide d’Azure Automation et de la Configuration de l’état souhaité](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>Désinstaller le service Mobilité
Vous pouvez créer des packages de Configuration Manager toouninstall Service mobilité. Utilisez hello suivant script toodo ainsi :

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt trop[activer la protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) pour vos ordinateurs virtuels.
