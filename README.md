**LAB 2 : Rooting Android**
Étape 1 : Rooter l'AVD

<img width="830" height="151" alt="image" src="https://github.com/user-attachments/assets/be148751-ef65-4154-bc9b-2e5cedeb484c" />

>Cette capture d'écran illustre l'étape initiale de l'interaction avec un appareil Android via le Android Debug Bridge (ADB). C'est une phase cruciale pour tout audit de sécurité ou test d'intrusion mobile.
>Utilisation de la commande adb devices pour lister les terminaux connectés. On observe qu'un émulateur Android (emulator-5554) est correctement détecté et prêt à recevoir des instructions via le pont de débogage Android (ADB).
<img width="911" height="251" alt="image" src="https://github.com/user-attachments/assets/75c74a4b-916f-44f8-afab-331afaf2b3f9" />

>Exécution de la commande adb root. Le système confirme le redémarrage du démon ADB (adbd) avec les droits d'administrateur (root). Cette étape est cruciale pour accéder aux fichiers système sensibles et effectuer des tests d'intrusion sur l'application mobile.




<img width="1800" height="748" alt="image" src="https://github.com/user-attachments/assets/ce564363-4629-4fca-8a54-57c905bba480" />


1. ```adb root```
Description : Redémarre le démon ADB (adbd) sur l'appareil avec les privilèges root (administrateur). Cela permet d'accéder aux fichiers système protégés.

2. ```adb shell id```
Description : Affiche l'identité de l'utilisateur actuel dans le shell Android. Dans votre cas, il confirme que vous êtes uid=0(root), ce qui signifie que vous avez les pleins pouvoirs sur le système.

3. ```adb shell getprop ro.boot.verifiedbootstate```
Description : Interroge la propriété système pour vérifier l'état du Verified Boot. Cela permet de savoir si le chargeur de démarrage (bootloader) est verrouillé ou si l'intégrité du système est compromise.

4. ```adb shell getprop ro.boot.veritymode```
Description : Vérifie le mode de dm-verity. Dans votre capture, il répond enforcing, ce qui signifie que le système vérifie strictement l'intégrité des partitions au démarrage et empêche les modifications non autorisées.

5. ```adb shell getprop ro.boot.vbmeta.device_state```
Description : Indique l'état actuel de la sécurité de l'appareil (généralement locked ou unlocked) basé sur les métadonnées de démarrage sécurisé (vbmeta).

6. ```adb shell "su -c id"```
Description : Tente d'exécuter la commande id en passant par l'utilitaire su (SuperUser).

Note sur l'erreur : Elle a échoué (invalid uid/gid '-c') parce que sur certains émulateurs ou versions d'Android, la syntaxe du binaire su est différente ou le paramètre -c n'est pas reconnu de cette manière. Cependant, comme vous êtes déjà en mode adb root, cette commande est redondante.

<img width="1248" height="264" alt="image" src="https://github.com/user-attachments/assets/2af064f2-93a2-488c-91bb-a59ed9e68939" />
# Journalisation :
<img width="1401" height="117" alt="image" src="https://github.com/user-attachments/assets/65296c20-4532-4b32-8f16-10292a831dd7" />

