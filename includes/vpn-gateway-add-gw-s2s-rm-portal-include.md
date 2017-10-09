1. Dans hello à gauche de la page du portail hello, cliquez sur  **+**  et type de passerelle de réseau virtuel dans la recherche. Dans **Résultats**, recherchez et cliquez sur **Passerelle de réseau virtuel**.
2. Au bas de hello du Panneau de « Passerelle de réseau virtuel » hello, cliquez sur **créer**. Cette opération ouvre hello **créer une passerelle réseau virtuelle** panneau.

    ![Créer les champs du panneau de la passerelle de réseau virtuel](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Nouvelle passerelle")

3. Sur hello **créer une passerelle réseau virtuelle** panneau, spécifiez les valeurs hello pour votre passerelle de réseau virtuel.

  - **Nom** : nommez votre passerelle. Cela n’est pas hello identique à un sous-réseau de passerelle d’affectation de noms. Il s’agit de nom hello d’objet hello passerelle que vous créez.
  - **Type de passerelle** : sélectionnez **VPN**. Passerelles VPN utilisent le type de passerelle de réseau virtuel hello **VPN**. 
  - **Type de VPN**: sélectionner le type VPN hello qui est spécifié pour votre configuration. La plupart des configurations requièrent un type de VPN basé sur un itinéraire.
  - **Référence (SKU)**: passerelle hello sélectionnez référence (SKU) à partir de la liste déroulante de hello. références (SKU) Hello répertoriés dans la liste déroulante de hello dépend hello type VPN que vous sélectionnez. Pour plus d’informations sur les références de passerelle, consultez [Références (SKU) de passerelle](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Emplacement**: vous devrez peut-être tooscroll toosee emplacement. Ajuster hello **emplacement** champ toopoint toohello emplacement de votre réseau virtuel. Si les emplacement hello ne pointent pas toohello la région où se trouve votre réseau virtuel, réseau virtuel de hello n’apparaît pas dans l’étape suivante de hello 'Choisir un réseau virtuel' la liste déroulante.
  - **Réseau virtuel**: choisissez hello réseau virtuel toowhich vous voulez tooadd cette passerelle. Cliquez sur **réseau virtuel** Panneau de « Choisir un réseau virtuel » tooopen hello. Sélectionnez hello réseau virtuel. Si vous ne voyez pas votre réseau virtuel, vérifiez que champ d’emplacement hello pointe toohello la région dans lequel se trouve votre réseau virtuel.
  - **Adresse IP publique**: panneau de hello 'Créer l’adresse IP publique' crée un objet d’adresse IP publique. adresse IP publique de Hello est attribué dynamiquement lors de la création de la passerelle VPN de hello. Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*. Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour. Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé. Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.

    - Tout d’abord, cliquez sur **adresse IP publique** tooopen hello 'Choisir l’adresse IP publique' un panneau, puis cliquez sur **+ créer de nouveaux** Panneau de « Créer une adresse IP publique » tooopen hello.
    - Ensuite, entrez un **nom** pour votre adresse IP publique, puis cliquez sur **OK** à hello en bas de cette toosave panneau vos modifications.

      ![Créer l’adresse IP publique](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "Créer PIP")

4. Vérifiez les paramètres de hello. Vous pouvez sélectionner **toodashboard du code confidentiel** bas hello du panneau hello si vous souhaitez que votre tooappear passerelle sur le tableau de bord hello. 
5. Cliquez sur **créer** toobegin création de passerelle VPN de hello. paramètres de Hello seront validés et vous verrez hello « Passerelle de réseau virtuel de déploiement » vignette sur le tableau de bord hello. Création d’une passerelle peut prendre jusqu'à too45 minutes. Vous devrez peut-être toorefresh votre état de hello terminée toosee page du portail.

Après la création de la passerelle de hello, afficher hello d’adresses IP qui a été attribué tooit en examinant le réseau virtuel de hello dans le portail de hello. passerelle de Hello apparaîtra comme un appareil connecté. Vous pouvez cliquer sur hello connecté le périphérique (votre passerelle de réseau virtuel) tooview plus d’informations.
