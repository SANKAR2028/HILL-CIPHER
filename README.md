
# HILL CIPHER
# EX. NO: 3 AIM:
 
```
NAME: SANKAR
DEPT: B.E/CSE
REG NO: 212224040291
```

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
import numpy as np

# A 2x2 key matrix for encryption
K = np.array([[3, 3], [2, 5]])

def mod_inverse(a, m):
    """
    Calculates the modular multiplicative inverse of a under modulo m.
    """
    for x in range(1, m):
        if (a * x) % m == 1:
            return x
    return -1

def matrix_inverse(M):
    """
    Calculates the modular inverse of a 2x2 matrix M.
    """
    det = int(np.round(np.linalg.det(M))) % 26
    if det < 0:
        det += 26
    
    det_inv = mod_inverse(det, 26)
    if det_inv == -1:
        raise ValueError("Key matrix is not invertible.")
    
    adjugate = np.array([[M[1, 1], -M[0, 1]], [-M[1, 0], M[0, 0]]])
    
    inv_matrix = (adjugate * det_inv) % 26
    
    # Handle negative values
    inv_matrix[inv_matrix < 0] += 26
    
    return inv_matrix

def hill_cipher(text, encrypt=True):
    """
    Encrypts or decrypts a message using the Hill cipher.
    """
    text = text.upper()
    
    # Pad the text if its length is not a multiple of 2
    if len(text) % 2 != 0:
        text += 'X'
        
    len_text = len(text)
    
    # Determine the matrix to use (key or inverse key)
    if encrypt:
        KM = K
    else:
        KM = matrix_inverse(K)
        
    result = []
    
    # Process the text in blocks of 2
    for i in range(0, len_text, 2):
        block = text[i:i+2]
        
        # Convert characters to numerical vectors
        vector = np.array([ord(c) - ord('A') for c in block])
        
        # Perform matrix multiplication and modulo 26
        transformed_vector = np.dot(KM, vector) % 26
        
        # Convert numerical vector back to characters
        result.extend([chr(val + ord('A')) for val in transformed_vector])
        
    return "".join(result)

# --- Main Program ---
if __name__ == "__main__":
    msg = "SANKAR"
    
    encrypted_text = hill_cipher(msg, encrypt=True)
    print("Encrypted:", encrypted_text)
    
    decrypted_text = hill_cipher(encrypted_text, encrypt=False)
    print("Decrypted:", decrypted_text)
```



## OUTPUT

<img width="1489" height="661" alt="image" src="https://github.com/user-attachments/assets/9ca9bc86-2bc4-4a1d-b999-7073df57f526" />

## RESULT

The program is executed successfully
