# dominik-zareba-bsk-umcs

#ZAD1 (bez zastosowania serwera - symulacja)

```
# simulate_md5.py
import hashlib, json
session_id = "abc123"
word = "randomword"
print("Server ->", {"session_id": session_id, "word": word})
h = hashlib.md5(word.encode()).hexdigest()
print("Client computed MD5:", h)
print("Client -> submit JSON:", json.dumps({"session_id": session_id, "hash": h}))
```
