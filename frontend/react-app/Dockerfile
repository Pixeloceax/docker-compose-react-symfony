# Utilisez une image de base contenant Node.js et npm
FROM node:21
# Définissez le répertoire de travail dans le conteneur
WORKDIR /app

# Copiez le package.json et le package-lock.json dans le conteneur
COPY package*.json ./

# Installez les dépendances
RUN npm install

# Copiez le reste des fichiers de l'application dans le conteneur
COPY . .


# Exposez le port sur lequel l'application écoute
EXPOSE 3000

# Démarrez l'application React
CMD ["npm", "start"]