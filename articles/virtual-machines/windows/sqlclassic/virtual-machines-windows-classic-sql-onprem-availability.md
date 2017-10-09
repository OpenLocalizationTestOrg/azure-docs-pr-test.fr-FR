---
title: "aaaExtend local tooAzure de groupes de disponibilité AlwaysOn | Documents Microsoft"
description: "Ce didacticiel utilise des ressources créées avec le modèle de déploiement classique hello et décrit comment toouse hello Assistant Ajouter un réplica dans SQL Server Management Studio (SSMS) tooadd un réplica de groupe de disponibilité AlwaysOn dans Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Étendre tooAzure de groupes de disponibilité AlwaysOn local
Les groupes de disponibilité Always On fournissent une haute disponibilité pour les groupes de bases de données en ajoutant des réplicas secondaires. Ces réplicas autorisent le basculement des bases de données en cas de défaillance. En outre, ils peuvent être utilisé toooffload lire les charges de travail ou des tâches de sauvegarde.

Vous pouvez étendre tooMicrosoft de groupes de disponibilité local Azure en configuration d’un ou plusieurs machines virtuelles Azure avec SQL Server puis en les ajoutant comme réplicas tooyour localement les groupes de disponibilité.

Ce didacticiel suppose que vous avez hello suivantes :

