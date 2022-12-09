# Salt And Pepper in Hashing & Passwords

Aim is to prevent rainbow/dictionary attacks.

Idea is to make same plain-text passwords have different hashes. Therefore achieving improved security.

> "But wait there has to be a mistakee, I was told hashed are one-way. It cannot be reversed, nooooo !"

Yeah but famous hash algorithms has gigantic databases of (unsalted) dictionaries, so it is not hard to find actual value for common inputs. There are websites and datasets for these

## Salt

- Is not mandatory to be top secret. But better if it is secret.
  - Because if salts are obtained, they can just generate rainbow table or dictionary according to it
- Random
- Unique
- Dynamic, may change and may be re-generated

## Pepper
- Not unique per data object (e.g: common for all users)
- Static value
- Should be stored in a different medium than salt (e.g: don't store this in DB because salt is stored in DB).
  
### How to apply

Most common example: for passwords.

1. Generate random, fixed-length, unique string for each user
2. Store these salts next to the password column. New column 'salt'.
3. Password hash function (pseudo):

**You can either append or prepend the salt to the plaintext password before hashing.**
```

preparePasswordHash(plaintextPassword,salt){
concatted=salt+plaintextPassword;
return Hash(concatted);
}
//As you can guess, without salt, this function was just Hash(plaintextPassword);
```

Before salting, the plaintext password "test" would result in this has (md5): `098f6bcd4621d373cade4e832627b4f6`

But after salting, the plaintext password "test" with the salt "thisismysalt" prepended, this hash (md5) would be produced: `5b146ac6e50cecdac1c9cc2e1f01366c`


3. When password changes for a user, prepare the new hash with the `preparePasswordHash()` passing the new plaintext password and the salt
4. When login is attempted: call the `preparePasswordHash()` with input password and the corresponding user's salt, and compare the hash with the user's password hash

- Some hash functions have parameter for it, allowing you to pass your salt directly to it
