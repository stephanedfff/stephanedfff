```cpp
#include <Adafruit_ILI9341.h>
#include <Adafruit_GFX.h>

#define TFT_CS     10
#define TFT_RST    9
#define TFT_DC     8

Adafruit_ILI9341 tft = Adafruit_ILI9341(TFT_CS, TFT_DC, TFT_RST);

int capteur1 = A0;
int capteur2 = A1;
int capteur3 = A2;

void setup() {
  Serial.begin(9600);
  tft.begin();

  tft.setRotation(3); // Rotation de l'écran TFT
}

void loop() {
  int valeurCapteur1 = analogRead(capteur1);
  int valeurCapteur2 = analogRead(capteur2);
  int valeurCapteur3 = analogRead(capteur3);

  float pourcentageCapteur1 = map(valeurCapteur1, 0, 1023, 0, 120); // Mapping de la valeur du capteur 1 en degrés
  float pourcentageCapteur2 = map(valeurCapteur2, 0, 1023, 0, 120); // Mapping de la valeur du capteur 2 en degrés
  float pourcentageCapteur3 = map(valeurCapteur3, 0, 1023, 0, 120); // Mapping de la valeur du capteur 3 en degrés

  pourcentageCapteur1 = map(pourcentageCapteur1, 0, 120, 0, 100); // Conversion en pourcentage
  pourcentageCapteur2 = map(pourcentageCapteur2, 0, 120, 0, 100);
  pourcentageCapteur3 = map(pourcentageCapteur3, 0, 120, 0, 100);

  tft.fillScreen(ILI9341_BLACK); // Effacer l'écran avec une couleur de fond

  tft.setCursor(10, 30);
  tft.setTextColor(ILI9341_WHITE); //
Couleur du texte en blanc
  tft.setTextSize(2); // Taille de police
  tft.print("Avance rabatteurs: ");
  tft.print(pourcentageCapteur1);
  tft.print("%");

  tft.setCursor(10, 70);
  tft.print("hauteur rabatteurs: ");
  tft.print(pourcentageCapteur2);
  tft.print("%");

  tft.setCursor(10, 110);
  tft.print("inclinaison horizontale coupe: ");
  tft.print(pourcentageCapteur3);
  tft.print("%");

  delay(1000); // Délai d'une seconde entre chaque lecture des capteurs
}
```
