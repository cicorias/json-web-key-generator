# json-web-key-generator [![Docker Pulls](https://img.shields.io/docker/pulls/cicorias/json-web-key-generator)](https://hub.docker.com/r/cicorias/json-web-key-generator)
A command-line Java-based generator for JSON Web Keys (JWK) and JSON Private/Shared Keys (JPSKs).


# Example runs of this container:

```
# generate RSA keys and wrtie to existing JSON file of keys (keysets)
docker run -it --rm -v ${PWD}:/keys cicorias/json-web-key-generator -t RSA -s 2048 -u sig -o /keys/jwks.json -S

# generate and display to console the result - in "keys"  format.
docker run -it --rm -v ${PWD}:/keys cicorias/json-web-key-generator -t RSA -s 2048 -u sig  -S -p

# same but just emit the json object for full private/public and public on its own.
docker run -it --rm -v ${PWD}:/keys cicorias/json-web-key-generator -t RSA -s 2048 -u sig  -p


```

## Getting Started

To compile, run `mvn package`.
This will generate a `json-web-key-generator.jar` in the `target` directory.

To generate a key, run `java -jar json-web-key-generator.jar -t <keytype>`.
Several other arguments are defined which may be required depending on your key type:

```
 -a <arg>   Algorithm (optional)
 -c <arg>   Key Curve, required for EC key type. Must be one of P-256,
            P-384, P-521
 -i <arg>   Key ID (optional), one will be generated if not defined
 -I         Don't generate a Key ID if none defined
 -o <arg>   Write output to file (will append to existing KeySet if -S is
            used), No Display of Key Material
 -p         Display public key separately
 -s <arg>   Key Size in bits, required for RSA and oct key types. Must be
            an integer divisible by 8
 -S         Wrap the generated key in a KeySet
 -t <arg>   Key Type, one of: RSA, oct, EC
 -u <arg>   Usage, one of: enc, sig (optional)
```

## Use Docker
When using the docker image and write to a file you must mount that file in the docker container.
