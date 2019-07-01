# hello-world
#include <iostream>
#include <string>
#include <stack>
#include <cassert>
using namespace std;


class Solution {
public:
    bool isValid(string s) {
        if(s == "") return true;
        if(s.length() % 2 != 0) return false;
        stack<char> ss;
        for(auto i:s)
        {
            if(i == '(' || i == '[' || i == '{')
                ss.push(i);
            else
            {
                if (ss.size() == 0 && (i == ']' || i == '}' || i == ')')) 
                    return false;
                else if((i == ']' && ss.top() != '[') || (i == ')' && ss.top() != '(') || (i == '}' && ss.top() != '{'))
                    return false;
                else ss.pop();
            }
        }
        if (ss.size() != 0 ) 
            return false; 
        else
            return true;
    }
};

string stringToString(string input) {
    assert(input.length() >= 2);
    string result;
    for (int i = 1; i < input.length() -1; i++) {
        char currentChar = input[i];
        if (input[i] == '\\') {
            char nextChar = input[i+1];
            switch (nextChar) {
                case '\"': result.push_back('\"'); break;
                case '/' : result.push_back('/'); break;
                case '\\': result.push_back('\\'); break;
                case 'b' : result.push_back('\b'); break;
                case 'f' : result.push_back('\f'); break;
                case 'r' : result.push_back('\r'); break;
                case 'n' : result.push_back('\n'); break;
                case 't' : result.push_back('\t'); break;
                default: break;
            }
            i++;
        } else {
          result.push_back(currentChar);
        }
    }
    return result;
}

string boolToString(bool input) {
    return input ? "True" : "False";
}
vector<string> ans;
    string s;
    vector<string> generateParenthesis(int n) {
        dfs(n, n);
        return ans;
    }
void dfs(int l, int r){
        if(r == 0){
            ans.push_back(s);
            return;
        }
            
        if(l){
            s += '(';
            dfs(l-1, r);
            s.pop_back();
        }
        if(r>l){
            s += ')';
            dfs(l, r-1);
            s.pop_back();
        }
    }
    
int main() {
    string line;
    while (getline(cin, line)) {
        string s = stringToString(line);
        
        bool ret = Solution().isValid(s);

        string out = boolToString(ret);
        cout << out << endl;
    }
    return 0;
}
