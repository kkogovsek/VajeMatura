void ports () {
     TRISB = 0x01;
}

void int_enable() {
     INTCON.GIE = 1;
     INTCON.T0IE = 1;
}

void interrupt() {
     PORTB = 0x50;
     INTCON.TMR0IF = 0;
}

void main() {
     int count = 0;
     ports();
     int_enable();
     while(1) {
              if(PORTB & 0x01)
                       count++;
              if(count == 3) {
                       count = 0;
                       INTCON.TMR0IF = 1;
              }
              Delay_ms(150);
              PORTB = 0;
     }
}