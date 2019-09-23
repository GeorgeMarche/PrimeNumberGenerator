# PrimeNumberGenerator
Input which prime number you want (ex. 5th, 10th, 100th... even the 30 millionth!), and my program can spit out the first 10 million primes in less than 15 minutes.
#include <cmath>
#include <iostream>
using namespace std;

int main(){
        // Get the array of prime "foundation" numbers
        int PFN[8];
        PFN[0] = 7;
        PFN[1] = 11;
        PFN[2] = 13;
        PFN[3] = 17;
        PFN[4] = 19;
        PFN[5] = 23;
        PFN[6] = 29;
        PFN[7] = 31;

        // Get the number of primes wanted
        int num;
        int sqrtNum;
        cout << "Number of primes wanted: ";
        cin >> num;
        int n = num;

        // Print them

        // Variables for "factor of 30"
        int fac30 = 0;
        int fac302;
        bool isPrime;

        // Print first 3 "exceptions"
        if (num > 0){
                cout << "2" << endl;
                num--;
        }
        if (num > 0){
                cout << "3" << endl;
                num--;
        }
        if (num > 0){
                cout << "5" << endl;
                num--;
        }

        // Anything past 3 prime numbers print here
        while (num > 0){

                // For each number 30*fac30 + PFN[i]...
                for (int i = 0; i < 8; i++){

                        // Set/reset counter and bool variables
                        fac302 = 0;
                        isPrime = true;
                        sqrtNum = sqrt(n - num) + (n - num)/11000;

                        // Create a condition for all numbers that aren't PFN numbers
                        while (sqrtNum > 0 && fac30 != 0){

                                // Check if the number being tested is divisible by any prime number that is at most the square root of it
                                for (int k = 0; k < 8; k++){

                                        // If it is divisible, then it's not a prime
                                        if ((PFN[i] + (30 * fac30))%(PFN[k] + (30 * fac302)) == 0 && sqrtNum != 0){
                                                isPrime = false;
                                        }

                                        // If it isn't prime, end this loop
                                        if (!isPrime){
                                                sqrtNum = 0;
                                                break;
                                        }
                                        sqrtNum--;
                                }
                                fac302++;
                        }

                        // If the number is prime and the number is within the range provided, print
                        if (num > 0 && isPrime){
                                cout << PFN[i] + (30 * fac30) << endl;
                                num--;
                        }
                }
                fac30++;
        }
}
