1. Dans le portail hello, à partir de **toutes les ressources**, cliquez sur **+ ajouter**. 
2. Bonjour **tout** panneau recherche, tapez **passerelle de réseau Local**, puis cliquez sur toosearch. Cette commande retourne une liste. Cliquez sur **passerelle de réseau Local** tooopen hello panneau, puis cliquez sur **créer** tooopen hello **créer une passerelle réseau local** panneau.

  ![créer une passerelle de réseau local](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. Sur hello **Panneau de passerelle de réseau local de créer**, spécifiez les valeurs hello pour votre passerelle de réseau local.

  - **Nom :** spécifiez un nom pour votre objet de passerelle de réseau local.
  - **Adresse IP :** hello une adresse IP publique du périphérique VPN hello souhaité Azure tooconnect à. Spécifiez une adresse IP publique valide. adresse IP de Hello ne peut pas se trouver derrière un NAT et a toobe accessible par Azure. Si vous n’avez adresse hello dès maintenant, vous pouvez utiliser les valeurs hello indiqués dans la capture d’écran de hello, mais vous devez toogo précédent et remplacez votre adresse de l’espace réservé hello adresse IP publique de votre périphérique VPN. Dans le cas contraire, Azure ne sera pas en mesure de tooconnect.
  - **L’espace d’adressage** fait référence toohello les plages d’adresses réseau hello représentant ce réseau local. Vous pouvez ajouter plusieurs plages d’espaces d’adressage. Assurez-vous que vous spécifiez ici des plages hello ne se chevauchent pas avec d’autres réseaux que vous souhaitez tooconnect à des plages. Azure achemine la plage d’adresses hello que vous spécifiez l’adresse IP du périphérique VPN toohello local. *Utiliser vos propres valeurs ici, ne Hello pas les valeurs indiquées dans la capture d’écran de hello*.
  - **L’abonnement :** Vérifiez que hello correct abonnement s’affiche.
  - **Groupe de ressources :** groupe de ressources hello Select que vous souhaitez toouse. Vous pouvez créer un groupe de ressources ou en sélectionner un déjà créé.
  - **Emplacement :** sélectionnez emplacement hello qui est créé dans cet objet. Vous souhaiterez tooselect hello même emplacement que votre réseau virtuel se trouve dans, mais vous n’êtes pas toodo requis ainsi.

4. Lorsque vous avez terminé de spécifier les valeurs hello, cliquez sur **créer** bas hello de passerelle de réseau local hello panneau toocreate hello.
