# scrypt
Herramienta sencilla para conversión a hash y verificación de contraseñas con el algoritmo **scrypt**.

## Uso

``` go
package dummy

import(
		"fmt"
		"log"
		xcrypto "github.com/ilgaleanos/scrypt"
)

func dummy( ) {
	 // e.g. r.PostFormValue("password")
	 passwordFromForm := "Alguna contraseña en modo texto"

	 // Generates a derived key of the form "N$r$p$salt$dk" where N, r and p are defined as per
	 // scrypt.Defaults (N=16384, r=8, p=1) makes it easy to provide these parameters, and
	 // (should you wish) provide your own values via the scrypt.Params type.
	 hash, err := xcrypto.GenerateFromPassword([]byte(passwordFromForm), xcrypto.DefaultParams)
	 if err != nil {
		 log.Fatal(err)
	 }

	 // Print the derived key with its parameters prepended.
	 fmt.Printf("%s\n", hash)

	 // Uses the parameters from the existing derived key. Return an error if they don't match.
	 err = xcrypto.CompareHashAndPassword(hash, []byte(passwordFromForm))
	 if err != nil {
		 log.Fatal(err)
	 }
}
```
