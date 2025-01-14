#include <iostream>
#include <cctype>   // For isupper(), islower(), isdigit()
#include <string>   // For string manipulation

using namespace std;  // Allows use of standard library components without prefix

// Function to check if a character is a special character
bool isSpecialChar(char ch) {
    return !(isalnum(ch));  // Returns true if character is neither a letter nor a digit
}

// Function to calculate password score
int calculatePasswordScore(const string &password) {
    bool hasUpper = false, hasLower = false, hasDigit = false, hasSpecial = false;
    int score = 0;

    // Loop through each character of the password
    for (int i = 0; i < password.length(); ++i) {
        char ch = password[i]; 
        if (isupper(ch)) hasUpper = true;
        if (islower(ch)) hasLower = true;
        if (isdigit(ch)) hasDigit = true;
        if (isSpecialChar(ch)) hasSpecial = true;
    }

    // Add points for each condition satisfied
    if (password.length() >= 8) score += 2;  // Length check
    if (hasUpper) score += 2;
    if (hasLower) score += 2;
    if (hasDigit) score += 2;
    if (hasSpecial) score += 2;

    return score;
}

// Function to analyze password strength
string getPasswordStrength(int score) {
    if (score >= 8) return "Strong";
    if (score >= 5) return "Moderate";
    return "Weak";
}

// Function to provide tips for strengthening the password
void giveTips(const string &password) {
 bool hasDigit = false, hasLower = false, hasUpper = false, hasSpecial = false;

if (password.length() < 8) 
    cout << "- Increase the length of your password to at least 8 characters.\n";
for (int i = 0; i < password.length(); ++i) {
    char c = password[i];
    if (isdigit(c)) hasDigit = true;
    else if (islower(c)) hasLower = true;
    else if (isupper(c)) hasUpper = true;
    else if (ispunct(c)) hasSpecial = true;
}
if (!hasDigit) cout << "- Add a digit to your password.\n";
if (!hasLower) cout << "- Add a lowercase letter to your password.\n";
if (!hasUpper) cout << "- Add an uppercase letter to your password.\n";
if (!hasSpecial) cout << "- Add a special character to your password.\n";

}

int main() {
    string password;

    cout << "Enter your password: ";
    cin >> password;

    int score = calculatePasswordScore(password);
    string strength = getPasswordStrength(score);
    cout << "\nPassword Score: " << score << "/10\n";
    cout << "Password Strength: " << strength << "\n";
    if (strength == "Weak") {
        cout << "\nTips to make your password stronger:\n";
        giveTips(password);
    }

    return 0;
}
