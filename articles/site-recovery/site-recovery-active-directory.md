---
title: aaaProtect Active Directory et DNS avec Azure Site Recovery | Documents Microsoft
description: "Cet article décrit comment tooimplement une solution de récupération d’urgence pour Active Directory à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Protéger Active Directory et DNS avec Azure Site Recovery
Les applications d’entreprise telles que SharePoint, Dynamics AX et SAP dépendent Active Directory et une toofunction d’infrastructure DNS correctement. Lorsque vous créez une solution de récupération d’urgence pour les applications, il est important tooremember que vous devez tooprotect et récupérez d’Active Directory et DNS avant de hello autres composants d’application, le tooensure choses fonctionnent correctement en cas de sinistre.

Site Recovery est un service Azure offrant une récupération d’urgence en coordonnant la réplication, le basculement et la récupération des machines virtuelles. Récupération de site prend en charge un certain nombre de scénarios de réplication tooconsistently protéger, en toute transparence basculement machines virtuelles et les applications tooprivate, public ou hébergeur clouds.

À l’aide de Site Recovery, vous pouvez créer un plan de récupération d’urgence automatisé complet pour Active Directory. En cas d’interruption, vous pouvez lancer un basculement en quelques secondes, où que vous soyez, et bénéficier d’un Active Directory opérationnel en quelques minutes. Si vous avez déployé Active Directory pour plusieurs applications, tels que SharePoint et SAP dans votre site principal, et que vous souhaitez toofail sur le site de hello terminée, vous pouvez basculer à l’aide de première Active Directory Site Recovery, puis basculer hello autres applications à l’aide de plans de récupération d’application spécifiques.

Cet article explique comment toocreate une solution de récupération d’urgence pour Active Directory, comment tooperform planifié, non planifié et les basculements de test à l’aide d’un plan de récupération d’un seul clic, hello configurations prises en charge et des conditions préalables.  Vous devez être capable d’utiliser Active Directory et Azure Site Recovery avant de commencer.

## <a name="replicating-domain-controller"></a>Réplication d’un contrôleur de domaine