* Un abonnement Azure actif. Vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Un groupe de disponibilité Always On local existant. Pour plus d’informations sur les groupes de disponibilité, voir [Groupes de disponibilité Always On](https://msdn.microsoft.com/library/hh510230.aspx).
* Connectivité entre hello sur site réseau et votre réseau virtuel Azure. Pour plus d’informations sur la création de ce réseau virtuel, consultez [à l’aide de la création d’un Site à Site connexion hello portail Azure (classique)](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

## <a name="add-azure-replica-wizard"></a>assistant Add Azure Replica
Cette section vous montre comment toouse hello **Assistant Ajouter un réplica** tooextend votre tooinclude de solution de groupe de disponibilité AlwaysOn Azure réplicas.

> [!IMPORTANT]
> Hello **Assistant Ajouter un réplica** prend uniquement en charge les ordinateurs virtuels créés avec le modèle de déploiement classique hello. Nouveaux déploiements d’ordinateurs virtuels doivent utiliser le modèle de gestionnaire de ressources hello plus récent. Si vous utilisez des machines virtuelles avec le Gestionnaire de ressources, vous devez ajouter manuellement hello secondaire un réplica Windows Azure à l’aide de commmands Transact-SQL (non illustré ici). Cet Assistant ne fonctionnera pas dans le scénario du Gestionnaire de ressources hello.

1. Dans SQL Server Management Studio, développez **Haute disponibilité Always On** > **Groupes de disponibilité** > **[Nom de votre groupe de disponibilité]**.
2. Cliquez avec le bouton droit sur **Réplicas de disponibilité**, puis sélectionnez **Ajouter un réplica**.
3. Par défaut, hello **tooAvailability d’ajouter un réplica groupe Assistant** s’affiche. Cliquez sur **Suivant**.  Si vous avez sélectionné hello **ne plus afficher cette page** option bas hello de page de hello au démarrage précédent de l’Assistant, cet écran ne sera pas affichée.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. Vous serez requis tooconnect tooall des réplicas secondaires existants. Cliquez sur **Connecter...** en regard de chaque réplica, ou vous pouvez cliquer sur **Connecter tout...** bas hello écran hello. Après l’authentification, cliquez sur **suivant** écran suivant de tooadvance toohello.
5. Sur hello **spécifier les réplicas** page, plusieurs onglets figurent en haut de hello : **réplicas**, **points de terminaison**, **préférences de sauvegarde**, et **Écouteur**. À partir de hello **réplicas** , cliquez sur **ajouter un réplica Azure...** toolaunch hello Assistant Ajouter un réplica.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Sélectionnez un certificat de gestion Azure existant à partir du magasin de certificats Windows hello local si vous avez installé une auparavant. Sélectionnez ou entrez les id hello d’un abonnement Azure si vous avez utilisé une auparavant. Vous pouvez cliquez sur téléchargement toodownload et installer un certificat de gestion Azure et télécharger la liste hello d’abonnements à l’aide d’un compte Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Vous renseignez chaque champ sur la page hello avec les valeurs qui seront utilisées toocreate hello Azure Virtual Machine (VM) qui héberge le réplica de hello.
   
   | Paramètre | Description |
   | --- | --- |
   | **Image** |Sélectionnez la combinaison hello souhaité de système d’exploitation et SQL Server |
   | **Taille de la machine virtuelle** |Sélectionnez la taille de machine virtuelle qui convient le mieux à vos besoins professionnels hello |
   | **Nom de la machine virtuelle** |Spécifiez un nom unique pour hello nouvelle machine virtuelle. Hello doit contenir entre 3 et 15 caractères, peut contenir uniquement des lettres, des chiffres et des traits d’union et doit commencer par une lettre et se terminer par une lettre ou un chiffre. |
   | **Nom d’utilisateur de la machine virtuelle** |Spécifiez un nom d’utilisateur qui deviendra le compte d’administrateur hello hello machine virtuelle |
   | **Mot de passe administrateur de la machine virtuelle** |Spécifiez un mot de passe pour le nouveau compte de hello |
   | **Confirmer le mot de passe** |Confirmer le mot de passe hello du nouveau compte de hello |
   | **Réseau virtuel** |Spécifiez hello du réseau virtuel Azure que hello nouvelle machine virtuelle doit utiliser. Pour plus d’informations sur les réseaux virtuels, voir [Présentation du réseau virtuel](../../../virtual-network/virtual-networks-overview.md). |
   | **Sous-réseau de réseau virtuel** |Spécifiez un sous-réseau de réseau virtuel hello que hello que nouvelle machine virtuelle doit utiliser |
   | **Domaine** |Confirmer la valeur par défaut pour le domaine de hello hello est correct |
   | **Nom d’utilisateur de domaine** |Spécifiez un compte qui se trouve dans le groupe d’administrateurs locaux hello sur les nœuds de cluster local hello |
   | **Mot de passe** |Spécifier un mot de passe hello pour nom d’utilisateur de domaine de hello |
8. Cliquez sur **OK** paramètres de déploiement toovalidate hello.
9. Les mentions légales s’affichent. Lisez et cliquez sur **OK** si vous acceptez toothese termes du contrat.
10. Hello **spécifier les réplicas** page s’affiche de nouveau. Vérifiez les paramètres de hello pour le nouveau réplica Azure hello sur hello **réplicas**, **points de terminaison**, et **préférences de sauvegarde** onglets. Modifier les paramètres toomeet besoins de votre entreprise.  Pour plus d’informations sur les paramètres de hello contenus dans ces onglets, consultez [Page spécifier les réplicas (nouvel Assistant groupe de disponibilité/ajouter de l’Assistant réplica)](https://msdn.microsoft.com/library/hh213088.aspx). Notez que les écouteurs ne peut pas être créés à l’aide d’onglet d’écouteur hello pour les groupes de disponibilité qui contiennent des réplicas Azure. En outre, si un écouteur existe déjà toolaunching préalable hello Assistant, vous recevrez un message indiquant qu’il n’est pas possible dans Azure. Nous allons aborder la façon dont les écouteurs toocreate hello **créer un écouteur de groupe de disponibilité** section.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. Cliquez sur **Suivant**.
12. Sélectionner la méthode de synchronisation de données hello souhaité toouse sur hello **sélectionner la synchronisation initiale des données** page, puis cliquez sur **suivant**. Pour la plupart des scénarios, sélectionnez **Synchronisation complète des données**. Pour plus d’informations sur les méthodes de synchronisation de données, voir [Page Sélectionner la synchronisation de données initiale (assistants de groupe de disponibilité AlwaysOn)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Passez en revue les résultats hello sur hello **Validation** page. Corrigez les problèmes et réexécuter la validation de hello si nécessaire. Cliquez sur **Suivant**.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Passez en revue les paramètres hello sur hello **Résumé** , puis cliquez sur **Terminer**.
15. Hello, processus de déploiement commence. Lorsque hello Assistant terminé, cliquez sur **fermer** tooexit en dehors de l’Assistant de hello.

> [!NOTE]
> Hello Assistant Ajouter un réplica Azure crée un fichier journal dans Users\User Name\AppData\Local\SQL Server\AddReplicaWizard. Ce fichier journal peut être de déploiements d’un réplica Windows Azure utilisé tootroubleshoot a échoué. Si hello Assistant échoue à l’exécution de n’importe quelle action, toutes les opérations précédentes sont restaurées, y compris la suppression hello configuré de machine virtuelle.
> 
> 

## <a name="create-an-availability-group-listener"></a>Créer un écouteur de groupe de disponibilité
Une fois le groupe de disponibilité hello a été créé, vous devez créer un écouteur pour les clients tooconnect toohello réplicas. Les écouteurs dirigent entrants hello tooeither connexions principal ou un réplica secondaire en lecture seule. Pour plus d’informations sur les écouteurs, voir [Configurer un écouteur à équilibrage de charge interne pour des groupes de disponibilité Always On dans Azure](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Étapes suivantes
Bonjour de toousing ajout **Assistant Ajouter un réplica** tooextend tooAzure de votre groupe de disponibilité AlwaysOn, vous pouvez également déplacer certaines charges de travail de SQL Server tooAzure complètement. tooget démarré, consultez [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur des Machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

