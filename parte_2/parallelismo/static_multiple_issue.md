# Static Multiple Issue
- I processori di tipo Static multiple-issue usano il `compilatore` per l'assistenza all'impacchettamento delle istruzioni e alla gestione degli hazard;
- In un tale processore l'insieme delle istruzioni rilasciate in un dato ciclo di clock viene chiamato `issue-packet`, che quindi costituisce un'unica grande istruzione con molteplici operazioni;
- Alcune delle responsabilità di tale compilatore può comprendere la predizione statica della branch e lo scheduling del codice per ridurre o prevenire del tutto gli hazard;
- Risulta comodo pensare all'issue-packet come un'istruzione che permette diverse operazioni in campi predefiniti, risultando in un approccio detto `Very Long Instruction Word (VLIW)`.