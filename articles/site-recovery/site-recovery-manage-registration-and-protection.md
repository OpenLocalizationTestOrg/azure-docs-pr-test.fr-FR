---
title: "les serveurs aaaRemove et désactivez la protection | Documents Microsoft"
description: "Cet article décrit comment toounregister les serveurs à partir d’une récupération de Site de coffre et la protection de toodisable pour les serveurs physiques et virtuels."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Supprimer des serveurs et désactiver la protection

Hello service Azure Site Recovery contribue tooyour continuité des activités et la stratégie de récupération d’urgence. service de Hello orchestre la réplication, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. Machines peuvent être répliquée tooAzure ou centre de données secondaire locale tooa. Pour avoir un rapide aperçu, consultez la section [Qu’est-ce qu’Azure Site Recovery ?](site-recovery-overview.md)

Cet article décrit comment toounregister les serveurs à partir des Services de récupération de coffre Bonjour portail Azure, et comment toodisable la protection des machines protégées par la récupération de Site.

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Annuler l’inscription d’un serveur de configuration connecté

Si vous répliquez des ordinateurs virtuels VMware ou tooAzure des serveurs physiques Windows/Linux, vous pouvez annuler l’inscription un serveur de configuration connecté à partir d’un archivage comme suit :

1. Désactivez la protection des ordinateurs. Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.
2. Dissociez les stratégies. Dans **Infrastructure Site Recovery** > **pour VMWare et les Machines physiques** > **stratégies de réplication**, double-cliquez sur hello stratégie associée. Serveur de configuration avec le bouton hello > **dissocier**.
3. Supprimez les processus locaux supplémentaires ou les serveurs cibles maîtres. Dans **Infrastructure Site Recovery** > **pour VMWare et les Machines physiques** > **serveurs de Configuration**, serveur de hello avec le bouton droit > **Supprimer**.
4. Supprimer le serveur de configuration hello.
5. Désinstaller manuellement le service de mobilité hello en cours d’exécution sur le serveur cible maître de hello (il s’agit soit distinct serveur, ou en cours d’exécution sur le serveur de configuration hello).
6. Désinstallez les serveurs de traitement supplémentaires.
7. Désinstallez le serveur de configuration hello.
8. Sur le serveur de configuration hello, désinstallez instance hello de MySQL qui a été installée par la récupération de Site.
9. Dans le Registre hello hello du serveur de configuration SUPPR hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Annuler l’inscription d’un serveur de configuration non connecté

Si vous répliquez des ordinateurs virtuels VMware ou tooAzure des serveurs physiques Windows/Linux, vous pouvez annuler l’inscription un serveur de configuration non connecté à partir d’un archivage comme suit :

1. Désactivez la protection des ordinateurs. Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**. Sélectionnez **arrêter la gestion hello machine**.
2. Supprimez les processus locaux supplémentaires ou les serveurs cibles maîtres. Dans **Infrastructure Site Recovery** > **pour VMWare et les Machines physiques** > **serveurs de Configuration**, serveur de hello avec le bouton droit > **Supprimer**.
3. Supprimer le serveur de configuration hello.
4. Désinstaller manuellement le service de mobilité hello en cours d’exécution sur le serveur cible maître de hello (il s’agit soit distinct serveur, ou en cours d’exécution sur le serveur de configuration hello).
5. Désinstallez les serveurs de traitement supplémentaires.
6. Désinstallez le serveur de configuration hello.
7. Sur le serveur de configuration hello, désinstallez instance hello de MySQL qui a été installée par la récupération de Site.
8. Dans le Registre hello hello du serveur de configuration SUPPR hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Annuler l’inscription d’un serveur VMM connecté

En tant que meilleure pratique, nous vous recommandons d’annuler l’inscription serveur VMM de hello lorsqu’il est connecté tooAzure. Cela garantit que les paramètres sur les serveurs VMM hello (et sur d’autres serveurs VMM avec les clouds associés) sont correctement nettoyées. En cas de problème de connectivité permanent, ne supprimez qu’un serveur non connecté. Si le serveur VMM de hello n’est pas connecté, vous devez toomanually exécuter un tooclean de script des paramètres.

1. Arrêter la réplication des machines virtuelles dans des clouds sur le serveur VMM tooremove de hello.
2. Supprimer tous les mappages réseau utilisés par les clouds sur le serveur VMM toodelete de hello. Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **le mappage réseau**, cliquez sur le mappage réseau hello >  **Supprimer**.
3. Dissocier des stratégies de réplication à partir de clouds sur le serveur VMM tooremove de hello.  Dans **Infrastructure Site Recovery** > **pour System Center VMM** >  **stratégies de réplication**, double-cliquez sur la stratégie de hello associé. Cliquez sur le cloud de hello > **dissocier**.
4. Supprimer le serveur VMM de hello ou nœud actif de VMM. Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **serveurs VMM**, serveur de hello avec le bouton droit >  **Supprimer**.
5. Désinstallez hello fournisseur manuellement sur le serveur VMM de hello. Si vous avez un cluster, supprimez-le de tous les nœuds.
6. Si vous effectuez une réplication tooAzure, supprimez manuellement hello Microsoft Recovery Services agent hôtes Hyper-V dans des clouds hello supprimé.



