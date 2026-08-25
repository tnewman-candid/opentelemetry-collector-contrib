# Building the Candid Fork Collector

## 1. Download OCB

```bash
curl --proto '=https' --tlsv1.2 -fL -o ocb \
  https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/cmd%2Fbuilder%2Fv0.159.0/ocb_0.159.0_darwin_arm64
chmod +x ocb
```

## 2. Build the binary

```bash
./ocb --config otelcolbuilder.yml
```

Output binary: `./dist/otelcol-contrib-candid`

## 3. Build and push the Docker image

```bash
docker build -f Dockerfile.candid -t us-central1-docker.pkg.dev/candid-central/candid-images/otel-collector-contrib-candid-fork:0.1 .
docker push us-central1-docker.pkg.dev/candid-central/candid-images/otel-collector-contrib-candid-fork:0.1
```
