# Lab 7: VALENTIN CRISTEA

Link to this file in your GitHub repository:

https://github.com/CristeaValentin/Digital-electronics-2

### Analog-to-Digital Conversion

1. Complete table with voltage divider, calculated, and measured ADC values for all five push buttons.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   | 0 |
   | Up     | 0.495&nbsp;V | 101 | 99 |
   | Down   |   1.2025 V    |   246  | 244 |
   | Left   |    1.969 V   |   403  | 409 |
   | Select |    3.181 V  |   650  | 641 |
   | none   |    5V   |   1023  | 1023 |

2. Code listing of ACD interrupt service routine for sending data to the LCD/UART and identification of the pressed button. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: ADC complete interrupt
 * Purpose:  Display value on LCD and send it to UART.
 **********************************************************************/
ISR(ADC_vect) { 
        // WRITE YOUR CODE HERE
        uint16_t value = 0;
        char lcd_string[4] = "0000";
        // Clear the value on the LCD
 
        lcd_gotoxy(8, 0);
        lcd_puts("    ");
        value = ADC;
 
        // Display the value on the LCD
        itoa(value, lcd_string, 10);
        lcd_gotoxy(8, 0);
        lcd_puts(lcd_string);
        // Display the value in the UART
 
        uart_puts(lcd_string);
        uart_puts(" ");
 
        //Display value in HEXA on the LCD
 
        itoa(value, lcd_string, 16);
        lcd_gotoxy(13, 0);
        lcd_puts(lcd_string);
 
        lcd_gotoxy(8, 1);
        // we clear the "c" spot of the display 
        lcd_puts("        ");
 
        //The following sequence will display which button was pressed on both LCD and the UART
 
        lcd_gotoxy(8, 1);
        if (value == 1023) {
                lcd_puts("none");
                uart_puts("none")
        } else if (value == 99) {
                lcd_puts("up");
                uart_puts("up");
        } else if (value == 0) {
                lcd_puts("right");
                uart_puts("right");
        } else if (value == 257) {
                lcd_puts("down");
                uart_puts("down");
        } else if (value == 410) {
                lcd_puts("left");
                uart_puts("left");
        } else if (value == 640) {
                lcd_puts("select");
                uart_puts("select");
        }
 
}
```

### UART communication

1. (Hand-drawn) picture of UART signal when transmitting three character data `De2` in 4800 7O2 mode (7 data bits, odd parity, 2 stop bits, 4800&nbsp;Bd).

   ![your figure](lab7fig1.jpg)

2. Flowchart figure for function `uint8_t get_parity(uint8_t data, uint8_t type)` which calculates a parity bit of input 8-bit `data` according to parameter `type`. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure]()

### Temperature meter

Consider an application for temperature measurement and display. Use temperature sensor [TC1046](http://ww1.microchip.com/downloads/en/DeviceDoc/21496C.pdf), LCD, one LED and a push button. After pressing the button, the temperature is measured, its value is displayed on the LCD and data is sent to the UART. When the temperature is too high, the LED will start blinking.

1. Scheme of temperature meter. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure](lab7fig3.jpg)
