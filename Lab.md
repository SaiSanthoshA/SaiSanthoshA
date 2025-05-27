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
