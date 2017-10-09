---
title: "aaaCreate un écouteur de groupe de disponibilité de SQL Server dans des machines virtuelles | Documents Microsoft"
description: "Instructions pas à pas pour la création d’un écouteur pour un groupe de disponibilité AlwaysOn pour SQL Server dans des machines virtuelles Azure"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Configurer un équilibreur de charge pour un groupe de disponibilité AlwaysOn dans Azure
Cet article explique comment toocreate un équilibreur de charge pour un groupe de disponibilité SQL Server Always On dans Azure virtual machines qui sont en cours d’exécution avec Azure Resource Manager. Un groupe de disponibilité requiert un équilibrage de charge lorsque les instances de SQL Server de hello se trouvent sur des machines virtuelles. équilibrage de charge Hello stocke l’adresse IP hello écouteur hello. Si un groupe de disponibilité englobe plusieurs régions, chaque région a besoin d’un équilibreur de charge.

toocomplete cette tâche, vous devez toohave un groupe de disponibilité de SQL Server est déployé sur les machines virtuelles qui s’exécutent avec le Gestionnaire de ressources. Les deux machines virtuelles de SQL Server doit appartenir toohello même groupe à haute disponibilité. Vous pouvez utiliser hello [modèle Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically créer le groupe de disponibilité hello dans le Gestionnaire de ressources. Ce modèle crée automatiquement un équilibreur de charge interne. 

Si vous préférez, vous pouvez [configurer manuellement un groupe de disponibilité](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Cet article nécessite que vos groupes de disponibilité soient déjà configurés.  

Rubriques connexes :

* [Configurer des groupes de disponibilité AlwaysOn dans une machine virtuelle Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurer une connexion de réseau virtuel à réseau virtuel à l’aide d’Azure Resource Manager et de PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

En progressant dans cet article, vous créez et configurez un équilibreur de charge Bonjour portail Azure. Après hello est terminée, vous configurez hello toouse hello adresse IP du cluster d’équilibrage de charge hello pour l’écouteur du groupe de disponibilité hello.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Créer et configurer l’équilibrage de charge hello Bonjour portail Azure
Dans cette partie de la tâche hello, procédez comme hello suivant :

1. Bonjour portail Azure, équilibrage de charge hello de créer et configurer une adresse IP de hello.
2. Configurer le pool principal d’hello.
3. Création de la sonde de hello. 
4. Définir des règles d’équilibrage de charge hello.

> [!NOTE]
> Si les instances de SQL Server hello se trouvent dans plusieurs groupes de ressources et les régions, effectuer chaque étape à deux reprises, une fois dans chaque groupe de ressources.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Étape 1 : Créer l’équilibreur de charge hello et configurer une adresse IP de hello
Commencez par créer équilibrage de charge hello. 

1. Bonjour portail Azure, ouvrez le groupe de ressources hello qui contient des machines virtuelles de SQL Server hello. 

2. Dans le groupe de ressources hello, cliquez sur **ajouter**.

3. Recherchez **l’équilibrage de charge** puis, dans les résultats de recherche hello **équilibrage de charge**, qui est publié par **Microsoft**.

4. Sur hello **équilibrage de charge** panneau, cliquez sur **créer**.

5. Bonjour **équilibrage de charge créer** boîte de dialogue zone, configurer équilibrage de charge hello comme suit :

   | Paramètre | Valeur |
   | --- | --- |
   | **Name** |Un nom représentant l’équilibrage de charge hello. Par exemple, **sqlLB**. |
   | **Type** |**Interne**: la plupart des implémentations utilisent un équilibreur de charge interne, ce qui permet aux applications dans hello même groupe de disponibilité toohello tooconnect réseau virtuel.  </br> **Externe**: autorise le groupe de disponibilité applications tooconnect toohello via une connexion Internet publique. |
   | **Réseau virtuel** |Sélectionnez le réseau virtuel hello qui sont des instances de SQL Server hello dans. |
   | **Sous-réseau** |Sélectionnez sous-réseau hello qui sont des instances de SQL Server hello dans. |
   | **Affectation d’adresses IP** |**Statique** |
   | **Adresse IP privée** |Spécifiez une adresse IP disponible à partir du sous-réseau de hello. Utilisez cette adresse IP lorsque vous créez un écouteur sur le cluster de hello. Dans un script PowerShell, plus loin dans cet article, utilisez cette adresse pour hello `$ILBIP` variable. |
   | **Abonnement** |Si vous avez plusieurs abonnements, ce champ doit normalement apparaître. Sélectionnez l’abonnement hello que vous souhaitez tooassociate avec cette ressource. Il est normalement hello même abonnement que toutes les ressources de hello pour le groupe de disponibilité hello. |
   | **Groupe de ressources** |Sélectionnez le groupe de ressources hello qui sont des instances de SQL Server hello dans. |
   | **Emplacement** |Sélectionnez hello emplacement Azure qui sont des instances de SQL Server hello dans. |

6. Cliquez sur **Créer**. 

Azure crée un équilibreur de charge hello. équilibrage de charge Hello appartient tooa réseau, de sous-réseau, de groupe de ressources et d’emplacement. Une fois la tâche hello terminée, vérifiez les paramètres d’équilibrage de charge hello dans Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Étape 2 : Configurer le pool principal de hello
Appels Azure hello pool d’adresses de serveur principal *pool principal*. Dans ce cas, le pool de principaux de hello est adresses hello de deux instances de SQL Server hello dans votre groupe de disponibilité. 

1. Dans votre groupe de ressources, cliquez sur l’équilibrage de charge hello que vous avez créé. 

2. Dans **Paramètres**, cliquez sur **Pools principaux**.

3. Sur **pools principaux**, cliquez sur **ajouter** toocreate un pool d’adresses du serveur principal. 

4. Sur **ajouter le pool principal**, sous **nom**, tapez un nom pour le pool principal d’hello.

5. Sous **Machines virtuelles**, cliquez sur **Ajouter une machine virtuelle**. 

6. Sous **choisir les machines virtuelles**, cliquez sur **choisir un ensemble de disponibilité**, puis spécifiez que les machines virtuelles de SQL Server hello appartiennent au groupe à haute disponibilité de hello.

7. Une fois que vous avez choisi hello à haute disponibilité, cliquez sur **choisissez hello virtuels**, sélectionnez hello deux machines virtuelles qui hébergent des instances de SQL Server hello hello groupe de disponibilité, puis cliquez sur **sélectionnez**. 

8. Cliquez sur **OK** tooclose des panneaux de hello pour **choisir les machines virtuelles**, et **ajouter le pool principal**. 

Azure met à jour les paramètres de hello pour le pool d’adresses principal hello. Votre groupe à haute disponibilité a maintenant un pool de deux instances de SQL Server.

### <a name="step-3-create-a-probe"></a>Étape 3 : Créer une sonde
Sonde de Hello définit comment Azure vérifie à qui des instances de SQL Server hello possède actuellement écouteur hello. Les tests de Azure service hello basé sur l’adresse IP de hello sur un port que vous définissez lors de la création de la sonde de hello.

1. L’équilibrage de charge sur hello **paramètres** panneau, cliquez sur **sondes d’intégrité**. 

2. Sur hello **sondes d’intégrité** panneau, cliquez sur **ajouter**.

3. Configurer la sonde de hello sur hello **ajouter sonde** panneau. Sonde de hello tooconfigure les valeurs hello utilisation suivant :

   | Paramètre | Valeur |
   | --- | --- |
   | **Name** |Un nom représentant la sonde de hello. Par exemple, **SQLAlwaysOnEndPointProbe**. |
   | **Protocole** |**TCP** |
   | **Port** |Vous pouvez utiliser n’importe quel port disponible. Par exemple, *59999*. |
   | **Intervalle** |*5* |
   | **Seuil de défaillance sur le plan de l’intégrité** |*2* |

4.  Cliquez sur **OK**. 

> [!NOTE]
> Assurez-vous que le port hello que vous spécifiez est ouvert sur les pare-feu hello des deux instances de SQL Server. Les deux instances nécessitent une règle de trafic entrant pour hello le port TCP que vous utilisez. Pour plus d’informations, consultez [Ajouter ou modifier une règle de pare-feu](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure crée hello sonde, puis il utilise tootest quelle instance de SQL Server a écouteur hello pour le groupe de disponibilité hello.

### <a name="step-4-set-hello-load-balancing-rules"></a>Étape 4 : Définir des règles d’équilibrage de charge de hello
règles d’équilibrage de charge Hello configurer comment équilibrage de charge hello route les instances de SQL Server toohello le trafic. Pour cet équilibrage de charge, vous activez retour direct du serveur, car seul l’un des deux instances de SQL Server hello possède la ressource de port d’écoute du groupe de disponibilité hello à la fois.

1. L’équilibrage de charge sur hello **paramètres** panneau, cliquez sur **règles d’équilibrage de charge**. 

2. Sur hello **règles d’équilibrage de charge** panneau, cliquez sur **ajouter**.

3. Sur hello **ajouter équilibrage des règles** panneau, configurer la règle d’équilibrage de charge hello. Utilisez hello suivant les paramètres : 

   | Paramètre | Valeur |
   | --- | --- |
   | **Name** |Un nom de texte représentant les règles d’équilibrage de charge hello. Par exemple, **SQLAlwaysOnEndPointListener**. |
   | **Protocole** |**TCP** |
   | **Port** |*1433* |
   | **Port principal** |*1433*. Cette valeur est ignorée, car cette règle utilise **Adresse IP flottante (retour direct du serveur)**. |
   | **Sonde** |Utiliser le nom hello de sonde hello que vous avez créé pour cet équilibrage de charge. |
   | **Persistance de session** |**Aucun** |
   | **Délai d’inactivité (minutes).** |*4* |
   | **Adresse IP flottante (retour serveur direct)** |**Activé** |

   > [!NOTE]
   > Vous pouvez avoir tooscroll vers le bas hello panneau tooview tous les paramètres de hello.
   > 

4. Cliquez sur **OK**. 
5. Azure configure la règle d’équilibrage de charge hello. Équilibrage de charge hello est maintenant une instance tooroute configuré le trafic toohello SQL Server qui héberge l’écoute hello pour le groupe de disponibilité hello. 

À ce stade, groupe de ressources hello possède un équilibreur de charge qui se connecte les ordinateurs SQL Server tooboth. équilibrage de charge Hello contient également une adresse IP pour hello SQL Server Always On écouteur, afin que l’ordinateur peut répondre toorequests hello groupes de disponibilité.

> [!NOTE]
> Si vos instances de SQL Server se trouvent dans deux régions distinctes, répétez les étapes de hello Bonjour autre région. Chaque région nécessite un équilibrage de charge. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Configurer l’adresse IP équilibrage de la charge hello cluster toouse hello
étape suivante de Hello est tooconfigure hello écouter le cluster de hello et mettez écouteur hello en ligne. Hello suivant : 

1. Créer l’écouteur hello sur le cluster de basculement hello. 

2. Mettez l’écouteur hello en ligne.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Étape 5 : Créer un écouteur du groupe de disponibilité hello sur le cluster de basculement hello
Dans cette étape, vous créez manuellement l’écouteur du groupe de disponibilité hello dans le Gestionnaire du Cluster de basculement et de SQL Server Management Studio.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Vérifier la configuration de hello d’écouteur de hello

Si les dépendances et les ressources de cluster hello sont correctement configurés, vous devez être en mesure de tooview un écouteur de hello dans SQL Server Management Studio. tooset hello du port d’écoute, hello suivant :

1. Démarrez SQL Server Management Studio, puis connectez-vous toohello le réplica principal.

2. Accédez trop**haute disponibilité AlwaysOn** > **groupes de disponibilité** > **écouteurs de groupe de disponibilité**.  
    Vous devez maintenant voir le nom de l’écouteur hello que vous avez créé dans le Gestionnaire de Cluster de basculement. 

3. Cliquez sur le nom d’écouteur hello, puis cliquez sur **propriétés**.

4. Bonjour **Port** , spécifiez un numéro de port hello écouteur hello à l’aide de hello $EndpointPort utilisé précédemment (1433 était la valeur par défaut hello), puis cliquez sur **OK**.

Vous disposez maintenant d’un groupe de disponibilité dans des machines virtuelles Azure s’exécutant en mode Resource Manager. 

## <a name="test-hello-connection-toohello-listener"></a>Écouteur de toohello connexion test hello
Tester la connexion hello de manière hello suivante :

1. Instance de SQL Server de tooa RDP est Bonjour virtuel même réseau, mais ne pas les réplicas hello propre. Ce serveur peut être hello autre instance SQL Server dans un cluster de hello.

2. Utilisez **sqlcmd** connexion de hello tootest utilitaire. Par exemple, hello script suivant établit une **sqlcmd** réplica principal de connexion toohello via écouteur hello avec l’authentification Windows :
   
        sqlcmd -S <listenerName> -E

Hello connexion de SQLCMD connecte automatiquement à instance toohello SQL Server qui héberge le réplica principal de hello. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Créer une adresse IP pour un groupe de disponibilité supplémentaire

Chaque groupe de disponibilité utilise un écouteur distinct. Chaque écouteur possède sa propre adresse IP. Utilisez hello identique à l’adresse IP toohold hello équilibrage de charge pour les écouteurs supplémentaires. Après avoir créé un groupe de disponibilité, ajoutez l’équilibrage de charge hello toohello de l’adresse IP, puis configurez port d’écoute hello.

tooadd un équilibrage de charge de tooa d’adresse IP avec hello portail Azure, procédez comme hello suivant :

1. Bonjour portail Azure, ouvrez le groupe de ressources hello qui contient l’équilibrage de charge hello, puis cliquez sur équilibrage de charge hello. 

2. Sous **PARAMÈTRES**, cliquez sur **Pool d’adresses IP frontales** puis cliquez sur **Ajouter**. 

3. Sous **ajouter une adresse IP de serveur frontal**, attribuez un nom de serveur frontal hello. 

4. Vérifiez que hello **réseau virtuel** et hello **sous-réseau** sont hello identique hello des instances de SQL Server.

5. Définissez adresse IP hello écouteur de hello. 
   
   >[!TIP]
   >Vous pouvez définir hello IP adresse toostatic et tapez une adresse qui n’est pas utilisée actuellement dans le sous-réseau de hello. Ou bien, vous pouvez définir des hello IP adresse toodynamic et enregistrer le nouveau pool IP frontale hello. Lorsque vous procédez ainsi, hello portail Azure affecte automatiquement un pool de toohello d’adresses IP disponible. Vous pouvez rouvrir le pool d’adresses IP frontal hello et modifier hello affectation toostatic. 

6. Enregistrer l’adresse IP de hello pour le port d’écoute hello. 

7. Ajouter une sonde d’intégrité à l’aide de hello suivant les paramètres :

   |Paramètre |Valeur
   |:-----|:----
   |**Name** |Une sonde de hello tooidentify de nom.
   |**Protocole** |TCP
   |**Port** |Un port TCP non utilisé doit être disponible sur toutes les machines virtuelles. Il ne peut pas être utilisé à d’autres fins. Aucun deux écouteurs ne peuvent utiliser hello même port de la sonde. 
   |**Intervalle** |Durée Hello entre sonde tentatives. Utilisez la valeur par défaut de hello (5).
   |**Seuil de défaillance sur le plan de l’intégrité** |nombre de Hello de seuils consécutifs qui doivent échouer avant un ordinateur virtuel est considéré comme non intègre.

8. Cliquez sur **OK** sonde de hello toosave. 

9. Créez une règle d’équilibrage de charge. Cliquez sur **Règles d’équilibrage de charge** puis sur **Ajouter**.

10. Configurer hello nouvelle équilibrage de charge règle à l’aide de hello suivant les paramètres :

   |Paramètre |Valeur
   |:-----|:----
   |**Name** |Un Bonjour tooidentify de nom de règle d’équilibrage de charger. 
   |**Adresse IP du serveur frontal** |Sélectionnez l’adresse IP de hello que vous avez créé. 
   |**Protocole** |TCP
   |**Port** |Utiliser le port hello qui utilisent des instances de SQL Server hello. Une instance par défaut utilise le port 1433, à moins que vous l’ayez changé. 
   |**Port principal** |Hello d’utiliser les mêmes valeurs que **Port**.
   |**Pool back-end** |pool Hello qui contient des machines virtuelles de hello avec des instances de SQL Server hello. 
   |**Sonde d’intégrité** |Choisissez la sonde hello que vous avez créé.
   |**Persistance de session** |Aucun
   |**Délai d’inactivité (minutes).** |Valeur par défaut (4)
   |**Adresse IP flottante (retour direct du serveur)** | Activé

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Configurer hello disponibilité groupe toouse hello nouvelle adresse IP

toofinish de configuration de cluster de hello, répétition hello étapes lorsque vous avez effectué le premier groupe de disponibilité hello. Autrement dit, configurer hello [toouse hello nouvelle adresse IP de cluster](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Après avoir ajouté une adresse IP pour le port d’écoute hello, configurez le groupe de disponibilité supplémentaires hello en procédant comme suit de hello : 

1. Vérifiez que le port de la sonde hello pour la nouvelle adresse IP de hello est ouvert sur les deux machines virtuelles de SQL Server. 

2. [Dans le Gestionnaire de Cluster, ajouter le point d’accès client hello](#addcap).

3. [Configurer les ressources IP de hello pour le groupe de disponibilité hello](#congroup).

   >[!IMPORTANT]
   >Lorsque vous créez des adresses IP de hello, utiliser l’adresse IP de hello que vous avez ajouté l’équilibrage de charge toohello.  

4. [Rendre les ressources de groupe de disponibilité de SQL Server hello dépendante sur le point d’accès client hello](#dependencyGroup).

5. [Hello d’accès client aux ressources dépendant de l’adresse IP de hello de point](#listname).
 
6. [Définir les paramètres de cluster hello dans PowerShell](#setparam).

Après avoir configuré hello disponibilité groupe toouse hello nouvelle adresse IP, configurez l’écouteur de toohello de connexion de hello. 

## <a name="next-steps"></a>Étapes suivantes

- [Configurer un groupe de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure dans des régions différentes](virtual-machines-windows-portal-sql-availability-group-dr.md)
