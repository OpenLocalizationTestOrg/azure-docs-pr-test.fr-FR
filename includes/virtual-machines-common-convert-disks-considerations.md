
* conversion de Hello nécessite un redémarrage de hello machine virtuelle, par conséquent, planifier la migration de vos machines virtuelles hello pendant une fenêtre de maintenance existant. 

* conversion de Hello n’est pas réversible. 

* Être sûr de conversion de hello tootest. Migrer un ordinateur virtuel de test avant d’effectuer la migration hello en production.

* Lors de la conversion de hello, vous libérez hello machine virtuelle. Hello machine virtuelle reçoit une nouvelle adresse IP lorsqu’il est démarré après la conversion de hello. Si nécessaire, vous pouvez [attribuer une adresse IP statique](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello machine virtuelle.

* Hello VHD d’origine et le compte de stockage hello utilisé par hello machine virtuelle avant la conversion ne sont pas supprimés. Ils continuent tooincur frais. tooavoid facturé pour ces artefacts, supprimer des objets BLOB de disque dur virtuel d’origine hello après avoir vérifié que la conversion de hello est terminée.
