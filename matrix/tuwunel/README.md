## Running the Application

```shell
flyctl deploy
```

## Creating secrets

```shell
flyctl secrets set --app "nyefan-matrix" "TUWUNEL_REGISTRATION_TOKEN=$(dd </dev/random count=1 bs=95 2>/dev/null | base64 --wrap=0 | base64 --wrap=0)"
flyctl secrets set --app "nyefan-matrix" "TUWUNEL_TURN_SECRET=$(dd </dev/random count=1 bs=95 2>/dev/null | base64 --wrap=0 | base64 --wrap=0)"
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


