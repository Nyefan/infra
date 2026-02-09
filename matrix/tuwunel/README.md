## Running the Application

```shell
flyctl deploy
```

## Creating secrets

```shell
flyctl secrets set --app "nyefan-matrix" "TUWUNEL_REGISTRATION_TOKEN=$(dd </dev/random count=1 bs=95 2>/dev/null | base64 --wrap=0 | tee .tuwunel_registration_secret | base64 --wrap=0)"
flyctl secrets set --app "nyefan-matrix" "TUWUNEL_TURN_SECRET=$(dd </dev/random count=1 bs=95 2>/dev/null | base64 --wrap=0 | tee .tuwunel_turn_secret | base64 --wrap=0)"
```

## Creating certificates
```shell
flyctl certs add "matrix.nyefan.org" --app "nyefan-matrix"
flyctl certs add "www.matrix.nyefan.org" --app "nyefan-matrix"
```
 Then create CNAME records
 
| subdomain   | type  | record                |
|-------------|-------|-----------------------|
| matrix.     | CNAME | nyefan-matrix.fly.dev |
| www.matrix. | CNAME | nyefan-matrix.fly.dev |


## Locally testing startup
```shell
docker run -v db:/var/lib/tuwunel/ \
  -e TUWUNEL_CONFIG=/etc/tuwunel/tuwunel.toml \
  --mount type=bind,source=$(pwd)/tuwunel.toml,target=/etc/tuwunel/tuwunel.toml \
  --mount type=bind,source=$(pwd)/.tuwunel_registration_secret_fake,target=/etc/tuwunel/.reg_token \
  --mount type=bind,source=$(pwd)/.tuwunel_turn_secret_fake,target=/etc/tuwunel/.turn_secret \
  ghcr.io/matrix-construct/tuwunel:v1.5.0
```