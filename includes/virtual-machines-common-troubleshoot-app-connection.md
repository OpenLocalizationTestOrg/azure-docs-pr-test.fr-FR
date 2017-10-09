Il existe différentes raisons lorsque vous ne pouvez pas démarrer ou application de tooan s’exécutant sur une machine virtuelle Azure (VM). Raisons incluent l’application hello ne pas en cours d’exécution ou à l’écoute sur les ports hello attendu, hello écoute le port bloqué, ou n’est pas correctement en passant application toohello au trafic des règles de mise en réseau. Cet article décrit une approche méthodique toofind et un problème de hello correct.

Si vous rencontrez des problèmes de connexion tooyour machine virtuelle à l’aide du protocole RDP ou SSH, consultez hello suivantes tout d’abord les articles :

* [Résoudre les problèmes de tooa des connexions Bureau à distance basé sur Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Résoudre les problèmes de SSH (Secure Shell) connexions tooa basés sur Linux machine virtuelle Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../articles/resource-manager-deployment-model.md). Cet article couvre l’utilisation de ces deux modèles, mais Microsoft recommande que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.

## <a name="quick-start-troubleshooting-steps"></a>Étapes de dépannage rapide
Si vous avez des problèmes de connexion tooan application, essayez de hello suivant les étapes de dépannage générales. Après chaque étape, essayez l’application tooyour connexion :

