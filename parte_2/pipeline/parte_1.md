## Pipeline
### Che cos'è?
- L'utilizzo delle pipeline è una tecnica di implementazione nella quale molteplici istruzioni vengono sovrapposte in esecuzione;
- Il vantaggio rispetto a implementazioni "non-pipelined" è che richiede molto meno tempo. Quello che fa è `aumentare il throughput` distribuendo il lavoro in `parallelo` anzichè attendere la completa esecuzione di un'istruzione per volta;
- Sotto condizioni ideali e con un grande numero di istruzioni l'incremento di velocità dovuto alle pipeline è approssimativamente equivalente al numero degli stage della pipe;
- Tuttavia vi sono maggiori complicazioni.

### Design dell'instruction set
- Tutte le `istruzioni nel MIPS hanno la stessa lunghezza`. Questa restrizione facilità il fetch delle istruzioni nel primo stadio della pipeline e la loro decodifica nel secondo stadio;
- Il MIPS `ha pochi format delle istruzioni`, con i campi del registro sorgente che sono locati nello stesso spazio in ogni istruzione. Questa simmetria significa che nel secondo stadio si può iniziare la lettura del file del registro nello stesso momento in cui l'hardware determina quale tipo di istruzione è stata passata (fetched);
- Gli `operandi di memoria compaiono solo nei caricamenti e nei salvataggi` nel MIPS. Questa restrizione comporta che si può sfruttare lo stadio di esecuzione per calcolare l'indirizzo di memoria e poi accedere alla memoria nella fase successiva;
- Gli `operandi in memoria devono essere allineati`. Dunque non ci si deve preoccupare di una singola istruzione di trasferimento dei dati che richieda due accessi ai dati in memoria. I dati richiesti possono essere trasferiti tra processore e memoria in una sola fase della pipeline.

### [Hazard](https://github.com/Gabri432/Architettura_elaboratori/blob/master/hazard/parte_1.md)