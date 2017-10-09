#### <a name="toocreate-a-virtual-device"></a>toocreate un appareil virtuel
1. Bonjour portail Azure, accédez à toohello **StorSimple Manager** service.
2. Accédez toohello **périphériques** page. Cliquez sur **créer un appareil virtuel** bas hello hello **périphériques** page.
3. Bonjour **boîte de dialogue Créer une machine virtuelle**, spécifiez les détails suivants de hello.
   
    ![Création d’un appareil virtuel StorSimple](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **Nom** : nom unique de votre appareil virtuel.
   2. **Modèle** -choisir modèle hello de l’appareil virtuel de hello. Ce champ n'apparaît que si vous exécutez Update 2 ou une version ultérieure. Un modèle d'appareil 8010 offre 30 To de stockage standard tandis qu'un modèle d'appareil 8020 offre 64 To de stockage Premium. Spécifiez 8010
   3. toodeploy scénarios de récupération au niveau élément à partir de sauvegardes. Sélectionnez 8020 toodeploy hautes performances, faible des charges de travail latence ou utilisé comme une unité secondaire pour la récupération d’urgence.
   4. **Version** -choisissez la version de l’appareil virtuel de hello hello. Si un modèle d’appareil 8020 est sélectionné, puis le champ version hello verront pas toohello utilisateur. Cette option est omise si tous les hello physique appareils inscrits auprès de ce service sont en cours d’exécution mise à jour 1 (ou version ultérieure). Ce champ est présenté uniquement si vous avez un mélange d’avant mise à jour 1 et 1 de la mise à jour des appareils physiques inscrits avec hello même service. Fonction hello version de l’appareil virtuel de hello détermine quel périphérique physique, vous pouvez basculement ou un clone à partir de, il est important que vous créez une version appropriée de l’appareil virtuel de hello. Sélectionnez :
      
      * la version Update 0.3 en cas de basculement ou de récupération d'urgence à partir d'un appareil physique exécutant la version Update 0.3 ou une version antérieure. 
      * la version Update 1 en cas de basculement ou de clonage à partir d'un appareil physique exécutant la version Update 1 (ou une version ultérieure). 
   5. **Réseau virtuel** – spécifiez un réseau virtuel que vous souhaitez toouse avec cet appareil virtuel. Si vous utilisez le stockage Premium (Update 2 ou version ultérieure), vous devez sélectionner un réseau virtuel qui est pris en charge par hello compte de stockage Premium. Hello non pris en charge des réseaux virtuels seront grisées dans la liste déroulante de hello. Vous êtes averti si vous sélectionnez un réseau virtuel non pris en charge. 
   6. **Compte de stockage pour la création de périphérique virtuel** – sélectionnez une image hello toohold du compte de stockage de l’appareil virtuel de hello lors de la configuration. Ce compte de stockage doit être Bonjour même région que le périphérique virtuel de hello et le réseau virtuel. Il ne doit pas être utilisée pour le stockage de données par hello physique ou sur un appareil virtuel hello. Par défaut, un compte de stockage est créé à cet effet. Toutefois, si vous savez que vous avez déjà un compte de stockage qui convient pour cette utilisation, vous pouvez le sélectionner à partir de la liste de hello. Si vous créez un périphérique virtuel premium, liste de déroulante hello affiche uniquement les comptes de stockage Premium. 
      
      > [!NOTE]
      > un appareil virtuel Hello ne fonctionnent qu’avec les comptes de stockage Azure hello. Autres fournisseurs de services cloud tels que Amazon, HP et OpenStack (qui sont prises en charge pour les appareils physiques hello) ne sont pas pris en charge pour un appareil virtuel StorSimple hello.
      > 
      > 
   7. Cliquez sur tooindicate de case à cocher hello que vous comprenez que les données hello stockées sur un appareil virtuel hello soit hébergées dans un centre de données Microsoft. Lorsque vous utilisez uniquement un appareil physique, votre clé de chiffrement est conservée avec celui-ci ; par conséquent, Microsoft ne peut pas le déchiffrer. 
      
       Lorsque vous utilisez un appareil virtuel, la clé de chiffrement hello et clé de déchiffrement hello sont stockées dans Microsoft Azure. Pour plus d’informations, consultez la page [Considérations de sécurité relatives à l’utilisation d’un appareil virtuel](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Cliquez sur périphérique virtuel hello du toocreate icône hello à cocher. Appareil de Hello peut prendre environ 30 minutes toobe configuré.
      
      ![Étape de création de l’appareil virtuel StorSimple](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

