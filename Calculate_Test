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
