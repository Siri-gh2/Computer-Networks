# Byte / Character Stuffing

## 📌 Concept
Byte (or Character) Stuffing is a **framing technique** used in the **Data Link Layer**
to ensure that the data does not get confused with control information.

Special characters are used to mark the **start and end of a frame**.
If these special characters appear inside the data, an **escape character** is added
before them to maintain data transparency.

---

## 🎯 Main Goal
- Clearly identify **frame boundaries**
- Prevent data from being misinterpreted as control characters
- Maintain **data transparency** during transmission

---

## 🧩 Assumptions
- **FLAG character** : `F` (marks start and end of frame)
- **ESC character**  : `E` (escape character)

---

## 📤 Sender Side (Byte Stuffing)

### 🔹 Logic
1. Add `FLAG` at the beginning and end of the frame
2. Traverse each character of the data
3. If the character is `FLAG` or `ESC`, insert `ESC` before it
4. Append the character to the output

---

### 🧾 Sender Program (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string data;
    cin >> data;

    char FLAG = 'F';
    char ESC  = 'E';

    string stuffed = "";
    stuffed += FLAG;

    for (char ch : data)
    {
        if (ch == FLAG || ch == ESC)
            stuffed += ESC;
        stuffed += ch;
    }

    stuffed += FLAG;

    cout << stuffed << endl;
    return 0;
}


📥 Receiver Side (De-Stuffing)
🔹 Logic

Remove the starting and ending FLAG

Traverse the remaining data

If ESC is encountered, skip it and take the next character

Reconstruct the original data

🧾 Receiver Program (C++)
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string stuffed;
    cin >> stuffed;

    char ESC = 'E';
    string original = "";

    for (int i = 1; i < stuffed.size() - 1; i++)
    {
        if (stuffed[i] == ESC)
            i++;            // skip escape character
        original += stuffed[i];
    }

    cout << original << endl;
    return 0;
}

Example
Input Data
DEENU

Stuffed Frame
FDEEEENUF

De-Stuffed Output
DEENU

✅ Conclusion

Byte stuffing ensures reliable data transmission by preventing confusion
between data characters and control characters, making it a crucial
framing technique in computer networks.
