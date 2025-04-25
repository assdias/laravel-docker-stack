FROM node:22

# Definir o diretório de trabalho como `/var/www` (onde você vai ter os projetos)
WORKDIR /var/www

# Instalar dependências do sistema, se necessário
RUN apt-get update && apt-get install -y \
  bash \
  curl \
  && rm -rf /var/lib/apt/lists/*

# Definir o comando para o projeto Laravel, no caso, "npm install" e "npm run dev"
# Isso irá mudar conforme o projeto
CMD ["bash"]
