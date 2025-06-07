# Erlang Hot Code Swapping Explained

This document explains how **hot code swapping** works in Erlang, allowing you to update running code without stopping the system — a key feature used in systems like WhatsApp for zero downtime deployments.

---

## What is Hot Code Swapping?

Hot code swapping means loading a **new version** of a module into a **running Erlang system** without restarting it. Erlang VM (BEAM) supports **two versions** of the same module simultaneously:

- **Old version** (currently running)
- **New version** (just loaded)

---

## How Does It Work?

1. You compile a new `.beam` file (Erlang compiled module) with your updated code.

2. The new `.beam` file is **loaded into the running system**.

3. The BEAM VM keeps **both old and new versions** of the module in memory.

4. **New processes** or function calls use the **new version** automatically.

5. **Old processes** continue to use the **old version** until they finish their work (e.g., processing pending messages).

6. Once no process uses the old version, BEAM removes it from memory.

---

## Key Benefits

- **Zero downtime**: No need to stop or restart the server.
- **No user disruption**: Users stay connected while updates are applied.
- **Safe upgrades**: Old tasks complete gracefully on the old version.
- **Built-in support**: Erlang VM handles version management automatically.

---

## Summary Table

| Feature                     | Description                             |
|-----------------------------|---------------------------------------|
| Number of active versions   | 2 (old and new)                       |
| Old processes behavior      | Continue running on old version until done |
| New processes behavior      | Automatically use the new version     |
| Server restart required?    | No                                    |
| Downtime?                  | None                                  |

---

## Example Use Case

- You have `chat_handler.erl` version 1 running, processing live chat messages.
- You compile and load version 2 with new features.
- Live chat messages currently being handled finish on version 1.
- New chat messages start processing on version 2.
- Once all old messages are done, version 1 is removed.

---

## Conclusion

Erlang's hot code swapping feature is a powerful tool for building **high-availability, fault-tolerant systems** where updates must happen without downtime or disruption.

---

## Further Reading

- [Erlang Hot Code Loading Guide](https://erlang.org/doc/tutorial/code_loading.html)
- [Understanding Erlang Releases and Upgrades](https://erlang.org/doc/design_principles/release_handling.html)

---

*Created by Your Name*

