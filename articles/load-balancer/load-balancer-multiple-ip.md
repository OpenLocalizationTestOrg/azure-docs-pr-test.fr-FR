---
title: "aaaLoad équilibrage sur plusieurs configurations IP dans Azure | Documents Microsoft"
description: "Équilibrage de charge sur des configurations IP principales et secondaires."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Équilibrage sur plusieurs configurations IP à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> * [Portail](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [INTERFACE DE LIGNE DE COMMANDE](load-balancer-multiple-ip-cli.md)

Cet article décrit comment toouse équilibrage de charge Azure avec adresse IP de plusieurs adresses sur une interface réseau secondaire (NIC). Pour ce scénario, nous avons deux machines virtuelles exécutant Windows, chacun avec un serveur principal et une seconde. Chacun des hello secondaire cartes réseau ont deux configurations IP. Chaque machine virtuelle héberge les deux sites web contoso.com et fabrikam.com. Chaque site Web est lié tooone de configurations IP hello hello seconde. Nous utilisons équilibrage de charge Azure tooexpose deux frontal adresses IP, une pour chaque site Web, toodistribute toohello respectifs IP configuration du trafic pour le site Web de hello. Ce scénario utilise hello même numéro de port entre les serveurs frontaux, ainsi que les deux adresses IP du pool principal.

![Image du scénario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Composants requis
Cet exemple suppose que vous disposez d’un groupe de ressources nommé *contosofabrikam* avec hello configuration suivante :
 -  inclut un réseau virtuel nommé *myVNet*, deux machines virtuelles appelés *VM1* et *VM2* respectivement dans hello même groupe à haute disponibilité nommée *myAvailset*. 
 - Chaque machine virtuelle possède une carte réseau principale et une carte réseau secondaire. Hello principal cartes réseau est nommées *VM1NIC1* et *VM2NIC1* et base de données secondaire hello cartes réseau est nommées *VM1NIC2* et *VM2NIC2*. Pour plus d’informations sur la création de machines virtuelles avec plusieurs cartes réseau, consultez [Créer une machine virtuelle avec plusieurs cartes réseau à l’aide de PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Solde de tooload étapes sur plusieurs configurations IP

Suivez ces étapes ci-dessous le scénario de hello tooachieve présentée dans cet article :

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>ÉTAPE 1 : Configurer hello NIC secondaire pour chaque machine virtuelle

Pour définir la configuration IP pour chaque machine virtuelle dans votre réseau virtuel, hello NIC secondaire comme suit :  

1. À partir d’un navigateur, accédez toohello portail Azure : http://portal.azure.com et connectez-vous avec votre compte Azure.
2. Sur hello supérieur gauche de l’écran hello, cliquez sur icône du groupe de ressources hello, puis cliquez sur hello de groupe de ressources hello machines virtuelles sont situés dans (par exemple, *contosofabrikam*). Hello **groupes de ressources** panneau qui répertorie toutes les ressources hello en même temps que les interfaces réseau de hello pour les machines virtuelles de hello est maintenant affichée.
3. toohello secondaire carte réseau de chaque machine virtuelle, ajoutez une configuration IP en procédant comme suit :
    1. Sélectionnez l’interface réseau hello que vous souhaitez tooadd hello configuration IP.
    2. Dans hello panneau qui s’affiche pour hello carte réseau que vous avez sélectionné, cliquez sur **configurations IP**. Puis cliquez sur **ajouter** vers le haut hello du panneau hello qui s’affiche.
    3. Bonjour **configurations d’ajouter une adresse IP** panneau, ajoutez une deuxième toohello de configuration IP réseau comme suit : 
        1. Tapez un nom pour votre configuration IP secondaire (par exemple, pour le nom de VM1 et VM2 hello configurations IP en tant que *VM1NIC2-ipconfig2* et *VM2NIC2-ipconfig2* respectivement).
        2. Dans **Private IP address (Adresse IP privée)**, pour **Allocation**, sélectionnez **Statique**.
        3. Cliquez sur **OK**.
        4. Lorsque hello deuxième configuration IP pour hello NIC secondaire est terminée, elle est affichée dans hello **configurations IP** Panneau de paramètres pour hello donné de carte réseau.

### <a name="step-2-create-a-load-balancer"></a>ÉTAPE 2 : Créer un équilibrage de charge

Créez un équilibrage de charge comme suit :

1. À partir d’un navigateur, accédez toohello portail Azure : http://portal.azure.com et connectez-vous avec votre compte Azure.
2. Dans hello supérieur gauche de l’écran hello, cliquez sur **nouveau** > **réseau** > **équilibrage de charge**. Ensuite, cliquez sur **Créer**.
3. Bonjour **équilibrage de charge créer** panneau, tapez un nom pour votre équilibreur de charge. Ici, il s’appelle *myLoadBalancer*.
4. Sous Public IP Address (Adresse IP publique), créez une adresse IP publique appelée **myPublicIP1**.
5. Sous le groupe de ressources, sélectionnez hello groupe de ressources existant de vos machines virtuelles (par exemple, *contosofabrikam*). Ensuite, sélectionnez l’emplacement approprié, puis cliquez sur **OK**. équilibrage de charge Hello commence ensuite à toodeploy et prendra quelques minutes toosuccessfully complète de déploiement.
6. Une fois déployé, l’équilibrage de charge hello s’affiche en tant que ressource dans votre groupe de ressources.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>ÉTAPE 3 : Configurer le pool d’adresses IP de serveur frontal de hello

Configurez votre pool IP frontal pour chaque site Web (Contoso et Fabrikam) comme suit :

1. Dans le portail de hello, cliquez sur **davantage de services** > type **adresse IP publique** dans hello zone de filtre, puis cliquez sur **des adresses IP publiques**. Cliquez sur **ajouter** vers le haut hello du panneau hello qui s’affiche.
2. Configurez deux adresses IP publiques (*PublicIP1* et *PublicIP2*) pour les deux sites Web (contoso et fabrikam) comme suit :
    1. Tapez le nom de votre adresse IP frontale.
    2. Pour **groupe de ressources**, sélectionnez hello groupe de ressources existant de hello machines virtuelles (par exemple, *contosofabrikam*).
    3. Pour **emplacement**, sélectionnez hello même emplacement que hello des machines virtuelles.
    4. Cliquez sur **OK**.
    5. Une fois que les adresses IP publiques de hello deux sont créés, ils sont tous deux affichés dans hello **adresse IP publique** panneau d’adresses.
3. Dans le portail de hello, cliquez sur **davantage de services** > type **l’équilibrage de charge** dans hello zone de filtre, puis cliquez sur **équilibrage de charge**.  
4. Sélectionnez l’équilibrage de charge hello (*mylb*) que vous souhaitez tooadd hello frontal IP pool.
5. Sous **Paramètres**, sélectionnez **Frontend Pools (Pools frontaux)**. Puis cliquez sur **ajouter** vers le haut hello du panneau hello qui s’affiche.
6. Tapez le nom de votre adresse IP frontale (*farbikamfe* ou **contosofe*).
7. Cliquez sur **adresse IP** et hello **adresse de choisir une adresse IP publique** panneau, les adresses IP de hello Sélectionnez pour votre serveur frontal (*PublicIP1* ou *PublicIP2*).
8. Répétez too7 étapes 3 dans cette section toocreate hello deuxième serveur frontal adresse IP.
9. Lors de la configuration de pool IP hello frontale est terminée, les deux adresses IP de serveur frontal sont affichés dans hello **Pool d’adresses IP de serveur frontal** Panneau de votre équilibreur de charge. 
    
### <a name="step-4-configure-hello-backend-pool"></a>ÉTAPE 4 : Configurer le pool principal d’hello   
Configurez les pools d’adresses hello principaux de votre équilibreur de charge pour chaque site Web (Contoso et Fabrikam) comme suit :
        
1. Dans le portail de hello, cliquez sur **davantage de services** > Équilibrage de charge dans la zone de filtre hello, puis tapez **équilibrage de charge**.  
2. Sélectionnez l’équilibrage de charge hello (*mylb*) que vous souhaitez tooadd hello principal pools.
3. Sous **Paramètres**, sélectionnez **Backend Pools (Pools principaux)**. Tapez le nom de votre pool principal (par exemple, *contosopool* ou *fabrikampool*). Puis cliquez sur hello **ajouter** bouton vers le haut hello du panneau hello qui s’affiche. 
4. Dans **Associated to (Associé à)**, sélectionnez **Availability set (Groupe à haute disponibilité)**.
5. Dans **Availability set (Groupe à haute disponibilité)**, sélectionnez **myAvailset**.
6. Ajoutez les configurations IP réseau cibles pour les deux machines virtuelles comme suit (voir la figure 2) :  
    1. Pour **machine virtuelle cible**, sélectionnez hello machine virtuelle que vous souhaitez tooadd toohello principal pool (par exemple, VM1 ou VM2).
    2. Pour **configuration IP de réseau**, sélectionnez configuration IP des cartes d’interface réseau secondaire de hello pour cette machine virtuelle (par exemple, VM1NIC2-ipconfig2 ou VM2NIC2-ipconfig2).
    ![Image du scénario LB](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Figure 2**: configuration d’équilibrage de charge hello avec pools principaux  
7. Cliquez sur **OK**.
8. Lors de la configuration du pool principal hello est terminée, les deux pools d’adresses principaux sont affichés dans hello **panneau du pool principal** de votre équilibreur de charge.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>ÉTAPE 5 : Configuration d’une sonde d’intégrité pour votre équilibrage de charge
Configurez une sonde d’intégrité pour votre équilibrage de charge comme suit :
    1. Dans le portail hello, cliquez sur plus de services > Équilibrage de charge dans la zone de filtre hello, puis tapez **équilibrage de charge**.  
    2. Sélectionnez l’équilibrage de charge hello tooadd hello principal pools souhaitées.
    3. Sous **Paramètres**, sélectionnez **Health Probe (Sonde d’intégrité)**. Puis cliquez sur **ajouter** vers le haut hello du panneau hello qui s’affiche.
    4. Tapez un nom pour la sonde d’intégrité hello (par exemple, HTTP), puis cliquez sur **OK**.

### <a name="step-6-configure-load-balancing-rules"></a>ÉTAPE 6 : Configurer les règles d’équilibrage de charge
Configurez les règles d’équilibrage de charge (*HTTPc* et *HTTPf*) pour chaque site Web comme suit :
    
1. Sous **Paramètres**, sélectionnez **Health Probe (Sonde d’intégrité)**. Puis cliquez sur **ajouter** vers le haut hello du panneau hello qui s’affiche.
2. Pour **nom**, tapez un nom pour la règle d’équilibrage de charge hello (par exemple, *HTTPc* pour Contoso, ou *HTTPf* pour Fabrikam)
3. Pour l’adresse IP de Frontend, sélectionnez l’adresse IP de hello hello frontale (par exemple *Contosofe* ou *Fabrikamfe*)
4. Pour **Port** et **port principal**, conservez la valeur par défaut de hello **80**.
5. Dans **Adresse IP flottante (retour serveur direct)**, cliquez sur **Activé**.
6. Cliquez sur **OK**.
7. Répétez too6 étapes 1 au sein de cette règle d’équilibrage de charge deuxième section toocreate hello.
8. Lorsque l’équilibrage de charge hello règles de configuration est terminée, les deux règles ((*HTTPc* et *HTTPf*) sont affichés dans hello **règles d’équilibrage de charge** Panneau de votre équilibreur de charge.

### <a name="step-7-configure-dns-records"></a>ÉTAPE 7 : Configurer les enregistrements DNS
Enfin, vous devez configurer DNS ressource enregistrements toopoint toohello respectifs adresse IP frontale d’équilibrage de charge hello. Vous pouvez héberger vos domaines dans Azure DNS. Pour plus d’informations sur l’utilisation d’Azure DNS avec un équilibrage de charge, voir [Utiliser Azure DNS avec d’autres services Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur le fonctionnement des services de l’équilibrage de charge toocombine dans Azure dans [à l’aide des services d’équilibrage de charge dans Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Découvrez comment vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes d’équilibrage de charge dans [journal analytique pour l’équilibrage de charge Azure](../load-balancer/load-balancer-monitor-log.md).
