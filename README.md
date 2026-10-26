# session-11


### Task 1: Pointer Declaration, Dereferencing, and Address Printing

```c
#include <stdio.h>

int main() {
    // Declare integer variable
    int likes = 1250;

    // Declare pointer variable and assign the address of 'likes'
    int *ptrLikes = &likes;

    // Printing values and addresses
    printf("Value of likes directly                  : %d\n", likes);
    printf("Address of likes (&likes)                 : %p\n", (void *)&likes);
    printf("Value stored in ptrLikes (Address held)   : %p\n", (void *)ptrLikes);
    printf("Value accessed via dereferencing (*ptrLikes): %d\n", *ptrLikes);

    return 0;
}

```

---

### Task 2: Swapping Playlist Counts Using Pointers

```c
#include <stdio.h>

// Function definition using pointer parameters
void swapPlaylistCounts(int *a, int *b) {
    int temp = *a; // Dereference 'a' to get its value
    *a = *b;       // Assign value of 'b' into memory location of 'a'
    *b = temp;     // Assign temp value into memory location of 'b'
}

int main() {
    int playlistA = 45; // Songs in Playlist A
    int playlistB = 80; // Songs in Playlist B

    printf("--- Before Swap ---\n");
    printf("Playlist A: %d songs\n", playlistA);
    printf("Playlist B: %d songs\n", playlistB);

    // Pass memory addresses using the reference operator (&)
    swapPlaylistCounts(&playlistA, &playlistB);

    printf("\n--- After Swap ---\n");
    printf("Playlist A: %d songs\n", playlistA);
    printf("Playlist B: %d songs\n", playlistB);

    return 0;
}

```

---

### Task 3: Iterating an Array Using Pointer Arithmetic

In C, an array's name decays to a pointer to its first element. Adding `1` to an `int *` moves the pointer forward by `sizeof(int)` bytes (typically 4 bytes).

```c
#include <stdio.h>

int main() {
    int orders[5] = {320, 150, 499, 850, 210};
    int *ptr = orders; // Points to orders[0]

    printf("--- Zomato Orders & Memory Addresses ---\n");
    for (int i = 0; i < 5; i++) {
        // *(ptr + i) dereferences the element at offset i
        // (ptr + i) yields the exact memory address of that element
        printf("Order %d: ₹%d | Memory Address: %p\n", i + 1, *(ptr + i), (void *)(ptr + i));
    }

    return 0;
}

```

---

### Task 4: Incrementing Followers Using Pointer Arithmetic

```c
#include <stdio.h>

// Function iterates through the array exclusively using pointer arithmetic
void incrementFollowers(int *followers, int n) {
    for (int i = 0; i < n; i++) {
        *(followers + i) += 100; // Increment value by 100 at each address
    }
}

int main() {
    int followerCounts[5] = {1200, 3450, 890, 5600, 2300};
    int n = 5;

    printf("--- Initial Follower Counts ---\n");
    for (int i = 0; i < n; i++) {
        printf("Friend %d: %d\n", i + 1, followerCounts[i]);
    }

    // Call function by passing array pointer and size
    incrementFollowers(followerCounts, n);

    printf("\n--- Updated Follower Counts (+100) ---\n");
    for (int i = 0; i < n; i++) {
        printf("Friend %d: %d\n", i + 1, followerCounts[i]);
    }

    return 0;
}

```

---

### Task 5: Memory Diagram for `likes` and `ptrLikes`

```text
========================================================================================
                                    RAM / MEMORY
========================================================================================

     Variable: ptrLikes                                 Variable: likes
     Data Type: int*                                    Data Type: int
     Memory Address: 0x7ffd9a12                         Memory Address: 0x7ffd9a00
    +-------------------------+                        +-------------------------+
    |                         |                        |                         |
    |       0x7ffd9a00        |───────────────────────>│          1250           |
    |  (Address of 'likes')   |    Points to Address   |    (Value of 'likes')   |
    |                         |                        |                         |
    +-------------------------+                        +-------------------------+
                 ▲                                                  ▲
                 │                                                  │
                 │                                                  │
         [ Pointer Variable ]                              [ Target Variable ]
   Holds the hexadecimal address                      Holds the actual data value.
    of the target variable.                           Dereferencing (*ptrLikes) reads
                                                      the value at 0x7ffd9a00.
========================================================================================

```

#### Diagram Labels Breakdown

* **Target Variable Name:** `likes`
* **Target Variable Address:** `0x7ffd9a00` *(Example hexadecimal stack address)*
* **Target Variable Value:** `1250`
* **Pointer Variable Name:** `ptrLikes`
* **Pointer Variable Address:** `0x7ffd9a12`
* **Pointer Variable Value:** `0x7ffd9a00` *(Stores the address of `likes`)*
* **Dereferencing Operation (`*ptrLikes`):** Follows the arrow from `0x7ffd9a00` to retrieve or modify `1250`.
