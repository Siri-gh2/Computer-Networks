# CRC (Cyclic Redundancy Check)

## 📌 Concept
CRC (Cyclic Redundancy Check) is an **error detection technique** used in the
**Data Link Layer** and **Transport Layer** to detect errors in transmitted data.

In CRC, the data is treated as a **binary polynomial** and divided by a
**generator polynomial** using **XOR division**.  
The remainder obtained from this division is called the **CRC** and is appended
to the original data before transmission.

---

## 🎯 Main Goal
- Detect errors during data transmission
- Ensure **data integrity**
- Provide strong error-detection capability with minimal overhead

---

## 🧩 Basic Terms
- **Dataword**: Original binary data
- **Generator Polynomial (Divisor)**: A predefined binary pattern
- **CRC**: Remainder obtained after XOR division
- **Codeword**: Dataword + CRC

---

## 📤 Sender Side (CRC Generation)

### 🔹 Logic
1. Read the dataword and generator polynomial
2. Append `(length of divisor − 1)` zeros to the dataword
3. Perform XOR division of the appended data with the divisor
4. Extract the remainder (CRC)
5. Append the CRC to the original dataword and transmit

---

### 🧾 Sender Program (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

string xorDivision(string dividend, string divisor)
{
    int n = divisor.length();

    for (int i = 0; i <= dividend.length() - n;)
    {
        if (dividend[i] == '1')
        {
            for (int j = 0; j < n; j++)
                dividend[i + j] =
                    (dividend[i + j] == divisor[j]) ? '0' : '1';
        }

        while (i < dividend.length() && dividend[i] != '1')
            i++;
    }
    return dividend;
}

int main()
{
    string data, divisor;
    cin >> data >> divisor;

    int k = divisor.length() - 1;
    string appendedData = data + string(k, '0');

    string result = xorDivision(appendedData, divisor);
    string crc = result.substr(result.length() - k);

    cout << "CRC: " << crc << endl;
    cout << "Transmitted Data: " << data + crc << endl;

    return 0;
}

📥 Receiver Side (CRC Check)
🔹 Logic

Receive the transmitted data

Divide it by the same generator polynomial

Check the remainder

If remainder contains only 0s → no error

Otherwise → error detected

🧾 Receiver Program (C++)
#include <bits/stdc++.h>
using namespace std;

string xorDivision(string dividend, string divisor)
{
    int n = divisor.length();

    for (int i = 0; i <= dividend.length() - n;)
    {
        if (dividend[i] == '1')
        {
            for (int j = 0; j < n; j++)
                dividend[i + j] =
                    (dividend[i + j] == divisor[j]) ? '0' : '1';
        }

        while (i < dividend.length() && dividend[i] != '1')
            i++;
    }
    return dividend;
}

int main()
{
    string receivedData, divisor;
    cin >> receivedData >> divisor;

    string result = xorDivision(receivedData, divisor);

    bool error = false;
    for (char bit : result)
    {
        if (bit == '1')
        {
            error = true;
            break;
        }
    }

    if (error)
        cout << "Error detected" << endl;
    else
        cout << "No error detected" << endl;

    return 0;
}

Example
Input
Dataword  : 110101
Divisor   : 1011

Process

Append zeros → 110101000

CRC obtained → 100

Transmitted data → 110101100

✅ Conclusion

CRC is a powerful and efficient error detection technique that uses polynomial
division to detect transmission errors. It is widely used in modern
communication protocols due to its high reliability.