Vous devez toosetup [réplication de Site Recovery](#enable-protection-using-site-recovery) sur au moins un ordinateur virtuel qui héberge le contrôleur de domaine et DNS. Si vous avez [plusieurs contrôleurs de domaine](#environment-with-multiple-domain-controllers) dans votre environnement, en outre tooreplicating hello ordinateur virtuel contrôleur de domaine avec Site Recovery, vous auriez également tooset d’un [le contrôleur de domaine supplémentaire](#protect-active-directory-with-active-directory-replication) sur le site de cible hello (Azure ou un centre de données secondaire locale). 

### <a name="single-domain-controller-environment"></a>Environnement avec un seul contrôleur de domaine
Si vous avez uniquement un seul contrôleur de domaine, ainsi que certaines applications souhaité toofail sur l’intégralité du site hello ensemble, puis nous recommandons d’utiliser le contrôleur de domaine de récupération de Site tooreplicate hello site secondaire de toohello (si vous avez basculé tooAzure ou site secondaire tooa). Hello même répliquées domaine DNS/contrôleur virtual machine peut être utilisé pour [test de basculement](#test-failover-considerations) également.

### <a name="environment-with-multiple-domain-controllers"></a>Environnement avec plusieurs contrôleurs de domaine
Si ont de nombreuses applications et il est plus d’un contrôleur de domaine dans un environnement de hello, ou si vous envisagez toofail sur quelques applications à la fois, nous vous recommandons qu’en plus contrôleur de domaine tooreplicating hello virtual machine avec Site Recovery vous également configurer un [contrôleur de domaine supplémentaire](#protect-active-directory-with-active-directory-replication) sur le site de cible hello (Azure ou un centre de données secondaire locale). Pour [test de basculement](#test-failover-considerations), vous utilisez le contrôleur de domaine répliqué par Site Recovery et pour le basculement, le contrôleur de domaine supplémentaire hello sur le site cible de hello. 


Hello sections suivantes expliquent comment protection tooenable pour un contrôleur de domaine en mode de récupération de Site et comment tooset d’un contrôleur de domaine dans Azure.

## <a name="prerequisites"></a>Composants requis
* Un déploiement local d’Active Directory et du serveur DNS.
* Un coffre Azure Site Recovery Services dans un abonnement Microsoft Azure.
* Si vous effectuez une réplication tooAzure, exécutez hello Azure Virtual Machine Readiness Assessment outil tooensure de machines virtuelles, elles sont compatibles avec les machines virtuelles Azure et Azure Site Recovery Services.

## <a name="enable-protection-using-site-recovery"></a>Activer la protection à l'aide de Site Recovery
### <a name="protect-hello-virtual-machine"></a>Protéger un ordinateur virtuel hello
Activer la protection d’ordinateur virtuel DNS/contrôleur du domaine hello en mode de récupération de Site. Configurer les paramètres de récupération de Site basés sur le type d’ordinateur virtuel hello (Hyper-V ou VMware). contrôleur de domaine Hello répliquée à l’aide de la récupération de Site est utilisé pour [test de basculement](#test-failover-considerations). Assurez-vous qu’il répond aux hello suivant les exigences :

1. contrôleur de domaine Hello est un serveur de catalogue global
2. contrôleur de domaine Hello doit être le propriétaire du rôle FSMO hello pour les rôles qui seront nécessaires durant un test de basculement (sans quoi ces rôles devez toobe [pris](http://aka.ms/ad_seize_fsmo) après le basculement de hello)

### <a name="configure-virtual-machine-network-settings"></a>Configurer les paramètres réseau de la machine virtuelle
Pour un ordinateur virtuel de DNS/contrôleur de domaine hello, configurez les paramètres réseau en mode de récupération de Site afin que machine virtuelle de hello réseau approprié de toohello attaché après le basculement. 

![Paramètres réseau de la machine virtuelle](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Protéger Active Directory avec la réplication Active Directory
### <a name="site-to-site-protection"></a>Protection de site à site
Créer un contrôleur de domaine sur le site secondaire de hello. Quand vous promouvez le contrôleur de domaine hello serveur tooa, spécifiez le nom hello Hello même domaine qui est utilisé sur le site principal de hello. Vous pouvez utiliser hello **les Sites Active Directory et les Services** -composant logiciel enfichable de l’objet paramètres tooconfigure sur le lien de sites hello toowhich hello sites sont ajoutés. En configurant des paramètres sur un lien de sites, vous pouvez contrôler le moment où la réplication a lieu entre deux sites ou plus, ainsi que la fréquence. Pour plus d’informations, consultez [Planification de la réplication entre des sites](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Protection de site vers Azure
Suivez les instructions de hello trop[créer un contrôleur de domaine dans un réseau virtuel Azure](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Lorsque vous promouvez le contrôleur de domaine hello serveur tooa, spécifiez hello même nom de domaine qui est utilisé sur le site principal de hello.

Puis [reconfigurer hello du serveur DNS pour le réseau virtuel de hello](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), serveurDNS toouse hello dans Azure.

![Réseau Azure](./media/site-recovery-active-directory/azure-network.png)

**DNS dans le réseau de production Azure**

## <a name="test-failover-considerations"></a>Considérations en matière de test de basculement
Le test de basculement est effectué dans un réseau isolé du réseau de production afin qu’il n’y ait aucun impact sur les charges de travail de production.

La plupart des applications nécessitent également la présence hello un contrôleur de domaine et une toofunction de serveur DNS. Par conséquent, avant de l’application hello est basculée, un contrôleur de domaine doit toobe créé dans hello isolé du réseau toobe est utilisé pour le test de basculement. Hello toodo de façon plus simple il s’agit de tooreplicate une machine virtuelle DNS/contrôleur domaine Site Recovery. Puis exécuter un test de basculement de l’ordinateur virtuel de contrôleur de domaine hello avant d’exécuter un test de basculement hello du plan de récupération pour une application hello. Voici comment procéder :

1. [Répliquer](site-recovery-replicate-vmware-to-azure.md) hello virtuels DNS/contrôleur de domaine à l’aide de la récupération de Site.
1. Créez un réseau isolé. Tout réseau virtuel créé dans Azure par défaut est isolé des autres réseaux. Nous recommandons que la plage d’adresses IP hello pour ce réseau est identique à celui de votre réseau de production. N’activez pas la connectivité de site à site sur ce réseau.
1. Fournissez une adresse IP DNS dans le réseau hello créé en tant qu’adresse IP de hello que vous attendez tooget de machine virtuelle DNS hello. Si vous effectuez une réplication tooAzure, puis fournissez hello adresse IP pour hello machine virtuelle qui est utilisé lors du basculement dans **adresse IP cible** définissant dans **de calcul et réseau** paramètres. 

    ![Adresse IP cible](./media/site-recovery-active-directory/DNS-Target-IP.png)**Adresse IP cible**

    ![Réseau de test Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS dans le réseau de test Azure**

> [!TIP]
> Machines virtuelles de test toocreate dans un sous-réseau portent le même nom de tentatives de récupération de site et à l’aide de hello même adresse IP que celle fournie dans **de calcul et réseau** paramètres d’ordinateur virtuel de hello. Si le sous-réseau de même nom n’est pas disponible dans hello réseau virtuel Azure fourni pour le test de basculement, puis l’ordinateur virtuel de test est créé dans le premier sous-réseau de hello par ordre alphabétique. Si hello cible IP fait partie de hello choisi sous-réseau, récupération de Site tente de machine virtuelle toocreate hello test de basculement à l’aide de hello cible IP. Si hello cible IP n’est pas partie de hello choisi sous-réseau, ordinateur virtuel de test de basculement est créé à l’aide d’une adresse IP disponible dans hello choisi de sous-réseau. 
>
>


1. Si vous effectuez une réplication tooanother sur site local et que vous utilisez DHCP, suivez les instructions de hello trop[l’installation de DNS et DHCP pour le test de basculement](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Effectuez un test de basculement de hello contrôleur de domaine s’exécutent dans un réseau isolé de hello. Utilisez dernière version disponible **application cohérente** point de récupération hello domaine contrôleur machine virtuelle toodo hello du basculement de test. 
1. Exécutez un test de basculement pour le plan de récupération hello qui contient les ordinateurs virtuels de l’application hello. 
1. Une fois le test terminé, **basculement de test de nettoyage** sur l’ordinateur virtuel de contrôleur de domaine hello. Cette étape supprime le contrôleur de domaine hello qui a été créé pour le test de basculement.


### <a name="removing-reference-tooother-domain-controllers"></a>Suppression des contrôleurs de domaine de référence tooother
Lorsque vous effectuez un test de basculement, vous ne mettez tous les contrôleurs de domaine hello dans le réseau de test hello. référence de hello tooremove d’autres contrôleurs de domaine qui existent dans votre environnement de production, vous devrez peut-être trop[prendre les rôles FSMO Active Directory](http://aka.ms/ad_seize_fsmo) et [le nettoyage des métadonnées](https://technet.microsoft.com/library/cc816907.aspx) pour le domaine manquant contrôleurs. 



> [!IMPORTANT]
> Certaines configurations hello décrites dans hello suivant la section ne sont pas des configurations de contrôleur de domaine hello standard/par défaut. Si vous ne souhaitez pas toomake que ces contrôleur de domaine de production tooa modifications, vous pouvez créer un toobe dédié de contrôleur de domaine utilisé pour la récupération de Site test de basculement et rendre ces toothat de modifications.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problèmes en raison de dispositifs de protection de la virtualisation 

À partir de Windows Server 2012, [des dispositifs de protection supplémentaires ont été intégrés dans Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Ces mécanismes de protection permettent de protéger les contrôleurs de domaine virtualisés contre les restaurations USN, tant que plateforme de l’hyperviseur sous-jacent hello prend en charge VM-GenerationID. Azure prend en charge VM-GenerationID, ce qui signifie que les contrôleurs de domaine qui exécutent Windows Server 2012 ou version ultérieure sur les machines virtuelles ont des garanties supplémentaires hello. 


Lorsque hello VM-GenerationID est réinitialisé, hello ID d’invocation de la base de données hello AD DS est également réinitialisé, hello pool RID est rejeté et SYSVOL est marqué comme ne faisant pas autorité. Pour plus d’informations, consultez [Introduction tooActive virtualisation des Services de domaine Active](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) et [virtualisation DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Basculement tooAzure peut provoquer la réinitialisation de VM-GenerationID et qui intervient dans les dispositifs de protection supplémentaires hello au démarrage de l’ordinateur virtuel de contrôleur de domaine hello dans Azure. Cela peut entraîner un **un délai important** utilisateur qui est en mesure de toologin toohello contrôleur de domaine. Étant donné que ce contrôleur de domaine doit être utilisé uniquement dans un test de basculement, les dispositifs de protection de la virtualisation ne sont pas nécessaires. tooensure VM-GenerationID de l’ordinateur virtuel de contrôleur de domaine hello ne change, vous pouvez modifier la valeur hello suivant too4 DWORD dans le contrôleur de domaine local hello.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Symptômes des dispositifs de protection de la virtualisation
 
Si les dispositifs de protection de la virtualisation sont intervenus après un test de basculement, vous pouvez observer un ou plusieurs des symptômes suivants :  

Modification de l’ID de génération

![Modification de l’ID de génération](./media/site-recovery-active-directory/Event2170.png)

Modification de l’ID d’appel

![Modification de l’ID d’appel](./media/site-recovery-active-directory/Event1109.png)

Les partages Sysvol et Netlogon ne sont pas disponibles

![Partage Sysvol](./media/site-recovery-active-directory/sysvolshare.png)

![Sysvol Ntfrs](./media/site-recovery-active-directory/Event13565.png)

Les bases de données DFSR sont supprimées

![Suppression de base de données DFSR](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Certaines configurations hello décrites dans hello suivant la section ne sont pas des configurations de contrôleur de domaine hello standard/par défaut. Si vous ne souhaitez pas toomake que ces contrôleur de domaine de production tooa modifications, vous pouvez créer un toobe dédié de contrôleur de domaine utilisé pour la récupération de Site test de basculement et rendre ces toothat de modifications.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Résolution des problèmes liés à un contrôleur de domaine survenant pendant un test de basculement


Sur une invite de commandes, exécutez hello suivant commande toocheck si dossiers SYSVOL et NETLOGON sont partagés :

    NET SHARE

Sur hello invite de commandes, exécutez hello suivant commande tooensure qui hello du contrôleur de domaine fonctionne correctement.

    dcdiag /v > dcdiag.txt

Dans le journal de sortie hello, recherchez tooconfirm texte suivant qui hello du contrôleur de domaine fonctionne correctement. 

* « passed test Connectivity »
* « passed test Advertising »
* « passed test MachineAccount »

Si hello conditions précédentes sont remplies, il est probable que contrôleur de domaine hello fonctionne correctement. Si ce n’est pas le cas, essayez les étapes ci-après.


* Effectuer une restauration faisant autorité hello du contrôleur de domaine.
    * Bien qu’il soit [déconseillé toouse FRS réplication](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), mais si vous utilisez toujours, puis suivez les étapes de hello fournis [ici](https://support.microsoft.com/kb/290762) toodo une restauration faisant autorité. Vous pouvez en savoir plus sur Burflags, nous avons vu dans le lien précédent de hello [ici](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Si vous utilisez une réplication DFSR, puis suivez les étapes hello disponibles [ici](https://support.microsoft.com/kb/2218556) toodo une restauration faisant autorité. Vous pouvez également utiliser les fonctions PowerShell disponibles [ici](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) à cet effet. 
    
* Ignorer l’exigence de synchronisation initiale en définissant suivant too0 de clé de Registre dans le contrôleur de domaine local hello. Si cette valeur DWORD n’existe pas, vous pouvez la créer sous le nœud « Paramètres ». Vous trouverez plus d’informations à ce sujet [ici](https://support.microsoft.com/kb/2001093).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Désactiver l’exigence hello qu’un serveur de catalogue global est ouverture de session utilisateur toovalidate disponible en définissant suivant too1 de clé de Registre dans le contrôleur de domaine local hello. Si cette valeur DWORD n’existe pas, vous pouvez la créer sous le nœud « Lsa ». Vous trouverez plus d’informations à ce sujet [ici](http://support.microsoft.com/kb/241789).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS et contrôleur de domaine sur différentes machines
Si DNS n’est pas sur hello même ordinateur virtuel en tant que contrôleur de domaine hello, vous devez toocreate une VM DNS pour le basculement de test hello. S’ils sont sur hello même machine virtuelle, vous pouvez ignorer cette section.

Vous pouvez utiliser un nouveau serveur DNS et créez toutes les zones hello requis. Par exemple, si votre domaine Active Directory est contoso.com, vous pouvez créer une zone DNS avec le nom de contoso.com hello. entrées Hello correspondant tooActive active doivent être mis à jour dans DNS, comme suit :

1. Assurez-vous que ces paramètres sont en place avant toute autre machine virtuelle dans le plan de récupération hello s’affiche :
   
   * zone de Hello doit être nommé après le nom de racine de forêt hello.
   * zone de Hello doit être sauvegardé.
   * zone de Hello doit être activée pour les mises à jour sécurisées et non sécurisées.
   * programme de résolution Hello d’ordinateur virtuel de contrôleur de domaine hello doit pointer adresse toohello de machine virtuelle de hello DNS.
2. Exécutez hello commande suivante sur le contrôleur de domaine :
   
    `nltest /dsregdns`
3. Ajouter une zone sur le serveur DNS de hello, autoriser les mises à jour non sécurisées et ajoutez-lui une entrée tooDNS :
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Étapes suivantes
Lecture [les charges de travail puis-je protéger ?](site-recovery-workload.md) toolearn plus sur la protection des charges de travail enterprise avec Azure Site Recovery.
