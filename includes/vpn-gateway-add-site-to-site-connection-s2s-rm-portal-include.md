1. Accédez à panneau de hello ouvrir tooand pour votre passerelle de réseau virtuel. Il existe plusieurs façons toonavigate. Dans notre exemple, nous avons accédé toohello passerelle 'VNet1GW' en accédant trop**TestVNet1 -> vue d’ensemble -> connecté périphériques -> VNet1GW**.
2. Dans le panneau de hello pour VNet1GW, cliquez sur **connexions**. En haut de hello du panneau des connexions hello, cliquez sur **+ ajouter** tooopen hello **ajouter une connexion** panneau.

    ![Créer une connexion de site à site](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. Sur hello **ajouter une connexion** panneau, hello, renseignez les valeurs toocreate votre connexion.

  - **Nom** : nommez votre connexion. Nous utilisons **VNet1toSite2** dans notre exemple.
  - **Type de connexion** : sélectionnez **Site à site (IPSec)**.
  - **Passerelle de réseau virtuel :** valeur de hello est fixe, car vous vous connectez à partir de cette passerelle.
  - **Passerelle de réseau local :** cliquez sur **choisir une passerelle de réseau local** et sélectionnez hello passerelle de réseau local que vous souhaitez toouse. Dans notre exemple, nous utilisons **Site2**.
  - **Clé partagée :** valeur hello ici doit correspondre à valeur hello que vous utilisez pour votre périphérique VPN de site local. Dans l’exemple de hello, nous avons utilisé « abc123 », mais vous pouvez (et doivent) utiliser quelque chose de plus complexe. Hello important est cette valeur hello que vous spécifiez ici doit être hello que même valeur que vous avez spécifié lors de la configuration de votre périphérique VPN.
  - Hello restantes pour **abonnement**, **groupe de ressources**, et **emplacement** sont fixes.

4. Cliquez sur **OK** toocreate votre connexion. Vous verrez *création d’une connexion* flash sur l’écran hello.
5. Vous pouvez afficher les connexions hello Bonjour **connexions** Panneau de passerelle de réseau virtuel hello. Hello état passe de *inconnu* trop*connexion*, puis trop*Succeeded*.
