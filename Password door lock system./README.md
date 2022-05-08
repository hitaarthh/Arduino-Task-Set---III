<div>
<a href="https://www.arduino.cc/"><img src="https://img.shields.io/badge/MicroController%3A-Arduino%20UNO%203-green[700]"height="25" align="left"></a>
<a href="https://www.tinkercad.com/things/077OPp6fBwy-password-door-lock-system-using-4x4-keypad/editel"><img src="https://img.shields.io/badge/Simulation:-Click%20to%20Simulate -blue" height="25"></a>
<a href="https://www.microchip.com/en-us/product/ATmega328P"><img src="https://img.shields.io/badge/Processor%3A-Atmega328P-black" height="25" align="right"></a>
</div>

<div align="center">
   <h1>Password Door Lock System</h1>
</div>

### ---> Introduction:
- A security system now is not only a facility but a necessity. It helps us store data securely and according to our requirements. There are many methods of security and usually, for digital devices, it starts with a password. 

- This circuit is deigned in such a way that it displays a meaningful message on the LCD Screen.

### --> Device Used:
- Keypad (4x4)
- Servo Motor
- LCD Screen(16 x 2)
- Arduino UNO 3
- Breadboard
- Connecting Wires

<a href="https://www.tinkercad.com/things/077OPp6fBwy-password-door-lock-system-using-4x4-keypad/editel"><img src="https://img.shields.io/badge/Simulation:-Click%20to%20Simulate -blue" height="25" ></a>

```c++
#include <Keypad.h>        // header files to interface keypad along with arduino.
#include <LiquidCrystal.h> // header files to interface LCD display along with arduino.
#include <Servo.h>         // header files to interface the servo motor along with the arduino.

#define Password_Length 5  // initialising a variable Password_length and giving it a constant value of 5.

Servo myservo;
LiquidCrystal lcd(A0, A1, A2, A3, A4, A5);

int pos = 0;

char Data[Password_Length]; // initialising a one-dimensional character array of length of the password.
char Master[Password_Length] = "1234"; // Storing the defauly password 1234.
byte data_count = 0, master_count = 0;

bool Pass_is_good; // variable to store the decision whether the password accepted is correct or not
bool door = false; // intialising the door condition, by default its closed.
char customKey;

/*---Initialising Keypad---*/
const byte ROWS = 4; //initialising the rows of our keypad.
const byte COLS = 4; //initialising the rows of our keypad.
char keys[ROWS][COLS] = { 
    {'1', '2', '3', 'A'},  // Initalising the numbers/characters present on the keypad.
    {'4', '5', '6', 'B'},
    {'7', '8', '9', 'C'},
    {'*', '0', '#', 'D'}};

byte rowPins[ROWS] = {0, 1, 2, 3};
byte colPins[COLS] = {4, 5, 6, 7};

Keypad customKeypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

/*--- Setting Up the Arduino ---*/
void setup()
{
    myservo.attach(9, 2000, 2400); // initialising the servo motor.
    ServoClose();                  // keeping servo motor in close state.
    lcd.begin(16, 2);              // initialising the LCD screen which has 16*2 pixels
    lcd.print("Welcome Home. ");   // meaningful message being printed on the screen
    loading("I'm Jarvis.");        // loading() function is being called which basically displays a message while system is rloading/re-loading
    lcd.clear();
}

void loop()
{
    if (door == true)
    {
        customKey = customKeypad.getKey();     // initialising the keypad to take inputs
        if (customKey == '#')
        {
            lcd.clear();
            ServoClose();
            lcd.print("Door is being closed"); // printing meaningful message 
            delay(3000);
            door = false;
        }
    }
    else
        Open();
}

// This function is intended to display a meaningful message while providing some delay to the system so that all the changes are clearly visible.
void loading(char msg[]) 
{
    lcd.setCursor(0, 1);
    lcd.print(msg);

    for (int i = 0; i < 9; i++)
    {
        delay(1000);
        lcd.print(".");
    }
}

// This function is intended to clear the entered password in order to close the door and reset the system.
void clearData()
{
    while (data_count != 0)
    {
        Data[data_count--] = 0;
    }
    return;
}

// This function is inteneded to close the servo motor slowly, which is a symbolic representation of a door closing.
void ServoClose()
{
    for (pos = 90; pos >= 0; pos -= 10)
    {
        myservo.write(pos);
    }
}

// This function is inteneded to open the servo motor slowly, which is a symbolic representation of a door closing.
void ServoOpen()
{
    for (pos = 0; pos <= 90; pos += 10)
    {
        myservo.write(pos);
    }
}

// This function is the main working of the whole system which intends to take the pass from user and check whether it is right or wrong.
void Open()
{
    lcd.setCursor(0, 0);
    lcd.print("Enter Password");

    customKey = customKeypad.getKey(); // Initialising the keypad to take input.
    if (customKey)
    {
        Data[data_count] = customKey; // storing the entered pass-key.
        lcd.setCursor(data_count, 1); // initialising LCD to print the pass-key entered from pixel 1,
        lcd.print(Data[data_count]);  // printing the pass-key in real time as it is entered by the user.
        data_count++;
    }

    if (data_count == Password_Length - 1) // this would check the pass-keu if the entered pass length is same to that of the default-pass.
    {
        if (!strcmp(Data, Master)) //this built function basically checks the each character of default and entered password, and returns either 0 or 1.
        {
            lcd.clear();
            ServoOpen();
            lcd.print(" Door is Open ");
            door = true;
            loading("You may go in");
            lcd.clear();
            lcd.print(" Time is up! ");
            delay(1000);
            ServoClose();
            door = false;
        }
        else
        {
            lcd.clear();
            lcd.print(" Wrong Password!! ");
            loading("Re-enter pass.");
            door = false;
        }
        delay(500);
        lcd.clear();
        clearData();
    }
} 
```




