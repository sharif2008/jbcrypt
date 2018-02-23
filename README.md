# What is jbcrypt
In PHP  password_hash() creates a new password hash using a strong one-way hashing algorithm. password_hash() is compatible with crypt(). Therefore, password hashes created by crypt() can be used with password_hash().

The following algorithms are currently supported:

    PASSWORD_DEFAULT - Use the bcrypt algorithm (default as of PHP 5.5.0). Note that this constant is designed to change over time as new and stronger algorithms are added to PHP. For that reason, the length of the result from using this identifier can change over time. Therefore, it is recommended to store the result in a database column that can expand beyond 60 characters (255 characters would be a good choice).
    PASSWORD_BCRYPT - Use the CRYPT_BLOWFISH algorithm to create the hash. This will produce a standard crypt() compatible hash using the "$2y$" identifier. 
    
   
    CRYPT_MD5 - MD5 hashing with a twelve character salt starting with $1$.
    
    CRYPT_BLOWFISH - Blowfish hashing with a salt as follows: "$2a$", "$2x$" or "$2y$", a two digit cost parameter, "$", and 22 characters from the alphabet "./0-9A-Za-z". Using characters outside of this range in the salt will cause crypt() to return a zero-length string. The two digit cost parameter is the base-2 logarithm of the iteration count for the underlying Blowfish-based hashing algorithmeter and must be in range 04-31, values outside this range will cause crypt() to fail. Versions of PHP before 5.3.7 only support "$2a$" as the salt prefix: PHP 5.3.7 introduced the new prefixes to fix a security weakness in the Blowfish implementation. Please refer to » this document for full details of the security fix, but to summarise, developers targeting only PHP 5.3.7 and later should use "$2y$" in preference to "$2a$". 
    
    CRYPT_SHA256 - SHA-256 hash with a sixteen character salt prefixed with $5$. If the salt string starts with 'rounds=<N>$', the numeric value of N is used to indicate how many times the hashing loop should be executed, much like the cost parameter on Blowfish. The default number of rounds is 5000, there is a minimum of 1000 and a maximum of 999,999,999. Any selection of N outside this range will be truncated to the nearest limit.
    
    So to check against php generated hash with indentifier "$2y$" this library is easily compatiable.
    
jBCrypt is an implementation the OpenBSD Blowfish password hashing algorithm, as described in "A Future-Adaptable Password Scheme" by NielsProvos and David Mazieres: http://www.openbsd.org/papers/bcrypt-paper.ps

This system hashes passwords using a version of Bruce Schneier's  Blowfish block cipher with modifications designed to raise the cost of off-line password cracking. The computation cost of the algorithm is parameterised, so it can be increased as computers get faster.

## How to use
A simple example that demonstrates most of the features:

	// Hash a password for the first time
	String hashed = BCrypt.hashpw(password, BCrypt.gensalt());

	// gensalt's log_rounds parameter determines the complexity
	// the work factor is 2**log_rounds, and the default is 10
	String hashed = BCrypt.hashpw(password, BCrypt.gensalt(12));

	// Check that an unencrypted password matches one that has
	// previously been hashed
	if (BCrypt.checkpw(candidate, hashed))
		System.out.println("It matches");
	else
		System.out.println("It does not match");
 
 
## Licence
jBCrypt is licensed under a ISC/BSD licence. See the LICENSE file for details. http://www.mindrot.org/files/jBCrypt/LICENSE


