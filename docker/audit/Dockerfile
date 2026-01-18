FROM rust:1.83-bookworm
ENV DEBIAN_FRONTEND=noninteractive

# Install OS deps needed for building some crates
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        curl \
        libssl-dev \
        pkg-config && \
    rm -rf /var/lib/apt/lists/*

ARG CARGO_AUDIT_VERSION=0.20.0
RUN cargo install cargo-audit cargo-deny

# Install cargo tools (compiled into the image so subsequent runs are fast)
RUN /usr/local/cargo/bin/cargo install \
        cargo-audit --version="${CARGO_AUDIT_VERSION}" --locked && \
    /usr/local/cargo/bin/cargo install \
        cargo-deny --version="${CARGO_DENY_VERSION}" --locked

WORKDIR /workspace

CMD ["bash"]
