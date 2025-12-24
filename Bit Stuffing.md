# Bit Stuffing

## 📌 Concept
Bit Stuffing is a **framing technique** used in the **Data Link Layer** for
**bit-oriented protocols** such as HDLC.

In this technique, the data is transmitted as a stream of bits.
To ensure that the data does not accidentally contain the same pattern as the
frame delimiter, extra bits are inserted by the sender.

---

## 🎯 Main Goal
- Prevent confusion between **data bits** and **frame delimiter bits**
- Maintain proper frame synchronization
- Ensure reliable and transparent data transmission

---

## 🧩 Rule Used
- **Frame Flag**: `01111110`
- **Stuffing Rule**:
  - After **five consecutive `1`s**, the sender inserts a `0`
  - The receiver removes this extra `0` during de-stuffing

---

## 📤 Sender Side (Bit Stuffing)

### 🔹 Logic
1. Read the input data bits
2. Traverse bit by bit
3. Count consecutive `1`s
4. After five `1`s, insert a `0`
5. Reset the count

---

### 🧾 Sender Program (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string data;
    cin >> data;

    string stuffed = "";
    int count = 0;

    for (char bit : data)
    {
        stuffed += bit;

        if (bit == '1')
        {
            count++;
            if (count == 5)
            {
                stuffed += '0';  // stuff a 0
                count = 0;
            }
        }
        else
        {
            count = 0;
        }
    }

    cout << stuffed << endl;
    return 0;
}

📥 Receiver Side (De-Stuffing)
🔹 Logic

Traverse the received bit stream

Count consecutive 1s

After five 1s, skip the next bit if it is 0

Reconstruct the original data

🧾 Receiver Program (C++)
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string stuffed;
    cin >> stuffed;

    string original = "";
    int count = 0;

    for (int i = 0; i < stuffed.size(); i++)
    {
        original += stuffed[i];

        if (stuffed[i] == '1')
        {
            count++;
            if (count == 5)
            {
                i++;        // skip stuffed 0
                count = 0;
            }
        }
        else
        {
            count = 0;
        }
    }

    cout << original << endl;
    return 0;
}

Example
Input Data
01111110111110

Stuffed Output
0111110101111100

✅ Conclusion

Bit stuffing ensures that the data stream never accidentally matches the
frame delimiter pattern, making it an essential framing technique for
bit-oriented communication protocols.
