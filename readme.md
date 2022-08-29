# Dokumentation Praktische Arbeit Vertiefung A - C

## Auftrag 1: Jobs

### Aufgabenstellung

Die Fachabteilungen legen mit grossen Batchjobs jeweils die ganze Informatik lahm. Diese Batchjobs sollen unterteilt und so strukturiert werden, dass sie jederzeit im Hintergrund durchgeführt werden können.

### Umsetzung

In dieser Aufgabe erstellen wir einen Job, der on Demand ausgeführt wird, und einen CronJob, der regelmässig automatisch ausgeführt wird. Es handelt sich um Pseude Jobs, die eine Funktionalität simulieren, jedoch nicht wirklich etwas machen.

#### Job erstellen

Als erstes erstellen deklarieren wir den Job in einem Yaml File:

```
apiVersion: batch/v1
kind: Job
metadata:
  name: backup
spec:
  template:
    spec:
      containers:
      - name: backup
        image: alpine
        imagePullPolicy: IfNotPresent
        command: 
        - echo Starting Backup...
        - wget https://raw.githubusercontent.com/ar-do/vcnt/main/jobs/backup_source/backup_file.txt
        - sleep 5
        - echo Backup done!
      restartPolicy: Never
```

Dieser Job holt sich ein Pseudo File auf dieser Repo, wartet 5 Sekunden und schreibt dann in die Konsole, dass das Backup durchgeführt wurde.

#### Job starten

Als nächstes muss auf dem Cluster der Job gestartet werden:
```
kubectl apply -f https://raw.githubusercontent.com/ar-do/vcnt/main/jobs/1_backup_job.yaml
```

#### CronJob erstellen

#### CronJob starten

#### Pods verwalten

## Auftrag 2: Health Probe Pattern

### Aufgabenstellung

Die von der Entwicklung angelieferten Microservices blockieren oder reagieren nicht mehr auf Kundenanfragen. Mittels den "Health Probe Pattern" soll die Ausfallsicherheit der Microservices verbessert werden.

### Umsetzung

## Auftrag 3: Init Container

### Aufgabenstellung

Die angelieferten Container Images weissenerhebliche Sicherheitsmängel auf. Und/oder beinhalten Abhandlungen, z.B. Erstellen von Datenbanktabellen, die nicht in die Container Images gehören. Mittels separaten InitContainer sollen die Sicherheitsmängel verkleinert werden. Nicht zu Microservices gehörende Abhandlungen, z.B. Erstellen von Datenbanktabellen, soll in separate InitContainer ausgelagert werden.

### Umsetzung
