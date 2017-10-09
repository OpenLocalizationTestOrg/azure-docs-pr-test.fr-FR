> [!NOTE]
> * passerelle VPN de Hello adresse IP publique change lors de la migration à partir d’un ancien tooa de référence (SKU) nouvelle référence (SKU).
> * Vous ne pouvez pas migrer toohello de passerelles VPN classique nouvelles références SKU. Les passerelles peuvent uniquement utiliser VPN classique hello hérités SKU (anciens).
> 

Vous ne pouvez pas redimensionner votre réseau privé virtuel Azure entre les passerelles hello anciennes références (SKU) et hello nouvelles familles de référence (SKU). Si vous avez des passerelles VPN dans le modèle de déploiement du Gestionnaire de ressources hello hello une ancienne version de hello références (SKU), vous pouvez migrer toohello nouvelles références SKU. toomigrate, vous supprimez la passerelle VPN existante de hello pour votre réseau virtuel, puis créez-en un nouveau.

Workflow de migration :

1. Supprimez toute passerelle de réseau virtuel toohello connexions.
2. Suppression de la passerelle VPN ancien de hello.
3. Créer la passerelle VPN hello.
4. Mettre à jour vos appareils VPN local avec hello nouvelle passerelle adresse IP VPN (pour les connexions de Site à Site).
5. Mettre à jour la valeur d’adresse IP hello passerelle pour les passerelles de réseau local à réseau qui se connecteront toothis passerelle.
6. Télécharger de nouveaux packages de configuration de VPN de client pour les clients P2S connexion de réseau virtuel de toohello via cette passerelle VPN.
7. Recréez la passerelle de réseau virtuel toohello hello connexions.
