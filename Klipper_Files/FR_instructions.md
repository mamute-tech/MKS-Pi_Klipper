# Instructions pour utiliser les GPIOs du MKS-Pi sous Klipper

la procédure est basée sur la documentation de klipper: https://www.klipper3d.org/fr/RPi_microcontroller.html.
Le système est celui fourni par Makerbase (lien dans le dossier [*System Images*](/System_Images/README.md) de ce repo)

Afin d'utiliser les GPIOs, il faut utiliser le MKS-Pi comme mcu secondaire (la procédure est tirée de la doc klipper et peut ne plus être à jour)
loggez vous en ssh avec l'utilisateur *mks* (mot de passe par défaut *makerbase* pour *mks* et *root*)

## Installer le script rc

Pour utiliser le MKS-Pi comme mcu secondaire, le processus klipper_mcu doit d'executer avant le processus klippy

```
cd ~/klipper/
sudo cp ./scripts/klipper-mcu.service /etc/systemd/system/
sudo systemctl enable klipper-mcu.service
```

## Construire le code du microcontrôleur

Pour pouvoir compiler le code du micro-contrôleur, il faut d'abord le configurer

```
cd ~/klipper/
make menuconfig
```

*écriture en cours, cette partie sera bientôt détaillée*


Ensuite vous pouvez compiler

```
sudo service klipper stop
make flash
sudo service klipper start
```

En cas d'erreur "Autorisation refusée, il faut ajouter votre utilisateur au groupe tty
```
sudo usermod -a -G tty pi
```

## Fin de configuration

Ajouter le fichier *mkspi.cfg* sur votre imprimante

Faite un include de celui-ci dans votre *printer.cfg*
```
[include mkspi.cfg]
```

