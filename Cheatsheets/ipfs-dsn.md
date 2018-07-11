# Use IPFS to host your webpage using a standard domain (includes cool DNS trick!)

If you are looking into having your application accesible through `youdomain.com`, instead of referencing it by a `/ipfs/hash`, follow the steps below.

Every IPFS node HTTP interface checks the host header when it receives a request from a browser, then it performs a DNS lookup for a TXT Record, looks if there is any MerkleLink available, and, if there is, it performs a lookup, caching that path and serving it as if it was a static webserver.

To make this work, simply:

1. Publish your application using `ipns name publish $HASH`.
2. Save the returned hash.
3. Find the IPFS ip addresses using `$ dig ipfs.io`. Example:

    ```sh
    $ dig +short ipfs.io
    178.62.61.185
    178.62.158.247
    104.236.76.40
    ...
    ```

4. Decide which domain or subdomain will host your IPFS application. We're going to use `ipfs.yourdomain.com`
5. In the DNS administration for your domain, add an A record for each of the ipfs.io IPs addresses. Example:

    ```sh
    yourdomain.com

    ipfs     A     178.62.61.185
    ipfs     A     178.62.158.247
    ipfs     A     104.236.76.40
    ...
    ```

    If you're using the root domain, your DNS rules should look like:

    ```sh
    yourdomain.com

    @        A     178.62.61.185
    @        A     178.62.158.247
    @        A     104.236.76.40
    ...
    ```

6. Next, the cool DNS trick. Add a TXT record with the hash of your IPFS application.
    Example:

    ```sh
    yourdomain.com

    ipfs     TXT     dnslink=/ipfs/QmfDw7pfgtYfki6HfYNbjxjBHb45hD7GrrqDp2Vvcte1Cj
    ```

7. Wait a little bit for DNS to propagate.
8. Open `ipfs.yourdomain.com` and see that your page was loaded!

Voilá, your page is now cached and is being served by IPFS.

**Note: You can also host your own IPFS nodes and use the same DNS trick.**
