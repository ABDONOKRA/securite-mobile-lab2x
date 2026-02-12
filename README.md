**LAB 2 : Rooting Android**
Étape 1 : Rooter l'AVD

<img width="830" height="151" alt="image" src="https://github.com/user-attachments/assets/be148751-ef65-4154-bc9b-2e5cedeb484c" />

>Cette capture d'écran illustre l'étape initiale de l'interaction avec un appareil Android via le Android Debug Bridge (ADB). C'est une phase cruciale pour tout audit de sécurité ou test d'intrusion mobile.
>Utilisation de la commande adb devices pour lister les terminaux connectés. On observe qu'un émulateur Android (emulator-5554) est correctement détecté et prêt à recevoir des instructions via le pont de débogage Android (ADB).
<img width="911" height="251" alt="image" src="https://github.com/user-attachments/assets/75c74a4b-916f-44f8-afab-331afaf2b3f9" />

>Exécution de la commande adb root. Le système confirme le redémarrage du démon ADB (adbd) avec les droits d'administrateur (root). Cette étape est cruciale pour accéder aux fichiers système sensibles et effectuer des tests d'intrusion sur l'application mobile.
