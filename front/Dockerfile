FROM node:20-alpine

WORKDIR /app

# Installer Angular CLI globalement
RUN npm install -g @angular/cli@latest

# Copier package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier tout le code source
COPY . .

# Exposer le port 4200
EXPOSE 4200

# Démarrer le serveur de développement
CMD ["ng", "serve", "--host", "0.0.0.0", "--port", "4200"]
