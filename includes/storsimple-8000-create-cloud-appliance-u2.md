#### <a name="toocreate-a-cloud-appliance"></a>toocreate un dispositif de cloud

1. Bonjour portail Azure, accédez à toohello **le Gestionnaire de périphériques StorSimple** service.
2. Accédez toohello **périphériques** panneau. Dans la barre de commandes hello dans le panneau de résumé hello service, cliquez sur **dispositif de cloud créer**.
    ![StorSimple - Créer une appliance cloud](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. Bonjour **dispositif de cloud créer** panneau, spécifiez les détails suivants de hello.
   
    ![StorSimple - Créer une appliance cloud](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **Nom** : nom unique de votre appliance cloud.
   2. **Modèle** -choisir modèle hello du dispositif de cloud hello. Un modèle d’appareil 8010 offre 30 To de stockage Standard, tandis qu’un modèle d’appareil 8020 offre 64 To de stockage Premium. Spécifiez 8010 scénarios de récupération au niveau élément toodeploy à partir de sauvegardes. Sélectionnez 8020 toodeploy hautes performances, les charges de travail à faible latence, ou utiliser comme une unité secondaire pour la récupération d’urgence.
   3. **Version** -choisissez la version de l’appliance du cloud hello hello. version de Hello correspond version toohello d’image de disque virtuel hello qui est utilisé toocreate hello cloud. Version hello du cloud de hello spécifiée appliance détermine quels physique appareil basculer ou de cloner dans, il est important que vous créez une version appropriée du dispositif de cloud hello.
   4. **Réseau virtuel** – spécifiez un réseau virtuel que vous souhaitez toouse avec cette solution de cloud. Si vous utilisez le stockage Premium, vous devez sélectionner un réseau virtuel qui est pris en charge par hello compte de stockage Premium. Hello non pris en charge des réseaux virtuels apparaissent en grisé dans la liste déroulante de hello. Vous êtes averti si vous sélectionnez un réseau virtuel non pris en charge.
   5. **Sous-réseau** -en fonction hello du réseau virtuel sélectionné, liste déroulante de hello affiche les sous-réseaux hello associé. Affecter un dispositif de sous-réseau tooyour cloud.
   6. **Compte de stockage** – sélectionnez une image hello toohold du compte de stockage de matériel de cloud hello lors de la configuration. Ce compte de stockage doit être Bonjour même région que le matériel de cloud hello et le réseau virtuel. Il ne doit pas être utilisée pour le stockage de données par hello physique ou de matériel de cloud hello. Par défaut, un compte de stockage est créé à cet effet. Toutefois, si vous savez que vous avez déjà un compte de stockage qui convient pour cette utilisation, vous pouvez le sélectionner à partir de la liste de hello. Si vous créez une application de cloud premium, liste de déroulante hello affiche uniquement les comptes de stockage Premium.
      
      > [!NOTE]
      > Dispositif de cloud Hello ne fonctionnent qu’avec les comptes de stockage Azure hello.
    
   7. Sélectionnez tooindicate de case à cocher hello que vous comprenez que les données hello stockées sur l’équipement de cloud hello sont hébergées dans un centre de données Microsoft.
       * Lorsque vous utilisez uniquement un appareil physique, votre clé de chiffrement est conservée avec celui-ci ; par conséquent, Microsoft ne peut pas le déchiffrer.

       * Lorsque vous utilisez un dispositif de cloud, clé de chiffrement hello et clé de déchiffrement hello sont stockées dans Microsoft Azure. Pour plus d’informations, consultez les [considérations de sécurité relatives à l’utilisation d’une appliance cloud](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security).
   8. Cliquez sur **créer** dispositif de cloud tooprovision hello. Appareil de Hello peut prendre environ 30 minutes toobe configuré. Vous êtes averti lorsque le dispositif de cloud hello est créé avec succès. Accédez tooDevices panneau et actualise la liste hello des périphériques matériel de cloud toodisplay hello. l’état de l’appliance de hello Hello est **prêt tooset des**.
      
      ![Dispositif de StorSimple de Cloud de prêt tooset des](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

