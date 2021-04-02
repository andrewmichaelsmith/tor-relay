 ### Environment variables

| Name                         | Description                                                                  | Default value |
| ---------------------------- |:----------------------------------------------------------------------------:| -------------:|
| **RELAY_TYPE**               | The type of relay (bridge, middle or exit)                                   | middle        |
| **RELAY_NICKNAME**           | The nickname of your relay                                                   | hacktheplanet |
| **CONTACT_GPG_FINGERPRINT**  | Your GPG ID or fingerprint                                                   | none          |
| **CONTACT_NAME**             | Your name                                                                    | none          |
| **CONTACT_EMAIL**            | Your contact email                                                           | none          |
| **RELAY_BANDWIDTH_RATE**     | Limit how much traffic will be allowed through your relay (must be > 20KB/s) | 100 KBytes    |
| **RELAY_BANDWIDTH_BURST**    | Allow temporary bursts up to a certain amount                                | 200 KBytes    |
| **RELAY_PORT**               | Default port used for incoming Tor connections (ORPort)                      | 9001          |

## Generate keys

Maybe you want  to generate them so that you can inject them in another way.

```
docker build -t x .
mkdir certs
sudo chown 100:100 certs/
docker run -v `pwd`/certs:/var/lib/tor/.tor/ x
```

# Kubernetes secret from keys

```
cd certs
kubectl create secret -o yaml generic tor-keys \
   --from-file=./secret_id_key \
   --from-file=./ed25519_signing_secret_key \
   --from-file=./ed25519_signing_cert \
   --from-file=./ed25519_master_id_secret_key \
   --from-file=./ed25519_master_id_public_key \
   --from-file=./secret_onion_key_ntor \
   --from-file=./secret_onion_key > tor-keys.yaml
```
