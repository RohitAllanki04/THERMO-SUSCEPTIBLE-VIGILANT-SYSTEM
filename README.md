# THERMO-SUSCEPTIBLE-VIGILANT-SYSTEM
#This system employs sensors as vigilant detectives, continuously monitoring temperature. Information is relayed to a smart computer using algorithms. It dynamically signals temperature status through lights by three different colors. Ideal for places like hospitals and large fridges, preventing issues by promptly alerting temperature fluctuations.
import java.util.concurrent.TimeUnit;
//system not sensor than output will be Temperature: 0.0?°C continuously..
public class TemperatureMonitor {

    private static final int LM35_PIN = 0; // Replace with the actual GPIO pin connected to LM35
    private static final int RED_PIN = 1;  // Replace with the actual GPIO pin for red LED
    private static final int GREEN_PIN = 2; // Replace with the actual GPIO pin for green LED
    private static final int ORANGE_PIN = 3; // Replace with the actual GPIO pin for orange LED

    private float lm_value;
    private float tempc;

    public void setup() {
        System.out.println("Temperature Monitor Started");
        // Simulate pinMode settings for LEDs
        // (Assuming you have a library or mechanism to control GPIO pins in Java)
        setPinMode(RED_PIN, "OUTPUT");
        setPinMode(GREEN_PIN, "OUTPUT");
        setPinMode(ORANGE_PIN, "OUTPUT");
    }

    public void loop() {
        // Simulate analogRead for LM35 sensor
        // (Assuming you have a library or mechanism to read analog values in Java)
        lm_value = analogRead(LM35_PIN);
        tempc = (lm_value * 500) / 1023;
        System.out.println("Temperature: " + tempc + "°C");

        // Control LEDs based on temperature
        if (tempc > 50) {
            digitalWrite(RED_PIN, true);
            digitalWrite(GREEN_PIN, false);
            digitalWrite(ORANGE_PIN, false);
        } else if (tempc < 40) {
            digitalWrite(RED_PIN, false);
            digitalWrite(GREEN_PIN, false);
            digitalWrite(ORANGE_PIN, true);
        } else {
            digitalWrite(GREEN_PIN, true);
            digitalWrite(RED_PIN, false);
            digitalWrite(ORANGE_PIN, false);
        }

        try {
            TimeUnit.SECONDS.sleep(1); // Delay for 1 second
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    // Placeholder methods for GPIO pin control (replace with actual implementations)
    private void setPinMode(int pin, String mode) {
        // Implement pin mode setting logic here
    }

    private float analogRead(int pin) {
        // Implement analog read logic here
        return 0.0f; // Replace with actual sensor reading
    }

    private void digitalWrite(int pin, boolean value) {
        // Implement digital write logic here
    }

    public static void main(String[] args) {
        TemperatureMonitor monitor = new TemperatureMonitor();
        monitor.setup();
        while (true) {
            monitor.loop();
        }
    }
}

