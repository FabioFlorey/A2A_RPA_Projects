<!-------------------------------------------------------------------------------------------
=============================================================================================
Project Name
=============================================================================================
PDD - Process Definition Document
---------------------------------------------------------------------------------------------
The document describes the sequence of actions performed as part of the business process, the
conditions and rules of the process prior to automation (AS IS) as well as the new sequence 
of actions that the process will follow as a result of preparation for automation (TO BE).

:Authors: Fabio Craig Wimmer Florey <fabioflorey@icloud.com>
:Version: 0.0.1
:License: MIT-0
-------------------------------------------------------------------------------------------->

<div align="center">
  <img alt="Company Logo" 
           src="https://user-images.githubusercontent.com/93403866/236409188-33a0146a-75a7-4417-a92e-2c863c50a08d.png"
           height="50">
  </img>
  <h1>Process Definition</h1>
  <h4>Comitato Progetti</h4>
  <hr>
</div>

## Overview

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam ultricies, metus sed sodales tincidunt, ante erat ullamcorper enim, vel sollicitudin metus nisl eu ipsum. Ut ultricies euismod metus et interdum. Suspendisse nec tellus sit amet nunc fringilla congue vel laoreet metus. Aliquam quam dui, rutrum at ullamcorper quis, pulvinar quis nulla. Proin fermentum mauris in tellus tempor congue. Maecenas arcu sapien, elementum ac tempor at, elementum non massa. Nulla iaculis, dui a egestas efficitur, ipsum ipsum tempor elit, dignissim molestie ligula mi non massa. In pulvinar ligula id tincidunt aliquam. Nulla velit nisi, bibendum nec orci vitae, auctor ultrices felis. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Sed sit amet porta ligula. Morbi tincidunt mi a pulvinar sagittis. Sed mattis sed nisi at eleifend. Cras tristique pulvinar nibh, in fermentum sem vestibulum quis. Vivamus auctor velit felis, at auctor lorem fringilla et.

## Descrizione del progetto AS IS
### Iniziative: Prototype, Implementation

- **Estrazione dei dati da Service Now**
  1. **Accesso a Service Now**

  2. **Filtro delle iniziative su Service Now** <br><br>
    - Data Ipotizzata &rarr; 
    - Stato &rarr; `In Corso`
    - Area di Riferimento &rarr; `contiene {Termine}` <sub>nell'esempio: `Reti` per Reti OT, Reti IT, Reti</sub>
    <br><br>
    ```diff
    @@ NOTA: La mappatura dei filtri Service Now per ogni comitato  sarà effettuata in fase di sviluppo @@ 
    ```

  3. **Raggruppamento per funzioni owner**

  <a name="mappatura_prototype_implementation"></a>
  #### **Mappatura Service Now &rarr; PowerPoint (Prototype, Implementation)**

    Un subset delle colonne in Service Now viene estratto a colonne nella diaposita PowerPoint con un rapporto 1:1  `Stato iniziative in Prototype / Implementation`, ad eccezione dei campi `Milestone`,  `% completamento effettiva` e `% completamento proposta`.

    | Service Now               | PowerPoint                        |
    | :------------------------ | :-------------------------------- |
    | Area                      | Area di Riferimento               |
    | Nome progetto             | Nome iniziativa                   |
    | Descrizione               | Descrizione e Principali Evidenze |
    | Attività in corso         | Descrizione e Principali Evidenze |
    | Attività completate       | Descrizione e Principali Evidenze |
    | Prossimi passi            | Descrizione e Principali Evidenze |
    | Fase                      | FASE                              |
    | Data inizio progetto      | DATA AVVIO                        |
    | Data fine progetto        | DATA FINE                         |
    | [Milestone](#milestone)   | Milestone                         |
    | % completamento effettiva | Avanzamento                       |
    | % completamento proposta  | Avanzamento                       |
    | Indicatore di progetto    | Stato                             |

    <sub>Tabella 1. Mappatura Service Now &rarr; PowerPoint</sub>

    ##### Nome progetto
    Il campo `Nome progetto` dovrà essere linkato alla diapositiva con il medesimo nome
    
    ##### Descrizione e Principali Evidenze
    Il campo `Descrizione e Principali Evidenze` su PowerPoint è un join delle colonne Service Now: `Descrizione`, `Attività in corso`, `Attività completate` e `Prossimi passi`.

    ##### Milestone
    Il campo `Milestone` non è un campo presente all'interno delle colonne Service Now, ma è ricavabile da un sottogruppo di operazioni da effettuare per ogni progetto:

    1. Aprire il progetto
    2. Aprire la sezione `Gantt di Progetto`
    3. Esplodere il progetto nella sezione (unica riga presente)
    
    L'esplosione del progetto rendererà visibile dei sotto-task, per ogni sotto-task:

    4. Aprire il sotto-task
    5. Visitare la sezione `Dettagli`
    
    Nella sezione dettagli sarà presente un campo `Milestone` con una checkbox. Se il campo non flaggato, si può passare al prossimo sotto-task. Se il campo è flaggato.

    6. Estarre l'informazione da `Breve descrizione`
    
    Da qui sarà necessario tornare indietro alla lista dei sottotask e passare al prossimo.

    Il campo `Milestone` sarà la join del campo `Breve descrizione` per ciascun task.

    ```diff
    -- Non si capisce bene da dove estrarre la milestone, se effettivamente è 'Breve descrizione' perché all GG/11/2023 la funzionalità non era stata rilasciata.
    ```
    
    ##### Avanzamento
    Il campo `Avanzamento (Powerpoint)` corrisponderà a uno dei due campi a seconda di quanto scelto dall'esecutore..
    
    ```diff
    @@ NOTA: Questa scelta sarà a discrezione dell'utente ed effettuata all'interno del file di input nel processo TO BE @@ 
    ```

    Il campo della presentazione Stato, va anch'esso mappato seguendo il seguente schema:
    
    | Indicatore di progetto (Service Now) | Stato (PowerPoint) |
    | :----------------------------------- | :----------------: |
    | In linea                             | 🟢                |
    | Rischi da gestire                    | 🟡                |
    | Criticità da gestire                 | 🔴                |

    <a name="tabella-2"></a>
    <sub>Tabella 2. Mappatura Service Now &rarr; PowerPoint</sub>


- **Inserimento dei dati nella diapositiva PowerPoint**
 
  Seguendo la <a href="#mappatura_prototype_implementation">mappatura lativa alla fase di Prototype e Implementation</a>, per ogni Funzione owner, per ciascun progetto listato, inserire una tabella di massimo 2 righe con in dati mappati corrispondenti corredando ciascuna diapositiva con un elemento grafico corrispondente alla Funzione owner.
  
  Ad ogni funzione owner è attribuito un nome &rarr; colore:
 
   | Nome (PowerPoint) | Colore (PowerPoint) | Funzione Owner | 
   | :---------------- | :------------------ | :------------- | 
   | Digital           |                     |                | 
   | Dati              |                     |                |
   | Innovation        |                     |                |
   | R&D               |                     |                |

    <a name="tabella-2"></a>
    <sub>Tabella 2. Figure PowerPoint &rarr; Funzione Owner </sub>
    
  ```diff
  -- NOTA: da rivedere
  ```  

#### Iniziative: Idea, Concept, Solution


#### Iniziative Concluse
