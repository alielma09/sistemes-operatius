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
![Moure al skel i nano](img/5_cd_nano.png)

```bash
cd /etc/skel

sudo nano .bashrc
```

![Edició bashrc](img/5_nano_bashrc.png)

Comprovem la comanda alias ll

```bash
alias ll
```

![Comprovem comanda](img/6_alias_ll.png)

Editem la config d’adduser per comprovar que el shell per defecte és Bash.

```bash
sudo nano /etc/adduser.conf
```

![Linea de codi](img/7_comanda.png)
![Config de l’usuari](img/7_comprov.png)

Creem l'usuari de prova `test1` amb la contrasenya `test1`

```bash
sudo adduser test1
```

![Usuari nou](img/8_useradd.png)

## 3. Creació i configuració d'usuaris

Ara, utilitzant la comanda anterior, creem els usuaris `pau_dev` i `laura_dev` amb les contrasenyes `usuari`.

![Usuari nou](img/9_lauradev.png)

![Usuari nou](img/9_paudev.png)

Comprovem amb la comanda

```bash
cat /etc/passwd
```

Ara creem els usuaris marc_sys i auditor, amb les comandes:

-M: Serveix per crear direcoris

-D: S'utilitza per marcar la ruta hon volem que estigui el direcortri

-S: Es per definir la terminal que ulizitzara

-G: Es per agregarlo al grup directament

-C: Serveix per si vols posar alguna descripico al conté.

```bash
sudo useradd -m -d /home/marc_sys -s /bin/bash -g sysadmin -G devs -c "Marc Soler" marc_sys
sudo useradd -m -d /home/auditor -s /bin/bash -g sysadmin -G devs -c "Marc Soler" auditor 
```

![Usuaris nous](img/10_spow.png)

Modifiquem permisos amb les comandes;

```bash
sudo usermod -aG devs pau_dev
sudo usermod -aG devs laura_dev
sudo usermod -aG devs marc_sys
sudo usermod -aG auditor auditor
```

![Permisos](img/11_permis.png)

## Inspecció del sistema i fitxers de configuració

Utilitzem la comanda `id marc_sys`

> La comanda id permet comprovar l’identificador d’usuari, el grup principal i els grups secundaris de marc_sys.

```bash
id marc_sys
```

![Marcsys](img/12_marcsys.png)

Iniciem sesió amb l'usuari `pau_dev`

```bash
su pau_dev
```

![paudev](img/13_paudev.png)

Consultem `/etc/passwd` 
> El directori /etc/passwd conté informació sobre grups i usuaris.

```bash
cat etc/passwd
```

![passwd](img/14_passwd.png)

Ara intentem consultar `/etc/shadow` pero el nostre usuari no pot.
> El directori /etc/shadow conté les contrasenyes dels usuaris pero encriptades en `hash`perque ningú les pugui lleguir a simple vista.

```bash
sudo cat/etc/shadow
cat /etc/shadow

*Permision denied*
```

![Permisió denegada](img/15_denegado.png)

Quin és el directori plantilla que s'utilitza per omplir el /home d'un usuari nou quan es crea?

El direcotri plantilla que s'utiliza es /etc/skel
Quina comanda o fitxer en defineix aquesta configuració?

useradd -d

## Manteniment, bloqueig i eliminació

Bloquejem el compte `pau_dev` (després es pot desbloquejar facilment)

```bash
sudo passwd -l pau_dev
```

![Bloqueig compte paudev](img/16_bloq_paudev.png)

