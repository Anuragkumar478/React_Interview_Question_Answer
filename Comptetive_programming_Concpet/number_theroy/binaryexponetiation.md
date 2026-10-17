static long power(long a, long n, long mod) {
    long ans = 1;

    while (n > 0) {
        if ((n & 1) == 1) {
            ans = (ans * a) % mod;
        }

        a = (a * a) % mod;
        n >>= 1;
    }

    return ans;
}