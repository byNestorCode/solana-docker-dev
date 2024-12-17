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
    curl \
    wget \
    && apt-get clean

# Instalar Node.js 20.17.0
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs && \
    apt-get clean

# Instalar yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" >> /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y yarn && \
    apt-get clean

# Eliminar el directorio de instalación de Rust antes de intentar instalarlo:
RUN rm -rf /root/.cargo /root/.rustup

# instalar Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --no-modify-path

# Configurar el entorno
ENV PATH="/root/.cargo/bin:${PATH}"

# Verificar la instalación
RUN rustc --version && cargo --version

# Instalar Solana CLI
RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

# Configurar el entorno de Solana
ENV PATH="/root/.local/share/solana/install/active_release/bin:${PATH}"

# Instalar Anchor CLI
RUN cargo install --git https://github.com/project-serum/anchor anchor-cli --locked

# Verificar las instalaciones
RUN rustc --version && solana --version && anchor --version && node --version && npm --version

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
