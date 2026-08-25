# Building the Candid Fork Collector

## 1. Download OCB

```bash
curl --proto '=https' --tlsv1.2 -fL -o ocb \
  https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/cmd%2Fbuilder%2Fv0.159.0/ocb_0.159.0_darwin_arm64
chmod +x ocb
```

## 2. Build the binary

Cross-compile for the GKE node platform (linux/amd64). Uses the full contrib component list with the local githubreceiver fork substituted in via the `replaces` directive in `cmd/otelcontribcol/builder-config.yaml`.

```bash
GOOS=linux GOARCH=amd64 ./ocb --config cmd/otelcontribcol/builder-config.yaml
```

Output binary: `./cmd/otelcontribcol/otelcontribcol`

## 3. Build and push the Docker image

```bash
docker build --platform linux/amd64 \
  -t us-central1-docker.pkg.dev/candid-central/candid-images/otel-collector-contrib-candid-fork:<tag> \
  cmd/otelcontribcol/

docker push us-central1-docker.pkg.dev/candid-central/candid-images/otel-collector-contrib-candid-fork:<tag>
```
