## Instructions

## Structure du projet
                         Partie A:
examen_devops-project/
├── app/
│   └── server.py
├── Dockerfile
├── docker-compose.yml
└── README.md

  
## app/server.py

from http.server import HTTPServer, BaseHTTPRequestHandler

class SimpleHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        # En-têtes de réponse
        self.send_response(200)
        self.send_header("Content-type", "text/html")
        self.end_headers()
        # Contenu de la réponse
        message = "<html><body><h1>Hello, Docker!</h1></body></html>"
        self.wfile.write(message.encode("utf-8"))

if __name__ == "__main__":
    PORT = 8000
    server_address = ("0.0.0.0", PORT)
    httpd = HTTPServer(server_address, SimpleHandler)
    print(f"Serving on port {PORT}...")
    httpd.serve_forever()

## fichier app/Dockerfile

   # Utiliser une image de base Python
   FROM python:3.9-slim

   # Définir le répertoire de travail
   WORKDIR /app

   # Copier le fichier server.py dans l'image
   COPY app/server.py .

   # Exposer le port 8000
   EXPOSE 8000

   # Commande pour exécuter le serveur
   CMD ["python", "server.py"]

 ## fichier docker-Compose.yml  


                
### Exécution avec Docker
         
1. Construire l'image Docker :
   
   # docker build -t examen-devops-app .
2. Lancer docker Compose

   # docker-compose up --build

3. accéder au server a l' addresse suivante 

  # http://localhost:8000



## Partie B : Pousser l’image de l’application vers DockerHub

### Étapes

1. **Construire l'image Docker** :
   
    docker build -t mouaz30/examen_devops:latest .

2. **Se connecter a DockerHub** : 

   docker login

3.  **Taguer l'image**  :

   docker tag examendevops-web Thierno/examen-devops:latest

4. **Pousser l'image** :

   docker push mouaz30/examen_devops:latest

## Automatisation du Push vers DockerHub

### Pipeline CI/CD

Ce projet utilise GitHub Actions pour automatiser la construction et le push de l'image Docker à chaque modification sur la branche principale.

### Configuration des Secrets

1. Accédez à votre dépôt GitHub.
2. Allez dans **Settings** > **Secrets and variables** > **Actions**.
3. Créez deux secrets :
   - `DOCKER_USERNAME` : Votre nom d'utilisateur DockerHub
   - `DOCKER_PASSWORD` : Votre mot de passe DockerHub
  
   - Cliquez sur **Secrets and variables** puis sur **Actions**.
   - Ajoutez les secrets nécessaires, comme `DOCKER_USERNAME` et `DOCKER_PASSWORD`.


  1. **Ajouter tous les fichiers à l'index Git** :
   
   git add .

  2. **Effectuer un commit avec un message**
  
         git commit -m "Add CI/CD pipeline "

  3. **Ajouter le dépôt distant**

      git remote add origin https://github.com/Mouaz30/examen_devops.git

  4. **Pousser les changements vers la branche principale**   

     git push origin main
     


  
   
   


