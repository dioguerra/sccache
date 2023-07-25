FROM ubuntu AS downloader

RUN apt-get update && apt-get install -y wget
RUN wget https://github.com/mozilla/sccache/releases/download/v0.5.4/sccache-dist-v0.5.4-x86_64-unknown-linux-musl.tar.gz
RUN tar -xvf sccache-dist-v0.5.4-x86_64-unknown-linux-musl.tar.gz

# FROM gcr.io/distroless/static-debian11:nonroot
FROM ubuntu
RUN apt-get update && apt-get install -y bubblewrap && rm -rf /var/lib/apt/lists/*

COPY --from=downloader sccache-dist-v0.5.4-x86_64-unknown-linux-musl/sccache-dist /

ENV SCCACHE_NO_DAEMON=1
ENV SCCACHE_LOG=info

ENTRYPOINT ["/sccache-dist"]