---
title: "aaaDeploy un équilibrage de charge connecté à Internet avec IPv6 - modèle Azure | Documents Microsoft"
description: "Comment toodeploy IPv6 prennent en charge pour l’équilibrage de charge Azure et d’équilibrage de la charge de machines virtuelles."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Déployer une solution d’équilibrage de charge sur Internet avec IPv6, à l’aide d’un modèle

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Interface de ligne de commande Azure](load-balancer-ipv6-internet-cli.md)
> * [Modèle](load-balancer-ipv6-internet-template.md)

Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP). équilibrage de charge Hello offre une haute disponibilité en répartissant le trafic entrant entre les instances de service intègre dans les services de cloud computing ou les machines virtuelles dans un jeu d’équilibrage de charge. Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.

## <a name="example-deployment-scenario"></a>Exemple de scénario de déploiement

Hello diagramme suivant illustre la solution d’équilibrage de charge de hello en cours de déploiement à l’aide du modèle d’exemple hello décrit dans cet article.

![Scénario d’équilibreur de charge](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

Dans ce scénario, vous allez créer hello suivant des ressources Azure :

* une interface de réseau virtuel pour chaque machine virtuelle avec des adresses IPv4 et IPv6 affectées ;
* un équilibrage de charge accessible sur Internet avec une adresse IP publique IPv4 et IPv6 ;
* deux charge équilibrage règles toomap hello VIP toohello privés points de terminaison publics
* un ensemble de disponibilité qui contient des machines virtuelles de hello deux
* deux machines virtuelles ;

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Déploiement du modèle hello avec hello portail Azure

Cet article fait référence à un modèle qui est publié dans hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) la galerie. Vous pouvez télécharger le modèle de hello à partir de la galerie de hello ou lancer le déploiement de hello dans Windows Azure directement à partir de la galerie de hello. Cet article suppose que vous avez téléchargé ordinateur local de hello modèle tooyour.

