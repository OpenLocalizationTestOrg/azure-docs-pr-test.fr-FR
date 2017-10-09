Si vous rencontrez des problèmes de connexion d’ordinateur virtuel de tooa sur votre connexion VPN, vérifiez suivantes de hello :

- Vérifiez que votre connexion VPN aboutit.
- Vérifiez que vous vous connectez toohello une adresse IP privée pour hello machine virtuelle.
- Si vous pouvez vous connecter toohello machine virtuelle à l’aide d’IP privé de hello adresse, mais ne Hello pas de nom de l’ordinateur, vérifiez que vous avez correctement configuré DNS. Pour plus d’informations sur le fonctionnement de la résolution de noms pour les machines virtuelles, consultez [Résolution de noms pour les machines virtuelles](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Lorsque vous vous connectez via un Point-to-Site, vérifiez hello éléments supplémentaires suivants :

- Utilisez « ipconfig » toocheck hello adresse IPv4 attribuée la carte Ethernet toohello ordinateur hello à partir de laquelle vous vous connectez. Adresse IP de hello est dans la plage d’adresses hello Hello réseau virtuel que vous vous connectez à ou au sein de la plage d’adresses hello de votre VPNClientAddressPool, il s’agit tooas auxquels un espace d’adressage qui se chevauchent. Lorsque votre espace d’adressage chevauche de cette façon, Azure n’atteint pas le trafic réseau de hello, il reste sur le réseau local de hello.
- Vérifiez que ce package de configuration de client VPN hello a été généré une fois que les adresses IP de serveur DNS hello ont été spécifiées pour hello réseau virtuel. Si vous mises à jour des adresses IP de serveur DNS hello, générer et installer un nouveau package de configuration de client VPN.

Pour plus d’informations sur le dépannage d’une connexion RDP, consultez [tooa de connexions de résoudre les problèmes de bureau à distance VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
