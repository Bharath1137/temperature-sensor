#include <LiquidCrystal.h>

LiquidCrystal lcd(8, 9, 10, 11, 12, 13);
#define sensor A0

byte degree[8] = {
  0b00011,
  0b00011,
  0b00000,
  0b00000,
  0b00000,
  0b00000,
  0b00000,
  0b00000
};

void setup() {
  lcd.begin(16, 2);
  lcd.createChar(1, degree);
  lcd.setCursor(0, 0);
  lcd.print(" Digital ");
  lcd.setCursor(0, 1);
  lcd.print(" Thermometer ");
  delay(1000);
  lcd.clear();
}

void loop() {
  /*---------Temperature-------*/
  float voltage = analogRead(sensor) * 5.0 / 1023.0;  // Read voltage (0-5V)
  float temperature = voltage * 10;                   // Convert voltage to temperature in Celsius (assuming LM35 with 10mV/°C)
  
    /* --Remove decimal value-- */
  int temperatureInt = (int)temperature;              // Cast temperature to integer to remove decimal

  /*------Display Result------*/
  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Temperature");
  lcd.setCursor(4, 1);
  lcd.print(temperature, 1);  // Print with one decimal place
  lcd.write(1);
  lcd.print("C");
  delay(1000);
}
