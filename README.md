# Anleitung zum Erstellen eines Kubernetes-Klusters mit VirtualBox und Vagrant

Diese Anleitung führt Sie Schritt für Schritt durch die Installation von [VirtualBox](https://www.virtualbox.org/) und [Vagrant](https://www.vagrantup.com/) auf einem Windows-System und zeigt Ihnen, wie Sie ihr eigenen Kubernetes-Kluster erstellen. Als Kubernetes-Distribution wird [K3s](https://k3s.io/) verwendet.

## Voraussetzungen

- Ein Computer mit Windows-Betriebssystem
- Internetzugang zum Herunterladen der Installationsdateien

## Schritt 1: VirtualBox installieren

1. **Download**:
   - Besuchen Sie die [VirtualBox Download-Seite](https://www.virtualbox.org/wiki/Downloads).
   - Klicken Sie auf den Link für die Windows Hosts, um das Installationsprogramm herunterzuladen.

2. **Installation**:
   - Öffnen Sie die heruntergeladene Datei (`VirtualBox-x.x.x-x-Win.exe`).
   - Folgen Sie den Anweisungen im Installationsassistenten und wählen Sie dabei die Standardoptionen.

3. **Bestätigen**:
   - Starten Sie VirtualBox nach der Installation, um sicherzustellen, dass es ordnungsgemäß installiert wurde.

## Schritt 2: Vagrant installieren

1. **Download**:
   - Besuchen Sie die [Vagrant Download-Seite](https://developer.hashicorp.com/vagrant/install#windows).
   - Klicken Sie auf den Link für Windows, um das Installationsprogramm herunterzuladen.

2. **Installation**:
   - Öffnen Sie die heruntergeladene Datei (`vagrant_x.x.x_windows_x.msi`).
   - Folgen Sie den Anweisungen im Installationsassistenten.
   - Wählen Sie die Standardoptionen.

3. **Bestätigen**:
   - Öffnen Sie eine Eingabeaufforderung (CMD) und geben Sie `vagrant --version` ein, um sicherzustellen, dass Vagrant erfolgreich installiert wurde.

## Schritt 3: VMs mit Kubernetes-Kluster erstellen

1. **Projektverzeichnis erstellen**:
   - Erstellen Sie ein neues Verzeichnis für Ihr Vagrant-Projekt, z.B. `C:\vagrant_project`.
   - Öffnen Sie eine Eingabeaufforderung und navigieren Sie zu diesem Verzeichnis:

     ```sh
     cd C:\vagrant_project
     ```

2. **Vagrantfile dorthin kopieren**:
   - Sie haben zwei Optionen, um das Vagrantfile in das Projektverzeichnis zu kopieren:
        - **Option 1: Git Repository klonen**:
          - Klonen Sie das Repository, das das Vagrantfile enthält (dafür muss `git` installiert sein):

            ```sh
            git clone <REPOSITORY_URL> .
            ```

        - **Option 2: Vagrantfile manuell herunterladen**:
          - Laden Sie das Vagrantfile manuell aus dem [Git-Repository](<REPOSITORY_URL>) herunter und verschieben Sie es in ihr Verzeichnis `C:\vagrant_project`.

3. **Vagrant-Umgebung (VMs) starten**:
   - Führen Sie den folgenden Befehl aus, um die Vagrant-Umgebung zu starten:

        ```sh
        vagrant up
        ```

4. **Bestätigen**:
   - Vagrant wird die spezifizierte virtuelle Maschine herunterladen und einrichten.
   - Nach Abschluss können Sie über SSH auf die VM zugreifen:

        ```sh
        ssh vagrant@192.168.56.101
        ```

   - Verwenden Sie dabei den Benutzernamen `vagrant` und das Passwort `vagrant`.
   - Sollten Sie im Vagrantfile die Start-IP-Adresse geändert haben, müssen Sie ihren SSH-Befehl dementsprechend anpassen.

5. **Vagrant-Umgebung (VMs) entfernen**
    - Führen Sie den folgenden Befehl aus, um die Vagrant-Umgebung wieder zu entfernen:

        ```sh
        vagrant destroy
        ```

## Zusammenfassung

Sie haben nun VirtualBox und Vagrant auf Ihrem Windows-System installiert und erfolgreich eine Vagrant-Umgebung mit einem Kubernetes-Kluster erstellt. Im Vagrantfile können Sie die Start-IP-Adresse und die Anzahl der VMs anpassen. Beachten Sie dabei, dass immer nur die erste VM der Master ist und alle weiteren VMs als Worker konfiguriert sind. Sie können jetzt mit der Nutzung und Konfiguration Ihres Klusters beginnen.


## Weiterführende Links

- [VirtualBox Dokumentation](https://www.virtualbox.org/wiki/Documentation)
- [Vagrant Dokumentation](https://www.vagrantup.com/docs)

