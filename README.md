#task1
#include <stdio.h>
#include <string.h>
#define MAX 100
void printLCS(char X[], char Y[], int m, int n) {
    int dp[MAX][MAX];
    int i, j;
 for (i = 0; i <= m; i++) {
        for (j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                dp[i][j] = 0;
            else if (X[i - 1] == Y[j - 1])
                dp[i][j] = dp[i - 1][j - 1] + 1;
            else
                dp[i][j] = (dp[i - 1][j] > dp[i][j - 1]) ? dp[i - 1][j] : dp[i][j - 1];
        }
    }
    printf("\nCost Matrix:\n");
    for (i = 0; i <= m; i++) {
        for (j = 0; j <= n; j++)
            printf("%2d ", dp[i][j]);
        printf("\n");
    }
    int index = dp[m][n];
    char lcs[index + 1];
    lcs[index] = '\0';  
    i = m;
    j = n;
    while (i > 0 && j > 0) {
        if (X[i - 1] == Y[j - 1]) {
            lcs[index - 1] = X[i - 1];
            i--;
            j--;
            index--;
        } else if (dp[i - 1][j] > dp[i][j - 1])
            i--;
        else
  j--;
    }
    printf("\nLongest Common Subsequence: %s", lcs);
    printf("\nLength of Longest Common Subsequence: %d\n", dp[m][n]);
}
int main() {
    char X[MAX] = "AGCCCTAAGGGCTACCTAGCTT";
    char Y[MAX] = "GACAGCCTACAAGCGTTAGCTTG";
    int m = strlen(X);
    int n = strlen(Y);
    printf("X = %s\nY = %s\n", X, Y);
    printLCS(X, Y, m, n);
    return 0;
}
#task2 
#include <stdio.h>
#include <string.h>
#define MAX 100
void printLRS(char str[]) {
    int n = strlen(str);
    int dp[MAX][MAX];
    int i, j;
    for (i = 0; i <= n; i++) {
        for (j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                dp[i][j] = 0;
            else if (str[i - 1] == str[j - 1] && i != j)
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = (dp[i - 1][j] > dp[i][j - 1]) ? dp[i - 1][j] : dp[i][j - 1];
        }
    }
    int index = dp[n][n];
    char lrs[index + 1];
    lrs[index] = '\0';
    i = n;
    j = n;
    while (i > 0 && j > 0) {
        if (dp[i][j] == dp[i - 1][j - 1] + 1 && str[i - 1] == str[j - 1] && i != j) {
            lrs[index - 1] = str[i - 1];
            i--;
            j--;
            index--;
        } else if (dp[i - 1][j] > dp[i][j - 1])
            i--;
        else
            j--;
    }
    printf("\nLongest Repeating Subsequence: %s", lrs);
    printf("\nLength of Longest Repeating Subsequence: %d\n", dp[n][n]);
}

int main() {
    char S[MAX] = "AABCBDC";
    printf("Input String: %s\n", S);
    printLRS(S);
    return 0;
}
