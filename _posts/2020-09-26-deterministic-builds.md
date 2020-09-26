---
title: Generating deterministic static libraries for iOS
categories: 
  - mobile
tags:
  - ios
  - development
---

When generating a static library there are times you may be required to generate the same binary. This means the binary hash is equal on consecutive builds (i.e. building twice without any changes to the code). An example is a bank would like to keep your code in escrow and they want proof that the code can be rebuilt to generate the same binary that the bank received.

A static library linking process generates a `.a` file. When archiving to a fat binary the _libtool_ inserts a timestamp. The result is binaries built at different times will have different timestamps. The screenshot shows two binaries with different timestamps.

![Variable timestamp](/assets/images/deterministic-build/variable-timestamp.png) 

We need a way to prevent the timestamp from getting added or force the timestamp to be a fixed value. The proposed solution is to force the timestamp to a fixed value of zero. This can easily be done by setting the environment variable `ZERO_AR_DATE=1`. The result is a timestamp that is always zero.
You can easily call your build script like this: `ZERO_AR_DATE=1 ./build.sh`.

In the screenshot you can see the binary on the right has the timestamp set to zero. The `ZERO_AR_DATE=1` environment variable has been set when generating the binary on the right.

![Zero timestamp](/assets/images/deterministic-build/zero-timestamp.png)

This method is simple and allows generation of deterministic binaries. The benefit is one can now compare binaries by their hashes.




