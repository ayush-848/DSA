# Problem

Given a text `hellohowareyouhellohowdoyoudo` and a pattern `how`, use the Boyer-Moore-Horspool algorithm to find all the starting indices of the pattern in the text.


### Input
- Text: `hellohowareyouhellohowdoyoudo`
- Pattern: `how`

### Expected Output
The pattern `how` appears at indices `5` and `17` in the text.

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

unordered_map<char, int> table(const string &pattern) {
    unordered_map<char, int> table;
    int n = pattern.size();
    for (int i = 0; i < n - 1; ++i) {
        table[pattern[i]] = max(1, n - i - 1);
    }
    return table;
}

vector<int> f(string &text, string &pattern) {
    int n = text.length();
    int m = pattern.length();
    vector<int> v;
    unordered_map<char, int> badCharTable = table(pattern);
    
    for (int i = 0; i <= n - m;) {
        int j = m - 1;
        while (j >= 0 && pattern[j] == text[i + j]) {
            j--;
        }
        if (j < 0) {
            v.push_back(i);
            i += m;
        } else {
            char mismatched = text[i + j];
            int shift = badCharTable.count(mismatched) ? badCharTable[mismatched] : m;
            i += max(1, shift);
        }
    }
    return v;
}

void position(vector<int>& v) {
    if (!v.empty()) {
        cout << "Pattern found at positions: ";
        for (int i : v) {
            cout << i << " ";
        }
        cout << endl;
    } else {
        cout << "Pattern not found" << endl;
    }
}

int main() {
    string text = "hellohowareyouhellohowdoyoudo";
    string pattern = "how";

    vector<int> v = f(text, pattern);

    position(v);

    return 0;
}
