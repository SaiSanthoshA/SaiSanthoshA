1.import rsa
import hashlib

# 1. Generate RSA keys
public_key, private_key = rsa.newkeys(2048)

# 2. Create message
message = b"Hello from Tani Sparkle!"

# 3. Hash the message
hash_value = hashlib.sha256(message).digest()

# 4. Sign the hash using private key
signature = rsa.sign(message, private_key, 'SHA-256')

# 5. Verify signature
try:
    rsa.verify(message, signature, public_key)
    print("Signature Verified: Message is authentic.")
except rsa.VerificationError:
    print("Verification Failed: Message may be tampered.")



13. from cryptography.fernet import Fernet

# 1. Generate a key
key = Fernet.generate_key()
cipher = Fernet(key)

# 2. Message to encrypt
message = b"Hello Tani Sparkle!"

# 3. Encrypt the message
encrypted = cipher.encrypt(message)

# 4. Decrypt the message
decrypted = cipher.decrypt(encrypted)

# 5. Print results
print("Key:", key)
print("Encrypted:", encrypted)
print("Decrypted:", decrypted)
