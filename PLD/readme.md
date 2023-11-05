#### PLD equations
```
Name     FDD35;
Date     2015-12-19;
Revision 01;
Device   g22v10;

/* *************** INPUT PINS *********************/
PIN 1   = !RFSH   ; /* REFRESH */ 
PIN 2   = !IORQ   ; /* IORQ */
PIN 3   = !MREQ   ; /* MREQ */ 
PIN 4   = !RD     ; /* RD */ 
PIN 5   = !WR     ; /* WR */ 
PIN 6   = A5      ; /* A5 */
PIN 7   = A6      ; /* A6 */ 
PIN 8   = A7      ; /* A7 */ 
PIN 9   = A13     ; /* A13 */ 
PIN 10  = A14     ; /* A14 */ 
PIN 11  = A15     ; /* A15 */ 
PIN 13  = !BOOT   ; /* BOOT */ 

/* *************** OUTPUT PINS *********************/
PIN 14  = !COUT   ; /* enable COM_OUT */ 
PIN 15  = !CIN    ; /* enable COM_IN */ 
PIN 16  = !RS1    ; /* enable WD2123 CH1 */ 
PIN 17  = !RS2    ; /* enable WD2123 CH2 */ 
PIN 18  = !RS3    ; /* enable WD2123 CTRL */ 
PIN 19  = !ROMCS  ; /* enable ROM */ 
PIN 20  = !RAMCS0 ; /* enable RAM0 */ 
PIN 21  = !RAMCS1 ; /* enable RAM1 */ 
PIN 22  = PE0     ; /* enable U4 LS273 */ 
PIN 23  = !FDC    ; /* enable WD1772 */

/* *** RS3 *** */
RS3     = IORQ & WR & !A7 & !A6 & !A5; /* ok */

/* *** COUT *** */
COUT    = IORQ & WR & !A7 & !A6 & A5;

/* *** CIN *** */
CIN     = IORQ & RD & !A7 & !A6 & A5;

/* *** RS2 *** */
RS2     = IORQ & (RD # WR) & !A7 & A6;

/* *** RS1 *** */
RS1     = IORQ & (RD # WR) & A7 & !A6;

/* *** FDC *** */
FDC     = IORQ & (RD # WR) & A7 & A6 & !A5;

/* *** PE0 *** */
PE0     = IORQ & WR & A7 & A6 & A5;

FMREQ   = MREQ & !RFSH;
/* *** ROMCS *** */
ROMCS   = FMREQ & BOOT & RD & !A15 & !A14 & !A13;

/* *** RAMCS0 *** */
RAMCS0  = FMREQ & (((!BOOT # A14 # A13) & RD) # WR) & !A15;

/* *** RAMCS1 *** */
RAMCS1  = FMREQ & (RD # WR) & A15;

/* end */
```
