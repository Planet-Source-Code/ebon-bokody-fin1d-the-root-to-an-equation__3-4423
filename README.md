<div align="center">

## Fin1d the root to an Equation


</div>

### Description

This code was an assignment of mine from university. There is actually no user input but you can change the code to solve any equation. You could also easily modify it so user input is used. This code is very stable and should work on all platforms. It is good Numerical Analysis code.
 
### More Info
 
Solves two mathematical equation using four different methods.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Ebon Bokody](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/ebon-bokody.md)
**Level**          |Beginner
**User Rating**    |3.7 (11 globes from 3 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Math](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/math__3-12.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/ebon-bokody-fin1d-the-root-to-an-equation__3-4423/archive/master.zip)





### Source Code

```
/*
root.cpp
Author: Ebon Bokody
Description: Numerical Analysis Assignment 1 -
Finds the positive root of the following equations to precision of at least
0.000001, using the bisection method, modified false position method, secant
method and newton's method. + Compare & comment on results & execution times
*/
#include <iostream.h>
#include <conio.h>
#include <math.h>
#include <time.h>
#include <sys/timeb.h>
// fn definitions
void bisection(int fn) ;
void mfp(int fn) ;
void secant(int fn) ;
void newton(int fn) ;
double f1(double) ;        // evaluates function1
double f1_derivative(double) ;
double f2(double) ;
double f2_derivative(double) ;
void DispProb(int fn) ;
void main()
{
 clrscr();
 cout << "\n J2788 NUMERICAL ANALYSIS - ASSIGNMENT 1 - FINDING ROOTS"
		 << "\n _______________________________________________________\n\n"
		 << "Welcome to the finding roots program:\n\n\tProgrammer: Ebon Bokody"
		 << "\n\tStudent ID: 13225966\n\n\nPress any key to begin!" ;
 getch(); clrscr();
 bisection(0) ; getch();
 bisection(1) ;
 cout << "\n\n\nPress any key to continue to modified false position method..." ;
 getch(); clrscr();
 mfp(0) ; getch();
 mfp(1) ;
 cout << "\n\n\nPress any key to continue to secant method..." ;
 getch(); clrscr();
 secant(0) ; getch();
 secant(1) ;
 cout << "\n\n\nPress any key to continue to newtons method..." ;
 getch(); clrscr();
 newton(0) ; getch();
 newton(1) ;
 cout << "\n\n\n\tGoodbye!" ;
 return;
}
// ------------------------------------------------------------------------- //
void bisection(int fn)
{
 double x, x0 = 0.5, x1 = 1.0, fx0 = f1(x0), fx = f1(x1) ;
 int i = 0 ;
 if (fn == 0)
	 cout << "\n USING BISECTION METHOD TO COMPUTE ROOTS"
			<< "\n _______________________________________\n\n" ;
 DispProb(fn);
 while ((fx > 0.0000001 || fx < -0.0000001) && i < 20)
 {
	 x = (x0 + x1)/2 ;
	 if (fn == 0)  // first equation
		fx = f1(x) ;
	 else      // second equation
		fx = f2(x) ;
	 if (fx0 * fx <= 0)
		x1 = x ;
	 else
	 {	x0 = x ;
			fx0 = fx ;
	 }
	 i++ ;
 }
 cout << "\n\nRoot: " << x0 << "\nIterations: " << i << "(max-20)" ;
 return;
} // bisection
// ------------------------------------------------------------------------- //
void mfp(int fn)
{
 if (fn == 0)
	 cout << "\n USING MODIFIED FALSE POSITION METHOD TO COMPUTE ROOTS"
			<< "\n _____________________________________________________\n\n" ;
 DispProb(fn) ;
 double x, fx = 1, x0 = 0.5, x1 = 1.0, fx0 = f1(x0), fx1 = f1(x1), lfx = fx0 ;
 int i =0 ;
 while ((fx < -0.0000001 || fx > 0.0000001) && i < 20)
 {
	 x = x0 - (fx0 * (x1 - x0)/(fx1 - fx0)) ;
	 if (fn == 0) // first equation
		fx = f1(x) ;
	 else     // second equation
		fx = f2(x) ;
	 if (fx0 * fx <= 0)
	 {
		x1 = x ;
		fx1 = fx ;
		if (lfx * fx > 0)
		 fx0 /= 2 ;
	 }
	 else
	 {
		x0 = x ;
		fx0 = fx ;
		if (lfx * fx > 0)
		 fx1 /= 2 ;
	 }
	 lfx = fx ;
	 i++;
 }
 cout << "\n\nRoot: " << x0 << "\nIterations: " << i << "(max-20)" ;
} // mfp
// ------------------------------------------------------------------------- //
void secant(int fn)
{
 if (fn == 0)    // first time
	 cout << "\n USING SECANT METHOD TO COMPUTE ROOTS"
			<< "\n ____________________________________\n\n" ;
 DispProb(fn) ;
 double fx0, fx1, x0 = 0.5, x1 = 1.0, x ;
 int i =0 ;
 fx0 = f1(x0) ;
 fx1 = f1(x1) ;
 while ((fx0 < -0.0000001 || fx0 > 0.0000001) && i < 20)
 {
	 x = x1 - fx1*(x1 - x0)/(fx1 - fx0) ;
	 x0 = x1 ;
	 fx0 = fx1 ;
	 x1 = x ;
	 if (fn == 0) // first equation
		fx1 = f1(x1) ;
	 else     // second equation
		fx1 = f2(x1) ;
	 i++;
 }
 cout << "\n\nRoot: " << x0 << "\nIterations: " << i << "(max-20)" ;
} // secant
// ------------------------------------------------------------------------- //
void newton(int fn)
{
 double fx = 1, x1 = 1, x0 = 1 ;
 int i = 0 ;
 if (fn == 0)
	 cout << "\n USING NEWTON'S METHOD TO COMPUTE ROOTS"
			<< "\n ______________________________________\n\n" ;
 DispProb(fn) ;
 while ((fx > 0.0000001 || fx < -0.0000001) && i < 20)
 {
	 x0 = x1 ;
	 if (fn == 0)  // first equation
	 {
		fx = f1(x0) ;
		x1 = x0 - fx/f1_derivative(x0) ;
	 }
	 else      // second equation
	 {
		fx = f2(x0) ;
		x1 = x0 - fx/f2_derivative(x0) ;
	 }
	 i++ ;
 }
 cout << "\n\nRoot: " << x0 << "\nIterations: " << i << "(max-20)" ;
 return;
} // newton
// ------------------------------------------------------------------------- //
double f1(double x)
{   return (x*x -exp(-x)) ;  }
double f1_derivative(double x)
{   return (2*x + exp(-x)) ;  }
// ------------------------------------------------------------------------- //
double f2(double x)
{   return (x*x*x - cos(x)) ; }
double f2_derivative(double x)
{   return (3*x*x + sin(x)) ; }
// ------------------------------------------------------------------------- //
void DispProb(int fn)
{
 if (fn == 0)
	 cout	<< "We will now solve the equation : \n1)\t (x*x) - Exp(-x)\n\n"
			<< "with original approximations of x0 = 0.5 and x1 = 1" ;
 else
	 cout << "\n_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ \n"
			<< "\nWe will now solve the equation : \n2)\t(x*x*x) - Cos(x)\n\n"
			<< "with original approximations of x0 = 0.5 and x1 = 1.0" ;
}
```

