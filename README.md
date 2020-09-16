# ROS-Gazebo
Software di simulazione per droni: <br>
Versione GAZEBO 7.0<br>
Versione ROS Melodic<br>

# Guida passo-passo
## Installazione
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
  
*N.B. Per poter lavorare in piena serenità, consigliamo di avere un PC con almeno 8 GB di RAM e almeno 25 GB di spazio libero su disco*

## Gestione Macchina Virtuale
Per poter accedere alla macchina virtuale, una volta installata, cliccare due volte sull'icona rappresentativa (RotorS(Melodic))<br>
Le credenziali di accesso alla macchina virtuale sono le seguenti:
 * Username: rotors
 * Password: rotors
 
## Gestione ROS & Gazebo
Per tutti i dettagli rimandiamo alla guida di [ROS.org](http://wiki.ros.org/)<br>
 * Gestione Ambiente:
   * Creazione Workspace: per poter creare la workspace (una directory in cui sono presenti al suo interni i, cosidetti, package di lavoro per Gazebo) basta semplicemente collocarsi in `/home` e crerare una directory (tramite linea di comando: `cd /home` + `mkdir nome_workspace`)
   * Filesystem:
      * Package: Organizzazione software (librerie, script ecc...)
      * Manifest(package.xml): descrizione del package (metadati)

