# COBOL---EMPLOYEE-PAYROLL

IDENTIFICATION DIVISION.

PROGRAM-ID. EMPLOYEE_PAYROLL.

AUTHOR. Group4_BSIT2-2.

DATA DIVISION.

WORKING-STORAGE SECTION.

01 EMP_NO PIC X(10).

01 EMP_NAME PIC X(25).

01 HRS_WORKED PIC 9(2)V99.

01 RATE_PER_HOUR PIC 9(3)V99.

01 SSS_PRM PIC 9(4)V99.

01 HDMF_PRM PIC 9(3)V99.

01 PHILHEALTH_PRM PIC 9(3)V99.

01 TAX PIC 9(4)V99.

01 BASIC_PAY PIC 9(7)V99.

01 DEDUCTIONS PIC 9(7)V99.

01 NET_PAY PIC S9(7)V99.

01 TOTDEDUCTION PIC 9(5)V99 VALUE ZERO.

01 TOTNETPAY PIC S9(7)V99 VALUE ZERO.

01 CHOICE PIC X.

01 ANOTHER_INPUT PIC X.

PROCEDURE DIVISION.

PERFORM UNTIL CHOICE = '2'

PERFORM DisplayMenu

ACCEPT CHOICE

IF CHOICE = '1' THEN

PERFORM GetEmployeeData

PERFORM CalculateBasicPay

PERFORM CalculateDeductions

PERFORM CalculateNetPay

PERFORM DisplayEmployeeInfo

PERFORM PromptForAnotherInput

ELSE IF CHOICE NOT EQUAL TO '2' THEN

DISPLAY "Invalid Choice. Please only 1 or 2"

ELSE

DISPLAY "Exiting program..."

END-IF

END-PERFORM

STOP RUN.

DisplayMenu.

DISPLAY "1. Enter employee data and Calculate net pay".

DISPLAY "2. Exit".

DISPLAY "Please choose between 1 or 2: ".

GetEmployeeData.

DISPLAY "Enter employee number: ".

ACCEPT EMP_NO.

DISPLAY "Enter employee name: ".

ACCEPT EMP_NAME.

DISPLAY "Enter hours worked: ".

ACCEPT HRS_WORKED.

IF FUNCTION NUMVAL(HRS_WORKED) = 0 THEN

DISPLAY "Invalid input. Please enter up to 99 hours only."

STOP RUN

END-IF.

DISPLAY "Enter Rate per hour: ".

ACCEPT RATE_PER_HOUR.

IF FUNCTION NUMVAL(RATE_PER_HOUR) = 0 THEN

DISPLAY "Invalid input. Please enter up to 3 digits only."

STOP RUN

END-IF.

DISPLAY "Enter SSS premium: ".

ACCEPT SSS_PRM.

IF FUNCTION NUMVAL(SSS_PRM) = 0 THEN

DISPLAY "Invalid input. Please enter up to 4 digits only."

STOP RUN

END-IF.

DISPLAY "Enter HDMF premium: ".

ACCEPT HDMF_PRM.

IF FUNCTION NUMVAL(HDMF_PRM) = 0 THEN

DISPLAY "Invalid input. Please enter up to 3 digits only."

STOP RUN

END-IF.

DISPLAY "Enter PHILHEALTH premium: ".

ACCEPT PHILHEALTH_PRM.

IF FUNCTION NUMVAL(PHILHEALTH_PRM) = 0 THEN

DISPLAY "Invalid input. Please enter up to 3 digits only."

STOP RUN

END-IF.

DISPLAY "Enter tax: ".

ACCEPT TAX.

IF FUNCTION NUMVAL(TAX) = 0 THEN

DISPLAY "Invalid input. Please enter up to 4 digits only."

STOP RUN

END-IF.

CalculateBasicPay.

COMPUTE BASIC_PAY = RATE_PER_HOUR * HRS_WORKED.

CalculateDeductions.

COMPUTE DEDUCTIONS = SSS_PRM + HDMF_PRM + PHILHEALTH_PRM +

TAX.

COMPUTE TOTDEDUCTION= TOTDEDUCTION + DEDUCTIONS.

CalculateNetPay.

COMPUTE NET_PAY = BASIC_PAY - DEDUCTIONS.

COMPUTE TOTNETPAY=TOTNETPAY + NET_PAY.

DisplayEmployeeInfo.

DISPLAY "---------------------------------------------------".

DISPLAY " BIG Company ".

DISPLAY " BGC, Taguig City ".

DISPLAY " PAYROLL ".

DISPLAY "---------------------------------------------------".

DISPLAY " ".

DISPLAY "Employee Information:".

DISPLAY "---------------------------------------------------".

DISPLAY "| Emp No. Emp Name Basic Pay ".

DISPLAY "| " EMP_NO " " EMP_NAME " "BASIC_PAY.

DISPLAY "---------------------------------------------------".

DISPLAY "| Deductions Net Pay ".

DISPLAY "| " DEDUCTIONS " " NET_PAY.

DISPLAY "---------------------------------------------------".

DISPLAY "TOTALS: ".

DISPLAY "| " TOTDEDUCTION " " TOTNETPAY.

PromptForAnotherInput.

DISPLAY " ".

DISPLAY "ANOTHER INPUT? (y/n): ".

ACCEPT ANOTHER_INPUT.

IF ANOTHER_INPUT = 'n' OR ANOTHER_INPUT = 'N' THEN

MOVE '2' TO CHOICE

ELSE

IF ANOTHER_INPUT <> 'y' AND ANOTHER_INPUT <> 'Y' THEN

DISPLAY "Invalid input. Please enter (y/n)."

PERFORM PromptForAnotherInput

END-IF

END-IF.
