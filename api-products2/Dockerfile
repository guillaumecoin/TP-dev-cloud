# Utiliser une image Node.js comme base
FROM node:18

# Installer sonar-scanner
RUN apt-get update && apt-get install -y unzip curl \
    && curl -o /opt/sonar-scanner.zip -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip \
    && unzip /opt/sonar-scanner.zip -d /opt \
    && ln -s /opt/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner \
    && rm /opt/sonar-scanner.zip

# Définir le PATH pour sonar-scanner
ENV PATH="/opt/sonar-scanner-4.6.2.2472-linux/bin:${PATH}"

# Créer un répertoire pour l'application
WORKDIR /usr/src/app

# Copier le fichier package.json et package-lock.json (si présent)
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le code source de l'application
COPY . .

# Construire l'application
RUN npm run build

# Exposer le port de l'application
EXPOSE 3000

# Démarrer l'application
CMD ["npm", "run", "start:prod"]
