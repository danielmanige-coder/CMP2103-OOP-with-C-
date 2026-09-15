#include <iostream>
#include <string>

// Function prototypes as requested
bool isValid(long long number);
int sumOfDoubleEvenPlace(long long number);
int getDigit(int number);
int sumOfOddPlace(long long number);
bool prefixMatched(long long number, int d);
int getSize(long long d);
long long getPrefix(long long number, int k);

int main() {
    long long cardNumber;
    std::cout << "Enter a credit card number as an integer: ";
    std::cin >> cardNumber;

    if (isValid(cardNumber)) {
        std::cout << cardNumber << " is valid" << std::endl;
    } else {
        std::cout << cardNumber << " is invalid" << std::endl;
    }

    return 0;
}

// Return true if the card number is valid
bool isValid(long long number) {
    // 1. Check length constraint (between 13 and 16 digits)
    int size = getSize(number);
    if (size < 13 || size > 16) {
        return false;
    }

    // 2. Check prefix constraint (starts with 4, 5, 37, or 6)
    if (!prefixMatched(number, 4) && 
        !prefixMatched(number, 5) && 
        !prefixMatched(number, 37) && 
        !prefixMatched(number, 6)) {
        return false;
    }

    // 3. Check Luhn Mod 10 validity rule
    int totalSum = sumOfDoubleEvenPlace(number) + sumOfOddPlace(number);
    return (totalSum % 10 == 0);
}

// Get the result from Step 2 (Double every second digit from right to left)
int sumOfDoubleEvenPlace(long long number) {
    int sum = 0;
    number /= 10; // Shift right by one position to start at the first even place from the right
    
    while (number > 0) {
        int digit = number % 10;
        sum += getDigit(digit * 2);
        number /= 100; // Skip to the next even position
    }
    return sum;
}

// Return this number if it is a single digit, otherwise, return the sum of the two digits
int getDigit(int number) {
    if (number < 10) {
        return number;
    }
    return (number % 10) + (number / 10);
}

// Return sum of odd place digits in number from right to left
int sumOfOddPlace(long long number) {
    int sum = 0;
    while (number > 0) {
        int digit = number % 10;
        sum += digit;
        number /= 100; // Skip to the next odd position
    }
    return sum;
}

// Return true if the digit d is a prefix for number
bool prefixMatched(long long number, int d) {
    return getPrefix(number, getSize(d)) == d;
}

// Return the number of digits in d
int getSize(long long d) {
    if (d == 0) return 1;
    
    int count = 0;
    while (d > 0) {
        count++;
        d /= 10;
    }
    return count;
}

// Return the first k number of digits from number. 
// If the number of digits in number is less than k, return number.
long long getPrefix(long long number, int k) {
    int size = getSize(number);
    if (size <= k) {
        return number;
    }
    
    // Peel off the rightmost digits until exactly k digits are left
    long long divisor = 1;
    for (int i = 0; i < (size - k); i++) {
        divisor *= 10;
    }
    return number / divisor;
}
