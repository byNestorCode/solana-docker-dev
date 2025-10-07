# Dockerfile
FROM ubuntu:latest

# Instalar paquetes necesarios
RUN apt-get update && apt-get install -y \
    openssh-server \
    git \
    curl \
    build-essential \
    clang \
    pkg-config \
    libudev-dev \
    libssl-dev \
    llvm \
    libclang-dev \
    protobuf-compiler \
    curl \
    wget \
    && apt-get clean

# Variables de entorno necesarias
ENV NVM_DIR=/root/.nvm
ENV NODE_VERSION=lts/*

# Dependencias del sistema
RUN apt-get update && apt-get install -y curl ca-certificates build-essential && apt-get clean

# Instalar NVM, última LTS de Node, y Yarn
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash \
    && . "$NVM_DIR/nvm.sh" \
    && nvm install ${NODE_VERSION} \
    && nvm alias default ${NODE_VERSION} \
    && nvm use default \
    && npm install -g yarn

# Exportar PATH (para tiempo de ejecución)
ENV PATH="$NVM_DIR/versions/node/$(bash -c '. "$NVM_DIR/nvm.sh" && nvm version ${NODE_VERSION}' | sed 's/v//')/bin:$PATH"

# Eliminar el directorio de instalación de Rust antes de intentar instalarlo:
RUN rm -rf /root/.cargo /root/.rustup

# instalar Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --no-modify-path

# Agregar Rust al PATH en bash interactivo
RUN echo 'source /root/.cargo/env' >> /root/.bashrc

# Configurar el entorno
ENV PATH="/root/.cargo/bin:${PATH}"

# Verificar la instalación
RUN rustc --version && cargo --version

# Instalar Solana CLI
RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

# Configurar el entorno de Solana
ENV PATH="/root/.local/share/solana/install/active_release/bin:${PATH}"

# Instalar Anchor CLI
RUN cargo install --git https://github.com/coral-xyz/anchor avm --force

# Comprobar version del avm
RUN avm --version

# Instalar una versión específica de Anchor
RUN avm install latest && avm use latest && anchor --version

# Crear el directorio de configuración y el keypair solo si no existe
RUN mkdir -p /root/.config/solana && \
    if [ ! -f /root/.config/solana/id.json ]; then \
        echo "Generating keypair..."; \
        solana-keygen new --outfile /root/.config/solana/id.json; \
    fi || echo "Keypair already exists, skipping generation."


# Crear el directorio para el servicio SSH si no existe
RUN if [ ! -d /var/run/sshd ]; then mkdir /var/run/sshd; fi

# Configurar la contraseña del usuario root
ARG ROOT_PASSWORD
RUN echo "root:${ROOT_PASSWORD}" | chpasswd

# Permitir el acceso SSH
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Exponer el puerto SSH
EXPOSE 22

# Iniciar el servicio SSH
CMD ["/usr/sbin/sshd", "-D"]
