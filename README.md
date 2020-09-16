# ROS-Gazebo
Software di simulazione per droni: <br>
Versione GAZEBO 7.0<br>
Versione ROS Melodic<br>


# Guida passo-passo

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
   * Creazione Workspace: per poter creare la workspace (una directory in cui sono presenti al suo interni i, cosidetti, package di lavoro per Gazebo) basta semplicemente collocarsi in `/home` e crerare una directory (tramite linea di comando: `$ cd /home` + `$ mkdir nome_workspace`)
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
 * `$ cd ~/workspace/src`
 * `$ catkin_create_pkg nome_package`
  * comando generale: `$ catkin_create_pkg <name> [dep1] [dep2] [dep3]`
Una volta create il package sarà possibile inserire all'interno le directory che andranno a strutturare il progetto.
 * `$ cd nome_package`
 * `$ mkdir launch | mkdir worlds`
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
Per poter compilare un package bisogna eseguire i seguenti passi:
 * `$ cd workspace`
 * `$ catkin_make`
 * `$ source ~/devel/setup.bash`
Fatto ciò sarà possibile eseguire un file di launch all'interno della workspace attracerso il comando `$ roslaunch <directory_package> <nome_file_launch>`

## 4. Lancio Del Software
Per poter lanciare il software e verificare che tutto nella macchina virtuale funzioni correttamente, seguire la seguente guida:
 * Aprire il terminale
 * `$ cd /home` se non si è già collocati al suo interno
 * `$ mkdir workspace_catkin`
 * `$ cd workspace_catkin`
 * `$ mkdir src`
 * `$ cd src/`
 * `$ catkin_create_pkg prova_gazebo` a 'prova_gazebo' può essere messo qualsiasi nome si voglia, per semplicità facciamo questo esempio.
 * `$ cd prova_gazebo`
 * `$ mkdir launch | mkdir worlds`
 * `$ cd launch`
 * `$ sudo nano prova.launch`
 * Si aprirà un editor di file e al suo interno copiamo e incolliamo quanto segue:
 
               <launch>
               <!-- We resume the logic in empty_world.launch, changing only the name of the world to be launched -->
               <include file="$(find gazebo_ros)/launch/empty_world.launch">
                 <arg name="world_name" value="$(find prova_gazebo)/worlds/prova.world"/>
                 <!-- more default parameters can be changed here -->
               </include>
               </launch>`

     *N.B. Per i prossimi file che si creeranno, basta sostituire all'interno dei tag la parola 'prova_gazebo' e 'prova.world' con il path e il file world che si vuole utilizzare*
     
 * `$ cd ..`
 * `$ cd worlds`
 * `$ sudo nano prova.world`
 * Si aprirà un editor e si dovrà inserire quanrto segue:
 
          <?xml version="1.0" ?>
          <sdf version="1.4">
            <world name="default">
              <include>
                <uri>model://ground_plane</uri>
              </include>
              <include>
                <uri>model://sun</uri>
              </include>
              <include>
                <uri>model://gas_station</uri>
                <name>gas_station</name>
                <pose>-2.0 7.0 0 0 0 0</pose>
              </include>
            </world>
          </sdf>
          
     *N.B. Si potrà inserire al suo interno tutte le componenti che si vogliono, chiamate 'model'. In questa piccola porzione di mondo troviamo un terreno, un sole(luminosità radiale) e una stazione di benzina (che potrà essere reperibile insieme a tantissime altre strutture e oggetti all'interno del database online di Gazebo.
     
 * `$ cd .. `
 * `$ cd ..`
 * `$ catkin_make`
 * `$ source ~/devel/setup.bash`
 * `$ roslaunch prova_gazebo prova.launch` --> partirà GAzebo e ROS con la simulazione di una stazione di servizio.
 
Per poter inserire un robot all'interno della scena, basta seguire i seguenti passi:
 * Aprire il file `prova.launch`:
   * `$ sudo nano src/prova_gazebo/launch/prova.launch`
 * Inserire quanto segue, prima del `</launch>`:
 
       <!-- Spawn a robot into Gazebo -->
       <node name="spawn_urdf" pkg="gazebo_ros" type="spawn_model" args="-file $(find baxter_description)/urdf/baxter.urdf -urdf -z 1 -model baxter" />
       
  *N.B. Se si sta eseguendo l'OVA, non si avranno problemi, in altri casi bisogna installare il pacchetto aggiuntivo del roboto attraverso il comando `$ git clone https://github.com/RethinkRobotics/baxter_common.git` e ricompilare la workspace con `$ catkin_make`.
  
* `$ catkin_make`
* `$ source ~/devel/setup.bash`
* `$ roslaunch prova_gazebo prova.launch` --> Si aprirà la stazione di servizio con un robot presente sulla scena.