### <a name="unregister-an-unconnected-vmm-server"></a>Annuler l’inscription d’un serveur VMM non connecté

1. Arrêter la réplication des machines virtuelles dans des clouds sur le serveur VMM tooremove de hello.
2. Supprimer tous les mappages réseau utilisés par les clouds sur le serveur VMM hello que vous souhaitez toodelete. Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **le mappage réseau**, cliquez sur le mappage réseau hello >  **Supprimer**.
3. Notez l’ID de hello du serveur VMM de hello.
4. Dissocier des stratégies de réplication à partir de clouds sur le serveur VMM tooremove de hello.  Dans **Infrastructure Site Recovery** > **pour System Center VMM** >  **stratégies de réplication**, double-cliquez sur la stratégie de hello associé. Cliquez sur le cloud de hello > **dissocier**.
5. Supprimer le serveur VMM de hello ou le nœud actif. Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **serveurs VMM**, serveur de hello avec le bouton droit >  **Supprimer**.
6. Téléchargez et exécutez hello [script de nettoyage](http://aka.ms/asr-cleanup-script-vmm) sur le serveur VMM de hello. Ouvrez PowerShell avec hello **exécuter en tant qu’administrateur** option, la stratégie d’exécution toochange hello pour l’étendue de la valeur par défaut (LocalMachine) hello. Dans le script de hello, spécifiez ID hello Hello serveur VMM que vous souhaitez tooremove. script de Hello supprime l’inscription et le cloud appariement des informations à partir du serveur de hello.
5. Exécutez le script de nettoyage de hello sur tous les serveurs VMM qui contiennent des clouds qui sont associés à des clouds sur le serveur VMM tooremove de hello.
6. Exécutez le script de nettoyage hello sur n’importe quel autres passifs nœuds de cluster VMM qui ont hello que fournisseur installé.
7. Désinstallez hello fournisseur manuellement sur le serveur VMM de hello. Si vous avez un cluster, supprimez-le de tous les nœuds.
8. Si vous tooAzure de réplication, vous pouvez supprimer hello Microsoft Recovery Services agent à partir des hôtes Hyper-V dans des clouds hello supprimé.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Annuler l’inscription d’un hôte Hyper-V dans un site Hyper-V

Les hôtes Hyper-V non gérés par VMM sont rassemblés dans un site Hyper-V. Pour supprimer un hôte d’un site Hyper-V, procédez comme suit :

1. Désactivez la réplication pour les machines virtuelles Hyper-V situé sur l’ordinateur hôte de hello.
2. Dissocier des stratégies pour le site de Hyper-V hello. Dans **Infrastructure Site Recovery** > **pour les Sites Hyper-V** >  **stratégies de réplication**, double-cliquez sur la stratégie de hello associé. Site de hello avec le bouton droit > **dissocier**.
3. Supprimez les hôtes Hyper-V. Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **hôtes Hyper-V**, serveur de hello avec le bouton droit >  **Supprimer**.
4. Supprimer le site de hello Hyper-V après la suppression de tous les ordinateurs hôtes à partir de celui-ci. Dans **Infrastructure Site Recovery** > **pour System Center VMM** > **Sites Hyper-V**, site de hello avec le bouton droit >  **Supprimer**.
5. Exécutez hello script suivant sur chaque hôte Hyper-V que vous avez supprimé. Hello script nettoie les paramètres sur le serveur de hello et annule l’inscription du coffre de hello.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Désactiver la protection d’une machine virtuelle VMware ou d’un serveur physique

1. Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.
2. Dans **Supprimer la machine**, sélectionnez une de ces options :
    - **Désactivez la protection de machine hello (recommandé)**. Utilisez cette toostop option réplication machine de hello. Les paramètres de Site Recovery seront nettoyés automatiquement. Vous voyez uniquement cette option Bonjour suivant circonstances :
        - **Vous avez redimensionné le volume de machine virtuelle hello**: quand vous redimensionnez un Bonjour volume virtuel ordinateur passe dans un état critique. Sélectionnez cette option toodisables la protection tout en conservant les points de récupération dans Azure. Lorsque vous réactivez la protection pour l’ordinateur de hello, données hello pour le volume de hello redimensionné seront transférée tooAzure.
        - **Vous avez exécuté récemment un basculement**— après avoir exécuté un basculement tootest votre environnement, sélectionnez ce toostart option protéger à nouveau les machines locales. Il désactive chaque machine virtuelle, et puis vous devez tooenable protection leur à nouveau. La désactivation de la machine hello avec ce paramètre n’affecte pas hello ordinateur virtuel dans Azure. Ne désinstallez pas service de mobilité hello à partir de l’ordinateur de hello.
    - **Arrêter la gestion hello machine**. Si vous sélectionnez cette option, hello ordinateur sera uniquement être supprimé le coffre hello. Paramètres de protection locale pour l’ordinateur de hello ne seront pas affectées. paramètres tooremove hello machine et ordinateur hello tooremove hello abonnement Azure, vous avez besoin de tooclean hello paramètres en désinstallant le service de mobilité hello.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Désactiver la protection d’une machine virtuelle Hyper-V dans un cloud VMM

1. Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.
2. Dans **Supprimer la machine**, sélectionnez une de ces options :

    - **Désactivez la protection de machine hello (recommandé)**. Utilisez cette toostop option réplication machine de hello. Les paramètres de Site Recovery seront nettoyés automatiquement.
    - **Arrêter la gestion hello machine**. Si vous sélectionnez cette option, hello ordinateur sera uniquement être supprimé le coffre hello. Paramètres de protection locale pour l’ordinateur de hello ne seront pas affectées. paramètres tooremove hello machine et ordinateur hello tooremove hello abonnement Azure, vous avez besoin de tooclean hello paramètres des manuellement, à l’aide d’instructions hello ci-dessous. Notez que si vous sélectionnez l’ordinateur virtuel de hello toodelete et ses disques durs, ils allez supprimés à partir de l’emplacement cible de hello.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Nettoyer les paramètres de protection - site VMM secondaire de réplication tooa

Si vous avez sélectionné **arrêter la gestion hello machine** et vous réplication tooa du site secondaire, exécutez ce script sur tooclean du serveur principal hello des paramètres de hello pour l’ordinateur virtuel principal hello. Dans la console VMM hello, cliquez sur console de VMM PowerShell hello PowerShell bouton tooopen hello. Remplacez SQLVM1 par nom hello de votre machine virtuelle.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Sur le serveur VMM secondaire de hello exécuter cette tooclean script des paramètres hello pour l’ordinateur virtuel secondaire de hello :

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Sur le serveur secondaire VMM hello, actualiser les machines virtuelles de hello sur le serveur hôte de Hyper-V hello, afin que hello machine virtuelle secondaire obtient détectée à nouveau dans la console VMM hello.
4. Hello étapes ci-dessus, désactivez les paramètres de réplication de hello sur le serveur VMM de hello. Si vous souhaitez que la réplication pour l’ordinateur virtuel de hello, exécuter le script suivant oh de hello toostop hello des ordinateurs virtuels principales et secondaires. Remplacez SQLVM1 par nom hello de votre machine virtuelle.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Nettoyer les paramètres de protection : tooAzure de réplication

1. Si vous avez sélectionné **arrêter la gestion hello machine** et vous répliquez tooAzure, exécutez ce script sur le serveur VMM source hello, à l’aide de PowerShell à partir de la console VMM hello.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hello étapes ci-dessus, désactivez les paramètres de réplication hello sur le serveur VMM de hello. réplication de toostop pour l’ordinateur virtuel de hello en cours d’exécution sur le serveur hôte de Hyper-V hello, exécutez ce script. Remplacez SQLVM1 par nom hello de votre machine virtuelle et host01.contoso.com avec nom hello du serveur hôte de Hyper-V hello.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Désactiver la protection d’une machine virtuelle Hyper-V dans un site Hyper-V

Utilisez cette procédure si vous effectuez une réplication tooAzure d’ordinateurs virtuels Hyper-V sans serveur VMM.

1. Dans **éléments protégés** > **répliquées des éléments**, machine de hello avec le bouton droit > **supprimer**.
2. Dans **supprimer la Machine**, vous pouvez sélectionner hello options suivantes :

   - **Désactivez la protection de machine hello (recommandé)**. Utilisez cette toostop option réplication machine de hello. Les paramètres de Site Recovery seront nettoyés automatiquement.
   - **Arrêter la gestion hello machine**. Si vous sélectionnez cette option machine de hello n’est supprimée du coffre de hello. Paramètres de protection locale pour l’ordinateur de hello ne seront pas affectées. paramètres tooremove sur la machine de hello et ordinateur virtuel tooremove hello hello abonnement Azure, vous devez appliquer tooclean hello paramètres configuration manuellement. Si vous sélectionnez l’ordinateur virtuel de hello toodelete et ses disques durs, ils sont supprimés à partir de l’emplacement cible de hello.
3. Si vous avez sélectionné **arrêter la gestion hello machine**, exécutez ce script sur le serveur hôte de Hyper-V source hello, la réplication tooremove pour la machine virtuelle de hello. Remplacez SQLVM1 par nom hello de votre machine virtuelle.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
