# soil-fertiliser-level-monitoring-system
// Soil Fertilizer Monitoring System - Simulated NPK Sensor

const int nitrogenPin = A0;   // Analog pin for Nitrogen
const int phosphorusPin = A1; // Analog pin for Phosphorus
const int potassiumPin = A2;  // Analog pin for Potassium

void setup() {
  Serial.begin(9600);
  Serial.println(" Soil Fertilizer Monitoring System Started");
}

void loop() {
  int nitrogenValue = analogRead(nitrogenPin);     // Simulated analog input
  int phosphorusValue = analogRead(phosphorusPin);
  int potassiumValue = analogRead(potassiumPin);

  Serial.println(" Soil Nutrient Readings:");

  checkNutrient("Nitrogen", nitrogenValue);
  checkNutrient("Phosphorus", phosphorusValue);
  checkNutrient("Potassium", potassiumValue);

  Serial.println("-----------------------------------\n");
  delay(3000); // Read every 3 seconds
}

void checkNutrient(String nutrient, int value) {
  // Assume analogRead gives values from 0 to 1023
  // Map to 0 - 100 scale for simplicity
  int level = map(value, 0, 1023, 0, 100);

  Serial.print(nutrient + " Level: ");
  Serial.print(level);
  Serial.println("%");

  if (level < 30) {
    Serial.println( " + nutrient + " is LOW. Add appropriate fertilizer.");
  } else if (level >= 30 && level <= 70) {
    Serial.println( " + nutrient + " level is OPTIMAL.");
  } else {
    Serial.println( " + nutrient + " is HIGH. Avoid over-fertilizing.");
  }
}
