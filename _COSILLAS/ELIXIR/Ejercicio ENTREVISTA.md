Escribe una modulo llamado WordFrequency, que posee la funcion count, que tome una cadena de texto como entrada.
Esta función debe devolver un mapa donde las claves sean las palabras únicas en el texto (sin distinguir mayúsculas de minúsculas) y los valores sean el número de veces que aparece cada palabra.

 * Las palabras deben estar separadas por espacios.
 * La puntuación debe ser ignorada
 * El conteo no debe distinguir entre mayúsculas y minúsculas (por ejemplo, "Elixir" y "elixir" cuentan como la misma palabra).
 * Se debe intentar no usar Enum/frequencies
 * Realizar unit tests / tdd

```
    assert WordFrequency.count("Hello Elixir, hello world!") == 
      %{"hello" => 2, "elixir" => 1, "world" => 1}

    assert WordFrequency.count("This is a Test. This is only a test.") ==
    %{"this" => 2, "is" => 2, "a" => 2, "test" => 2, "only" => 1}
```

https://gist.github.com/marianogabriels/f3086e6a215c0812e5801a40a987cd7a 
