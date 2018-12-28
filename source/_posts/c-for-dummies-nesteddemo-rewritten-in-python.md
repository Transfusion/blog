---
title: 'C++ For Dummies - Chapter 5: NestedDemo rewritten in Python'
url: 64.html
id: 64
categories:
  - Programming
date: 2013-10-26 16:30:58
tags:
---

// NestedDemo - input a series of numbers.
//              Continue to accumulate the sum
//              of these numbers until the user
//              enters a 0. Repeat the process
//              until the sum is 0.
#include #include #include using namespace std;

int main(int nNumberofArgs, char* pszArgs\[\])
{
    // the outer loop
    cout << "This program sums multiple seriesn"
         << "of numbers. Terminate each sequencen"
         << "by entering a negative number.n"
         << "Terminate the series by entering twon"
         << "negative numbers in a rown";

    // continue to accumulate sequences
    int accumulator;
    for(;;)
    {
        // start entering the next sequence
        // of numbers
        accumulator = 0;
        cout << "Start the next sequencen";

        // loop forever
        for(;;)
        {
            // fetch another number
            int nValue = 0;
            cout << "Enter next number: ";
            cin  >> nValue;

            // if it's negative...
            if (nValue < 0)
            {
                // ...then exit
                break;
            }

            // ...otherwise add the number to the
            // accumulator
            accumulator += nValue;
        }

        // exit the loop if the total accumulated is 0
        if (accumulator == 0)
        {
            break;
        }

        // output the accumulated result and start over
        cout << "The total for this sequence is "
            << accumulator
            << endl << endl;
    }

    // we're about to quit
    cout << "Thank you" << endl;

    // wait until user is ready before terminating program
    // to allow the user to see the program results
    system("PAUSE");
    return 0;
} 

#! /usr/bin/python
print "This program sums multiple seriesnof numbers. Terminate each sequencenb
y entering a negative number.nTerminate the series by entering twonnegative nu
mbers in a row"

def sumSequence():
    negative = True
    sum = 0
    while negative == True:
        inputnumber = int(raw_input("Enter next number: "))
        if inputnumber >= 0:
            sum += inputnumber
        else:
            negative = False
    return sum

def startSum():
    returnZero = True
    while returnZero == True:
        print "Start the next sequence"
        u = sumSequence()
        if u > 0:
            print "The total for this sequence is "+str(u)
        else:
            returnZero = False
    print "Thank you"

startSum()
raw_input()
#Transfusion's rewriting