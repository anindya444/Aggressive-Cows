# Aggressive-Cows
Given an array stalls[] which denotes the position of a stall and an integer k which denotes the number of aggressive cows. The task is to assign stalls to k cows such that the minimum distance between any two of them is the maximum possible
#include <iostream>
#include<vector>
#include<algorithm>
using namespace std;


bool check(vector<int> &a, int dist, int cows) {
    int n = a.size(); 
    int cnt = 1; 
    int last = a[0];
    for (int i = 1; i < n; i++) {
        if (a[i] - last >= dist) {
            cnt++; 
            last = a[i]; 
        }
    }
    return (cnt>=cows);
}
int aggressiveCows(vector<int> &a, int k) {
    int n = a.size();
     sort(a.begin(), a.end());
    int res=1;
    int lo = 1, hi = a[n - 1] - a[0];
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        if (check(a, mid, k)) {
            lo = mid + 1;
            res=mid;
        }
        else hi = mid - 1;
    }
    return res;
}

int main()
{
    vector<int> a = {1,2,4,8,9};
    int k = 3;
   
    cout << aggressiveCows(a, k);
    return 0;
}

