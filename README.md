### TEST-RESULTS - Sistemsko testiranje Java kalkulatora

#### 1. Opšti pregled koda
Kod sadrži metodu za evaluaciju i izračunavanje matematičkih izraza, podržavajući osnovne aritmetičke operacije: sabiranje, oduzimanje, množenje i deljenje. Osnovne funkcije su:
- `Run(String expression)`: Metoda koja prima matematički izraz kao string i vraća rezultat kao string.
- `evaluateExpression(String expression)`: Metoda koja obrađuje string izraz, razdvaja brojeve i operacije, i prosleđuje ih metodi `Calculate` za izračunavanje.
- `Calculate(List<Float> numbers, List<String> operations)`: Rekurzivna metoda koja obračunava finalni rezultat na osnovu lista brojeva i operacija.

#### 2. Detektovani nedostaci
- **Problem sa inicijalizacijom izraza**: Ako izraz počinje sa znakom plus (`+`) ili minus (`-`), program dodaje nulu na početak, ali ovo može dovesti do grešaka u interpretaciji izraza.
- **Parseovanje izraza**: Metoda koristi `Operations.ToString()` za kreiranje regexa koji se koristi za razdvajanje brojeva, što nije efikasno jer rezultira stringom `+*-`, što nije validan regex izraz. Potrebno je escape-ovati specijalne karaktere.
- **Rekurzivni poziv u `Calculate`**: Logika rekurzije može dovesti do stack overflow greške ako je izraz previše kompleksan zbog velikog broja operacija.
- **Greške u proračunavanju prioriteta operacija**: Postoji mogućnost da prioritet operacija nije uvek ispoštovan, naročito u kompleksnijim izrazima zbog načina na koji se operacije i brojevi uklanjaju iz lista.
- **Handleovanje beskonačnosti i grešaka**: Ako korisnik unese `Infinity` ili `-Infinity`, program to prihvata, ali nije jasno kako su ovi slučajevi testirani u praksi.
- **Obrada grešaka**: Program vraća `"ERROR"` za bilo koju grešku prilikom parsiranja brojeva, što može biti zbunjujuće jer ne specificira tip greške.

#### 3. Jedinični test za metodu `Calculate`

Za testiranje metode `Calculate`, mogli bismo napisati jednostavan test koji proverava osnovne funkcionalnosti:

```java
import static org.junit.Assert.*;
import org.junit.Test;
import java.util.Arrays;
import java.util.List;

public class CalculatorTest {
    @Test
    public void testCalculate() {
        // Scenario: 10 + 5 * 4 + 3
        List<Float> numbers = Arrays.asList(10f, 5f, 4f, 3f);
        List<String> operations = Arrays.asList("+", "*", "+");
        Calculator.Calculate(numbers, operations);
        float result = Calculator.finalResult;
        assertEquals(33.0, result, 0.001);  // Očekivani rezultat je 33
    }
}
```

#### 4. Zaključak
Ovaj test proverava osnovnu funkcionalnost metode `Calculate`, proveravajući da li pravilno izračunava kombinaciju operacija sa prioritizacijom množenja nad sabiranjem. Ovakav test može pomoći u otkrivanju grešaka u logici i osigurati da metoda pravilno funkcioniše pre njene upotrebe u produkciji.

---

