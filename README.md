# dominik-zareba-bsk-umcs

# ZAD1 (bez zastosowania serwera - symulacja) oraz wersja z serwerem

## bez serwera
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

## z serwerem
1. uruchamiamy kontener

```
docker run -p 10001:10001 mazurkatarzyna/hashing-md5-ex1:latest
```

2. Pobieramy od serwera słowo

```
curl http://127.0.0.1:10001/hash
# otrzymasz JSON np. {"session_id":"abc123","word":"randomword"}
```

3. Obliczamy MD5 słowa używając OpenSSL

```
echo -n 'randomword' | openssl dgst -md5
# lub: echo -n 'randomword' | openssl md5
# wynik: (stdin)= 5eb63bbbe01eeed093cb22bb8f5acdc3  -> hex
```

4. Wysyłamy na serwer odpowiedź w json-ie

```
curl -X POST http://127.0.0.1:10001/submit \
  -H "Content-Type: application/json" \
  -d '{"session_id":"abc123","hash":"5eb63bbbe01eeed093cb22bb8f5acdc3"}'
```

==MD5==
: algorytm kryptograficzny, który z dowolnego długości słowa generuje 128-bitowy skrót.
