# Backtracking

- [Recursion](#recursion)
- [Backtracking](#backtracking)
- [Backtracking Problems](#backtracking-problems)
  - [KnapSack](#knapsack)
  - [Target Sum](#target-sum)
  - [Letter Combinations of a Phone Number](#letter-combinations-of-a-phone-number)
  - [Non-decreasing Subsequences](#non-decreasing-subsequences)
  - [Word Search](#word-search)
  - [Permutations](#permutations)

## Recursion

Recursion is a method where the solution to a problem depends on solutions to smaller instances of the same problem. The process continues until it reaches a base case.

```cpp

void recursion(int n) {
    if (n < 1) {
        return;
    } else {
        recursion(n - 1);
    }
}

```

## Backtracking

Backtracking is a general algorithm for finding all (or some) solutions to some computational problems, notably constraint satisfaction problems, that incrementally builds candidates to the solutions, and abandons a candidate as soon as it determines that the candidate cannot possibly be completed to a valid solution.

There are three types of problems in backtracking:

1. Decision Problem: In this, we search for a feasible solution.
2. Optimization Problem: In this, we search for the best solution.
3. Enumeration Problem: In this, we find all feasible solutions.

### Any Backtracking Problems Needs:

1. Goal: A way to determine if the solution is complete.
2. Choice: A way to break down the problem into smaller problems.
3. Base Case: A way to determine if the solution is valid, or to stop the recursion.

## Backtracking Problems

### KnapSack

Knapsack problem is a problem in combinatorial optimization. Given a set of items, each with a weight and a value, determine the number of each item to include in a collection so that the total weight is less than or equal to a given limit and the total value is as large as possible.

<b>Problem Type:</b> Optimization Problem, Find the maximum value of the items in the knapsack.

1. Goal: We want to maximize the value of the items in the knapsack.
2. Choice: We can either include the item in the knapsack or not.
3. Base Case: If we have included all the items or the weight of the item is greater than the weight of the knapsack.

```cpp

int n;
int values[n], weights[n];

int knapsack(int i, int w) {
    if (i == n) {
        return 0;
    }
    if (weights[i] > w) {
        return knapsack(i + 1, w);
    }
    return max(knapsack(i + 1, w), knapsack(i + 1, w - weights[i]) + values[i]);
}

```

### Target Sum

[LeetCode](https://leetcode.com/problems/target-sum/description/)

Given an array of integers, find the number of ways to add/subtract the elements of the array to get a target sum.

<b>Problem Type:</b> Enumeration Problem, Find all feasible solutions, in this case, the number of ways to get the target sum.

1. Goal: We want to find the number ways to get the target sum.
2. Choice: We can either add or subtract the element from the target sum.
3. Base Case: If we have reached the end of the array, then if the target sum is 0, then we have found a way to get the target sum.

```cpp

int n, target;
int nums[n];

int targetSum(int i, int sum) {
    if (i == n) {
        return sum == target ? 1 : 0;
    }
    return targetSum(i + 1, sum + nums[i]) + targetSum(i + 1, sum - nums[i]);
}

```

### Letter Combinations of a Phone Number

[LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

<b>Problem Type:</b> Enumeration Problem, Find all feasible solutions, in this case, all possible letter combinations of the phone number.

1. Goal: We want to find all possible letter combinations from each cell of the phone number.
2. Choice: For each cell, we can choose any of the letters that are mapped to the cell.
3. Base Case: If we have reached the end of the phone number, then we have found a letter combination.

```cpp

vector<string> letterCombinations(string digits) {
    vector<string> res;
    if (digits.empty()) {
        return res;
    }
    vector<string> dict = {"","","abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    string path;
    letterCombinationsHelper(digits, dict, 0, path, res);
    return res;
}

void letterCombinationsHelper(string digits, vector<string>& dict, int i, string& path, vector<string>& res) {
    if (i == digits.size()) {
        res.push_back(path);
        return;
    }
    for (char c : dict[digits[i] - '0']) {
        path.push_back(c);
        letterCombinationsHelper(digits, dict, i + 1, path, res);
        path.pop_back();
    }
}

```

### Non-decreasing Subsequences

[LeetCode](https://leetcode.com/problems/non-decreasing-subsequences/description/)

Given an integer array, find all the different possible increasing subsequences of the given array.

<b>Problem Type:</b> Enumeration Problem, Find all feasible solutions, in this case, all possible non-decreasing subsequences of the array.

1. Goal: We want to find all possible non-decreasing subsequences of the array.
2. Choice: For each element, we can either include it in the subsequence if and only if it is greater than or equal to the last element in the subsequence.
3. Base Case: If we have reached the end of the array, then we have found a non-decreasing subsequence.

```cpp

vector<vector<int>> findSubsequences(vector<int>& nums) {
    vector<vector<int>> res;
    vector<int> path;
    findSubsequencesHelper(nums, 0, path, res);
    return res;
}

set<vector<int>> usd;
void findSubsequencesHelper(vector<int>& nums, int i, vector<int>& path, vector<vector<int>>& res) {

    if (path.size() > 1) {
        if(!usd.count(path))
            res.push_back(path),usd.insert(path);
    }

    for (int j = i; j < nums.size(); j++) {
        if (!path.empty() and nums[j] < path.back()) {
            continue;
        }
        path.push_back(nums[j]);
        findSubsequencesHelper(nums, j + 1, path, res);
        path.pop_back();
    }
}

```

### Word Search

[LeetCode](https://leetcode.com/problems/word-search/description/)

Given a 2D board and a word, find if the word exists in the grid, such that the word can be constructed from the letters of sequentially adjacent cells, where "adjacent" cells are horizontally or vertically neighboring.

<b>Problem Type:</b> Decision Problem, Find a feasible solution, in this case, if the word exists in the grid.

1. Goal: We want to find if the word exists in the grid.
2. Choice: For each cell, that starts with the first letter of the word, we can always try all the possible adjacent cells, if the next letter of the word is equal to the letter in the adjacent cell, also we can mark the cell as visited.
3. Base Case: If we have reached the end of the word, or if we have visited all the cells in the grid, or if the next letter of the word is not equal to the letter in the adjacent cell.

```cpp

bool exist(vector<vector<char>>& board, string word) {
    int m = board.size();
    int n = board[0].size();

    function<bool(int, int, int)> backtrack = [&](int i, int j, int k) {
        if (k == word.length()) {
            return true;
        }
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != word[k]) {
            return false;
        }

        char temp = board[i][j];
        board[i][j] = '\0';

        if (backtrack(i + 1, j, k + 1) || backtrack(i - 1, j, k + 1) ||
            backtrack(i, j + 1, k + 1) || backtrack(i, j - 1, k + 1)) {
            return true;
        }

        board[i][j] = temp;
        return false;
    };

    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            if (backtrack(i, j, 0)) {
                return true;
            }
        }
    }
    return false;
}


```

### Permutations

[LeetCode](https://leetcode.com/problems/permutations/description/)

Given a collection of distinct integers, return all possible permutations.

<b>Problem Type:</b> Enumeration Problem, Find all feasible solutions, in this case, all possible permutations of the array.

1. Goal: We want to find all possible permutations of the array.
2. Choice: For each element, we can choose to insert it at any available position in the permutation.
3. Base Case: If we have reached the end of the array, then we have found a permutation.

```cpp

vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> res;
    vector<int> path;
    vector<bool> used(nums.size(), false);
    permuteHelper(nums, used, path, res);
    return res;
}

void permuteHelper(vector<int>& nums, vector<bool>& used, vector<int>& path, vector<vector<int>>& res) {
    if (path.size() == nums.size()) {
        res.push_back(path);
        return;
    }
    for (int i = 0; i < nums.size(); i++) {
        if (used[i]) {
            continue;
        }
        path.push_back(nums[i]);
        used[i] = true;
        permuteHelper(nums, used, path, res);
        path.pop_back();
        used[i] = false;
    }
}

```
