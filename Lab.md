14.import rsa
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

output:Signature Verified: Message is authentic.


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

output:Key: b'vJ1uC8rMEvM5Xo...'
Encrypted: b'gAAAAABlY...'
Decrypted: b'Hello Tani Sparkle!'


14.from cryptography import x509
from cryptography.x509.oid import NameOID
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.asymmetric import rsa, padding
from datetime import datetime, timedelta

# 1. Generate keys
private_key = rsa.generate_private_key(public_exponent=65537, key_size=2048)
public_key = private_key.public_key()

# 2. Create a simple self-signed certificate
name = x509.Name([
    x509.NameAttribute(NameOID.COMMON_NAME, "Tani Sparkle"),
])
certificate = x509.CertificateBuilder()\
    .subject_name(name)\
    .issuer_name(name)\
    .public_key(public_key)\
    .serial_number(x509.random_serial_number())\
    .not_valid_before(datetime.utcnow())\
    .not_valid_after(datetime.utcnow() + timedelta(days=365))\
    .sign(private_key, hashes.SHA256())

# 3. Sign a message (Digital Signature)
message = b"Hello from Tani Sparkle!"
signature = private_key.sign(message, padding.PKCS1v15(), hashes.SHA256())

# 4. Verify the signature using public key from certificate
try:
    certificate.public_key().verify(signature, message, padding.PKCS1v15(), hashes.SHA256())
    print("Signature is VALID and verified using the certificate.")
except:
    print("Signature is INVALID.")

output:Signature is VALID and verified using the certificate.
