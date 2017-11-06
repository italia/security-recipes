# domain-scan + Secure the News (deployment)

Sistema di deploy opensource per un'integrazione tra domain-scan e Secure the News.

## Descrizione

Prevede 3 ruoli Ansible per il deploy di:

- domain-scan
- securethenews
- import custom (in python)

Sono stati riscritti tutti i Dockerfile per la creazione di un ambiente adatto alla produzione a partire dai relativi script per development. Si è scelto di usare come base principale Debian. Sono stati aggiornati i pacchetti software laddove questi non causavano problemi con il sistema.

Il tutto è stato testato in locale e i default sono relativi a questo ambiente, ma è facilmente configurabile per un deploy remoto impostando le variabili del playbook base e gli host nel file hosts. Ulteriori variabili opzionali sono presenti come default dei vari ruoli.

L'architettura finale prevede:

- una macchina Docker con domain-scan avviata all'occorrenza;
- un cluster composto da macchine Docker: postgres, node+python, gunicorn, nginx; per securethenews;
- uno script in python che aggiorna lo scan e importa i dati in securethenews eseguito in cron.


## Istruzioni

Per l'esecuzione del sistema base è sufficiente avere installato Docker (nell'ambiente di deploy) e Ansible (in locale) e lanciare il comando:

ansible-playbook site.yml -i hosts
