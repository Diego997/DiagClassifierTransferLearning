# DiagClassifierTransferLearning

Il codice è suddiviso in 4 parti, la prima riguarda la classificazione con la VGG16
1) VGG16.ipynb


	Da qui si vanno ad estrarre le feature dalle immagini presenti nella cartella "Paintings"
	le feature estratte vengono salvate nel file "CNNFeatureExtraction.csv"
	successivamente vengono utilizzati degli algoritmi di classificazione per le feature estratte
2) neuralNetwork.ipynb 


	Qui è presente un tentativo di addestramento della rete neurale con l'utilizzo dell'intera immagine come fatto per la VGG16
	ma questo ha portato a dei pessimi risultati con una accuratezza in fase di addestramento molto bassa.
	per poter utilizzare il notebook bisogna scaricare il dateset IAM dal seguente link: 
	https://fki.tic.heia-fr.ch/databases/iam-handwriting-database
	in particolar modo viene utilizzata la cartella "forms" e il file "forms.txt"
	successivamente va eseguita tutta la parte di pre-processing che rimuove le parti non contenenti testo scritto a mano 
	e rende le immagini delle stesse dimensioni senza applicare resizing, generando la cartella rectFormsSegment che verrà 
	utilizzata successivamente per l'addestramento.
	Questo lavoro avrebbe dovuto concludersi con l'estrazione delle featrures e la classificazione ma dati i pessimi risultati
	durante l'addestramento si è deciso di non proseguire con questi due passaggi 
3) nN Sentences.ipynb 


	Come per il precedente notebook anche qui è necessario scaricare il dataset IAM, del quale verra utilizzato il file 
	testuale "forms.txt" e la cartella  "sentences" poichè qui verranno utilizzate le frasi invece che l'intero foglio. 
	Eseguendo il codice verrà generata una cartella "temp_sentences" dove saranno contenute solo le frasi dei 50 scrittori 
	con più testi scritti, successivamente verrà applicata l'Augmentation, infine ci sarà la CNN e l'addestramento
	durante il quale verrà salvato ad ogni epoca un checkpoint nella cartella "model_checkpoint", nel lavoro 
	effettuato l'addestramento è stato fatto per 200 epoche, successivamente sono state rinominate le epoche di interesse:
	"check_20.hdf5", "check_100.hdf5", "check_200.hdf5"
4) TLNNSentences.ipynb 


	Infine in questo ultimo notebook, sono state utilizzate le immagini relative alla disgrafia suddivise in linee salvate
	nella cartella "Lines", inoltre è stato utilizzato il dataset updatedDataset.csv contenente le informazioni relative
	alle immagini (verrà utilizzato solo l'ID dell'immagine e la diagnosi) tutto questo per poter estrarre le feature dalla 
	rete neurale preaddestrata.
	Quindi alle immagini viene applicato lo stesso pre-processing e augmentation ed infine verranno estratte le feature dai 
	tre modelli generati dal notebook precedente ("check_20.hdf5", "check_100.hdf5", "check_200.hdf5")
	Per ognuno di questi verranno generati due file csv durante l'estrazione, uno dopo la rimozione di 5 layer l'altro 6 .
	Quindi verranno generati i seguenti file: 
		"CNNFeatureExtractionEpoch20.-5layer.csv"
		,"CNNFeatureExtractionEpoch20.-6layer.csv"
		,"CNNFeatureExtractionEpoch100.-5layer.csv"
		,"CNNFeatureExtractionEpoch100.-6layer.csv"
		,"CNNFeatureExtractionEpoch200.-5layer.csv"
		,"CNNFeatureExtractionEpoch200.-6layer.csv".
	Dai quali verrà poi effettuata la classificazione 
	(Dato il tempo molto elevato per questa esecuzione di codice la generazione del dataset e la ridenominazione viene fatta
	manualmente andando a modificare il modello da leggere e il numero di layer da rimuovere ed il nome dei file generati)
	Infine una volta generati i csv si potrà proseguire con la classificazione per ognuno di essi
