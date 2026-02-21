# MPU6050 Arduino Tutorial

This project demonstrates how to use the MPU6050 6-axis motion sensor with Arduino.

## 🧠 Features
- Reads Accelerometer (X, Y, Z)
- Reads Gyroscope (X, Y, Z)
- Uses I2C Communication
- Displays data in Serial Monitor

## 🔌 Wiring

MPU6050 → Arduino Uno
VCC → 5V
GND → GND
SDA → A4
SCL → A5

## 📚 Used In
- Drones
- Self-balancing robots
- Motion tracking systems
 
Created by Code and Circuits 🚀

the code for the mpu6050  👇👇



#include <Wire.h>

const int MPU_addr = 0x68;  // I2C address of MPU6050

int16_t AcX, AcY, AcZ, GyX, GyY, GyZ;

void setup() {
  Wire.begin();
  Wire.beginTransmission(MPU_addr);
  Wire.write(0x6B);  // Power management register
  Wire.write(0);     // Wake up MPU6050
  Wire.endTransmission(true);

  Serial.begin(9600);
}

void loop() {
  Wire.beginTransmission(MPU_addr);
  Wire.write(0x3B);  // Starting register for accel data
  Wire.endTransmission(false);
  Wire.requestFrom(MPU_addr, 14, true);

  AcX = Wire.read() << 8 | Wire.read();
  AcY = Wire.read() << 8 | Wire.read();
  AcZ = Wire.read() << 8 | Wire.read();
  Wire.read(); Wire.read(); // Skip temperature
  GyX = Wire.read() << 8 | Wire.read();
  GyY = Wire.read() << 8 | Wire.read();
  GyZ = Wire.read() << 8 | Wire.read();

  Serial.print("Accel: ");
  Serial.print(AcX); Serial.print(" ");
  Serial.print(AcY); Serial.print(" ");
  Serial.print(AcZ);

  Serial.print(" | Gyro: ");
  Serial.print(GyX); Serial.print(" ");
  Serial.print(GyY); Serial.print(" ");
  Serial.println(GyZ);

  delay(500);
}
