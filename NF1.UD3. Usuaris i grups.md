# NF1.UD3. Usuaris i grups

## Objectiu de la tasca

L’objectiu d’aquesta tasca és practicar l’administració d’usuaris i grups a Ubuntu Server.
 S’han creat els grups necessaris i diversos usuaris amb els seus directoris personals i shells corresponents. També s’ha configurat el fitxer de benvinguda, l’estructura de `/etc/skel` i l’àlies `ll`; s’han comprovat els fitxers del sistema relacionats amb els comptes, s’ha gestionat el bloqueig i desbloqueig d’un usuari, s’ha eliminat un compte i s’ha configurat el shell Fish per a `laura_dev`.

## 1. Creació de la jerarquia de grups

Les ordres següents creen els grups devs, sysadmin i auditor.

![Creació de grups](img/1_groupadd.png)
```bash
sudo addgroup devs
sudo addgroup sysadmin
sudo addgroup auditor
```
A continuació comprovem els grups a la carpeta `/etc/group`

![Comprobació amb el cat](img/2_cat_groups.png)


## 2. Gestió dels perfils d'usuari

> Passem al ssh per més comoditat

Creem l'arxiu benvinguda.txt i posem les normatives.

```bash
nano ~/benvinguda.txt
```
![Normatives dins el nano](img/3_texto_nano.png)

Creem el directori `Documents` que utilitzarán els usuaris nous.

```bash
mkdir -p ~/Documents
```
![Creació carpeta i ls](img/4_mkdir_ls.png)


Entrem al directori plantilla `/etc/skel` i editem el fitxer `.bashrc` per configurar l’àlies ll.