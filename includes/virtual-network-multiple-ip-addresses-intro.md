> [!div class="op_single_selector"]
> * [Portail](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Modèle](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Une Machine virtuelle Azure (VM) possède une ou plusieurs interfaces réseau (NIC) joint tooit. Une carte réseau peut avoir l’une ou plus statique ou dynamique publiques et privées adresses tooit attribué. L’attribution d’IP de plusieurs adresses tooa machine virtuelle active hello suivant de fonctionnalités :

* D’héberger plusieurs sites web ou services avec des adresses IP différentes et des certificats SSL sur un serveur unique.
* de jouer le rôle d’une appliance virtuelle réseau, telle qu’un pare-feu ou un équilibreur de charge.
* Bonjour tooadd possibilité toutes de l’adresse IP privée hello les adresses pour une des cartes réseau de hello tooan pool principal d’équilibreur de charge Azure. Bonjour passé, hello uniquement une adresse IP principale pour hello que carte réseau principale peut être ajouté pool principal de tooa. toolearn en savoir plus sur comment tooload équilibrer plusieurs configurations IP, lire hello [plusieurs configurations IP d’équilibrage de la charge](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.

Chaque carte réseau attachée de tooa machine virtuelle possède une ou plusieurs configurations IP associés tooit. Une adresse IP privée statique ou dynamique est affectée à chaque configuration. Chaque configuration peut également avoir un tooit du ressources associées des adresse IP publique. Une ressource d’adresse IP publique a soit un dynamique ou statique publique IP adresse affectée tooit. toolearn savoir plus sur IP adresses dans Azure, lisez hello [les adresses IP dans Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) l’article. 

Est un toohow de limite IP privé nombreuses adresses peuvent être attribuées à la carte réseau de tooa. Il existe également une limite toohow plusieurs adresses IP publiques qui peuvent être utilisés dans un abonnement Azure. Consultez hello [Azure limite](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) article pour plus d’informations.
