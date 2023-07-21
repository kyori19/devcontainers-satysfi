# make args available in FROM directive
ARG VARIANT="latest"

FROM rust:latest AS build-lsp

ARG LSP_VERSION="master"
RUN <<EOF
curl -fsSL https://github.com/monaqa/satysfi-language-server/archive/${LSP_VERSION}.tar.gz | tar xzvf -
mv satysfi-language-server-${LSP_VERSION} satysfi-language-server
cd satysfi-language-server
cargo build --release
EOF

FROM kyori/satysfi:${VARIANT}

COPY --from=build-lsp /satysfi-language-server/target/release/satysfi-language-server /usr/local/bin/satysfi-language-server
