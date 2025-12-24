# 📘 Computer Networks

This repository contains **core concepts and practical implementations of Computer Networks**, with a strong focus on the **Data Link Layer** and its **framing and error detection techniques**.

The code and explanations here are aligned with **CN theory, labs, and exams**, making this repository useful for both **learning and revision**.

---

## 🧠 About Computer Networks

A **Computer Network** is a collection of interconnected devices that communicate and share data using well-defined protocols.  
Computer Networks enable services such as file sharing, internet access, email, cloud computing, and distributed systems.

Networks are commonly studied using the **OSI Model**, which divides communication into layers for better design and understanding.

---

## 📚 Focus of This Repository

This repository mainly focuses on the **Data Link Layer (Layer 2)** of the OSI Model, which is responsible for:

- Framing
- Error detection
- Reliable data transfer
- Data transparency

---

## 🧩 Data Link Layer – Overview

The **Data Link Layer** ensures that data sent from the sender reaches the receiver **without errors and in proper frame format**.

### Key Responsibilities:
- **Framing**: Dividing raw bit streams into manageable frames
- **Error Detection**: Detecting transmission errors
- **Data Transparency**: Ensuring control information does not interfere with actual data
- **Flow Control**: Managing sender–receiver speed mismatch

---

## 🧷 Framing Techniques Covered

Framing is the process of **grouping bits into frames** so the receiver can correctly identify the start and end of data.

This repository covers the following **Data Link Layer framing techniques**:

---

### 📌 1. Byte / Character Stuffing

**Concept**  
Special characters (such as FLAG and ESC) are used to mark the beginning and end of a frame.  
If these characters appear in the data, an escape character is inserted before them.

**Goal**
- Maintain data transparency
- Avoid confusion between data and control characters

**Implementation**
- Sender-side byte stuffing
- Receiver-side de-stuffing

---

### 📌 2. Bit Stuffing

**Concept**  
Data is transmitted as bits.  
To prevent the data from matching the frame delimiter pattern, a `0` is inserted after **five consecutive `1`s**.

**Goal**
- Prevent accidental frame delimiter patterns inside data
- Maintain synchronization in bit-oriented protocols (e.g., HDLC)

**Implementation**
- Bit stuffing at sender
- Bit de-stuffing at receiver

---

### 📌 3. CRC (Cyclic Redundancy Check)

**Concept**  
CRC is an **error detection technique** that treats data as a binary polynomial and performs division using XOR with a generator polynomial.

**Goal**
- Detect transmission errors
- Ensure data integrity

**Implementation**
- CRC generation at sender
- CRC verification at receiver

---

## 📁 Repository Structure

```text
Computer-Networks/
│
├── Byte-Stuffing.md
├── Bit-Stuffing.md
├── CRC.md
├── README.md


Each topic includes:

Clear concept explanation

Main objective

Sender program

Receiver program

🛠️ Technologies Used

Language: C++

Concepts: OSI Model, Data Link Layer

Focus: Framing & Error Detection

🎯 Learning Outcomes

By exploring this repository, you will understand:

How framing is implemented in real networks

The difference between byte-oriented and bit-oriented protocols

How errors are detected during data transmission

Practical C++ implementations of CN concepts

📌 Future Enhancements

Sliding Window Protocols

Stop-and-Wait ARQ

Go-Back-N ARQ

Selective Repeat ARQ

Network Layer routing algorithms

📜 License

This repository is open-source and intended for educational purposes.
Feel free to use, modify, and improve it.


---

### Straight truth
This README now:
- ✅ Clearly mentions **Data Link Layer**
- ✅ Explains **framing techniques properly**
- ✅ Matches **CN exam theory**
- ✅ Looks **serious on GitHub**

If you want next:
- Add **diagrams section**
- Add **OSI model explanation**
- Convert this into **lab record style**
- Review file naming & repo structure

Say the word.
