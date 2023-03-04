## Hazard
### Cos'è?
- L'utilizzo delle pipeline porta al verificarsi di situazioni nelle quali non è possibile eseguire la prossima istruzione nel seguente ciclo di clock. Tali eventi si chiamano `Hazard` e si suddiviono in tre tipi: `strutturali`, `sui dati`, `sul controllo`.

### Hazard strutturali 
- Avvengono quando l'hardware non è in grado di supportare la combinazione di istruzioni che si vuole eseguire nello stesso ciclo. Si cerca di intervenire aumentando le risorse hardware, perchè diverse istruzioni necessitano delle stesse risorse;

### Hazard sui dati
- Avvengono quando la pipeline deve essere messa in stallo per l'attesa del completamento di un passaggio;
- Vengono causati dalla `dipendenza di una istruzione su un'altra precedente` che è ancora in pipeline e senza intervento tale stallo può essere serio. Per esempio la add scrive il risultato solo al quinto stadio, sprecando così 3 cicli di clock;
- L'utilizzo del compilatore non sarebbe soddisfaciente perchè tali dipendenze sono molto frequenti e l'attesa sarebbe troppo lunga;
- Si osserva dunque che `non è necessario il completamento dell'istruzione`. La tecnica utilizzata è quella del `forwarding` o `bypassing`, dove si fa utilizzo di buffer interni anzichè attendere i dati dai registri o dalla memoria.

### Hazard sul controllo
- Avvengono quando l'istruzione acquisita non è quella necessaria;
- Una prima soluzione è lo `stallo`, che anche se funziona risulta lento. L'istruzione successiva deve essere acquisita dopo la branch proprio nel ciclo di clock successivo. La pipeline non sa quale possa essere la prossima istruzione, dato che avrebbe da poco ricevuto l'istruzione di branch dalla memoria;
- Si potrebbe quindi attendere che la predizione della branch per sapere da quale indirizzo si farà il fetch.
- La seconda soluzione è la `predizione`. Una predizione corretta non comporta alcun rallentamento, una predizione sbagliata costa una ripetizione del lavoro.
#### Predizione
- Un approccio semplice è quello di ritenere che la branch non sia mai da prendere, che nel caso corretto la pipeline procede a piena velocità, altrimenti si verifica uno stallo;
- Un approccio più complesso è quello del `branch di predizione`, che predice che alcuni branch verranno presi ed altri no;
- La predizione può essere rigida e non tenere conto dell'individualità di una istruzione di branch specifico ma affidarsi a comportamenti classici;
- La predizione può essere `Dinamica` e quindi cambiare in base al successo di quella precedente. Si tiene traccia della storia di ogni branch come presa o non presa, e si usa il comportamento passato recente. L'accuratezza raggiunge il 90%;
- Quando la predizione è errata il controllo della pipeline deve assicurarsi che l'istruzione seguente tale errore non abbia effetto, e deve riprendere la pipeline dall'indirizzo di branch opportuno.
#### Delayed Branch (branch ritardata)
- La soluzione effettivamente usata nel MIPS, con la quale si esegue l'istruzione successiva sequenziale, prevede che la branch venga valutata dopo un ritardo di istruzione (one instruction delay). In genere il compilatore nasconde questo aspetto poichè riordina le istruzioni per ottenere il comportamento di branch desiderato;
- I programmi software nel MIPS piazzeranno immediatamente dopo l'istruzione di delayed branch un'istruzione che non ne sia stata affetta, e la branch presa cambia l'indirizzo dell'istruzione che segue questa istruzione sicura.