* Redémarrer la machine virtuelle de hello
* Recréez le point de terminaison hello, des règles de pare-feu, règles de sécurité de groupe (NSG) du réseau
  * [Modèle Resource Manager : gérer les groupes de sécurité réseau](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Modèle Classic : gérer les points de terminaison Cloud Services](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Connectez-vous à partir d’un emplacement différent, tel qu’un autre réseau virtuel Azure.
* Redéployer la machine virtuelle de hello
  * [Redéployez la machine virtuelle Windows.](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Redéployer la machine virtuelle Linux.](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Recréer la machine virtuelle de hello

Pour plus d'informations, consultez [Résolution des problèmes de connectivité de point de terminaison (échecs RDP/SSH/HTTP, etc.)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Vue d’ensemble détaillée de la résolution de problèmes
Il existe quatre domaines principaux l’accès hello tootroubleshoot d’une application qui s’exécute sur une machine virtuelle Azure.

![dépannage - impossible de démarrer l’application](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. application Hello en cours d’exécution sur hello machine virtuelle Azure.
   * Application hello lui-même s’exécute correctement ?
2. Hello machine virtuelle Azure.
   * Hello machine virtuelle fonctionne correctement et répondre toorequests ?
3. Points de terminaison réseau Azure.
   * Nuage de points de terminaison de service pour les machines virtuelles dans le modèle de déploiement classique hello.
   * Groupes de sécurité réseau et règles NAT de trafic entrant pour les machines virtuelles dans le modèle de déploiement Resource Manager.
   * Peut le trafic à partir des utilisateurs toohello/application de machine virtuelle sur les ports hello attendu ?
4. Votre périphérique de périmètre Internet.
   * Les règles de pare-feu en place empêchent-elles la circulation correcte du trafic ?

Pour les ordinateurs clients qui accèdent à application hello via une connexion ExpressRoute ou VPN de site à site, les zones principales hello qui peuvent entraîner des problèmes sont application hello et hello machine virtuelle Azure.

toodetermine hello source hello problème et sa correction, procédez comme suit.

## <a name="step-1-access-application-from-target-vm"></a>Étape 1 : Accéder à une application à partir de la machine virtuelle cible
Essayez l’application hello tooaccess avec le programme client approprié de hello VM hello sur lequel il est en cours d’exécution. Utiliser le nom d’hôte local hello, l’adresse IP locale hello ou adresse de bouclage hello (127.0.0.1).

![Démarrer l’application directement à partir de la machine virtuelle de hello](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Par exemple, si l’application hello est un serveur web, ouvrez un navigateur sur hello machine virtuelle et recommencez tooaccess une page web hébergée sur hello machine virtuelle.

Si vous pouvez accéder à application hello, passez trop[étape 2](#step2).

Si vous ne pouvez pas accéder à application hello, vérifiez hello suivant les paramètres :

* application Hello est en cours d’exécution sur la machine virtuelle cible hello.
* application Hello est à l’écoute sur les ports TCP et UDP hello attendu.

Sur Windows et les ordinateurs virtuels Linux, utilisez hello **netstat** commande tooshow hello de ports d’écoute actives. Examinez la sortie hello pour les ports hello attendu sur lequel votre application doit être à l’écoute. Redémarrez l’application hello ou configurer les ports toouse hello prévu en fonction des besoins et réessayez l’application de hello tooaccess localement.

## <a id="step2"></a>Étape 2 : Accéder à une application à partir d’une autre machine virtuelle Bonjour même réseau virtuel
Essayez d’application de hello tooaccess à partir d’une machine virtuelle différente, mais dans hello même réseau virtuel, à l’aide du nom d’hôte de la machine virtuelle hello ou son Azure-public, private ou fournisseur d’adresse IP attribuée par. Pour les ordinateurs virtuels créés à l’aide du modèle de déploiement classique de hello, n’utilisez pas hello adresse IP publique du service de cloud computing hello.

![démarrer l’application à partir d’une autre machine virtuelle](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Par exemple, si l’application hello est un serveur web, tooaccess réessayer une page web à partir d’un navigateur sur un autre ordinateur virtuel hello même réseau virtuel.

Si vous pouvez accéder à application hello, passez trop[étape 3](#step3).

Si vous ne pouvez pas accéder à application hello, vérifiez hello suivant les paramètres :

* pare-feu d’hôte Hello sur la cible de hello machine virtuelle permet aux demandes entrantes de hello et le trafic de réponse sortante.
* Détection d’intrusion ou des logiciels en cours d’exécution sur la cible de hello VM d’analyse réseau autorise le trafic de hello.
* Points de terminaison de Services cloud ou des groupes de sécurité réseau sont nombreuses à autoriser le trafic de hello :
  * [Modèle Classic : gérer les points de terminaison Cloud Services](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Modèle Resource Manager : gérer les groupes de sécurité réseau](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Un composant distinct qui s’exécute dans votre machine virtuelle dans le chemin d’accès hello entre les tests hello machine virtuelle et votre machine virtuelle, tel qu’un équilibrage de charge ou un pare-feu, autorisez le trafic de hello.

Sur un ordinateur virtuel basé sur Windows, utilisez le pare-feu Windows avec fonctions avancées de sécurité toodetermine si les règles de pare-feu hello exclure du trafic entrant et sortant de votre application.

## <a id="step3"></a>Étape 3 : Accéder à une application de réseau virtuel de hello externe
Essayez l’application hello de tooaccess à partir d’un ordinateur en dehors du réseau virtuel de hello en tant que machine virtuelle de hello sur lequel l’application hello s’exécute. Utilisez un réseau différent de celui de votre ordinateur client d’origine.

![Démarrer l’application à partir d’un ordinateur en dehors du réseau virtuel de hello](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Par exemple, si l’application hello est un serveur web, essayez de tooaccess hello web page à partir d’un navigateur en cours d’exécution sur un ordinateur qui n’est pas dans le réseau virtuel de hello.

Si vous ne pouvez pas accéder à application hello, vérifiez hello suivant les paramètres :

* Pour les ordinateurs virtuels créés à l’aide du modèle de déploiement classique hello :
  
  * Vérifiez que hello que VM autorise le passage du trafic entrant hello, en particulier les protocole hello (TCP ou UDP) et les numéros de port public et privé hello dans la configuration de point de terminaison hello.
  * Vérifiez que les listes de contrôle d’accès (ACL) sur le point de terminaison hello n’empêchent pas le trafic entrant à partir de hello Internet.
  * Pour plus d’informations, consultez [comment tooSet des points de terminaison tooa Machine virtuelle](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Pour les machines virtuelles créées à l’aide du modèle de déploiement du Gestionnaire de ressources hello :
  
  * Vérifiez que hello configuration des règles NAT entrante pour hello que VM autorise le passage du trafic entrant hello, en particulier les protocole hello (TCP ou UDP) et les numéros de port public et privé hello.
  * Vérifiez que les groupes de sécurité réseau sont permettant demande entrante de hello et le trafic de réponse sortante.
  * Pour plus d’informations, voir [Présentation du groupe de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md)

Si l’ordinateur virtuel de hello ou un point de terminaison est un membre d’un jeu d’équilibrage de charge :

* Vérifiez que le protocole de sonde hello (TCP ou UDP) et le numéro de port sont corrects.
* Si hello sonde protocole et port est différent de celui hello un équilibrage de charge protocole et port :
  * Vérifiez qu’application hello écoute sur le protocole de sonde hello (TCP ou UDP) et le numéro de port (utilisez **netstat – a** sur hello la machine virtuelle cible).
  * Vérifiez que le pare-feu hôte hello sur cible hello que VM autorise demande de sonde entrants hello et le trafic de réponse de sonde sortant.

Si vous pouvez accéder à application hello, assurez-vous que votre périphérique de périmètre Internet autorise le passage :

* Hello sortant application demande le trafic à partir de votre toohello d’ordinateur client machine virtuelle Azure.
* Bonjour le trafic de réponse entrant d’application à partir de la machine virtuelle Azure de hello.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Si l’application hello, utiliser les paramètres de hello IP Vérifiez toocheck Impossible d’accéder à l’étape 4. 

Pour plus d’informations, consultez [Vue d’ensemble de la surveillance réseau Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Ressources supplémentaires
[Résoudre les problèmes de tooa des connexions Bureau à distance basé sur Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Résoudre les problèmes de SSH (Secure Shell) connexions tooa basés sur Linux machine virtuelle Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