1. Ouvrez hello portail Azure et connectez-vous avec un compte qui dispose des autorisations toocreate machines virtuelles et des ressources réseau au sein d’un abonnement Azure. En outre, sauf si vous utilisez des ressources existantes, compte de hello doit autorisation toocreate un groupe de ressources et d’un compte de stockage.
2. Cliquez sur « + Nouveau » du menu de hello puis de type « modèle » dans la zone de recherche hello. Sélectionnez « Déploiement de modèle » hello résultats de recherche.

    ![lb-ipv6-portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. Dans hello tout ce panneau, cliquez sur « Déploiement de modèle ».

    ![lb-ipv6-portal-step3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. Cliquez sur « Créer ».

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. Cliquez sur « Modifier le modèle ». Supprimer le contenu existant de hello et copier/coller dans le contenu entier de hello hello du fichier de modèle (tooinclude hello de début et de fin {}), puis cliquez sur « Enregistrer ».

    > [!NOTE]
    > Si vous utilisez Microsoft Internet Explorer, lorsque vous collez vous recevez une boîte de dialogue vous demandant de Presse-papiers de Windows toohello tooallow accès. Click « Autoriser l’accès ».

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. Cliquez sur « Modifier les paramètres ». Dans le panneau de paramètres hello, spécifiez les valeurs de hello selon les recommandations de hello Bonjour section des paramètres de modèle, puis cliquez sur « Enregistrer » tooclose hello paramètres panneau. Dans le panneau de déploiement de personnalisée hello, sélectionnez votre abonnement, un groupe de ressources existant ou créez-en un. Si vous créez un groupe de ressources, puis sélectionnez un emplacement pour le groupe de ressources hello. Ensuite, cliquez sur **juridiques**, puis cliquez sur **achat** pour les conditions juridiques hello. Azure commence le déploiement de ressources de hello. Il prend plusieurs minutes toodeploy toutes les ressources hello.

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Pour plus d’informations sur ces paramètres, consultez hello [les variables et les paramètres de modèle](#template-parameters-and-variables) section plus loin dans cet article.

7. les ressources de hello toosee créées par le modèle de hello, cliquez sur Parcourir, faites défiler vers le bas la liste de hello jusqu'à ce que vous consultez « Groupes de ressources », puis cliquez dessus.

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. Dans Panneau de groupes de ressources hello, cliquez sur nom hello hello du groupe de ressources spécifié à l’étape 6. Vous voyez une liste de toutes les ressources hello qui ont été déployées. Si tout s’est bien passé, la mention « Réussi » apparaît en regard de « Dernier déploiement ». Si ce n’est pas le cas, vérifiez que hello votre compte dispose des ressources nécessaires d’autorisations toocreate hello.

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > Si vous accédez à vos groupes de ressources immédiatement après avoir terminé l’étape 6, « Dernier déploiement » affichera hello de « Déploiement » alors que les ressources hello sont déployées.

9. Cliquez sur « myIPv6PublicIP » dans la liste hello des ressources. Vous voyez qu’il possède une adresse IPv6 sous adresse IP, et que son nom DNS est la valeur hello spécifiée pour le paramètre de dnsNameforIPv6LbIP hello à l’étape 6. Cette ressource est hello publique IPv6 adresse et nom d’hôte qui est accessibles tooInternet-les clients.

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Valider la connectivité

Lorsque le modèle de hello a déployé avec succès, vous pouvez valider la connectivité en effectuant hello tâches suivantes :

1. Se connecter toohello portail Azure et se connecter tooeach Hello machines virtuelles créées par le déploiement du modèle hello. Si vous avez déployé une machine virtuelle Windows Server, exécutez ipconfig /all à partir d’une invite de commandes. Vous voyez que les machines virtuelles de hello ont les adresses IPv4 et IPv6. Si vous avez déployé des machines virtuelles Linux, vous devez tooconfigure hello du système d’exploitation Linux tooreceive IPv6 des adresses dynamiques à l’aide d’instructions hello fournies pour votre distribution Linux.
2. À partir d’un client connecté à Internet de IPv6, lancer une connexion toohello adresse IPv6 publique d’équilibrage de charge hello. tooconfirm qui hello d’équilibrage de charge est équilibrage de charge entre les machines virtuelles de hello deux, vous pouviez installer un serveur web, comme Microsoft Internet Information Services (IIS) sur chacune des machines virtuelles de hello. Hello page de web par défaut sur chaque serveur peut contenir le texte hello « Server0 » ou « Server1 » toouniquely l’identifier. Ensuite, ouvrez un navigateur Internet sur un client connecté à Internet IPv6 et rechercher le nom d’hôte toohello que vous avez spécifié pour le paramètre de dnsNameforIPv6LbIP hello de bout en bout tooconfirm hello charge équilibrage IPv6 connectivité tooeach machine virtuelle. Si vous voyez uniquement la page web de hello à partir d’un seul serveur, vous devrez peut-être tooclear cache de votre navigateur. Ouvrez plusieurs sessions de navigation privées. Une réponse pour chaque serveur doit s’afficher.
3. À partir d’un client connecté Internet IPv4, lancer une connexion toohello adresse IPv4 publique de l’équilibrage de charge hello. tooconfirm qui hello d’équilibrage de charge est l’équilibrage de charge hello deux machines virtuelles, vous pouvez tester à l’aide d’IIS, comme indiqué dans l’étape 2.
4. À partir de chaque machine virtuelle, lancer une connexion sortante tooan IPv6 ou un périphérique de connexion d’IPv4 Internet. Dans les deux cas, affiché par le périphérique de destination hello l’adresse IP source hello est hello publique adresse IPv4 ou IPv6 de l’équilibrage de charge hello.

> [!NOTE]
> ICMP pour IPv4 et IPv6 est bloqué dans hello réseau Azure. Par conséquent, les outils ICMP comme le test Ping sont toujours mis en échec. connectivité de tootest, utilisez une alternative TCP tels que TCPing ou hello applet de commande PowerShell Test-NetConnection. Notez que les adresses IP hello hello illustrés sont des exemples de valeurs que vous pouvez voir. Étant donné que les adresses IPv6 de hello sont attribuées de façon dynamique, adresses hello que vous recevez varient et peuvent varier par région. En outre, il est courant pour une adresse IPv6 publique hello sur toostart d’équilibrage de charge hello avec un préfixe différent que hello des adresses IPv6 privées dans le pool principal d’hello.

## <a name="template-parameters-and-variables"></a>Paramètres et variables de modèle

Un modèle Azure Resource Manager contient plusieurs variables et paramètres que vous pouvez personnaliser les besoins de tooyour. Les variables sont utilisés pour des valeurs fixes que vous ne voulez pas un toochange de l’utilisateur. Les paramètres sont utilisés pour les valeurs que vous souhaitez un tooprovide utilisateur lors du déploiement de modèle de hello. exemple de modèle de Hello est configuré pour le scénario hello décrit dans cet article. Vous pouvez personnaliser ce tooneeds de votre environnement.

exemple Hello modèle utilisé dans cet article inclut des éléments suivants de hello variables et des paramètres :

| Paramètre / Variable | Remarques |
| --- | --- |
| adminUsername |Spécifier le nom hello du compte d’administrateur hello utilisé toosign dans des machines virtuelles toohello avec. |
| adminPassword |Spécifiez un mot de passe hello pour le compte d’administrateur hello utilisé toosign dans des machines virtuelles toohello avec. |
| dnsNameforIPv4LbIP |Spécifiez le nom d’hôte DNS hello souhaité tooassign comme nom de public hello d’équilibrage de charge hello. Ce nom résout l’adresse IPv4 publique de l’équilibreur de charge toohello. nom de Hello doit être en minuscules et correspond à hello regex : ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Spécifiez le nom d’hôte DNS hello souhaité tooassign comme nom de public hello d’équilibrage de charge hello. Ce nom résout l’adresse IPv6 de l’équilibrage de charge toohello. nom de Hello doit être en minuscules et correspond à hello regex : ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Il peut s’agir hello même nom que l’adresse IPv4 de hello. Lorsqu’un client envoie une requête DNS pour ce nom Azure retournera hello A et enregistrements AAAA lorsque le nom de hello est partagé. |
| vmNamePrefix |Spécifiez le préfixe du nom de machine virtuelle hello. modèle de Hello ajoute un numéro (0, 1, etc.) toohello nom lorsque hello les machines virtuelles sont créées. |
| nicNamePrefix |Spécifiez le préfixe de nom interface hello réseau. modèle de Hello ajoute un numéro (0, 1, etc.) toohello nom lors de la création des interfaces réseau de hello. |
| storageAccountName |Entrez le nom hello d’un compte de stockage existant ou spécifier nom hello d’un une toobe nouvelle créée par le modèle de hello. |
| availabilitySetName |Entrez le nom de la disponibilité de hello définir toobe utilisé avec hello machines virtuelles |
| addressPrefix |préfixe d’adresse Hello utilisé la plage d’adresses toodefine hello Hello réseau virtuel |
| subnetName |nom de Hello du sous-réseau hello dans créé pour hello réseau virtuel |
| subnetPrefix |préfixe d’adresse Hello utilisé toodefine hello plage d’adresses hello sous-réseau |
| vnetName |Spécifiez nom hello hello réseau virtuel utilisé par hello machines virtuelles. |
| ipv4PrivateIPAddressType |méthode d’allocation de Hello utilisé hello privé adresse IP (statique ou dynamique) |
| ipv6PrivateIPAddressType |méthode d’allocation de Hello utilisé hello privé à l’adresse IP (dynamique). IPv6 prend uniquement en charge l’allocation dynamique. |
| numberOfInstances |nombre de Hello de charge équilibrée instances déployées par le modèle de hello |
| ipv4PublicIPAddressName |Indiquez le hello DNS nom toocommunicate toouse avec une adresse IPv4 publique hello d’équilibrage de charge hello. |
| ipv4PublicIPAddressType |méthode d’allocation de Hello utilisée pour hello adresse IP publique (statique ou dynamique) |
| Ipv6PublicIPAddressName |Indiquez le hello DNS nom toocommunicate toouse avec les adresses IPv6 publique hello d’équilibrage de charge hello. |
| ipv6PublicIPAddressType |méthode d’allocation Hello utilisé pour hello d’adresse IP publique (dynamique). IPv6 prend uniquement en charge l’allocation dynamique. |
| lbName |Spécifiez le nom hello d’équilibrage de charge hello. Ce nom est affiché dans le portail de hello ou lorsqu’il se rapporte tooit avec une commande CLI ou PowerShell. |

autres variables de Hello dans le modèle de hello contiennent des valeurs dérivées qui sont affectés lorsque Azure crée des ressources de hello. Ne modifiez pas ces variables.
