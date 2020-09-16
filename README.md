# ROS-Gazebo
Software di simulazione per droni: <br>
Versione GAZEBO 7.0<br>
Versione ROS Melodic<br>

-----------------------------------------------------------------------------------------

# Guida passo-passo
-----------------------------------------------------------------------------------------
## 1. Installazione
Per poter installare ROS+Gazebo, si dovrà avere a disposizione una distribuzione Ubuntu (consigliamo 18.04 +) su macchina virtuale (es: Virtual Box) o tramite partizione.
  * Proponiamo un link alla guida ufficiale di GitHub per l'installazione: [GUIDA INSTALLAZIONE](https://github.com/ethz-asl/rotors_simulator)
  * proponiamo anche un link (che consigliamo) in cui è presente una OVA per macchina virtuale VirtalBox, in modo da poterla importare ed avere un ambiente di sviluppo già pronto e funzionante: [DOWNLOAD OVA](https://univpm-my.sharepoint.com/:f:/g/personal/s1088279_studenti_univpm_it/EjDqAEOL1WRCgjfu0cDKMvsB2gNqCj9FmYp-Dh4ALNuY8g?e=PsrsZR)
  
Per poter installare l'OVA sulla propria VirtualBox, seguire i seguenti passi:
  * Aprire VirtualBox
  * `File > Importa Applicazione Virtuale`
  * Selezionare il file OVA scaricato attraverso la schermata che si aprirà dopo aver cliccato sull'icona della cartella in basso a destra
  * Cliccare su 'Successivo'
  * Lasciare le impostazioni così come sono e cliccare su 'Importa'
  * Attendere il completamento (circa qualche minuto)
  
*N.B. Per poter lavorare in piena serenità, consigliamo di avere un PC con almeno 8 GB di RAM e almeno 25 GB di spazio libero su disco. Istallando il software su una distribuzione Linux, da zero, porterà ad avere una serie di problemi che possono esssere risolti solamente se si conosce l'ambiente di sviluppo, pertanto sconsigliamo di farlo e di seguire l'installazione dell'OVA*

## 2. Gestione Macchina Virtuale
Per poter accedere alla macchina virtuale, una volta installata, cliccare due volte sull'icona rappresentativa (RotorS(Melodic))<br>
Le credenziali di accesso alla macchina virtuale sono le seguenti:
 * Username: rotors
 * Password: rotors
 
## 3. Gestione ROS & Gazebo
Per tutti i dettagli rimandiamo alla guida di [ROS.org](http://wiki.ros.org/)<br>
 * Gestione Ambiente:
   * Creazione Workspace: per poter creare la workspace (una directory in cui sono presenti al suo interni i, cosidetti, package di lavoro per Gazebo) basta semplicemente collocarsi in `/home` e crerare una directory (tramite linea di comando: `cd /home` + `mkdir nome_workspace`)
   * Filesystem:
      * Package: Organizzazione software (librerie, script ecc...)
      * Manifest(package.xml): descrizione del package (metadati)
 
### 3.1. Package

#### 3.1.1. Directory Tree

-> my-package/<br>
---> CMakeList.txt(file testo standard)<br>
---> package.xml<br>

#### 3.1.2. Directory Tree MultiPackage

-> workspace/<br>
---> src/<br>
-----> package_1/<br>
--------> CMakeList.txt<br>
--------> package.xml<br>
-----> package_2/<br>
--------> CMakeList.txt<br>
--------> package.xml<br>

#### 3.1.3. Creare un package

Da terminale:
 * `cd ~/workspace/src`
 * `catkin_create_pkg nome_package`
  * comando generale: `catkin_create_pkg <name> [dep1] [dep2] [dep3]`
Una volta create il package sarà possibile inserire all'interno le directory che andranno a strutturare il progetto.
 * `cd nome_package`
 * `mkdir launch | mkdir worlds`
Le due directory create ospiteranno la struttura dell'intero simulatore.
All'interno di `launch` verranno creati e/o posizionati i file `.launch` in cui al loro interno hanno hanno una serie di tag che vanno a identificare il mondo virtuale, il robot e tutte le caratteristiche da implementare in un mondo virtuale (vedremo launch nel dettaglio dopo).
All'interno di `worlds` verranno creati e/o posizionati i file `.world` in cui al loro intewrno hanno una serie di tag che vanno a identificare, in modo specifico, un mondo e le sue caratterisriche (esempio: una casa, un ambiente vuoto, una cava ecc...).

#### 3.1.4. Package.xml
 * description tags: `<description> ... </description>` --> Tag per la descrizione del package
 * maintainer tags: `<mainteiner> ... </maintenìiner>` ---> Tag per immettere i contatti dello sviluppatore del package
 * license tags: `<license> ... </license>` ---> Tag immettere le license e le versioni del software che si sta realizzando
 * dependecies tags: 
   * `<build_depend> ... <build_depend>`
   * `<buildtool_depend> ... <buildtool_depend>`
   * `<run_depend> ... <run_depend>`
   * `<test_depend> ... <test_depend>`
   
#### 3.1.5. Compilare un Package
