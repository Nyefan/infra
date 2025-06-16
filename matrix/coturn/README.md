## Running the Application

```shell
flyctl deploy
```

## Creating secrets

copy TURN_SECRET into `coturn.conf`
```shell
flyctl secrets set --app "nyefan-coturn" "TUWUNEL_TURN_SECRET=${TUWUNEL_TURN_SECRET}"
```

## Creating certificates
```shell
flyctl certs add "turn.nyefan.org" --app "nyefan-coturn"
flyctl certs add "www.turn.nyefan.org" --app "nyefan-coturn"
```
 Then create CNAME records
 
| subdomain   | type  | record                |
|-------------|-------|-----------------------|
| turn.       | CNAME | nyefan-coturn.fly.dev |
| www.turn.   | CNAME | nyefan-coturn.fly.dev |


