# ROS-Gazebo
Software di simulazione per droni: <br>
Versione GAZEBO 9.0<br>
Versione ROS Melodic<br>

# Indice
* <a href="#install">Installazione</a>
* <a href="#gest-mac">Gestione Macchina Virtuale</a>
* <a href="#gest-ros">Gestione ROS&Gazebo</a>
  * <a href="#gest-ros-pac">Package</a>
* <a href="#run">Lancio Programma</a>
* <a href="#command">Uso e Comandi di Gazebo</a>
  * <a href="#control">Controllo</a>
    * <a href="#control-key">Tastiera</a>
    * <a href="#control-joy">Joypad</a>
  * <a href="#plugin">Utilizzo Plugin</a>
    * <a href="#camera">Camera</a>


# Guida passo-passo

## <a name="install"/></a> 1. Installazione
Per poter installare ROS+Gazebo, si dovrà avere a disposizione una distribuzione Ubuntu (consigliamo 18.04 +) su macchina virtuale (es: Virtual Box) o tramite partizione.
  * Proponiamo un link alla guida ufficiale di GitHub per l'installazione: [GUIDA INSTALLAZIONE](https://github.com/ethz-asl/rotors_simulator)
  * Proponiamo anche un link (che consigliamo) in cui è presente una OVA per macchina virtuale VirtalBox, in modo da poterla importare ed avere un ambiente di sviluppo già pronto e funzionante: [DOWNLOAD OVA](https://univpm-my.sharepoint.com/:f:/g/personal/s1088279_studenti_univpm_it/EjDqAEOL1WRCgjfu0cDKMvsB2gNqCj9FmYp-Dh4ALNuY8g?e=PsrsZR)
  
  <a href="https://univpm-my.sharepoint.com/personal/s1088279_studenti_univpm_it/_layouts/15/onedrive.aspx?originalPath=aHR0cHM6Ly91bml2cG0tbXkuc2hhcmVwb2ludC5jb20vOmY6L2cvcGVyc29uYWwvczEwODgyNzlfc3R1ZGVudGlfdW5pdnBtX2l0L0VqRHFBRU9MMVdSQ2dqZnUwY0RLTXZzQjJnTnFDajlGbVlwLURoNEFMTnVZOGc%5FcnRpbWU9MGJsMUZTNWEyRWc&id=%2Fpersonal%2Fs1088279%5Fstudenti%5Funivpm%5Fit%2FDocuments%2FProgetto%20Misure%2FRotorS%28Melodic%29%2Eova&parent=%2Fpersonal%2Fs1088279%5Fstudenti%5Funivpm%5Fit%2FDocuments%2FProgetto%20Misure"><img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/OVA.png"/></a>
  
Per poter installare l'OVA sulla propria VirtualBox, seguire i seguenti passi:
  * Installare [VirtualBox](https://www.virtualbox.org/)
  * Aprire VirtualBox
  * `File > Importa Applicazione Virtuale`
  * Selezionare il file OVA scaricato attraverso la schermata che si aprirà dopo aver cliccato sull'icona della cartella in basso a destra
  * Cliccare su 'Successivo'
  * Lasciare le impostazioni così come sono e cliccare su 'Importa'
  * Attendere il completamento (circa qualche minuto)
  
*N.B. Per poter lavorare in piena serenità, consigliamo di avere un PC con almeno 8 GB di RAM e almeno 25 GB di spazio libero su disco. Istallando il software su una distribuzione Linux, da zero, porterà ad avere una serie di problemi che possono esssere risolti solamente se si conosce l'ambiente di sviluppo, pertanto sconsigliamo di farlo e di seguire l'installazione dell'OVA*

## <a name="gest-mac"/></a> 2. Gestione Macchina Virtuale
Per poter accedere alla macchina virtuale, una volta installata, cliccare due volte sull'icona rappresentativa (RotorS(Melodic))<br>
Le credenziali di accesso alla macchina virtuale sono le seguenti:
 * Username: rotors
 * Password: rotors
 
 <img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/ubuntu.png"/>
 
## <a name="gest-ros"/></a> 3. Gestione ROS & Gazebo
Per tutti i dettagli rimandiamo alla guida di [ROS.org](http://wiki.ros.org/)<br>
 * Gestione Ambiente:
   * Creazione Workspace: per poter creare la workspace (una directory in cui sono presenti al suo interni i, cosidetti, package di lavoro per Gazebo) basta semplicemente collocarsi in `/home` e crerare una directory (tramite linea di comando: `$ cd /home` + `$ mkdir nome_workspace`)
   * Filesystem:
      * Package: Organizzazione software (librerie, script ecc...)
      * Manifest(package.xml): descrizione del package (metadati)
 
### <a name="gest-ros-pac"/></a> 3.1. Package

#### <a name="gest-ros-pac-dir"/></a> 3.1.1. Directory Tree

     my-package/
       CMakeList.txt(file testo standard)
       package.xml

#### <a name="gest-ros-pac-dir2"/></a> 3.1.2. Directory Tree MultiPackage

    workspace/
     src/
      package_1/
        CMakeList.txt
        package.xml
      package_2/
        CMakeList.txt
        package.xml

#### <a name="gest-ros-pac-make"/></a> 3.1.3. Creare un package

Da terminale:
 * `$ cd ~/workspace/src`
 * `$ catkin_create_pkg nome_package`
  * comando generale: `$ catkin_create_pkg <name> [dep1] [dep2] [dep3]`<br>
Una volta create il package sarà possibile inserire all'interno le directory che andranno a strutturare il progetto.
 * `$ cd nome_package`
 * `$ mkdir launch | mkdir worlds`
Le due directory create ospiteranno la struttura dell'intero simulatore.
All'interno di `launch` verranno creati e/o posizionati i file `.launch` in cui al loro interno hanno una serie di tag che vanno a identificare il mondo virtuale, il robot e tutte le caratteristiche da implementare in un mondo virtuale (vedremo launch nel dettaglio dopo).
All'interno di `worlds` verranno creati e/o posizionati i file `.world` in cui al loro intewrno hanno una serie di tag che vanno a identificare, in modo specifico, un mondo e le sue caratterisriche (esempio: una casa, un ambiente vuoto, una cava ecc...).

#### <a name="gest-ros-pac-pac"/></a> 3.1.4. Package.xml
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
 
 <img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/catkinmake.png"/>
 
 * `$ source ~/devel/setup.bash`
Fatto ciò sarà possibile eseguire un file di launch all'interno della workspace attracerso il comando `$ roslaunch <directory_package> <nome_file_launch>`

## <a name="run"/></a> 4. Lancio Del Software
Per poter lanciare il software e verificare che tutto nella macchina virtuale funzioni correttamente, seguire la seguente guida:
 * Aprire il terminale
 
                $ mkdir workspace_catkin
                $ cd workspace_catkin
                $ mkdir src
                $ cd src
                $ catkin_create_pkg prova_gazebo --> 'prova_gazebo' può essere sostituito con qualsiasi nome si voglia, per semplicità facciamo questo esempio.
                $ cd prova_gazebo
                $ mkdir launch | mkdir worlds
                $ cd launch
                $ sudo nano prova.launch
                
 * Si aprirà un editor di file e al suo interno copiamo e incolliamo quanto segue:
 
               <launch>
               <!-- We resume the logic in empty_world.launch, changing only the name of the world to be launched -->
               <include file="$(find gazebo_ros)/launch/empty_world.launch">
                 <arg name="world_name" value="$(find prova_gazebo)/worlds/prova.world"/>
                 <!-- more default parameters can be changed here -->
               </include>
               </launch>`

     *N.B. Per i prossimi file che si creeranno, basta sostituire all'interno dei tag la parola 'prova_gazebo' e 'prova.world' con il path e il file world che si vuole utilizzare*
     
        $ cd ..
        $ cd worlds
        $ sudo nano prova.world
        
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
          
     *N.B. Si potrà inserire al suo interno tutte le componenti che si vogliono, chiamate 'model'. In questa piccola porzione di mondo troviamo un terreno, un sole(luminosità radiale) e una stazione di benzina (che potrà essere reperibile insieme a tantissime altre strutture e oggetti all'interno del database online di Gazebo. Esempio: al posto di gas_statio è possibile mettere empty o qualsiasi altro modello di mondo presente a [Questo Link](http://models.gazebosim.org/)*
     
       $ cd .. 
       $ cd ..
       $ cd ..
       $ catkin_make
       $ source ~/devel/setup.bash
       $ roslaunch prova_gazebo prova.launch --> partirà GAzebo e ROS con la simulazione di una stazione di servizio.
 
 <img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/GasStation.png"/>
 
Per poter inserire un robot all'interno della scena, basta seguire i seguenti passi:
 * Aprire il file `prova.launch`:
   * `$ sudo nano src/prova_gazebo/launch/prova.launch`
 * Inserire quanto segue, prima del `</launch>`:
 
       <!-- Spawn a robot into Gazebo -->
       <node name="spawn_urdf" pkg="gazebo_ros" type="spawn_model" args="-file $(find baxter_description)/urdf/baxter.urdf -urdf -z 1 -model baxter" />
       
  *N.B. Se si sta eseguendo l'OVA, non si avranno problemi, in altri casi bisogna installare il pacchetto aggiuntivo del roboto attraverso il comando `$ git clone https://github.com/RethinkRobotics/baxter_common.git` e ricompilare la workspace con `$ catkin_make`.*
  
     $ catkin_make
     $ source ~/devel/setup.bash
     $ roslaunch prova_gazebo prova.launch --> Si aprirà la stazione di servizio con un robot presente sulla scena.

<img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Gas_baxter.png"/>


Il software può essere lanciato con tutte le prove e esempi che si trovano online, allo stesso modo, oppure creando, come nella guida, un file di lancio e uno di mondo che vada a rappresentare quello che si vuole realizzare. I vari modelli che è possibile utilizzare sono presenti al seguente [LINK](http://models.gazebosim.org/)


## <a name="command"/></a> 5. Uso & Comandi di Gazebo
Una volta fatto partire un package, verrà aperta una finestra di Gazebo con il mondo virtuale che abbiamo creto o che abbiamo importato.
La finestra di Gazebo deve apparire pressapoco così:

<img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_01.png"/>

*N.B. il file di lanch che abbiamo fatto partire è quello presente nella directory ufficiale, in cui sono presenti tutti gli esempi di simulazione, reperibile a [questo link](https://github.com/ethz-asl/rotors_simulator). Tuttavia la directory è già presente mella macchina virtuale scaricata. Per poterla far partire basta digitare su terminale i seguenti comandi: `$ cd diffDrive_ws` + `$  source devel/setup.bash` + `$ roslaunch rotors_gazebo mav_hovering_example.launch`. Tali file sono presenti nle persorso `/home/diffDrive_ws/src/rotors_simulation/rotors_gazebo/launch`.*

Come possiamo vedere dall'immagine nella parte alta abbiamo la barra degli strumenti, in cui è possibile vedere tutte le operazioni grafiche sulla scena rappresentata.

<img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_02.png"/>

I primi 4 sono i tasti posizionali, in cui è possibile muoversi nella mappa, allargare e ruotare. I comandi possono essere impartiti anche da mouse, infatti, con la rotella possiamo effettuare uno zoom sull'inquadratura e il tasto sinistro ci permette di trascinare la visuale. Il tasto con il magnete ci permette di muoverci, trascinando la mappa con il tasto sinistro, facendo ruotare la mappa stessa. I comandi rappresentati da una sfera, un cubo e un cilindro permettono di creare delle figure geometriche tridimensionali sulla mappa. I comandi identificati dal sole o raggi solari permettono di cambiare l'ìlluminazione.

Nella parte sinistra della finestra vediamo un menu che identifica i vari componenti presenti sulla mappa:

<img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_03.png"/>

Cliccando su un componente è possibile vedere le sotto-componenti di cui è composto. Nel caso del drone aereo, cliccando col tatso destro è possibile vedere un menu a tendina e cliccando su 'follow' sarà possibile seguire i movimenti del drone e dov'è collocato in quel preciso momento.

In basso è presente la timeline della simulazione e all'inizio di questa timeline troviamo il bottone di play/pausa che una volta cliccato congela lo stato della simulazione (se si clicca 'pausa') o la fa avanzare nel tempo (se si clicca 'play'). Nella simulazione che si è fatta partire (mav_hovering_example.launch) viene fatto fluttuare a mezz'aria il drone attraverso le caratteristiche di odometria.

### <a name="control"/></a> 5.1. Controllo del drone
#### <a name="control-key"/></a> 5.1.1. Tastiera
In questo paragrafo vedremo come controllare un drone attraverso i comandi impartiti da tastiera.

*N.B. Nella macchina virtuale scaricata saranno già presente tutti i pacchetti per permettere di controllare un drone. In altri casi bisogna seguire la guida presente a [questo link](https://github.com/ethz-asl/rotors_simulator/wiki/Setup-virtual-keyboard-joystick)*

Per poter far partire una simulazione con drone controllabile da tastiera, seguire questi passi:
 * Aprire il terminale
 
         $ cd diffDrive_ws
         $ source devel/setup.bash
         $ roslaunch rotors_gazebo mav_with_keyboard.launch mav_name:=firefly world_name:=basic
         
    Verrà fatto partire un simulatore con un lettore di comandi attraverso pygame (un plag-in di python).
    
    <img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_05.png"/>
    
    *N.B. Potrebbe capitare che durante l'avvio del programma risulti un errore di questo tipo:*
    <img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_04.png"/>
    
    *E il controller della tastiera non verrà fuori. Per rislvere ciò eseguire questi comandi da terminale:*
        
           $ cd /dev
           $ sudo chmod -R 777 uinput
           
     *Riportarsi in `diffDrive_ws` e rieseguire i comandi.*
     
  * Sarà possibile controllare il drone dopo aver cliccato play
  * I controlli si focalizzano su 8 tasti principali: W, A, S, D, ↓, ↑, →, ←.
  * I controlli sono estremamente sensibili e bisogna prendere esperienza
  
#### <a name="control-joy"/></a> 5.1.1. Joypad
Per poter far partire una simulazione con drone controllabile da Joypad, seguire questi passi:
 * Connettere un joypad al PC tramite porta USB o Bluetooth
 * Aprire il terminale
 
         $ cd diffDrive_ws
         $ source devel/setup.bash
         $ roslaunch rotors_gazebo mav_with_joy.launch mav_name:=firefly world_name:=basic
 
 * Sarà possibile controllare il drone dopo aver cliccato play
  * I controlli si focalizzano su L2 e sugli analogici per modulare i valori di accelerazione, pitch, roll e thrust
  * I controlli sono estremamente sensibili e bisogna prendere esperienza
  
 ### <a name="plugin"/></a> 5.2. Utilizzo Plugin
 Per poter utilizzare un plugin, in ROS+Gazebo, ricorriamo allòa guida ufficiale e facciamo un esempio pratico.
 I plugin Gazebo offrono ai tuoi modelli URDF(Unified Robotic Description Format), ovvero i file che descrivono un determinato robot o drone che deve essere utilizzato, maggiori funzionalità e possono collegare messaggi ROS e chiamate di servizio per l'uscita del sensore e l'ingresso del motore.
 
In breve, il plugin è inserito all'interno dell'URDF attraverso la tag `<gazebo>`:

      <robot>
        ... robot description ...
        <gazebo>
          <plugin name="differential_drive_controller" filename="libdiffdrive_plugin.so">
            ... plugin parameters ...
          </plugin>
        </gazebo>
        ... robot description ...
      </robot>
      
La specifica dei plug-in del sensore è leggermente diversa; i sensori in Gazebo sono pensati per essere collegati ai `<plugin>`, quindi la tag `<gazebo>`che descrive quel sensore deve essere un riferimento a quel collegamento. Per esempio: 

     <robot>
       ... robot description ...
       <link name="sensor_link">
         ... link description ...
       </link>

       <gazebo reference="sensor_link">
         <sensor type="camera" name="camera1">
           ... sensor parameters ...
           <plugin name="camera_controller" filename="libgazebo_ros_camera.so">
             ... plugin parameters ..
           </plugin>
         </sensor>
       </gazebo>

     </robot>
     
     
Parlato in generale di quelli che sono i plugin forniti da Gazebo, vediamo un plugin utilizzato in questo ambito, ovvero la videocamera o semplicemente camera.

#### <a name="camera"/></a> 5.2.1. Camera
Esponiamo, prima di tutto un esempio, che utilizza la camera e poi andremo a strutturare nel dettaglio il plugin spiegando le sue caratteristiche.
Per utilizzare una workspace già pronta e poterne testarne l'uso della camera, apriamo il terminale e seguimo i seguenti passi:

          $ cd /home
          $ git clone https://github.com/richardw05/mybot_ws
          $ cd mybot_ws
          
Questa sarà la nuova workspace in cui, al suo interno, è pressente una serie di package su cui prendere spunto per i lavori di utilizzo camera futuri.

          $ catkin_make
          $ ls
          
Noteremo la comparsa di nuove directory, tra cui `/devel` e `/logs` per citarne due.

          $ source devel/setup.bash
          
La workspace è pronta e quindi sarà possibile far partire i file di lancio presenti all'interno della directory `/mybot_ws/src/<dir_scelta>/launch`.

Proviamo un esempio di lancio:

     $ roslaunch mybot_gazebo mybot_world.launch
     
*N.B. se premiamo il tasto TAB quando si esegue una chiamata, ci verrà in aiuto per la compilazione automatica del nome del file di tipo `.launch`*

Aprire un altro terminale e digitare:

     $ source mybot_ws/devel/setup.bash
     $ rosrun image_view image_view image: = /mybot/camera1/image_raw
     
Si apriranno due schermate: 
 * Gazebo, con il drone di terra e l'ambiente virtuale
 * La finestra di visuale del drone
 
Se dovessimo mettiamo un ostacolo davanti al drone, ad esempio una sfera o una figura tridimensionale, questa apparirà anche nell'inquadratura della camera in tempo reale.

<img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_06.png"/>


La visuale è disponibile anche facendo partire RVIZ (un software di gestione) e noteremo che la camera invia delle immagini che vengono visualizzate in tempo reale. 

    $ source mybot_ws/devel/setup.bash
    $ roslaunch mybot_description mybot_rviz.launch
    
<img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/Screen/schermata_07.png"/>

Se non lo si visualizza, provare a cliccare su *Add*, aggiungere *Image*. Aprire *Image* sul menu sinistro e su *Image Topic* cliccare sul box a destra e cliccare sul percorso che uscirà dal menu a tendina (verrà visualizzato solamnete la camera collegata al drone di Gazebo).


Il codice incorporato nel file `.launch`, in modo da attivare la camera e visualizzare il contenuto è il seguente:

     <link name="camera">
        <collision>
          <origin xyz="0 0 0" rpy="0 0 0"/>
          <geometry>
            <box size="${cameraSize} ${cameraSize} ${cameraSize}"/>
          </geometry>
        </collision>

        <visual>
          <origin xyz="0 0 0" rpy="0 0 0"/>
          <geometry>
            <box size="${cameraSize} ${cameraSize} ${cameraSize}"/>
          </geometry>
          <material name="green"/>
        </visual>

        <inertial>
          <mass value="${cameraMass}" />
          <origin xyz="0 0 0" rpy="0 0 0"/>
          <box_inertia m="${cameraMass}" x="${cameraSize}" y="${cameraSize}" z="${cameraSize}" />
          <inertia ixx="1e-6" ixy="0" ixz="0" iyy="1e-6" iyz="0" izz="1e-6" />
        </inertial>
      </link>

      <joint name="camera_joint" type="fixed">
        <axis xyz="0 1 0" />
        <origin xyz=".2 0 0" rpy="0 0 0"/>
        <parent link="chassis"/>
        <child link="camera"/>
      </joint>
      
      
Importare tale codice nel file del drone `.xacro`, mentre nel file del drone con estensione `.gazebo` importare il seguente codice:

     <gazebo reference="camera">
         <material>Gazebo/Green</material>
         <sensor type="camera" name="camera1">
           <update_rate>30.0</update_rate>
           <camera name="head">
             <horizontal_fov>1.3962634</horizontal_fov>
             <image>
               <width>800</width>
               <height>800</height>
               <format>R8G8B8</format>
             </image>
             <clip>
               <near>0.02</near>
               <far>300</far>
             </clip>
           </camera>
           <plugin name="camera_controller" filename="libgazebo_ros_camera.so">
             <alwaysOn>true</alwaysOn>
             <updateRate>0.0</updateRate>
             <cameraName>mybot/camera1</cameraName>
             <imageTopicName>image_raw</imageTopicName>
             <cameraInfoTopicName>camera_info</cameraInfoTopicName>
             <frameName>camera</frameName>
             <hackBaseline>0.07</hackBaseline>
             <distortionK1>0.0</distortionK1>
             <distortionK2>0.0</distortionK2>
             <distortionK3>0.0</distortionK3>
             <distortionT1>0.0</distortionT1>
             <distortionT2>0.0</distortionT2>
           </plugin>
         </sensor>
       </gazebo>

Tali codici attivano l'uso della camera su un qualsiasi drone. 

*N.B. Per droni aerei, o di forma differente, alcuni dei dati dovranno essere modificati per poter essere adattati al robot stesso. Nell'esempio si parla di un drone di terra molto semplice, con due ruote e una scocca a forma di parallelepipedo*


_________________________________________________________________________________________

<a href="http://gazebosim.org/"><img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/gazebo_logo.png"/> <a href="https://www.ros.org//"><img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/ros_logo.png"/> <a href="https://www.ubuntu-it.org/"><img src="https://github.com/Project-Misure/RotorS-Gazebo/blob/master/Img/ubuntu_logo.png"/>
