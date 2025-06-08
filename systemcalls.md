# 🧠 System Calls — Learning Summary

This README summarizes everything I've learned about **system calls** — the bridge between programs and the operating system.

---

## 📌 What is a System Call?

A **system call** is how a program requests a service from the **operating system kernel**.

> Programs can't directly access hardware or critical system resources. So they "call" the OS to do tasks like reading files, accessing memory, or creating processes.

---

## 🛠️ What System Calls Do

| Task                  | Example System Calls              |
|-----------------------|-----------------------------------|
| File operations       | `open()`, `read()`, `write()`, `close()` |
| Process management    | `fork()`, `exec()`, `wait()`, `exit()` |
| Memory management     | `mmap()`, `brk()`, `munmap()`     |
| Device control        | `ioctl()`, `read()`               |
| IPC (communication)   | `pipe()`, `signal()`, `msgget()`  |

---

## 🧱 User Mode vs Kernel Mode

| Mode         | Can Access Hardware? | Who Runs Here?                  |
|--------------|-----------------------|----------------------------------|
| User Mode    | ❌ No                 | Regular apps and programs        |
| Kernel Mode  | ✅ Yes                | OS kernel and system calls       |

- **System calls** switch from **user mode ➜ kernel mode** to perform privileged operations.

---

## 🧠 What is the Kernel?

The **kernel** is the core of the OS:
- Manages memory, processes, files, devices.
- Only runs in **kernel mode**.
- Apps **must ask the kernel** to do low-level tasks using system calls.

---

## 🧪 How a System Call Works (Simplified)

1. Your app calls a function like `read()`.
2. A **system call instruction** triggers a switch to kernel mode.
3. The kernel does the requested task (e.g., read file data).
4. Control is returned to your program with the result.

---

## 🧰 Examples in Real Life

- `read(0, buf, 100)` → reads from keyboard (stdin).
- `fork()` → creates a new child process.
- `write(1, "Hello\n", 6)` → prints to terminal (stdout).
- `open("file.txt")` → requests file handle from the OS.

---

## 📚 What’s Next?

Here’s a **learning roadmap** to go deeper:

### ✅ Basics
- [x] What system calls are
- [x] Kernel vs user mode
- [x] Common system calls

### 🟡 Intermediate
- [ ] Write raw syscall-based code in C
- [ ] Learn how processes & memory are handled (`fork`, `exec`, `mmap`)
- [ ] Understand file descriptors & pipes

### 🔴 Advanced
- [ ] Learn how syscalls are implemented (`syscall`, `int 0x80`)
- [ ] Use `strace` to debug running programs
- [ ] Sandbox with `seccomp`
- [ ] Try writing a simple kernel module (Linux)

---

## 🔍 Bonus: Trace Any Program

Use `strace` to see what system calls a program makes:

```bash
strace ls
strace ./your_program

